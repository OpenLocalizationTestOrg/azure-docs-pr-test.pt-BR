---
title: "Azure Data Factory - Referência de Script do JSON | Microsoft Docs"
description: Oferece esquemas JSON para entidades do Data Factory.
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: 
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: 805106c0a5cdbff1f143f22a2ae59f6d2a0bf126
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="azure-data-factory---json-scripting-reference"></a><span data-ttu-id="8b587-103">Azure Data Factory - Referência de Script do JSON</span><span class="sxs-lookup"><span data-stu-id="8b587-103">Azure Data Factory - JSON Scripting Reference</span></span>
<span data-ttu-id="8b587-104">Este artigo fornece esquemas JSON e exemplos para definir entidades do Azure Data Factory (pipeline, atividade, conjunto de dados e serviço vinculado).</span><span class="sxs-lookup"><span data-stu-id="8b587-104">This article provides JSON schemas and examples for defining Azure Data Factory entities (pipeline, activity, dataset, and linked service).</span></span>  

## <a name="pipeline"></a><span data-ttu-id="8b587-105">Pipeline</span><span class="sxs-lookup"><span data-stu-id="8b587-105">Pipeline</span></span> 
<span data-ttu-id="8b587-106">A estrutura geral de uma definição de pipeline é a seguinte:</span><span class="sxs-lookup"><span data-stu-id="8b587-106">The high-level structure for a pipeline definition is as follows:</span></span> 

```json
{
  "name": "SamplePipeline",
  "properties": {
    "description": "Describe what pipeline does",
    "activities": [
    ],
    "start": "2016-07-12T00:00:00",
    "end": "2016-07-13T00:00:00"
  }
} 
```

<span data-ttu-id="8b587-107">A tabela a seguir descreve as propriedades na definição de JSON de pipeline:</span><span class="sxs-lookup"><span data-stu-id="8b587-107">Following table describes the properties within the pipeline JSON definition:</span></span>

| <span data-ttu-id="8b587-108">Propriedade</span><span class="sxs-lookup"><span data-stu-id="8b587-108">Property</span></span> | <span data-ttu-id="8b587-109">Descrição</span><span class="sxs-lookup"><span data-stu-id="8b587-109">Description</span></span> | <span data-ttu-id="8b587-110">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="8b587-110">Required</span></span>
-------- | ----------- | --------
| <span data-ttu-id="8b587-111">name</span><span class="sxs-lookup"><span data-stu-id="8b587-111">name</span></span> | <span data-ttu-id="8b587-112">Nome do pipeline.</span><span class="sxs-lookup"><span data-stu-id="8b587-112">Name of the pipeline.</span></span> <span data-ttu-id="8b587-113">Especifique um nome que representa a ação que a atividade ou o pipeline é configurado para executar</span><span class="sxs-lookup"><span data-stu-id="8b587-113">Specify a name that represents the action that the activity or pipeline is configured to do</span></span><br/><ul><li><span data-ttu-id="8b587-114">Número máximo de caracteres: 260</span><span class="sxs-lookup"><span data-stu-id="8b587-114">Maximum number of characters: 260</span></span></li><li><span data-ttu-id="8b587-115">Deve começar com uma letra, um número ou um sublinhado (_)</span><span class="sxs-lookup"><span data-stu-id="8b587-115">Must start with a letter number, or an underscore (_)</span></span></li><li><span data-ttu-id="8b587-116">Os seguintes caracteres não são permitidos: “.”, “+”, “?”, “/”, “<”,”>”,”*”,”%”,”&”,”:”,”\\”</span><span class="sxs-lookup"><span data-stu-id="8b587-116">Following characters are not allowed: “.”, “+”, “?”, “/”, “<”,”>”,”*”,”%”,”&”,”:”,”\\”</span></span></li></ul> |<span data-ttu-id="8b587-117">Sim</span><span class="sxs-lookup"><span data-stu-id="8b587-117">Yes</span></span> |
| <span data-ttu-id="8b587-118">Descrição</span><span class="sxs-lookup"><span data-stu-id="8b587-118">description</span></span> |<span data-ttu-id="8b587-119">Texto que descreve para que a atividade ou o pipeline é usado</span><span class="sxs-lookup"><span data-stu-id="8b587-119">Text describing what the activity or pipeline is used for</span></span> | <span data-ttu-id="8b587-120">Não</span><span class="sxs-lookup"><span data-stu-id="8b587-120">No</span></span> |
| <span data-ttu-id="8b587-121">atividades</span><span class="sxs-lookup"><span data-stu-id="8b587-121">activities</span></span> | <span data-ttu-id="8b587-122">Contém uma lista de atividades.</span><span class="sxs-lookup"><span data-stu-id="8b587-122">Contains a list of activities.</span></span> | <span data-ttu-id="8b587-123">Sim</span><span class="sxs-lookup"><span data-stu-id="8b587-123">Yes</span></span> |
| <span data-ttu-id="8b587-124">iniciar</span><span class="sxs-lookup"><span data-stu-id="8b587-124">start</span></span> |<span data-ttu-id="8b587-125">Data e hora de início para o pipeline.</span><span class="sxs-lookup"><span data-stu-id="8b587-125">Start date-time for the pipeline.</span></span> <span data-ttu-id="8b587-126">Deve estar no [formato ISO](http://en.wikipedia.org/wiki/ISO_8601).</span><span class="sxs-lookup"><span data-stu-id="8b587-126">Must be in [ISO format](http://en.wikipedia.org/wiki/ISO_8601).</span></span> <span data-ttu-id="8b587-127">Por exemplo: 2014-10-14T16:32:41.</span><span class="sxs-lookup"><span data-stu-id="8b587-127">For example: 2014-10-14T16:32:41.</span></span> <br/><br/><span data-ttu-id="8b587-128">É possível especificar uma hora local, por exemplo, EST.</span><span class="sxs-lookup"><span data-stu-id="8b587-128">It is possible to specify a local time, for example an EST time.</span></span> <span data-ttu-id="8b587-129">Aqui está um exemplo: `2016-02-27T06:00:00**-05:00`, que é 6 AM EST.</span><span class="sxs-lookup"><span data-stu-id="8b587-129">Here is an example: `2016-02-27T06:00:00**-05:00`, which is 6 AM EST.</span></span><br/><br/><span data-ttu-id="8b587-130">As propriedades de início e término especificam o período ativo para o pipeline.</span><span class="sxs-lookup"><span data-stu-id="8b587-130">The start and end properties together specify active period for the pipeline.</span></span> <span data-ttu-id="8b587-131">Fatias de saída são produzidas somente nesse período ativo.</span><span class="sxs-lookup"><span data-stu-id="8b587-131">Output slices are only produced with in this active period.</span></span> |<span data-ttu-id="8b587-132">Não</span><span class="sxs-lookup"><span data-stu-id="8b587-132">No</span></span><br/><br/><span data-ttu-id="8b587-133">Se você especificar um valor para a propriedade final, será necessário especificar um valor para a propriedade inicial.</span><span class="sxs-lookup"><span data-stu-id="8b587-133">If you specify a value for the end property, you must specify value for the start property.</span></span><br/><br/><span data-ttu-id="8b587-134">Os horários de início e fim podem estar vazios para criar um pipeline.</span><span class="sxs-lookup"><span data-stu-id="8b587-134">The start and end times can both be empty to create a pipeline.</span></span> <span data-ttu-id="8b587-135">Você deve especificar ambos os valores para definir um período ativo de execução do pipeline.</span><span class="sxs-lookup"><span data-stu-id="8b587-135">You must specify both values to set an active period for the pipeline to run.</span></span> <span data-ttu-id="8b587-136">Se não especificar os horários de início e fim ao criar um pipeline, você poderá defini-los depois usando o cmdlet Set-AzureRmDataFactoryPipelineActivePeriod.</span><span class="sxs-lookup"><span data-stu-id="8b587-136">If you do not specify start and end times when creating a pipeline, you can set them using the Set-AzureRmDataFactoryPipelineActivePeriod cmdlet later.</span></span> |
| <span data-ttu-id="8b587-137">end</span><span class="sxs-lookup"><span data-stu-id="8b587-137">end</span></span> |<span data-ttu-id="8b587-138">Data e hora de término para o pipeline.</span><span class="sxs-lookup"><span data-stu-id="8b587-138">End date-time for the pipeline.</span></span> <span data-ttu-id="8b587-139">Se especificado, deve estar no formato ISO.</span><span class="sxs-lookup"><span data-stu-id="8b587-139">If specified must be in ISO format.</span></span> <span data-ttu-id="8b587-140">Por exemplo: 2014-10-14T17:32:41.</span><span class="sxs-lookup"><span data-stu-id="8b587-140">For example: 2014-10-14T17:32:41</span></span> <br/><br/><span data-ttu-id="8b587-141">É possível especificar uma hora local, por exemplo, EST.</span><span class="sxs-lookup"><span data-stu-id="8b587-141">It is possible to specify a local time, for example an EST time.</span></span> <span data-ttu-id="8b587-142">Veja este exemplo: `2016-02-27T06:00:00**-05:00`, que é 6 AM EST.</span><span class="sxs-lookup"><span data-stu-id="8b587-142">Here is an example: `2016-02-27T06:00:00**-05:00`, which is 6 AM EST.</span></span><br/><br/><span data-ttu-id="8b587-143">Para executar o pipeline indefinidamente, especifique 9999-09-09 como o valor da propriedade end.</span><span class="sxs-lookup"><span data-stu-id="8b587-143">To run the pipeline indefinitely, specify 9999-09-09 as the value for the end property.</span></span> |<span data-ttu-id="8b587-144">Não</span><span class="sxs-lookup"><span data-stu-id="8b587-144">No</span></span> <br/><br/><span data-ttu-id="8b587-145">Se você especificar um valor para a propriedade inicial, será necessário especificar um valor para a propriedade final.</span><span class="sxs-lookup"><span data-stu-id="8b587-145">If you specify a value for the start property, you must specify value for the end property.</span></span><br/><br/><span data-ttu-id="8b587-146">Confira as observações para a propriedade **iniciar** .</span><span class="sxs-lookup"><span data-stu-id="8b587-146">See notes for the **start** property.</span></span> |
| <span data-ttu-id="8b587-147">isPaused</span><span class="sxs-lookup"><span data-stu-id="8b587-147">isPaused</span></span> |<span data-ttu-id="8b587-148">Se definido como verdadeiro, o pipeline não é executado.</span><span class="sxs-lookup"><span data-stu-id="8b587-148">If set to true the pipeline does not run.</span></span> <span data-ttu-id="8b587-149">Valor padrão = falso.</span><span class="sxs-lookup"><span data-stu-id="8b587-149">Default value = false.</span></span> <span data-ttu-id="8b587-150">Você pode usar essa propriedade para habilitar ou desabilitar.</span><span class="sxs-lookup"><span data-stu-id="8b587-150">You can use this property to enable or disable.</span></span> |<span data-ttu-id="8b587-151">Não</span><span class="sxs-lookup"><span data-stu-id="8b587-151">No</span></span> |
| <span data-ttu-id="8b587-152">pipelineMode</span><span class="sxs-lookup"><span data-stu-id="8b587-152">pipelineMode</span></span> |<span data-ttu-id="8b587-153">O método de agendamento é executado para o pipeline.</span><span class="sxs-lookup"><span data-stu-id="8b587-153">The method for scheduling runs for the pipeline.</span></span> <span data-ttu-id="8b587-154">Os valores permitidos são: scheduled (padrão), onetime.</span><span class="sxs-lookup"><span data-stu-id="8b587-154">Allowed values are: scheduled (default), onetime.</span></span><br/><br/><span data-ttu-id="8b587-155">'Scheduled' indica que o pipeline será executado em um intervalo de tempo especificado de acordo com seu período ativo (hora de início e término).</span><span class="sxs-lookup"><span data-stu-id="8b587-155">‘Scheduled’ indicates that the pipeline runs at a specified time interval according to its active period (start and end time).</span></span> <span data-ttu-id="8b587-156">“Onetime” indica que o pipeline é executado apenas uma vez.</span><span class="sxs-lookup"><span data-stu-id="8b587-156">‘Onetime’ indicates that the pipeline runs only once.</span></span> <span data-ttu-id="8b587-157">Pipelines Onetime não podem ser modificados e atualizados depois de criados atualmente.</span><span class="sxs-lookup"><span data-stu-id="8b587-157">Onetime pipelines once created cannot be modified/updated currently.</span></span> <span data-ttu-id="8b587-158">Confira [Pipeline avulso](data-factory-create-pipelines.md#onetime-pipeline) para obter detalhes sobre a configuração única.</span><span class="sxs-lookup"><span data-stu-id="8b587-158">See [Onetime pipeline](data-factory-create-pipelines.md#onetime-pipeline) for details about onetime setting.</span></span> |<span data-ttu-id="8b587-159">Não</span><span class="sxs-lookup"><span data-stu-id="8b587-159">No</span></span> |
| <span data-ttu-id="8b587-160">expirationTime</span><span class="sxs-lookup"><span data-stu-id="8b587-160">expirationTime</span></span> |<span data-ttu-id="8b587-161">Duração de tempo após a criação pela qual o pipeline é válido e deve permanecer provisionado.</span><span class="sxs-lookup"><span data-stu-id="8b587-161">Duration of time after creation for which the pipeline is valid and should remain provisioned.</span></span> <span data-ttu-id="8b587-162">Se não houver execuções ativas, com falha ou pendentes, o pipeline será excluído automaticamente depois de atingir o tempo de expiração.</span><span class="sxs-lookup"><span data-stu-id="8b587-162">If it does not have any active, failed, or pending runs, the pipeline is deleted automatically once it reaches the expiration time.</span></span> |<span data-ttu-id="8b587-163">Não</span><span class="sxs-lookup"><span data-stu-id="8b587-163">No</span></span> |


## <a name="activity"></a><span data-ttu-id="8b587-164">Atividade</span><span class="sxs-lookup"><span data-stu-id="8b587-164">Activity</span></span> 
<span data-ttu-id="8b587-165">A estrutura de alto nível de uma atividade dentro de uma definição de pipeline (elemento atividades) é a seguinte:</span><span class="sxs-lookup"><span data-stu-id="8b587-165">The high-level structure for an activity within a pipeline definition (activities element) is as follows:</span></span>

```json
{
    "name": "ActivityName",
    "description": "description", 
    "type": "<ActivityType>",
    "inputs":  "[]",
    "outputs":  "[]",
    "linkedServiceName": "MyLinkedService",
    "typeProperties":
    {

    },
    "policy":
    {
    }
    "scheduler":
    {
    }
}
```

<span data-ttu-id="8b587-166">A tabela a seguir descreve as propriedades na definição de JSON de atividade:</span><span class="sxs-lookup"><span data-stu-id="8b587-166">Following table describe the properties within the activity JSON definition:</span></span>

| <span data-ttu-id="8b587-167">Marca</span><span class="sxs-lookup"><span data-stu-id="8b587-167">Tag</span></span> | <span data-ttu-id="8b587-168">Descrição</span><span class="sxs-lookup"><span data-stu-id="8b587-168">Description</span></span> | <span data-ttu-id="8b587-169">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="8b587-169">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8b587-170">name</span><span class="sxs-lookup"><span data-stu-id="8b587-170">name</span></span> |<span data-ttu-id="8b587-171">Nome da atividade.</span><span class="sxs-lookup"><span data-stu-id="8b587-171">Name of the activity.</span></span> <span data-ttu-id="8b587-172">Especifique um nome que representa a ação que a atividade é configurada para executar</span><span class="sxs-lookup"><span data-stu-id="8b587-172">Specify a name that represents the action that the activity is configured to do</span></span><br/><ul><li><span data-ttu-id="8b587-173">Número máximo de caracteres: 260</span><span class="sxs-lookup"><span data-stu-id="8b587-173">Maximum number of characters: 260</span></span></li><li><span data-ttu-id="8b587-174">Deve começar com uma letra, um número ou um sublinhado (_)</span><span class="sxs-lookup"><span data-stu-id="8b587-174">Must start with a letter number, or an underscore (_)</span></span></li><li><span data-ttu-id="8b587-175">Os seguintes caracteres não são permitidos: “.”, “+”, “?”, “/”, “<”,”>”,”*”,”%”,”&”,”:”,”\\”</span><span class="sxs-lookup"><span data-stu-id="8b587-175">Following characters are not allowed: “.”, “+”, “?”, “/”, “<”,”>”,”*”,”%”,”&”,”:”,”\\”</span></span></li></ul> |<span data-ttu-id="8b587-176">Sim</span><span class="sxs-lookup"><span data-stu-id="8b587-176">Yes</span></span> |
| <span data-ttu-id="8b587-177">description</span><span class="sxs-lookup"><span data-stu-id="8b587-177">description</span></span> |<span data-ttu-id="8b587-178">Texto que descreve qual a utilidade da atividade.</span><span class="sxs-lookup"><span data-stu-id="8b587-178">Text describing what the activity is used for.</span></span> |<span data-ttu-id="8b587-179">Sim</span><span class="sxs-lookup"><span data-stu-id="8b587-179">Yes</span></span> |
| <span data-ttu-id="8b587-180">type</span><span class="sxs-lookup"><span data-stu-id="8b587-180">type</span></span> |<span data-ttu-id="8b587-181">Especifica o tipo da atividade.</span><span class="sxs-lookup"><span data-stu-id="8b587-181">Specifies the type of the activity.</span></span> <span data-ttu-id="8b587-182">Consulte as seções [ARMAZENAMENTOS DE DADOS](#data-stores) e [ATIVIDADES DE TRANSFORMAÇÃO DE DADOS](#data-transformation-activities) para obter diferentes tipos de atividade.</span><span class="sxs-lookup"><span data-stu-id="8b587-182">See the [DATA STORES](#data-stores) and [DATA TRANSFORMATION ACTIVITIES](#data-transformation-activities) sections for different types of activities.</span></span> |<span data-ttu-id="8b587-183">Sim</span><span class="sxs-lookup"><span data-stu-id="8b587-183">Yes</span></span> |
| <span data-ttu-id="8b587-184">inputs</span><span class="sxs-lookup"><span data-stu-id="8b587-184">inputs</span></span> |<span data-ttu-id="8b587-185">Tabelas de entrada utilizadas pela atividade</span><span class="sxs-lookup"><span data-stu-id="8b587-185">Input tables used by the activity</span></span><br/><br/>`// one input table`<br/>`"inputs":  [ { "name": "inputtable1"  } ],`<br/><br/>`// two input tables` <br/>`"inputs":  [ { "name": "inputtable1"  }, { "name": "inputtable2"  } ],` |<span data-ttu-id="8b587-186">Sim</span><span class="sxs-lookup"><span data-stu-id="8b587-186">Yes</span></span> |
| <span data-ttu-id="8b587-187">outputs</span><span class="sxs-lookup"><span data-stu-id="8b587-187">outputs</span></span> |<span data-ttu-id="8b587-188">Tabelas de saída utilizadas pela atividade.</span><span class="sxs-lookup"><span data-stu-id="8b587-188">Output tables used by the activity.</span></span><br/><br/>`// one output table`<br/>`"outputs":  [ { "name": “outputtable1” } ],`<br/><br/>`//two output tables`<br/>`"outputs":  [ { "name": “outputtable1” }, { "name": “outputtable2” }  ],` |<span data-ttu-id="8b587-189">Sim</span><span class="sxs-lookup"><span data-stu-id="8b587-189">Yes</span></span> |
| <span data-ttu-id="8b587-190">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="8b587-190">linkedServiceName</span></span> |<span data-ttu-id="8b587-191">Nome do serviço vinculado usado pela atividade.</span><span class="sxs-lookup"><span data-stu-id="8b587-191">Name of the linked service used by the activity.</span></span> <br/><br/><span data-ttu-id="8b587-192">Uma atividade pode exigir que você especifique o serviço vinculado que é vinculado ao ambiente de computação necessário.</span><span class="sxs-lookup"><span data-stu-id="8b587-192">An activity may require that you specify the linked service that links to the required compute environment.</span></span> |<span data-ttu-id="8b587-193">Sim para atividades de HDInsight, atividades de Azure Machine Learning e Atividade de Procedimento Armazenado.</span><span class="sxs-lookup"><span data-stu-id="8b587-193">Yes for HDInsight activities, Azure Machine Learning activities, and Stored Procedure Activity.</span></span> <br/><br/><span data-ttu-id="8b587-194">Não para todas as outros</span><span class="sxs-lookup"><span data-stu-id="8b587-194">No for all others</span></span> |
| <span data-ttu-id="8b587-195">typeProperties</span><span class="sxs-lookup"><span data-stu-id="8b587-195">typeProperties</span></span> |<span data-ttu-id="8b587-196">As propriedades na seção typeProperties dependem do tipo de atividade.</span><span class="sxs-lookup"><span data-stu-id="8b587-196">Properties in the typeProperties section depend on type of the activity.</span></span> |<span data-ttu-id="8b587-197">Não</span><span class="sxs-lookup"><span data-stu-id="8b587-197">No</span></span> |
| <span data-ttu-id="8b587-198">policy</span><span class="sxs-lookup"><span data-stu-id="8b587-198">policy</span></span> |<span data-ttu-id="8b587-199">Políticas que afetam o comportamento de tempo de execução da atividade.</span><span class="sxs-lookup"><span data-stu-id="8b587-199">Policies that affect the run-time behavior of the activity.</span></span> <span data-ttu-id="8b587-200">Se não for especificado, as políticas padrão serão utilizadas.</span><span class="sxs-lookup"><span data-stu-id="8b587-200">If it is not specified, default policies are used.</span></span> |<span data-ttu-id="8b587-201">Não</span><span class="sxs-lookup"><span data-stu-id="8b587-201">No</span></span> |
| <span data-ttu-id="8b587-202">agendador</span><span class="sxs-lookup"><span data-stu-id="8b587-202">scheduler</span></span> |<span data-ttu-id="8b587-203">A propriedade "scheduler" é usada para definir o agendamento desejado para a atividade.</span><span class="sxs-lookup"><span data-stu-id="8b587-203">“scheduler” property is used to define desired scheduling for the activity.</span></span> <span data-ttu-id="8b587-204">Suas sub-propriedades são aquelas na [propriedade de disponibilidade em um conjunto de dados](data-factory-create-datasets.md#dataset-availability).</span><span class="sxs-lookup"><span data-stu-id="8b587-204">Its subproperties are the same as the ones in the [availability property in a dataset](data-factory-create-datasets.md#dataset-availability).</span></span> |<span data-ttu-id="8b587-205">Não</span><span class="sxs-lookup"><span data-stu-id="8b587-205">No</span></span> |

### <a name="policies"></a><span data-ttu-id="8b587-206">Políticas</span><span class="sxs-lookup"><span data-stu-id="8b587-206">Policies</span></span>
<span data-ttu-id="8b587-207">As políticas afetam o comportamento de tempo de execução de uma atividade, especialmente quando a divisão de uma tabela é processada.</span><span class="sxs-lookup"><span data-stu-id="8b587-207">Policies affect the run-time behavior of an activity, specifically when the slice of a table is processed.</span></span> <span data-ttu-id="8b587-208">A tabela a seguir fornece os detalhes.</span><span class="sxs-lookup"><span data-stu-id="8b587-208">The following table provides the details.</span></span>

| <span data-ttu-id="8b587-209">Propriedade</span><span class="sxs-lookup"><span data-stu-id="8b587-209">Property</span></span> | <span data-ttu-id="8b587-210">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="8b587-210">Permitted values</span></span> | <span data-ttu-id="8b587-211">Valor Padrão</span><span class="sxs-lookup"><span data-stu-id="8b587-211">Default Value</span></span> | <span data-ttu-id="8b587-212">Descrição</span><span class="sxs-lookup"><span data-stu-id="8b587-212">Description</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="8b587-213">simultaneidade</span><span class="sxs-lookup"><span data-stu-id="8b587-213">concurrency</span></span> |<span data-ttu-id="8b587-214">Inteiro </span><span class="sxs-lookup"><span data-stu-id="8b587-214">Integer</span></span> <br/><br/><span data-ttu-id="8b587-215">Valor máximo: 10</span><span class="sxs-lookup"><span data-stu-id="8b587-215">Max value: 10</span></span> |<span data-ttu-id="8b587-216">1</span><span class="sxs-lookup"><span data-stu-id="8b587-216">1</span></span> |<span data-ttu-id="8b587-217">Número de execuções simultâneas da atividade.</span><span class="sxs-lookup"><span data-stu-id="8b587-217">Number of concurrent executions of the activity.</span></span><br/><br/><span data-ttu-id="8b587-218">Determina o número de execuções de atividade paralela que podem ocorrer em divisões diferentes.</span><span class="sxs-lookup"><span data-stu-id="8b587-218">It determines the number of parallel activity executions that can happen on different slices.</span></span> <span data-ttu-id="8b587-219">Por exemplo, se uma atividade precisa passar por um grande conjunto de dados disponíveis, ter um valor de concorrência maior acelera o processamento de dados.</span><span class="sxs-lookup"><span data-stu-id="8b587-219">For example, if an activity needs to go through a large set of available data, having a larger concurrency value speeds up the data processing.</span></span> |
| <span data-ttu-id="8b587-220">executionPriorityOrder</span><span class="sxs-lookup"><span data-stu-id="8b587-220">executionPriorityOrder</span></span> |<span data-ttu-id="8b587-221">NewestFirst</span><span class="sxs-lookup"><span data-stu-id="8b587-221">NewestFirst</span></span><br/><br/><span data-ttu-id="8b587-222">OldestFirst</span><span class="sxs-lookup"><span data-stu-id="8b587-222">OldestFirst</span></span> |<span data-ttu-id="8b587-223">OldestFirst</span><span class="sxs-lookup"><span data-stu-id="8b587-223">OldestFirst</span></span> |<span data-ttu-id="8b587-224">Determina a ordem das divisões de dados que estão sendo processadas.</span><span class="sxs-lookup"><span data-stu-id="8b587-224">Determines the ordering of data slices that are being processed.</span></span><br/><br/><span data-ttu-id="8b587-225">Por exemplo, se houver duas fatias (uma ocorre às 16h e a outra às 17h),e ambas estiverem com a execução pendente.</span><span class="sxs-lookup"><span data-stu-id="8b587-225">For example, if you have 2 slices (one happening at 4pm, and another one at 5pm), and both are pending execution.</span></span> <span data-ttu-id="8b587-226">Se você definir executionPriorityOrder como NewestFirst, a divisão às 17h será processada primeiro.</span><span class="sxs-lookup"><span data-stu-id="8b587-226">If you set the executionPriorityOrder to be NewestFirst, the slice at 5 PM is processed first.</span></span> <span data-ttu-id="8b587-227">De modo semelhante, se você definir executionPriorityORder como OldestFIrst, a fatia às 16h será processada.</span><span class="sxs-lookup"><span data-stu-id="8b587-227">Similarly if you set the executionPriorityORder to be OldestFIrst, then the slice at 4 PM is processed.</span></span> |
| <span data-ttu-id="8b587-228">tentar novamente</span><span class="sxs-lookup"><span data-stu-id="8b587-228">retry</span></span> |<span data-ttu-id="8b587-229">Número inteiro</span><span class="sxs-lookup"><span data-stu-id="8b587-229">Integer</span></span><br/><br/><span data-ttu-id="8b587-230">O valor máximo pode ser 10</span><span class="sxs-lookup"><span data-stu-id="8b587-230">Max value can be 10</span></span> |<span data-ttu-id="8b587-231">0</span><span class="sxs-lookup"><span data-stu-id="8b587-231">0</span></span> |<span data-ttu-id="8b587-232">Número de novas tentativas antes do processamento de dados da divisão ser marcado como Com falha.</span><span class="sxs-lookup"><span data-stu-id="8b587-232">Number of retries before the data processing for the slice is marked as Failure.</span></span> <span data-ttu-id="8b587-233">A execução da atividade para uma divisão de dados é repetida até a contagem de repetição especificada.</span><span class="sxs-lookup"><span data-stu-id="8b587-233">Activity execution for a data slice is retried up to the specified retry count.</span></span> <span data-ttu-id="8b587-234">A nova tentativa é feita logo após a falha.</span><span class="sxs-lookup"><span data-stu-id="8b587-234">The retry is done as soon as possible after the failure.</span></span> |
| <span data-ttu-id="8b587-235">Tempo limite</span><span class="sxs-lookup"><span data-stu-id="8b587-235">timeout</span></span> |<span data-ttu-id="8b587-236">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="8b587-236">TimeSpan</span></span> |<span data-ttu-id="8b587-237">00:00:00</span><span class="sxs-lookup"><span data-stu-id="8b587-237">00:00:00</span></span> |<span data-ttu-id="8b587-238">Tempo limite para a atividade.</span><span class="sxs-lookup"><span data-stu-id="8b587-238">Timeout for the activity.</span></span> <span data-ttu-id="8b587-239">Exemplo: 00:10:00 (implica o tempo limite de 10 minutos)</span><span class="sxs-lookup"><span data-stu-id="8b587-239">Example: 00:10:00 (implies timeout 10 mins)</span></span><br/><br/><span data-ttu-id="8b587-240">Se um valor não for especificado ou for 0, o tempo limite será infinito.</span><span class="sxs-lookup"><span data-stu-id="8b587-240">If a value is not specified or is 0, the timeout is infinite.</span></span><br/><br/><span data-ttu-id="8b587-241">Se o tempo de processamento de dados em uma divisão exceder o valor de tempo limite, ele será cancelado e o sistema tentará repetir o processamento.</span><span class="sxs-lookup"><span data-stu-id="8b587-241">If the data processing time on a slice exceeds the timeout value, it is canceled, and the system attempts to retry the processing.</span></span> <span data-ttu-id="8b587-242">O número de repetições depende da propriedade de repetição.</span><span class="sxs-lookup"><span data-stu-id="8b587-242">The number of retries depends on the retry property.</span></span> <span data-ttu-id="8b587-243">Quando atingir o tempo limite, o status será TimedOut.</span><span class="sxs-lookup"><span data-stu-id="8b587-243">When timeout occurs, the status is set to TimedOut.</span></span> |
| <span data-ttu-id="8b587-244">atrasar</span><span class="sxs-lookup"><span data-stu-id="8b587-244">delay</span></span> |<span data-ttu-id="8b587-245">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="8b587-245">TimeSpan</span></span> |<span data-ttu-id="8b587-246">00:00:00</span><span class="sxs-lookup"><span data-stu-id="8b587-246">00:00:00</span></span> |<span data-ttu-id="8b587-247">Especifique o atraso antes do processamento de dados da divisão começar.</span><span class="sxs-lookup"><span data-stu-id="8b587-247">Specify the delay before data processing of the slice starts.</span></span><br/><br/><span data-ttu-id="8b587-248">A execução da atividade de uma fatia de dados será iniciada após o atraso passar do tempo de execução esperado.</span><span class="sxs-lookup"><span data-stu-id="8b587-248">The execution of activity for a data slice is started after the Delay is past the expected execution time.</span></span><br/><br/><span data-ttu-id="8b587-249">Exemplo: 00:10:00 (implica um atraso de 10 minutos)</span><span class="sxs-lookup"><span data-stu-id="8b587-249">Example: 00:10:00 (implies delay of 10 mins)</span></span> |
| <span data-ttu-id="8b587-250">longRetry</span><span class="sxs-lookup"><span data-stu-id="8b587-250">longRetry</span></span> |<span data-ttu-id="8b587-251">Inteiro </span><span class="sxs-lookup"><span data-stu-id="8b587-251">Integer</span></span><br/><br/><span data-ttu-id="8b587-252">Valor máximo: 10</span><span class="sxs-lookup"><span data-stu-id="8b587-252">Max value: 10</span></span> |<span data-ttu-id="8b587-253">1</span><span class="sxs-lookup"><span data-stu-id="8b587-253">1</span></span> |<span data-ttu-id="8b587-254">O número de tentativas repetidas longas antes que a execução da divisão falhe.</span><span class="sxs-lookup"><span data-stu-id="8b587-254">The number of long retry attempts before the slice execution is failed.</span></span><br/><br/><span data-ttu-id="8b587-255">Tentativas de longRetry são espaçadas por longRetryInterval.</span><span class="sxs-lookup"><span data-stu-id="8b587-255">longRetry attempts are spaced by longRetryInterval.</span></span> <span data-ttu-id="8b587-256">Portanto, se você precisar especificar um tempo entre tentativas de repetição, use longRetry.</span><span class="sxs-lookup"><span data-stu-id="8b587-256">So if you need to specify a time between retry attempts, use longRetry.</span></span> <span data-ttu-id="8b587-257">Se Retry e longRetry forem especificados, cada tentativa de longRetry incluirá tentativas de Retry, e o número máximo de tentativas será Retry * longRetry.</span><span class="sxs-lookup"><span data-stu-id="8b587-257">If both Retry and longRetry are specified, each longRetry attempt includes Retry attempts and the max number of attempts is Retry * longRetry.</span></span><br/><br/><span data-ttu-id="8b587-258">Por exemplo, se tivermos as seguintes configurações na política de atividade:</span><span class="sxs-lookup"><span data-stu-id="8b587-258">For example, if we have the following settings in the activity policy:</span></span><br/><span data-ttu-id="8b587-259">Retry: 3</span><span class="sxs-lookup"><span data-stu-id="8b587-259">Retry: 3</span></span><br/><span data-ttu-id="8b587-260">longRetry: 2</span><span class="sxs-lookup"><span data-stu-id="8b587-260">longRetry: 2</span></span><br/><span data-ttu-id="8b587-261">longRetryInterval: 01:00:00</span><span class="sxs-lookup"><span data-stu-id="8b587-261">longRetryInterval: 01:00:00</span></span><br/><br/><span data-ttu-id="8b587-262">Presumindo que haja apenas uma fatia para execução (o status é Aguardando) e a execução da atividade sempre falhe.</span><span class="sxs-lookup"><span data-stu-id="8b587-262">Assume there is only one slice to execute (status is Waiting) and the activity execution fails every time.</span></span> <span data-ttu-id="8b587-263">Inicialmente haveria três tentativas consecutivas de execução.</span><span class="sxs-lookup"><span data-stu-id="8b587-263">Initially there would be 3 consecutive execution attempts.</span></span> <span data-ttu-id="8b587-264">Após cada tentativa, o status de divisão seria Retry.</span><span class="sxs-lookup"><span data-stu-id="8b587-264">After each attempt, the slice status would be Retry.</span></span> <span data-ttu-id="8b587-265">Depois das três primeiras tentativas, o status da divisão seria LongRetry.</span><span class="sxs-lookup"><span data-stu-id="8b587-265">After first 3 attempts are over, the slice status would be LongRetry.</span></span><br/><br/><span data-ttu-id="8b587-266">Depois de uma hora (ou seja, valor de longRetryInteval), deve haver outro conjunto de três tentativas consecutivas de execução.</span><span class="sxs-lookup"><span data-stu-id="8b587-266">After an hour (that is, longRetryInteval’s value), there would be another set of 3 consecutive execution attempts.</span></span> <span data-ttu-id="8b587-267">Depois disso, o status da divisão seria Com falha e não haveria nova tentativa.</span><span class="sxs-lookup"><span data-stu-id="8b587-267">After that, the slice status would be Failed and no more retries would be attempted.</span></span> <span data-ttu-id="8b587-268">Portanto, em geral, foram feitas seis tentativas.</span><span class="sxs-lookup"><span data-stu-id="8b587-268">Hence overall 6 attempts were made.</span></span><br/><br/><span data-ttu-id="8b587-269">Se qualquer execução for bem-sucedida, o status da fatia seria Ready e não haverá mais nenhuma tentativa.</span><span class="sxs-lookup"><span data-stu-id="8b587-269">If any execution succeeds, the slice status would be Ready and no more retries are attempted.</span></span><br/><br/><span data-ttu-id="8b587-270">longRetry pode ser usado em situações em que dados dependentes chegam em horários não determinísticos ou o ambiente geral está instável onde o processamento de dados ocorre.</span><span class="sxs-lookup"><span data-stu-id="8b587-270">longRetry may be used in situations where dependent data arrives at non-deterministic times or the overall environment is flaky under which data processing occurs.</span></span> <span data-ttu-id="8b587-271">Nesses casos, fazer novas tentativas uma após a outra pode não ajudar e fazer isso após um intervalo de tempo resulta na saída desejada.</span><span class="sxs-lookup"><span data-stu-id="8b587-271">In such cases, doing retries one after another may not help and doing so after an interval of time results in the desired output.</span></span><br/><br/><span data-ttu-id="8b587-272">Advertência: não defina valores altos para longRetry ou longRetryInterval.</span><span class="sxs-lookup"><span data-stu-id="8b587-272">Word of caution: do not set high values for longRetry or longRetryInterval.</span></span> <span data-ttu-id="8b587-273">Normalmente, os valores mais altos implicam outros problemas sistêmicos.</span><span class="sxs-lookup"><span data-stu-id="8b587-273">Typically, higher values imply other systemic issues.</span></span> |
| <span data-ttu-id="8b587-274">longRetryInterval</span><span class="sxs-lookup"><span data-stu-id="8b587-274">longRetryInterval</span></span> |<span data-ttu-id="8b587-275">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="8b587-275">TimeSpan</span></span> |<span data-ttu-id="8b587-276">00:00:00</span><span class="sxs-lookup"><span data-stu-id="8b587-276">00:00:00</span></span> |<span data-ttu-id="8b587-277">O intervalo entre tentativas de repetição longa</span><span class="sxs-lookup"><span data-stu-id="8b587-277">The delay between long retry attempts</span></span> |

### <a name="typeproperties-section"></a><span data-ttu-id="8b587-278">Seção typeProperties</span><span class="sxs-lookup"><span data-stu-id="8b587-278">typeProperties section</span></span>
<span data-ttu-id="8b587-279">A seção typeProperties é diferente para cada tipo de atividade.</span><span class="sxs-lookup"><span data-stu-id="8b587-279">The typeProperties section is different for each activity.</span></span> <span data-ttu-id="8b587-280">Atividades de transformação possuem apenas as propriedades de tipo.</span><span class="sxs-lookup"><span data-stu-id="8b587-280">Transformation activities have just the type properties.</span></span> <span data-ttu-id="8b587-281">Consulte [ATIVIDADES DE TRANSFORMAÇÃO DE DADOS](#data-transformation-activities) neste artigo para obter exemplos de JSON que definem atividades de transformação em um pipeline.</span><span class="sxs-lookup"><span data-stu-id="8b587-281">See [DATA TRANSFORMATION ACTIVITIES](#data-transformation-activities) section in this article for JSON samples that define transformation activities in a pipeline.</span></span> 

<span data-ttu-id="8b587-282">A **atividade de cópia** possui duas subseções na seção typeProperties: **fonte** e **coletor**.</span><span class="sxs-lookup"><span data-stu-id="8b587-282">**Copy activity** has two subsections in the typeProperties section: **source** and **sink**.</span></span> <span data-ttu-id="8b587-283">Consulte a seção [ARMAZENAMENTOS DE DADOS](#data-stores) neste artigo para exemplos de JSON que mostram como usar um armazenamento de dados como uma fonte e/ou coletor.</span><span class="sxs-lookup"><span data-stu-id="8b587-283">See [DATA STORES](#data-stores) section in this article for JSON samples that show how to use a data store as a source and/or sink.</span></span> 

### <a name="sample-copy-pipeline"></a><span data-ttu-id="8b587-284">Pipeline de cópia de exemplo</span><span class="sxs-lookup"><span data-stu-id="8b587-284">Sample copy pipeline</span></span>
<span data-ttu-id="8b587-285">No pipeline de exemplo a seguir, há uma atividade do tipo **Cópia** in the **atividades** .</span><span class="sxs-lookup"><span data-stu-id="8b587-285">In the following sample pipeline, there is one activity of type **Copy** in the **activities** section.</span></span> <span data-ttu-id="8b587-286">Neste exemplo, a [Atividade de cópia](data-factory-data-movement-activities.md) copia dados de um Armazenamento de Blobs do Azure para um banco de dados SQL do Azure.</span><span class="sxs-lookup"><span data-stu-id="8b587-286">In this sample, the [Copy activity](data-factory-data-movement-activities.md) copies data from an Azure Blob storage to an Azure SQL database.</span></span> 

```json
{
  "name": "CopyPipeline",
  "properties": {
    "description": "Copy data from a blob to Azure SQL table",
    "activities": [
      {
        "name": "CopyFromBlobToSQL",
        "type": "Copy",
        "inputs": [
          {
            "name": "InputDataset"
          }
        ],
        "outputs": [
          {
            "name": "OutputDataset"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "BlobSource"
          },
          "sink": {
            "type": "SqlSink",
            "writeBatchSize": 10000,
            "writeBatchTimeout": "60:00:00"
          }
        },
        "Policy": {
          "concurrency": 1,
          "executionPriorityOrder": "NewestFirst",
          "retry": 0,
          "timeout": "01:00:00"
        }
      }
    ],
    "start": "2016-07-12T00:00:00",
    "end": "2016-07-13T00:00:00"
  }
} 
```

<span data-ttu-id="8b587-287">Observe os seguintes pontos:</span><span class="sxs-lookup"><span data-stu-id="8b587-287">Note the following points:</span></span>

* <span data-ttu-id="8b587-288">Na seção de atividades, há apenas uma atividade cujo **tipo** é definido como **Copy**.</span><span class="sxs-lookup"><span data-stu-id="8b587-288">In the activities section, there is only one activity whose **type** is set to **Copy**.</span></span>
* <span data-ttu-id="8b587-289">A entrada da atividade é definida como **InputDataset** e a saída da atividade é definida como **OutputDataset**.</span><span class="sxs-lookup"><span data-stu-id="8b587-289">Input for the activity is set to **InputDataset** and output for the activity is set to **OutputDataset**.</span></span>
* <span data-ttu-id="8b587-290">Na seção **typeProperties**, **BlobSource** é especificado como o tipo de origem e **SqlSink** é especificado como o tipo de coletor.</span><span class="sxs-lookup"><span data-stu-id="8b587-290">In the **typeProperties** section, **BlobSource** is specified as the source type and **SqlSink** is specified as the sink type.</span></span>

<span data-ttu-id="8b587-291">Consulte a seção [ARMAZENAMENTOS DE DADOS](#data-stores) neste artigo para exemplos de JSON que mostram como usar um armazenamento de dados como uma fonte e/ou coletor.</span><span class="sxs-lookup"><span data-stu-id="8b587-291">See [DATA STORES](#data-stores) section in this article for JSON samples that show how to use a data store as a source and/or sink.</span></span>    

<span data-ttu-id="8b587-292">Para obter uma explicação completa da criação desse pipeline, confira [Tutorial: copiar dados de Armazenamento de Blobs para o Banco de Dados SQL](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="8b587-292">For a complete walkthrough of creating this pipeline, see [Tutorial: Copy data from Blob Storage to SQL Database](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span> 

### <a name="sample-transformation-pipeline"></a><span data-ttu-id="8b587-293">Pipeline de transformação de exemplo</span><span class="sxs-lookup"><span data-stu-id="8b587-293">Sample transformation pipeline</span></span>
<span data-ttu-id="8b587-294">No pipeline de exemplo a seguir, há uma atividade do tipo **HDInsightHive** in the **atividades** .</span><span class="sxs-lookup"><span data-stu-id="8b587-294">In the following sample pipeline, there is one activity of type **HDInsightHive** in the **activities** section.</span></span> <span data-ttu-id="8b587-295">Neste exemplo, a [atividade de Hive do HDInsight](data-factory-hive-activity.md) transforma os dados de um Armazenamento de Blobs do Azure executando um arquivo de script do Hive em um cluster Hadoop do HDInsight do Azure.</span><span class="sxs-lookup"><span data-stu-id="8b587-295">In this sample, the [HDInsight Hive activity](data-factory-hive-activity.md) transforms data from an Azure Blob storage by running a Hive script file on an Azure HDInsight Hadoop cluster.</span></span> 

```json
{
    "name": "TransformPipeline",
    "properties": {
        "description": "My first Azure Data Factory pipeline",
        "activities": [
            {
                "type": "HDInsightHive",
                "typeProperties": {
                    "scriptPath": "adfgetstarted/script/partitionweblogs.hql",
                    "scriptLinkedService": "AzureStorageLinkedService",
                    "defines": {
                        "inputtable": "wasb://adfgetstarted@<storageaccountname>.blob.core.windows.net/inputdata",
                        "partitionedtable": "wasb://adfgetstarted@<storageaccountname>.blob.core.windows.net/partitioneddata"
                    }
                },
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
                "policy": {
                    "concurrency": 1,
                    "retry": 3
                },
                "scheduler": {
                    "frequency": "Month",
                    "interval": 1
                },
                "name": "RunSampleHiveActivity",
                "linkedServiceName": "HDInsightOnDemandLinkedService"
            }
        ],
        "start": "2016-04-01T00:00:00",
        "end": "2016-04-02T00:00:00",
        "isPaused": false
    }
}
```

<span data-ttu-id="8b587-296">Observe os seguintes pontos:</span><span class="sxs-lookup"><span data-stu-id="8b587-296">Note the following points:</span></span> 

* <span data-ttu-id="8b587-297">Na seção de atividades, há apenas uma atividade cujo **tipo** é definido como **HDInsightHive**.</span><span class="sxs-lookup"><span data-stu-id="8b587-297">In the activities section, there is only one activity whose **type** is set to **HDInsightHive**.</span></span>
* <span data-ttu-id="8b587-298">O arquivo de script do Hive, **partitionweblogs.hql**, é armazenado na conta de armazenamento do Azure (especificada pelo scriptLinkedService chamado **AzureStorageLinkedService**) e na pasta **script** no contêiner **adfgetstarted**.</span><span class="sxs-lookup"><span data-stu-id="8b587-298">The Hive script file, **partitionweblogs.hql**, is stored in the Azure storage account (specified by the scriptLinkedService, called **AzureStorageLinkedService**), and in **script** folder in the container **adfgetstarted**.</span></span>
* <span data-ttu-id="8b587-299">A seção **defines`${hiveconf:partitionedtable}` é usada para especificar as configurações de tempo de execução passadas para o script do hive como valores de configuração de Hive (por exemplo,** , `${hiveconf:inputtable}`).</span><span class="sxs-lookup"><span data-stu-id="8b587-299">The **defines** section is used to specify the runtime settings that are passed to the hive script as Hive configuration values (e.g `${hiveconf:inputtable}`, `${hiveconf:partitionedtable}`).</span></span>

<span data-ttu-id="8b587-300">Consulte [ATIVIDADES DE TRANSFORMAÇÃO DE DADOS](#data-transformation-activities) neste artigo para obter exemplos de JSON que definem atividades de transformação em um pipeline.</span><span class="sxs-lookup"><span data-stu-id="8b587-300">See [DATA TRANSFORMATION ACTIVITIES](#data-transformation-activities) section in this article for JSON samples that define transformation activities in a pipeline.</span></span>

<span data-ttu-id="8b587-301">Para obter uma explicação completa da criação desse pipeline, confira [Tutorial: criar seu primeiro pipeline para processar dados usando o cluster Hadoop](data-factory-build-your-first-pipeline.md).</span><span class="sxs-lookup"><span data-stu-id="8b587-301">For a complete walkthrough of creating this pipeline, see [Tutorial: Build your first pipeline to process data using Hadoop cluster](data-factory-build-your-first-pipeline.md).</span></span> 

## <a name="linked-service"></a><span data-ttu-id="8b587-302">Serviço vinculado</span><span class="sxs-lookup"><span data-stu-id="8b587-302">Linked service</span></span>
<span data-ttu-id="8b587-303">A estrutura de alto nível de uma definição de um serviço vinculado é a seguinte:</span><span class="sxs-lookup"><span data-stu-id="8b587-303">The high-level structure for a linked service definition is as follows:</span></span>

```json
{
    "name": "<name of the linked service>",
    "properties": {
        "type": "<type of the linked service>",
        "typeProperties": {
        }
    }
}
```

<span data-ttu-id="8b587-304">A tabela a seguir descreve as propriedades na definição de JSON de atividade:</span><span class="sxs-lookup"><span data-stu-id="8b587-304">Following table describe the properties within the activity JSON definition:</span></span>

| <span data-ttu-id="8b587-305">Propriedade</span><span class="sxs-lookup"><span data-stu-id="8b587-305">Property</span></span> | <span data-ttu-id="8b587-306">Descrição</span><span class="sxs-lookup"><span data-stu-id="8b587-306">Description</span></span> | <span data-ttu-id="8b587-307">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="8b587-307">Required</span></span> |
| -------- | ----------- | -------- | 
| <span data-ttu-id="8b587-308">name</span><span class="sxs-lookup"><span data-stu-id="8b587-308">name</span></span> | <span data-ttu-id="8b587-309">Nome do serviço vinculado.</span><span class="sxs-lookup"><span data-stu-id="8b587-309">Name of the linked service.</span></span> | <span data-ttu-id="8b587-310">Sim</span><span class="sxs-lookup"><span data-stu-id="8b587-310">Yes</span></span> | 
| <span data-ttu-id="8b587-311">properties - type</span><span class="sxs-lookup"><span data-stu-id="8b587-311">properties - type</span></span> | <span data-ttu-id="8b587-312">Tipo de serviço vinculado.</span><span class="sxs-lookup"><span data-stu-id="8b587-312">Type of the linked service.</span></span> <span data-ttu-id="8b587-313">Por exemplo: Armazenamento do Azure, Banco de Dados SQL do Azure.</span><span class="sxs-lookup"><span data-stu-id="8b587-313">For example: Azure Storage, Azure SQL Database.</span></span> |
| <span data-ttu-id="8b587-314">typeProperties</span><span class="sxs-lookup"><span data-stu-id="8b587-314">typeProperties</span></span> | <span data-ttu-id="8b587-315">A seção typeProperties possui elementos que são diferentes para cada armazenamento de dados ou ambiente de computação.</span><span class="sxs-lookup"><span data-stu-id="8b587-315">The typeProperties section has elements that are different for each data store or compute environment.</span></span> <span data-ttu-id="8b587-316">Consulte a seção [armazenamentos de dados](#datastores) para saber sobre todos os serviços vinculados de repositório de dados e [ambientes de computação](#compute-environments) para os serviços vinculados à computação</span><span class="sxs-lookup"><span data-stu-id="8b587-316">See [data stores](#datastores) section for all the data store linked services and [compute environments](#compute-environments) for all the compute linked services</span></span> |   

## <a name="dataset"></a><span data-ttu-id="8b587-317">Conjunto de dados</span><span class="sxs-lookup"><span data-stu-id="8b587-317">Dataset</span></span> 
<span data-ttu-id="8b587-318">Um conjunto de dados no Azure Data Factory é definido da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="8b587-318">A dataset in Azure Data Factory is defined as follows:</span></span>

```json
{
    "name": "<name of dataset>",
    "properties": {
        "type": "<type of dataset: AzureBlob, AzureSql etc...>",
        "external": <boolean flag to indicate external data. only for input datasets>,
        "linkedServiceName": "<Name of the linked service that refers to a data store.>",
        "structure": [
            {
                "name": "<Name of the column>",
                "type": "<Name of the type>"
            }
        ],
        "typeProperties": {
            "<type specific property>": "<value>",
            "<type specific property 2>": "<value 2>",
        },
        "availability": {
            "frequency": "<Specifies the time unit for data slice production. Supported frequency: Minute, Hour, Day, Week, Month>",
            "interval": "<Specifies the interval within the defined frequency. For example, frequency set to 'Hour' and interval set to 1 indicates that new data slices should be produced hourly>"
        },
       "policy":
        {      
        }
    }
}
```

<span data-ttu-id="8b587-319">A tabela a seguir descreve as propriedades no JSON acima:</span><span class="sxs-lookup"><span data-stu-id="8b587-319">The following table describes properties in the above JSON:</span></span>   

| <span data-ttu-id="8b587-320">Propriedade</span><span class="sxs-lookup"><span data-stu-id="8b587-320">Property</span></span> | <span data-ttu-id="8b587-321">Descrição</span><span class="sxs-lookup"><span data-stu-id="8b587-321">Description</span></span> | <span data-ttu-id="8b587-322">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="8b587-322">Required</span></span> | <span data-ttu-id="8b587-323">Padrão</span><span class="sxs-lookup"><span data-stu-id="8b587-323">Default</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="8b587-324">name</span><span class="sxs-lookup"><span data-stu-id="8b587-324">name</span></span> | <span data-ttu-id="8b587-325">Nome do conjunto de dados.</span><span class="sxs-lookup"><span data-stu-id="8b587-325">Name of the dataset.</span></span> <span data-ttu-id="8b587-326">Confira [Azure Data Factory - Regras de nomenclatura](data-factory-naming-rules.md) para ver as regras de nomenclatura.</span><span class="sxs-lookup"><span data-stu-id="8b587-326">See [Azure Data Factory - Naming rules](data-factory-naming-rules.md) for naming rules.</span></span> |<span data-ttu-id="8b587-327">Sim</span><span class="sxs-lookup"><span data-stu-id="8b587-327">Yes</span></span> |<span data-ttu-id="8b587-328">ND</span><span class="sxs-lookup"><span data-stu-id="8b587-328">NA</span></span> |
| <span data-ttu-id="8b587-329">type</span><span class="sxs-lookup"><span data-stu-id="8b587-329">type</span></span> | <span data-ttu-id="8b587-330">Tipo de conjunto de dados.</span><span class="sxs-lookup"><span data-stu-id="8b587-330">Type of the dataset.</span></span> <span data-ttu-id="8b587-331">Especifique um dos tipos com suporte no Azure Data Factory (por exemplo: AzureBlob, AzureSqlTable).</span><span class="sxs-lookup"><span data-stu-id="8b587-331">Specify one of the types supported by Azure Data Factory (for example: AzureBlob, AzureSqlTable).</span></span> <span data-ttu-id="8b587-332">Consulte a seção [ARMAZENAMENTOS DE DADOS](#data-stores) para saber sobre todos os tipos de conjunto de dados e armazenamento de dados com suporte da data factory.</span><span class="sxs-lookup"><span data-stu-id="8b587-332">See [DATA STORES](#data-stores) section for all the data stores and dataset types supported by Data Factory.</span></span> | 
| <span data-ttu-id="8b587-333">estrutura</span><span class="sxs-lookup"><span data-stu-id="8b587-333">structure</span></span> | <span data-ttu-id="8b587-334">Esquema do conjunto de dados.</span><span class="sxs-lookup"><span data-stu-id="8b587-334">Schema of the dataset.</span></span> <span data-ttu-id="8b587-335">Ela contém colunas, seus tipos, etc.</span><span class="sxs-lookup"><span data-stu-id="8b587-335">It contains columns, their types, etc.</span></span> | <span data-ttu-id="8b587-336">Não</span><span class="sxs-lookup"><span data-stu-id="8b587-336">No</span></span> |<span data-ttu-id="8b587-337">ND</span><span class="sxs-lookup"><span data-stu-id="8b587-337">NA</span></span> |
| <span data-ttu-id="8b587-338">typeProperties</span><span class="sxs-lookup"><span data-stu-id="8b587-338">typeProperties</span></span> | <span data-ttu-id="8b587-339">Propriedades que correspondem ao tipo selecionado.</span><span class="sxs-lookup"><span data-stu-id="8b587-339">Properties corresponding to the selected type.</span></span> <span data-ttu-id="8b587-340">Consulte a seção [ARMAZENAMENTOS DE DADOS](#data-stores) para saber quais são os tipos com suporte e suas propriedades.</span><span class="sxs-lookup"><span data-stu-id="8b587-340">See [DATA STORES](#data-stores) section for supported types and their properties.</span></span> |<span data-ttu-id="8b587-341">Sim</span><span class="sxs-lookup"><span data-stu-id="8b587-341">Yes</span></span> |<span data-ttu-id="8b587-342">ND</span><span class="sxs-lookup"><span data-stu-id="8b587-342">NA</span></span> |
| <span data-ttu-id="8b587-343">externo</span><span class="sxs-lookup"><span data-stu-id="8b587-343">external</span></span> | <span data-ttu-id="8b587-344">Sinalizador booliano para especificar se um conjunto de dados é explicitamente produzido por um pipeline de data factory ou não.</span><span class="sxs-lookup"><span data-stu-id="8b587-344">Boolean flag to specify whether a dataset is explicitly produced by a data factory pipeline or not.</span></span> |<span data-ttu-id="8b587-345">Não</span><span class="sxs-lookup"><span data-stu-id="8b587-345">No</span></span> |<span data-ttu-id="8b587-346">false</span><span class="sxs-lookup"><span data-stu-id="8b587-346">false</span></span> |
| <span data-ttu-id="8b587-347">disponibilidade</span><span class="sxs-lookup"><span data-stu-id="8b587-347">availability</span></span> | <span data-ttu-id="8b587-348">Define a janela de processamento ou o modelo de fatiamento para a produção de conjunto de dados.</span><span class="sxs-lookup"><span data-stu-id="8b587-348">Defines the processing window or the slicing model for the dataset production.</span></span> <span data-ttu-id="8b587-349">Para obter detalhes sobre o modelo de divisão do conjunto de dados, consulte o artigo [Agendamento e Execução](data-factory-scheduling-and-execution.md) .</span><span class="sxs-lookup"><span data-stu-id="8b587-349">For details on the dataset slicing model, see [Scheduling and Execution](data-factory-scheduling-and-execution.md) article.</span></span> |<span data-ttu-id="8b587-350">Sim</span><span class="sxs-lookup"><span data-stu-id="8b587-350">Yes</span></span> |<span data-ttu-id="8b587-351">ND</span><span class="sxs-lookup"><span data-stu-id="8b587-351">NA</span></span> |
| <span data-ttu-id="8b587-352">policy</span><span class="sxs-lookup"><span data-stu-id="8b587-352">policy</span></span> |<span data-ttu-id="8b587-353">Define os critérios ou a condição que as fatias de conjunto de dados devem atender.</span><span class="sxs-lookup"><span data-stu-id="8b587-353">Defines the criteria or the condition that the dataset slices must fulfill.</span></span> <br/><br/><span data-ttu-id="8b587-354">Para obter detalhes, consulte a seção [Política do Conjunto de Dados](#Policy) .</span><span class="sxs-lookup"><span data-stu-id="8b587-354">For details, see [Dataset Policy](#Policy) section.</span></span> |<span data-ttu-id="8b587-355">Não</span><span class="sxs-lookup"><span data-stu-id="8b587-355">No</span></span> |<span data-ttu-id="8b587-356">ND</span><span class="sxs-lookup"><span data-stu-id="8b587-356">NA</span></span> |

<span data-ttu-id="8b587-357">Cada coluna na seção **structure** contém as seguintes propriedades:</span><span class="sxs-lookup"><span data-stu-id="8b587-357">Each column in the **structure** section contains the following properties:</span></span>

| <span data-ttu-id="8b587-358">Propriedade</span><span class="sxs-lookup"><span data-stu-id="8b587-358">Property</span></span> | <span data-ttu-id="8b587-359">Descrição</span><span class="sxs-lookup"><span data-stu-id="8b587-359">Description</span></span> | <span data-ttu-id="8b587-360">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="8b587-360">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8b587-361">name</span><span class="sxs-lookup"><span data-stu-id="8b587-361">name</span></span> |<span data-ttu-id="8b587-362">Nome da coluna.</span><span class="sxs-lookup"><span data-stu-id="8b587-362">Name of the column.</span></span> |<span data-ttu-id="8b587-363">Sim</span><span class="sxs-lookup"><span data-stu-id="8b587-363">Yes</span></span> |
| <span data-ttu-id="8b587-364">type</span><span class="sxs-lookup"><span data-stu-id="8b587-364">type</span></span> |<span data-ttu-id="8b587-365">Tipo de dados da coluna.</span><span class="sxs-lookup"><span data-stu-id="8b587-365">Data type of the column.</span></span>  |<span data-ttu-id="8b587-366">Não</span><span class="sxs-lookup"><span data-stu-id="8b587-366">No</span></span> |
| <span data-ttu-id="8b587-367">culture</span><span class="sxs-lookup"><span data-stu-id="8b587-367">culture</span></span> |<span data-ttu-id="8b587-368">Cultura baseada em .NET a ser usada quando o tipo é especificado e é o tipo .NET `Datetime` ou `Datetimeoffset`.</span><span class="sxs-lookup"><span data-stu-id="8b587-368">.NET based culture to be used when type is specified and is .NET type `Datetime` or `Datetimeoffset`.</span></span> <span data-ttu-id="8b587-369">O padrão é `en-us`.</span><span class="sxs-lookup"><span data-stu-id="8b587-369">Default is `en-us`.</span></span> |<span data-ttu-id="8b587-370">Não</span><span class="sxs-lookup"><span data-stu-id="8b587-370">No</span></span> |
| <span data-ttu-id="8b587-371">formato</span><span class="sxs-lookup"><span data-stu-id="8b587-371">format</span></span> |<span data-ttu-id="8b587-372">O formato de cadeia de caracteres a ser usado quando o tipo é especificado e é o tipo .NET `Datetime` ou `Datetimeoffset`.</span><span class="sxs-lookup"><span data-stu-id="8b587-372">Format string to be used when type is specified and is .NET type `Datetime` or `Datetimeoffset`.</span></span> |<span data-ttu-id="8b587-373">Não</span><span class="sxs-lookup"><span data-stu-id="8b587-373">No</span></span> |

<span data-ttu-id="8b587-374">No exemplo a seguir, o conjunto de dados tem três colunas: `slicetimestamp`, `projectname` e `pageviews`, sendo dos seguintes tipos: String, String e Decimal, respectivamente.</span><span class="sxs-lookup"><span data-stu-id="8b587-374">In the following example, the dataset has three columns `slicetimestamp`, `projectname`, and `pageviews` and they are of type: String, String, and Decimal respectively.</span></span>

```json
structure:  
[
    { "name": "slicetimestamp", "type": "String"},
    { "name": "projectname", "type": "String"},
    { "name": "pageviews", "type": "Decimal"}
]
```

<span data-ttu-id="8b587-375">A tabela a seguir descreve as propriedades que você pode usar na seção de **availability**:</span><span class="sxs-lookup"><span data-stu-id="8b587-375">The following table describes properties you can use in the **availability** section:</span></span>

| <span data-ttu-id="8b587-376">Propriedade</span><span class="sxs-lookup"><span data-stu-id="8b587-376">Property</span></span> | <span data-ttu-id="8b587-377">Descrição</span><span class="sxs-lookup"><span data-stu-id="8b587-377">Description</span></span> | <span data-ttu-id="8b587-378">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="8b587-378">Required</span></span> | <span data-ttu-id="8b587-379">Padrão</span><span class="sxs-lookup"><span data-stu-id="8b587-379">Default</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="8b587-380">frequência</span><span class="sxs-lookup"><span data-stu-id="8b587-380">frequency</span></span> |<span data-ttu-id="8b587-381">Especifica a unidade de tempo para a produção da fatia de conjunto de dados.</span><span class="sxs-lookup"><span data-stu-id="8b587-381">Specifies the time unit for dataset slice production.</span></span><br/><br/><span data-ttu-id="8b587-382"><b>Frequência com suporte</b>: Minuto, Hora, Dia, Semana, Mês</span><span class="sxs-lookup"><span data-stu-id="8b587-382"><b>Supported frequency</b>: Minute, Hour, Day, Week, Month</span></span> |<span data-ttu-id="8b587-383">Sim</span><span class="sxs-lookup"><span data-stu-id="8b587-383">Yes</span></span> |<span data-ttu-id="8b587-384">ND</span><span class="sxs-lookup"><span data-stu-id="8b587-384">NA</span></span> |
| <span data-ttu-id="8b587-385">intervalo</span><span class="sxs-lookup"><span data-stu-id="8b587-385">interval</span></span> |<span data-ttu-id="8b587-386">Especifica um multiplicador para frequência</span><span class="sxs-lookup"><span data-stu-id="8b587-386">Specifies a multiplier for frequency</span></span><br/><br/><span data-ttu-id="8b587-387">"Intervalo de frequência x" determina a frequência com que a fatia é produzida.</span><span class="sxs-lookup"><span data-stu-id="8b587-387">”Frequency x interval” determines how often the slice is produced.</span></span><br/><br/><span data-ttu-id="8b587-388">Se você precisa que o conjunto de dados seja dividido por hora, defina <b>Frequência</b> como <b>Hora</b> e <b>intervalo</b> como <b>1</b>.</span><span class="sxs-lookup"><span data-stu-id="8b587-388">If you need the dataset to be sliced on an hourly basis, you set <b>Frequency</b> to <b>Hour</b>, and <b>interval</b> to <b>1</b>.</span></span><br/><br/><span data-ttu-id="8b587-389"><b>Observação:</b>: caso você especifique a frequência como minuto, recomendamos que defina o intervalo como não inferior a 15</span><span class="sxs-lookup"><span data-stu-id="8b587-389"><b>Note</b>: If you specify Frequency as Minute, we recommend that you set the interval to no less than 15</span></span> |<span data-ttu-id="8b587-390">Sim</span><span class="sxs-lookup"><span data-stu-id="8b587-390">Yes</span></span> |<span data-ttu-id="8b587-391">ND</span><span class="sxs-lookup"><span data-stu-id="8b587-391">NA</span></span> |
| <span data-ttu-id="8b587-392">estilo</span><span class="sxs-lookup"><span data-stu-id="8b587-392">style</span></span> |<span data-ttu-id="8b587-393">Especifica se a fatia deve ser produzida no início/término do intervalo.</span><span class="sxs-lookup"><span data-stu-id="8b587-393">Specifies whether the slice should be produced at the start/end of the interval.</span></span><ul><li><span data-ttu-id="8b587-394">StartOfInterval</span><span class="sxs-lookup"><span data-stu-id="8b587-394">StartOfInterval</span></span></li><li><span data-ttu-id="8b587-395">EndOfInterval</span><span class="sxs-lookup"><span data-stu-id="8b587-395">EndOfInterval</span></span></li></ul><br/><br/><span data-ttu-id="8b587-396">Se a frequência for definida como Mês e o estilo como EndOfInterval, a fatia será produzida no último dia do mês.</span><span class="sxs-lookup"><span data-stu-id="8b587-396">If Frequency is set to Month and style is set to EndOfInterval, the slice is produced on the last day of month.</span></span> <span data-ttu-id="8b587-397">Se o estilo for definido como StartOfInterval, a fatia será produzida no primeiro dia do mês.</span><span class="sxs-lookup"><span data-stu-id="8b587-397">If the style is set to StartOfInterval, the slice is produced on the first day of month.</span></span><br/><br/><span data-ttu-id="8b587-398">Se a frequência for definida como Dia e o estilo como EndOfInterval, a fatia será produzida na última hora do dia.</span><span class="sxs-lookup"><span data-stu-id="8b587-398">If Frequency is set to Day and style is set to EndOfInterval, the slice is produced in the last hour of the day.</span></span><br/><br/><span data-ttu-id="8b587-399">Se a Frequência for definida como Hora e o estilo como EndOfInterval, a fatia será produzida ao final da hora.</span><span class="sxs-lookup"><span data-stu-id="8b587-399">If Frequency is set to Hour and style is set to EndOfInterval, the slice is produced at the end of the hour.</span></span> <span data-ttu-id="8b587-400">Por exemplo, para uma fatia de período 13h – 14h, a fatia é produzida às 14h.</span><span class="sxs-lookup"><span data-stu-id="8b587-400">For example, for a slice for 1 PM – 2 PM period, the slice is produced at 2 PM.</span></span> |<span data-ttu-id="8b587-401">Não</span><span class="sxs-lookup"><span data-stu-id="8b587-401">No</span></span> |<span data-ttu-id="8b587-402">EndOfInterval</span><span class="sxs-lookup"><span data-stu-id="8b587-402">EndOfInterval</span></span> |
| <span data-ttu-id="8b587-403">anchorDateTime</span><span class="sxs-lookup"><span data-stu-id="8b587-403">anchorDateTime</span></span> |<span data-ttu-id="8b587-404">Define a posição absoluta no tempo usada pelo agendador para computar limites de fatia do conjunto de dados.</span><span class="sxs-lookup"><span data-stu-id="8b587-404">Defines the absolute position in time used by scheduler to compute dataset slice boundaries.</span></span> <br/><br/><span data-ttu-id="8b587-405"><b>Observação:</b> se AnchorDateTime tiver partes de datas mais granulares do que a frequência, as partes mais granulares serão ignoradas.</span><span class="sxs-lookup"><span data-stu-id="8b587-405"><b>Note</b>: If the AnchorDateTime has date parts that are more granular than the frequency then the more granular parts are ignored.</span></span> <br/><br/><span data-ttu-id="8b587-406">Por exemplo, se o <b>intervalo</b> for <b>por hora</b> (frequência: hora e intervalo: 1) e o <b>AnchorDateTime</b> contiver <b>minutos e segundos</b>, as partes <b>minutos e segundos</b> do AnchorDateTime serão ignoradas.</span><span class="sxs-lookup"><span data-stu-id="8b587-406">For example, if the <b>interval</b> is <b>hourly</b> (frequency: hour and interval: 1) and the <b>AnchorDateTime</b> contains <b>minutes and seconds</b> then the <b>minutes and seconds</b> parts of the AnchorDateTime are ignored.</span></span> |<span data-ttu-id="8b587-407">Não</span><span class="sxs-lookup"><span data-stu-id="8b587-407">No</span></span> |<span data-ttu-id="8b587-408">01/01/0001</span><span class="sxs-lookup"><span data-stu-id="8b587-408">01/01/0001</span></span> |
| <span data-ttu-id="8b587-409">deslocamento</span><span class="sxs-lookup"><span data-stu-id="8b587-409">offset</span></span> |<span data-ttu-id="8b587-410">O período de tempo no qual o início e o término de todas as fatias de conjunto de dados são deslocados.</span><span class="sxs-lookup"><span data-stu-id="8b587-410">Timespan by which the start and end of all dataset slices are shifted.</span></span> <br/><br/><span data-ttu-id="8b587-411"><b>Observação:</b> se anchorDateTime e o deslocamento forem especificados, o resultado será um deslocamento combinado.</span><span class="sxs-lookup"><span data-stu-id="8b587-411"><b>Note</b>: If both anchorDateTime and offset are specified, the result is the combined shift.</span></span> |<span data-ttu-id="8b587-412">Não</span><span class="sxs-lookup"><span data-stu-id="8b587-412">No</span></span> |<span data-ttu-id="8b587-413">ND</span><span class="sxs-lookup"><span data-stu-id="8b587-413">NA</span></span> |

<span data-ttu-id="8b587-414">A seção de disponibilidade a seguir especifica que o conjunto de dados de saída é produzido por hora (ou) o conjunto de dados de entrada está disponível por hora:</span><span class="sxs-lookup"><span data-stu-id="8b587-414">The following availability section specifies that the output dataset is either produced hourly (or) input dataset is available hourly:</span></span>

```json
"availability":    
{    
    "frequency": "Hour",        
    "interval": 1    
}
```

<span data-ttu-id="8b587-415">A seção **política** na definição do conjunto de dados define os critérios ou a condição que as divisões de conjunto de dados devem atender.</span><span class="sxs-lookup"><span data-stu-id="8b587-415">The **policy** section in dataset definition defines the criteria or the condition that the dataset slices must fulfill.</span></span>

| <span data-ttu-id="8b587-416">Nome da política</span><span class="sxs-lookup"><span data-stu-id="8b587-416">Policy Name</span></span> | <span data-ttu-id="8b587-417">Descrição</span><span class="sxs-lookup"><span data-stu-id="8b587-417">Description</span></span> | <span data-ttu-id="8b587-418">Aplicado a</span><span class="sxs-lookup"><span data-stu-id="8b587-418">Applied To</span></span> | <span data-ttu-id="8b587-419">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="8b587-419">Required</span></span> | <span data-ttu-id="8b587-420">Padrão</span><span class="sxs-lookup"><span data-stu-id="8b587-420">Default</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="8b587-421">minimumSizeMB</span><span class="sxs-lookup"><span data-stu-id="8b587-421">minimumSizeMB</span></span> |<span data-ttu-id="8b587-422">Valida que os dados em um **blob do Azure** atendem aos requisitos de tamanho mínimo (em megabytes).</span><span class="sxs-lookup"><span data-stu-id="8b587-422">Validates that the data in an **Azure blob** meets the minimum size requirements (in megabytes).</span></span> |<span data-ttu-id="8b587-423">blob do Azure</span><span class="sxs-lookup"><span data-stu-id="8b587-423">Azure Blob</span></span> |<span data-ttu-id="8b587-424">Não</span><span class="sxs-lookup"><span data-stu-id="8b587-424">No</span></span> |<span data-ttu-id="8b587-425">ND</span><span class="sxs-lookup"><span data-stu-id="8b587-425">NA</span></span> |
| <span data-ttu-id="8b587-426">minimumRows</span><span class="sxs-lookup"><span data-stu-id="8b587-426">minimumRows</span></span> |<span data-ttu-id="8b587-427">Valida que os dados em um **Banco de Dados SQL do Azure** ou uma **tabela do Azure** contêm o número mínimo de linhas.</span><span class="sxs-lookup"><span data-stu-id="8b587-427">Validates that the data in an **Azure SQL database** or an **Azure table** contains the minimum number of rows.</span></span> |<ul><li><span data-ttu-id="8b587-428">Banco de Dados SQL do Azure</span><span class="sxs-lookup"><span data-stu-id="8b587-428">Azure SQL Database</span></span></li><li><span data-ttu-id="8b587-429">tabela do Azure</span><span class="sxs-lookup"><span data-stu-id="8b587-429">Azure Table</span></span></li></ul> |<span data-ttu-id="8b587-430">Não</span><span class="sxs-lookup"><span data-stu-id="8b587-430">No</span></span> |<span data-ttu-id="8b587-431">ND</span><span class="sxs-lookup"><span data-stu-id="8b587-431">NA</span></span> |

<span data-ttu-id="8b587-432">**Exemplo:**</span><span class="sxs-lookup"><span data-stu-id="8b587-432">**Example:**</span></span>

```json
"policy":

{
    "validation":
    {
        "minimumSizeMB": 10.0
    }
}
```

<span data-ttu-id="8b587-433">A menos que um conjunto de dados seja produzido pela Azure Data Factory, ele deverá ser marcado como **externo**.</span><span class="sxs-lookup"><span data-stu-id="8b587-433">Unless a dataset is being produced by Azure Data Factory, it should be marked as **external**.</span></span> <span data-ttu-id="8b587-434">Essa configuração geralmente se aplica às entradas da primeira atividade em um pipeline, a menos que uma atividade ou pipeline encadeamento esteja sendo usado.</span><span class="sxs-lookup"><span data-stu-id="8b587-434">This setting generally applies to the inputs of first activity in a pipeline unless activity or pipeline chaining is being used.</span></span>

| <span data-ttu-id="8b587-435">name</span><span class="sxs-lookup"><span data-stu-id="8b587-435">Name</span></span> | <span data-ttu-id="8b587-436">Descrição</span><span class="sxs-lookup"><span data-stu-id="8b587-436">Description</span></span> | <span data-ttu-id="8b587-437">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="8b587-437">Required</span></span> | <span data-ttu-id="8b587-438">Valor Padrão</span><span class="sxs-lookup"><span data-stu-id="8b587-438">Default Value</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="8b587-439">dataDelay</span><span class="sxs-lookup"><span data-stu-id="8b587-439">dataDelay</span></span> |<span data-ttu-id="8b587-440">Tempo para esperar a verificação na disponibilidade dos dados externos de uma determinada divisão.</span><span class="sxs-lookup"><span data-stu-id="8b587-440">Time to delay the check on the availability of the external data for the given slice.</span></span> <span data-ttu-id="8b587-441">Por exemplo, se os dados estiverem disponíveis por hora, a verificação para ver se os dados externos estão disponíveis e se a fatia correspondente está Pronta pode ser atrasada usando dataDelay.</span><span class="sxs-lookup"><span data-stu-id="8b587-441">For example, if the data is available hourly, the check to see the external data is available and the corresponding slice is Ready can be delayed by using dataDelay.</span></span><br/><br/><span data-ttu-id="8b587-442">Aplica-se apenas à hora atual.</span><span class="sxs-lookup"><span data-stu-id="8b587-442">Only applies to the present time.</span></span>  <span data-ttu-id="8b587-443">Por exemplo, se agora forem 13hs e se esse valor for 10 minutos, a validação começará às 13:10hs.</span><span class="sxs-lookup"><span data-stu-id="8b587-443">For example, if it is 1:00 PM right now and this value is 10 minutes, the validation starts at 1:10 PM.</span></span><br/><br/><span data-ttu-id="8b587-444">Essa configuração não afeta fatias no passado (fatias com hora de término da fatia + dataDelay < Agora são processadas sem demora).</span><span class="sxs-lookup"><span data-stu-id="8b587-444">This setting does not affect slices in the past (slices with Slice End Time + dataDelay < Now) are processed without any delay.</span></span><br/><br/><span data-ttu-id="8b587-445">Um horário superior a 23:59 horas precisa ser especificado usando o formato `day.hours:minutes:seconds`.</span><span class="sxs-lookup"><span data-stu-id="8b587-445">Time greater than 23:59 hours need to specified using the `day.hours:minutes:seconds` format.</span></span> <span data-ttu-id="8b587-446">Por exemplo, para especificar 24 horas, não use 24:00:00; em vez disso, use 1.00:00:00.</span><span class="sxs-lookup"><span data-stu-id="8b587-446">For example, to specify 24 hours, don't use 24:00:00; instead, use 1.00:00:00.</span></span> <span data-ttu-id="8b587-447">Se você usar 24:00:00, isso será tratado como 24 dias (24.00:00:00).</span><span class="sxs-lookup"><span data-stu-id="8b587-447">If you use 24:00:00, it is treated as 24 days (24.00:00:00).</span></span> <span data-ttu-id="8b587-448">Para 1 dia e 4 horas, especifique 1:04:00:00.</span><span class="sxs-lookup"><span data-stu-id="8b587-448">For 1 day and 4 hours, specify 1:04:00:00.</span></span> |<span data-ttu-id="8b587-449">Não</span><span class="sxs-lookup"><span data-stu-id="8b587-449">No</span></span> |<span data-ttu-id="8b587-450">0</span><span class="sxs-lookup"><span data-stu-id="8b587-450">0</span></span> |
| <span data-ttu-id="8b587-451">retryInterval</span><span class="sxs-lookup"><span data-stu-id="8b587-451">retryInterval</span></span> |<span data-ttu-id="8b587-452">O tempo de espera entre uma falha e a próxima tentativa de repetição.</span><span class="sxs-lookup"><span data-stu-id="8b587-452">The wait time between a failure and the next retry attempt.</span></span> <span data-ttu-id="8b587-453">Se uma tentativa falhar, a próxima tentativa será após retryInterval.</span><span class="sxs-lookup"><span data-stu-id="8b587-453">If a try fails, the next try is after retryInterval.</span></span> <br/><br/><span data-ttu-id="8b587-454">Se agora for 1:00 PM, iniciaremos a primeira tentativa.</span><span class="sxs-lookup"><span data-stu-id="8b587-454">If it is 1:00 PM right now, we begin the first try.</span></span> <span data-ttu-id="8b587-455">Se a duração para concluir a primeira verificação de validação for 1 minuto e a operação tiver falhado, a próxima repetição será 1:00 + 1 min (duração) + 1min (intervalo de repetição) = 1:02.</span><span class="sxs-lookup"><span data-stu-id="8b587-455">If the duration to complete the first validation check is 1 minute and the operation failed, the next retry is at 1:00 + 1 min (duration) + 1 min (retry interval) = 1:02 PM.</span></span> <br/><br/><span data-ttu-id="8b587-456">Para fatias no passado, não haverá nenhum atraso.</span><span class="sxs-lookup"><span data-stu-id="8b587-456">For slices in the past, there is no delay.</span></span> <span data-ttu-id="8b587-457">A repetição acontece imediatamente.</span><span class="sxs-lookup"><span data-stu-id="8b587-457">The retry happens immediately.</span></span> |<span data-ttu-id="8b587-458">Não</span><span class="sxs-lookup"><span data-stu-id="8b587-458">No</span></span> |<span data-ttu-id="8b587-459">00:01:00 (1 minuto)</span><span class="sxs-lookup"><span data-stu-id="8b587-459">00:01:00 (1 minute)</span></span> |
| <span data-ttu-id="8b587-460">retryTimeout</span><span class="sxs-lookup"><span data-stu-id="8b587-460">retryTimeout</span></span> |<span data-ttu-id="8b587-461">O tempo limite para cada tentativa de repetição.</span><span class="sxs-lookup"><span data-stu-id="8b587-461">The timeout for each retry attempt.</span></span><br/><br/><span data-ttu-id="8b587-462">Se essa propriedade for definida para 10 minutos, a validação precisará ser concluída em 10 minutos.</span><span class="sxs-lookup"><span data-stu-id="8b587-462">If this property is set to 10 minutes, the validation needs to be completed within 10 minutes.</span></span> <span data-ttu-id="8b587-463">Se demorar mais de 10 minutos para executar a validação, a repetição atingirá o tempo limite.</span><span class="sxs-lookup"><span data-stu-id="8b587-463">If it takes longer than 10 minutes to perform the validation, the retry times out.</span></span><br/><br/><span data-ttu-id="8b587-464">Se todas as tentativas para a validação excederem o tempo limite, a fatia será marcada como TimedOut.</span><span class="sxs-lookup"><span data-stu-id="8b587-464">If all attempts for the validation times out, the slice is marked as TimedOut.</span></span> |<span data-ttu-id="8b587-465">Não</span><span class="sxs-lookup"><span data-stu-id="8b587-465">No</span></span> |<span data-ttu-id="8b587-466">00:10:00 (10 minutos)</span><span class="sxs-lookup"><span data-stu-id="8b587-466">00:10:00 (10 minutes)</span></span> |
| <span data-ttu-id="8b587-467">maximumRetry</span><span class="sxs-lookup"><span data-stu-id="8b587-467">maximumRetry</span></span> |<span data-ttu-id="8b587-468">Número de vezes para verificar a disponibilidade dos dados externos.</span><span class="sxs-lookup"><span data-stu-id="8b587-468">Number of times to check for the availability of the external data.</span></span> <span data-ttu-id="8b587-469">O valor máximo permitido é 10.</span><span class="sxs-lookup"><span data-stu-id="8b587-469">The allowed maximum value is 10.</span></span> |<span data-ttu-id="8b587-470">Não</span><span class="sxs-lookup"><span data-stu-id="8b587-470">No</span></span> |<span data-ttu-id="8b587-471">3</span><span class="sxs-lookup"><span data-stu-id="8b587-471">3</span></span> |


## <a name="data-stores"></a><span data-ttu-id="8b587-472">ARMAZENAMENTOS DE DADOS</span><span class="sxs-lookup"><span data-stu-id="8b587-472">DATA STORES</span></span>
<span data-ttu-id="8b587-473">A seção [serviço vinculado](#linked-service) forneceu descrições para elementos JSON que são comuns a todos os tipos de serviços vinculados.</span><span class="sxs-lookup"><span data-stu-id="8b587-473">The [Linked service](#linked-service) section provided descriptions for JSON elements that are common to all types of linked services.</span></span> <span data-ttu-id="8b587-474">Esta seção fornece detalhes sobre os elementos JSON específicos para cada armazenamento de dados.</span><span class="sxs-lookup"><span data-stu-id="8b587-474">This section provides details about JSON elements that are specific to each data store.</span></span>

<span data-ttu-id="8b587-475">A seção [Conjunto de dados](#dataset) forneceu descrições para elementos JSON que são comuns a todos os tipos de conjuntos de dados.</span><span class="sxs-lookup"><span data-stu-id="8b587-475">The [Dataset](#dataset) section provided descriptions for JSON elements that are common to all types of datasets.</span></span> <span data-ttu-id="8b587-476">Esta seção fornece detalhes sobre os elementos JSON específicos para cada armazenamento de dados.</span><span class="sxs-lookup"><span data-stu-id="8b587-476">This section provides details about JSON elements that are specific to each data store.</span></span>

<span data-ttu-id="8b587-477">A seção [Atividade](#activity) forneceu descrições para elementos JSON que são comuns a todos os tipos de atividades.</span><span class="sxs-lookup"><span data-stu-id="8b587-477">The [Activity](#activity) section provided descriptions for JSON elements that are common to all types of activities.</span></span> <span data-ttu-id="8b587-478">Esta seção fornece detalhes sobre os elementos JSON que são específicos para cada armazenamento de dados quando ele é usado como um fonte/coletor em uma atividade de cópia.</span><span class="sxs-lookup"><span data-stu-id="8b587-478">This section provides details about JSON elements that are specific to each data store when it is used as a source/sink in a copy activity.</span></span>  

<span data-ttu-id="8b587-479">Clique no link para o armazenamento no qual você está interessado em ver os esquemas JSON para o serviço vinculado, conjunto de dados e a fonte/coletor para a atividade de cópia.</span><span class="sxs-lookup"><span data-stu-id="8b587-479">Click the link for the store you are interested in to see the JSON schemas for linked service, dataset, and the source/sink for the copy activity.</span></span>

| <span data-ttu-id="8b587-480">Categoria</span><span class="sxs-lookup"><span data-stu-id="8b587-480">Category</span></span> | <span data-ttu-id="8b587-481">Armazenamento de dados</span><span class="sxs-lookup"><span data-stu-id="8b587-481">Data store</span></span> 
|:--- |:--- |
| <span data-ttu-id="8b587-482">**As tabelas**</span><span class="sxs-lookup"><span data-stu-id="8b587-482">**Azure**</span></span> |[<span data-ttu-id="8b587-483">Armazenamento de Blobs do Azure</span><span class="sxs-lookup"><span data-stu-id="8b587-483">Azure Blob storage</span></span>](#azure-blob-storage) |
| &nbsp; |[<span data-ttu-id="8b587-484">Repositório Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="8b587-484">Azure Data Lake Store</span></span>](#azure-datalake-store) |
| &nbsp; |[<span data-ttu-id="8b587-485">Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="8b587-485">Azure Cosmos DB</span></span>](#azure-cosmos-db) |
| &nbsp; |[<span data-ttu-id="8b587-486">Banco de Dados SQL do Azure</span><span class="sxs-lookup"><span data-stu-id="8b587-486">Azure SQL Database</span></span>](#azure-sql-database) |
| &nbsp; |[<span data-ttu-id="8b587-487">SQL Data Warehouse do Azure</span><span class="sxs-lookup"><span data-stu-id="8b587-487">Azure SQL Data Warehouse</span></span>](#azure-sql-data-warehouse) |
| &nbsp; |[<span data-ttu-id="8b587-488">Pesquisa do Azure</span><span class="sxs-lookup"><span data-stu-id="8b587-488">Azure Search</span></span>](#azure-search) |
| &nbsp; |[<span data-ttu-id="8b587-489">Armazenamento de Tabelas do Azure</span><span class="sxs-lookup"><span data-stu-id="8b587-489">Azure Table storage</span></span>](#azure-table-storage) |
| <span data-ttu-id="8b587-490">**Bancos de dados**</span><span class="sxs-lookup"><span data-stu-id="8b587-490">**Databases**</span></span> |[<span data-ttu-id="8b587-491">Amazon Redshift</span><span class="sxs-lookup"><span data-stu-id="8b587-491">Amazon Redshift</span></span>](#amazon-redshift) |
| &nbsp; |[<span data-ttu-id="8b587-492">IBM DB2</span><span class="sxs-lookup"><span data-stu-id="8b587-492">IBM DB2</span></span>](#ibm-db2) |
| &nbsp; |[<span data-ttu-id="8b587-493">MySQL</span><span class="sxs-lookup"><span data-stu-id="8b587-493">MySQL</span></span>](#mysql) |
| &nbsp; |[<span data-ttu-id="8b587-494">Oracle</span><span class="sxs-lookup"><span data-stu-id="8b587-494">Oracle</span></span>](#oracle) |
| &nbsp; |[<span data-ttu-id="8b587-495">PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="8b587-495">PostgreSQL</span></span>](#postgresql) |
| &nbsp; |[<span data-ttu-id="8b587-496">SAP Business Warehouse</span><span class="sxs-lookup"><span data-stu-id="8b587-496">SAP Business Warehouse</span></span>](#sap-business-warehouse) |
| &nbsp; |[<span data-ttu-id="8b587-497">SAP HANA</span><span class="sxs-lookup"><span data-stu-id="8b587-497">SAP HANA</span></span>](#sap-hana) |
| &nbsp; |[<span data-ttu-id="8b587-498">SQL Server</span><span class="sxs-lookup"><span data-stu-id="8b587-498">SQL Server</span></span>](#sql-server) |
| &nbsp; |[<span data-ttu-id="8b587-499">Sybase</span><span class="sxs-lookup"><span data-stu-id="8b587-499">Sybase</span></span>](#sybase) |
| &nbsp; |[<span data-ttu-id="8b587-500">Teradata</span><span class="sxs-lookup"><span data-stu-id="8b587-500">Teradata</span></span>](#teradata) |
| <span data-ttu-id="8b587-501">**NoSQL**</span><span class="sxs-lookup"><span data-stu-id="8b587-501">**NoSQL**</span></span> |[<span data-ttu-id="8b587-502">Cassandra</span><span class="sxs-lookup"><span data-stu-id="8b587-502">Cassandra</span></span>](#cassandra) |
| &nbsp; |[<span data-ttu-id="8b587-503">MongoDB</span><span class="sxs-lookup"><span data-stu-id="8b587-503">MongoDB</span></span>](#mongodb) |
| <span data-ttu-id="8b587-504">**Arquivo**</span><span class="sxs-lookup"><span data-stu-id="8b587-504">**File**</span></span> |[<span data-ttu-id="8b587-505">Amazon S3</span><span class="sxs-lookup"><span data-stu-id="8b587-505">Amazon S3</span></span>](#amazon-s3) |
| &nbsp; |[<span data-ttu-id="8b587-506">Sistema de Arquivos</span><span class="sxs-lookup"><span data-stu-id="8b587-506">File System</span></span>](#file-system) |
| &nbsp; |[<span data-ttu-id="8b587-507">FTP</span><span class="sxs-lookup"><span data-stu-id="8b587-507">FTP</span></span>](#ftp) |
| &nbsp; |[<span data-ttu-id="8b587-508">HDFS</span><span class="sxs-lookup"><span data-stu-id="8b587-508">HDFS</span></span>](#hdfs) |
| &nbsp; |[<span data-ttu-id="8b587-509">SFTP</span><span class="sxs-lookup"><span data-stu-id="8b587-509">SFTP</span></span>](#sftp) |
| <span data-ttu-id="8b587-510">**Outros**</span><span class="sxs-lookup"><span data-stu-id="8b587-510">**Others**</span></span> |[<span data-ttu-id="8b587-511">HTTP</span><span class="sxs-lookup"><span data-stu-id="8b587-511">HTTP</span></span>](#http) |
| &nbsp; |[<span data-ttu-id="8b587-512">OData</span><span class="sxs-lookup"><span data-stu-id="8b587-512">OData</span></span>](#odata) |
| &nbsp; |[<span data-ttu-id="8b587-513">ODBC</span><span class="sxs-lookup"><span data-stu-id="8b587-513">ODBC</span></span>](#odbc) |
| &nbsp; |[<span data-ttu-id="8b587-514">Salesforce</span><span class="sxs-lookup"><span data-stu-id="8b587-514">Salesforce</span></span>](#salesforce) |
| &nbsp; |[<span data-ttu-id="8b587-515">Tabela da Web</span><span class="sxs-lookup"><span data-stu-id="8b587-515">Web Table</span></span>](#web-table) |

## <a name="azure-blob-storage"></a><span data-ttu-id="8b587-516">Armazenamento do Blobs do Azure</span><span class="sxs-lookup"><span data-stu-id="8b587-516">Azure Blob Storage</span></span>

### <a name="linked-service"></a><span data-ttu-id="8b587-517">Serviço vinculado</span><span class="sxs-lookup"><span data-stu-id="8b587-517">Linked service</span></span>
<span data-ttu-id="8b587-518">Há dois tipos de serviços vinculados: serviço vinculado do Armazenamento do Azure e serviço vinculado do Armazenamento do Azure SAS.</span><span class="sxs-lookup"><span data-stu-id="8b587-518">There are two types of linked services: Azure Storage linked service and Azure Storage SAS linked service.</span></span>

#### <a name="azure-storage-linked-service"></a><span data-ttu-id="8b587-519">Serviço vinculado de armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="8b587-519">Azure Storage Linked Service</span></span>
<span data-ttu-id="8b587-520">Para vincular uma conta de armazenamento do Azure ao data factory usando a **chave de conta**, crie um serviço vinculado do Armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="8b587-520">To link your Azure storage account to a data factory by using the **account key**, create an Azure Storage linked service.</span></span> <span data-ttu-id="8b587-521">Para definir um serviço vinculado do Armazenamento do Azure, defina o **tipo** do serviço vinculado para **AzureStorage**.</span><span class="sxs-lookup"><span data-stu-id="8b587-521">To define an Azure Storage linked service, set the **type** of the linked service to **AzureStorage**.</span></span> <span data-ttu-id="8b587-522">Em seguida, você pode especificar as seguintes propriedades na seção **typeProperties**:</span><span class="sxs-lookup"><span data-stu-id="8b587-522">Then, you can specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="8b587-523">Propriedade</span><span class="sxs-lookup"><span data-stu-id="8b587-523">Property</span></span> | <span data-ttu-id="8b587-524">Descrição</span><span class="sxs-lookup"><span data-stu-id="8b587-524">Description</span></span> | <span data-ttu-id="8b587-525">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="8b587-525">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="8b587-526">connectionString</span><span class="sxs-lookup"><span data-stu-id="8b587-526">connectionString</span></span> |<span data-ttu-id="8b587-527">Especifique as informações necessárias para se conectar ao armazenamento do Azure para a propriedade connectionString.</span><span class="sxs-lookup"><span data-stu-id="8b587-527">Specify information needed to connect to Azure storage for the connectionString property.</span></span> |<span data-ttu-id="8b587-528">Sim</span><span class="sxs-lookup"><span data-stu-id="8b587-528">Yes</span></span> |

##### <a name="example"></a><span data-ttu-id="8b587-529">Exemplo</span><span class="sxs-lookup"><span data-stu-id="8b587-529">Example</span></span>  

```json
{
    "name": "StorageLinkedService",
    "properties": {
        "type": "AzureStorage",
        "typeProperties": {
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
        }
    }
}
```

#### <a name="azure-storage-sas-linked-service"></a><span data-ttu-id="8b587-530">Serviço vinculado de SAS de Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="8b587-530">Azure Storage SAS Linked Service</span></span>
<span data-ttu-id="8b587-531">O serviço vinculado de SAS de armazenamento do Azure permite que você vincule uma conta de armazenamento do Azure ao Azure Data Factory usando uma SAS (Assinatura de Acesso Compartilhado).</span><span class="sxs-lookup"><span data-stu-id="8b587-531">The Azure Storage SAS linked service allows you to link an Azure Storage Account to an Azure data factory by using a Shared Access Signature (SAS).</span></span> <span data-ttu-id="8b587-532">Isso fornece ao data factory acesso restrito/acesso total, com limite de tempo/recursos específicos (blob/contêiner) no armazenamento.</span><span class="sxs-lookup"><span data-stu-id="8b587-532">It provides the data factory with restricted/time-bound access to all/specific resources (blob/container) in the storage.</span></span> <span data-ttu-id="8b587-533">Para vincular uma conta de Armazenamento do Azure ao data factory usando a Assinatura de Acesso Compartilhado, crie um serviço vinculado de SAS do Armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="8b587-533">To link your Azure storage account to a data factory by using Shared Access Signature, create an Azure Storage SAS linked service.</span></span> <span data-ttu-id="8b587-534">Para definir um serviço vinculado de SAS do Armazenamento do Azure, defina o **type** do serviço vinculado para **AzureStorageSas**.</span><span class="sxs-lookup"><span data-stu-id="8b587-534">To define an Azure Storage SAS linked service, set the **type** of the linked service to **AzureStorageSas**.</span></span> <span data-ttu-id="8b587-535">Em seguida, você pode especificar as seguintes propriedades na seção **typeProperties**:</span><span class="sxs-lookup"><span data-stu-id="8b587-535">Then, you can specify following properties in the **typeProperties** section:</span></span>   

| <span data-ttu-id="8b587-536">Propriedade</span><span class="sxs-lookup"><span data-stu-id="8b587-536">Property</span></span> | <span data-ttu-id="8b587-537">Descrição</span><span class="sxs-lookup"><span data-stu-id="8b587-537">Description</span></span> | <span data-ttu-id="8b587-538">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="8b587-538">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="8b587-539">sasUri</span><span class="sxs-lookup"><span data-stu-id="8b587-539">sasUri</span></span> |<span data-ttu-id="8b587-540">Especificar o URI de Assinatura de Acesso Compartilhado para os recursos de Armazenamento do Azure, como blob, contêiner ou tabela.</span><span class="sxs-lookup"><span data-stu-id="8b587-540">Specify Shared Access Signature URI to the Azure Storage resources such as blob, container, or table.</span></span> |<span data-ttu-id="8b587-541">Sim</span><span class="sxs-lookup"><span data-stu-id="8b587-541">Yes</span></span> |

##### <a name="example"></a><span data-ttu-id="8b587-542">Exemplo</span><span class="sxs-lookup"><span data-stu-id="8b587-542">Example</span></span>

```json
{  
    "name": "StorageSasLinkedService",  
    "properties": {  
        "type": "AzureStorageSas",  
        "typeProperties": {  
            "sasUri": "<storageUri>?<sasToken>"   
        }  
    }  
}  
```

<span data-ttu-id="8b587-543">Para obter mais informações sobre esses serviços vinculados, consulte o artigo [Conector de Armazenamento de Blobs do Azure](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="8b587-543">For more information about these linked services, see [Azure Blob Storage connector](data-factory-azure-blob-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="8b587-544">Conjunto de dados</span><span class="sxs-lookup"><span data-stu-id="8b587-544">Dataset</span></span>
<span data-ttu-id="8b587-545">Para definir um conjunto de dados de Blob do Azure, defina o **type** do conjunto de dados para **AzureBlob**.</span><span class="sxs-lookup"><span data-stu-id="8b587-545">To define an Azure Blob dataset, set the **type** of the dataset to **AzureBlob**.</span></span> <span data-ttu-id="8b587-546">Em seguida, especifique as seguintes propriedades específicas do Blob do Azure na seção **typeProperties**:</span><span class="sxs-lookup"><span data-stu-id="8b587-546">Then, specify the following Azure Blob specific properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="8b587-547">Propriedade</span><span class="sxs-lookup"><span data-stu-id="8b587-547">Property</span></span> | <span data-ttu-id="8b587-548">Descrição</span><span class="sxs-lookup"><span data-stu-id="8b587-548">Description</span></span> | <span data-ttu-id="8b587-549">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="8b587-549">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8b587-550">folderPath</span><span class="sxs-lookup"><span data-stu-id="8b587-550">folderPath</span></span> |<span data-ttu-id="8b587-551">Caminho para o contêiner e a pasta no armazenamento de blob.</span><span class="sxs-lookup"><span data-stu-id="8b587-551">Path to the container and folder in the blob storage.</span></span> <span data-ttu-id="8b587-552">Exemplo: myblobcontainer\myblobfolder\\</span><span class="sxs-lookup"><span data-stu-id="8b587-552">Example: myblobcontainer\myblobfolder\\</span></span> |<span data-ttu-id="8b587-553">Sim</span><span class="sxs-lookup"><span data-stu-id="8b587-553">Yes</span></span> |
| <span data-ttu-id="8b587-554">fileName</span><span class="sxs-lookup"><span data-stu-id="8b587-554">fileName</span></span> |<span data-ttu-id="8b587-555">O nome do blob.</span><span class="sxs-lookup"><span data-stu-id="8b587-555">Name of the blob.</span></span> <span data-ttu-id="8b587-556">fileName é opcional e diferencia maiúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="8b587-556">fileName is optional and case-sensitive.</span></span><br/><br/><span data-ttu-id="8b587-557">Caso você especifique um nome de arquivo, a atividade (incluindo Cópia) funcionará no Blob específico.</span><span class="sxs-lookup"><span data-stu-id="8b587-557">If you specify a filename, the activity (including Copy) works on the specific Blob.</span></span><br/><br/><span data-ttu-id="8b587-558">Quando fileName não for especificado, a Cópia incluirá todos os Blobs do folderPath para o conjunto de dados de entrada.</span><span class="sxs-lookup"><span data-stu-id="8b587-558">When fileName is not specified, Copy includes all Blobs in the folderPath for input dataset.</span></span><br/><br/><span data-ttu-id="8b587-559">Quando fileName não for especificado para um conjunto de dados de saída, o nome do arquivo gerado estaria no seguinte formato: Data.<Guid>.txt (por exemplo: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt)</span><span class="sxs-lookup"><span data-stu-id="8b587-559">When fileName is not specified for an output dataset, the name of the generated file would be in the following this format: Data.<Guid>.txt (for example: : Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span></span> |<span data-ttu-id="8b587-560">Não</span><span class="sxs-lookup"><span data-stu-id="8b587-560">No</span></span> |
| <span data-ttu-id="8b587-561">partitionedBy</span><span class="sxs-lookup"><span data-stu-id="8b587-561">partitionedBy</span></span> |<span data-ttu-id="8b587-562">partitionedBy é uma propriedade opcional.</span><span class="sxs-lookup"><span data-stu-id="8b587-562">partitionedBy is an optional property.</span></span> <span data-ttu-id="8b587-563">Você pode usá-lo para especificar um folderPath dinâmico e o nome de arquivo para dados de série temporal.</span><span class="sxs-lookup"><span data-stu-id="8b587-563">You can use it to specify a dynamic folderPath and filename for time series data.</span></span> <span data-ttu-id="8b587-564">Por exemplo, folderPath pode ser parametrizado para cada hora dos dados.</span><span class="sxs-lookup"><span data-stu-id="8b587-564">For example, folderPath can be parameterized for every hour of data.</span></span> |<span data-ttu-id="8b587-565">Não</span><span class="sxs-lookup"><span data-stu-id="8b587-565">No</span></span> |
| <span data-ttu-id="8b587-566">formato</span><span class="sxs-lookup"><span data-stu-id="8b587-566">format</span></span> | <span data-ttu-id="8b587-567">Há suporte para os seguintes tipos de formato: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat** e **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="8b587-567">The following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="8b587-568">Defina a propriedade **type** sob formato como um desses valores.</span><span class="sxs-lookup"><span data-stu-id="8b587-568">Set the **type** property under format to one of these values.</span></span> <span data-ttu-id="8b587-569">Para saber mais, veja as seções [Formato de texto](data-factory-supported-file-and-compression-formats.md#text-format), [Formato Json](data-factory-supported-file-and-compression-formats.md#json-format), [Formato Avro](data-factory-supported-file-and-compression-formats.md#avro-format), [Formato Orc](data-factory-supported-file-and-compression-formats.md#orc-format), e [Formato Parquet](data-factory-supported-file-and-compression-formats.md#parquet-format).</span><span class="sxs-lookup"><span data-stu-id="8b587-569">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="8b587-570">Se você quiser **copiar arquivos no estado em que se encontram** entre repositórios baseados em arquivo (cópia binária), ignore a seção de formato nas duas definições de conjunto de dados de entrada e de saída.</span><span class="sxs-lookup"><span data-stu-id="8b587-570">If you want to **copy files as-is** between file-based stores (binary copy), skip the format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="8b587-571">Não</span><span class="sxs-lookup"><span data-stu-id="8b587-571">No</span></span> |
| <span data-ttu-id="8b587-572">compactação</span><span class="sxs-lookup"><span data-stu-id="8b587-572">compression</span></span> | <span data-ttu-id="8b587-573">Especifique o tipo e o nível de compactação para os dados.</span><span class="sxs-lookup"><span data-stu-id="8b587-573">Specify the type and level of compression for the data.</span></span> <span data-ttu-id="8b587-574">Os tipos com suporte são: **GZip**, **Deflate**, **BZip2** e **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="8b587-574">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="8b587-575">Os níveis com suporte são **Ideal** e **O mais rápido**.</span><span class="sxs-lookup"><span data-stu-id="8b587-575">Supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="8b587-576">Para saber mais, confira [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support) (Formatos de arquivo e de compactação no Azure Data Factory).</span><span class="sxs-lookup"><span data-stu-id="8b587-576">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="8b587-577">Não</span><span class="sxs-lookup"><span data-stu-id="8b587-577">No</span></span> |

#### <a name="example"></a><span data-ttu-id="8b587-578">Exemplo</span><span class="sxs-lookup"><span data-stu-id="8b587-578">Example</span></span>

```json
{
    "name": "AzureBlobInput",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "fileName": "input.log",
            "folderPath": "adfgetstarted/inputdata",
            "format": {
                "type": "TextFormat",
                "columnDelimiter": ","
            }
        },
        "availability": {
            "frequency": "Month",
            "interval": 1
        },
        "external": true,
        "policy": {}
    }
}
 ```


<span data-ttu-id="8b587-579">Para obter mais informações, consulte o artigo [Conector de Blob do Azure](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="8b587-579">For more information, see [Azure Blob connector](data-factory-azure-blob-connector.md#dataset-properties) article.</span></span>

### <a name="blobsource-in-copy-activity"></a><span data-ttu-id="8b587-580">BlobSource na Atividade de Cópia</span><span class="sxs-lookup"><span data-stu-id="8b587-580">BlobSource in Copy Activity</span></span>
<span data-ttu-id="8b587-581">Se você estiver copiando dados de um Armazenamento de Blobs do Azure, defina o **source type** da atividade de cópia para **BlobSource** e especifique as propriedades a seguir na seção **source**:</span><span class="sxs-lookup"><span data-stu-id="8b587-581">If you are copying data from an Azure Blob Storage, set the **source type** of the copy activity to **BlobSource**, and specify following properties in the **source **section:</span></span>

| <span data-ttu-id="8b587-582">Propriedade</span><span class="sxs-lookup"><span data-stu-id="8b587-582">Property</span></span> | <span data-ttu-id="8b587-583">Descrição</span><span class="sxs-lookup"><span data-stu-id="8b587-583">Description</span></span> | <span data-ttu-id="8b587-584">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="8b587-584">Allowed values</span></span> | <span data-ttu-id="8b587-585">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="8b587-585">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="8b587-586">recursiva</span><span class="sxs-lookup"><span data-stu-id="8b587-586">recursive</span></span> |<span data-ttu-id="8b587-587">Indica se os dados são lidos recursivamente por meio de subpastas ou somente da pasta especificada.</span><span class="sxs-lookup"><span data-stu-id="8b587-587">Indicates whether the data is read recursively from the sub folders or only from the specified folder.</span></span> |<span data-ttu-id="8b587-588">True (valor padrão), False</span><span class="sxs-lookup"><span data-stu-id="8b587-588">True (default value), False</span></span> |<span data-ttu-id="8b587-589">Não</span><span class="sxs-lookup"><span data-stu-id="8b587-589">No</span></span> |

#### <a name="example-blobsource"></a><span data-ttu-id="8b587-590">Exemplo: BlobSource**</span><span class="sxs-lookup"><span data-stu-id="8b587-590">Example: BlobSource**</span></span>
```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "AzureBlobtoSQL",
            "description": "Copy Activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureBlobInput"
            }],
            "outputs": [{
                "name": "AzureSqlOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "BlobSource"
                },
                "sink": {
                    "type": "SqlSink"
                }
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```
### <a name="blobsink-in-copy-activity"></a><span data-ttu-id="8b587-591">BlobSink na Atividade de Cópia</span><span class="sxs-lookup"><span data-stu-id="8b587-591">BlobSink in Copy Activity</span></span>
<span data-ttu-id="8b587-592">Se você estiver copiando dados para um Armazenamento de Blobs do Azure, defina o **sink type** da atividade de cópia para **BlobSource** e especifique as propriedades a seguir na seção **source**:</span><span class="sxs-lookup"><span data-stu-id="8b587-592">If you are copying data to an Azure Blob Storage, set the **sink type** of the copy activity to **BlobSink**, and specify following properties in the **sink** section:</span></span>

| <span data-ttu-id="8b587-593">Propriedade</span><span class="sxs-lookup"><span data-stu-id="8b587-593">Property</span></span> | <span data-ttu-id="8b587-594">Descrição</span><span class="sxs-lookup"><span data-stu-id="8b587-594">Description</span></span> | <span data-ttu-id="8b587-595">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="8b587-595">Allowed values</span></span> | <span data-ttu-id="8b587-596">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="8b587-596">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="8b587-597">copyBehavior</span><span class="sxs-lookup"><span data-stu-id="8b587-597">copyBehavior</span></span> |<span data-ttu-id="8b587-598">Define o comportamento de cópia quando a origem é BlobSource ou FileSystem.</span><span class="sxs-lookup"><span data-stu-id="8b587-598">Defines the copy behavior when the source is BlobSource or FileSystem.</span></span> |<span data-ttu-id="8b587-599"><b>PreserveHierarchy:</b> preserva a hierarquia de arquivos na pasta de destino.</span><span class="sxs-lookup"><span data-stu-id="8b587-599"><b>PreserveHierarchy</b>: preserves the file hierarchy in the target folder.</span></span> <span data-ttu-id="8b587-600">O caminho relativo do arquivo de origem para a pasta de origem é idêntico ao caminho relativo do arquivo de destino para a pasta de destino.</span><span class="sxs-lookup"><span data-stu-id="8b587-600">The relative path of source file to source folder is identical to the relative path of target file to target folder.</span></span><br/><br/><span data-ttu-id="8b587-601"><b>FlattenHierarchy:</b> todos os arquivos da pasta de origem estão no primeiro nível da pasta de destino.</span><span class="sxs-lookup"><span data-stu-id="8b587-601"><b>FlattenHierarchy</b>: all files from the source folder are in the first level of target folder.</span></span> <span data-ttu-id="8b587-602">Os arquivos de destino têm o nome gerado automaticamente.</span><span class="sxs-lookup"><span data-stu-id="8b587-602">The target files have auto generated name.</span></span> <br/><br/><span data-ttu-id="8b587-603"><b>MergeFiles (padrão)</b>: mescla todos os arquivos da pasta de origem em um arquivo.</span><span class="sxs-lookup"><span data-stu-id="8b587-603"><b>MergeFiles (default):</b> merges all files from the source folder to one file.</span></span> <span data-ttu-id="8b587-604">Se o nome do arquivo/blob for especificado, o nome do arquivo mesclado será o nome especificado; caso contrário, será o nome de arquivo gerado automaticamente.</span><span class="sxs-lookup"><span data-stu-id="8b587-604">If the File/Blob Name is specified, the merged file name would be the specified name; otherwise, would be auto-generated file name.</span></span> |<span data-ttu-id="8b587-605">Não</span><span class="sxs-lookup"><span data-stu-id="8b587-605">No</span></span> |

#### <a name="example-blobsink"></a><span data-ttu-id="8b587-606">Exemplo: BlobSink</span><span class="sxs-lookup"><span data-stu-id="8b587-606">Example: BlobSink</span></span>

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline for copy activity",
        "activities": [{
            "name": "AzureSQLtoBlob",
            "description": "copy activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureSQLInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "SqlSource",
                    "SqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

<span data-ttu-id="8b587-607">Para obter mais informações, consulte o artigo [Conector de Blob do Azure](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="8b587-607">For more information, see [Azure Blob connector](data-factory-azure-blob-connector.md#copy-activity-properties) article.</span></span> 

## <a name="azure-data-lake-store"></a><span data-ttu-id="8b587-608">Repositório Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="8b587-608">Azure Data Lake Store</span></span>

### <a name="linked-service"></a><span data-ttu-id="8b587-609">Serviço vinculado</span><span class="sxs-lookup"><span data-stu-id="8b587-609">Linked service</span></span>
<span data-ttu-id="8b587-610">Para definir um serviço vinculado do Azure Data Lake Store, defina o tipo do serviço vinculado para **AzureDataLakeStore**e especifique as propriedades a seguir na seção **typeProperties**:</span><span class="sxs-lookup"><span data-stu-id="8b587-610">To define an Azure Data Lake Store linked service, set the type of the linked service to **AzureDataLakeStore**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="8b587-611">Propriedade</span><span class="sxs-lookup"><span data-stu-id="8b587-611">Property</span></span> | <span data-ttu-id="8b587-612">Descrição</span><span class="sxs-lookup"><span data-stu-id="8b587-612">Description</span></span> | <span data-ttu-id="8b587-613">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="8b587-613">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="8b587-614">type</span><span class="sxs-lookup"><span data-stu-id="8b587-614">type</span></span> | <span data-ttu-id="8b587-615">A propriedade type deve ser definida como: **AzureDataLakeStore**</span><span class="sxs-lookup"><span data-stu-id="8b587-615">The type property must be set to: **AzureDataLakeStore**</span></span> | <span data-ttu-id="8b587-616">Sim</span><span class="sxs-lookup"><span data-stu-id="8b587-616">Yes</span></span> |
| <span data-ttu-id="8b587-617">dataLakeStoreUri</span><span class="sxs-lookup"><span data-stu-id="8b587-617">dataLakeStoreUri</span></span> | <span data-ttu-id="8b587-618">Especifica informações sobre a conta do Repositório Data Lake do Azure.</span><span class="sxs-lookup"><span data-stu-id="8b587-618">Specify information about the Azure Data Lake Store account.</span></span> <span data-ttu-id="8b587-619">Ele está no seguinte formato: `https://[accountname].azuredatalakestore.net/webhdfs/v1` ou `adl://[accountname].azuredatalakestore.net/`.</span><span class="sxs-lookup"><span data-stu-id="8b587-619">It is in the following format: `https://[accountname].azuredatalakestore.net/webhdfs/v1` or `adl://[accountname].azuredatalakestore.net/`.</span></span> | <span data-ttu-id="8b587-620">Sim</span><span class="sxs-lookup"><span data-stu-id="8b587-620">Yes</span></span> |
| <span data-ttu-id="8b587-621">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="8b587-621">subscriptionId</span></span> | <span data-ttu-id="8b587-622">Id de assinatura do Azure ao qual pertence Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="8b587-622">Azure subscription Id to which Data Lake Store belongs.</span></span> | <span data-ttu-id="8b587-623">Obrigatório para coletor</span><span class="sxs-lookup"><span data-stu-id="8b587-623">Required for sink</span></span> |
| <span data-ttu-id="8b587-624">resourceGroupName</span><span class="sxs-lookup"><span data-stu-id="8b587-624">resourceGroupName</span></span> | <span data-ttu-id="8b587-625">Nome do grupo de recursos do Azure ao qual pertence Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="8b587-625">Azure resource group name to which Data Lake Store belongs.</span></span> | <span data-ttu-id="8b587-626">Obrigatório para coletor</span><span class="sxs-lookup"><span data-stu-id="8b587-626">Required for sink</span></span> |
| <span data-ttu-id="8b587-627">servicePrincipalId</span><span class="sxs-lookup"><span data-stu-id="8b587-627">servicePrincipalId</span></span> | <span data-ttu-id="8b587-628">Especifique a ID do cliente do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="8b587-628">Specify the application's client ID.</span></span> | <span data-ttu-id="8b587-629">Sim (para autenticação de entidade de serviço)</span><span class="sxs-lookup"><span data-stu-id="8b587-629">Yes (for service principal authentication)</span></span> |
| <span data-ttu-id="8b587-630">servicePrincipalKey</span><span class="sxs-lookup"><span data-stu-id="8b587-630">servicePrincipalKey</span></span> | <span data-ttu-id="8b587-631">Especifique a chave do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="8b587-631">Specify the application's key.</span></span> | <span data-ttu-id="8b587-632">Sim (para autenticação de entidade de serviço)</span><span class="sxs-lookup"><span data-stu-id="8b587-632">Yes (for service principal authentication)</span></span> |
| <span data-ttu-id="8b587-633">locatário</span><span class="sxs-lookup"><span data-stu-id="8b587-633">tenant</span></span> | <span data-ttu-id="8b587-634">Especifique as informações de locatário (domínio nome ou ID do Locatário) em que o aplicativo reside.</span><span class="sxs-lookup"><span data-stu-id="8b587-634">Specify the tenant information (domain name or tenant ID) under which your application resides.</span></span> <span data-ttu-id="8b587-635">É possível recuperá-lo focalizando o canto superior direito do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="8b587-635">You can retrieve it by hovering the mouse in the top-right corner of the Azure portal.</span></span> | <span data-ttu-id="8b587-636">Sim (para autenticação de entidade de serviço)</span><span class="sxs-lookup"><span data-stu-id="8b587-636">Yes (for service principal authentication)</span></span> |
| <span data-ttu-id="8b587-637">authorization</span><span class="sxs-lookup"><span data-stu-id="8b587-637">authorization</span></span> | <span data-ttu-id="8b587-638">Clique no botão **Autorizar** no **Editor do Data Factory** e insira as suas credenciais, que atribui a URL de autorização gerada automaticamente a essa propriedade.</span><span class="sxs-lookup"><span data-stu-id="8b587-638">Click **Authorize** button in the **Data Factory Editor** and enter your credential that assigns the auto-generated authorization URL to this property.</span></span> | <span data-ttu-id="8b587-639">Sim (para autenticação de credenciais de usuário)</span><span class="sxs-lookup"><span data-stu-id="8b587-639">Yes (for user credential authentication)</span></span>|
| <span data-ttu-id="8b587-640">sessionId</span><span class="sxs-lookup"><span data-stu-id="8b587-640">sessionId</span></span> | <span data-ttu-id="8b587-641">A ID de sessão OAuth da sessão de autorização OAuth.</span><span class="sxs-lookup"><span data-stu-id="8b587-641">OAuth session id from the OAuth authorization session.</span></span> <span data-ttu-id="8b587-642">Cada ID da sessão é exclusiva e pode ser usado somente uma vez.</span><span class="sxs-lookup"><span data-stu-id="8b587-642">Each session id is unique and may only be used once.</span></span> <span data-ttu-id="8b587-643">Essa configuração é gerada automaticamente quando você usa o Editor do Data Factory.</span><span class="sxs-lookup"><span data-stu-id="8b587-643">This setting is automatically generated when you use Data Factory Editor.</span></span> | <span data-ttu-id="8b587-644">Sim (para autenticação de credenciais de usuário)</span><span class="sxs-lookup"><span data-stu-id="8b587-644">Yes (for user credential authentication)</span></span> |

#### <a name="example-using-service-principal-authentication"></a><span data-ttu-id="8b587-645">Exemplo: usando a autenticação da entidade de serviço</span><span class="sxs-lookup"><span data-stu-id="8b587-645">Example: using service principal authentication</span></span>
```json
{
    "name": "AzureDataLakeStoreLinkedService",
    "properties": {
        "type": "AzureDataLakeStore",
        "typeProperties": {
            "dataLakeStoreUri": "https://<accountname>.azuredatalakestore.net/webhdfs/v1",
            "servicePrincipalId": "<service principal id>",
            "servicePrincipalKey": "<service principal key>",
            "tenant": "<tenant info. Example: microsoft.onmicrosoft.com>"
        }
    }
}
```

#### <a name="example-using-user-credential-authentication"></a><span data-ttu-id="8b587-646">Exemplo: usando a autenticação de credenciais de usuário</span><span class="sxs-lookup"><span data-stu-id="8b587-646">Example: using user credential authentication</span></span>
```json
{
    "name": "AzureDataLakeStoreLinkedService",
    "properties": {
        "type": "AzureDataLakeStore",
        "typeProperties": {
            "dataLakeStoreUri": "https://<accountname>.azuredatalakestore.net/webhdfs/v1",
            "sessionId": "<session ID>",
            "authorization": "<authorization URL>",
            "subscriptionId": "<subscription of ADLS>",
            "resourceGroupName": "<resource group of ADLS>"
        }
    }
}
```

<span data-ttu-id="8b587-647">Para saber mais, consulte o artigo [Conector do Azure Data Lake Store](data-factory-azure-datalake-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="8b587-647">For more information, see [Azure Data Lake Store connector](data-factory-azure-datalake-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="8b587-648">Conjunto de dados</span><span class="sxs-lookup"><span data-stu-id="8b587-648">Dataset</span></span>
<span data-ttu-id="8b587-649">Para definir um conjunto de dados do Azure Data Lake Store, defina o **type** do conjunto de dados para **AzureDataLakeStore** e especifique as propriedades a seguir na seção **typeProperties**:</span><span class="sxs-lookup"><span data-stu-id="8b587-649">To define an Azure Data Lake Store dataset, set the **type** of the dataset to **AzureDataLakeStore**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="8b587-650">Propriedade</span><span class="sxs-lookup"><span data-stu-id="8b587-650">Property</span></span> | <span data-ttu-id="8b587-651">Descrição</span><span class="sxs-lookup"><span data-stu-id="8b587-651">Description</span></span> | <span data-ttu-id="8b587-652">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="8b587-652">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="8b587-653">folderPath</span><span class="sxs-lookup"><span data-stu-id="8b587-653">folderPath</span></span> |<span data-ttu-id="8b587-654">Caminho para o contêiner e a pasta no repositório do Azure Data Lake.</span><span class="sxs-lookup"><span data-stu-id="8b587-654">Path to the container and folder in the Azure Data Lake store.</span></span> |<span data-ttu-id="8b587-655">Sim</span><span class="sxs-lookup"><span data-stu-id="8b587-655">Yes</span></span> |
| <span data-ttu-id="8b587-656">fileName</span><span class="sxs-lookup"><span data-stu-id="8b587-656">fileName</span></span> |<span data-ttu-id="8b587-657">O nome do arquivo no repositório Azure Data Lake.</span><span class="sxs-lookup"><span data-stu-id="8b587-657">Name of the file in the Azure Data Lake store.</span></span> <span data-ttu-id="8b587-658">fileName é opcional e diferencia maiúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="8b587-658">fileName is optional and case-sensitive.</span></span> <br/><br/><span data-ttu-id="8b587-659">Caso você especifique um nome de arquivo, a atividade (incluindo Cópia) funcionará no arquivo específico.</span><span class="sxs-lookup"><span data-stu-id="8b587-659">If you specify a filename, the activity (including Copy) works on the specific file.</span></span><br/><br/><span data-ttu-id="8b587-660">Quando fileName não for especificado, a Cópia incluirá todos os arquivos do folderPath para o conjunto de dados de entrada.</span><span class="sxs-lookup"><span data-stu-id="8b587-660">When fileName is not specified, Copy includes all files in the folderPath for input dataset.</span></span><br/><br/><span data-ttu-id="8b587-661">Quando fileName não for especificado para um conjunto de dados de saída, o nome do arquivo gerado estaria no seguinte formato: Data<Guid>.txt (por exemplo: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt)</span><span class="sxs-lookup"><span data-stu-id="8b587-661">When fileName is not specified for an output dataset, the name of the generated file would be in the following this format: Data.<Guid>.txt (for example: : Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span></span> |<span data-ttu-id="8b587-662">Não</span><span class="sxs-lookup"><span data-stu-id="8b587-662">No</span></span> |
| <span data-ttu-id="8b587-663">partitionedBy</span><span class="sxs-lookup"><span data-stu-id="8b587-663">partitionedBy</span></span> |<span data-ttu-id="8b587-664">partitionedBy é uma propriedade opcional.</span><span class="sxs-lookup"><span data-stu-id="8b587-664">partitionedBy is an optional property.</span></span> <span data-ttu-id="8b587-665">Você pode usá-lo para especificar um folderPath dinâmico e o nome de arquivo para dados de série temporal.</span><span class="sxs-lookup"><span data-stu-id="8b587-665">You can use it to specify a dynamic folderPath and filename for time series data.</span></span> <span data-ttu-id="8b587-666">Por exemplo, folderPath pode ser parametrizado para cada hora dos dados.</span><span class="sxs-lookup"><span data-stu-id="8b587-666">For example, folderPath can be parameterized for every hour of data.</span></span> |<span data-ttu-id="8b587-667">Não</span><span class="sxs-lookup"><span data-stu-id="8b587-667">No</span></span> |
| <span data-ttu-id="8b587-668">formato</span><span class="sxs-lookup"><span data-stu-id="8b587-668">format</span></span> | <span data-ttu-id="8b587-669">Há suporte para os seguintes tipos de formato: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat** e **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="8b587-669">The following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="8b587-670">Defina a propriedade **type** sob formato como um desses valores.</span><span class="sxs-lookup"><span data-stu-id="8b587-670">Set the **type** property under format to one of these values.</span></span> <span data-ttu-id="8b587-671">Para saber mais, veja as seções [Formato de texto](data-factory-supported-file-and-compression-formats.md#text-format), [Formato Json](data-factory-supported-file-and-compression-formats.md#json-format), [Formato Avro](data-factory-supported-file-and-compression-formats.md#avro-format), [Formato Orc](data-factory-supported-file-and-compression-formats.md#orc-format), e [Formato Parquet](data-factory-supported-file-and-compression-formats.md#parquet-format).</span><span class="sxs-lookup"><span data-stu-id="8b587-671">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="8b587-672">Se você quiser **copiar arquivos no estado em que se encontram** entre repositórios baseados em arquivo (cópia binária), ignore a seção de formato nas duas definições de conjunto de dados de entrada e de saída.</span><span class="sxs-lookup"><span data-stu-id="8b587-672">If you want to **copy files as-is** between file-based stores (binary copy), skip the format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="8b587-673">Não</span><span class="sxs-lookup"><span data-stu-id="8b587-673">No</span></span> |
| <span data-ttu-id="8b587-674">compactação</span><span class="sxs-lookup"><span data-stu-id="8b587-674">compression</span></span> | <span data-ttu-id="8b587-675">Especifique o tipo e o nível de compactação para os dados.</span><span class="sxs-lookup"><span data-stu-id="8b587-675">Specify the type and level of compression for the data.</span></span> <span data-ttu-id="8b587-676">Os tipos com suporte são: **GZip**, **Deflate**, **BZip2** e **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="8b587-676">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="8b587-677">Os níveis com suporte são **Ideal** e **O mais rápido**.</span><span class="sxs-lookup"><span data-stu-id="8b587-677">Supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="8b587-678">Para saber mais, confira [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support) (Formatos de arquivo e de compactação no Azure Data Factory).</span><span class="sxs-lookup"><span data-stu-id="8b587-678">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="8b587-679">Não</span><span class="sxs-lookup"><span data-stu-id="8b587-679">No</span></span> |

#### <a name="example"></a><span data-ttu-id="8b587-680">Exemplo</span><span class="sxs-lookup"><span data-stu-id="8b587-680">Example</span></span>
```json
{
    "name": "AzureDataLakeStoreInput",
    "properties": {
        "type": "AzureDataLakeStore",
        "linkedServiceName": "AzureDataLakeStoreLinkedService",
        "typeProperties": {
            "folderPath": "datalake/input/",
            "fileName": "SearchLog.tsv",
            "format": {
                "type": "TextFormat",
                "rowDelimiter": "\n",
                "columnDelimiter": "\t"
            }
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```

<span data-ttu-id="8b587-681">Para saber mais, consulte o artigo [Conector do Azure Data Lake Store](data-factory-azure-datalake-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="8b587-681">For more information, see [Azure Data Lake Store connector](data-factory-azure-datalake-connector.md#dataset-properties) article.</span></span> 

### <a name="azure-data-lake-store-source-in-copy-activity"></a><span data-ttu-id="8b587-682">Fonte do Azure Data Lake Store na Atividade de Cópia</span><span class="sxs-lookup"><span data-stu-id="8b587-682">Azure Data Lake Store Source in Copy Activity</span></span>
<span data-ttu-id="8b587-683">Se você estiver copiando dados de um Azure Data Lake Store, defina o **source type** da atividade de cópia para **AzureDataLakeStoreSource** e especifique as propriedades a seguir na seção **source**:</span><span class="sxs-lookup"><span data-stu-id="8b587-683">If you are copying data from an Azure Data Lake Store, set the **source type** of the copy activity to **AzureDataLakeStoreSource**, and specify following properties in the **source** section:</span></span>

<span data-ttu-id="8b587-684">**AzureDataLakeStoreSource** dá suporte à seção **typeProperties** das seguintes propriedades:</span><span class="sxs-lookup"><span data-stu-id="8b587-684">**AzureDataLakeStoreSource** supports the following properties **typeProperties** section:</span></span>

| <span data-ttu-id="8b587-685">Propriedade</span><span class="sxs-lookup"><span data-stu-id="8b587-685">Property</span></span> | <span data-ttu-id="8b587-686">Descrição</span><span class="sxs-lookup"><span data-stu-id="8b587-686">Description</span></span> | <span data-ttu-id="8b587-687">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="8b587-687">Allowed values</span></span> | <span data-ttu-id="8b587-688">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="8b587-688">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="8b587-689">recursiva</span><span class="sxs-lookup"><span data-stu-id="8b587-689">recursive</span></span> |<span data-ttu-id="8b587-690">Indica se os dados são lidos recursivamente por meio de subpastas ou somente da pasta especificada.</span><span class="sxs-lookup"><span data-stu-id="8b587-690">Indicates whether the data is read recursively from the sub folders or only from the specified folder.</span></span> |<span data-ttu-id="8b587-691">True (valor padrão), False</span><span class="sxs-lookup"><span data-stu-id="8b587-691">True (default value), False</span></span> |<span data-ttu-id="8b587-692">Não</span><span class="sxs-lookup"><span data-stu-id="8b587-692">No</span></span> |

#### <a name="example-azuredatalakestoresource"></a><span data-ttu-id="8b587-693">Exemplo: AzureDataLakeStoreSource</span><span class="sxs-lookup"><span data-stu-id="8b587-693">Example: AzureDataLakeStoreSource</span></span>

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline for copy activity",
        "activities": [{
            "name": "AzureDakeLaketoBlob",
            "description": "copy activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureDataLakeStoreInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "AzureDataLakeStoreSource"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

<span data-ttu-id="8b587-694">Para saber mais, consulte o artigo [Conector do Azure Data Lake Store](data-factory-azure-datalake-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="8b587-694">For more information, see [Azure Data Lake Store connector](data-factory-azure-datalake-connector.md#copy-activity-properties) article.</span></span>

### <a name="azure-data-lake-store-sink-in-copy-activity"></a><span data-ttu-id="8b587-695">Coletor do Azure Data Lake Store na Atividade de Cópia</span><span class="sxs-lookup"><span data-stu-id="8b587-695">Azure Data Lake Store Sink in Copy Activity</span></span>
<span data-ttu-id="8b587-696">Se você estiver copiando dados para um Azure Data Lake Store, defina o **sink type** da atividade de cópia para **AzureDataLakeStoreSink** e especifique as propriedades a seguir na seção **sink**:</span><span class="sxs-lookup"><span data-stu-id="8b587-696">If you are copying data to an Azure Data Lake Store, set the **sink type** of the copy activity to **AzureDataLakeStoreSink**, and specify following properties in the **sink** section:</span></span>

| <span data-ttu-id="8b587-697">Propriedade</span><span class="sxs-lookup"><span data-stu-id="8b587-697">Property</span></span> | <span data-ttu-id="8b587-698">Descrição</span><span class="sxs-lookup"><span data-stu-id="8b587-698">Description</span></span> | <span data-ttu-id="8b587-699">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="8b587-699">Allowed values</span></span> | <span data-ttu-id="8b587-700">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="8b587-700">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="8b587-701">copyBehavior</span><span class="sxs-lookup"><span data-stu-id="8b587-701">copyBehavior</span></span> |<span data-ttu-id="8b587-702">Especifica o comportamento da cópia.</span><span class="sxs-lookup"><span data-stu-id="8b587-702">Specifies the copy behavior.</span></span> |<span data-ttu-id="8b587-703"><b>PreserveHierarchy:</b> preserva a hierarquia de arquivos na pasta de destino.</span><span class="sxs-lookup"><span data-stu-id="8b587-703"><b>PreserveHierarchy</b>: preserves the file hierarchy in the target folder.</span></span> <span data-ttu-id="8b587-704">O caminho relativo do arquivo de origem para a pasta de origem é idêntico ao caminho relativo do arquivo de destino para a pasta de destino.</span><span class="sxs-lookup"><span data-stu-id="8b587-704">The relative path of source file to source folder is identical to the relative path of target file to target folder.</span></span><br/><br/><span data-ttu-id="8b587-705"><b>FlattenHierarchy:</b> todos os arquivos da pasta de origem são criados no primeiro nível da pasta de destino.</span><span class="sxs-lookup"><span data-stu-id="8b587-705"><b>FlattenHierarchy</b>: all files from the source folder are created in the first level of target folder.</span></span> <span data-ttu-id="8b587-706">Os arquivos de destino são criados com o nome gerado automaticamente.</span><span class="sxs-lookup"><span data-stu-id="8b587-706">The target files are created with auto generated name.</span></span><br/><br/><span data-ttu-id="8b587-707"><b>MergeFiles:</b> mescla todos os arquivos da pasta de origem em um arquivo.</span><span class="sxs-lookup"><span data-stu-id="8b587-707"><b>MergeFiles</b>: merges all files from the source folder to one file.</span></span> <span data-ttu-id="8b587-708">Se o nome do arquivo/blob for especificado, o nome do arquivo mesclado será o nome especificado; caso contrário, será o nome de arquivo gerado automaticamente.</span><span class="sxs-lookup"><span data-stu-id="8b587-708">If the File/Blob Name is specified, the merged file name would be the specified name; otherwise, would be auto-generated file name.</span></span> |<span data-ttu-id="8b587-709">Não</span><span class="sxs-lookup"><span data-stu-id="8b587-709">No</span></span> |

#### <a name="example-azuredatalakestoresink"></a><span data-ttu-id="8b587-710">Exemplo: AzureDataLakeStoreSink</span><span class="sxs-lookup"><span data-stu-id="8b587-710">Example: AzureDataLakeStoreSink</span></span>
```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "AzureBlobtoDataLake",
            "description": "Copy Activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureBlobInput"
            }],
            "outputs": [{
                "name": "AzureDataLakeStoreOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "BlobSource"
                },
                "sink": {
                    "type": "AzureDataLakeStoreSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

<span data-ttu-id="8b587-711">Para saber mais, consulte o artigo [Conector do Azure Data Lake Store](data-factory-azure-datalake-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="8b587-711">For more information, see [Azure Data Lake Store connector](data-factory-azure-datalake-connector.md#copy-activity-properties) article.</span></span> 

## <a name="azure-cosmos-db"></a><span data-ttu-id="8b587-712">Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="8b587-712">Azure Cosmos DB</span></span>  

### <a name="linked-service"></a><span data-ttu-id="8b587-713">Serviço vinculado</span><span class="sxs-lookup"><span data-stu-id="8b587-713">Linked service</span></span>
<span data-ttu-id="8b587-714">Para definir um serviço vinculado do Azure Cosmos DB, defina o **type** do serviço vinculado como **DocumentDb** e especifique as seguintes propriedades na seção **typeProperties**:</span><span class="sxs-lookup"><span data-stu-id="8b587-714">To define an Azure Cosmos DB linked service, set the **type** of the linked service to **DocumentDb**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="8b587-715">**Propriedade**</span><span class="sxs-lookup"><span data-stu-id="8b587-715">**Property**</span></span> | <span data-ttu-id="8b587-716">**Descrição**</span><span class="sxs-lookup"><span data-stu-id="8b587-716">**Description**</span></span> | <span data-ttu-id="8b587-717">**Obrigatório**</span><span class="sxs-lookup"><span data-stu-id="8b587-717">**Required**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8b587-718">connectionString</span><span class="sxs-lookup"><span data-stu-id="8b587-718">connectionString</span></span> |<span data-ttu-id="8b587-719">Especifique as informações necessárias para se conectar ao banco de dados do Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="8b587-719">Specify information needed to connect to Azure Cosmos DB database.</span></span> |<span data-ttu-id="8b587-720">Sim</span><span class="sxs-lookup"><span data-stu-id="8b587-720">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="8b587-721">Exemplo</span><span class="sxs-lookup"><span data-stu-id="8b587-721">Example</span></span>

```json
{
    "name": "CosmosDBLinkedService",
    "properties": {
        "type": "DocumentDb",
        "typeProperties": {
            "connectionString": "AccountEndpoint=<EndpointUrl>;AccountKey=<AccessKey>;Database=<Database>"
        }
    }
}
```
<span data-ttu-id="8b587-722">Para obter mais informações, consulte o artigo [Conector do Azure Cosmos DB](data-factory-azure-documentdb-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="8b587-722">For more information, see [Azure Cosmos DB connector](data-factory-azure-documentdb-connector.md#linked-service-properties) article.</span></span>

### <a name="dataset"></a><span data-ttu-id="8b587-723">Conjunto de dados</span><span class="sxs-lookup"><span data-stu-id="8b587-723">Dataset</span></span>
<span data-ttu-id="8b587-724">Para definir um conjunto de dados do Azure Cosmos DB, defina o **type** do conjunto de dados como **DocumentDbCollection** e especifique as seguintes propriedades na seção **typeProperties**:</span><span class="sxs-lookup"><span data-stu-id="8b587-724">To define an Azure Cosmos DB dataset, set the **type** of the dataset to **DocumentDbCollection**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="8b587-725">**Propriedade**</span><span class="sxs-lookup"><span data-stu-id="8b587-725">**Property**</span></span> | <span data-ttu-id="8b587-726">**Descrição**</span><span class="sxs-lookup"><span data-stu-id="8b587-726">**Description**</span></span> | <span data-ttu-id="8b587-727">**Obrigatório**</span><span class="sxs-lookup"><span data-stu-id="8b587-727">**Required**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8b587-728">collectionName</span><span class="sxs-lookup"><span data-stu-id="8b587-728">collectionName</span></span> |<span data-ttu-id="8b587-729">Nome da coleção do Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="8b587-729">Name of the Azure Cosmos DB collection.</span></span> |<span data-ttu-id="8b587-730">Sim</span><span class="sxs-lookup"><span data-stu-id="8b587-730">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="8b587-731">Exemplo</span><span class="sxs-lookup"><span data-stu-id="8b587-731">Example</span></span>

```json
{
    "name": "PersonCosmosDBTable",
    "properties": {
        "type": "DocumentDbCollection",
        "linkedServiceName": "CosmosDBLinkedService",
        "typeProperties": {
            "collectionName": "Person"
        },
        "external": true,
        "availability": {
            "frequency": "Day",
            "interval": 1
        }
    }
}
```
<span data-ttu-id="8b587-732">Para obter mais informações, consulte o artigo [Conector do Azure Cosmos DB](data-factory-azure-documentdb-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="8b587-732">For more information, see [Azure Cosmos DB connector](data-factory-azure-documentdb-connector.md#dataset-properties) article.</span></span>

### <a name="azure-cosmos-db-collection-source-in-copy-activity"></a><span data-ttu-id="8b587-733">Fonte de coleta do Azure Cosmos DB na Atividade de Cópia</span><span class="sxs-lookup"><span data-stu-id="8b587-733">Azure Cosmos DB Collection Source in Copy Activity</span></span>
<span data-ttu-id="8b587-734">Se você estiver copiando dados de um Azure Cosmos DB, defina o **source type** da atividade de cópia como **DocumentDbCollectionSource** e especifique as seguintes propriedades na seção **source**:</span><span class="sxs-lookup"><span data-stu-id="8b587-734">If you are copying data from an Azure Cosmos DB, set the **source type** of the copy activity to **DocumentDbCollectionSource**, and specify following properties in the **source** section:</span></span>


| <span data-ttu-id="8b587-735">**Propriedade**</span><span class="sxs-lookup"><span data-stu-id="8b587-735">**Property**</span></span> | <span data-ttu-id="8b587-736">**Descrição**</span><span class="sxs-lookup"><span data-stu-id="8b587-736">**Description**</span></span> | <span data-ttu-id="8b587-737">**Valores permitidos**</span><span class="sxs-lookup"><span data-stu-id="8b587-737">**Allowed values**</span></span> | <span data-ttu-id="8b587-738">**Obrigatório**</span><span class="sxs-lookup"><span data-stu-id="8b587-738">**Required**</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="8b587-739">query</span><span class="sxs-lookup"><span data-stu-id="8b587-739">query</span></span> |<span data-ttu-id="8b587-740">Especifique a consulta para ler dados.</span><span class="sxs-lookup"><span data-stu-id="8b587-740">Specify the query to read data.</span></span> |<span data-ttu-id="8b587-741">Cadeia de consulta com suporte no Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="8b587-741">Query string supported by Azure Cosmos DB.</span></span> <br/><br/><span data-ttu-id="8b587-742">Exemplo: `SELECT c.BusinessEntityID, c.PersonType, c.NameStyle, c.Title, c.Name.First AS FirstName, c.Name.Last AS LastName, c.Suffix, c.EmailPromotion FROM c WHERE c.ModifiedDate > \"2009-01-01T00:00:00\"`</span><span class="sxs-lookup"><span data-stu-id="8b587-742">Example: `SELECT c.BusinessEntityID, c.PersonType, c.NameStyle, c.Title, c.Name.First AS FirstName, c.Name.Last AS LastName, c.Suffix, c.EmailPromotion FROM c WHERE c.ModifiedDate > \"2009-01-01T00:00:00\"`</span></span> |<span data-ttu-id="8b587-743">Não</span><span class="sxs-lookup"><span data-stu-id="8b587-743">No</span></span> <br/><br/><span data-ttu-id="8b587-744">Se não for especificada, a instrução SQL executada será: `select <columns defined in structure> from mycollection`</span><span class="sxs-lookup"><span data-stu-id="8b587-744">If not specified, the SQL statement that is executed: `select <columns defined in structure> from mycollection`</span></span> |
| <span data-ttu-id="8b587-745">nestingSeparator</span><span class="sxs-lookup"><span data-stu-id="8b587-745">nestingSeparator</span></span> |<span data-ttu-id="8b587-746">Caractere especial para indicar que o documento está aninhado</span><span class="sxs-lookup"><span data-stu-id="8b587-746">Special character to indicate that the document is nested</span></span> |<span data-ttu-id="8b587-747">Qualquer caractere.</span><span class="sxs-lookup"><span data-stu-id="8b587-747">Any character.</span></span> <br/><br/><span data-ttu-id="8b587-748">O Azure Cosmos DB é um repositório NoSQL para documentos JSON, em que estruturas aninhadas são permitidas.</span><span class="sxs-lookup"><span data-stu-id="8b587-748">Azure Cosmos DB is a NoSQL store for JSON documents, where nested structures are allowed.</span></span> <span data-ttu-id="8b587-749">O Azure Data Factory permite que o usuário indique a hierarquia via nestingSeparator, que é "."</span><span class="sxs-lookup"><span data-stu-id="8b587-749">Azure Data Factory enables user to denote hierarchy via nestingSeparator, which is “.”</span></span> <span data-ttu-id="8b587-750">nos exemplos acima.</span><span class="sxs-lookup"><span data-stu-id="8b587-750">in the above examples.</span></span> <span data-ttu-id="8b587-751">Com o separador, a atividade de cópia vai gerar o objeto "Name" com três elementos filhos First, Middle e Last, de acordo com "Name.First", "Name.Middle" e "Name.Last" na definição da tabela.</span><span class="sxs-lookup"><span data-stu-id="8b587-751">With the separator, the copy activity will generate the “Name” object with three children elements First, Middle and Last, according to “Name.First”, “Name.Middle” and “Name.Last” in the table definition.</span></span> |<span data-ttu-id="8b587-752">Não</span><span class="sxs-lookup"><span data-stu-id="8b587-752">No</span></span> |

#### <a name="example"></a><span data-ttu-id="8b587-753">Exemplo</span><span class="sxs-lookup"><span data-stu-id="8b587-753">Example</span></span>

```json
{
    "name": "DocDbToBlobPipeline",
    "properties": {
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "DocumentDbCollectionSource",
                    "query": "SELECT Person.Id, Person.Name.First AS FirstName, Person.Name.Middle as MiddleName, Person.Name.Last AS LastName FROM Person",
                    "nestingSeparator": "."
                },
                "sink": {
                    "type": "BlobSink",
                    "blobWriterAddHeader": true,
                    "writeBatchSize": 1000,
                    "writeBatchTimeout": "00:00:59"
                }
            },
            "inputs": [{
                "name": "PersonCosmosDBTable"
            }],
            "outputs": [{
                "name": "PersonBlobTableOut"
            }],
            "policy": {
                "concurrency": 1
            },
            "name": "CopyFromCosmosDbToBlob"
        }],
        "start": "2016-04-01T00:00:00",
        "end": "2016-04-02T00:00:00"
    }
}
```

### <a name="azure-cosmos-db-collection-sink-in-copy-activity"></a><span data-ttu-id="8b587-754">Coletor para coleta do Azure Cosmos DB na Atividade de Cópia</span><span class="sxs-lookup"><span data-stu-id="8b587-754">Azure Cosmos DB Collection Sink in Copy Activity</span></span>
<span data-ttu-id="8b587-755">Se você estiver copiando dados para um Azure Cosmos DB, defina o **sink type** da atividade de cópia como **DocumentDbCollectionSink** e especifique as seguintes propriedades na seção **sink**:</span><span class="sxs-lookup"><span data-stu-id="8b587-755">If you are copying data to Azure Cosmos DB, set the **sink type** of the copy activity to **DocumentDbCollectionSink**, and specify following properties in the **sink** section:</span></span>

| <span data-ttu-id="8b587-756">**Propriedade**</span><span class="sxs-lookup"><span data-stu-id="8b587-756">**Property**</span></span> | <span data-ttu-id="8b587-757">**Descrição**</span><span class="sxs-lookup"><span data-stu-id="8b587-757">**Description**</span></span> | <span data-ttu-id="8b587-758">**Valores permitidos**</span><span class="sxs-lookup"><span data-stu-id="8b587-758">**Allowed values**</span></span> | <span data-ttu-id="8b587-759">**Obrigatório**</span><span class="sxs-lookup"><span data-stu-id="8b587-759">**Required**</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="8b587-760">nestingSeparator</span><span class="sxs-lookup"><span data-stu-id="8b587-760">nestingSeparator</span></span> |<span data-ttu-id="8b587-761">Um caractere especial no nome da coluna de fonte para indicar que esse documento aninhado é necessário.</span><span class="sxs-lookup"><span data-stu-id="8b587-761">A special character in the source column name to indicate that nested document is needed.</span></span> <br/><br/><span data-ttu-id="8b587-762">No exemplo acima: `Name.First` na tabela de saída produz a seguinte estrutura JSON no documento do Cosmos DB:</span><span class="sxs-lookup"><span data-stu-id="8b587-762">For example above: `Name.First` in the output table produces the following JSON structure in the Cosmos DB document:</span></span><br/><br/><span data-ttu-id="8b587-763">"Name": {</span><span class="sxs-lookup"><span data-stu-id="8b587-763">"Name": {</span></span><br/>    <span data-ttu-id="8b587-764">"First": "John"</span><span class="sxs-lookup"><span data-stu-id="8b587-764">"First": "John"</span></span><br/><span data-ttu-id="8b587-765">},</span><span class="sxs-lookup"><span data-stu-id="8b587-765">},</span></span> |<span data-ttu-id="8b587-766">Caractere que é usado para separar os níveis de aninhamento.</span><span class="sxs-lookup"><span data-stu-id="8b587-766">Character that is used to separate nesting levels.</span></span><br/><br/><span data-ttu-id="8b587-767">O valor padrão é `.` (ponto).</span><span class="sxs-lookup"><span data-stu-id="8b587-767">Default value is `.` (dot).</span></span> |<span data-ttu-id="8b587-768">Caractere que é usado para separar os níveis de aninhamento.</span><span class="sxs-lookup"><span data-stu-id="8b587-768">Character that is used to separate nesting levels.</span></span> <br/><br/><span data-ttu-id="8b587-769">O valor padrão é `.` (ponto).</span><span class="sxs-lookup"><span data-stu-id="8b587-769">Default value is `.` (dot).</span></span> |
| <span data-ttu-id="8b587-770">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="8b587-770">writeBatchSize</span></span> |<span data-ttu-id="8b587-771">Número de solicitações paralelas ao serviço Azure Cosmos DB para criar documentos.</span><span class="sxs-lookup"><span data-stu-id="8b587-771">Number of parallel requests to Azure Cosmos DB service to create documents.</span></span><br/><br/><span data-ttu-id="8b587-772">Você pode ajustar o desempenho ao copiar dados de/para o Azure Cosmos DB usando essa propriedade.</span><span class="sxs-lookup"><span data-stu-id="8b587-772">You can fine-tune the performance when copying data to/from Azure Cosmos DB by using this property.</span></span> <span data-ttu-id="8b587-773">Você pode esperar um melhor desempenho ao aumentar writeBatchSize, pois mais solicitações paralelas para o Azure Cosmos DB são enviadas.</span><span class="sxs-lookup"><span data-stu-id="8b587-773">You can expect a better performance when you increase writeBatchSize because more parallel requests to Azure Cosmos DB are sent.</span></span> <span data-ttu-id="8b587-774">No entanto, será necessário evitar a limitação que pode gerar a mensagem de erro: "A taxa de solicitação é grande".</span><span class="sxs-lookup"><span data-stu-id="8b587-774">However you’ll need to avoid throttling that can throw the error message: "Request rate is large".</span></span><br/><br/><span data-ttu-id="8b587-775">A limitação é decida por uma série de fatores, incluindo o tamanho dos documentos, o número de termos incluídos, a política de indexação da coleção de destino, etc. Para operações de cópia, você pode usar uma coleção melhor (por exemplo, S3) para ter mais taxa de transferência disponível (solicitação de 2.500 unidades/segundo).</span><span class="sxs-lookup"><span data-stu-id="8b587-775">Throttling is decided by a number of factors, including size of documents, number of terms in documents, indexing policy of target collection, etc. For copy operations, you can use a better collection (for example, S3) to have the most throughput available (2,500 request units/second).</span></span> |<span data-ttu-id="8b587-776">Número inteiro</span><span class="sxs-lookup"><span data-stu-id="8b587-776">Integer</span></span> |<span data-ttu-id="8b587-777">Não (padrão: 5)</span><span class="sxs-lookup"><span data-stu-id="8b587-777">No (default: 5)</span></span> |
| <span data-ttu-id="8b587-778">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="8b587-778">writeBatchTimeout</span></span> |<span data-ttu-id="8b587-779">Tempo de espera para a operação ser concluída antes de atingir o tempo limite.</span><span class="sxs-lookup"><span data-stu-id="8b587-779">Wait time for the operation to complete before it times out.</span></span> |<span data-ttu-id="8b587-780">timespan</span><span class="sxs-lookup"><span data-stu-id="8b587-780">timespan</span></span><br/><br/> <span data-ttu-id="8b587-781">Exemplo: "00:30:00" (30 minutos).</span><span class="sxs-lookup"><span data-stu-id="8b587-781">Example: “00:30:00” (30 minutes).</span></span> |<span data-ttu-id="8b587-782">Não</span><span class="sxs-lookup"><span data-stu-id="8b587-782">No</span></span> |

#### <a name="example"></a><span data-ttu-id="8b587-783">Exemplo</span><span class="sxs-lookup"><span data-stu-id="8b587-783">Example</span></span>

```json
{
    "name": "BlobToDocDbPipeline",
    "properties": {
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "BlobSource"
                },
                "sink": {
                    "type": "DocumentDbCollectionSink",
                    "nestingSeparator": ".",
                    "writeBatchSize": 2,
                    "writeBatchTimeout": "00:00:00"
                },
                "translator": {
                    "type": "TabularTranslator",
                    "ColumnMappings": "FirstName: Name.First, MiddleName: Name.Middle, LastName: Name.Last, BusinessEntityID: BusinessEntityID, PersonType: PersonType, NameStyle: NameStyle, Title: Title, Suffix: Suffix"
                }
            },
            "inputs": [{
                "name": "PersonBlobTableIn"
            }],
            "outputs": [{
                "name": "PersonCosmosDbTableOut"
            }],
            "policy": {
                "concurrency": 1
            },
            "name": "CopyFromBlobToCosmosDb"
        }],
        "start": "2016-04-14T00:00:00",
        "end": "2016-04-15T00:00:00"
    }
}
```

<span data-ttu-id="8b587-784">Para obter mais informações, consulte o artigo [Conector do Azure Cosmos DB](data-factory-azure-documentdb-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="8b587-784">For more information, see [Azure Cosmos DB connector](data-factory-azure-documentdb-connector.md#copy-activity-properties) article.</span></span>

## <a name="azure-sql-database"></a><span data-ttu-id="8b587-785">Banco de Dados SQL do Azure</span><span class="sxs-lookup"><span data-stu-id="8b587-785">Azure SQL Database</span></span>

### <a name="linked-service"></a><span data-ttu-id="8b587-786">Serviço vinculado</span><span class="sxs-lookup"><span data-stu-id="8b587-786">Linked service</span></span>
<span data-ttu-id="8b587-787">Para definir um serviço vinculado do Banco de Dados SQL do Azure, defina o **type** do serviço vinculado para **AzureSqlDatabase** e especifique as propriedades a seguir na seção **typeProperties**:</span><span class="sxs-lookup"><span data-stu-id="8b587-787">To define an Azure SQL Database linked service, set the **type** of the linked service to **AzureSqlDatabase**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="8b587-788">Propriedade</span><span class="sxs-lookup"><span data-stu-id="8b587-788">Property</span></span> | <span data-ttu-id="8b587-789">Descrição</span><span class="sxs-lookup"><span data-stu-id="8b587-789">Description</span></span> | <span data-ttu-id="8b587-790">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="8b587-790">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8b587-791">connectionString</span><span class="sxs-lookup"><span data-stu-id="8b587-791">connectionString</span></span> |<span data-ttu-id="8b587-792">Especifique as informações necessárias para se conectar à instância do Banco de Dados SQL Azure para a propriedade connectionString.</span><span class="sxs-lookup"><span data-stu-id="8b587-792">Specify information needed to connect to the Azure SQL Database instance for the connectionString property.</span></span> |<span data-ttu-id="8b587-793">Sim</span><span class="sxs-lookup"><span data-stu-id="8b587-793">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="8b587-794">Exemplo</span><span class="sxs-lookup"><span data-stu-id="8b587-794">Example</span></span>
```json
{
    "name": "AzureSqlLinkedService",
    "properties": {
        "type": "AzureSqlDatabase",
        "typeProperties": {
            "connectionString": "Server=tcp:<servername>.database.windows.net,1433;Database=<databasename>;User ID=<username>@<servername>;Password=<password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
        }
    }
}
```

<span data-ttu-id="8b587-795">Para obter mais informações, consulte o artigo [Conector de SQL do Azure](data-factory-azure-sql-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="8b587-795">For more information, see [Azure SQL connector](data-factory-azure-sql-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="8b587-796">Conjunto de dados</span><span class="sxs-lookup"><span data-stu-id="8b587-796">Dataset</span></span>
<span data-ttu-id="8b587-797">Para definir um conjunto de dados do Banco de Dados SQL do Azure, defina o **type** do conjunto de dados para **AzureSqlTable** e especifique as propriedades a seguir na seção **typeProperties**:</span><span class="sxs-lookup"><span data-stu-id="8b587-797">To define an Azure SQL Database dataset, set the **type** of the dataset to **AzureSqlTable**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="8b587-798">Propriedade</span><span class="sxs-lookup"><span data-stu-id="8b587-798">Property</span></span> | <span data-ttu-id="8b587-799">Descrição</span><span class="sxs-lookup"><span data-stu-id="8b587-799">Description</span></span> | <span data-ttu-id="8b587-800">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="8b587-800">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8b587-801">tableName</span><span class="sxs-lookup"><span data-stu-id="8b587-801">tableName</span></span> |<span data-ttu-id="8b587-802">Nome da tabela ou exibição na instância do Banco de Dados SQL Azure à qual o serviço vinculado se refere.</span><span class="sxs-lookup"><span data-stu-id="8b587-802">Name of the table or view in the Azure SQL Database instance that linked service refers to.</span></span> |<span data-ttu-id="8b587-803">Sim</span><span class="sxs-lookup"><span data-stu-id="8b587-803">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="8b587-804">Exemplo</span><span class="sxs-lookup"><span data-stu-id="8b587-804">Example</span></span>

```json
{
    "name": "AzureSqlInput",
    "properties": {
        "type": "AzureSqlTable",
        "linkedServiceName": "AzureSqlLinkedService",
        "typeProperties": {
            "tableName": "MyTable"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```
<span data-ttu-id="8b587-805">Para obter mais informações, consulte o artigo [Conector de SQL do Azure](data-factory-azure-sql-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="8b587-805">For more information, see [Azure SQL connector](data-factory-azure-sql-connector.md#dataset-properties) article.</span></span> 

### <a name="sql-source-in-copy-activity"></a><span data-ttu-id="8b587-806">Origem do SQL na atividade de cópia</span><span class="sxs-lookup"><span data-stu-id="8b587-806">SQL Source in Copy Activity</span></span>
<span data-ttu-id="8b587-807">Se você estiver copiando dados de um Banco de Dados SQL do Azure, defina o **source type** da atividade de cópia para **SqlSource** e especifique as propriedades a seguir na seção **source**:</span><span class="sxs-lookup"><span data-stu-id="8b587-807">If you are copying data from an Azure SQL Database, set the **source type** of the copy activity to **SqlSource**, and specify following properties in the **source** section:</span></span>


| <span data-ttu-id="8b587-808">Propriedade</span><span class="sxs-lookup"><span data-stu-id="8b587-808">Property</span></span> | <span data-ttu-id="8b587-809">Descrição</span><span class="sxs-lookup"><span data-stu-id="8b587-809">Description</span></span> | <span data-ttu-id="8b587-810">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="8b587-810">Allowed values</span></span> | <span data-ttu-id="8b587-811">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="8b587-811">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="8b587-812">SqlReaderQuery</span><span class="sxs-lookup"><span data-stu-id="8b587-812">sqlReaderQuery</span></span> |<span data-ttu-id="8b587-813">Utiliza a consulta personalizada para ler os dados.</span><span class="sxs-lookup"><span data-stu-id="8b587-813">Use the custom query to read data.</span></span> |<span data-ttu-id="8b587-814">Cadeia de caracteres de consulta SQL.</span><span class="sxs-lookup"><span data-stu-id="8b587-814">SQL query string.</span></span> <span data-ttu-id="8b587-815">Exemplo: `select * from MyTable`.</span><span class="sxs-lookup"><span data-stu-id="8b587-815">Example: `select * from MyTable`.</span></span> |<span data-ttu-id="8b587-816">Não</span><span class="sxs-lookup"><span data-stu-id="8b587-816">No</span></span> |
| <span data-ttu-id="8b587-817">sqlReaderStoredProcedureName</span><span class="sxs-lookup"><span data-stu-id="8b587-817">sqlReaderStoredProcedureName</span></span> |<span data-ttu-id="8b587-818">Nome do procedimento armazenado que lê os dados da tabela de origem.</span><span class="sxs-lookup"><span data-stu-id="8b587-818">Name of the stored procedure that reads data from the source table.</span></span> |<span data-ttu-id="8b587-819">Nome do procedimento armazenado.</span><span class="sxs-lookup"><span data-stu-id="8b587-819">Name of the stored procedure.</span></span> |<span data-ttu-id="8b587-820">Não</span><span class="sxs-lookup"><span data-stu-id="8b587-820">No</span></span> |
| <span data-ttu-id="8b587-821">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="8b587-821">storedProcedureParameters</span></span> |<span data-ttu-id="8b587-822">Parâmetros para o procedimento armazenado.</span><span class="sxs-lookup"><span data-stu-id="8b587-822">Parameters for the stored procedure.</span></span> |<span data-ttu-id="8b587-823">Pares de nome/valor.</span><span class="sxs-lookup"><span data-stu-id="8b587-823">Name/value pairs.</span></span> <span data-ttu-id="8b587-824">Nomes e uso de maiúsculas e minúsculas de parâmetros devem corresponder aos nomes e o uso de maiúsculas e minúsculas dos parâmetros do procedimento armazenado.</span><span class="sxs-lookup"><span data-stu-id="8b587-824">Names and casing of parameters must match the names and casing of the stored procedure parameters.</span></span> |<span data-ttu-id="8b587-825">Não</span><span class="sxs-lookup"><span data-stu-id="8b587-825">No</span></span> |

#### <a name="example"></a><span data-ttu-id="8b587-826">Exemplo</span><span class="sxs-lookup"><span data-stu-id="8b587-826">Example</span></span>

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline for copy activity",
        "activities": [{
            "name": "AzureSQLtoBlob",
            "description": "copy activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureSQLInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "SqlSource",
                    "SqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```
<span data-ttu-id="8b587-827">Para obter mais informações, consulte o artigo [Conector de SQL do Azure](data-factory-azure-sql-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="8b587-827">For more information, see [Azure SQL connector](data-factory-azure-sql-connector.md#copy-activity-properties) article.</span></span> 

### <a name="sql-sink-in-copy-activity"></a><span data-ttu-id="8b587-828">Coletor do SQL na Atividade de Cópia</span><span class="sxs-lookup"><span data-stu-id="8b587-828">SQL Sink in Copy Activity</span></span>
<span data-ttu-id="8b587-829">Se você estiver copiando dados para um Banco de Dados SQL do Azure, defina o **sink type** da atividade de cópia para **SqlSink** e especifique as propriedades a seguir na seção **sink**:</span><span class="sxs-lookup"><span data-stu-id="8b587-829">If you are copying data to Azure SQL Database, set the **sink type** of the copy activity to **SqlSink**, and specify following properties in the **sink** section:</span></span>

| <span data-ttu-id="8b587-830">Propriedade</span><span class="sxs-lookup"><span data-stu-id="8b587-830">Property</span></span> | <span data-ttu-id="8b587-831">Descrição</span><span class="sxs-lookup"><span data-stu-id="8b587-831">Description</span></span> | <span data-ttu-id="8b587-832">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="8b587-832">Allowed values</span></span> | <span data-ttu-id="8b587-833">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="8b587-833">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="8b587-834">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="8b587-834">writeBatchTimeout</span></span> |<span data-ttu-id="8b587-835">Tempo de espera para a operação de inserção em lotes ser concluída antes de atingir o tempo limite.</span><span class="sxs-lookup"><span data-stu-id="8b587-835">Wait time for the batch insert operation to complete before it times out.</span></span> |<span data-ttu-id="8b587-836">timespan</span><span class="sxs-lookup"><span data-stu-id="8b587-836">timespan</span></span><br/><br/> <span data-ttu-id="8b587-837">Exemplo: "00:30:00" (30 minutos).</span><span class="sxs-lookup"><span data-stu-id="8b587-837">Example: “00:30:00” (30 minutes).</span></span> |<span data-ttu-id="8b587-838">Não</span><span class="sxs-lookup"><span data-stu-id="8b587-838">No</span></span> |
| <span data-ttu-id="8b587-839">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="8b587-839">writeBatchSize</span></span> |<span data-ttu-id="8b587-840">Insere dados na tabela SQL quando o tamanho do buffer atinge writeBatchSize.</span><span class="sxs-lookup"><span data-stu-id="8b587-840">Inserts data into the SQL table when the buffer size reaches writeBatchSize.</span></span> |<span data-ttu-id="8b587-841">Inteiro (número de linhas)</span><span class="sxs-lookup"><span data-stu-id="8b587-841">Integer (number of rows)</span></span> |<span data-ttu-id="8b587-842">Não (padrão: 10000)</span><span class="sxs-lookup"><span data-stu-id="8b587-842">No (default: 10000)</span></span> |
| <span data-ttu-id="8b587-843">sqlWriterCleanupScript</span><span class="sxs-lookup"><span data-stu-id="8b587-843">sqlWriterCleanupScript</span></span> |<span data-ttu-id="8b587-844">Especifique uma consulta da Atividade de Cópia a executar para que os dados de uma fatia específica sejam removidos.</span><span class="sxs-lookup"><span data-stu-id="8b587-844">Specify a query for Copy Activity to execute such that data of a specific slice is cleaned up.</span></span> |<span data-ttu-id="8b587-845">Uma instrução de consulta.</span><span class="sxs-lookup"><span data-stu-id="8b587-845">A query statement.</span></span> |<span data-ttu-id="8b587-846">Não</span><span class="sxs-lookup"><span data-stu-id="8b587-846">No</span></span> |
| <span data-ttu-id="8b587-847">sliceIdentifierColumnName</span><span class="sxs-lookup"><span data-stu-id="8b587-847">sliceIdentifierColumnName</span></span> |<span data-ttu-id="8b587-848">Especifique um nome de coluna para a Atividade de Cópia a preencher com o identificador de fatias gerado automaticamente, que é usado para limpar os dados de uma fatia específica ao executar novamente.</span><span class="sxs-lookup"><span data-stu-id="8b587-848">Specify a column name for Copy Activity to fill with auto generated slice identifier, which is used to clean up data of a specific slice when rerun.</span></span> |<span data-ttu-id="8b587-849">Nome de uma coluna com tipo de dados de binário (32).</span><span class="sxs-lookup"><span data-stu-id="8b587-849">Column name of a column with data type of binary(32).</span></span> |<span data-ttu-id="8b587-850">Não</span><span class="sxs-lookup"><span data-stu-id="8b587-850">No</span></span> |
| <span data-ttu-id="8b587-851">sqlWriterStoredProcedureName</span><span class="sxs-lookup"><span data-stu-id="8b587-851">sqlWriterStoredProcedureName</span></span> |<span data-ttu-id="8b587-852">Nome do procedimento armazenado que upserts (atualiza/insere) na tabela de destino.</span><span class="sxs-lookup"><span data-stu-id="8b587-852">Name of the stored procedure that upserts (updates/inserts) data into the target table.</span></span> |<span data-ttu-id="8b587-853">Nome do procedimento armazenado.</span><span class="sxs-lookup"><span data-stu-id="8b587-853">Name of the stored procedure.</span></span> |<span data-ttu-id="8b587-854">Não</span><span class="sxs-lookup"><span data-stu-id="8b587-854">No</span></span> |
| <span data-ttu-id="8b587-855">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="8b587-855">storedProcedureParameters</span></span> |<span data-ttu-id="8b587-856">Parâmetros para o procedimento armazenado.</span><span class="sxs-lookup"><span data-stu-id="8b587-856">Parameters for the stored procedure.</span></span> |<span data-ttu-id="8b587-857">Pares de nome/valor.</span><span class="sxs-lookup"><span data-stu-id="8b587-857">Name/value pairs.</span></span> <span data-ttu-id="8b587-858">Nomes e uso de maiúsculas e minúsculas de parâmetros devem corresponder aos nomes e o uso de maiúsculas e minúsculas dos parâmetros do procedimento armazenado.</span><span class="sxs-lookup"><span data-stu-id="8b587-858">Names and casing of parameters must match the names and casing of the stored procedure parameters.</span></span> |<span data-ttu-id="8b587-859">Não</span><span class="sxs-lookup"><span data-stu-id="8b587-859">No</span></span> |
| <span data-ttu-id="8b587-860">sqlWriterTableType</span><span class="sxs-lookup"><span data-stu-id="8b587-860">sqlWriterTableType</span></span> |<span data-ttu-id="8b587-861">Especifique um nome do tipo de tabela a ser usado no procedimento armazenado.</span><span class="sxs-lookup"><span data-stu-id="8b587-861">Specify a table type name to be used in the stored procedure.</span></span> <span data-ttu-id="8b587-862">A atividade de cópia disponibiliza aqueles dados sendo movidos em uma tabela temporária com esse tipo de tabela.</span><span class="sxs-lookup"><span data-stu-id="8b587-862">Copy activity makes the data being moved available in a temp table with this table type.</span></span> <span data-ttu-id="8b587-863">O código de procedimento armazenado pode mesclar os dados sendo copiados com dados existentes.</span><span class="sxs-lookup"><span data-stu-id="8b587-863">Stored procedure code can then merge the data being copied with existing data.</span></span> |<span data-ttu-id="8b587-864">Um nome de tipo de tabela.</span><span class="sxs-lookup"><span data-stu-id="8b587-864">A table type name.</span></span> |<span data-ttu-id="8b587-865">Não</span><span class="sxs-lookup"><span data-stu-id="8b587-865">No</span></span> |

#### <a name="example"></a><span data-ttu-id="8b587-866">Exemplo</span><span class="sxs-lookup"><span data-stu-id="8b587-866">Example</span></span>

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "AzureBlobtoSQL",
            "description": "Copy Activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureBlobInput"
            }],
            "outputs": [{
                "name": "AzureSqlOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "BlobSource",
                    "blobColumnSeparators": ","
                },
                "sink": {
                    "type": "SqlSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

<span data-ttu-id="8b587-867">Para obter mais informações, consulte o artigo [Conector de SQL do Azure](data-factory-azure-sql-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="8b587-867">For more information, see [Azure SQL connector](data-factory-azure-sql-connector.md#copy-activity-properties) article.</span></span> 

## <a name="azure-sql-data-warehouse"></a><span data-ttu-id="8b587-868">SQL Data Warehouse do Azure</span><span class="sxs-lookup"><span data-stu-id="8b587-868">Azure SQL Data Warehouse</span></span>

### <a name="linked-service"></a><span data-ttu-id="8b587-869">Serviço vinculado</span><span class="sxs-lookup"><span data-stu-id="8b587-869">Linked service</span></span>
<span data-ttu-id="8b587-870">Para definir um serviço vinculado do SQL Data Warehouse do Azure, defina o **type** do serviço vinculado para **AzureSqlDW** e especifique as propriedades a seguir na seção **typeProperties**:</span><span class="sxs-lookup"><span data-stu-id="8b587-870">To define an Azure SQL Data Warehouse linked service, set the **type** of the linked service to **AzureSqlDW**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="8b587-871">Propriedade</span><span class="sxs-lookup"><span data-stu-id="8b587-871">Property</span></span> | <span data-ttu-id="8b587-872">Descrição</span><span class="sxs-lookup"><span data-stu-id="8b587-872">Description</span></span> | <span data-ttu-id="8b587-873">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="8b587-873">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8b587-874">connectionString</span><span class="sxs-lookup"><span data-stu-id="8b587-874">connectionString</span></span> |<span data-ttu-id="8b587-875">Especifique as informações necessárias para se conectar à instância do SQL Data Warehouse do Azure para a propriedade connectionString.</span><span class="sxs-lookup"><span data-stu-id="8b587-875">Specify information needed to connect to the Azure SQL Data Warehouse instance for the connectionString property.</span></span> |<span data-ttu-id="8b587-876">Sim</span><span class="sxs-lookup"><span data-stu-id="8b587-876">Yes</span></span> |



#### <a name="example"></a><span data-ttu-id="8b587-877">Exemplo</span><span class="sxs-lookup"><span data-stu-id="8b587-877">Example</span></span>

```json
{
    "name": "AzureSqlDWLinkedService",
    "properties": {
        "type": "AzureSqlDW",
        "typeProperties": {
            "connectionString": "Server=tcp:<servername>.database.windows.net,1433;Database=<databasename>;User ID=<username>@<servername>;Password=<password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
        }
    }
}
```

<span data-ttu-id="8b587-878">Para obter mais informações, consulte o artigo [Conector do SQL Data Warehouse do Azure](data-factory-azure-sql-data-warehouse-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="8b587-878">For more information, see [Azure SQL Data Warehouse connector](data-factory-azure-sql-data-warehouse-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="8b587-879">Conjunto de dados</span><span class="sxs-lookup"><span data-stu-id="8b587-879">Dataset</span></span>
<span data-ttu-id="8b587-880">Para definir um conjunto de dados do SQL Data Warehouse do Azure, defina o **type** do conjunto de dados para **AzureSqlDWTable** e especifique as propriedades a seguir na seção **typeProperties**:</span><span class="sxs-lookup"><span data-stu-id="8b587-880">To define an Azure SQL Data Warehouse dataset, set the **type** of the dataset to **AzureSqlDWTable**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="8b587-881">Propriedade</span><span class="sxs-lookup"><span data-stu-id="8b587-881">Property</span></span> | <span data-ttu-id="8b587-882">Descrição</span><span class="sxs-lookup"><span data-stu-id="8b587-882">Description</span></span> | <span data-ttu-id="8b587-883">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="8b587-883">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8b587-884">tableName</span><span class="sxs-lookup"><span data-stu-id="8b587-884">tableName</span></span> |<span data-ttu-id="8b587-885">Nome da tabela ou exibição no banco de dados SQL Data Warehouse do Azure ao qual o serviço vinculado se refere.</span><span class="sxs-lookup"><span data-stu-id="8b587-885">Name of the table or view in the Azure SQL Data Warehouse database that the linked service refers to.</span></span> |<span data-ttu-id="8b587-886">Sim</span><span class="sxs-lookup"><span data-stu-id="8b587-886">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="8b587-887">Exemplo</span><span class="sxs-lookup"><span data-stu-id="8b587-887">Example</span></span>

```json
{
    "name": "AzureSqlDWInput",
    "properties": {
    "type": "AzureSqlDWTable",
        "linkedServiceName": "AzureSqlDWLinkedService",
        "typeProperties": {
            "tableName": "MyTable"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```

<span data-ttu-id="8b587-888">Para obter mais informações, consulte o artigo [Conector do SQL Data Warehouse do Azure](data-factory-azure-sql-data-warehouse-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="8b587-888">For more information, see [Azure SQL Data Warehouse connector](data-factory-azure-sql-data-warehouse-connector.md#dataset-properties) article.</span></span> 

### <a name="sql-dw-source-in-copy-activity"></a><span data-ttu-id="8b587-889">Origem do SQL DW na Atividade de Cópia</span><span class="sxs-lookup"><span data-stu-id="8b587-889">SQL DW Source in Copy Activity</span></span>
<span data-ttu-id="8b587-890">Se você estiver copiando dados de um SQL Data Warehouse do Azure, defina o **source type** da atividade de cópia para **SqlDWSource** e especifique as propriedades a seguir na seção **source**:</span><span class="sxs-lookup"><span data-stu-id="8b587-890">If you are copying data from Azure SQL Data Warehouse, set the **source type** of the copy activity to **SqlDWSource**, and specify following properties in the **source** section:</span></span>


| <span data-ttu-id="8b587-891">Propriedade</span><span class="sxs-lookup"><span data-stu-id="8b587-891">Property</span></span> | <span data-ttu-id="8b587-892">Descrição</span><span class="sxs-lookup"><span data-stu-id="8b587-892">Description</span></span> | <span data-ttu-id="8b587-893">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="8b587-893">Allowed values</span></span> | <span data-ttu-id="8b587-894">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="8b587-894">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="8b587-895">SqlReaderQuery</span><span class="sxs-lookup"><span data-stu-id="8b587-895">sqlReaderQuery</span></span> |<span data-ttu-id="8b587-896">Utiliza a consulta personalizada para ler os dados.</span><span class="sxs-lookup"><span data-stu-id="8b587-896">Use the custom query to read data.</span></span> |<span data-ttu-id="8b587-897">Cadeia de caracteres de consulta SQL.</span><span class="sxs-lookup"><span data-stu-id="8b587-897">SQL query string.</span></span> <span data-ttu-id="8b587-898">Por exemplo: `select * from MyTable`.</span><span class="sxs-lookup"><span data-stu-id="8b587-898">For example: `select * from MyTable`.</span></span> |<span data-ttu-id="8b587-899">Não</span><span class="sxs-lookup"><span data-stu-id="8b587-899">No</span></span> |
| <span data-ttu-id="8b587-900">sqlReaderStoredProcedureName</span><span class="sxs-lookup"><span data-stu-id="8b587-900">sqlReaderStoredProcedureName</span></span> |<span data-ttu-id="8b587-901">Nome do procedimento armazenado que lê os dados da tabela de origem.</span><span class="sxs-lookup"><span data-stu-id="8b587-901">Name of the stored procedure that reads data from the source table.</span></span> |<span data-ttu-id="8b587-902">Nome do procedimento armazenado.</span><span class="sxs-lookup"><span data-stu-id="8b587-902">Name of the stored procedure.</span></span> |<span data-ttu-id="8b587-903">Não</span><span class="sxs-lookup"><span data-stu-id="8b587-903">No</span></span> |
| <span data-ttu-id="8b587-904">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="8b587-904">storedProcedureParameters</span></span> |<span data-ttu-id="8b587-905">Parâmetros para o procedimento armazenado.</span><span class="sxs-lookup"><span data-stu-id="8b587-905">Parameters for the stored procedure.</span></span> |<span data-ttu-id="8b587-906">Pares de nome/valor.</span><span class="sxs-lookup"><span data-stu-id="8b587-906">Name/value pairs.</span></span> <span data-ttu-id="8b587-907">Nomes e uso de maiúsculas e minúsculas de parâmetros devem corresponder aos nomes e o uso de maiúsculas e minúsculas dos parâmetros do procedimento armazenado.</span><span class="sxs-lookup"><span data-stu-id="8b587-907">Names and casing of parameters must match the names and casing of the stored procedure parameters.</span></span> |<span data-ttu-id="8b587-908">Não</span><span class="sxs-lookup"><span data-stu-id="8b587-908">No</span></span> |

#### <a name="example"></a><span data-ttu-id="8b587-909">Exemplo</span><span class="sxs-lookup"><span data-stu-id="8b587-909">Example</span></span>

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline for copy activity",
        "activities": [{
            "name": "AzureSQLDWtoBlob",
            "description": "copy activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureSqlDWInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "SqlDWSource",
                    "sqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

<span data-ttu-id="8b587-910">Para obter mais informações, consulte o artigo [Conector do SQL Data Warehouse do Azure](data-factory-azure-sql-data-warehouse-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="8b587-910">For more information, see [Azure SQL Data Warehouse connector](data-factory-azure-sql-data-warehouse-connector.md#copy-activity-properties) article.</span></span> 

### <a name="sql-dw-sink-in-copy-activity"></a><span data-ttu-id="8b587-911">Coletor do SQL DW na Atividade de Cópia</span><span class="sxs-lookup"><span data-stu-id="8b587-911">SQL DW Sink in Copy Activity</span></span>
<span data-ttu-id="8b587-912">Se você estiver copiando dados de um SQL Data Warehouse do Azure, defina o **sink type** da atividade de cópia para **SqlDWSink** e especifique as propriedades a seguir na seção **sink**:</span><span class="sxs-lookup"><span data-stu-id="8b587-912">If you are copying data to Azure SQL Data Warehouse, set the **sink type** of the copy activity to **SqlDWSink**, and specify following properties in the **sink** section:</span></span>

| <span data-ttu-id="8b587-913">Propriedade</span><span class="sxs-lookup"><span data-stu-id="8b587-913">Property</span></span> | <span data-ttu-id="8b587-914">Descrição</span><span class="sxs-lookup"><span data-stu-id="8b587-914">Description</span></span> | <span data-ttu-id="8b587-915">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="8b587-915">Allowed values</span></span> | <span data-ttu-id="8b587-916">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="8b587-916">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="8b587-917">sqlWriterCleanupScript</span><span class="sxs-lookup"><span data-stu-id="8b587-917">sqlWriterCleanupScript</span></span> |<span data-ttu-id="8b587-918">Especifique uma consulta da Atividade de Cópia a executar para que os dados de uma fatia específica sejam removidos.</span><span class="sxs-lookup"><span data-stu-id="8b587-918">Specify a query for Copy Activity to execute such that data of a specific slice is cleaned up.</span></span> |<span data-ttu-id="8b587-919">Uma instrução de consulta.</span><span class="sxs-lookup"><span data-stu-id="8b587-919">A query statement.</span></span> |<span data-ttu-id="8b587-920">Não</span><span class="sxs-lookup"><span data-stu-id="8b587-920">No</span></span> |
| <span data-ttu-id="8b587-921">allowPolyBase</span><span class="sxs-lookup"><span data-stu-id="8b587-921">allowPolyBase</span></span> |<span data-ttu-id="8b587-922">Indica se o PolyBase (quando aplicável) deve ser utilizado em vez do mecanismo BULKINSERT.</span><span class="sxs-lookup"><span data-stu-id="8b587-922">Indicates whether to use PolyBase (when applicable) instead of BULKINSERT mechanism.</span></span> <br/><br/> <span data-ttu-id="8b587-923">**Usar o PolyBase é a maneira recomendada para carregar dados no SQL Data Warehouse.**</span><span class="sxs-lookup"><span data-stu-id="8b587-923">**Using PolyBase is the recommended way to load data into SQL Data Warehouse.**</span></span> |<span data-ttu-id="8b587-924">True </span><span class="sxs-lookup"><span data-stu-id="8b587-924">True</span></span> <br/><span data-ttu-id="8b587-925">False (padrão)</span><span class="sxs-lookup"><span data-stu-id="8b587-925">False (default)</span></span> |<span data-ttu-id="8b587-926">Não</span><span class="sxs-lookup"><span data-stu-id="8b587-926">No</span></span> |
| <span data-ttu-id="8b587-927">polyBaseSettings</span><span class="sxs-lookup"><span data-stu-id="8b587-927">polyBaseSettings</span></span> |<span data-ttu-id="8b587-928">Um grupo de propriedades que pode ser especificado quando a propriedade **allowPolybase** está definida como **true**.</span><span class="sxs-lookup"><span data-stu-id="8b587-928">A group of properties that can be specified when the **allowPolybase** property is set to **true**.</span></span> |&nbsp; |<span data-ttu-id="8b587-929">Não</span><span class="sxs-lookup"><span data-stu-id="8b587-929">No</span></span> |
| <span data-ttu-id="8b587-930">rejectValue</span><span class="sxs-lookup"><span data-stu-id="8b587-930">rejectValue</span></span> |<span data-ttu-id="8b587-931">Especifica o número ou o percentual de linhas que podem ser rejeitadas antes de a consulta falhar.</span><span class="sxs-lookup"><span data-stu-id="8b587-931">Specifies the number or percentage of rows that can be rejected before the query fails.</span></span> <br/><br/><span data-ttu-id="8b587-932">Saiba mais sobre as opções de rejeição do PolyBase na seção **Argumentos** do tópico [CRIAR TABELA EXTERNA (Transact-SQL)](https://msdn.microsoft.com/library/dn935021.aspx) .</span><span class="sxs-lookup"><span data-stu-id="8b587-932">Learn more about the PolyBase’s reject options in the **Arguments** section of [CREATE EXTERNAL TABLE (Transact-SQL)](https://msdn.microsoft.com/library/dn935021.aspx) topic.</span></span> |<span data-ttu-id="8b587-933">0 (padrão), 1, 2, …</span><span class="sxs-lookup"><span data-stu-id="8b587-933">0 (default), 1, 2, …</span></span> |<span data-ttu-id="8b587-934">Não</span><span class="sxs-lookup"><span data-stu-id="8b587-934">No</span></span> |
| <span data-ttu-id="8b587-935">rejectType</span><span class="sxs-lookup"><span data-stu-id="8b587-935">rejectType</span></span> |<span data-ttu-id="8b587-936">Especifica se a opção rejectValue é especificada como um valor literal ou um percentual.</span><span class="sxs-lookup"><span data-stu-id="8b587-936">Specifies whether the rejectValue option is specified as a literal value or a percentage.</span></span> |<span data-ttu-id="8b587-937">Valor (padrão), Percentual</span><span class="sxs-lookup"><span data-stu-id="8b587-937">Value (default), Percentage</span></span> |<span data-ttu-id="8b587-938">Não</span><span class="sxs-lookup"><span data-stu-id="8b587-938">No</span></span> |
| <span data-ttu-id="8b587-939">rejectSampleValue</span><span class="sxs-lookup"><span data-stu-id="8b587-939">rejectSampleValue</span></span> |<span data-ttu-id="8b587-940">Determina o número de linhas a serem recuperadas antes de o PolyBase recalcular o percentual de linhas rejeitadas.</span><span class="sxs-lookup"><span data-stu-id="8b587-940">Determines the number of rows to retrieve before the PolyBase recalculates the percentage of rejected rows.</span></span> |<span data-ttu-id="8b587-941">1, 2, …</span><span class="sxs-lookup"><span data-stu-id="8b587-941">1, 2, …</span></span> |<span data-ttu-id="8b587-942">Sim, se **rejectType** for **percentual**</span><span class="sxs-lookup"><span data-stu-id="8b587-942">Yes, if **rejectType** is **percentage**</span></span> |
| <span data-ttu-id="8b587-943">useTypeDefault</span><span class="sxs-lookup"><span data-stu-id="8b587-943">useTypeDefault</span></span> |<span data-ttu-id="8b587-944">Especifica como tratar valores ausentes nos arquivos de texto delimitados quando PolyBase recupera dados do arquivo de texto.</span><span class="sxs-lookup"><span data-stu-id="8b587-944">Specifies how to handle missing values in delimited text files when PolyBase retrieves data from the text file.</span></span><br/><br/><span data-ttu-id="8b587-945">Saiba mais sobre essa propriedade na seção Argumentos em [CRIAR FORMATO DE ARQUIVO EXTERNO (Transact-SQL)](https://msdn.microsoft.com/library/dn935026.aspx).</span><span class="sxs-lookup"><span data-stu-id="8b587-945">Learn more about this property from the Arguments section in [CREATE EXTERNAL FILE FORMAT (Transact-SQL)](https://msdn.microsoft.com/library/dn935026.aspx).</span></span> |<span data-ttu-id="8b587-946">True, False (padrão)</span><span class="sxs-lookup"><span data-stu-id="8b587-946">True, False (default)</span></span> |<span data-ttu-id="8b587-947">Não</span><span class="sxs-lookup"><span data-stu-id="8b587-947">No</span></span> |
| <span data-ttu-id="8b587-948">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="8b587-948">writeBatchSize</span></span> |<span data-ttu-id="8b587-949">Insere dados na tabela SQL quando o tamanho do buffer atinge writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="8b587-949">Inserts data into the SQL table when the buffer size reaches writeBatchSize</span></span> |<span data-ttu-id="8b587-950">Inteiro (número de linhas)</span><span class="sxs-lookup"><span data-stu-id="8b587-950">Integer (number of rows)</span></span> |<span data-ttu-id="8b587-951">Não (padrão: 10000)</span><span class="sxs-lookup"><span data-stu-id="8b587-951">No (default: 10000)</span></span> |
| <span data-ttu-id="8b587-952">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="8b587-952">writeBatchTimeout</span></span> |<span data-ttu-id="8b587-953">Tempo de espera para a operação de inserção em lotes ser concluída antes de atingir o tempo limite.</span><span class="sxs-lookup"><span data-stu-id="8b587-953">Wait time for the batch insert operation to complete before it times out.</span></span> |<span data-ttu-id="8b587-954">timespan</span><span class="sxs-lookup"><span data-stu-id="8b587-954">timespan</span></span><br/><br/> <span data-ttu-id="8b587-955">Exemplo: "00:30:00" (30 minutos).</span><span class="sxs-lookup"><span data-stu-id="8b587-955">Example: “00:30:00” (30 minutes).</span></span> |<span data-ttu-id="8b587-956">Não</span><span class="sxs-lookup"><span data-stu-id="8b587-956">No</span></span> |

#### <a name="example"></a><span data-ttu-id="8b587-957">Exemplo</span><span class="sxs-lookup"><span data-stu-id="8b587-957">Example</span></span>

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "AzureBlobtoSQLDW",
            "description": "Copy Activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureBlobInput"
            }],
            "outputs": [{
                "name": "AzureSqlDWOutput"
            }],
            "typeProperties": {
                "source": {
                "type": "BlobSource",
                    "blobColumnSeparators": ","
                },
                "sink": {
                    "type": "SqlDWSink",
                    "allowPolyBase": true
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

<span data-ttu-id="8b587-958">Para obter mais informações, consulte o artigo [Conector do SQL Data Warehouse do Azure](data-factory-azure-sql-data-warehouse-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="8b587-958">For more information, see [Azure SQL Data Warehouse connector](data-factory-azure-sql-data-warehouse-connector.md#copy-activity-properties) article.</span></span> 

## <a name="azure-search"></a><span data-ttu-id="8b587-959">Pesquisa do Azure</span><span class="sxs-lookup"><span data-stu-id="8b587-959">Azure Search</span></span>

### <a name="linked-service"></a><span data-ttu-id="8b587-960">Serviço vinculado</span><span class="sxs-lookup"><span data-stu-id="8b587-960">Linked service</span></span>
<span data-ttu-id="8b587-961">Para definir um serviço vinculado do Azure Search, defina o **type** do serviço vinculado para **AzureSearch**e especifique as propriedades a seguir na seção **typeProperties**:</span><span class="sxs-lookup"><span data-stu-id="8b587-961">To define an Azure Search linked service, set the **type** of the linked service to **AzureSearch**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="8b587-962">Propriedade</span><span class="sxs-lookup"><span data-stu-id="8b587-962">Property</span></span> | <span data-ttu-id="8b587-963">Descrição</span><span class="sxs-lookup"><span data-stu-id="8b587-963">Description</span></span> | <span data-ttu-id="8b587-964">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="8b587-964">Required</span></span> |
| -------- | ----------- | -------- |
| <span data-ttu-id="8b587-965">url</span><span class="sxs-lookup"><span data-stu-id="8b587-965">url</span></span> | <span data-ttu-id="8b587-966">URL para o serviço Azure Search.</span><span class="sxs-lookup"><span data-stu-id="8b587-966">URL for the Azure Search service.</span></span> | <span data-ttu-id="8b587-967">Sim</span><span class="sxs-lookup"><span data-stu-id="8b587-967">Yes</span></span> |
| <span data-ttu-id="8b587-968">chave</span><span class="sxs-lookup"><span data-stu-id="8b587-968">key</span></span> | <span data-ttu-id="8b587-969">Chave de administração para o serviço Azure Search.</span><span class="sxs-lookup"><span data-stu-id="8b587-969">Admin key for the Azure Search service.</span></span> | <span data-ttu-id="8b587-970">Sim</span><span class="sxs-lookup"><span data-stu-id="8b587-970">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="8b587-971">Exemplo</span><span class="sxs-lookup"><span data-stu-id="8b587-971">Example</span></span>

```json
{
    "name": "AzureSearchLinkedService",
    "properties": {
        "type": "AzureSearch",
        "typeProperties": {
            "url": "https://<service>.search.windows.net",
            "key": "<AdminKey>"
        }
    }
}
```

<span data-ttu-id="8b587-972">Para obter mais informações, consulte o artigo [Conector do Azure Search](data-factory-azure-search-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="8b587-972">For more information, see [Azure Search connector](data-factory-azure-search-connector.md#linked-service-properties) article.</span></span>

### <a name="dataset"></a><span data-ttu-id="8b587-973">Conjunto de dados</span><span class="sxs-lookup"><span data-stu-id="8b587-973">Dataset</span></span>
<span data-ttu-id="8b587-974">Para definir um conjunto de dados do Azure Search, defina o **type** do conjunto de dados para **AzureSearchIndex** e especifique as propriedades a seguir na seção **typeProperties**:</span><span class="sxs-lookup"><span data-stu-id="8b587-974">To define an Azure Search dataset, set the **type** of the dataset to **AzureSearchIndex**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="8b587-975">Propriedade</span><span class="sxs-lookup"><span data-stu-id="8b587-975">Property</span></span> | <span data-ttu-id="8b587-976">Descrição</span><span class="sxs-lookup"><span data-stu-id="8b587-976">Description</span></span> | <span data-ttu-id="8b587-977">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="8b587-977">Required</span></span> |
| -------- | ----------- | -------- |
| <span data-ttu-id="8b587-978">type</span><span class="sxs-lookup"><span data-stu-id="8b587-978">type</span></span> | <span data-ttu-id="8b587-979">A propriedade type deve ser definida como: **AzureSearchIndex**.</span><span class="sxs-lookup"><span data-stu-id="8b587-979">The type property must be set to **AzureSearchIndex**.</span></span>| <span data-ttu-id="8b587-980">Sim</span><span class="sxs-lookup"><span data-stu-id="8b587-980">Yes</span></span> |
| <span data-ttu-id="8b587-981">indexName</span><span class="sxs-lookup"><span data-stu-id="8b587-981">indexName</span></span> | <span data-ttu-id="8b587-982">Nome do índice do Azure Search.</span><span class="sxs-lookup"><span data-stu-id="8b587-982">Name of the Azure Search index.</span></span> <span data-ttu-id="8b587-983">O Data Factory não cria o índice.</span><span class="sxs-lookup"><span data-stu-id="8b587-983">Data Factory does not create the index.</span></span> <span data-ttu-id="8b587-984">O índice deve existir no Azure Search.</span><span class="sxs-lookup"><span data-stu-id="8b587-984">The index must exist in Azure Search.</span></span> | <span data-ttu-id="8b587-985">Sim</span><span class="sxs-lookup"><span data-stu-id="8b587-985">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="8b587-986">Exemplo</span><span class="sxs-lookup"><span data-stu-id="8b587-986">Example</span></span>

```json
{
    "name": "AzureSearchIndexDataset",
    "properties": {
        "type": "AzureSearchIndex",
        "linkedServiceName": "AzureSearchLinkedService",
        "typeProperties": {
            "indexName": "products"
        },
        "availability": {
            "frequency": "Minute",
            "interval": 15
        }
    }
}
```

<span data-ttu-id="8b587-987">Para obter mais informações, consulte o artigo [Conector do Azure Search](data-factory-azure-search-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="8b587-987">For more information, see [Azure Search connector](data-factory-azure-search-connector.md#dataset-properties) article.</span></span>

### <a name="azure-search-index-sink-in-copy-activity"></a><span data-ttu-id="8b587-988">Coletor do Índice do Azure Search na Atividade de Cópia</span><span class="sxs-lookup"><span data-stu-id="8b587-988">Azure Search Index Sink in Copy Activity</span></span>
<span data-ttu-id="8b587-989">Se você estiver copiando dados para um índice do Azure Search, defina o **sink type** da atividade de cópia para **AzureSearchIndexSink** e especifique as propriedades a seguir na seção **sink**:</span><span class="sxs-lookup"><span data-stu-id="8b587-989">If you are copying data to an Azure Search index, set the **sink type** of the copy activity to **AzureSearchIndexSink**, and specify following properties in the **sink** section:</span></span>

| <span data-ttu-id="8b587-990">Propriedade</span><span class="sxs-lookup"><span data-stu-id="8b587-990">Property</span></span> | <span data-ttu-id="8b587-991">Descrição</span><span class="sxs-lookup"><span data-stu-id="8b587-991">Description</span></span> | <span data-ttu-id="8b587-992">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="8b587-992">Allowed values</span></span> | <span data-ttu-id="8b587-993">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="8b587-993">Required</span></span> |
| -------- | ----------- | -------------- | -------- |
| <span data-ttu-id="8b587-994">WriteBehavior</span><span class="sxs-lookup"><span data-stu-id="8b587-994">WriteBehavior</span></span> | <span data-ttu-id="8b587-995">Especifica se deve mesclar ou substituir quando já existe um documento no índice.</span><span class="sxs-lookup"><span data-stu-id="8b587-995">Specifies whether to merge or replace when a document already exists in the index.</span></span> | <span data-ttu-id="8b587-996">Merge (padrão)</span><span class="sxs-lookup"><span data-stu-id="8b587-996">Merge (default)</span></span><br/><span data-ttu-id="8b587-997">Carregar</span><span class="sxs-lookup"><span data-stu-id="8b587-997">Upload</span></span>| <span data-ttu-id="8b587-998">Não</span><span class="sxs-lookup"><span data-stu-id="8b587-998">No</span></span> |
| <span data-ttu-id="8b587-999">WriteBatchSize</span><span class="sxs-lookup"><span data-stu-id="8b587-999">WriteBatchSize</span></span> | <span data-ttu-id="8b587-1000">Carrega dados para o índice do Azure Search quando o tamanho do buffer atinge writeBatchSize.</span><span class="sxs-lookup"><span data-stu-id="8b587-1000">Uploads data into the Azure Search index when the buffer size reaches writeBatchSize.</span></span> | <span data-ttu-id="8b587-1001">1 a 1.000.</span><span class="sxs-lookup"><span data-stu-id="8b587-1001">1 to 1,000.</span></span> <span data-ttu-id="8b587-1002">O valor padrão é 1000.</span><span class="sxs-lookup"><span data-stu-id="8b587-1002">Default value is 1000.</span></span> | <span data-ttu-id="8b587-1003">Não</span><span class="sxs-lookup"><span data-stu-id="8b587-1003">No</span></span> |

#### <a name="example"></a><span data-ttu-id="8b587-1004">Exemplo</span><span class="sxs-lookup"><span data-stu-id="8b587-1004">Example</span></span>

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline for copy activity",
        "activities": [{
            "name": "SqlServertoAzureSearchIndex",
            "description": "copy activity",
            "type": "Copy",
            "inputs": [{
                "name": " SqlServerInput"
            }],
            "outputs": [{
                "name": "AzureSearchIndexDataset"
            }],
            "typeProperties": {
                "source": {
                    "type": "SqlSource",
                    "SqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
                },
                "sink": {
                    "type": "AzureSearchIndexSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

<span data-ttu-id="8b587-1005">Para obter mais informações, consulte o artigo [Conector do Azure Search](data-factory-azure-search-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="8b587-1005">For more information, see [Azure Search connector](data-factory-azure-search-connector.md#copy-activity-properties) article.</span></span>

## <a name="azure-table-storage"></a><span data-ttu-id="8b587-1006">Armazenamento de Tabelas do Azure</span><span class="sxs-lookup"><span data-stu-id="8b587-1006">Azure Table Storage</span></span>

### <a name="linked-service"></a><span data-ttu-id="8b587-1007">Serviço vinculado</span><span class="sxs-lookup"><span data-stu-id="8b587-1007">Linked service</span></span>
<span data-ttu-id="8b587-1008">Há dois tipos de serviços vinculados: serviço vinculado do Armazenamento do Azure e serviço vinculado do Armazenamento do Azure SAS.</span><span class="sxs-lookup"><span data-stu-id="8b587-1008">There are two types of linked services: Azure Storage linked service and Azure Storage SAS linked service.</span></span>

#### <a name="azure-storage-linked-service"></a><span data-ttu-id="8b587-1009">Serviço vinculado de armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="8b587-1009">Azure Storage Linked Service</span></span>
<span data-ttu-id="8b587-1010">Para vincular uma conta de armazenamento do Azure ao data factory usando a **chave de conta**, crie um serviço vinculado do Armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="8b587-1010">To link your Azure storage account to a data factory by using the **account key**, create an Azure Storage linked service.</span></span> <span data-ttu-id="8b587-1011">Para definir um serviço vinculado do Armazenamento do Azure, defina o **tipo** do serviço vinculado para **AzureStorage**.</span><span class="sxs-lookup"><span data-stu-id="8b587-1011">To define an Azure Storage linked service, set the **type** of the linked service to **AzureStorage**.</span></span> <span data-ttu-id="8b587-1012">Em seguida, você pode especificar as seguintes propriedades na seção **typeProperties**:</span><span class="sxs-lookup"><span data-stu-id="8b587-1012">Then, you can specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="8b587-1013">Propriedade</span><span class="sxs-lookup"><span data-stu-id="8b587-1013">Property</span></span> | <span data-ttu-id="8b587-1014">Descrição</span><span class="sxs-lookup"><span data-stu-id="8b587-1014">Description</span></span> | <span data-ttu-id="8b587-1015">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="8b587-1015">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="8b587-1016">type</span><span class="sxs-lookup"><span data-stu-id="8b587-1016">type</span></span> |<span data-ttu-id="8b587-1017">A propriedade type deve ser definida como: **AzureStorage**</span><span class="sxs-lookup"><span data-stu-id="8b587-1017">The type property must be set to: **AzureStorage**</span></span> |<span data-ttu-id="8b587-1018">Sim</span><span class="sxs-lookup"><span data-stu-id="8b587-1018">Yes</span></span> |
| <span data-ttu-id="8b587-1019">connectionString</span><span class="sxs-lookup"><span data-stu-id="8b587-1019">connectionString</span></span> |<span data-ttu-id="8b587-1020">Especifique as informações necessárias para se conectar ao armazenamento do Azure para a propriedade connectionString.</span><span class="sxs-lookup"><span data-stu-id="8b587-1020">Specify information needed to connect to Azure storage for the connectionString property.</span></span> |<span data-ttu-id="8b587-1021">Sim</span><span class="sxs-lookup"><span data-stu-id="8b587-1021">Yes</span></span> |

<span data-ttu-id="8b587-1022">**Exemplo:**</span><span class="sxs-lookup"><span data-stu-id="8b587-1022">**Example:**</span></span>  

```json
{  
    "name": "StorageLinkedService",  
    "properties": {  
        "type": "AzureStorage",  
        "typeProperties": {  
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"  
        }  
    }  
}  
```

#### <a name="azure-storage-sas-linked-service"></a><span data-ttu-id="8b587-1023">Serviço vinculado de SAS de Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="8b587-1023">Azure Storage SAS Linked Service</span></span>
<span data-ttu-id="8b587-1024">O serviço vinculado de SAS de armazenamento do Azure permite que você vincule uma conta de armazenamento do Azure ao Azure Data Factory usando uma SAS (Assinatura de Acesso Compartilhado).</span><span class="sxs-lookup"><span data-stu-id="8b587-1024">The Azure Storage SAS linked service allows you to link an Azure Storage Account to an Azure data factory by using a Shared Access Signature (SAS).</span></span> <span data-ttu-id="8b587-1025">Isso fornece ao data factory acesso restrito/acesso total, com limite de tempo/recursos específicos (blob/contêiner) no armazenamento.</span><span class="sxs-lookup"><span data-stu-id="8b587-1025">It provides the data factory with restricted/time-bound access to all/specific resources (blob/container) in the storage.</span></span> <span data-ttu-id="8b587-1026">Para vincular uma conta de Armazenamento do Azure ao data factory usando a Assinatura de Acesso Compartilhado, crie um serviço vinculado de SAS do Armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="8b587-1026">To link your Azure storage account to a data factory by using Shared Access Signature, create an Azure Storage SAS linked service.</span></span> <span data-ttu-id="8b587-1027">Para definir um serviço vinculado de SAS do Armazenamento do Azure, defina o **type** do serviço vinculado para **AzureStorageSas**.</span><span class="sxs-lookup"><span data-stu-id="8b587-1027">To define an Azure Storage SAS linked service, set the **type** of the linked service to **AzureStorageSas**.</span></span> <span data-ttu-id="8b587-1028">Em seguida, você pode especificar as seguintes propriedades na seção **typeProperties**:</span><span class="sxs-lookup"><span data-stu-id="8b587-1028">Then, you can specify following properties in the **typeProperties** section:</span></span>   

| <span data-ttu-id="8b587-1029">Propriedade</span><span class="sxs-lookup"><span data-stu-id="8b587-1029">Property</span></span> | <span data-ttu-id="8b587-1030">Descrição</span><span class="sxs-lookup"><span data-stu-id="8b587-1030">Description</span></span> | <span data-ttu-id="8b587-1031">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="8b587-1031">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="8b587-1032">type</span><span class="sxs-lookup"><span data-stu-id="8b587-1032">type</span></span> |<span data-ttu-id="8b587-1033">A propriedade type deve ser definida como: **AzureStorageSas**</span><span class="sxs-lookup"><span data-stu-id="8b587-1033">The type property must be set to: **AzureStorageSas**</span></span> |<span data-ttu-id="8b587-1034">Sim</span><span class="sxs-lookup"><span data-stu-id="8b587-1034">Yes</span></span> |
| <span data-ttu-id="8b587-1035">sasUri</span><span class="sxs-lookup"><span data-stu-id="8b587-1035">sasUri</span></span> |<span data-ttu-id="8b587-1036">Especificar o URI de Assinatura de Acesso Compartilhado para os recursos de Armazenamento do Azure, como blob, contêiner ou tabela.</span><span class="sxs-lookup"><span data-stu-id="8b587-1036">Specify Shared Access Signature URI to the Azure Storage resources such as blob, container, or table.</span></span> |<span data-ttu-id="8b587-1037">Sim</span><span class="sxs-lookup"><span data-stu-id="8b587-1037">Yes</span></span> |

<span data-ttu-id="8b587-1038">**Exemplo:**</span><span class="sxs-lookup"><span data-stu-id="8b587-1038">**Example:**</span></span>

```json
{  
    "name": "StorageSasLinkedService",  
    "properties": {  
        "type": "AzureStorageSas",  
        "typeProperties": {  
            "sasUri": "<storageUri>?<sasToken>"   
        }  
    }  
}  
```

<span data-ttu-id="8b587-1039">Para obter mais informações sobre esses serviços vinculados, consulte o artigo [Conector de Armazenamento de Tabelas do Azure](data-factory-azure-table-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="8b587-1039">For more information about these linked services, see [Azure Table Storage connector](data-factory-azure-table-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="8b587-1040">Conjunto de dados</span><span class="sxs-lookup"><span data-stu-id="8b587-1040">Dataset</span></span>
<span data-ttu-id="8b587-1041">Para definir um conjunto de dados da Tabela do Azure, defina o **type** do conjunto de dados para **AzureTable** e especifique as propriedades a seguir na seção **typeProperties**:</span><span class="sxs-lookup"><span data-stu-id="8b587-1041">To define an Azure Table dataset, set the **type** of the dataset to **AzureTable**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="8b587-1042">Propriedade</span><span class="sxs-lookup"><span data-stu-id="8b587-1042">Property</span></span> | <span data-ttu-id="8b587-1043">Descrição</span><span class="sxs-lookup"><span data-stu-id="8b587-1043">Description</span></span> | <span data-ttu-id="8b587-1044">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="8b587-1044">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8b587-1045">tableName</span><span class="sxs-lookup"><span data-stu-id="8b587-1045">tableName</span></span> |<span data-ttu-id="8b587-1046">Nome da tabela na instância do Banco de Dados da Tabela do Azure à qual o serviço vinculado se refere.</span><span class="sxs-lookup"><span data-stu-id="8b587-1046">Name of the table in the Azure Table Database instance that linked service refers to.</span></span> |<span data-ttu-id="8b587-1047">Sim.</span><span class="sxs-lookup"><span data-stu-id="8b587-1047">Yes.</span></span> <span data-ttu-id="8b587-1048">Quando um nome de tabela é especificado sem uma azureTableSourceQuery, todos os registros da tabela são copiados para o destino.</span><span class="sxs-lookup"><span data-stu-id="8b587-1048">When a tableName is specified without an azureTableSourceQuery, all records from the table are copied to the destination.</span></span> <span data-ttu-id="8b587-1049">Se uma azureTableSourceQuery também for especificada, os registros da tabela que atende à consulta são copiados para o destino.</span><span class="sxs-lookup"><span data-stu-id="8b587-1049">If an azureTableSourceQuery is also specified, records from the table that satisfies the query are copied to the destination.</span></span> |

#### <a name="example"></a><span data-ttu-id="8b587-1050">Exemplo</span><span class="sxs-lookup"><span data-stu-id="8b587-1050">Example</span></span>

```json
{
    "name": "AzureTableInput",
    "properties": {
        "type": "AzureTable",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
            "tableName": "MyTable"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```

<span data-ttu-id="8b587-1051">Para obter mais informações sobre esses serviços vinculados, consulte o artigo [Conector de Armazenamento de Tabelas do Azure](data-factory-azure-table-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="8b587-1051">For more information about these linked services, see [Azure Table Storage connector](data-factory-azure-table-connector.md#dataset-properties) article.</span></span> 

### <a name="azure-table-source-in-copy-activity"></a><span data-ttu-id="8b587-1052">Origem da Tabela do Azure na Atividade de Cópia</span><span class="sxs-lookup"><span data-stu-id="8b587-1052">Azure Table Source in Copy Activity</span></span>
<span data-ttu-id="8b587-1053">Se você estiver copiando dados de um Armazenamento de Tabelas do Azure, defina o **source type** da atividade de cópia para **AzureTableSource** e especifique as propriedades a seguir na seção **source**:</span><span class="sxs-lookup"><span data-stu-id="8b587-1053">If you are copying data from Azure Table Storage, set the **source type** of the copy activity to **AzureTableSource**, and specify following properties in the **source** section:</span></span>

| <span data-ttu-id="8b587-1054">Propriedade</span><span class="sxs-lookup"><span data-stu-id="8b587-1054">Property</span></span> | <span data-ttu-id="8b587-1055">Descrição</span><span class="sxs-lookup"><span data-stu-id="8b587-1055">Description</span></span> | <span data-ttu-id="8b587-1056">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="8b587-1056">Allowed values</span></span> | <span data-ttu-id="8b587-1057">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="8b587-1057">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="8b587-1058">AzureTableSourceQuery</span><span class="sxs-lookup"><span data-stu-id="8b587-1058">azureTableSourceQuery</span></span> |<span data-ttu-id="8b587-1059">Utiliza a consulta personalizada para ler os dados.</span><span class="sxs-lookup"><span data-stu-id="8b587-1059">Use the custom query to read data.</span></span> |<span data-ttu-id="8b587-1060">Cadeia de caracteres de consulta de tabela do Azure.</span><span class="sxs-lookup"><span data-stu-id="8b587-1060">Azure table query string.</span></span> <span data-ttu-id="8b587-1061">Veja exemplos na próxima seção.</span><span class="sxs-lookup"><span data-stu-id="8b587-1061">See examples in the next section.</span></span> |<span data-ttu-id="8b587-1062">Não.</span><span class="sxs-lookup"><span data-stu-id="8b587-1062">No.</span></span> <span data-ttu-id="8b587-1063">Quando um nome de tabela é especificado sem uma azureTableSourceQuery, todos os registros da tabela são copiados para o destino.</span><span class="sxs-lookup"><span data-stu-id="8b587-1063">When a tableName is specified without an azureTableSourceQuery, all records from the table are copied to the destination.</span></span> <span data-ttu-id="8b587-1064">Se uma azureTableSourceQuery também for especificada, os registros da tabela que atende à consulta são copiados para o destino.</span><span class="sxs-lookup"><span data-stu-id="8b587-1064">If an azureTableSourceQuery is also specified, records from the table that satisfies the query are copied to the destination.</span></span> |
| <span data-ttu-id="8b587-1065">azureTableSourceIgnoreTableNotFound</span><span class="sxs-lookup"><span data-stu-id="8b587-1065">azureTableSourceIgnoreTableNotFound</span></span> |<span data-ttu-id="8b587-1066">Indique se assimilar a exceção da tabela não existe.</span><span class="sxs-lookup"><span data-stu-id="8b587-1066">Indicate whether swallow the exception of table not exist.</span></span> |<span data-ttu-id="8b587-1067">TRUE</span><span class="sxs-lookup"><span data-stu-id="8b587-1067">TRUE</span></span><br/><span data-ttu-id="8b587-1068">FALSE</span><span class="sxs-lookup"><span data-stu-id="8b587-1068">FALSE</span></span> |<span data-ttu-id="8b587-1069">Não</span><span class="sxs-lookup"><span data-stu-id="8b587-1069">No</span></span> |

#### <a name="example"></a><span data-ttu-id="8b587-1070">Exemplo</span><span class="sxs-lookup"><span data-stu-id="8b587-1070">Example</span></span>

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline for copy activity",
        "activities": [{
            "name": "AzureTabletoBlob",
            "description": "copy activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureTableInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "AzureTableSource",
                    "AzureTableSourceQuery": "PartitionKey eq 'DefaultPartitionKey'"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

<span data-ttu-id="8b587-1071">Para obter mais informações sobre esses serviços vinculados, consulte o artigo [Conector de Armazenamento de Tabelas do Azure](data-factory-azure-table-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="8b587-1071">For more information about these linked services, see [Azure Table Storage connector](data-factory-azure-table-connector.md#copy-activity-properties) article.</span></span> 

### <a name="azure-table-sink-in-copy-activity"></a><span data-ttu-id="8b587-1072">Coletor da Tabela do Azure na Atividade de Cópia</span><span class="sxs-lookup"><span data-stu-id="8b587-1072">Azure Table Sink in Copy Activity</span></span>
<span data-ttu-id="8b587-1073">Se você estiver copiando dados para um Armazenamento de Tabelas do Azure, defina o **sink type** da atividade de cópia para **AzureTableSink** e especifique as propriedades a seguir na seção **sink**:</span><span class="sxs-lookup"><span data-stu-id="8b587-1073">If you are copying data to Azure Table Storage, set the **sink type** of the copy activity to **AzureTableSink**, and specify following properties in the **sink** section:</span></span>

| <span data-ttu-id="8b587-1074">Propriedade</span><span class="sxs-lookup"><span data-stu-id="8b587-1074">Property</span></span> | <span data-ttu-id="8b587-1075">Descrição</span><span class="sxs-lookup"><span data-stu-id="8b587-1075">Description</span></span> | <span data-ttu-id="8b587-1076">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="8b587-1076">Allowed values</span></span> | <span data-ttu-id="8b587-1077">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="8b587-1077">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="8b587-1078">azureTableDefaultPartitionKeyValue</span><span class="sxs-lookup"><span data-stu-id="8b587-1078">azureTableDefaultPartitionKeyValue</span></span> |<span data-ttu-id="8b587-1079">Valor de chave de partição padrão que pode ser utilizado pelo coletor.</span><span class="sxs-lookup"><span data-stu-id="8b587-1079">Default partition key value that can be used by the sink.</span></span> |<span data-ttu-id="8b587-1080">Um valor de cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="8b587-1080">A string value.</span></span> |<span data-ttu-id="8b587-1081">Não</span><span class="sxs-lookup"><span data-stu-id="8b587-1081">No</span></span> |
| <span data-ttu-id="8b587-1082">azureTablePartitionKeyName</span><span class="sxs-lookup"><span data-stu-id="8b587-1082">azureTablePartitionKeyName</span></span> |<span data-ttu-id="8b587-1083">Especifique o nome da coluna cujos valores são usados como chaves de partição.</span><span class="sxs-lookup"><span data-stu-id="8b587-1083">Specify name of the column whose values are used as partition keys.</span></span> <span data-ttu-id="8b587-1084">Se não especificado, AzureTableDefaultPartitionKeyValue será utilizado como a chave da partição.</span><span class="sxs-lookup"><span data-stu-id="8b587-1084">If not specified, AzureTableDefaultPartitionKeyValue is used as the partition key.</span></span> |<span data-ttu-id="8b587-1085">Um nome de coluna.</span><span class="sxs-lookup"><span data-stu-id="8b587-1085">A column name.</span></span> |<span data-ttu-id="8b587-1086">Não</span><span class="sxs-lookup"><span data-stu-id="8b587-1086">No</span></span> |
| <span data-ttu-id="8b587-1087">azureTableRowKeyName</span><span class="sxs-lookup"><span data-stu-id="8b587-1087">azureTableRowKeyName</span></span> |<span data-ttu-id="8b587-1088">Especifique o nome da coluna cujos valores são usados como chaves de linha.</span><span class="sxs-lookup"><span data-stu-id="8b587-1088">Specify name of the column whose column values are used as row key.</span></span> <span data-ttu-id="8b587-1089">Se não especificado, um GUID é usado para cada linha.</span><span class="sxs-lookup"><span data-stu-id="8b587-1089">If not specified, use a GUID for each row.</span></span> |<span data-ttu-id="8b587-1090">Um nome de coluna.</span><span class="sxs-lookup"><span data-stu-id="8b587-1090">A column name.</span></span> |<span data-ttu-id="8b587-1091">Não</span><span class="sxs-lookup"><span data-stu-id="8b587-1091">No</span></span> |
| <span data-ttu-id="8b587-1092">azureTableInsertType</span><span class="sxs-lookup"><span data-stu-id="8b587-1092">azureTableInsertType</span></span> |<span data-ttu-id="8b587-1093">O modo para inserir dados na tabela do Azure.</span><span class="sxs-lookup"><span data-stu-id="8b587-1093">The mode to insert data into Azure table.</span></span><br/><br/><span data-ttu-id="8b587-1094">Essa propriedade controla se linhas existentes na tabela de saída com a partição correspondente e as chaves de linha terão seus valores substituídos ou mesclados.</span><span class="sxs-lookup"><span data-stu-id="8b587-1094">This property controls whether existing rows in the output table with matching partition and row keys have their values replaced or merged.</span></span> <br/><br/><span data-ttu-id="8b587-1095">Para saber mais sobre como essas configurações (mesclagem e substituição) funcionam, consulte os tópicos [Inserir ou Mesclar Entidade](https://msdn.microsoft.com/library/azure/hh452241.aspx) e [Inserir ou Substituir Entidade](https://msdn.microsoft.com/library/azure/hh452242.aspx).</span><span class="sxs-lookup"><span data-stu-id="8b587-1095">To learn about how these settings (merge and replace) work, see [Insert or Merge Entity](https://msdn.microsoft.com/library/azure/hh452241.aspx) and [Insert or Replace Entity](https://msdn.microsoft.com/library/azure/hh452242.aspx) topics.</span></span> <br/><br> <span data-ttu-id="8b587-1096">Essa configuração se aplica ao nível de linha e não ao nível de tabela e nenhuma das opções excluirá as linhas na tabela de saída que não existirem na entrada.</span><span class="sxs-lookup"><span data-stu-id="8b587-1096">This setting applies at the row level, not the table level, and neither option deletes rows in the output table that do not exist in the input.</span></span> |<span data-ttu-id="8b587-1097">mesclar (padrão)</span><span class="sxs-lookup"><span data-stu-id="8b587-1097">merge (default)</span></span><br/><span data-ttu-id="8b587-1098">substituir</span><span class="sxs-lookup"><span data-stu-id="8b587-1098">replace</span></span> |<span data-ttu-id="8b587-1099">Não</span><span class="sxs-lookup"><span data-stu-id="8b587-1099">No</span></span> |
| <span data-ttu-id="8b587-1100">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="8b587-1100">writeBatchSize</span></span> |<span data-ttu-id="8b587-1101">Insere dados na tabela do Azure quando o writeBatchSize ou writeBatchTimeout for atingido.</span><span class="sxs-lookup"><span data-stu-id="8b587-1101">Inserts data into the Azure table when the writeBatchSize or writeBatchTimeout is hit.</span></span> |<span data-ttu-id="8b587-1102">Inteiro (número de linhas)</span><span class="sxs-lookup"><span data-stu-id="8b587-1102">Integer (number of rows)</span></span> |<span data-ttu-id="8b587-1103">Não (padrão: 10000)</span><span class="sxs-lookup"><span data-stu-id="8b587-1103">No (default: 10000)</span></span> |
| <span data-ttu-id="8b587-1104">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="8b587-1104">writeBatchTimeout</span></span> |<span data-ttu-id="8b587-1105">Insere dados na tabela do Azure quando o writeBatchSize ou writeBatchTimeout for atingido</span><span class="sxs-lookup"><span data-stu-id="8b587-1105">Inserts data into the Azure table when the writeBatchSize or writeBatchTimeout is hit</span></span> |<span data-ttu-id="8b587-1106">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="8b587-1106">timespan</span></span><br/><br/><span data-ttu-id="8b587-1107">Exemplo: "00:20:00" (20 minutos)</span><span class="sxs-lookup"><span data-stu-id="8b587-1107">Example: “00:20:00” (20 minutes)</span></span> |<span data-ttu-id="8b587-1108">Não (padrão para 90 seg. de valor de tempo padrão de cliente de armazenamento)</span><span class="sxs-lookup"><span data-stu-id="8b587-1108">No (Default to storage client default timeout value 90 sec)</span></span> |

#### <a name="example"></a><span data-ttu-id="8b587-1109">Exemplo</span><span class="sxs-lookup"><span data-stu-id="8b587-1109">Example</span></span>

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "AzureBlobtoTable",
            "description": "Copy Activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureBlobInput"
            }],
            "outputs": [{
                "name": "AzureTableOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "BlobSource"
                },
                "sink": {
                    "type": "AzureTableSink",
                    "writeBatchSize": 100,
                    "writeBatchTimeout": "01:00:00"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```
<span data-ttu-id="8b587-1110">Para obter mais informações sobre esses serviços vinculados, consulte o artigo [Conector de Armazenamento de Tabelas do Azure](data-factory-azure-table-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="8b587-1110">For more information about these linked services, see [Azure Table Storage connector](data-factory-azure-table-connector.md#copy-activity-properties) article.</span></span> 

## <a name="amazon-redshift"></a><span data-ttu-id="8b587-1111">Amazon RedShift</span><span class="sxs-lookup"><span data-stu-id="8b587-1111">Amazon RedShift</span></span>

### <a name="linked-service"></a><span data-ttu-id="8b587-1112">Serviço vinculado</span><span class="sxs-lookup"><span data-stu-id="8b587-1112">Linked service</span></span>
<span data-ttu-id="8b587-1113">Para definir um serviço vinculado do Amazon Redshift, defina o **type** do serviço vinculado para **AmazonRedshift** e especifique as propriedades a seguir na seção **typeProperties**:</span><span class="sxs-lookup"><span data-stu-id="8b587-1113">To define an Amazon Redshift linked service, set the **type** of the linked service to **AmazonRedshift**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="8b587-1114">Propriedade</span><span class="sxs-lookup"><span data-stu-id="8b587-1114">Property</span></span> | <span data-ttu-id="8b587-1115">Descrição</span><span class="sxs-lookup"><span data-stu-id="8b587-1115">Description</span></span> | <span data-ttu-id="8b587-1116">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="8b587-1116">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8b587-1117">server</span><span class="sxs-lookup"><span data-stu-id="8b587-1117">server</span></span> |<span data-ttu-id="8b587-1118">Endereço IP ou nome do host do servidor Amazon Redshift.</span><span class="sxs-lookup"><span data-stu-id="8b587-1118">IP address or host name of the Amazon Redshift server.</span></span> |<span data-ttu-id="8b587-1119">Sim</span><span class="sxs-lookup"><span data-stu-id="8b587-1119">Yes</span></span> |
| <span data-ttu-id="8b587-1120">porta</span><span class="sxs-lookup"><span data-stu-id="8b587-1120">port</span></span> |<span data-ttu-id="8b587-1121">O número da porta TCP usada pelo servidor Amazon Redshift para ouvir conexões de cliente.</span><span class="sxs-lookup"><span data-stu-id="8b587-1121">The number of the TCP port that the Amazon Redshift server uses to listen for client connections.</span></span> |<span data-ttu-id="8b587-1122">Não, valor padrão: 5439</span><span class="sxs-lookup"><span data-stu-id="8b587-1122">No, default value: 5439</span></span> |
| <span data-ttu-id="8b587-1123">database</span><span class="sxs-lookup"><span data-stu-id="8b587-1123">database</span></span> |<span data-ttu-id="8b587-1124">Nome do banco de dados do Amazon Redshift.</span><span class="sxs-lookup"><span data-stu-id="8b587-1124">Name of the Amazon Redshift database.</span></span> |<span data-ttu-id="8b587-1125">Sim</span><span class="sxs-lookup"><span data-stu-id="8b587-1125">Yes</span></span> |
| <span data-ttu-id="8b587-1126">Nome de Usuário</span><span class="sxs-lookup"><span data-stu-id="8b587-1126">username</span></span> |<span data-ttu-id="8b587-1127">Nome de usuário que tem acesso ao banco de dados.</span><span class="sxs-lookup"><span data-stu-id="8b587-1127">Name of user who has access to the database.</span></span> |<span data-ttu-id="8b587-1128">Sim</span><span class="sxs-lookup"><span data-stu-id="8b587-1128">Yes</span></span> |
| <span data-ttu-id="8b587-1129">Senha</span><span class="sxs-lookup"><span data-stu-id="8b587-1129">password</span></span> |<span data-ttu-id="8b587-1130">Senha para a conta de usuário.</span><span class="sxs-lookup"><span data-stu-id="8b587-1130">Password for the user account.</span></span> |<span data-ttu-id="8b587-1131">Sim</span><span class="sxs-lookup"><span data-stu-id="8b587-1131">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="8b587-1132">Exemplo</span><span class="sxs-lookup"><span data-stu-id="8b587-1132">Example</span></span>

```json
{
    "name": "AmazonRedshiftLinkedService",
    "properties": {
        "type": "AmazonRedshift",
        "typeProperties": {
            "server": "<Amazon Redshift host name or IP address>",
            "port": 5439,
            "database": "<database name>",
            "username": "user",
            "password": "password"
        }
    }
}
```

<span data-ttu-id="8b587-1133">Para obter mais informações, consulte o artigo [Conector do Amazon Redshift](#data-factory-amazon-redshift-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="8b587-1133">For more information, see [Amazon Redshift connector](#data-factory-amazon-redshift-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="8b587-1134">Conjunto de dados</span><span class="sxs-lookup"><span data-stu-id="8b587-1134">Dataset</span></span>
<span data-ttu-id="8b587-1135">Para definir um conjunto de dados do Amazon Redshift, defina o **type** do conjunto de dados para **RelationalTable** e especifique as propriedades a seguir na seção **typeProperties**:</span><span class="sxs-lookup"><span data-stu-id="8b587-1135">To define an Amazon Redshift dataset, set the **type** of the dataset to **RelationalTable**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="8b587-1136">Propriedade</span><span class="sxs-lookup"><span data-stu-id="8b587-1136">Property</span></span> | <span data-ttu-id="8b587-1137">Descrição</span><span class="sxs-lookup"><span data-stu-id="8b587-1137">Description</span></span> | <span data-ttu-id="8b587-1138">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="8b587-1138">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8b587-1139">tableName</span><span class="sxs-lookup"><span data-stu-id="8b587-1139">tableName</span></span> |<span data-ttu-id="8b587-1140">Nome da tabela na instância do banco de dados do Amazon Redshift à qual o serviço vinculado se refere.</span><span class="sxs-lookup"><span data-stu-id="8b587-1140">Name of the table in the Amazon Redshift database that linked service refers to.</span></span> |<span data-ttu-id="8b587-1141">Não (se **query** de **RelationalSource** for especificado)</span><span class="sxs-lookup"><span data-stu-id="8b587-1141">No (if **query** of **RelationalSource** is specified)</span></span> |


#### <a name="example"></a><span data-ttu-id="8b587-1142">Exemplo</span><span class="sxs-lookup"><span data-stu-id="8b587-1142">Example</span></span>

```json
{
    "name": "AmazonRedshiftInputDataset",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "AmazonRedshiftLinkedService",
        "typeProperties": {
            "tableName": "<Table name>"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```
<span data-ttu-id="8b587-1143">Para obter mais informações, consulte o artigo [Conector do Amazon Redshift](#data-factory-amazon-redshift-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="8b587-1143">For more information, see [Amazon Redshift connector](#data-factory-amazon-redshift-connector.md#dataset-properties) article.</span></span>

### <a name="relational-source-in-copy-activity"></a><span data-ttu-id="8b587-1144">Origem Relacional na Atividade de Cópia</span><span class="sxs-lookup"><span data-stu-id="8b587-1144">Relational Source in Copy Activity</span></span> 
<span data-ttu-id="8b587-1145">Se você estiver copiando dados de um Amazon Redshift, defina o **source type** da atividade de cópia para **RelationalSource** e especifique as propriedades a seguir na seção **source**:</span><span class="sxs-lookup"><span data-stu-id="8b587-1145">If you are copying data from Amazon Redshift, set the **source type** of the copy activity to **RelationalSource**, and specify following properties in the **source** section:</span></span>

| <span data-ttu-id="8b587-1146">Propriedade</span><span class="sxs-lookup"><span data-stu-id="8b587-1146">Property</span></span> | <span data-ttu-id="8b587-1147">Descrição</span><span class="sxs-lookup"><span data-stu-id="8b587-1147">Description</span></span> | <span data-ttu-id="8b587-1148">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="8b587-1148">Allowed values</span></span> | <span data-ttu-id="8b587-1149">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="8b587-1149">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="8b587-1150">query</span><span class="sxs-lookup"><span data-stu-id="8b587-1150">query</span></span> |<span data-ttu-id="8b587-1151">Utiliza a consulta personalizada para ler os dados.</span><span class="sxs-lookup"><span data-stu-id="8b587-1151">Use the custom query to read data.</span></span> |<span data-ttu-id="8b587-1152">Cadeia de caracteres de consulta SQL.</span><span class="sxs-lookup"><span data-stu-id="8b587-1152">SQL query string.</span></span> <span data-ttu-id="8b587-1153">Por exemplo: `select * from MyTable`.</span><span class="sxs-lookup"><span data-stu-id="8b587-1153">For example: `select * from MyTable`.</span></span> |<span data-ttu-id="8b587-1154">Não (se **tableName** de **dataset** for especificado)</span><span class="sxs-lookup"><span data-stu-id="8b587-1154">No (if **tableName** of **dataset** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="8b587-1155">Exemplo</span><span class="sxs-lookup"><span data-stu-id="8b587-1155">Example</span></span>

```json
{
    "name": "CopyAmazonRedshiftToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "$$Text.Format('select * from MyTable where timestamp >= \\'{0:yyyy-MM-ddTHH:mm:ss}\\' AND timestamp < \\'{1:yyyy-MM-ddTHH:mm:ss}\\'', WindowStart, WindowEnd)"
                },
                "sink": {
                    "type": "BlobSink",
                    "writeBatchSize": 0,
                    "writeBatchTimeout": "00:00:00"
                }
            },
            "inputs": [{
                "name": "AmazonRedshiftInputDataset"
            }],
            "outputs": [{
                "name": "AzureBlobOutputDataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "AmazonRedshiftToBlob"
        }],
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00"
    }
}
```
<span data-ttu-id="8b587-1156">Para obter mais informações, consulte o artigo [Conector do Amazon Redshift](#data-factory-amazon-redshift-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="8b587-1156">For more information, see [Amazon Redshift connector](#data-factory-amazon-redshift-connector.md#copy-activity-properties) article.</span></span>

## <a name="ibm-db2"></a><span data-ttu-id="8b587-1157">IBM DB2</span><span class="sxs-lookup"><span data-stu-id="8b587-1157">IBM DB2</span></span>

### <a name="linked-service"></a><span data-ttu-id="8b587-1158">Serviço vinculado</span><span class="sxs-lookup"><span data-stu-id="8b587-1158">Linked service</span></span>
<span data-ttu-id="8b587-1159">Para definir um serviço vinculado do IBM DB2, defina o **type** do serviço vinculado para **OnPremisesDB2** e especifique as propriedades a seguir na seção **typeProperties**:</span><span class="sxs-lookup"><span data-stu-id="8b587-1159">To define an IBM DB2 linked service, set the **type** of the linked service to **OnPremisesDB2**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="8b587-1160">Propriedade</span><span class="sxs-lookup"><span data-stu-id="8b587-1160">Property</span></span> | <span data-ttu-id="8b587-1161">Descrição</span><span class="sxs-lookup"><span data-stu-id="8b587-1161">Description</span></span> | <span data-ttu-id="8b587-1162">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="8b587-1162">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8b587-1163">server</span><span class="sxs-lookup"><span data-stu-id="8b587-1163">server</span></span> |<span data-ttu-id="8b587-1164">Nome do servidor DB2.</span><span class="sxs-lookup"><span data-stu-id="8b587-1164">Name of the DB2 server.</span></span> |<span data-ttu-id="8b587-1165">Sim</span><span class="sxs-lookup"><span data-stu-id="8b587-1165">Yes</span></span> |
| <span data-ttu-id="8b587-1166">database</span><span class="sxs-lookup"><span data-stu-id="8b587-1166">database</span></span> |<span data-ttu-id="8b587-1167">Nome do banco de dados DB2.</span><span class="sxs-lookup"><span data-stu-id="8b587-1167">Name of the DB2 database.</span></span> |<span data-ttu-id="8b587-1168">Sim</span><span class="sxs-lookup"><span data-stu-id="8b587-1168">Yes</span></span> |
| <span data-ttu-id="8b587-1169">schema</span><span class="sxs-lookup"><span data-stu-id="8b587-1169">schema</span></span> |<span data-ttu-id="8b587-1170">Nome do esquema no banco de dados.</span><span class="sxs-lookup"><span data-stu-id="8b587-1170">Name of the schema in the database.</span></span> <span data-ttu-id="8b587-1171">O nome do esquema diferencia maiúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="8b587-1171">The schema name is case-sensitive.</span></span> |<span data-ttu-id="8b587-1172">Não</span><span class="sxs-lookup"><span data-stu-id="8b587-1172">No</span></span> |
| <span data-ttu-id="8b587-1173">authenticationType</span><span class="sxs-lookup"><span data-stu-id="8b587-1173">authenticationType</span></span> |<span data-ttu-id="8b587-1174">Tipo de autenticação usado para se conectar ao banco de dados DB2.</span><span class="sxs-lookup"><span data-stu-id="8b587-1174">Type of authentication used to connect to the DB2 database.</span></span> <span data-ttu-id="8b587-1175">Os valores possíveis são: Anonymous, Basic e Windows.</span><span class="sxs-lookup"><span data-stu-id="8b587-1175">Possible values are: Anonymous, Basic, and Windows.</span></span> |<span data-ttu-id="8b587-1176">Sim</span><span class="sxs-lookup"><span data-stu-id="8b587-1176">Yes</span></span> |
| <span data-ttu-id="8b587-1177">Nome de Usuário</span><span class="sxs-lookup"><span data-stu-id="8b587-1177">username</span></span> |<span data-ttu-id="8b587-1178">Especifique o nome de usuário se você estiver usando a autenticação Basic ou Windows.</span><span class="sxs-lookup"><span data-stu-id="8b587-1178">Specify user name if you are using Basic or Windows authentication.</span></span> |<span data-ttu-id="8b587-1179">Não</span><span class="sxs-lookup"><span data-stu-id="8b587-1179">No</span></span> |
| <span data-ttu-id="8b587-1180">Senha</span><span class="sxs-lookup"><span data-stu-id="8b587-1180">password</span></span> |<span data-ttu-id="8b587-1181">Especifique a senha da conta de usuário que você especificou para o nome de usuário.</span><span class="sxs-lookup"><span data-stu-id="8b587-1181">Specify password for the user account you specified for the username.</span></span> |<span data-ttu-id="8b587-1182">Não</span><span class="sxs-lookup"><span data-stu-id="8b587-1182">No</span></span> |
| <span data-ttu-id="8b587-1183">gatewayName</span><span class="sxs-lookup"><span data-stu-id="8b587-1183">gatewayName</span></span> |<span data-ttu-id="8b587-1184">O nome do gateway que o serviço Data Factory deve usar para se conectar ao banco de dados DB2 local.</span><span class="sxs-lookup"><span data-stu-id="8b587-1184">Name of the gateway that the Data Factory service should use to connect to the on-premises DB2 database.</span></span> |<span data-ttu-id="8b587-1185">Sim</span><span class="sxs-lookup"><span data-stu-id="8b587-1185">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="8b587-1186">Exemplo</span><span class="sxs-lookup"><span data-stu-id="8b587-1186">Example</span></span>
```json
{
    "name": "OnPremDb2LinkedService",
    "properties": {
        "type": "OnPremisesDb2",
        "typeProperties": {
            "server": "<server>",
            "database": "<database>",
            "schema": "<schema>",
            "authenticationType": "<authentication type>",
            "username": "<username>",
            "password": "<password>",
            "gatewayName": "<gatewayName>"
        }
    }
}
```
<span data-ttu-id="8b587-1187">Para obter mais informações, consulte o artigo [Conector do IBM DB2](#data-factory-onprem-db2-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="8b587-1187">For more information, see [IBM DB2 connector](#data-factory-onprem-db2-connector.md#linked-service-properties) article.</span></span>

### <a name="dataset"></a><span data-ttu-id="8b587-1188">Conjunto de dados</span><span class="sxs-lookup"><span data-stu-id="8b587-1188">Dataset</span></span>
<span data-ttu-id="8b587-1189">Para definir um conjunto de dados do DB2, defina o **type** do conjunto de dados para **RelationalTable** e especifique as propriedades a seguir na seção **typeProperties**:</span><span class="sxs-lookup"><span data-stu-id="8b587-1189">To define a DB2 dataset, set the **type** of the dataset to **RelationalTable**, and specify the following properties in the **typeProperties** section:</span></span>

| <span data-ttu-id="8b587-1190">Propriedade</span><span class="sxs-lookup"><span data-stu-id="8b587-1190">Property</span></span> | <span data-ttu-id="8b587-1191">Descrição</span><span class="sxs-lookup"><span data-stu-id="8b587-1191">Description</span></span> | <span data-ttu-id="8b587-1192">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="8b587-1192">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8b587-1193">tableName</span><span class="sxs-lookup"><span data-stu-id="8b587-1193">tableName</span></span> |<span data-ttu-id="8b587-1194">Nome da tabela na instância do Banco de Dados DB2 à qual o serviço vinculado se refere.</span><span class="sxs-lookup"><span data-stu-id="8b587-1194">Name of the table in the DB2 Database instance that linked service refers to.</span></span> <span data-ttu-id="8b587-1195">O tableName diferencia maiúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="8b587-1195">The tableName is case-sensitive.</span></span> |<span data-ttu-id="8b587-1196">Não (se **query** de **RelationalSource** for especificado)</span><span class="sxs-lookup"><span data-stu-id="8b587-1196">No (if **query** of **RelationalSource** is specified)</span></span> 

#### <a name="example"></a><span data-ttu-id="8b587-1197">Exemplo</span><span class="sxs-lookup"><span data-stu-id="8b587-1197">Example</span></span>
```json
{
    "name": "Db2DataSet",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "OnPremDb2LinkedService",
        "typeProperties": {},
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```

<span data-ttu-id="8b587-1198">Para obter mais informações, consulte o artigo [Conector do IBM DB2](#data-factory-onprem-db2-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="8b587-1198">For more information, see [IBM DB2 connector](#data-factory-onprem-db2-connector.md#dataset-properties) article.</span></span>

### <a name="relational-source-in-copy-activity"></a><span data-ttu-id="8b587-1199">Origem Relacional na Atividade de Cópia</span><span class="sxs-lookup"><span data-stu-id="8b587-1199">Relational Source in Copy Activity</span></span>
<span data-ttu-id="8b587-1200">Se você estiver copiando dados do IBM DB2, defina o **source type** da atividade de cópia para **RelationalSource** e especifique as propriedades a seguir na seção **source**:</span><span class="sxs-lookup"><span data-stu-id="8b587-1200">If you are copying data from IBM DB2, set the **source type** of the copy activity to **RelationalSource**, and specify following properties in the **source** section:</span></span>


| <span data-ttu-id="8b587-1201">Propriedade</span><span class="sxs-lookup"><span data-stu-id="8b587-1201">Property</span></span> | <span data-ttu-id="8b587-1202">Descrição</span><span class="sxs-lookup"><span data-stu-id="8b587-1202">Description</span></span> | <span data-ttu-id="8b587-1203">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="8b587-1203">Allowed values</span></span> | <span data-ttu-id="8b587-1204">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="8b587-1204">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="8b587-1205">query</span><span class="sxs-lookup"><span data-stu-id="8b587-1205">query</span></span> |<span data-ttu-id="8b587-1206">Utiliza a consulta personalizada para ler os dados.</span><span class="sxs-lookup"><span data-stu-id="8b587-1206">Use the custom query to read data.</span></span> |<span data-ttu-id="8b587-1207">Cadeia de caracteres de consulta SQL.</span><span class="sxs-lookup"><span data-stu-id="8b587-1207">SQL query string.</span></span> <span data-ttu-id="8b587-1208">Por exemplo: `"query": "select * from "MySchema"."MyTable""`.</span><span class="sxs-lookup"><span data-stu-id="8b587-1208">For example: `"query": "select * from "MySchema"."MyTable""`.</span></span> |<span data-ttu-id="8b587-1209">Não (se **tableName** de **dataset** for especificado)</span><span class="sxs-lookup"><span data-stu-id="8b587-1209">No (if **tableName** of **dataset** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="8b587-1210">Exemplo</span><span class="sxs-lookup"><span data-stu-id="8b587-1210">Example</span></span>
```json
{
    "name": "CopyDb2ToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "select * from \"Orders\""
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "inputs": [{
                "name": "Db2DataSet"
            }],
            "outputs": [{
                "name": "AzureBlobDb2DataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "Db2ToBlob"
        }],
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00"
    }
}
```
<span data-ttu-id="8b587-1211">Para obter mais informações, consulte o artigo [Conector do IBM DB2](#data-factory-onprem-db2-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="8b587-1211">For more information, see [IBM DB2 connector](#data-factory-onprem-db2-connector.md#copy-activity-properties) article.</span></span>

## <a name="mysql"></a><span data-ttu-id="8b587-1212">MySQL</span><span class="sxs-lookup"><span data-stu-id="8b587-1212">MySQL</span></span>

### <a name="linked-service"></a><span data-ttu-id="8b587-1213">Serviço vinculado</span><span class="sxs-lookup"><span data-stu-id="8b587-1213">Linked service</span></span>
<span data-ttu-id="8b587-1214">Para definir um serviço vinculado do MySQL, defina o **type** do serviço vinculado para **OnPremisesMySql** e especifique as propriedades a seguir na seção **typeProperties**:</span><span class="sxs-lookup"><span data-stu-id="8b587-1214">To define a MySQL linked service, set the **type** of the linked service to **OnPremisesMySql**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="8b587-1215">Propriedade</span><span class="sxs-lookup"><span data-stu-id="8b587-1215">Property</span></span> | <span data-ttu-id="8b587-1216">Descrição</span><span class="sxs-lookup"><span data-stu-id="8b587-1216">Description</span></span> | <span data-ttu-id="8b587-1217">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="8b587-1217">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8b587-1218">server</span><span class="sxs-lookup"><span data-stu-id="8b587-1218">server</span></span> |<span data-ttu-id="8b587-1219">Nome do servidor MySQL.</span><span class="sxs-lookup"><span data-stu-id="8b587-1219">Name of the MySQL server.</span></span> |<span data-ttu-id="8b587-1220">Sim</span><span class="sxs-lookup"><span data-stu-id="8b587-1220">Yes</span></span> |
| <span data-ttu-id="8b587-1221">database</span><span class="sxs-lookup"><span data-stu-id="8b587-1221">database</span></span> |<span data-ttu-id="8b587-1222">Nome do banco de dados MySQL.</span><span class="sxs-lookup"><span data-stu-id="8b587-1222">Name of the MySQL database.</span></span> |<span data-ttu-id="8b587-1223">Sim</span><span class="sxs-lookup"><span data-stu-id="8b587-1223">Yes</span></span> |
| <span data-ttu-id="8b587-1224">schema</span><span class="sxs-lookup"><span data-stu-id="8b587-1224">schema</span></span> |<span data-ttu-id="8b587-1225">Nome do esquema no banco de dados.</span><span class="sxs-lookup"><span data-stu-id="8b587-1225">Name of the schema in the database.</span></span> |<span data-ttu-id="8b587-1226">Não</span><span class="sxs-lookup"><span data-stu-id="8b587-1226">No</span></span> |
| <span data-ttu-id="8b587-1227">authenticationType</span><span class="sxs-lookup"><span data-stu-id="8b587-1227">authenticationType</span></span> |<span data-ttu-id="8b587-1228">Tipo de autenticação usado para se conectar ao banco de dados MySQL.</span><span class="sxs-lookup"><span data-stu-id="8b587-1228">Type of authentication used to connect to the MySQL database.</span></span> <span data-ttu-id="8b587-1229">Os valores possíveis são: `Basic`.</span><span class="sxs-lookup"><span data-stu-id="8b587-1229">Possible values are: `Basic`.</span></span> |<span data-ttu-id="8b587-1230">Sim</span><span class="sxs-lookup"><span data-stu-id="8b587-1230">Yes</span></span> |
| <span data-ttu-id="8b587-1231">Nome de Usuário</span><span class="sxs-lookup"><span data-stu-id="8b587-1231">username</span></span> |<span data-ttu-id="8b587-1232">Especifique o nome de usuário para se conectar ao banco de dados MySQL.</span><span class="sxs-lookup"><span data-stu-id="8b587-1232">Specify user name to connect to the MySQL database.</span></span> |<span data-ttu-id="8b587-1233">Sim</span><span class="sxs-lookup"><span data-stu-id="8b587-1233">Yes</span></span> |
| <span data-ttu-id="8b587-1234">Senha</span><span class="sxs-lookup"><span data-stu-id="8b587-1234">password</span></span> |<span data-ttu-id="8b587-1235">Especifique a senha da conta de usuário que você especificou.</span><span class="sxs-lookup"><span data-stu-id="8b587-1235">Specify password for the user account you specified.</span></span> |<span data-ttu-id="8b587-1236">Sim</span><span class="sxs-lookup"><span data-stu-id="8b587-1236">Yes</span></span> |
| <span data-ttu-id="8b587-1237">gatewayName</span><span class="sxs-lookup"><span data-stu-id="8b587-1237">gatewayName</span></span> |<span data-ttu-id="8b587-1238">O nome do gateway que o serviço Data Factory deve usar para se conectar ao banco de dados MySQL local.</span><span class="sxs-lookup"><span data-stu-id="8b587-1238">Name of the gateway that the Data Factory service should use to connect to the on-premises MySQL database.</span></span> |<span data-ttu-id="8b587-1239">Sim</span><span class="sxs-lookup"><span data-stu-id="8b587-1239">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="8b587-1240">Exemplo</span><span class="sxs-lookup"><span data-stu-id="8b587-1240">Example</span></span>

```json
{
    "name": "OnPremMySqlLinkedService",
    "properties": {
        "type": "OnPremisesMySql",
        "typeProperties": {
            "server": "<server name>",
            "database": "<database name>",
            "schema": "<schema name>",
            "authenticationType": "<authentication type>",
            "userName": "<user name>",
            "password": "<password>",
            "gatewayName": "<gateway>"
        }
    }
}
```

<span data-ttu-id="8b587-1241">Para obter mais informações, consulte o artigo [Conector do MySQL](data-factory-onprem-mysql-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="8b587-1241">For more information, see [MySQL connector](data-factory-onprem-mysql-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="8b587-1242">Conjunto de dados</span><span class="sxs-lookup"><span data-stu-id="8b587-1242">Dataset</span></span>
<span data-ttu-id="8b587-1243">Para definir um conjunto de dados do MySQL, defina o **type** do conjunto de dados para **RelationalTable** e especifique as propriedades a seguir na seção **typeProperties**:</span><span class="sxs-lookup"><span data-stu-id="8b587-1243">To define a MySQL dataset, set the **type** of the dataset to **RelationalTable**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="8b587-1244">Propriedade</span><span class="sxs-lookup"><span data-stu-id="8b587-1244">Property</span></span> | <span data-ttu-id="8b587-1245">Descrição</span><span class="sxs-lookup"><span data-stu-id="8b587-1245">Description</span></span> | <span data-ttu-id="8b587-1246">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="8b587-1246">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8b587-1247">tableName</span><span class="sxs-lookup"><span data-stu-id="8b587-1247">tableName</span></span> |<span data-ttu-id="8b587-1248">Nome da tabela na instância do Banco de Dados MySQL à qual o serviço vinculado se refere.</span><span class="sxs-lookup"><span data-stu-id="8b587-1248">Name of the table in the MySQL Database instance that linked service refers to.</span></span> |<span data-ttu-id="8b587-1249">Não (se **query** de **RelationalSource** for especificado)</span><span class="sxs-lookup"><span data-stu-id="8b587-1249">No (if **query** of **RelationalSource** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="8b587-1250">Exemplo</span><span class="sxs-lookup"><span data-stu-id="8b587-1250">Example</span></span>

```json
{
    "name": "MySqlDataSet",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "OnPremMySqlLinkedService",
        "typeProperties": {},
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```
<span data-ttu-id="8b587-1251">Para obter mais informações, consulte o artigo [Conector do MySQL](data-factory-onprem-mysql-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="8b587-1251">For more information, see [MySQL connector](data-factory-onprem-mysql-connector.md#dataset-properties) article.</span></span> 

### <a name="relational-source-in-copy-activity"></a><span data-ttu-id="8b587-1252">Origem Relacional na Atividade de Cópia</span><span class="sxs-lookup"><span data-stu-id="8b587-1252">Relational Source in Copy Activity</span></span>
<span data-ttu-id="8b587-1253">Se você estiver copiando dados de um banco de dados do MySQL, defina o **source type** da atividade de cópia para **RelationalSource** e especifique as propriedades a seguir na seção **source**:</span><span class="sxs-lookup"><span data-stu-id="8b587-1253">If you are copying data from a MySQL database, set the **source type** of the copy activity to **RelationalSource**, and specify following properties in the **source** section:</span></span>


| <span data-ttu-id="8b587-1254">Propriedade</span><span class="sxs-lookup"><span data-stu-id="8b587-1254">Property</span></span> | <span data-ttu-id="8b587-1255">Descrição</span><span class="sxs-lookup"><span data-stu-id="8b587-1255">Description</span></span> | <span data-ttu-id="8b587-1256">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="8b587-1256">Allowed values</span></span> | <span data-ttu-id="8b587-1257">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="8b587-1257">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="8b587-1258">query</span><span class="sxs-lookup"><span data-stu-id="8b587-1258">query</span></span> |<span data-ttu-id="8b587-1259">Utiliza a consulta personalizada para ler os dados.</span><span class="sxs-lookup"><span data-stu-id="8b587-1259">Use the custom query to read data.</span></span> |<span data-ttu-id="8b587-1260">Cadeia de caracteres de consulta SQL.</span><span class="sxs-lookup"><span data-stu-id="8b587-1260">SQL query string.</span></span> <span data-ttu-id="8b587-1261">Por exemplo: `select * from MyTable`.</span><span class="sxs-lookup"><span data-stu-id="8b587-1261">For example: `select * from MyTable`.</span></span> |<span data-ttu-id="8b587-1262">Não (se **tableName** de **dataset** for especificado)</span><span class="sxs-lookup"><span data-stu-id="8b587-1262">No (if **tableName** of **dataset** is specified)</span></span> |


#### <a name="example"></a><span data-ttu-id="8b587-1263">Exemplo</span><span class="sxs-lookup"><span data-stu-id="8b587-1263">Example</span></span>
```json
{
    "name": "CopyMySqlToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "$$Text.Format('select * from MyTable where timestamp >= \\'{0:yyyy-MM-ddTHH:mm:ss}\\' AND timestamp < \\'{1:yyyy-MM-ddTHH:mm:ss}\\'', WindowStart, WindowEnd)"
                },
                "sink": {
                    "type": "BlobSink",
                    "writeBatchSize": 0,
                    "writeBatchTimeout": "00:00:00"
                }
            },
            "inputs": [{
                "name": "MySqlDataSet"
            }],
            "outputs": [{
                "name": "AzureBlobMySqlDataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "MySqlToBlob"
        }],
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00"
    }
}
```

<span data-ttu-id="8b587-1264">Para obter mais informações, consulte o artigo [Conector do MySQL](data-factory-onprem-mysql-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="8b587-1264">For more information, see [MySQL connector](data-factory-onprem-mysql-connector.md#copy-activity-properties) article.</span></span> 

## <a name="oracle"></a><span data-ttu-id="8b587-1265">Oracle</span><span class="sxs-lookup"><span data-stu-id="8b587-1265">Oracle</span></span> 

### <a name="linked-service"></a><span data-ttu-id="8b587-1266">Serviço vinculado</span><span class="sxs-lookup"><span data-stu-id="8b587-1266">Linked service</span></span>
<span data-ttu-id="8b587-1267">Para definir um serviço vinculado do Oracle, defina o **type** do serviço vinculado para **OnPremisesOracle** e especifique as propriedades a seguir na seção **typeProperties**:</span><span class="sxs-lookup"><span data-stu-id="8b587-1267">To define an Oracle linked service, set the **type** of the linked service to **OnPremisesOracle**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="8b587-1268">Propriedade</span><span class="sxs-lookup"><span data-stu-id="8b587-1268">Property</span></span> | <span data-ttu-id="8b587-1269">Descrição</span><span class="sxs-lookup"><span data-stu-id="8b587-1269">Description</span></span> | <span data-ttu-id="8b587-1270">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="8b587-1270">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8b587-1271">driverType</span><span class="sxs-lookup"><span data-stu-id="8b587-1271">driverType</span></span> | <span data-ttu-id="8b587-1272">Especifique qual driver a ser usado para copiar dados de/para o banco de dados Oracle.</span><span class="sxs-lookup"><span data-stu-id="8b587-1272">Specify which driver to use to copy data from/to Oracle Database.</span></span> <span data-ttu-id="8b587-1273">Valores permitidos são **Microsoft** ou **ODP** (padrão).</span><span class="sxs-lookup"><span data-stu-id="8b587-1273">Allowed values are **Microsoft** or **ODP** (default).</span></span> <span data-ttu-id="8b587-1274">Consulte [suporte para instalação e da versão](#supported-versions-and-installation) seção detalhes do driver.</span><span class="sxs-lookup"><span data-stu-id="8b587-1274">See [Supported version and installation](#supported-versions-and-installation) section on driver details.</span></span> | <span data-ttu-id="8b587-1275">Não</span><span class="sxs-lookup"><span data-stu-id="8b587-1275">No</span></span> |
| <span data-ttu-id="8b587-1276">connectionString</span><span class="sxs-lookup"><span data-stu-id="8b587-1276">connectionString</span></span> | <span data-ttu-id="8b587-1277">Especifique as informações necessárias para se conectar à instância do Banco de Dados Oracle para a propriedade connectionString.</span><span class="sxs-lookup"><span data-stu-id="8b587-1277">Specify information needed to connect to the Oracle Database instance for the connectionString property.</span></span> | <span data-ttu-id="8b587-1278">Sim</span><span class="sxs-lookup"><span data-stu-id="8b587-1278">Yes</span></span> |
| <span data-ttu-id="8b587-1279">gatewayName</span><span class="sxs-lookup"><span data-stu-id="8b587-1279">gatewayName</span></span> | <span data-ttu-id="8b587-1280">Nome do gateway usado para conectar o servidor Oracle local</span><span class="sxs-lookup"><span data-stu-id="8b587-1280">Name of the gateway that that is used to connect to the on-premises Oracle server</span></span> |<span data-ttu-id="8b587-1281">Sim</span><span class="sxs-lookup"><span data-stu-id="8b587-1281">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="8b587-1282">Exemplo</span><span class="sxs-lookup"><span data-stu-id="8b587-1282">Example</span></span>
```json
{
    "name": "OnPremisesOracleLinkedService",
    "properties": {
        "type": "OnPremisesOracle",
        "typeProperties": {
            "driverType": "Microsoft",
            "connectionString": "Host=<host>;Port=<port>;Sid=<sid>;User Id=<username>;Password=<password>;",
            "gatewayName": "<gateway name>"
        }
    }
}
```

<span data-ttu-id="8b587-1283">Para obter mais informações, consulte o artigo [Conector do Oracle](data-factory-onprem-oracle-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="8b587-1283">For more information, see [Oracle connector](data-factory-onprem-oracle-connector.md#linked-service-properties) article.</span></span>

### <a name="dataset"></a><span data-ttu-id="8b587-1284">Conjunto de dados</span><span class="sxs-lookup"><span data-stu-id="8b587-1284">Dataset</span></span>
<span data-ttu-id="8b587-1285">Para definir um conjunto de dados do Oracle, defina o **type** do conjunto de dados para **OracleTable** e especifique as propriedades a seguir na seção **typeProperties**:</span><span class="sxs-lookup"><span data-stu-id="8b587-1285">To define an Oracle dataset, set the **type** of the dataset to **OracleTable**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="8b587-1286">Propriedade</span><span class="sxs-lookup"><span data-stu-id="8b587-1286">Property</span></span> | <span data-ttu-id="8b587-1287">Descrição</span><span class="sxs-lookup"><span data-stu-id="8b587-1287">Description</span></span> | <span data-ttu-id="8b587-1288">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="8b587-1288">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8b587-1289">tableName</span><span class="sxs-lookup"><span data-stu-id="8b587-1289">tableName</span></span> |<span data-ttu-id="8b587-1290">Nome da tabela no Banco de Dados Oracle à qual o serviço vinculado se refere.</span><span class="sxs-lookup"><span data-stu-id="8b587-1290">Name of the table in the Oracle Database that the linked service refers to.</span></span> |<span data-ttu-id="8b587-1291">Não (se **oracleReaderQuery** de **OracleSource** for especificado)</span><span class="sxs-lookup"><span data-stu-id="8b587-1291">No (if **oracleReaderQuery** of **OracleSource** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="8b587-1292">Exemplo</span><span class="sxs-lookup"><span data-stu-id="8b587-1292">Example</span></span>

```json
{
    "name": "OracleInput",
    "properties": {
        "type": "OracleTable",
        "linkedServiceName": "OnPremisesOracleLinkedService",
        "typeProperties": {
            "tableName": "MyTable"
        },
        "external": true,
        "availability": {
            "offset": "01:00:00",
            "interval": "1",
            "anchorDateTime": "2016-02-27T12:00:00",
            "frequency": "Hour"
        },
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```
<span data-ttu-id="8b587-1293">Para obter mais informações, consulte o artigo [Conector do Oracle](data-factory-onprem-oracle-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="8b587-1293">For more information, see [Oracle connector](data-factory-onprem-oracle-connector.md#dataset-properties) article.</span></span>

### <a name="oracle-source-in-copy-activity"></a><span data-ttu-id="8b587-1294">Origem do Oracle na Atividade de Cópia</span><span class="sxs-lookup"><span data-stu-id="8b587-1294">Oracle Source in Copy Activity</span></span>
<span data-ttu-id="8b587-1295">Se você estiver copiando dados de um Banco de Dados SQL do Azure, defina o **source type** da atividade de cópia para **OracleSource** e especifique as propriedades a seguir na seção **source**:</span><span class="sxs-lookup"><span data-stu-id="8b587-1295">If you are copying data from an Oracle database, set the **source type** of the copy activity to **OracleSource**, and specify following properties in the **source** section:</span></span>

| <span data-ttu-id="8b587-1296">Propriedade</span><span class="sxs-lookup"><span data-stu-id="8b587-1296">Property</span></span> | <span data-ttu-id="8b587-1297">Descrição</span><span class="sxs-lookup"><span data-stu-id="8b587-1297">Description</span></span> | <span data-ttu-id="8b587-1298">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="8b587-1298">Allowed values</span></span> | <span data-ttu-id="8b587-1299">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="8b587-1299">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="8b587-1300">oracleReaderQuery</span><span class="sxs-lookup"><span data-stu-id="8b587-1300">oracleReaderQuery</span></span> |<span data-ttu-id="8b587-1301">Utiliza a consulta personalizada para ler os dados.</span><span class="sxs-lookup"><span data-stu-id="8b587-1301">Use the custom query to read data.</span></span> |<span data-ttu-id="8b587-1302">Cadeia de caracteres de consulta SQL.</span><span class="sxs-lookup"><span data-stu-id="8b587-1302">SQL query string.</span></span> <span data-ttu-id="8b587-1303">Por exemplo: `select * from MyTable`</span><span class="sxs-lookup"><span data-stu-id="8b587-1303">For example: `select * from MyTable`</span></span> <br/><br/><span data-ttu-id="8b587-1304">Se não for especificada, a instrução SQL executada será: `select * from MyTable`</span><span class="sxs-lookup"><span data-stu-id="8b587-1304">If not specified, the SQL statement that is executed: `select * from MyTable`</span></span> |<span data-ttu-id="8b587-1305">Não (se **tableName** de **dataset** for especificado)</span><span class="sxs-lookup"><span data-stu-id="8b587-1305">No (if **tableName** of **dataset** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="8b587-1306">Exemplo</span><span class="sxs-lookup"><span data-stu-id="8b587-1306">Example</span></span>

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline for copy activity",
        "activities": [{
            "name": "OracletoBlob",
            "description": "copy activity",
            "type": "Copy",
            "inputs": [{
                "name": " OracleInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "OracleSource",
                    "oracleReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "scheduler": {
            "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

<span data-ttu-id="8b587-1307">Para obter mais informações, consulte o artigo [Conector do Oracle](data-factory-onprem-oracle-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="8b587-1307">For more information, see [Oracle connector](data-factory-onprem-oracle-connector.md#copy-activity-properties) article.</span></span>

### <a name="oracle-sink-in-copy-activity"></a><span data-ttu-id="8b587-1308">Coletor do Oracle na Atividade de Cópia</span><span class="sxs-lookup"><span data-stu-id="8b587-1308">Oracle Sink in Copy Activity</span></span>
<span data-ttu-id="8b587-1309">Se você estiver copiando dados para um banco de dados do Oracle, defina o **source type** da atividade de cópia para **OracleSink** e especifique as propriedades a seguir na seção **sink**:</span><span class="sxs-lookup"><span data-stu-id="8b587-1309">If you are copying data to am Oracle database, set the **sink type** of the copy activity to **OracleSink**, and specify following properties in the **sink** section:</span></span>

| <span data-ttu-id="8b587-1310">Propriedade</span><span class="sxs-lookup"><span data-stu-id="8b587-1310">Property</span></span> | <span data-ttu-id="8b587-1311">Descrição</span><span class="sxs-lookup"><span data-stu-id="8b587-1311">Description</span></span> | <span data-ttu-id="8b587-1312">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="8b587-1312">Allowed values</span></span> | <span data-ttu-id="8b587-1313">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="8b587-1313">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="8b587-1314">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="8b587-1314">writeBatchTimeout</span></span> |<span data-ttu-id="8b587-1315">Tempo de espera para a operação de inserção em lotes ser concluída antes de atingir o tempo limite.</span><span class="sxs-lookup"><span data-stu-id="8b587-1315">Wait time for the batch insert operation to complete before it times out.</span></span> |<span data-ttu-id="8b587-1316">timespan</span><span class="sxs-lookup"><span data-stu-id="8b587-1316">timespan</span></span><br/><br/> <span data-ttu-id="8b587-1317">Exemplo: "00:30:00" (30 minutos).</span><span class="sxs-lookup"><span data-stu-id="8b587-1317">Example: 00:30:00 (30 minutes).</span></span> |<span data-ttu-id="8b587-1318">Não</span><span class="sxs-lookup"><span data-stu-id="8b587-1318">No</span></span> |
| <span data-ttu-id="8b587-1319">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="8b587-1319">writeBatchSize</span></span> |<span data-ttu-id="8b587-1320">Insere dados na tabela SQL quando o tamanho do buffer atinge writeBatchSize.</span><span class="sxs-lookup"><span data-stu-id="8b587-1320">Inserts data into the SQL table when the buffer size reaches writeBatchSize.</span></span> |<span data-ttu-id="8b587-1321">Inteiro (número de linhas)</span><span class="sxs-lookup"><span data-stu-id="8b587-1321">Integer (number of rows)</span></span> |<span data-ttu-id="8b587-1322">Não (padrão: 100)</span><span class="sxs-lookup"><span data-stu-id="8b587-1322">No (default: 100)</span></span> |
| <span data-ttu-id="8b587-1323">sqlWriterCleanupScript</span><span class="sxs-lookup"><span data-stu-id="8b587-1323">sqlWriterCleanupScript</span></span> |<span data-ttu-id="8b587-1324">Especifique uma consulta da Atividade de Cópia a executar para que os dados de uma fatia específica sejam removidos.</span><span class="sxs-lookup"><span data-stu-id="8b587-1324">Specify a query for Copy Activity to execute such that data of a specific slice is cleaned up.</span></span> |<span data-ttu-id="8b587-1325">Uma instrução de consulta.</span><span class="sxs-lookup"><span data-stu-id="8b587-1325">A query statement.</span></span> |<span data-ttu-id="8b587-1326">Não</span><span class="sxs-lookup"><span data-stu-id="8b587-1326">No</span></span> |
| <span data-ttu-id="8b587-1327">sliceIdentifierColumnName</span><span class="sxs-lookup"><span data-stu-id="8b587-1327">sliceIdentifierColumnName</span></span> |<span data-ttu-id="8b587-1328">Especifique o nome de coluna para a Atividade de Cópia a ser preenchido com o identificador de fatia gerado automaticamente, que é usado para limpar dados de uma fatia específica quando executado novamente.</span><span class="sxs-lookup"><span data-stu-id="8b587-1328">Specify column name for Copy Activity to fill with auto generated slice identifier, which is used to clean up data of a specific slice when rerun.</span></span> |<span data-ttu-id="8b587-1329">Nome de uma coluna com tipo de dados de binário (32).</span><span class="sxs-lookup"><span data-stu-id="8b587-1329">Column name of a column with data type of binary(32).</span></span> |<span data-ttu-id="8b587-1330">Não</span><span class="sxs-lookup"><span data-stu-id="8b587-1330">No</span></span> |

#### <a name="example"></a><span data-ttu-id="8b587-1331">Exemplo</span><span class="sxs-lookup"><span data-stu-id="8b587-1331">Example</span></span>
```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-05T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "AzureBlobtoOracle",
            "description": "Copy Activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureBlobInput"
            }],
            "outputs": [{
                "name": "OracleOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "BlobSource"
                },
                "sink": {
                    "type": "OracleSink"
                }
            },
            "scheduler": {
                "frequency": "Day",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```
<span data-ttu-id="8b587-1332">Para obter mais informações, consulte o artigo [Conector do Oracle](data-factory-onprem-oracle-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="8b587-1332">For more information, see [Oracle connector](data-factory-onprem-oracle-connector.md#copy-activity-properties) article.</span></span>

## <a name="postgresql"></a><span data-ttu-id="8b587-1333">PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="8b587-1333">PostgreSQL</span></span>

### <a name="linked-service"></a><span data-ttu-id="8b587-1334">Serviço vinculado</span><span class="sxs-lookup"><span data-stu-id="8b587-1334">Linked service</span></span>
<span data-ttu-id="8b587-1335">Para definir um serviço vinculado do PostgreSQL, defina o **type** do serviço vinculado para **OnPremisesPostgreSql** e especifique as propriedades a seguir na seção **typeProperties**:</span><span class="sxs-lookup"><span data-stu-id="8b587-1335">To define a PostgreSQL linked service, set the **type** of the linked service to **OnPremisesPostgreSql**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="8b587-1336">Propriedade</span><span class="sxs-lookup"><span data-stu-id="8b587-1336">Property</span></span> | <span data-ttu-id="8b587-1337">Descrição</span><span class="sxs-lookup"><span data-stu-id="8b587-1337">Description</span></span> | <span data-ttu-id="8b587-1338">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="8b587-1338">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8b587-1339">server</span><span class="sxs-lookup"><span data-stu-id="8b587-1339">server</span></span> |<span data-ttu-id="8b587-1340">Nome do servidor PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="8b587-1340">Name of the PostgreSQL server.</span></span> |<span data-ttu-id="8b587-1341">Sim</span><span class="sxs-lookup"><span data-stu-id="8b587-1341">Yes</span></span> |
| <span data-ttu-id="8b587-1342">database</span><span class="sxs-lookup"><span data-stu-id="8b587-1342">database</span></span> |<span data-ttu-id="8b587-1343">Nome do banco de dados PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="8b587-1343">Name of the PostgreSQL database.</span></span> |<span data-ttu-id="8b587-1344">Sim</span><span class="sxs-lookup"><span data-stu-id="8b587-1344">Yes</span></span> |
| <span data-ttu-id="8b587-1345">schema</span><span class="sxs-lookup"><span data-stu-id="8b587-1345">schema</span></span> |<span data-ttu-id="8b587-1346">Nome do esquema no banco de dados.</span><span class="sxs-lookup"><span data-stu-id="8b587-1346">Name of the schema in the database.</span></span> <span data-ttu-id="8b587-1347">O nome do esquema diferencia maiúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="8b587-1347">The schema name is case-sensitive.</span></span> |<span data-ttu-id="8b587-1348">Não</span><span class="sxs-lookup"><span data-stu-id="8b587-1348">No</span></span> |
| <span data-ttu-id="8b587-1349">authenticationType</span><span class="sxs-lookup"><span data-stu-id="8b587-1349">authenticationType</span></span> |<span data-ttu-id="8b587-1350">Tipo de autenticação usado para se conectar ao banco de dados PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="8b587-1350">Type of authentication used to connect to the PostgreSQL database.</span></span> <span data-ttu-id="8b587-1351">Os valores possíveis são: Anonymous, Basic e Windows.</span><span class="sxs-lookup"><span data-stu-id="8b587-1351">Possible values are: Anonymous, Basic, and Windows.</span></span> |<span data-ttu-id="8b587-1352">Sim</span><span class="sxs-lookup"><span data-stu-id="8b587-1352">Yes</span></span> |
| <span data-ttu-id="8b587-1353">Nome de Usuário</span><span class="sxs-lookup"><span data-stu-id="8b587-1353">username</span></span> |<span data-ttu-id="8b587-1354">Especifique o nome de usuário se você estiver usando a autenticação Basic ou Windows.</span><span class="sxs-lookup"><span data-stu-id="8b587-1354">Specify user name if you are using Basic or Windows authentication.</span></span> |<span data-ttu-id="8b587-1355">Não</span><span class="sxs-lookup"><span data-stu-id="8b587-1355">No</span></span> |
| <span data-ttu-id="8b587-1356">Senha</span><span class="sxs-lookup"><span data-stu-id="8b587-1356">password</span></span> |<span data-ttu-id="8b587-1357">Especifique a senha da conta de usuário que você especificou para o nome de usuário.</span><span class="sxs-lookup"><span data-stu-id="8b587-1357">Specify password for the user account you specified for the username.</span></span> |<span data-ttu-id="8b587-1358">Não</span><span class="sxs-lookup"><span data-stu-id="8b587-1358">No</span></span> |
| <span data-ttu-id="8b587-1359">gatewayName</span><span class="sxs-lookup"><span data-stu-id="8b587-1359">gatewayName</span></span> |<span data-ttu-id="8b587-1360">O nome do gateway que o serviço Data Factory deve usar para se conectar ao banco de dados PostgreSQL local.</span><span class="sxs-lookup"><span data-stu-id="8b587-1360">Name of the gateway that the Data Factory service should use to connect to the on-premises PostgreSQL database.</span></span> |<span data-ttu-id="8b587-1361">Sim</span><span class="sxs-lookup"><span data-stu-id="8b587-1361">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="8b587-1362">Exemplo</span><span class="sxs-lookup"><span data-stu-id="8b587-1362">Example</span></span>

```json
{
    "name": "OnPremPostgreSqlLinkedService",
    "properties": {
        "type": "OnPremisesPostgreSql",
        "typeProperties": {
            "server": "<server>",
            "database": "<database>",
            "schema": "<schema>",
            "authenticationType": "<authentication type>",
            "username": "<username>",
            "password": "<password>",
            "gatewayName": "<gatewayName>"
        }
    }
}
```
<span data-ttu-id="8b587-1363">Para obter mais informações, consulte o artigo [Conector do PostgreSQL](data-factory-onprem-postgresql-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="8b587-1363">For more information, see [PostgreSQL connector](data-factory-onprem-postgresql-connector.md#linked-service-properties) article.</span></span>

### <a name="dataset"></a><span data-ttu-id="8b587-1364">Conjunto de dados</span><span class="sxs-lookup"><span data-stu-id="8b587-1364">Dataset</span></span>
<span data-ttu-id="8b587-1365">Para definir um conjunto de dados do PostgreSQL, defina o **type** do conjunto de dados para **RelationalTable** e especifique as propriedades a seguir na seção **typeProperties**:</span><span class="sxs-lookup"><span data-stu-id="8b587-1365">To define a PostgreSQL dataset, set the **type** of the dataset to **RelationalTable**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="8b587-1366">Propriedade</span><span class="sxs-lookup"><span data-stu-id="8b587-1366">Property</span></span> | <span data-ttu-id="8b587-1367">Descrição</span><span class="sxs-lookup"><span data-stu-id="8b587-1367">Description</span></span> | <span data-ttu-id="8b587-1368">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="8b587-1368">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8b587-1369">tableName</span><span class="sxs-lookup"><span data-stu-id="8b587-1369">tableName</span></span> |<span data-ttu-id="8b587-1370">Nome da tabela na instância do banco de dados PostgreSQL à qual o serviço vinculado se refere.</span><span class="sxs-lookup"><span data-stu-id="8b587-1370">Name of the table in the PostgreSQL Database instance that linked service refers to.</span></span> <span data-ttu-id="8b587-1371">O tableName diferencia maiúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="8b587-1371">The tableName is case-sensitive.</span></span> |<span data-ttu-id="8b587-1372">Não (se **query** de **RelationalSource** for especificado)</span><span class="sxs-lookup"><span data-stu-id="8b587-1372">No (if **query** of **RelationalSource** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="8b587-1373">Exemplo</span><span class="sxs-lookup"><span data-stu-id="8b587-1373">Example</span></span>
```json
{
    "name": "PostgreSqlDataSet",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "OnPremPostgreSqlLinkedService",
        "typeProperties": {},
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```
<span data-ttu-id="8b587-1374">Para obter mais informações, consulte o artigo [Conector do PostgreSQL](data-factory-onprem-postgresql-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="8b587-1374">For more information, see [PostgreSQL connector](data-factory-onprem-postgresql-connector.md#dataset-properties) article.</span></span>

### <a name="relational-source-in-copy-activity"></a><span data-ttu-id="8b587-1375">Origem Relacional na Atividade de Cópia</span><span class="sxs-lookup"><span data-stu-id="8b587-1375">Relational Source in Copy Activity</span></span>
<span data-ttu-id="8b587-1376">Se você estiver copiando dados de um banco de dados do PostgreSQL, defina o **source type** da atividade de cópia para **RelationalSource** e especifique as propriedades a seguir na seção **source**:</span><span class="sxs-lookup"><span data-stu-id="8b587-1376">If you are copying data from a PostgreSQL database, set the **source type** of the copy activity to **RelationalSource**, and specify following properties in the **source** section:</span></span>


| <span data-ttu-id="8b587-1377">Propriedade</span><span class="sxs-lookup"><span data-stu-id="8b587-1377">Property</span></span> | <span data-ttu-id="8b587-1378">Descrição</span><span class="sxs-lookup"><span data-stu-id="8b587-1378">Description</span></span> | <span data-ttu-id="8b587-1379">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="8b587-1379">Allowed values</span></span> | <span data-ttu-id="8b587-1380">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="8b587-1380">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="8b587-1381">query</span><span class="sxs-lookup"><span data-stu-id="8b587-1381">query</span></span> |<span data-ttu-id="8b587-1382">Utiliza a consulta personalizada para ler os dados.</span><span class="sxs-lookup"><span data-stu-id="8b587-1382">Use the custom query to read data.</span></span> |<span data-ttu-id="8b587-1383">Cadeia de caracteres de consulta SQL.</span><span class="sxs-lookup"><span data-stu-id="8b587-1383">SQL query string.</span></span> <span data-ttu-id="8b587-1384">Por exemplo: "query": "select * from \"MySchema\".\"MyTable\"".</span><span class="sxs-lookup"><span data-stu-id="8b587-1384">For example: "query": "select * from \"MySchema\".\"MyTable\"".</span></span> |<span data-ttu-id="8b587-1385">Não (se **tableName** de **dataset** for especificado)</span><span class="sxs-lookup"><span data-stu-id="8b587-1385">No (if **tableName** of **dataset** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="8b587-1386">Exemplo</span><span class="sxs-lookup"><span data-stu-id="8b587-1386">Example</span></span>

```json
{
    "name": "CopyPostgreSqlToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "select * from \"public\".\"usstates\""
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "inputs": [{
                "name": "PostgreSqlDataSet"
            }],
            "outputs": [{
                "name": "AzureBlobPostgreSqlDataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "PostgreSqlToBlob"
        }],
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00"
    }
}
```

<span data-ttu-id="8b587-1387">Para obter mais informações, consulte o artigo [Conector do PostgreSQL](data-factory-onprem-postgresql-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="8b587-1387">For more information, see [PostgreSQL connector](data-factory-onprem-postgresql-connector.md#copy-activity-properties) article.</span></span>

## <a name="sap-business-warehouse"></a><span data-ttu-id="8b587-1388">SAP Business Warehouse</span><span class="sxs-lookup"><span data-stu-id="8b587-1388">SAP Business Warehouse</span></span>


### <a name="linked-service"></a><span data-ttu-id="8b587-1389">Serviço vinculado</span><span class="sxs-lookup"><span data-stu-id="8b587-1389">Linked service</span></span>
<span data-ttu-id="8b587-1390">Para definir um serviço vinculado do SAP Business Warehouse (BW), defina o **type** do serviço vinculado para **SapBw** e especifique as propriedades a seguir na seção **typeProperties**:</span><span class="sxs-lookup"><span data-stu-id="8b587-1390">To define a SAP Business Warehouse (BW) linked service, set the **type** of the linked service to **SapBw**, and specify following properties in the **typeProperties** section:</span></span>  

<span data-ttu-id="8b587-1391">Propriedade</span><span class="sxs-lookup"><span data-stu-id="8b587-1391">Property</span></span> | <span data-ttu-id="8b587-1392">Descrição</span><span class="sxs-lookup"><span data-stu-id="8b587-1392">Description</span></span> | <span data-ttu-id="8b587-1393">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="8b587-1393">Allowed values</span></span> | <span data-ttu-id="8b587-1394">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="8b587-1394">Required</span></span>
-------- | ----------- | -------------- | --------
<span data-ttu-id="8b587-1395">server</span><span class="sxs-lookup"><span data-stu-id="8b587-1395">server</span></span> | <span data-ttu-id="8b587-1396">Nome do servidor no qual reside a instância do SAP BW.</span><span class="sxs-lookup"><span data-stu-id="8b587-1396">Name of the server on which the SAP BW instance resides.</span></span> | <span data-ttu-id="8b587-1397">string</span><span class="sxs-lookup"><span data-stu-id="8b587-1397">string</span></span> | <span data-ttu-id="8b587-1398">Sim</span><span class="sxs-lookup"><span data-stu-id="8b587-1398">Yes</span></span>
<span data-ttu-id="8b587-1399">systemNumber</span><span class="sxs-lookup"><span data-stu-id="8b587-1399">systemNumber</span></span> | <span data-ttu-id="8b587-1400">Número de sistema do sistema SAP BW.</span><span class="sxs-lookup"><span data-stu-id="8b587-1400">System number of the SAP BW system.</span></span> | <span data-ttu-id="8b587-1401">Número decimal de dois dígitos representado como uma cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="8b587-1401">Two-digit decimal number represented as a string.</span></span> | <span data-ttu-id="8b587-1402">Sim</span><span class="sxs-lookup"><span data-stu-id="8b587-1402">Yes</span></span>
<span data-ttu-id="8b587-1403">clientId</span><span class="sxs-lookup"><span data-stu-id="8b587-1403">clientId</span></span> | <span data-ttu-id="8b587-1404">ID de Cliente do cliente no sistema SAP W.</span><span class="sxs-lookup"><span data-stu-id="8b587-1404">Client ID of the client in the SAP W system.</span></span> | <span data-ttu-id="8b587-1405">Número decimal de três dígitos representado como uma cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="8b587-1405">Three-digit decimal number represented as a string.</span></span> | <span data-ttu-id="8b587-1406">Sim</span><span class="sxs-lookup"><span data-stu-id="8b587-1406">Yes</span></span>
<span data-ttu-id="8b587-1407">Nome de Usuário</span><span class="sxs-lookup"><span data-stu-id="8b587-1407">username</span></span> | <span data-ttu-id="8b587-1408">Nome do usuário que tem acesso ao servidor SAP</span><span class="sxs-lookup"><span data-stu-id="8b587-1408">Name of the user who has access to the SAP server</span></span> | <span data-ttu-id="8b587-1409">string</span><span class="sxs-lookup"><span data-stu-id="8b587-1409">string</span></span> | <span data-ttu-id="8b587-1410">Sim</span><span class="sxs-lookup"><span data-stu-id="8b587-1410">Yes</span></span>
<span data-ttu-id="8b587-1411">Senha</span><span class="sxs-lookup"><span data-stu-id="8b587-1411">password</span></span> | <span data-ttu-id="8b587-1412">Senha do usuário.</span><span class="sxs-lookup"><span data-stu-id="8b587-1412">Password for the user.</span></span> | <span data-ttu-id="8b587-1413">string</span><span class="sxs-lookup"><span data-stu-id="8b587-1413">string</span></span> | <span data-ttu-id="8b587-1414">Sim</span><span class="sxs-lookup"><span data-stu-id="8b587-1414">Yes</span></span>
<span data-ttu-id="8b587-1415">gatewayName</span><span class="sxs-lookup"><span data-stu-id="8b587-1415">gatewayName</span></span> | <span data-ttu-id="8b587-1416">O nome do gateway que o serviço Data Factory deve usar para se conectar à instância local do SAP BW.</span><span class="sxs-lookup"><span data-stu-id="8b587-1416">Name of the gateway that the Data Factory service should use to connect to the on-premises SAP BW instance.</span></span> | <span data-ttu-id="8b587-1417">string</span><span class="sxs-lookup"><span data-stu-id="8b587-1417">string</span></span> | <span data-ttu-id="8b587-1418">Sim</span><span class="sxs-lookup"><span data-stu-id="8b587-1418">Yes</span></span>
<span data-ttu-id="8b587-1419">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="8b587-1419">encryptedCredential</span></span> | <span data-ttu-id="8b587-1420">A cadeia de caracteres de credencial criptografada.</span><span class="sxs-lookup"><span data-stu-id="8b587-1420">The encrypted credential string.</span></span> | <span data-ttu-id="8b587-1421">string</span><span class="sxs-lookup"><span data-stu-id="8b587-1421">string</span></span> | <span data-ttu-id="8b587-1422">Não</span><span class="sxs-lookup"><span data-stu-id="8b587-1422">No</span></span>

#### <a name="example"></a><span data-ttu-id="8b587-1423">Exemplo</span><span class="sxs-lookup"><span data-stu-id="8b587-1423">Example</span></span>

```json
{
    "name": "SapBwLinkedService",
    "properties": {
        "type": "SapBw",
        "typeProperties": {
            "server": "<server name>",
            "systemNumber": "<system number>",
            "clientId": "<client id>",
            "username": "<SAP user>",
            "password": "<Password for SAP user>",
            "gatewayName": "<gateway name>"
        }
    }
}
```

<span data-ttu-id="8b587-1424">Para obter mais informações, consulte o artigo [Conector do SAP Business Warehouse](data-factory-sap-business-warehouse-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="8b587-1424">For more information, see [SAP Business Warehouse connector](data-factory-sap-business-warehouse-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="8b587-1425">Conjunto de dados</span><span class="sxs-lookup"><span data-stu-id="8b587-1425">Dataset</span></span>
<span data-ttu-id="8b587-1426">Para definir o conjunto de dados do SAP BW defina o **type** do conjunto de dados como **RelationalTable**.</span><span class="sxs-lookup"><span data-stu-id="8b587-1426">To define a SAP BW dataset, set the **type** of the dataset to **RelationalTable**.</span></span> <span data-ttu-id="8b587-1427">Não há propriedades específicas ao tipo com suporte para o conjunto de dados do SAP BW do tipo **RelationalTable**.</span><span class="sxs-lookup"><span data-stu-id="8b587-1427">There are no type-specific properties supported for the SAP BW dataset of type **RelationalTable**.</span></span>  

#### <a name="example"></a><span data-ttu-id="8b587-1428">Exemplo</span><span class="sxs-lookup"><span data-stu-id="8b587-1428">Example</span></span>

```json
{
    "name": "SapBwDataset",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "SapBwLinkedService",
        "typeProperties": {},
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```
<span data-ttu-id="8b587-1429">Para obter mais informações, consulte o artigo [Conector do SAP Business Warehouse](data-factory-sap-business-warehouse-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="8b587-1429">For more information, see [SAP Business Warehouse connector](data-factory-sap-business-warehouse-connector.md#dataset-properties) article.</span></span> 

### <a name="relational-source-in-copy-activity"></a><span data-ttu-id="8b587-1430">Origem Relacional na Atividade de Cópia</span><span class="sxs-lookup"><span data-stu-id="8b587-1430">Relational Source in Copy Activity</span></span>
<span data-ttu-id="8b587-1431">Se você estiver copiando dados de um banco de dados do SAP Business Warehouse, defina o **source type** da atividade de cópia para **RelationalSource** e especifique as propriedades a seguir na seção **source**:</span><span class="sxs-lookup"><span data-stu-id="8b587-1431">If you are copying data from SAP Business Warehouse, set the **source type** of the copy activity to **RelationalSource**, and specify following properties in the **source** section:</span></span>


| <span data-ttu-id="8b587-1432">Propriedade</span><span class="sxs-lookup"><span data-stu-id="8b587-1432">Property</span></span> | <span data-ttu-id="8b587-1433">Descrição</span><span class="sxs-lookup"><span data-stu-id="8b587-1433">Description</span></span> | <span data-ttu-id="8b587-1434">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="8b587-1434">Allowed values</span></span> | <span data-ttu-id="8b587-1435">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="8b587-1435">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="8b587-1436">query</span><span class="sxs-lookup"><span data-stu-id="8b587-1436">query</span></span> | <span data-ttu-id="8b587-1437">Especifica a consulta MDX para ler dados da instância do SAP BW.</span><span class="sxs-lookup"><span data-stu-id="8b587-1437">Specifies the MDX query to read data from the SAP BW instance.</span></span> | <span data-ttu-id="8b587-1438">Consulta MDX.</span><span class="sxs-lookup"><span data-stu-id="8b587-1438">MDX query.</span></span> | <span data-ttu-id="8b587-1439">Sim</span><span class="sxs-lookup"><span data-stu-id="8b587-1439">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="8b587-1440">Exemplo</span><span class="sxs-lookup"><span data-stu-id="8b587-1440">Example</span></span>

```json
{
    "name": "CopySapBwToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "<MDX query for SAP BW>"
                },
                "sink": {
                    "type": "BlobSink",
                    "writeBatchSize": 0,
                    "writeBatchTimeout": "00:00:00"
                }
            },
            "inputs": [{
                "name": "SapBwDataset"
            }],
            "outputs": [{
                "name": "AzureBlobDataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "SapBwToBlob"
        }],
        "start": "2017-03-01T18:00:00",
        "end": "2017-03-01T19:00:00"
    }
}
```

<span data-ttu-id="8b587-1441">Para obter mais informações, consulte o artigo [Conector do SAP Business Warehouse](data-factory-sap-business-warehouse-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="8b587-1441">For more information, see [SAP Business Warehouse connector](data-factory-sap-business-warehouse-connector.md#copy-activity-properties) article.</span></span> 

## <a name="sap-hana"></a><span data-ttu-id="8b587-1442">SAP HANA</span><span class="sxs-lookup"><span data-stu-id="8b587-1442">SAP HANA</span></span>

### <a name="linked-service"></a><span data-ttu-id="8b587-1443">Serviço vinculado</span><span class="sxs-lookup"><span data-stu-id="8b587-1443">Linked service</span></span>
<span data-ttu-id="8b587-1444">Para definir um serviço vinculado do SAP HANA, defina o **type** do serviço vinculado para **SapHana** e especifique as propriedades a seguir na seção **typeProperties**:</span><span class="sxs-lookup"><span data-stu-id="8b587-1444">To define a SAP HANA linked service, set the **type** of the linked service to **SapHana**, and specify following properties in the **typeProperties** section:</span></span>  

<span data-ttu-id="8b587-1445">Propriedade</span><span class="sxs-lookup"><span data-stu-id="8b587-1445">Property</span></span> | <span data-ttu-id="8b587-1446">Descrição</span><span class="sxs-lookup"><span data-stu-id="8b587-1446">Description</span></span> | <span data-ttu-id="8b587-1447">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="8b587-1447">Allowed values</span></span> | <span data-ttu-id="8b587-1448">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="8b587-1448">Required</span></span>
-------- | ----------- | -------------- | --------
<span data-ttu-id="8b587-1449">server</span><span class="sxs-lookup"><span data-stu-id="8b587-1449">server</span></span> | <span data-ttu-id="8b587-1450">Nome do servidor no qual reside a instância do SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="8b587-1450">Name of the server on which the SAP HANA instance resides.</span></span> <span data-ttu-id="8b587-1451">Se o servidor estiver usando uma porta personalizada, especifique `server:port`.</span><span class="sxs-lookup"><span data-stu-id="8b587-1451">If your server is using a customized port, specify `server:port`.</span></span> | <span data-ttu-id="8b587-1452">string</span><span class="sxs-lookup"><span data-stu-id="8b587-1452">string</span></span> | <span data-ttu-id="8b587-1453">Sim</span><span class="sxs-lookup"><span data-stu-id="8b587-1453">Yes</span></span>
<span data-ttu-id="8b587-1454">authenticationType</span><span class="sxs-lookup"><span data-stu-id="8b587-1454">authenticationType</span></span> | <span data-ttu-id="8b587-1455">Tipo de autenticação.</span><span class="sxs-lookup"><span data-stu-id="8b587-1455">Type of authentication.</span></span> | <span data-ttu-id="8b587-1456">cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="8b587-1456">string.</span></span> <span data-ttu-id="8b587-1457">"Básico" ou "Windows"</span><span class="sxs-lookup"><span data-stu-id="8b587-1457">"Basic" or "Windows"</span></span> | <span data-ttu-id="8b587-1458">Sim</span><span class="sxs-lookup"><span data-stu-id="8b587-1458">Yes</span></span> 
<span data-ttu-id="8b587-1459">Nome de Usuário</span><span class="sxs-lookup"><span data-stu-id="8b587-1459">username</span></span> | <span data-ttu-id="8b587-1460">Nome do usuário que tem acesso ao servidor SAP</span><span class="sxs-lookup"><span data-stu-id="8b587-1460">Name of the user who has access to the SAP server</span></span> | <span data-ttu-id="8b587-1461">string</span><span class="sxs-lookup"><span data-stu-id="8b587-1461">string</span></span> | <span data-ttu-id="8b587-1462">Sim</span><span class="sxs-lookup"><span data-stu-id="8b587-1462">Yes</span></span>
<span data-ttu-id="8b587-1463">Senha</span><span class="sxs-lookup"><span data-stu-id="8b587-1463">password</span></span> | <span data-ttu-id="8b587-1464">Senha do usuário.</span><span class="sxs-lookup"><span data-stu-id="8b587-1464">Password for the user.</span></span> | <span data-ttu-id="8b587-1465">string</span><span class="sxs-lookup"><span data-stu-id="8b587-1465">string</span></span> | <span data-ttu-id="8b587-1466">Sim</span><span class="sxs-lookup"><span data-stu-id="8b587-1466">Yes</span></span>
<span data-ttu-id="8b587-1467">gatewayName</span><span class="sxs-lookup"><span data-stu-id="8b587-1467">gatewayName</span></span> | <span data-ttu-id="8b587-1468">O nome do gateway que o serviço Data Factory deve usar para se conectar à instância local do SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="8b587-1468">Name of the gateway that the Data Factory service should use to connect to the on-premises SAP HANA instance.</span></span> | <span data-ttu-id="8b587-1469">string</span><span class="sxs-lookup"><span data-stu-id="8b587-1469">string</span></span> | <span data-ttu-id="8b587-1470">Sim</span><span class="sxs-lookup"><span data-stu-id="8b587-1470">Yes</span></span>
<span data-ttu-id="8b587-1471">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="8b587-1471">encryptedCredential</span></span> | <span data-ttu-id="8b587-1472">A cadeia de caracteres de credencial criptografada.</span><span class="sxs-lookup"><span data-stu-id="8b587-1472">The encrypted credential string.</span></span> | <span data-ttu-id="8b587-1473">string</span><span class="sxs-lookup"><span data-stu-id="8b587-1473">string</span></span> | <span data-ttu-id="8b587-1474">Não</span><span class="sxs-lookup"><span data-stu-id="8b587-1474">No</span></span>

#### <a name="example"></a><span data-ttu-id="8b587-1475">Exemplo</span><span class="sxs-lookup"><span data-stu-id="8b587-1475">Example</span></span>

```json
{
    "name": "SapHanaLinkedService",
    "properties": {
        "type": "SapHana",
        "typeProperties": {
            "server": "<server name>",
            "authenticationType": "<Basic, or Windows>",
            "username": "<SAP user>",
            "password": "<Password for SAP user>",
            "gatewayName": "<gateway name>"
        }
    }
}

```
<span data-ttu-id="8b587-1476">Para obter mais informações, consulte o artigo [Conector do SAP HANA](data-factory-sap-hana-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="8b587-1476">For more information, see [SAP HANA connector](data-factory-sap-hana-connector.md#linked-service-properties) article.</span></span>
 
### <a name="dataset"></a><span data-ttu-id="8b587-1477">Conjunto de dados</span><span class="sxs-lookup"><span data-stu-id="8b587-1477">Dataset</span></span>
<span data-ttu-id="8b587-1478">Para definir o conjunto de dados do SAP HANA defina o **type** do conjunto de dados como **RelationalTable**.</span><span class="sxs-lookup"><span data-stu-id="8b587-1478">To define a SAP HANA dataset, set the **type** of the dataset to **RelationalTable**.</span></span> <span data-ttu-id="8b587-1479">Não há propriedades específicas ao tipo com suporte para o conjunto de dados do SAP HANA do tipo **RelationalTable**.</span><span class="sxs-lookup"><span data-stu-id="8b587-1479">There are no type-specific properties supported for the SAP HANA dataset of type **RelationalTable**.</span></span> 

#### <a name="example"></a><span data-ttu-id="8b587-1480">Exemplo</span><span class="sxs-lookup"><span data-stu-id="8b587-1480">Example</span></span>

```json
{
    "name": "SapHanaDataset",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "SapHanaLinkedService",
        "typeProperties": {},
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```
<span data-ttu-id="8b587-1481">Para obter mais informações, consulte o artigo [Conector do SAP HANA](data-factory-sap-hana-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="8b587-1481">For more information, see [SAP HANA connector](data-factory-sap-hana-connector.md#dataset-properties) article.</span></span> 

### <a name="relational-source-in-copy-activity"></a><span data-ttu-id="8b587-1482">Origem Relacional na Atividade de Cópia</span><span class="sxs-lookup"><span data-stu-id="8b587-1482">Relational Source in Copy Activity</span></span>
<span data-ttu-id="8b587-1483">Se você estiver copiando dados de um armazenamento de dados do SAP HANA, defina o **source type** da atividade de cópia para **RelationalSource** e especifique as propriedades a seguir na seção **source**:</span><span class="sxs-lookup"><span data-stu-id="8b587-1483">If you are copying data from a SAP HANA data store, set the **source type** of the copy activity to **RelationalSource**, and specify following properties in the **source** section:</span></span>

| <span data-ttu-id="8b587-1484">Propriedade</span><span class="sxs-lookup"><span data-stu-id="8b587-1484">Property</span></span> | <span data-ttu-id="8b587-1485">Descrição</span><span class="sxs-lookup"><span data-stu-id="8b587-1485">Description</span></span> | <span data-ttu-id="8b587-1486">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="8b587-1486">Allowed values</span></span> | <span data-ttu-id="8b587-1487">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="8b587-1487">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="8b587-1488">query</span><span class="sxs-lookup"><span data-stu-id="8b587-1488">query</span></span> | <span data-ttu-id="8b587-1489">Especifica a consulta SQL para ler dados da instância do SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="8b587-1489">Specifies the SQL query to read data from the SAP HANA instance.</span></span> | <span data-ttu-id="8b587-1490">Consulta SQL.</span><span class="sxs-lookup"><span data-stu-id="8b587-1490">SQL query.</span></span> | <span data-ttu-id="8b587-1491">Sim</span><span class="sxs-lookup"><span data-stu-id="8b587-1491">Yes</span></span> |


#### <a name="example"></a><span data-ttu-id="8b587-1492">Exemplo</span><span class="sxs-lookup"><span data-stu-id="8b587-1492">Example</span></span>


```json
{
    "name": "CopySapHanaToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "<SQL Query for HANA>"
                },
                "sink": {
                    "type": "BlobSink",
                    "writeBatchSize": 0,
                    "writeBatchTimeout": "00:00:00"
                }
            },
            "inputs": [{
                "name": "SapHanaDataset"
            }],
            "outputs": [{
                "name": "AzureBlobDataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "SapHanaToBlob"
        }],
        "start": "2017-03-01T18:00:00",
        "end": "2017-03-01T19:00:00"
    }
}
```

<span data-ttu-id="8b587-1493">Para obter mais informações, consulte o artigo [Conector do SAP HANA](data-factory-sap-hana-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="8b587-1493">For more information, see [SAP HANA connector](data-factory-sap-hana-connector.md#copy-activity-properties) article.</span></span>


## <a name="sql-server"></a><span data-ttu-id="8b587-1494">SQL Server</span><span class="sxs-lookup"><span data-stu-id="8b587-1494">SQL Server</span></span>

### <a name="linked-service"></a><span data-ttu-id="8b587-1495">Serviço vinculado</span><span class="sxs-lookup"><span data-stu-id="8b587-1495">Linked service</span></span>
<span data-ttu-id="8b587-1496">Você cria um serviço vinculado do tipo **OnPremisesSqlServer** para vincular um banco de dados do SQL Server local a um data factory.</span><span class="sxs-lookup"><span data-stu-id="8b587-1496">You create a linked service of type **OnPremisesSqlServer** to link an on-premises SQL Server database to a data factory.</span></span> <span data-ttu-id="8b587-1497">A tabela a seguir fornece a descrição para elementos JSON específicos para o serviço vinculado do SQL Server local.</span><span class="sxs-lookup"><span data-stu-id="8b587-1497">The following table provides description for JSON elements specific to on-premises SQL Server linked service.</span></span>

<span data-ttu-id="8b587-1498">A tabela a seguir fornece a descrição para elementos JSON específicos para o serviço vinculado do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="8b587-1498">The following table provides description for JSON elements specific to SQL Server linked service.</span></span>

| <span data-ttu-id="8b587-1499">Propriedade</span><span class="sxs-lookup"><span data-stu-id="8b587-1499">Property</span></span> | <span data-ttu-id="8b587-1500">Descrição</span><span class="sxs-lookup"><span data-stu-id="8b587-1500">Description</span></span> | <span data-ttu-id="8b587-1501">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="8b587-1501">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8b587-1502">type</span><span class="sxs-lookup"><span data-stu-id="8b587-1502">type</span></span> |<span data-ttu-id="8b587-1503">A propriedade type deve ser definida como: **OnPremisesSqlServer**.</span><span class="sxs-lookup"><span data-stu-id="8b587-1503">The type property should be set to: **OnPremisesSqlServer**.</span></span> |<span data-ttu-id="8b587-1504">Sim</span><span class="sxs-lookup"><span data-stu-id="8b587-1504">Yes</span></span> |
| <span data-ttu-id="8b587-1505">connectionString</span><span class="sxs-lookup"><span data-stu-id="8b587-1505">connectionString</span></span> |<span data-ttu-id="8b587-1506">Especifique as informações de connectionString necessárias para conexão com o banco de dados do SQL Server local usando a autenticação do SQL ou então a autenticação do Windows.</span><span class="sxs-lookup"><span data-stu-id="8b587-1506">Specify connectionString information needed to connect to the on-premises SQL Server database using either SQL authentication or Windows authentication.</span></span> |<span data-ttu-id="8b587-1507">Sim</span><span class="sxs-lookup"><span data-stu-id="8b587-1507">Yes</span></span> |
| <span data-ttu-id="8b587-1508">gatewayName</span><span class="sxs-lookup"><span data-stu-id="8b587-1508">gatewayName</span></span> |<span data-ttu-id="8b587-1509">O nome do gateway que o serviço Data Factory deve usar para se conectar ao banco de dados do SQL Server local.</span><span class="sxs-lookup"><span data-stu-id="8b587-1509">Name of the gateway that the Data Factory service should use to connect to the on-premises SQL Server database.</span></span> |<span data-ttu-id="8b587-1510">Sim</span><span class="sxs-lookup"><span data-stu-id="8b587-1510">Yes</span></span> |
| <span data-ttu-id="8b587-1511">Nome de Usuário</span><span class="sxs-lookup"><span data-stu-id="8b587-1511">username</span></span> |<span data-ttu-id="8b587-1512">Especifique o nome de usuário se você estiver usando a Autenticação do Windows.</span><span class="sxs-lookup"><span data-stu-id="8b587-1512">Specify user name if you are using Windows Authentication.</span></span> <span data-ttu-id="8b587-1513">Exemplo: **domainname\\username**.</span><span class="sxs-lookup"><span data-stu-id="8b587-1513">Example: **domainname\\username**.</span></span> |<span data-ttu-id="8b587-1514">Não</span><span class="sxs-lookup"><span data-stu-id="8b587-1514">No</span></span> |
| <span data-ttu-id="8b587-1515">Senha</span><span class="sxs-lookup"><span data-stu-id="8b587-1515">password</span></span> |<span data-ttu-id="8b587-1516">Especifique a senha da conta de usuário que você especificou para o nome de usuário.</span><span class="sxs-lookup"><span data-stu-id="8b587-1516">Specify password for the user account you specified for the username.</span></span> |<span data-ttu-id="8b587-1517">Não</span><span class="sxs-lookup"><span data-stu-id="8b587-1517">No</span></span> |

<span data-ttu-id="8b587-1518">Criptografe as credenciais usando o cmdlet **New-AzureRmDataFactoryEncryptValue** e use-as na cadeia de conexão, como mostrado no seguinte exemplo (propriedade **EncryptedCredential**):</span><span class="sxs-lookup"><span data-stu-id="8b587-1518">You can encrypt credentials using the **New-AzureRmDataFactoryEncryptValue** cmdlet and use them in the connection string as shown in the following example (**EncryptedCredential** property):</span></span>  

```json
"connectionString": "Data Source=<servername>;Initial Catalog=<databasename>;Integrated Security=True;EncryptedCredential=<encrypted credential>",
```


#### <a name="example-json-for-using-sql-authentication"></a><span data-ttu-id="8b587-1519">Exemplo: JSON para usar Autenticação SQL</span><span class="sxs-lookup"><span data-stu-id="8b587-1519">Example: JSON for using SQL Authentication</span></span>

```json
{
    "name": "MyOnPremisesSQLDB",
    "properties": {
        "type": "OnPremisesSqlServer",
        "typeProperties": {
            "connectionString": "Data Source=<servername>;Initial Catalog=MarketingCampaigns;Integrated Security=False;User ID=<username>;Password=<password>;",
            "gatewayName": "<gateway name>"
        }
    }
}
```
#### <a name="example-json-for-using-windows-authentication"></a><span data-ttu-id="8b587-1520">Exemplo: JSON para usar Autenticação Windows</span><span class="sxs-lookup"><span data-stu-id="8b587-1520">Example: JSON for using Windows Authentication</span></span>

<span data-ttu-id="8b587-1521">Se o nome de usuário e a senha forem especificados, o gateway os usará para representar a conta de usuário especificada para se conectar ao banco de dados SQL Server local.</span><span class="sxs-lookup"><span data-stu-id="8b587-1521">If username and password are specified, gateway uses them to impersonate the specified user account to connect to the on-premises SQL Server database.</span></span> <span data-ttu-id="8b587-1522">Caso contrário, o gateway se conectará ao SQL Server diretamente com o contexto de segurança do Gateway (a sua conta de inicialização).</span><span class="sxs-lookup"><span data-stu-id="8b587-1522">Otherwise, gateway connects to the SQL Server directly with the security context of Gateway (its startup account).</span></span>

```json
{
    "Name": " MyOnPremisesSQLDB",
    "Properties": {
        "type": "OnPremisesSqlServer",
        "typeProperties": {
            "ConnectionString": "Data Source=<servername>;Initial Catalog=MarketingCampaigns;Integrated Security=True;",
            "username": "<domain\\username>",
            "password": "<password>",
            "gatewayName": "<gateway name>"
        }
    }
}
```

<span data-ttu-id="8b587-1523">Para obter mais informações, consulte o artigo [Conector de SQL Server](data-factory-sqlserver-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="8b587-1523">For more information, see [SQL Server connector](data-factory-sqlserver-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="8b587-1524">Conjunto de dados</span><span class="sxs-lookup"><span data-stu-id="8b587-1524">Dataset</span></span>
<span data-ttu-id="8b587-1525">Para definir um conjunto de dados do SQL Server, defina o **type** do conjunto de dados para **SqlServerTable** e especifique as propriedades a seguir na seção **typeProperties**:</span><span class="sxs-lookup"><span data-stu-id="8b587-1525">To define a SQL Server dataset, set the **type** of the dataset to **SqlServerTable**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="8b587-1526">Propriedade</span><span class="sxs-lookup"><span data-stu-id="8b587-1526">Property</span></span> | <span data-ttu-id="8b587-1527">Descrição</span><span class="sxs-lookup"><span data-stu-id="8b587-1527">Description</span></span> | <span data-ttu-id="8b587-1528">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="8b587-1528">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8b587-1529">tableName</span><span class="sxs-lookup"><span data-stu-id="8b587-1529">tableName</span></span> |<span data-ttu-id="8b587-1530">Nome da tabela ou exibição na instância do Banco de Dados SQL Server à qual o serviço vinculado se refere.</span><span class="sxs-lookup"><span data-stu-id="8b587-1530">Name of the table or view in the SQL Server Database instance that linked service refers to.</span></span> |<span data-ttu-id="8b587-1531">Sim</span><span class="sxs-lookup"><span data-stu-id="8b587-1531">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="8b587-1532">Exemplo</span><span class="sxs-lookup"><span data-stu-id="8b587-1532">Example</span></span>
```json
{
    "name": "SqlServerInput",
    "properties": {
        "type": "SqlServerTable",
        "linkedServiceName": "SqlServerLinkedService",
        "typeProperties": {
            "tableName": "MyTable"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```

<span data-ttu-id="8b587-1533">Para obter mais informações, consulte o artigo [Conector de SQL Server](data-factory-sqlserver-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="8b587-1533">For more information, see [SQL Server connector](data-factory-sqlserver-connector.md#dataset-properties) article.</span></span> 

### <a name="sql-source-in-copy-activity"></a><span data-ttu-id="8b587-1534">Origem do SQL na Atividade de Cópia</span><span class="sxs-lookup"><span data-stu-id="8b587-1534">Sql Source in Copy Activity</span></span>
<span data-ttu-id="8b587-1535">Se você estiver copiando dados de um banco de dados SQL do Azure, defina o **source type** da atividade de cópia para **SqlSource** e especifique as propriedades a seguir na seção **source**:</span><span class="sxs-lookup"><span data-stu-id="8b587-1535">If you are copying data from a SQL Server database, set the **source type** of the copy activity to **SqlSource**, and specify following properties in the **source** section:</span></span>


| <span data-ttu-id="8b587-1536">Propriedade</span><span class="sxs-lookup"><span data-stu-id="8b587-1536">Property</span></span> | <span data-ttu-id="8b587-1537">Descrição</span><span class="sxs-lookup"><span data-stu-id="8b587-1537">Description</span></span> | <span data-ttu-id="8b587-1538">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="8b587-1538">Allowed values</span></span> | <span data-ttu-id="8b587-1539">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="8b587-1539">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="8b587-1540">SqlReaderQuery</span><span class="sxs-lookup"><span data-stu-id="8b587-1540">sqlReaderQuery</span></span> |<span data-ttu-id="8b587-1541">Utiliza a consulta personalizada para ler os dados.</span><span class="sxs-lookup"><span data-stu-id="8b587-1541">Use the custom query to read data.</span></span> |<span data-ttu-id="8b587-1542">Cadeia de caracteres de consulta SQL.</span><span class="sxs-lookup"><span data-stu-id="8b587-1542">SQL query string.</span></span> <span data-ttu-id="8b587-1543">Por exemplo: `select * from MyTable`.</span><span class="sxs-lookup"><span data-stu-id="8b587-1543">For example: `select * from MyTable`.</span></span> <span data-ttu-id="8b587-1544">Pode fazer referência a várias tabelas do banco de dados referenciado pelo conjunto de dados de entrada.</span><span class="sxs-lookup"><span data-stu-id="8b587-1544">May reference multiple tables from the database referenced by the input dataset.</span></span> <span data-ttu-id="8b587-1545">Se não for especificada, a instrução SQL que é executada é: select from MyTable.</span><span class="sxs-lookup"><span data-stu-id="8b587-1545">If not specified, the SQL statement that is executed: select from MyTable.</span></span> |<span data-ttu-id="8b587-1546">Não</span><span class="sxs-lookup"><span data-stu-id="8b587-1546">No</span></span> |
| <span data-ttu-id="8b587-1547">sqlReaderStoredProcedureName</span><span class="sxs-lookup"><span data-stu-id="8b587-1547">sqlReaderStoredProcedureName</span></span> |<span data-ttu-id="8b587-1548">Nome do procedimento armazenado que lê os dados da tabela de origem.</span><span class="sxs-lookup"><span data-stu-id="8b587-1548">Name of the stored procedure that reads data from the source table.</span></span> |<span data-ttu-id="8b587-1549">Nome do procedimento armazenado.</span><span class="sxs-lookup"><span data-stu-id="8b587-1549">Name of the stored procedure.</span></span> |<span data-ttu-id="8b587-1550">Não</span><span class="sxs-lookup"><span data-stu-id="8b587-1550">No</span></span> |
| <span data-ttu-id="8b587-1551">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="8b587-1551">storedProcedureParameters</span></span> |<span data-ttu-id="8b587-1552">Parâmetros para o procedimento armazenado.</span><span class="sxs-lookup"><span data-stu-id="8b587-1552">Parameters for the stored procedure.</span></span> |<span data-ttu-id="8b587-1553">Pares de nome/valor.</span><span class="sxs-lookup"><span data-stu-id="8b587-1553">Name/value pairs.</span></span> <span data-ttu-id="8b587-1554">Nomes e uso de maiúsculas e minúsculas de parâmetros devem corresponder aos nomes e o uso de maiúsculas e minúsculas dos parâmetros do procedimento armazenado.</span><span class="sxs-lookup"><span data-stu-id="8b587-1554">Names and casing of parameters must match the names and casing of the stored procedure parameters.</span></span> |<span data-ttu-id="8b587-1555">Não</span><span class="sxs-lookup"><span data-stu-id="8b587-1555">No</span></span> |

<span data-ttu-id="8b587-1556">Se **sqlReaderQuery** for especificado para SqlSource, a Atividade de Cópia executará essa consulta na fonte do Banco do SQL Server para obter os dados.</span><span class="sxs-lookup"><span data-stu-id="8b587-1556">If the **sqlReaderQuery** is specified for the SqlSource, the Copy Activity runs this query against the SQL Server Database source to get the data.</span></span>

<span data-ttu-id="8b587-1557">Como alternativa, você pode especificar um procedimento armazenado especificando o **sqlReaderStoredProcedureName** e o **storedProcedureParameters** (se o procedimento armazenado usa parâmetros).</span><span class="sxs-lookup"><span data-stu-id="8b587-1557">Alternatively, you can specify a stored procedure by specifying the **sqlReaderStoredProcedureName** and **storedProcedureParameters** (if the stored procedure takes parameters).</span></span>

<span data-ttu-id="8b587-1558">Se você não especificar sqlReaderQuery nem sqlReaderStoredProcedureName, as colunas definidas na seção de estrutura serão usadas para criar uma consulta seleção a ser executada no Banco de Dados SQL Server.</span><span class="sxs-lookup"><span data-stu-id="8b587-1558">If you do not specify either sqlReaderQuery or sqlReaderStoredProcedureName, the columns defined in the structure section are used to build a select query to run against the SQL Server Database.</span></span> <span data-ttu-id="8b587-1559">Se a definição de conjunto de dados não tem a estrutura, todas as colunas serão selecionadas da tabela.</span><span class="sxs-lookup"><span data-stu-id="8b587-1559">If the dataset definition does not have the structure, all columns are selected from the table.</span></span>

> [!NOTE]
> <span data-ttu-id="8b587-1560">Quando você usa **sqlReaderStoredProcedureName**, ainda é necessário especificar um valor para a propriedade **tableName** no JSON do conjunto de dados.</span><span class="sxs-lookup"><span data-stu-id="8b587-1560">When you use **sqlReaderStoredProcedureName**, you still need to specify a value for the **tableName** property in the dataset JSON.</span></span> <span data-ttu-id="8b587-1561">Contudo, não há nenhuma validação executada nessa tabela.</span><span class="sxs-lookup"><span data-stu-id="8b587-1561">There are no validations performed against this table though.</span></span>


#### <a name="example"></a><span data-ttu-id="8b587-1562">Exemplo</span><span class="sxs-lookup"><span data-stu-id="8b587-1562">Example</span></span>
```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline for copy activity",
        "activities": [{
            "name": "SqlServertoBlob",
            "description": "copy activity",
            "type": "Copy",
            "inputs": [{
                "name": " SqlServerInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "SqlSource",
                    "SqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

<span data-ttu-id="8b587-1563">Neste exemplo, **sqlReaderQuery** é especificada para SqlSource.</span><span class="sxs-lookup"><span data-stu-id="8b587-1563">In this example, **sqlReaderQuery** is specified for the SqlSource.</span></span> <span data-ttu-id="8b587-1564">A Atividade de Cópia executa essa consulta na fonte do Banco de Dados do SQL Server para obter os dados.</span><span class="sxs-lookup"><span data-stu-id="8b587-1564">The Copy Activity runs this query against the SQL Server Database source to get the data.</span></span> <span data-ttu-id="8b587-1565">Como alternativa, você pode especificar um procedimento armazenado especificando o **sqlReaderStoredProcedureName** e o **storedProcedureParameters** (se o procedimento armazenado usa parâmetros).</span><span class="sxs-lookup"><span data-stu-id="8b587-1565">Alternatively, you can specify a stored procedure by specifying the **sqlReaderStoredProcedureName** and **storedProcedureParameters** (if the stored procedure takes parameters).</span></span> <span data-ttu-id="8b587-1566">A sqlReaderQuery pode fazer referência a várias tabelas no banco de dados referenciado pelo conjunto de dados de entrada.</span><span class="sxs-lookup"><span data-stu-id="8b587-1566">The sqlReaderQuery can reference multiple tables within the database referenced by the input dataset.</span></span> <span data-ttu-id="8b587-1567">A propriedade não se limita apenas à tabela definida como typeProperty de tableName do conjunto de dados.</span><span class="sxs-lookup"><span data-stu-id="8b587-1567">It is not limited to only the table set as the dataset's tableName typeProperty.</span></span>

<span data-ttu-id="8b587-1568">Se você não especificar sqlReaderQuery nem sqlReaderStoredProcedureName, as colunas definidas na seção de estrutura serão usadas para criar uma consulta seleção a ser executada no Banco de Dados SQL Server.</span><span class="sxs-lookup"><span data-stu-id="8b587-1568">If you do not specify sqlReaderQuery or sqlReaderStoredProcedureName, the columns defined in the structure section are used to build a select query to run against the SQL Server Database.</span></span> <span data-ttu-id="8b587-1569">Se a definição de conjunto de dados não tem a estrutura, todas as colunas serão selecionadas da tabela.</span><span class="sxs-lookup"><span data-stu-id="8b587-1569">If the dataset definition does not have the structure, all columns are selected from the table.</span></span>

<span data-ttu-id="8b587-1570">Para obter mais informações, consulte o artigo [Conector de SQL Server](data-factory-sqlserver-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="8b587-1570">For more information, see [SQL Server connector](data-factory-sqlserver-connector.md#copy-activity-properties) article.</span></span> 

### <a name="sql-sink-in-copy-activity"></a><span data-ttu-id="8b587-1571">Coletor do Sql na Atividade de Cópia</span><span class="sxs-lookup"><span data-stu-id="8b587-1571">Sql Sink in Copy Activity</span></span>
<span data-ttu-id="8b587-1572">Se você estiver copiando dados para um banco de dados SQL Server, defina o **sink type** da atividade de cópia para **SqlSink** e especifique as propriedades a seguir na seção **sink**:</span><span class="sxs-lookup"><span data-stu-id="8b587-1572">If you are copying data to a SQL Server database, set the **sink type** of the copy activity to **SqlSink**, and specify following properties in the **sink** section:</span></span>

| <span data-ttu-id="8b587-1573">Propriedade</span><span class="sxs-lookup"><span data-stu-id="8b587-1573">Property</span></span> | <span data-ttu-id="8b587-1574">Descrição</span><span class="sxs-lookup"><span data-stu-id="8b587-1574">Description</span></span> | <span data-ttu-id="8b587-1575">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="8b587-1575">Allowed values</span></span> | <span data-ttu-id="8b587-1576">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="8b587-1576">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="8b587-1577">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="8b587-1577">writeBatchTimeout</span></span> |<span data-ttu-id="8b587-1578">Tempo de espera para a operação de inserção em lotes ser concluída antes de atingir o tempo limite.</span><span class="sxs-lookup"><span data-stu-id="8b587-1578">Wait time for the batch insert operation to complete before it times out.</span></span> |<span data-ttu-id="8b587-1579">timespan</span><span class="sxs-lookup"><span data-stu-id="8b587-1579">timespan</span></span><br/><br/> <span data-ttu-id="8b587-1580">Exemplo: "00:30:00" (30 minutos).</span><span class="sxs-lookup"><span data-stu-id="8b587-1580">Example: “00:30:00” (30 minutes).</span></span> |<span data-ttu-id="8b587-1581">Não</span><span class="sxs-lookup"><span data-stu-id="8b587-1581">No</span></span> |
| <span data-ttu-id="8b587-1582">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="8b587-1582">writeBatchSize</span></span> |<span data-ttu-id="8b587-1583">Insere dados na tabela SQL quando o tamanho do buffer atinge writeBatchSize.</span><span class="sxs-lookup"><span data-stu-id="8b587-1583">Inserts data into the SQL table when the buffer size reaches writeBatchSize.</span></span> |<span data-ttu-id="8b587-1584">Inteiro (número de linhas)</span><span class="sxs-lookup"><span data-stu-id="8b587-1584">Integer (number of rows)</span></span> |<span data-ttu-id="8b587-1585">Não (padrão: 10000)</span><span class="sxs-lookup"><span data-stu-id="8b587-1585">No (default: 10000)</span></span> |
| <span data-ttu-id="8b587-1586">sqlWriterCleanupScript</span><span class="sxs-lookup"><span data-stu-id="8b587-1586">sqlWriterCleanupScript</span></span> |<span data-ttu-id="8b587-1587">Especifique a consulta para a Atividade de Cópia a ser executada para que os dados de uma fatia especifica sejam removidos.</span><span class="sxs-lookup"><span data-stu-id="8b587-1587">Specify query for Copy Activity to execute such that data of a specific slice is cleaned up.</span></span> <span data-ttu-id="8b587-1588">Para saber mais, confira a seção de [repetição](#repeatability-during-copy) .</span><span class="sxs-lookup"><span data-stu-id="8b587-1588">For more information, see [repeatability](#repeatability-during-copy) section.</span></span> |<span data-ttu-id="8b587-1589">Uma instrução de consulta.</span><span class="sxs-lookup"><span data-stu-id="8b587-1589">A query statement.</span></span> |<span data-ttu-id="8b587-1590">Não</span><span class="sxs-lookup"><span data-stu-id="8b587-1590">No</span></span> |
| <span data-ttu-id="8b587-1591">sliceIdentifierColumnName</span><span class="sxs-lookup"><span data-stu-id="8b587-1591">sliceIdentifierColumnName</span></span> |<span data-ttu-id="8b587-1592">Especifique o nome de coluna para a Atividade de Cópia a ser preenchido com o identificador de fatia gerado automaticamente, que é usado para limpar dados de uma fatia específica quando executado novamente.</span><span class="sxs-lookup"><span data-stu-id="8b587-1592">Specify column name for Copy Activity to fill with auto generated slice identifier, which is used to clean up data of a specific slice when rerun.</span></span> <span data-ttu-id="8b587-1593">Para saber mais, confira a seção de [repetição](#repeatability-during-copy) .</span><span class="sxs-lookup"><span data-stu-id="8b587-1593">For more information, see [repeatability](#repeatability-during-copy) section.</span></span> |<span data-ttu-id="8b587-1594">Nome de uma coluna com tipo de dados de binário (32).</span><span class="sxs-lookup"><span data-stu-id="8b587-1594">Column name of a column with data type of binary(32).</span></span> |<span data-ttu-id="8b587-1595">Não</span><span class="sxs-lookup"><span data-stu-id="8b587-1595">No</span></span> |
| <span data-ttu-id="8b587-1596">sqlWriterStoredProcedureName</span><span class="sxs-lookup"><span data-stu-id="8b587-1596">sqlWriterStoredProcedureName</span></span> |<span data-ttu-id="8b587-1597">Nome do procedimento armazenado que upserts (atualiza/insere) na tabela de destino.</span><span class="sxs-lookup"><span data-stu-id="8b587-1597">Name of the stored procedure that upserts (updates/inserts) data into the target table.</span></span> |<span data-ttu-id="8b587-1598">Nome do procedimento armazenado.</span><span class="sxs-lookup"><span data-stu-id="8b587-1598">Name of the stored procedure.</span></span> |<span data-ttu-id="8b587-1599">Não</span><span class="sxs-lookup"><span data-stu-id="8b587-1599">No</span></span> |
| <span data-ttu-id="8b587-1600">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="8b587-1600">storedProcedureParameters</span></span> |<span data-ttu-id="8b587-1601">Parâmetros para o procedimento armazenado.</span><span class="sxs-lookup"><span data-stu-id="8b587-1601">Parameters for the stored procedure.</span></span> |<span data-ttu-id="8b587-1602">Pares de nome/valor.</span><span class="sxs-lookup"><span data-stu-id="8b587-1602">Name/value pairs.</span></span> <span data-ttu-id="8b587-1603">Nomes e uso de maiúsculas e minúsculas de parâmetros devem corresponder aos nomes e o uso de maiúsculas e minúsculas dos parâmetros do procedimento armazenado.</span><span class="sxs-lookup"><span data-stu-id="8b587-1603">Names and casing of parameters must match the names and casing of the stored procedure parameters.</span></span> |<span data-ttu-id="8b587-1604">Não</span><span class="sxs-lookup"><span data-stu-id="8b587-1604">No</span></span> |
| <span data-ttu-id="8b587-1605">sqlWriterTableType</span><span class="sxs-lookup"><span data-stu-id="8b587-1605">sqlWriterTableType</span></span> |<span data-ttu-id="8b587-1606">Especifique o nome do tipo de tabela a ser usado no procedimento armazenado.</span><span class="sxs-lookup"><span data-stu-id="8b587-1606">Specify table type name to be used in the stored procedure.</span></span> <span data-ttu-id="8b587-1607">A atividade de cópia disponibiliza aqueles dados sendo movidos em uma tabela temporária com esse tipo de tabela.</span><span class="sxs-lookup"><span data-stu-id="8b587-1607">Copy activity makes the data being moved available in a temp table with this table type.</span></span> <span data-ttu-id="8b587-1608">O código de procedimento armazenado pode mesclar os dados sendo copiados com dados existentes.</span><span class="sxs-lookup"><span data-stu-id="8b587-1608">Stored procedure code can then merge the data being copied with existing data.</span></span> |<span data-ttu-id="8b587-1609">Um nome de tipo de tabela.</span><span class="sxs-lookup"><span data-stu-id="8b587-1609">A table type name.</span></span> |<span data-ttu-id="8b587-1610">Não</span><span class="sxs-lookup"><span data-stu-id="8b587-1610">No</span></span> |

#### <a name="example"></a><span data-ttu-id="8b587-1611">Exemplo</span><span class="sxs-lookup"><span data-stu-id="8b587-1611">Example</span></span>
<span data-ttu-id="8b587-1612">O pipeline contém uma Atividade de Cópia que está configurada para usar os conjuntos de dados de entrada e saída e agendada para ser executada a cada hora.</span><span class="sxs-lookup"><span data-stu-id="8b587-1612">The pipeline contains a Copy Activity that is configured to use these input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="8b587-1613">Na definição de JSON do pipeline, o tipo de **fonte** está definido como **BlobSource** e o tipo de **coletor** está definido como **SqlSink**.</span><span class="sxs-lookup"><span data-stu-id="8b587-1613">In the pipeline JSON definition, the **source** type is set to **BlobSource** and **sink** type is set to **SqlSink**.</span></span>

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "AzureBlobtoSQL",
            "description": "Copy Activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureBlobInput"
            }],
            "outputs": [{
                "name": " SqlServerOutput "
            }],
            "typeProperties": {
                "source": {
                    "type": "BlobSource",
                    "blobColumnSeparators": ","
                },
                "sink": {
                    "type": "SqlSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

<span data-ttu-id="8b587-1614">Para obter mais informações, consulte o artigo [Conector de SQL Server](data-factory-sqlserver-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="8b587-1614">For more information, see [SQL Server connector](data-factory-sqlserver-connector.md#copy-activity-properties) article.</span></span> 

## <a name="sybase"></a><span data-ttu-id="8b587-1615">Sybase</span><span class="sxs-lookup"><span data-stu-id="8b587-1615">Sybase</span></span>

### <a name="linked-service"></a><span data-ttu-id="8b587-1616">Serviço vinculado</span><span class="sxs-lookup"><span data-stu-id="8b587-1616">Linked service</span></span>
<span data-ttu-id="8b587-1617">Para definir um serviço vinculado do Sybase, defina o **type** do serviço vinculado para **OnPremisesSybase** e especifique as propriedades a seguir na seção **typeProperties**:</span><span class="sxs-lookup"><span data-stu-id="8b587-1617">To define a Sybase linked service, set the **type** of the linked service to **OnPremisesSybase**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="8b587-1618">Propriedade</span><span class="sxs-lookup"><span data-stu-id="8b587-1618">Property</span></span> | <span data-ttu-id="8b587-1619">Descrição</span><span class="sxs-lookup"><span data-stu-id="8b587-1619">Description</span></span> | <span data-ttu-id="8b587-1620">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="8b587-1620">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8b587-1621">server</span><span class="sxs-lookup"><span data-stu-id="8b587-1621">server</span></span> |<span data-ttu-id="8b587-1622">Nome do servidor do Sybase.</span><span class="sxs-lookup"><span data-stu-id="8b587-1622">Name of the Sybase server.</span></span> |<span data-ttu-id="8b587-1623">Sim</span><span class="sxs-lookup"><span data-stu-id="8b587-1623">Yes</span></span> |
| <span data-ttu-id="8b587-1624">database</span><span class="sxs-lookup"><span data-stu-id="8b587-1624">database</span></span> |<span data-ttu-id="8b587-1625">Nome do banco de dados do Sybase.</span><span class="sxs-lookup"><span data-stu-id="8b587-1625">Name of the Sybase database.</span></span> |<span data-ttu-id="8b587-1626">Sim</span><span class="sxs-lookup"><span data-stu-id="8b587-1626">Yes</span></span> |
| <span data-ttu-id="8b587-1627">schema</span><span class="sxs-lookup"><span data-stu-id="8b587-1627">schema</span></span> |<span data-ttu-id="8b587-1628">Nome do esquema no banco de dados.</span><span class="sxs-lookup"><span data-stu-id="8b587-1628">Name of the schema in the database.</span></span> |<span data-ttu-id="8b587-1629">Não</span><span class="sxs-lookup"><span data-stu-id="8b587-1629">No</span></span> |
| <span data-ttu-id="8b587-1630">authenticationType</span><span class="sxs-lookup"><span data-stu-id="8b587-1630">authenticationType</span></span> |<span data-ttu-id="8b587-1631">Tipo de autenticação usado para se conectar ao banco de dados Sybase.</span><span class="sxs-lookup"><span data-stu-id="8b587-1631">Type of authentication used to connect to the Sybase database.</span></span> <span data-ttu-id="8b587-1632">Os valores possíveis são: Anonymous, Basic e Windows.</span><span class="sxs-lookup"><span data-stu-id="8b587-1632">Possible values are: Anonymous, Basic, and Windows.</span></span> |<span data-ttu-id="8b587-1633">Sim</span><span class="sxs-lookup"><span data-stu-id="8b587-1633">Yes</span></span> |
| <span data-ttu-id="8b587-1634">Nome de Usuário</span><span class="sxs-lookup"><span data-stu-id="8b587-1634">username</span></span> |<span data-ttu-id="8b587-1635">Especifique o nome de usuário se você estiver usando a autenticação Basic ou Windows.</span><span class="sxs-lookup"><span data-stu-id="8b587-1635">Specify user name if you are using Basic or Windows authentication.</span></span> |<span data-ttu-id="8b587-1636">Não</span><span class="sxs-lookup"><span data-stu-id="8b587-1636">No</span></span> |
| <span data-ttu-id="8b587-1637">Senha</span><span class="sxs-lookup"><span data-stu-id="8b587-1637">password</span></span> |<span data-ttu-id="8b587-1638">Especifique a senha da conta de usuário que você especificou para o nome de usuário.</span><span class="sxs-lookup"><span data-stu-id="8b587-1638">Specify password for the user account you specified for the username.</span></span> |<span data-ttu-id="8b587-1639">Não</span><span class="sxs-lookup"><span data-stu-id="8b587-1639">No</span></span> |
| <span data-ttu-id="8b587-1640">gatewayName</span><span class="sxs-lookup"><span data-stu-id="8b587-1640">gatewayName</span></span> |<span data-ttu-id="8b587-1641">O nome do gateway que o serviço Data Factory deve usar para se conectar ao banco de dados local do Sybase.</span><span class="sxs-lookup"><span data-stu-id="8b587-1641">Name of the gateway that the Data Factory service should use to connect to the on-premises Sybase database.</span></span> |<span data-ttu-id="8b587-1642">Sim</span><span class="sxs-lookup"><span data-stu-id="8b587-1642">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="8b587-1643">Exemplo</span><span class="sxs-lookup"><span data-stu-id="8b587-1643">Example</span></span>
```json
{
    "name": "OnPremSybaseLinkedService",
    "properties": {
        "type": "OnPremisesSybase",
        "typeProperties": {
            "server": "<server>",
            "database": "<database>",
            "schema": "<schema>",
            "authenticationType": "<authentication type>",
            "username": "<username>",
            "password": "<password>",
            "gatewayName": "<gatewayName>"
        }
    }
}
```

<span data-ttu-id="8b587-1644">Para obter mais informações, consulte o artigo [Conector do Sybase](data-factory-onprem-sybase-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="8b587-1644">For more information, see [Sybase connector](data-factory-onprem-sybase-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="8b587-1645">Conjunto de dados</span><span class="sxs-lookup"><span data-stu-id="8b587-1645">Dataset</span></span>
<span data-ttu-id="8b587-1646">Para definir um conjunto de dados do Sybase, defina o **type** do conjunto de dados para **RelationalTable** e especifique as propriedades a seguir na seção **typeProperties**:</span><span class="sxs-lookup"><span data-stu-id="8b587-1646">To define a Sybase dataset, set the **type** of the dataset to **RelationalTable**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="8b587-1647">Propriedade</span><span class="sxs-lookup"><span data-stu-id="8b587-1647">Property</span></span> | <span data-ttu-id="8b587-1648">Descrição</span><span class="sxs-lookup"><span data-stu-id="8b587-1648">Description</span></span> | <span data-ttu-id="8b587-1649">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="8b587-1649">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8b587-1650">tableName</span><span class="sxs-lookup"><span data-stu-id="8b587-1650">tableName</span></span> |<span data-ttu-id="8b587-1651">Nome da tabela na instância do banco de dados Sybase à qual o serviço vinculado se refere.</span><span class="sxs-lookup"><span data-stu-id="8b587-1651">Name of the table in the Sybase Database instance that linked service refers to.</span></span> |<span data-ttu-id="8b587-1652">Não (se **query** de **RelationalSource** for especificado)</span><span class="sxs-lookup"><span data-stu-id="8b587-1652">No (if **query** of **RelationalSource** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="8b587-1653">Exemplo</span><span class="sxs-lookup"><span data-stu-id="8b587-1653">Example</span></span>

```json
{
    "name": "SybaseDataSet",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "OnPremSybaseLinkedService",
        "typeProperties": {},
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```

<span data-ttu-id="8b587-1654">Para obter mais informações, consulte o artigo [Conector do Sybase](data-factory-onprem-sybase-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="8b587-1654">For more information, see [Sybase connector](data-factory-onprem-sybase-connector.md#dataset-properties) article.</span></span> 

### <a name="relational-source-in-copy-activity"></a><span data-ttu-id="8b587-1655">Origem Relacional na Atividade de Cópia</span><span class="sxs-lookup"><span data-stu-id="8b587-1655">Relational Source in Copy Activity</span></span>
<span data-ttu-id="8b587-1656">Se você estiver copiando dados de um banco de dados do Sybase, defina o **source type** da atividade de cópia para **RelationalSource** e especifique as propriedades a seguir na seção **source**:</span><span class="sxs-lookup"><span data-stu-id="8b587-1656">If you are copying data from a Sybase database, set the **source type** of the copy activity to **RelationalSource**, and specify following properties in the **source** section:</span></span>


| <span data-ttu-id="8b587-1657">Propriedade</span><span class="sxs-lookup"><span data-stu-id="8b587-1657">Property</span></span> | <span data-ttu-id="8b587-1658">Descrição</span><span class="sxs-lookup"><span data-stu-id="8b587-1658">Description</span></span> | <span data-ttu-id="8b587-1659">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="8b587-1659">Allowed values</span></span> | <span data-ttu-id="8b587-1660">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="8b587-1660">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="8b587-1661">query</span><span class="sxs-lookup"><span data-stu-id="8b587-1661">query</span></span> |<span data-ttu-id="8b587-1662">Utiliza a consulta personalizada para ler os dados.</span><span class="sxs-lookup"><span data-stu-id="8b587-1662">Use the custom query to read data.</span></span> |<span data-ttu-id="8b587-1663">Cadeia de caracteres de consulta SQL.</span><span class="sxs-lookup"><span data-stu-id="8b587-1663">SQL query string.</span></span> <span data-ttu-id="8b587-1664">Por exemplo: `select * from MyTable`.</span><span class="sxs-lookup"><span data-stu-id="8b587-1664">For example: `select * from MyTable`.</span></span> |<span data-ttu-id="8b587-1665">Não (se **tableName** de **dataset** for especificado)</span><span class="sxs-lookup"><span data-stu-id="8b587-1665">No (if **tableName** of **dataset** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="8b587-1666">Exemplo</span><span class="sxs-lookup"><span data-stu-id="8b587-1666">Example</span></span>

```json
{
    "name": "CopySybaseToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "select * from DBA.Orders"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "inputs": [{
                "name": "SybaseDataSet"
            }],
            "outputs": [{
                "name": "AzureBlobSybaseDataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "SybaseToBlob"
        }],
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00"
    }
}
```

<span data-ttu-id="8b587-1667">Para obter mais informações, consulte o artigo [Conector do Sybase](data-factory-onprem-sybase-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="8b587-1667">For more information, see [Sybase connector](data-factory-onprem-sybase-connector.md#copy-activity-properties) article.</span></span>

## <a name="teradata"></a><span data-ttu-id="8b587-1668">Teradata</span><span class="sxs-lookup"><span data-stu-id="8b587-1668">Teradata</span></span>

### <a name="linked-service"></a><span data-ttu-id="8b587-1669">Serviço vinculado</span><span class="sxs-lookup"><span data-stu-id="8b587-1669">Linked service</span></span>
<span data-ttu-id="8b587-1670">Para definir um serviço vinculado do Teradata, defina o **type** do serviço vinculado para **OnPremisesTeradata** e especifique as propriedades a seguir na seção **typeProperties**:</span><span class="sxs-lookup"><span data-stu-id="8b587-1670">To define a Teradata linked service, set the **type** of the linked service to **OnPremisesTeradata**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="8b587-1671">Propriedade</span><span class="sxs-lookup"><span data-stu-id="8b587-1671">Property</span></span> | <span data-ttu-id="8b587-1672">Descrição</span><span class="sxs-lookup"><span data-stu-id="8b587-1672">Description</span></span> | <span data-ttu-id="8b587-1673">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="8b587-1673">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8b587-1674">server</span><span class="sxs-lookup"><span data-stu-id="8b587-1674">server</span></span> |<span data-ttu-id="8b587-1675">Nome do servidor Teradata.</span><span class="sxs-lookup"><span data-stu-id="8b587-1675">Name of the Teradata server.</span></span> |<span data-ttu-id="8b587-1676">Sim</span><span class="sxs-lookup"><span data-stu-id="8b587-1676">Yes</span></span> |
| <span data-ttu-id="8b587-1677">authenticationType</span><span class="sxs-lookup"><span data-stu-id="8b587-1677">authenticationType</span></span> |<span data-ttu-id="8b587-1678">Tipo de autenticação usado para se conectar ao banco de dados Teradata.</span><span class="sxs-lookup"><span data-stu-id="8b587-1678">Type of authentication used to connect to the Teradata database.</span></span> <span data-ttu-id="8b587-1679">Os valores possíveis são: Anonymous, Basic e Windows.</span><span class="sxs-lookup"><span data-stu-id="8b587-1679">Possible values are: Anonymous, Basic, and Windows.</span></span> |<span data-ttu-id="8b587-1680">Sim</span><span class="sxs-lookup"><span data-stu-id="8b587-1680">Yes</span></span> |
| <span data-ttu-id="8b587-1681">Nome de Usuário</span><span class="sxs-lookup"><span data-stu-id="8b587-1681">username</span></span> |<span data-ttu-id="8b587-1682">Especifique o nome de usuário se você estiver usando a autenticação Basic ou Windows.</span><span class="sxs-lookup"><span data-stu-id="8b587-1682">Specify user name if you are using Basic or Windows authentication.</span></span> |<span data-ttu-id="8b587-1683">Não</span><span class="sxs-lookup"><span data-stu-id="8b587-1683">No</span></span> |
| <span data-ttu-id="8b587-1684">Senha</span><span class="sxs-lookup"><span data-stu-id="8b587-1684">password</span></span> |<span data-ttu-id="8b587-1685">Especifique a senha da conta de usuário que você especificou para o nome de usuário.</span><span class="sxs-lookup"><span data-stu-id="8b587-1685">Specify password for the user account you specified for the username.</span></span> |<span data-ttu-id="8b587-1686">Não</span><span class="sxs-lookup"><span data-stu-id="8b587-1686">No</span></span> |
| <span data-ttu-id="8b587-1687">gatewayName</span><span class="sxs-lookup"><span data-stu-id="8b587-1687">gatewayName</span></span> |<span data-ttu-id="8b587-1688">O nome do gateway que o serviço Data Factory deve usar para se conectar ao banco de dados Teradata local.</span><span class="sxs-lookup"><span data-stu-id="8b587-1688">Name of the gateway that the Data Factory service should use to connect to the on-premises Teradata database.</span></span> |<span data-ttu-id="8b587-1689">Sim</span><span class="sxs-lookup"><span data-stu-id="8b587-1689">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="8b587-1690">Exemplo</span><span class="sxs-lookup"><span data-stu-id="8b587-1690">Example</span></span>
```json
{
    "name": "OnPremTeradataLinkedService",
    "properties": {
        "type": "OnPremisesTeradata",
        "typeProperties": {
            "server": "<server>",
            "authenticationType": "<authentication type>",
            "username": "<username>",
            "password": "<password>",
            "gatewayName": "<gatewayName>"
        }
    }
}
```

<span data-ttu-id="8b587-1691">Para obter mais informações, consulte o artigo [Conector do Teradata](data-factory-onprem-teradata-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="8b587-1691">For more information, see [Teradata connector](data-factory-onprem-teradata-connector.md#linked-service-properties) article.</span></span>

### <a name="dataset"></a><span data-ttu-id="8b587-1692">Conjunto de dados</span><span class="sxs-lookup"><span data-stu-id="8b587-1692">Dataset</span></span>
<span data-ttu-id="8b587-1693">Para definir o conjunto de dados do Blobo do Teradata defina o **type** do conjunto de dados como **RelationalTable**.</span><span class="sxs-lookup"><span data-stu-id="8b587-1693">To define a Teradata Blob dataset, set the **type** of the dataset to **RelationalTable**.</span></span> <span data-ttu-id="8b587-1694">Atualmente, não há nenhuma propriedade do tipo com suporte para o conjunto de dados Teradata.</span><span class="sxs-lookup"><span data-stu-id="8b587-1694">Currently, there are no type properties supported for the Teradata dataset.</span></span> 

#### <a name="example"></a><span data-ttu-id="8b587-1695">Exemplo</span><span class="sxs-lookup"><span data-stu-id="8b587-1695">Example</span></span>
```json
{
    "name": "TeradataDataSet",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "OnPremTeradataLinkedService",
        "typeProperties": {},
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```

<span data-ttu-id="8b587-1696">Para obter mais informações, consulte o artigo [Conector do Teradata](data-factory-onprem-teradata-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="8b587-1696">For more information, see [Teradata connector](data-factory-onprem-teradata-connector.md#dataset-properties) article.</span></span>

### <a name="relational-source-in-copy-activity"></a><span data-ttu-id="8b587-1697">Origem Relacional na Atividade de Cópia</span><span class="sxs-lookup"><span data-stu-id="8b587-1697">Relational Source in Copy Activity</span></span>
<span data-ttu-id="8b587-1698">Se você estiver copiando dados de um banco de dados do Teradata, defina o **source type** da atividade de cópia para **RelationalSource** e especifique as propriedades a seguir na seção **source**:</span><span class="sxs-lookup"><span data-stu-id="8b587-1698">If you are copying data from a Teradata database, set the **source type** of the copy activity to **RelationalSource**, and specify following properties in the **source** section:</span></span>

| <span data-ttu-id="8b587-1699">Propriedade</span><span class="sxs-lookup"><span data-stu-id="8b587-1699">Property</span></span> | <span data-ttu-id="8b587-1700">Descrição</span><span class="sxs-lookup"><span data-stu-id="8b587-1700">Description</span></span> | <span data-ttu-id="8b587-1701">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="8b587-1701">Allowed values</span></span> | <span data-ttu-id="8b587-1702">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="8b587-1702">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="8b587-1703">query</span><span class="sxs-lookup"><span data-stu-id="8b587-1703">query</span></span> |<span data-ttu-id="8b587-1704">Utiliza a consulta personalizada para ler os dados.</span><span class="sxs-lookup"><span data-stu-id="8b587-1704">Use the custom query to read data.</span></span> |<span data-ttu-id="8b587-1705">Cadeia de caracteres de consulta SQL.</span><span class="sxs-lookup"><span data-stu-id="8b587-1705">SQL query string.</span></span> <span data-ttu-id="8b587-1706">Por exemplo: `select * from MyTable`.</span><span class="sxs-lookup"><span data-stu-id="8b587-1706">For example: `select * from MyTable`.</span></span> |<span data-ttu-id="8b587-1707">Sim</span><span class="sxs-lookup"><span data-stu-id="8b587-1707">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="8b587-1708">Exemplo</span><span class="sxs-lookup"><span data-stu-id="8b587-1708">Example</span></span>

```json
{
    "name": "CopyTeradataToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "$$Text.Format('select * from MyTable where timestamp >= \\'{0:yyyy-MM-ddTHH:mm:ss}\\' AND timestamp < \\'{1:yyyy-MM-ddTHH:mm:ss}\\'', SliceStart, SliceEnd)"
                },
                "sink": {
                    "type": "BlobSink",
                    "writeBatchSize": 0,
                    "writeBatchTimeout": "00:00:00"
                }
            },
            "inputs": [{
                "name": "TeradataDataSet"
            }],
            "outputs": [{
                "name": "AzureBlobTeradataDataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "TeradataToBlob"
        }],
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "isPaused": false
    }
}
```

<span data-ttu-id="8b587-1709">Para obter mais informações, consulte o artigo [Conector do Teradata](data-factory-onprem-teradata-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="8b587-1709">For more information, see [Teradata connector](data-factory-onprem-teradata-connector.md#copy-activity-properties) article.</span></span>

## <a name="cassandra"></a><span data-ttu-id="8b587-1710">Cassandra</span><span class="sxs-lookup"><span data-stu-id="8b587-1710">Cassandra</span></span>


### <a name="linked-service"></a><span data-ttu-id="8b587-1711">Serviço vinculado</span><span class="sxs-lookup"><span data-stu-id="8b587-1711">Linked service</span></span>
<span data-ttu-id="8b587-1712">Para definir um serviço vinculado do Cassandra, defina o **type** do serviço vinculado para **OnPremisesCassandra** e especifique as propriedades a seguir na seção **typeProperties**:</span><span class="sxs-lookup"><span data-stu-id="8b587-1712">To define a Cassandra linked service, set the **type** of the linked service to **OnPremisesCassandra**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="8b587-1713">Propriedade</span><span class="sxs-lookup"><span data-stu-id="8b587-1713">Property</span></span> | <span data-ttu-id="8b587-1714">Descrição</span><span class="sxs-lookup"><span data-stu-id="8b587-1714">Description</span></span> | <span data-ttu-id="8b587-1715">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="8b587-1715">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8b587-1716">host</span><span class="sxs-lookup"><span data-stu-id="8b587-1716">host</span></span> |<span data-ttu-id="8b587-1717">Um ou mais endereços IP ou nomes de host dos servidores Cassandra.</span><span class="sxs-lookup"><span data-stu-id="8b587-1717">One or more IP addresses or host names of Cassandra servers.</span></span><br/><br/><span data-ttu-id="8b587-1718">Especifique uma lista separada por vírgulas de endereços IP ou nomes de host para se conectar simultaneamente a todos os servidores.</span><span class="sxs-lookup"><span data-stu-id="8b587-1718">Specify a comma-separated list of IP addresses or host names to connect to all servers concurrently.</span></span> |<span data-ttu-id="8b587-1719">Sim</span><span class="sxs-lookup"><span data-stu-id="8b587-1719">Yes</span></span> |
| <span data-ttu-id="8b587-1720">porta</span><span class="sxs-lookup"><span data-stu-id="8b587-1720">port</span></span> |<span data-ttu-id="8b587-1721">A porta TCP usada pelo servidor Cassandra para ouvir conexões de cliente.</span><span class="sxs-lookup"><span data-stu-id="8b587-1721">The TCP port that the Cassandra server uses to listen for client connections.</span></span> |<span data-ttu-id="8b587-1722">Não, valor padrão: 9042</span><span class="sxs-lookup"><span data-stu-id="8b587-1722">No, default value: 9042</span></span> |
| <span data-ttu-id="8b587-1723">authenticationType</span><span class="sxs-lookup"><span data-stu-id="8b587-1723">authenticationType</span></span> |<span data-ttu-id="8b587-1724">Básica, ou Anônima</span><span class="sxs-lookup"><span data-stu-id="8b587-1724">Basic, or Anonymous</span></span> |<span data-ttu-id="8b587-1725">Sim</span><span class="sxs-lookup"><span data-stu-id="8b587-1725">Yes</span></span> |
| <span data-ttu-id="8b587-1726">Nome de Usuário</span><span class="sxs-lookup"><span data-stu-id="8b587-1726">username</span></span> |<span data-ttu-id="8b587-1727">Especifique o nome de usuário da conta de usuário.</span><span class="sxs-lookup"><span data-stu-id="8b587-1727">Specify user name for the user account.</span></span> |<span data-ttu-id="8b587-1728">Sim, se authenticationType for definida como Básica.</span><span class="sxs-lookup"><span data-stu-id="8b587-1728">Yes, if authenticationType is set to Basic.</span></span> |
| <span data-ttu-id="8b587-1729">Senha</span><span class="sxs-lookup"><span data-stu-id="8b587-1729">password</span></span> |<span data-ttu-id="8b587-1730">Especifique a senha para a conta de usuário.</span><span class="sxs-lookup"><span data-stu-id="8b587-1730">Specify password for the user account.</span></span> |<span data-ttu-id="8b587-1731">Sim, se authenticationType for definida como Básica.</span><span class="sxs-lookup"><span data-stu-id="8b587-1731">Yes, if authenticationType is set to Basic.</span></span> |
| <span data-ttu-id="8b587-1732">gatewayName</span><span class="sxs-lookup"><span data-stu-id="8b587-1732">gatewayName</span></span> |<span data-ttu-id="8b587-1733">O nome do gateway que é usado para se conectar ao servidor Cassandra local.</span><span class="sxs-lookup"><span data-stu-id="8b587-1733">The name of the gateway that is used to connect to the on-premises Cassandra database.</span></span> |<span data-ttu-id="8b587-1734">Sim</span><span class="sxs-lookup"><span data-stu-id="8b587-1734">Yes</span></span> |
| <span data-ttu-id="8b587-1735">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="8b587-1735">encryptedCredential</span></span> |<span data-ttu-id="8b587-1736">Credencial criptografada pelo gateway.</span><span class="sxs-lookup"><span data-stu-id="8b587-1736">Credential encrypted by the gateway.</span></span> |<span data-ttu-id="8b587-1737">Não</span><span class="sxs-lookup"><span data-stu-id="8b587-1737">No</span></span> |

#### <a name="example"></a><span data-ttu-id="8b587-1738">Exemplo</span><span class="sxs-lookup"><span data-stu-id="8b587-1738">Example</span></span>

```json
{
    "name": "CassandraLinkedService",
    "properties": {
        "type": "OnPremisesCassandra",
        "typeProperties": {
            "authenticationType": "Basic",
            "host": "<cassandra server name or IP address>",
            "port": 9042,
            "username": "user",
            "password": "password",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

<span data-ttu-id="8b587-1739">Para obter mais informações, consulte o artigo [Conector do Cassandra](data-factory-onprem-cassandra-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="8b587-1739">For more information, see [Cassandra connector](data-factory-onprem-cassandra-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="8b587-1740">Conjunto de dados</span><span class="sxs-lookup"><span data-stu-id="8b587-1740">Dataset</span></span>
<span data-ttu-id="8b587-1741">Para definir um conjunto de dados do Cassandra, defina o **type** do conjunto de dados para **CassandraTable** e especifique as propriedades a seguir na seção **typeProperties**:</span><span class="sxs-lookup"><span data-stu-id="8b587-1741">To define a Cassandra dataset, set the **type** of the dataset to **CassandraTable**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="8b587-1742">Propriedade</span><span class="sxs-lookup"><span data-stu-id="8b587-1742">Property</span></span> | <span data-ttu-id="8b587-1743">Descrição</span><span class="sxs-lookup"><span data-stu-id="8b587-1743">Description</span></span> | <span data-ttu-id="8b587-1744">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="8b587-1744">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8b587-1745">keyspace</span><span class="sxs-lookup"><span data-stu-id="8b587-1745">keyspace</span></span> |<span data-ttu-id="8b587-1746">Nome do keyspace ou do esquema no banco de dados Cassandra.</span><span class="sxs-lookup"><span data-stu-id="8b587-1746">Name of the keyspace or schema in Cassandra database.</span></span> |<span data-ttu-id="8b587-1747">Sim (se a **consulta** para **CassandraSource** não estiver definida).</span><span class="sxs-lookup"><span data-stu-id="8b587-1747">Yes (If **query** for **CassandraSource** is not defined).</span></span> |
| <span data-ttu-id="8b587-1748">tableName</span><span class="sxs-lookup"><span data-stu-id="8b587-1748">tableName</span></span> |<span data-ttu-id="8b587-1749">Nome da tabela no banco de dados Cassandra.</span><span class="sxs-lookup"><span data-stu-id="8b587-1749">Name of the table in Cassandra database.</span></span> |<span data-ttu-id="8b587-1750">Sim (se a **consulta** para **CassandraSource** não estiver definida).</span><span class="sxs-lookup"><span data-stu-id="8b587-1750">Yes (If **query** for **CassandraSource** is not defined).</span></span> |

#### <a name="example"></a><span data-ttu-id="8b587-1751">Exemplo</span><span class="sxs-lookup"><span data-stu-id="8b587-1751">Example</span></span>

```json
{
    "name": "CassandraInput",
    "properties": {
        "linkedServiceName": "CassandraLinkedService",
        "type": "CassandraTable",
        "typeProperties": {
            "tableName": "mytable",
            "keySpace": "<key space>"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```

<span data-ttu-id="8b587-1752">Para obter mais informações, consulte o artigo [Conector do Cassandra](data-factory-onprem-cassandra-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="8b587-1752">For more information, see [Cassandra connector](data-factory-onprem-cassandra-connector.md#dataset-properties) article.</span></span> 

### <a name="cassandra-source-in-copy-activity"></a><span data-ttu-id="8b587-1753">Origem do Cassandra na Atividade de Cópia</span><span class="sxs-lookup"><span data-stu-id="8b587-1753">Cassandra Source in Copy Activity</span></span>
<span data-ttu-id="8b587-1754">Se você estiver copiando dados do Cassandra, defina o **source type** da atividade de cópia para **CassandraSource** e especifique as propriedades a seguir na seção **source**:</span><span class="sxs-lookup"><span data-stu-id="8b587-1754">If you are copying data from Cassandra, set the **source type** of the copy activity to **CassandraSource**, and specify following properties in the **source** section:</span></span>

| <span data-ttu-id="8b587-1755">Propriedade</span><span class="sxs-lookup"><span data-stu-id="8b587-1755">Property</span></span> | <span data-ttu-id="8b587-1756">Descrição</span><span class="sxs-lookup"><span data-stu-id="8b587-1756">Description</span></span> | <span data-ttu-id="8b587-1757">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="8b587-1757">Allowed values</span></span> | <span data-ttu-id="8b587-1758">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="8b587-1758">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="8b587-1759">query</span><span class="sxs-lookup"><span data-stu-id="8b587-1759">query</span></span> |<span data-ttu-id="8b587-1760">Utiliza a consulta personalizada para ler os dados.</span><span class="sxs-lookup"><span data-stu-id="8b587-1760">Use the custom query to read data.</span></span> |<span data-ttu-id="8b587-1761">Consulta SQL-92 ou consulta CQL.</span><span class="sxs-lookup"><span data-stu-id="8b587-1761">SQL-92 query or CQL query.</span></span> <span data-ttu-id="8b587-1762">Veja [Referência ao CQL](https://docs.datastax.com/en/cql/3.1/cql/cql_reference/cqlReferenceTOC.html).</span><span class="sxs-lookup"><span data-stu-id="8b587-1762">See [CQL reference](https://docs.datastax.com/en/cql/3.1/cql/cql_reference/cqlReferenceTOC.html).</span></span> <br/><br/><span data-ttu-id="8b587-1763">Ao usar a consulta SQL, especifique **keyspace name.table name** para representar a tabela que deseja consultar.</span><span class="sxs-lookup"><span data-stu-id="8b587-1763">When using SQL query, specify **keyspace name.table name** to represent the table you want to query.</span></span> |<span data-ttu-id="8b587-1764">Não (se tableName e keyspace no conjunto de dados estiverem definidos).</span><span class="sxs-lookup"><span data-stu-id="8b587-1764">No (if tableName and keyspace on dataset are defined).</span></span> |
| <span data-ttu-id="8b587-1765">consistencyLevel</span><span class="sxs-lookup"><span data-stu-id="8b587-1765">consistencyLevel</span></span> |<span data-ttu-id="8b587-1766">O nível de consistência especifica quantas réplicas devem responder a uma solicitação de leitura antes de retornar dados ao aplicativo cliente.</span><span class="sxs-lookup"><span data-stu-id="8b587-1766">The consistency level specifies how many replicas must respond to a read request before returning data to the client application.</span></span> <span data-ttu-id="8b587-1767">O Cassandra verifica o número especificado de réplicas de dados atender à solicitação de leitura.</span><span class="sxs-lookup"><span data-stu-id="8b587-1767">Cassandra checks the specified number of replicas for data to satisfy the read request.</span></span> |<span data-ttu-id="8b587-1768">ONE, TWO, THREE, QUORUM, ALL, LOCAL_QUORUM, EACH_QUORUM, LOCAL_ONE.</span><span class="sxs-lookup"><span data-stu-id="8b587-1768">ONE, TWO, THREE, QUORUM, ALL, LOCAL_QUORUM, EACH_QUORUM, LOCAL_ONE.</span></span> <span data-ttu-id="8b587-1769">Confira [Configuring data consistency (Configurando a consistência de dados)](http://docs.datastax.com/en//cassandra/2.0/cassandra/dml/dml_config_consistency_c.html) para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="8b587-1769">See [Configuring data consistency](http://docs.datastax.com/en//cassandra/2.0/cassandra/dml/dml_config_consistency_c.html) for details.</span></span> |<span data-ttu-id="8b587-1770">Não.</span><span class="sxs-lookup"><span data-stu-id="8b587-1770">No.</span></span> <span data-ttu-id="8b587-1771">O valor padrão é ONE.</span><span class="sxs-lookup"><span data-stu-id="8b587-1771">Default value is ONE.</span></span> |

#### <a name="example"></a><span data-ttu-id="8b587-1772">Exemplo</span><span class="sxs-lookup"><span data-stu-id="8b587-1772">Example</span></span>
  
```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "CassandraToAzureBlob",
            "description": "Copy from Cassandra to an Azure blob",
            "type": "Copy",
            "inputs": [{
                "name": "CassandraInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "CassandraSource",
                    "query": "select id, firstname, lastname from mykeyspace.mytable"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

<span data-ttu-id="8b587-1773">Para obter mais informações, consulte o artigo [Conector do Cassandra](data-factory-onprem-cassandra-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="8b587-1773">For more information, see [Cassandra connector](data-factory-onprem-cassandra-connector.md#copy-activity-properties) article.</span></span>

## <a name="mongodb"></a><span data-ttu-id="8b587-1774">MongoDB</span><span class="sxs-lookup"><span data-stu-id="8b587-1774">MongoDB</span></span>

### <a name="linked-service"></a><span data-ttu-id="8b587-1775">Serviço vinculado</span><span class="sxs-lookup"><span data-stu-id="8b587-1775">Linked service</span></span>
<span data-ttu-id="8b587-1776">Para definir um serviço vinculado do MongoDB, defina o **type** do serviço vinculado para **OnPremisesMongoDB** e especifique as propriedades a seguir na seção **typeProperties**:</span><span class="sxs-lookup"><span data-stu-id="8b587-1776">To define a MongoDB linked service, set the **type** of the linked service to **OnPremisesMongoDB**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="8b587-1777">Propriedade</span><span class="sxs-lookup"><span data-stu-id="8b587-1777">Property</span></span> | <span data-ttu-id="8b587-1778">Descrição</span><span class="sxs-lookup"><span data-stu-id="8b587-1778">Description</span></span> | <span data-ttu-id="8b587-1779">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="8b587-1779">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8b587-1780">server</span><span class="sxs-lookup"><span data-stu-id="8b587-1780">server</span></span> |<span data-ttu-id="8b587-1781">Endereço IP ou nome do host do servidor MongoDB.</span><span class="sxs-lookup"><span data-stu-id="8b587-1781">IP address or host name of the MongoDB server.</span></span> |<span data-ttu-id="8b587-1782">Sim</span><span class="sxs-lookup"><span data-stu-id="8b587-1782">Yes</span></span> |
| <span data-ttu-id="8b587-1783">porta</span><span class="sxs-lookup"><span data-stu-id="8b587-1783">port</span></span> |<span data-ttu-id="8b587-1784">A porta TCP usada pelo servidor MongoDB para ouvir conexões de cliente.</span><span class="sxs-lookup"><span data-stu-id="8b587-1784">TCP port that the MongoDB server uses to listen for client connections.</span></span> |<span data-ttu-id="8b587-1785">Opcional, valor padrão: 27017</span><span class="sxs-lookup"><span data-stu-id="8b587-1785">Optional, default value: 27017</span></span> |
| <span data-ttu-id="8b587-1786">authenticationType</span><span class="sxs-lookup"><span data-stu-id="8b587-1786">authenticationType</span></span> |<span data-ttu-id="8b587-1787">Básica ou Anônima.</span><span class="sxs-lookup"><span data-stu-id="8b587-1787">Basic, or Anonymous.</span></span> |<span data-ttu-id="8b587-1788">Sim</span><span class="sxs-lookup"><span data-stu-id="8b587-1788">Yes</span></span> |
| <span data-ttu-id="8b587-1789">Nome de Usuário</span><span class="sxs-lookup"><span data-stu-id="8b587-1789">username</span></span> |<span data-ttu-id="8b587-1790">Conta de usuário para acessar o MongoDB.</span><span class="sxs-lookup"><span data-stu-id="8b587-1790">User account to access MongoDB.</span></span> |<span data-ttu-id="8b587-1791">Sim (se a autenticação básica for usada).</span><span class="sxs-lookup"><span data-stu-id="8b587-1791">Yes (if basic authentication is used).</span></span> |
| <span data-ttu-id="8b587-1792">Senha</span><span class="sxs-lookup"><span data-stu-id="8b587-1792">password</span></span> |<span data-ttu-id="8b587-1793">Senha do usuário.</span><span class="sxs-lookup"><span data-stu-id="8b587-1793">Password for the user.</span></span> |<span data-ttu-id="8b587-1794">Sim (se a autenticação básica for usada).</span><span class="sxs-lookup"><span data-stu-id="8b587-1794">Yes (if basic authentication is used).</span></span> |
| <span data-ttu-id="8b587-1795">authSource</span><span class="sxs-lookup"><span data-stu-id="8b587-1795">authSource</span></span> |<span data-ttu-id="8b587-1796">Nome do banco de dados MongoDB que você deseja usar para verificar suas credenciais para autenticação.</span><span class="sxs-lookup"><span data-stu-id="8b587-1796">Name of the MongoDB database that you want to use to check your credentials for authentication.</span></span> |<span data-ttu-id="8b587-1797">Opcional (se a autenticação básica for usada).</span><span class="sxs-lookup"><span data-stu-id="8b587-1797">Optional (if basic authentication is used).</span></span> <span data-ttu-id="8b587-1798">Padrão: usa a conta de administrador e o banco de dados especificado usando a propriedade databaseName.</span><span class="sxs-lookup"><span data-stu-id="8b587-1798">default: uses the admin account and the database specified using databaseName property.</span></span> |
| <span data-ttu-id="8b587-1799">databaseName</span><span class="sxs-lookup"><span data-stu-id="8b587-1799">databaseName</span></span> |<span data-ttu-id="8b587-1800">Nome do banco de dados MongoDB que você deseja acessar.</span><span class="sxs-lookup"><span data-stu-id="8b587-1800">Name of the MongoDB database that you want to access.</span></span> |<span data-ttu-id="8b587-1801">Sim</span><span class="sxs-lookup"><span data-stu-id="8b587-1801">Yes</span></span> |
| <span data-ttu-id="8b587-1802">gatewayName</span><span class="sxs-lookup"><span data-stu-id="8b587-1802">gatewayName</span></span> |<span data-ttu-id="8b587-1803">Nome do gateway que acessa o armazenamento de dados.</span><span class="sxs-lookup"><span data-stu-id="8b587-1803">Name of the gateway that accesses the data store.</span></span> |<span data-ttu-id="8b587-1804">Sim</span><span class="sxs-lookup"><span data-stu-id="8b587-1804">Yes</span></span> |
| <span data-ttu-id="8b587-1805">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="8b587-1805">encryptedCredential</span></span> |<span data-ttu-id="8b587-1806">Credencial criptografada pelo gateway.</span><span class="sxs-lookup"><span data-stu-id="8b587-1806">Credential encrypted by gateway.</span></span> |<span data-ttu-id="8b587-1807">Opcional</span><span class="sxs-lookup"><span data-stu-id="8b587-1807">Optional</span></span> |

#### <a name="example"></a><span data-ttu-id="8b587-1808">Exemplo</span><span class="sxs-lookup"><span data-stu-id="8b587-1808">Example</span></span>

```json
{
    "name": "OnPremisesMongoDbLinkedService",
    "properties": {
        "type": "OnPremisesMongoDb",
        "typeProperties": {
            "authenticationType": "<Basic or Anonymous>",
            "server": "< The IP address or host name of the MongoDB server >",
            "port": "<The number of the TCP port that the MongoDB server uses to listen for client connections.>",
            "username": "<username>",
            "password": "<password>",
            "authSource": "< The database that you want to use to check your credentials for authentication. >",
            "databaseName": "<database name>",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

<span data-ttu-id="8b587-1809">Para obter mais informações, consulte o artigo [Conector do MongoDB](data-factory-on-premises-mongodb-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="8b587-1809">For more information, see [MongoDB connector article](data-factory-on-premises-mongodb-connector.md#linked-service-properties)</span></span>

### <a name="dataset"></a><span data-ttu-id="8b587-1810">Conjunto de dados</span><span class="sxs-lookup"><span data-stu-id="8b587-1810">Dataset</span></span>
<span data-ttu-id="8b587-1811">Para definir um conjunto de dados do MongoDB, defina o **type** do conjunto de dados para **MongoDbCollection** e especifique as propriedades a seguir na seção **typeProperties**:</span><span class="sxs-lookup"><span data-stu-id="8b587-1811">To define a MongoDB dataset, set the **type** of the dataset to **MongoDbCollection**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="8b587-1812">Propriedade</span><span class="sxs-lookup"><span data-stu-id="8b587-1812">Property</span></span> | <span data-ttu-id="8b587-1813">Descrição</span><span class="sxs-lookup"><span data-stu-id="8b587-1813">Description</span></span> | <span data-ttu-id="8b587-1814">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="8b587-1814">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8b587-1815">collectionName</span><span class="sxs-lookup"><span data-stu-id="8b587-1815">collectionName</span></span> |<span data-ttu-id="8b587-1816">Nome da coleção no banco de dados MongoDB.</span><span class="sxs-lookup"><span data-stu-id="8b587-1816">Name of the collection in MongoDB database.</span></span> |<span data-ttu-id="8b587-1817">Sim</span><span class="sxs-lookup"><span data-stu-id="8b587-1817">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="8b587-1818">Exemplo</span><span class="sxs-lookup"><span data-stu-id="8b587-1818">Example</span></span>

```json
{
    "name": "MongoDbInputDataset",
    "properties": {
        "type": "MongoDbCollection",
        "linkedServiceName": "OnPremisesMongoDbLinkedService",
        "typeProperties": {
            "collectionName": "<Collection name>"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```

<span data-ttu-id="8b587-1819">Para obter mais informações, consulte o artigo [Conector do MongoDB](data-factory-on-premises-mongodb-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="8b587-1819">For more information, see [MongoDB connector article](data-factory-on-premises-mongodb-connector.md#dataset-properties)</span></span>

#### <a name="mongodb-source-in-copy-activity"></a><span data-ttu-id="8b587-1820">Origem do MongoDB na Atividade de Cópia</span><span class="sxs-lookup"><span data-stu-id="8b587-1820">MongoDB Source in Copy Activity</span></span>
<span data-ttu-id="8b587-1821">Se você estiver copiando dados do MongoDB, defina o **source type** da atividade de cópia para **MongoDbSource** e especifique as propriedades a seguir na seção **source**:</span><span class="sxs-lookup"><span data-stu-id="8b587-1821">If you are copying data from MongoDB, set the **source type** of the copy activity to **MongoDbSource**, and specify following properties in the **source** section:</span></span>

| <span data-ttu-id="8b587-1822">Propriedade</span><span class="sxs-lookup"><span data-stu-id="8b587-1822">Property</span></span> | <span data-ttu-id="8b587-1823">Descrição</span><span class="sxs-lookup"><span data-stu-id="8b587-1823">Description</span></span> | <span data-ttu-id="8b587-1824">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="8b587-1824">Allowed values</span></span> | <span data-ttu-id="8b587-1825">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="8b587-1825">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="8b587-1826">query</span><span class="sxs-lookup"><span data-stu-id="8b587-1826">query</span></span> |<span data-ttu-id="8b587-1827">Utiliza a consulta personalizada para ler os dados.</span><span class="sxs-lookup"><span data-stu-id="8b587-1827">Use the custom query to read data.</span></span> |<span data-ttu-id="8b587-1828">Cadeia de consulta SQL-92.</span><span class="sxs-lookup"><span data-stu-id="8b587-1828">SQL-92 query string.</span></span> <span data-ttu-id="8b587-1829">Por exemplo: `select * from MyTable`.</span><span class="sxs-lookup"><span data-stu-id="8b587-1829">For example: `select * from MyTable`.</span></span> |<span data-ttu-id="8b587-1830">Não (se **collectionName** de **dataset** for especificado)</span><span class="sxs-lookup"><span data-stu-id="8b587-1830">No (if **collectionName** of **dataset** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="8b587-1831">Exemplo</span><span class="sxs-lookup"><span data-stu-id="8b587-1831">Example</span></span>

```json
{
    "name": "CopyMongoDBToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "MongoDbSource",
                    "query": "select * from MyTable"
                },
                "sink": {
                    "type": "BlobSink",
                    "writeBatchSize": 0,
                    "writeBatchTimeout": "00:00:00"
                }
            },
            "inputs": [{
                "name": "MongoDbInputDataset"
            }],
            "outputs": [{
                "name": "AzureBlobOutputDataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "MongoDBToAzureBlob"
        }],
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00"
    }
}
```

<span data-ttu-id="8b587-1832">Para obter mais informações, consulte o artigo [Conector do MongoDB](data-factory-on-premises-mongodb-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="8b587-1832">For more information, see [MongoDB connector article](data-factory-on-premises-mongodb-connector.md#copy-activity-properties)</span></span>

## <a name="amazon-s3"></a><span data-ttu-id="8b587-1833">Amazon S3</span><span class="sxs-lookup"><span data-stu-id="8b587-1833">Amazon S3</span></span>


### <a name="linked-service"></a><span data-ttu-id="8b587-1834">Serviço vinculado</span><span class="sxs-lookup"><span data-stu-id="8b587-1834">Linked service</span></span>
<span data-ttu-id="8b587-1835">Para definir um serviço vinculado do Amazon S3, defina o **type** do serviço vinculado para **AwsAccessKey** e especifique as propriedades a seguir na seção **typeProperties**:</span><span class="sxs-lookup"><span data-stu-id="8b587-1835">To define an Amazon S3 linked service, set the **type** of the linked service to **AwsAccessKey**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="8b587-1836">Propriedade</span><span class="sxs-lookup"><span data-stu-id="8b587-1836">Property</span></span> | <span data-ttu-id="8b587-1837">Descrição</span><span class="sxs-lookup"><span data-stu-id="8b587-1837">Description</span></span> | <span data-ttu-id="8b587-1838">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="8b587-1838">Allowed values</span></span> | <span data-ttu-id="8b587-1839">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="8b587-1839">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="8b587-1840">accessKeyID</span><span class="sxs-lookup"><span data-stu-id="8b587-1840">accessKeyID</span></span> |<span data-ttu-id="8b587-1841">ID da chave de acesso secreta.</span><span class="sxs-lookup"><span data-stu-id="8b587-1841">ID of the secret access key.</span></span> |<span data-ttu-id="8b587-1842">string</span><span class="sxs-lookup"><span data-stu-id="8b587-1842">string</span></span> |<span data-ttu-id="8b587-1843">Sim</span><span class="sxs-lookup"><span data-stu-id="8b587-1843">Yes</span></span> |
| <span data-ttu-id="8b587-1844">secretAccessKey</span><span class="sxs-lookup"><span data-stu-id="8b587-1844">secretAccessKey</span></span> |<span data-ttu-id="8b587-1845">A chave de acesso do secreta em si.</span><span class="sxs-lookup"><span data-stu-id="8b587-1845">The secret access key itself.</span></span> |<span data-ttu-id="8b587-1846">Cadeia de caracteres secreta criptografada</span><span class="sxs-lookup"><span data-stu-id="8b587-1846">Encrypted secret string</span></span> |<span data-ttu-id="8b587-1847">Sim</span><span class="sxs-lookup"><span data-stu-id="8b587-1847">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="8b587-1848">Exemplo</span><span class="sxs-lookup"><span data-stu-id="8b587-1848">Example</span></span>
```json
{
    "name": "AmazonS3LinkedService",
    "properties": {
        "type": "AwsAccessKey",
        "typeProperties": {
            "accessKeyId": "<access key id>",
            "secretAccessKey": "<secret access key>"
        }
    }
}
```

<span data-ttu-id="8b587-1849">Para obter mais informações, consulte o artigo [Conector do Amazon S3](data-factory-amazon-simple-storage-service-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="8b587-1849">For more information, see [Amazon S3 connector article](data-factory-amazon-simple-storage-service-connector.md#linked-service-properties).</span></span>

### <a name="dataset"></a><span data-ttu-id="8b587-1850">Conjunto de dados</span><span class="sxs-lookup"><span data-stu-id="8b587-1850">Dataset</span></span>
<span data-ttu-id="8b587-1851">Para definir um conjunto de dados do Amazon S3, defina o **type** do conjunto de dados para **AmazonS3** e especifique as propriedades a seguir na seção **typeProperties**:</span><span class="sxs-lookup"><span data-stu-id="8b587-1851">To define an Amazon S3 dataset, set the **type** of the dataset to **AmazonS3**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="8b587-1852">Propriedade</span><span class="sxs-lookup"><span data-stu-id="8b587-1852">Property</span></span> | <span data-ttu-id="8b587-1853">Descrição</span><span class="sxs-lookup"><span data-stu-id="8b587-1853">Description</span></span> | <span data-ttu-id="8b587-1854">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="8b587-1854">Allowed values</span></span> | <span data-ttu-id="8b587-1855">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="8b587-1855">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="8b587-1856">bucketName</span><span class="sxs-lookup"><span data-stu-id="8b587-1856">bucketName</span></span> |<span data-ttu-id="8b587-1857">O nome do bucket S3.</span><span class="sxs-lookup"><span data-stu-id="8b587-1857">The S3 bucket name.</span></span> |<span data-ttu-id="8b587-1858">string</span><span class="sxs-lookup"><span data-stu-id="8b587-1858">String</span></span> |<span data-ttu-id="8b587-1859">Sim</span><span class="sxs-lookup"><span data-stu-id="8b587-1859">Yes</span></span> |
| <span data-ttu-id="8b587-1860">chave</span><span class="sxs-lookup"><span data-stu-id="8b587-1860">key</span></span> |<span data-ttu-id="8b587-1861">A chave do objeto S3.</span><span class="sxs-lookup"><span data-stu-id="8b587-1861">The S3 object key.</span></span> |<span data-ttu-id="8b587-1862">string</span><span class="sxs-lookup"><span data-stu-id="8b587-1862">String</span></span> |<span data-ttu-id="8b587-1863">Não</span><span class="sxs-lookup"><span data-stu-id="8b587-1863">No</span></span> |
| <span data-ttu-id="8b587-1864">prefixo</span><span class="sxs-lookup"><span data-stu-id="8b587-1864">prefix</span></span> |<span data-ttu-id="8b587-1865">Prefixo da chave do objeto S3.</span><span class="sxs-lookup"><span data-stu-id="8b587-1865">Prefix for the S3 object key.</span></span> <span data-ttu-id="8b587-1866">Objetos cujas chaves começam com esse prefixo serão selecionados.</span><span class="sxs-lookup"><span data-stu-id="8b587-1866">Objects whose keys start with this prefix are selected.</span></span> <span data-ttu-id="8b587-1867">Aplica-se apenas quando a chave está vazia.</span><span class="sxs-lookup"><span data-stu-id="8b587-1867">Applies only when key is empty.</span></span> |<span data-ttu-id="8b587-1868">string</span><span class="sxs-lookup"><span data-stu-id="8b587-1868">String</span></span> |<span data-ttu-id="8b587-1869">Não</span><span class="sxs-lookup"><span data-stu-id="8b587-1869">No</span></span> |
| <span data-ttu-id="8b587-1870">version</span><span class="sxs-lookup"><span data-stu-id="8b587-1870">version</span></span> |<span data-ttu-id="8b587-1871">A versão do objeto S3 se o controle de versão do S3 está habilitado.</span><span class="sxs-lookup"><span data-stu-id="8b587-1871">The version of S3 object if S3 versioning is enabled.</span></span> |<span data-ttu-id="8b587-1872">string</span><span class="sxs-lookup"><span data-stu-id="8b587-1872">String</span></span> |<span data-ttu-id="8b587-1873">Não</span><span class="sxs-lookup"><span data-stu-id="8b587-1873">No</span></span> |
| <span data-ttu-id="8b587-1874">formato</span><span class="sxs-lookup"><span data-stu-id="8b587-1874">format</span></span> | <span data-ttu-id="8b587-1875">Há suporte para os seguintes tipos de formato: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat** e **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="8b587-1875">The following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="8b587-1876">Defina a propriedade **type** sob formato como um desses valores.</span><span class="sxs-lookup"><span data-stu-id="8b587-1876">Set the **type** property under format to one of these values.</span></span> <span data-ttu-id="8b587-1877">Para saber mais, veja as seções [Formato de texto](data-factory-supported-file-and-compression-formats.md#text-format), [Formato Json](data-factory-supported-file-and-compression-formats.md#json-format), [Formato Avro](data-factory-supported-file-and-compression-formats.md#avro-format), [Formato Orc](data-factory-supported-file-and-compression-formats.md#orc-format), e [Formato Parquet](data-factory-supported-file-and-compression-formats.md#parquet-format).</span><span class="sxs-lookup"><span data-stu-id="8b587-1877">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="8b587-1878">Se você quiser **copiar arquivos no estado em que se encontram** entre repositórios baseados em arquivo (cópia binária), ignore a seção de formato nas duas definições de conjunto de dados de entrada e de saída.</span><span class="sxs-lookup"><span data-stu-id="8b587-1878">If you want to **copy files as-is** between file-based stores (binary copy), skip the format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="8b587-1879">Não</span><span class="sxs-lookup"><span data-stu-id="8b587-1879">No</span></span> | |
| <span data-ttu-id="8b587-1880">compactação</span><span class="sxs-lookup"><span data-stu-id="8b587-1880">compression</span></span> | <span data-ttu-id="8b587-1881">Especifique o tipo e o nível de compactação para os dados.</span><span class="sxs-lookup"><span data-stu-id="8b587-1881">Specify the type and level of compression for the data.</span></span> <span data-ttu-id="8b587-1882">Os tipos com suporte são: **GZip**, **Deflate**, **BZip2** e **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="8b587-1882">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="8b587-1883">Os níveis com suporte são **Ideal** e **Mais rápido**.</span><span class="sxs-lookup"><span data-stu-id="8b587-1883">The supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="8b587-1884">Para obter mais informações, consulte [Formatos de arquivo e de compactação no Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="8b587-1884">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="8b587-1885">Não</span><span class="sxs-lookup"><span data-stu-id="8b587-1885">No</span></span> | |


> [!NOTE]
> <span data-ttu-id="8b587-1886">bucketName + chave especifica a localização do objeto S3 em que bucket é o contêiner raiz para objetos S3 e a chave é o caminho completo para o objeto S3.</span><span class="sxs-lookup"><span data-stu-id="8b587-1886">bucketName + key specifies the location of the S3 object where bucket is the root container for S3 objects and key is the full path to S3 object.</span></span>

#### <a name="example-sample-dataset-with-prefix"></a><span data-ttu-id="8b587-1887">Exemplo: Conjunto de dados de exemplo com o prefixo</span><span class="sxs-lookup"><span data-stu-id="8b587-1887">Example: Sample dataset with prefix</span></span>

```json
{
    "name": "dataset-s3",
    "properties": {
        "type": "AmazonS3",
        "linkedServiceName": "link- testS3",
        "typeProperties": {
            "prefix": "testFolder/test",
            "bucketName": "<S3 bucket name>",
            "format": {
                "type": "OrcFormat"
            }
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```
#### <a name="example-sample-data-set-with-version"></a><span data-ttu-id="8b587-1888">Exemplo: Conjunto de dados de exemplo (com a versão)</span><span class="sxs-lookup"><span data-stu-id="8b587-1888">Example: Sample data set (with version)</span></span>

```json
{
    "name": "dataset-s3",
    "properties": {
        "type": "AmazonS3",
        "linkedServiceName": "link- testS3",
        "typeProperties": {
            "key": "testFolder/test.orc",
            "bucketName": "<S3 bucket name>",
            "version": "XXXXXXXXXczm0CJajYkHf0_k6LhBmkcL",
            "format": {
                "type": "OrcFormat"
            }
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```

#### <a name="example-dynamic-paths-for-s3"></a><span data-ttu-id="8b587-1889">Exemplo: Caminhos dinâmicos para S3</span><span class="sxs-lookup"><span data-stu-id="8b587-1889">Example: Dynamic paths for S3</span></span>
<span data-ttu-id="8b587-1890">No exemplo, usamos valores fixos para as propriedades de chave e bucketName no conjunto de dados do Amazon S3.</span><span class="sxs-lookup"><span data-stu-id="8b587-1890">In the sample, we use fixed values for key and bucketName properties in the Amazon S3 dataset.</span></span>

```json
"key": "testFolder/test.orc",
"bucketName": "<S3 bucket name>",
```

<span data-ttu-id="8b587-1891">Você pode fazer com que o Data Factory calcule a chave e bucketName dinamicamente em tempo de execução usando variáveis de sistema como SliceStart.</span><span class="sxs-lookup"><span data-stu-id="8b587-1891">You can have Data Factory calculate the key and bucketName dynamically at runtime by using system variables such as SliceStart.</span></span>

```json
"key": "$$Text.Format('{0:MM}/{0:dd}/test.orc', SliceStart)"
"bucketName": "$$Text.Format('{0:yyyy}', SliceStart)"
```

<span data-ttu-id="8b587-1892">Você pode fazer o mesmo para a propriedade de prefixo de um conjunto de dados do Amazon S3.</span><span class="sxs-lookup"><span data-stu-id="8b587-1892">You can do the same for the prefix property of an Amazon S3 dataset.</span></span> <span data-ttu-id="8b587-1893">Veja [Funções e variáveis do sistema do Data Factory](data-factory-functions-variables.md) para obter uma lista das funções e variáveis com suporte.</span><span class="sxs-lookup"><span data-stu-id="8b587-1893">See [Data Factory functions and system variables](data-factory-functions-variables.md) for a list of supported functions and variables.</span></span>

<span data-ttu-id="8b587-1894">Para obter mais informações, consulte o artigo [Conector do Amazon S3](data-factory-amazon-simple-storage-service-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="8b587-1894">For more information, see [Amazon S3 connector article](data-factory-amazon-simple-storage-service-connector.md#dataset-properties).</span></span>

### <a name="file-system-source-in-copy-activity"></a><span data-ttu-id="8b587-1895">Origem do Sistema de Arquivos na Atividade de Cópia</span><span class="sxs-lookup"><span data-stu-id="8b587-1895">File System Source in Copy Activity</span></span>
<span data-ttu-id="8b587-1896">Se você estiver copiando dados do Amazon S3, defina o **source type** da atividade de cópia para **FileSystemSource** e especifique as propriedades a seguir na seção **source**:</span><span class="sxs-lookup"><span data-stu-id="8b587-1896">If you are copying data from Amazon S3, set the **source type** of the copy activity to **FileSystemSource**, and specify following properties in the **source** section:</span></span>


| <span data-ttu-id="8b587-1897">Propriedade</span><span class="sxs-lookup"><span data-stu-id="8b587-1897">Property</span></span> | <span data-ttu-id="8b587-1898">Descrição</span><span class="sxs-lookup"><span data-stu-id="8b587-1898">Description</span></span> | <span data-ttu-id="8b587-1899">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="8b587-1899">Allowed values</span></span> | <span data-ttu-id="8b587-1900">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="8b587-1900">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="8b587-1901">recursive</span><span class="sxs-lookup"><span data-stu-id="8b587-1901">recursive</span></span> |<span data-ttu-id="8b587-1902">Especifica se devemos listar recursivamente objetos S3 no diretório.</span><span class="sxs-lookup"><span data-stu-id="8b587-1902">Specifies whether to recursively list S3 objects under the directory.</span></span> |<span data-ttu-id="8b587-1903">true/false</span><span class="sxs-lookup"><span data-stu-id="8b587-1903">true/false</span></span> |<span data-ttu-id="8b587-1904">Não</span><span class="sxs-lookup"><span data-stu-id="8b587-1904">No</span></span> |


#### <a name="example"></a><span data-ttu-id="8b587-1905">Exemplo</span><span class="sxs-lookup"><span data-stu-id="8b587-1905">Example</span></span>


```json
{
    "name": "CopyAmazonS3ToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "FileSystemSource",
                    "recursive": true
                },
                "sink": {
                    "type": "BlobSink",
                    "writeBatchSize": 0,
                    "writeBatchTimeout": "00:00:00"
                }
            },
            "inputs": [{
                "name": "AmazonS3InputDataset"
            }],
            "outputs": [{
                "name": "AzureBlobOutputDataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "AmazonS3ToBlob"
        }],
        "start": "2016-08-08T18:00:00",
        "end": "2016-08-08T19:00:00"
    }
}
```

<span data-ttu-id="8b587-1906">Para obter mais informações, consulte o artigo [Conector do Amazon S3](data-factory-amazon-simple-storage-service-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="8b587-1906">For more information, see [Amazon S3 connector article](data-factory-amazon-simple-storage-service-connector.md#copy-activity-properties).</span></span>

## <a name="file-system"></a><span data-ttu-id="8b587-1907">Sistema de Arquivos</span><span class="sxs-lookup"><span data-stu-id="8b587-1907">File System</span></span>


### <a name="linked-service"></a><span data-ttu-id="8b587-1908">Serviço vinculado</span><span class="sxs-lookup"><span data-stu-id="8b587-1908">Linked service</span></span>
<span data-ttu-id="8b587-1909">Você pode vincular um sistema de arquivos local ao Azure Data Factory com o serviço vinculado do **Servidor de Arquivos Local**.</span><span class="sxs-lookup"><span data-stu-id="8b587-1909">You can link an on-premises file system to an Azure data factory with the **On-Premises File Server** linked service.</span></span> <span data-ttu-id="8b587-1910">A tabela a seguir fornece descrições dos elementos JSON específicos para o serviço vinculado do Servidor de Arquivos Local.</span><span class="sxs-lookup"><span data-stu-id="8b587-1910">The following table provides descriptions for JSON elements that are specific to the On-Premises File Server linked service.</span></span>

| <span data-ttu-id="8b587-1911">Propriedade</span><span class="sxs-lookup"><span data-stu-id="8b587-1911">Property</span></span> | <span data-ttu-id="8b587-1912">Descrição</span><span class="sxs-lookup"><span data-stu-id="8b587-1912">Description</span></span> | <span data-ttu-id="8b587-1913">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="8b587-1913">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8b587-1914">type</span><span class="sxs-lookup"><span data-stu-id="8b587-1914">type</span></span> |<span data-ttu-id="8b587-1915">Verifique se a propriedade de tipo foi definida como **OnPremisesFileServer**.</span><span class="sxs-lookup"><span data-stu-id="8b587-1915">Ensure that the type property is set to **OnPremisesFileServer**.</span></span> |<span data-ttu-id="8b587-1916">Sim</span><span class="sxs-lookup"><span data-stu-id="8b587-1916">Yes</span></span> |
| <span data-ttu-id="8b587-1917">host</span><span class="sxs-lookup"><span data-stu-id="8b587-1917">host</span></span> |<span data-ttu-id="8b587-1918">Especifica o caminho raiz da pasta que você deseja copiar.</span><span class="sxs-lookup"><span data-stu-id="8b587-1918">Specifies the root path of the folder that you want to copy.</span></span> <span data-ttu-id="8b587-1919">Use o caractere de escape ‘ \ ’ para caracteres especiais na cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="8b587-1919">Use the escape character ‘ \ ’ for special characters in the string.</span></span> <span data-ttu-id="8b587-1920">Confira [Definições de conjunto de dados e serviço vinculado de exemplo](#sample-linked-service-and-dataset-definitions) para obter exemplos.</span><span class="sxs-lookup"><span data-stu-id="8b587-1920">See [Sample linked service and dataset definitions](#sample-linked-service-and-dataset-definitions) for examples.</span></span> |<span data-ttu-id="8b587-1921">Sim</span><span class="sxs-lookup"><span data-stu-id="8b587-1921">Yes</span></span> |
| <span data-ttu-id="8b587-1922">userid</span><span class="sxs-lookup"><span data-stu-id="8b587-1922">userid</span></span> |<span data-ttu-id="8b587-1923">Especifique a ID do usuário que tem acesso ao servidor.</span><span class="sxs-lookup"><span data-stu-id="8b587-1923">Specify the ID of the user who has access to the server.</span></span> |<span data-ttu-id="8b587-1924">Não (se você escolher encryptedcredential)</span><span class="sxs-lookup"><span data-stu-id="8b587-1924">No (if you choose encryptedCredential)</span></span> |
| <span data-ttu-id="8b587-1925">Senha</span><span class="sxs-lookup"><span data-stu-id="8b587-1925">password</span></span> |<span data-ttu-id="8b587-1926">Especifique a senha para o usuário (userid).</span><span class="sxs-lookup"><span data-stu-id="8b587-1926">Specify the password for the user (userid).</span></span> |<span data-ttu-id="8b587-1927">Não (se você escolher encryptedcredential</span><span class="sxs-lookup"><span data-stu-id="8b587-1927">No (if you choose encryptedCredential</span></span> |
| <span data-ttu-id="8b587-1928">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="8b587-1928">encryptedCredential</span></span> |<span data-ttu-id="8b587-1929">Especifique as credenciais criptografadas que você pode obter executando o cmdlet New-AzureRmDataFactoryEncryptValue.</span><span class="sxs-lookup"><span data-stu-id="8b587-1929">Specify the encrypted credentials that you can get by running the New-AzureRmDataFactoryEncryptValue cmdlet.</span></span> |<span data-ttu-id="8b587-1930">Não (se você optar por especificar userid e password em texto sem formatação)</span><span class="sxs-lookup"><span data-stu-id="8b587-1930">No (if you choose to specify userid and password in plain text)</span></span> |
| <span data-ttu-id="8b587-1931">gatewayName</span><span class="sxs-lookup"><span data-stu-id="8b587-1931">gatewayName</span></span> |<span data-ttu-id="8b587-1932">Especifica o nome do gateway que o Data Factory deve usar para se conectar ao servidor de arquivos local.</span><span class="sxs-lookup"><span data-stu-id="8b587-1932">Specifies the name of the gateway that Data Factory should use to connect to the on-premises file server.</span></span> |<span data-ttu-id="8b587-1933">Sim</span><span class="sxs-lookup"><span data-stu-id="8b587-1933">Yes</span></span> |

#### <a name="sample-folder-path-definitions"></a><span data-ttu-id="8b587-1934">Exemplos de definições de caminho de pasta</span><span class="sxs-lookup"><span data-stu-id="8b587-1934">Sample folder path definitions</span></span> 
| <span data-ttu-id="8b587-1935">Cenário</span><span class="sxs-lookup"><span data-stu-id="8b587-1935">Scenario</span></span> | <span data-ttu-id="8b587-1936">Host em definição de serviço vinculado</span><span class="sxs-lookup"><span data-stu-id="8b587-1936">Host in linked service definition</span></span> | <span data-ttu-id="8b587-1937">folderPath em definição de conjunto de dados</span><span class="sxs-lookup"><span data-stu-id="8b587-1937">folderPath in dataset definition</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8b587-1938">Pasta local no computador do Gateway de Gerenciamento de Dados </span><span class="sxs-lookup"><span data-stu-id="8b587-1938">Local folder on Data Management Gateway machine:</span></span> <br/><br/><span data-ttu-id="8b587-1939">Exemplos: D:\\\* ou D:\pasta\subpasta\\*</span><span class="sxs-lookup"><span data-stu-id="8b587-1939">Examples: D:\\\* or D:\folder\subfolder\\*</span></span> |<span data-ttu-id="8b587-1940">D:\\\\ (para o Gateway de Gerenciamento de Dados 2.0 e versões posteriores)</span><span class="sxs-lookup"><span data-stu-id="8b587-1940">D:\\\\ (for Data Management Gateway 2.0 and later versions)</span></span> <br/><br/> <span data-ttu-id="8b587-1941">localhost (para versões anteriores do Gateway de Gerenciamento de Dados 2.0)</span><span class="sxs-lookup"><span data-stu-id="8b587-1941">localhost (for earlier versions than Data Management Gateway 2.0)</span></span> |<span data-ttu-id="8b587-1942">.\\\\ ou pasta\\\\subpasta (para o Gateway de Gerenciamento de Dados 2.0 e versões posteriores)</span><span class="sxs-lookup"><span data-stu-id="8b587-1942">.\\\\ or folder\\\\subfolder (for Data Management Gateway 2.0 and later versions)</span></span> <br/><br/><span data-ttu-id="8b587-1943">D:\\\\ ou D:\\\\pasta\\\\subpasta (para a versão de gateway abaixo de 2.0)</span><span class="sxs-lookup"><span data-stu-id="8b587-1943">D:\\\\ or D:\\\\folder\\\\subfolder (for gateway version below 2.0)</span></span> |
| <span data-ttu-id="8b587-1944">Pasta compartilhada remota: </span><span class="sxs-lookup"><span data-stu-id="8b587-1944">Remote shared folder:</span></span> <br/><br/><span data-ttu-id="8b587-1945">Exemplos: \\\\meuservidor\\compartilhar\\\* ou \\\\meuservidor\\compartilhar\\pasta\\subpasta\\*</span><span class="sxs-lookup"><span data-stu-id="8b587-1945">Examples: \\\\myserver\\share\\\* or \\\\myserver\\share\\folder\\subfolder\\*</span></span> |<span data-ttu-id="8b587-1946">\\\\\\\\meuservidor\\\\compartilhar</span><span class="sxs-lookup"><span data-stu-id="8b587-1946">\\\\\\\\myserver\\\\share</span></span> |<span data-ttu-id="8b587-1947">.\\\\ ou pasta\\\\subpasta</span><span class="sxs-lookup"><span data-stu-id="8b587-1947">.\\\\ or folder\\\\subfolder</span></span> |


#### <a name="example-using-username-and-password-in-plain-text"></a><span data-ttu-id="8b587-1948">Exemplo: usando username e password em texto sem formatação</span><span class="sxs-lookup"><span data-stu-id="8b587-1948">Example: Using username and password in plain text</span></span>

```json
{
    "Name": "OnPremisesFileServerLinkedService",
    "properties": {
        "type": "OnPremisesFileServer",
        "typeProperties": {
            "host": "\\\\Contosogame-Asia",
            "userid": "Admin",
            "password": "123456",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

#### <a name="example-using-encryptedcredential"></a><span data-ttu-id="8b587-1949">Exemplo: usando encryptedcredential</span><span class="sxs-lookup"><span data-stu-id="8b587-1949">Example: Using encryptedcredential</span></span>

```json
{
    "Name": " OnPremisesFileServerLinkedService ",
    "properties": {
        "type": "OnPremisesFileServer",
        "typeProperties": {
            "host": "D:\\",
            "encryptedCredential": "WFuIGlzIGRpc3Rpbmd1aXNoZWQsIG5vdCBvbmx5IGJ5xxxxxxxxxxxxxxxxx",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

<span data-ttu-id="8b587-1950">Para obter mais informações, consulte o [artigo Conector do Sistema de Arquivos](data-factory-onprem-file-system-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="8b587-1950">For more information, see [File System connector article](data-factory-onprem-file-system-connector.md#linked-service-properties).</span></span>

### <a name="dataset"></a><span data-ttu-id="8b587-1951">Conjunto de dados</span><span class="sxs-lookup"><span data-stu-id="8b587-1951">Dataset</span></span>
<span data-ttu-id="8b587-1952">Para definir um conjunto de dados do Sistema de Arquivos, defina o **type** do conjunto de dados para **FileShare** e especifique as propriedades a seguir na seção **typeProperties**:</span><span class="sxs-lookup"><span data-stu-id="8b587-1952">To define a File System dataset, set the **type** of the dataset to **FileShare**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="8b587-1953">Propriedade</span><span class="sxs-lookup"><span data-stu-id="8b587-1953">Property</span></span> | <span data-ttu-id="8b587-1954">Descrição</span><span class="sxs-lookup"><span data-stu-id="8b587-1954">Description</span></span> | <span data-ttu-id="8b587-1955">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="8b587-1955">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8b587-1956">folderPath</span><span class="sxs-lookup"><span data-stu-id="8b587-1956">folderPath</span></span> |<span data-ttu-id="8b587-1957">Especifica o subcaminho para a pasta.</span><span class="sxs-lookup"><span data-stu-id="8b587-1957">Specifies the subpath to the folder.</span></span> <span data-ttu-id="8b587-1958">Use o caractere de escape ‘\’ para caracteres especiais na cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="8b587-1958">Use the escape character ‘\’ for special characters in the string.</span></span> <span data-ttu-id="8b587-1959">Confira [Definições de conjunto de dados e serviço vinculado de exemplo](#sample-linked-service-and-dataset-definitions) para obter exemplos.</span><span class="sxs-lookup"><span data-stu-id="8b587-1959">See [Sample linked service and dataset definitions](#sample-linked-service-and-dataset-definitions) for examples.</span></span><br/><br/><span data-ttu-id="8b587-1960">Você pode combinar essa propriedade com **partitionBy** para ter caminhos de pastas com base na fatia de data/hora de início/término.</span><span class="sxs-lookup"><span data-stu-id="8b587-1960">You can combine this property with **partitionBy** to have folder paths based on slice start/end date-times.</span></span> |<span data-ttu-id="8b587-1961">Sim</span><span class="sxs-lookup"><span data-stu-id="8b587-1961">Yes</span></span> |
| <span data-ttu-id="8b587-1962">fileName</span><span class="sxs-lookup"><span data-stu-id="8b587-1962">fileName</span></span> |<span data-ttu-id="8b587-1963">Especifique o nome do arquivo no **folderPath** se quiser que a tabela se refira a um arquivo específico na pasta.</span><span class="sxs-lookup"><span data-stu-id="8b587-1963">Specify the name of the file in the **folderPath** if you want the table to refer to a specific file in the folder.</span></span> <span data-ttu-id="8b587-1964">Se você não especificar algum valor para essa propriedade, a tabela apontará para todos os arquivos na pasta.</span><span class="sxs-lookup"><span data-stu-id="8b587-1964">If you do not specify any value for this property, the table points to all files in the folder.</span></span><br/><br/><span data-ttu-id="8b587-1965">Quando o fileName não for especificado para um conjunto de dados de saída, o nome do arquivo gerado será no seguinte formato:</span><span class="sxs-lookup"><span data-stu-id="8b587-1965">When fileName is not specified for an output dataset, the name of the generated file is in the following format:</span></span> <br/><br/><span data-ttu-id="8b587-1966">`Data.<Guid>.txt` (Exemplo: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt)</span><span class="sxs-lookup"><span data-stu-id="8b587-1966">`Data.<Guid>.txt` (Example: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt)</span></span> |<span data-ttu-id="8b587-1967">Não</span><span class="sxs-lookup"><span data-stu-id="8b587-1967">No</span></span> |
| <span data-ttu-id="8b587-1968">fileFilter</span><span class="sxs-lookup"><span data-stu-id="8b587-1968">fileFilter</span></span> |<span data-ttu-id="8b587-1969">Especifique um filtro a ser usado para selecionar um subconjunto de arquivos no folderPath em vez de todos os arquivos.</span><span class="sxs-lookup"><span data-stu-id="8b587-1969">Specify a filter to be used to select a subset of files in the folderPath rather than all files.</span></span> <br/><br/><span data-ttu-id="8b587-1970">Os valores permitidos são: `*` (vários caracteres) e `?` (um único caractere).</span><span class="sxs-lookup"><span data-stu-id="8b587-1970">Allowed values are: `*` (multiple characters) and `?` (single character).</span></span><br/><br/><span data-ttu-id="8b587-1971">Exemplo 1: "fileFilter": "*.log"</span><span class="sxs-lookup"><span data-stu-id="8b587-1971">Example 1: "fileFilter": "*.log"</span></span><br/><span data-ttu-id="8b587-1972">Exemplo 2: "fileFilter": 2016-1-?.txt"</span><span class="sxs-lookup"><span data-stu-id="8b587-1972">Example 2: "fileFilter": 2016-1-?.txt"</span></span><br/><br/><span data-ttu-id="8b587-1973">Observe que fileFilter é aplicável a um conjunto de dados FileShare de entrada.</span><span class="sxs-lookup"><span data-stu-id="8b587-1973">Note that fileFilter is applicable for an input FileShare dataset.</span></span> |<span data-ttu-id="8b587-1974">Não</span><span class="sxs-lookup"><span data-stu-id="8b587-1974">No</span></span> |
| <span data-ttu-id="8b587-1975">partitionedBy</span><span class="sxs-lookup"><span data-stu-id="8b587-1975">partitionedBy</span></span> |<span data-ttu-id="8b587-1976">Você pode usar partitionedBy para especificar um folderPath/fileName dinâmico para dados de série temporal.</span><span class="sxs-lookup"><span data-stu-id="8b587-1976">You can use partitionedBy to specify a dynamic folderPath/fileName for time-series data.</span></span> <span data-ttu-id="8b587-1977">Um exemplo é folderPath parametrizado para cada hora dos dados.</span><span class="sxs-lookup"><span data-stu-id="8b587-1977">An example is folderPath parameterized for every hour of data.</span></span> |<span data-ttu-id="8b587-1978">Não</span><span class="sxs-lookup"><span data-stu-id="8b587-1978">No</span></span> |
| <span data-ttu-id="8b587-1979">formato</span><span class="sxs-lookup"><span data-stu-id="8b587-1979">format</span></span> | <span data-ttu-id="8b587-1980">Há suporte para os seguintes tipos de formato: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat** e **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="8b587-1980">The following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="8b587-1981">Defina a propriedade **type** sob formato como um desses valores.</span><span class="sxs-lookup"><span data-stu-id="8b587-1981">Set the **type** property under format to one of these values.</span></span> <span data-ttu-id="8b587-1982">Para saber mais, veja as seções [Formato de texto](data-factory-supported-file-and-compression-formats.md#text-format), [Formato Json](data-factory-supported-file-and-compression-formats.md#json-format), [Formato Avro](data-factory-supported-file-and-compression-formats.md#avro-format), [Formato Orc](data-factory-supported-file-and-compression-formats.md#orc-format), e [Formato Parquet](data-factory-supported-file-and-compression-formats.md#parquet-format).</span><span class="sxs-lookup"><span data-stu-id="8b587-1982">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="8b587-1983">Se você quiser **copiar arquivos no estado em que se encontram** entre repositórios baseados em arquivo (cópia binária), ignore a seção de formato nas duas definições de conjunto de dados de entrada e de saída.</span><span class="sxs-lookup"><span data-stu-id="8b587-1983">If you want to **copy files as-is** between file-based stores (binary copy), skip the format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="8b587-1984">Não</span><span class="sxs-lookup"><span data-stu-id="8b587-1984">No</span></span> |
| <span data-ttu-id="8b587-1985">compactação</span><span class="sxs-lookup"><span data-stu-id="8b587-1985">compression</span></span> | <span data-ttu-id="8b587-1986">Especifique o tipo e o nível de compactação para os dados.</span><span class="sxs-lookup"><span data-stu-id="8b587-1986">Specify the type and level of compression for the data.</span></span> <span data-ttu-id="8b587-1987">Os tipos compatíveis são: **GZip**, **Deflate**, **BZip2** e **ZipDeflate**; e os níveis permitidos são: **Ideal** e **Mais rápido**.</span><span class="sxs-lookup"><span data-stu-id="8b587-1987">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**; and supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="8b587-1988">confira [Formatos de arquivo e de compactação no Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="8b587-1988">see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="8b587-1989">Não</span><span class="sxs-lookup"><span data-stu-id="8b587-1989">No</span></span> |

> [!NOTE]
> <span data-ttu-id="8b587-1990">Você não pode usar fileName e fileFilter simultaneamente.</span><span class="sxs-lookup"><span data-stu-id="8b587-1990">You cannot use fileName and fileFilter simultaneously.</span></span>

#### <a name="example"></a><span data-ttu-id="8b587-1991">Exemplo</span><span class="sxs-lookup"><span data-stu-id="8b587-1991">Example</span></span>

```json
{
    "name": "OnpremisesFileSystemInput",
    "properties": {
        "type": " FileShare",
        "linkedServiceName": " OnPremisesFileServerLinkedService ",
        "typeProperties": {
            "folderPath": "mysharedfolder/yearno={Year}/monthno={Month}/dayno={Day}",
            "fileName": "{Hour}.csv",
            "partitionedBy": [{
                "name": "Year",
                "value": {
                    "type": "DateTime",
                    "date": "SliceStart",
                        "format": "yyyy"
                }
            }, {
                "name": "Month",
                "value": {
                    "type": "DateTime",
                    "date": "SliceStart",
                    "format": "MM"
                }
            }, {
                "name": "Day",
                "value": {
                    "type": "DateTime",
                    "date": "SliceStart",
                    "format": "dd"
                }
            }, {
                "name": "Hour",
                "value": {
                    "type": "DateTime",
                    "date": "SliceStart",
                    "format": "HH"
                }
            }]
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```

<span data-ttu-id="8b587-1992">Para obter mais informações, consulte o [artigo Conector do Sistema de Arquivos](data-factory-onprem-file-system-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="8b587-1992">For more information, see [File System connector article](data-factory-onprem-file-system-connector.md#dataset-properties).</span></span>

### <a name="file-system-source-in-copy-activity"></a><span data-ttu-id="8b587-1993">Origem do Sistema de Arquivos na Atividade de Cópia</span><span class="sxs-lookup"><span data-stu-id="8b587-1993">File System Source in Copy Activity</span></span>
<span data-ttu-id="8b587-1994">Se você estiver copiando dados do Sistema de Arquivos, defina o **source type** da atividade de cópia para **FileSystemSource** e especifique as propriedades a seguir na seção **source**:</span><span class="sxs-lookup"><span data-stu-id="8b587-1994">If you are copying data from File System, set the **source type** of the copy activity to **FileSystemSource**, and specify following properties in the **source** section:</span></span>

| <span data-ttu-id="8b587-1995">Propriedade</span><span class="sxs-lookup"><span data-stu-id="8b587-1995">Property</span></span> | <span data-ttu-id="8b587-1996">Descrição</span><span class="sxs-lookup"><span data-stu-id="8b587-1996">Description</span></span> | <span data-ttu-id="8b587-1997">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="8b587-1997">Allowed values</span></span> | <span data-ttu-id="8b587-1998">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="8b587-1998">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="8b587-1999">recursiva</span><span class="sxs-lookup"><span data-stu-id="8b587-1999">recursive</span></span> |<span data-ttu-id="8b587-2000">Indica se os dados são lidos recursivamente das subpastas ou somente da pasta especificada.</span><span class="sxs-lookup"><span data-stu-id="8b587-2000">Indicates whether the data is read recursively from the subfolders or only from the specified folder.</span></span> |<span data-ttu-id="8b587-2001">True, False (padrão)</span><span class="sxs-lookup"><span data-stu-id="8b587-2001">True, False (default)</span></span> |<span data-ttu-id="8b587-2002">Não</span><span class="sxs-lookup"><span data-stu-id="8b587-2002">No</span></span> |

#### <a name="example"></a><span data-ttu-id="8b587-2003">Exemplo</span><span class="sxs-lookup"><span data-stu-id="8b587-2003">Example</span></span>

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2015-06-01T18:00:00",
        "end": "2015-06-01T19:00:00",
        "description": "Pipeline for copy activity",
        "activities": [{
            "name": "OnpremisesFileSystemtoBlob",
            "description": "copy activity",
            "type": "Copy",
            "inputs": [{
                "name": "OnpremisesFileSystemInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "FileSystemSource"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "scheduler": {
            "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```
<span data-ttu-id="8b587-2004">Para obter mais informações, consulte o [artigo Conector do Sistema de Arquivos](data-factory-onprem-file-system-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="8b587-2004">For more information, see [File System connector article](data-factory-onprem-file-system-connector.md#copy-activity-properties).</span></span>

### <a name="file-system-sink-in-copy-activity"></a><span data-ttu-id="8b587-2005">Coletor do Sistema de Arquivos na Atividade de Cópia</span><span class="sxs-lookup"><span data-stu-id="8b587-2005">File System Sink in Copy Activity</span></span>
<span data-ttu-id="8b587-2006">Se você estiver copiando dados para um Sistema de Arquivos, defina o **sink type** da atividade de cópia para **FileSystemSink** e especifique as propriedades a seguir na seção **sink**:</span><span class="sxs-lookup"><span data-stu-id="8b587-2006">If you are copying data to File System, set the **sink type** of the copy activity to **FileSystemSink**, and specify following properties in the **sink** section:</span></span>

| <span data-ttu-id="8b587-2007">Propriedade</span><span class="sxs-lookup"><span data-stu-id="8b587-2007">Property</span></span> | <span data-ttu-id="8b587-2008">Descrição</span><span class="sxs-lookup"><span data-stu-id="8b587-2008">Description</span></span> | <span data-ttu-id="8b587-2009">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="8b587-2009">Allowed values</span></span> | <span data-ttu-id="8b587-2010">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="8b587-2010">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="8b587-2011">copyBehavior</span><span class="sxs-lookup"><span data-stu-id="8b587-2011">copyBehavior</span></span> |<span data-ttu-id="8b587-2012">Define o comportamento de cópia quando a origem é BlobSource ou FileSystem.</span><span class="sxs-lookup"><span data-stu-id="8b587-2012">Defines the copy behavior when the source is BlobSource or FileSystem.</span></span> |<span data-ttu-id="8b587-2013">**PreserveHierarchy:** preserva a hierarquia de arquivos na pasta de destino.</span><span class="sxs-lookup"><span data-stu-id="8b587-2013">**PreserveHierarchy:** Preserves the file hierarchy in the target folder.</span></span> <span data-ttu-id="8b587-2014">Ou seja, o caminho relativo do arquivo de origem para a pasta de origem é o mesmo que o caminho relativo do arquivo de destino para a pasta de destino.</span><span class="sxs-lookup"><span data-stu-id="8b587-2014">That is, the relative path of the source file to the source folder is the same as the relative path of the target file to the target folder.</span></span><br/><br/><span data-ttu-id="8b587-2015">**FlattenHierarchy:** todos os arquivos da pasta de origem estarão no primeiro nível da pasta de destino.</span><span class="sxs-lookup"><span data-stu-id="8b587-2015">**FlattenHierarchy:** All files from the source folder are created in the first level of target folder.</span></span> <span data-ttu-id="8b587-2016">Os arquivos de destino são criados com um nome gerado automaticamente.</span><span class="sxs-lookup"><span data-stu-id="8b587-2016">The target files are created with an autogenerated name.</span></span><br/><br/><span data-ttu-id="8b587-2017">**MergeFiles**: mescla todos os arquivos da pasta de origem em um arquivo.</span><span class="sxs-lookup"><span data-stu-id="8b587-2017">**MergeFiles:** Merges all files from the source folder to one file.</span></span> <span data-ttu-id="8b587-2018">Se o nome do arquivo/nome do blob for especificado, o nome do arquivo mesclado será o nome especificado.</span><span class="sxs-lookup"><span data-stu-id="8b587-2018">If the file name/blob name is specified, the merged file name is the specified name.</span></span> <span data-ttu-id="8b587-2019">Caso contrário, ele será um nome de arquivo gerado automaticamente.</span><span class="sxs-lookup"><span data-stu-id="8b587-2019">Otherwise, it is an auto-generated file name.</span></span> |<span data-ttu-id="8b587-2020">Não</span><span class="sxs-lookup"><span data-stu-id="8b587-2020">No</span></span> |
<span data-ttu-id="8b587-2021">auto-</span><span class="sxs-lookup"><span data-stu-id="8b587-2021">auto-</span></span>

#### <a name="example"></a><span data-ttu-id="8b587-2022">Exemplo</span><span class="sxs-lookup"><span data-stu-id="8b587-2022">Example</span></span>

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2015-06-01T18:00:00",
        "end": "2015-06-01T20:00:00",
        "description": "pipeline for copy activity",
        "activities": [{
            "name": "AzureSQLtoOnPremisesFile",
            "description": "copy activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureSQLInput"
            }],
            "outputs": [{
                "name": "OnpremisesFileSystemOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "SqlSource",
                    "SqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd}\\'', WindowStart, WindowEnd)"
                },
                "sink": {
                    "type": "FileSystemSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 3,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

<span data-ttu-id="8b587-2023">Para obter mais informações, consulte o [artigo Conector do Sistema de Arquivos](data-factory-onprem-file-system-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="8b587-2023">For more information, see [File System connector article](data-factory-onprem-file-system-connector.md#copy-activity-properties).</span></span>

## <a name="ftp"></a><span data-ttu-id="8b587-2024">FTP</span><span class="sxs-lookup"><span data-stu-id="8b587-2024">FTP</span></span>

### <a name="linked-service"></a><span data-ttu-id="8b587-2025">Serviço vinculado</span><span class="sxs-lookup"><span data-stu-id="8b587-2025">Linked service</span></span>
<span data-ttu-id="8b587-2026">Para definir um serviço vinculado do FTP, defina o **type** do serviço vinculado para **FtpServer** e especifique as propriedades a seguir na seção **typeProperties**:</span><span class="sxs-lookup"><span data-stu-id="8b587-2026">To define an FTP linked service, set the **type** of the linked service to **FtpServer**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="8b587-2027">Propriedade</span><span class="sxs-lookup"><span data-stu-id="8b587-2027">Property</span></span> | <span data-ttu-id="8b587-2028">Descrição</span><span class="sxs-lookup"><span data-stu-id="8b587-2028">Description</span></span> | <span data-ttu-id="8b587-2029">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="8b587-2029">Required</span></span> | <span data-ttu-id="8b587-2030">Padrão</span><span class="sxs-lookup"><span data-stu-id="8b587-2030">Default</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="8b587-2031">host</span><span class="sxs-lookup"><span data-stu-id="8b587-2031">host</span></span> |<span data-ttu-id="8b587-2032">Nome ou endereço IP do servidor FTP</span><span class="sxs-lookup"><span data-stu-id="8b587-2032">Name or IP address of the FTP Server</span></span> |<span data-ttu-id="8b587-2033">Sim</span><span class="sxs-lookup"><span data-stu-id="8b587-2033">Yes</span></span> |&nbsp; |
| <span data-ttu-id="8b587-2034">authenticationType</span><span class="sxs-lookup"><span data-stu-id="8b587-2034">authenticationType</span></span> |<span data-ttu-id="8b587-2035">Especificar tipo de autenticação</span><span class="sxs-lookup"><span data-stu-id="8b587-2035">Specify authentication type</span></span> |<span data-ttu-id="8b587-2036">Sim</span><span class="sxs-lookup"><span data-stu-id="8b587-2036">Yes</span></span> |<span data-ttu-id="8b587-2037">Básica, Anônima</span><span class="sxs-lookup"><span data-stu-id="8b587-2037">Basic, Anonymous</span></span> |
| <span data-ttu-id="8b587-2038">Nome de Usuário</span><span class="sxs-lookup"><span data-stu-id="8b587-2038">username</span></span> |<span data-ttu-id="8b587-2039">Usuário que tem acesso ao servidor FTP</span><span class="sxs-lookup"><span data-stu-id="8b587-2039">User who has access to the FTP server</span></span> |<span data-ttu-id="8b587-2040">Não</span><span class="sxs-lookup"><span data-stu-id="8b587-2040">No</span></span> |&nbsp; |
| <span data-ttu-id="8b587-2041">Senha</span><span class="sxs-lookup"><span data-stu-id="8b587-2041">password</span></span> |<span data-ttu-id="8b587-2042">Senha do usuário (nome de usuário)</span><span class="sxs-lookup"><span data-stu-id="8b587-2042">Password for the user (username)</span></span> |<span data-ttu-id="8b587-2043">Não</span><span class="sxs-lookup"><span data-stu-id="8b587-2043">No</span></span> |&nbsp; |
| <span data-ttu-id="8b587-2044">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="8b587-2044">encryptedCredential</span></span> |<span data-ttu-id="8b587-2045">Credencial criptografada para acessar o servidor FTP</span><span class="sxs-lookup"><span data-stu-id="8b587-2045">Encrypted credential to access the FTP server</span></span> |<span data-ttu-id="8b587-2046">Não</span><span class="sxs-lookup"><span data-stu-id="8b587-2046">No</span></span> |&nbsp; |
| <span data-ttu-id="8b587-2047">gatewayName</span><span class="sxs-lookup"><span data-stu-id="8b587-2047">gatewayName</span></span> |<span data-ttu-id="8b587-2048">Nome do Gateway de Gerenciamento de Dados para se conectar a um servidor FTP local</span><span class="sxs-lookup"><span data-stu-id="8b587-2048">Name of the Data Management Gateway gateway to connect to an on-premises FTP server</span></span> |<span data-ttu-id="8b587-2049">Não</span><span class="sxs-lookup"><span data-stu-id="8b587-2049">No</span></span> |&nbsp; |
| <span data-ttu-id="8b587-2050">porta</span><span class="sxs-lookup"><span data-stu-id="8b587-2050">port</span></span> |<span data-ttu-id="8b587-2051">Porta na qual o servidor FTP está escutando</span><span class="sxs-lookup"><span data-stu-id="8b587-2051">Port on which the FTP server is listening</span></span> |<span data-ttu-id="8b587-2052">Não</span><span class="sxs-lookup"><span data-stu-id="8b587-2052">No</span></span> |<span data-ttu-id="8b587-2053">21</span><span class="sxs-lookup"><span data-stu-id="8b587-2053">21</span></span> |
| <span data-ttu-id="8b587-2054">enableSsl</span><span class="sxs-lookup"><span data-stu-id="8b587-2054">enableSsl</span></span> |<span data-ttu-id="8b587-2055">Especifique se deseja usar o canal FTP sobre SSL/TLS</span><span class="sxs-lookup"><span data-stu-id="8b587-2055">Specify whether to use FTP over SSL/TLS channel</span></span> |<span data-ttu-id="8b587-2056">Não</span><span class="sxs-lookup"><span data-stu-id="8b587-2056">No</span></span> |<span data-ttu-id="8b587-2057">verdadeiro</span><span class="sxs-lookup"><span data-stu-id="8b587-2057">true</span></span> |
| <span data-ttu-id="8b587-2058">enableServerCertificateValidation</span><span class="sxs-lookup"><span data-stu-id="8b587-2058">enableServerCertificateValidation</span></span> |<span data-ttu-id="8b587-2059">Especifique se deseja habilitar a validação do certificado SSL do servidor ao usar o canal FTP sobre SSL/TLS</span><span class="sxs-lookup"><span data-stu-id="8b587-2059">Specify whether to enable server SSL certificate validation when using FTP over SSL/TLS channel</span></span> |<span data-ttu-id="8b587-2060">Não</span><span class="sxs-lookup"><span data-stu-id="8b587-2060">No</span></span> |<span data-ttu-id="8b587-2061">verdadeiro</span><span class="sxs-lookup"><span data-stu-id="8b587-2061">true</span></span> |

#### <a name="example-using-anonymous-authentication"></a><span data-ttu-id="8b587-2062">Exemplo: Usando a autenticação anônima</span><span class="sxs-lookup"><span data-stu-id="8b587-2062">Example: Using Anonymous authentication</span></span>

```json
{
    "name": "FTPLinkedService",
    "properties": {
        "type": "FtpServer",
            "typeProperties": {
            "authenticationType": "Anonymous",
            "host": "myftpserver.com"
        }
    }
}
```

#### <a name="example-using-username-and-password-in-plain-text-for-basic-authentication"></a><span data-ttu-id="8b587-2063">Exemplo: Usando o nome de usuário e a senha em texto sem formatação para autenticação básica</span><span class="sxs-lookup"><span data-stu-id="8b587-2063">Example: Using username and password in plain text for basic authentication</span></span>

```json
{
    "name": "FTPLinkedService",
    "properties": {
        "type": "FtpServer",
        "typeProperties": {
            "host": "myftpserver.com",
            "authenticationType": "Basic",
            "username": "Admin",
            "password": "123456"
        }
    }
}
```

#### <a name="example-using-port-enablessl-enableservercertificatevalidation"></a><span data-ttu-id="8b587-2064">Exemplo: Usando a porta, enableSsl, enableServerCertificateValidation</span><span class="sxs-lookup"><span data-stu-id="8b587-2064">Example: Using port, enableSsl, enableServerCertificateValidation</span></span>

```json
{
    "name": "FTPLinkedService",
    "properties": {
        "type": "FtpServer",
        "typeProperties": {
            "host": "myftpserver.com",
            "authenticationType": "Basic",    
            "username": "Admin",
            "password": "123456",
            "port": "21",
            "enableSsl": true,
            "enableServerCertificateValidation": true
        }
    }
}
```

#### <a name="example-using-encryptedcredential-for-authentication-and-gateway"></a><span data-ttu-id="8b587-2065">Exemplo: Usando encryptedCredential para autenticação e gateway</span><span class="sxs-lookup"><span data-stu-id="8b587-2065">Example: Using encryptedCredential for authentication and gateway</span></span>

```json
{
    "name": "FTPLinkedService",
    "properties": {
        "type": "FtpServer",
        "typeProperties": {
            "host": "myftpserver.com",
            "authenticationType": "Basic",
            "encryptedCredential": "xxxxxxxxxxxxxxxxx",
            "gatewayName": "<onpremgateway>"
        }
      }
}
```

<span data-ttu-id="8b587-2066">Para obter mais informações, consulte o artigo [Conector do FTP](data-factory-ftp-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="8b587-2066">For more information, see [FTP connector](data-factory-ftp-connector.md#linked-service-properties) article.</span></span>

### <a name="dataset"></a><span data-ttu-id="8b587-2067">Conjunto de dados</span><span class="sxs-lookup"><span data-stu-id="8b587-2067">Dataset</span></span>
<span data-ttu-id="8b587-2068">Para definir um conjunto de dados do FTP, defina o **type** do conjunto de dados para **FileShare** e especifique as propriedades a seguir na seção **typeProperties**:</span><span class="sxs-lookup"><span data-stu-id="8b587-2068">To define an FTP dataset, set the **type** of the dataset to **FileShare**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="8b587-2069">Propriedade</span><span class="sxs-lookup"><span data-stu-id="8b587-2069">Property</span></span> | <span data-ttu-id="8b587-2070">Descrição</span><span class="sxs-lookup"><span data-stu-id="8b587-2070">Description</span></span> | <span data-ttu-id="8b587-2071">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="8b587-2071">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8b587-2072">folderPath</span><span class="sxs-lookup"><span data-stu-id="8b587-2072">folderPath</span></span> |<span data-ttu-id="8b587-2073">Subcaminho para a pasta.</span><span class="sxs-lookup"><span data-stu-id="8b587-2073">Sub path to the folder.</span></span> <span data-ttu-id="8b587-2074">Use o caractere de escape ' \ ' para caracteres especiais na cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="8b587-2074">Use escape character ‘ \ ’ for special characters in the string.</span></span> <span data-ttu-id="8b587-2075">Confira [Definições de conjunto de dados e serviço vinculado de exemplo](#sample-linked-service-and-dataset-definitions) para obter exemplos.</span><span class="sxs-lookup"><span data-stu-id="8b587-2075">See [Sample linked service and dataset definitions](#sample-linked-service-and-dataset-definitions) for examples.</span></span><br/><br/><span data-ttu-id="8b587-2076">Você pode combinar essa propriedade com **partitionBy** para ter caminhos de pastas com base na fatia de data/hora de início/término.</span><span class="sxs-lookup"><span data-stu-id="8b587-2076">You can combine this property with **partitionBy** to have folder paths based on slice start/end date-times.</span></span> |<span data-ttu-id="8b587-2077">Sim</span><span class="sxs-lookup"><span data-stu-id="8b587-2077">Yes</span></span> 
| <span data-ttu-id="8b587-2078">fileName</span><span class="sxs-lookup"><span data-stu-id="8b587-2078">fileName</span></span> |<span data-ttu-id="8b587-2079">Especifique o nome do arquivo no **folderPath** se quiser que a tabela se refira a um arquivo específico na pasta.</span><span class="sxs-lookup"><span data-stu-id="8b587-2079">Specify the name of the file in the **folderPath** if you want the table to refer to a specific file in the folder.</span></span> <span data-ttu-id="8b587-2080">Se você não especificar algum valor para essa propriedade, a tabela apontará para todos os arquivos na pasta.</span><span class="sxs-lookup"><span data-stu-id="8b587-2080">If you do not specify any value for this property, the table points to all files in the folder.</span></span><br/><br/><span data-ttu-id="8b587-2081">Quando o fileName não for especificado para um conjunto de dados de saída, o nome do arquivo gerado será no seguinte formato:</span><span class="sxs-lookup"><span data-stu-id="8b587-2081">When fileName is not specified for an output dataset, the name of the generated file would be in the following this format:</span></span> <br/><br/><span data-ttu-id="8b587-2082">Data.<Guid>.txt (por exemplo: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span><span class="sxs-lookup"><span data-stu-id="8b587-2082">Data.<Guid>.txt (Example: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span></span> |<span data-ttu-id="8b587-2083">Não</span><span class="sxs-lookup"><span data-stu-id="8b587-2083">No</span></span> |
| <span data-ttu-id="8b587-2084">fileFilter</span><span class="sxs-lookup"><span data-stu-id="8b587-2084">fileFilter</span></span> |<span data-ttu-id="8b587-2085">Especifique um filtro a ser usado para selecionar um subconjunto de arquivos no folderPath em vez de todos os arquivos.</span><span class="sxs-lookup"><span data-stu-id="8b587-2085">Specify a filter to be used to select a subset of files in the folderPath rather than all files.</span></span><br/><br/><span data-ttu-id="8b587-2086">Os valores permitidos são: `*` (vários caracteres) e `?` (um único caractere).</span><span class="sxs-lookup"><span data-stu-id="8b587-2086">Allowed values are: `*` (multiple characters) and `?` (single character).</span></span><br/><br/><span data-ttu-id="8b587-2087">Exemplo 1: `"fileFilter": "*.log"`</span><span class="sxs-lookup"><span data-stu-id="8b587-2087">Examples 1: `"fileFilter": "*.log"`</span></span><br/><span data-ttu-id="8b587-2088">Exemplo 2: `"fileFilter": 2016-1-?.txt"`</span><span class="sxs-lookup"><span data-stu-id="8b587-2088">Example 2: `"fileFilter": 2016-1-?.txt"`</span></span><br/><br/> <span data-ttu-id="8b587-2089">fileFilter é aplicável a um conjunto de dados FileShare de entrada.</span><span class="sxs-lookup"><span data-stu-id="8b587-2089">fileFilter is applicable for an input FileShare dataset.</span></span> <span data-ttu-id="8b587-2090">Essa propriedade não tem suporte com HDFS.</span><span class="sxs-lookup"><span data-stu-id="8b587-2090">This property is not supported with HDFS.</span></span> |<span data-ttu-id="8b587-2091">Não</span><span class="sxs-lookup"><span data-stu-id="8b587-2091">No</span></span> |
| <span data-ttu-id="8b587-2092">partitionedBy</span><span class="sxs-lookup"><span data-stu-id="8b587-2092">partitionedBy</span></span> |<span data-ttu-id="8b587-2093">partitionedBy pode usado para especificar um filename, folderPath dinâmico para dados de série temporal.</span><span class="sxs-lookup"><span data-stu-id="8b587-2093">partitionedBy can be used to specify a dynamic folderPath, filename for time series data.</span></span> <span data-ttu-id="8b587-2094">Por exemplo, folderPath parametrizado para cada hora dos dados.</span><span class="sxs-lookup"><span data-stu-id="8b587-2094">For example, folderPath parameterized for every hour of data.</span></span> |<span data-ttu-id="8b587-2095">Não</span><span class="sxs-lookup"><span data-stu-id="8b587-2095">No</span></span> |
| <span data-ttu-id="8b587-2096">formato</span><span class="sxs-lookup"><span data-stu-id="8b587-2096">format</span></span> | <span data-ttu-id="8b587-2097">Há suporte para os seguintes tipos de formato: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat** e **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="8b587-2097">The following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="8b587-2098">Defina a propriedade **type** sob formato como um desses valores.</span><span class="sxs-lookup"><span data-stu-id="8b587-2098">Set the **type** property under format to one of these values.</span></span> <span data-ttu-id="8b587-2099">Para saber mais, veja as seções [Formato de texto](data-factory-supported-file-and-compression-formats.md#text-format), [Formato Json](data-factory-supported-file-and-compression-formats.md#json-format), [Formato Avro](data-factory-supported-file-and-compression-formats.md#avro-format), [Formato Orc](data-factory-supported-file-and-compression-formats.md#orc-format), e [Formato Parquet](data-factory-supported-file-and-compression-formats.md#parquet-format).</span><span class="sxs-lookup"><span data-stu-id="8b587-2099">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="8b587-2100">Se você quiser **copiar arquivos no estado em que se encontram** entre repositórios baseados em arquivo (cópia binária), ignore a seção de formato nas duas definições de conjunto de dados de entrada e de saída.</span><span class="sxs-lookup"><span data-stu-id="8b587-2100">If you want to **copy files as-is** between file-based stores (binary copy), skip the format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="8b587-2101">Não</span><span class="sxs-lookup"><span data-stu-id="8b587-2101">No</span></span> |
| <span data-ttu-id="8b587-2102">compactação</span><span class="sxs-lookup"><span data-stu-id="8b587-2102">compression</span></span> | <span data-ttu-id="8b587-2103">Especifique o tipo e o nível de compactação para os dados.</span><span class="sxs-lookup"><span data-stu-id="8b587-2103">Specify the type and level of compression for the data.</span></span> <span data-ttu-id="8b587-2104">Os tipos compatíveis são: **GZip**, **Deflate**, **BZip2** e **ZipDeflate**; e os níveis permitidos são: **Ideal** e **Mais rápido**.</span><span class="sxs-lookup"><span data-stu-id="8b587-2104">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**; and supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="8b587-2105">Para saber mais, confira [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support) (Formatos de arquivo e de compactação no Azure Data Factory).</span><span class="sxs-lookup"><span data-stu-id="8b587-2105">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="8b587-2106">Não</span><span class="sxs-lookup"><span data-stu-id="8b587-2106">No</span></span> |
| <span data-ttu-id="8b587-2107">useBinaryTransfer</span><span class="sxs-lookup"><span data-stu-id="8b587-2107">useBinaryTransfer</span></span> |<span data-ttu-id="8b587-2108">Especifique se deve usar o modo de transferência Binário.</span><span class="sxs-lookup"><span data-stu-id="8b587-2108">Specify whether use Binary transfer mode.</span></span> <span data-ttu-id="8b587-2109">True para o modo binário e ASCII false.</span><span class="sxs-lookup"><span data-stu-id="8b587-2109">True for binary mode and false ASCII.</span></span> <span data-ttu-id="8b587-2110">Valor padrão: True.</span><span class="sxs-lookup"><span data-stu-id="8b587-2110">Default value: True.</span></span> <span data-ttu-id="8b587-2111">Essa propriedade só pode ser usada quando o tipo de serviço vinculado associado for do tipo: FtpServer.</span><span class="sxs-lookup"><span data-stu-id="8b587-2111">This property can only be used when associated linked service type is of type: FtpServer.</span></span> |<span data-ttu-id="8b587-2112">Não</span><span class="sxs-lookup"><span data-stu-id="8b587-2112">No</span></span> |

> [!NOTE]
> <span data-ttu-id="8b587-2113">filename e fileFilter não podem ser usados simultaneamente.</span><span class="sxs-lookup"><span data-stu-id="8b587-2113">filename and fileFilter cannot be used simultaneously.</span></span>

#### <a name="example"></a><span data-ttu-id="8b587-2114">Exemplo</span><span class="sxs-lookup"><span data-stu-id="8b587-2114">Example</span></span>

```json
{
    "name": "FTPFileInput",
    "properties": {
        "type": "FileShare",
        "linkedServiceName": "FTPLinkedService",
        "typeProperties": {
            "folderPath": "<path to shared folder>",
            "fileName": "test.csv",
            "useBinaryTransfer": true
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

<span data-ttu-id="8b587-2115">Para obter mais informações, consulte o artigo [Conector do FTP](data-factory-ftp-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="8b587-2115">For more information, see [FTP connector](data-factory-ftp-connector.md#dataset-properties) article.</span></span>

### <a name="file-system-source-in-copy-activity"></a><span data-ttu-id="8b587-2116">Origem do Sistema de Arquivos na Atividade de Cópia</span><span class="sxs-lookup"><span data-stu-id="8b587-2116">File System Source in Copy Activity</span></span>
<span data-ttu-id="8b587-2117">Se você estiver copiando dados do FTP, defina o **source type** da atividade de cópia para **FileSystemSource** e especifique as propriedades a seguir na seção **source**:</span><span class="sxs-lookup"><span data-stu-id="8b587-2117">If you are copying data from an FTP server, set the **source type** of the copy activity to **FileSystemSource**, and specify following properties in the **source** section:</span></span>

| <span data-ttu-id="8b587-2118">Propriedade</span><span class="sxs-lookup"><span data-stu-id="8b587-2118">Property</span></span> | <span data-ttu-id="8b587-2119">Descrição</span><span class="sxs-lookup"><span data-stu-id="8b587-2119">Description</span></span> | <span data-ttu-id="8b587-2120">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="8b587-2120">Allowed values</span></span> | <span data-ttu-id="8b587-2121">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="8b587-2121">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="8b587-2122">recursiva</span><span class="sxs-lookup"><span data-stu-id="8b587-2122">recursive</span></span> |<span data-ttu-id="8b587-2123">Indica se os dados são lidos recursivamente a partir das subpastas ou somente da pasta especificada.</span><span class="sxs-lookup"><span data-stu-id="8b587-2123">Indicates whether the data is read recursively from the sub folders or only from the specified folder.</span></span> |<span data-ttu-id="8b587-2124">True, False (padrão)</span><span class="sxs-lookup"><span data-stu-id="8b587-2124">True, False (default)</span></span> |<span data-ttu-id="8b587-2125">Não</span><span class="sxs-lookup"><span data-stu-id="8b587-2125">No</span></span> |

#### <a name="example"></a><span data-ttu-id="8b587-2126">Exemplo</span><span class="sxs-lookup"><span data-stu-id="8b587-2126">Example</span></span>

```json
{
    "name": "pipeline",
    "properties": {
        "activities": [{
            "name": "FTPToBlobCopy",
            "inputs": [{
                "name": "FtpFileInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "FileSystemSource"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "NewestFirst",
                "retry": 1,
                "timeout": "00:05:00"
            }
        }],
        "start": "2016-08-24T18:00:00",
        "end": "2016-08-24T19:00:00"
    }
}
```

<span data-ttu-id="8b587-2127">Para obter mais informações, consulte o artigo [Conector do FTP](data-factory-ftp-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="8b587-2127">For more information, see [FTP connector](data-factory-ftp-connector.md#copy-activity-properties) article.</span></span>


## <a name="hdfs"></a><span data-ttu-id="8b587-2128">HDFS</span><span class="sxs-lookup"><span data-stu-id="8b587-2128">HDFS</span></span>

### <a name="linked-service"></a><span data-ttu-id="8b587-2129">Serviço vinculado</span><span class="sxs-lookup"><span data-stu-id="8b587-2129">Linked service</span></span>
<span data-ttu-id="8b587-2130">Para definir um serviço vinculado do HDFS, defina o **type** do serviço vinculado para **Hdfs** e especifique as propriedades a seguir na seção **typeProperties**:</span><span class="sxs-lookup"><span data-stu-id="8b587-2130">To define a HDFS linked service, set the **type** of the linked service to **Hdfs**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="8b587-2131">Propriedade</span><span class="sxs-lookup"><span data-stu-id="8b587-2131">Property</span></span> | <span data-ttu-id="8b587-2132">Descrição</span><span class="sxs-lookup"><span data-stu-id="8b587-2132">Description</span></span> | <span data-ttu-id="8b587-2133">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="8b587-2133">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8b587-2134">type</span><span class="sxs-lookup"><span data-stu-id="8b587-2134">type</span></span> |<span data-ttu-id="8b587-2135">A propriedade type deve ser definida como: **Hdfs**</span><span class="sxs-lookup"><span data-stu-id="8b587-2135">The type property must be set to: **Hdfs**</span></span> |<span data-ttu-id="8b587-2136">Sim</span><span class="sxs-lookup"><span data-stu-id="8b587-2136">Yes</span></span> |
| <span data-ttu-id="8b587-2137">Url</span><span class="sxs-lookup"><span data-stu-id="8b587-2137">Url</span></span> |<span data-ttu-id="8b587-2138">URL para o HDFS</span><span class="sxs-lookup"><span data-stu-id="8b587-2138">URL to the HDFS</span></span> |<span data-ttu-id="8b587-2139">Sim</span><span class="sxs-lookup"><span data-stu-id="8b587-2139">Yes</span></span> |
| <span data-ttu-id="8b587-2140">authenticationType</span><span class="sxs-lookup"><span data-stu-id="8b587-2140">authenticationType</span></span> |<span data-ttu-id="8b587-2141">Anônimo ou Windows.</span><span class="sxs-lookup"><span data-stu-id="8b587-2141">Anonymous, or Windows.</span></span> <br><br> <span data-ttu-id="8b587-2142">Para usar **autenticação Kerberos** com o conector HDFS, veja [esta seção](#use-kerberos-authentication-for-hdfs-connector) para configurar seu ambiente local adequadamente.</span><span class="sxs-lookup"><span data-stu-id="8b587-2142">To use **Kerberos authentication** for HDFS connector, refer to [this section](#use-kerberos-authentication-for-hdfs-connector) to set up your on-premises environment accordingly.</span></span> |<span data-ttu-id="8b587-2143">Sim</span><span class="sxs-lookup"><span data-stu-id="8b587-2143">Yes</span></span> |
| <span data-ttu-id="8b587-2144">userName</span><span class="sxs-lookup"><span data-stu-id="8b587-2144">userName</span></span> |<span data-ttu-id="8b587-2145">Nome de usuário para a autenticação do Windows.</span><span class="sxs-lookup"><span data-stu-id="8b587-2145">Username for Windows authentication.</span></span> |<span data-ttu-id="8b587-2146">Sim (para a Autenticação do Windows)</span><span class="sxs-lookup"><span data-stu-id="8b587-2146">Yes (for Windows Authentication)</span></span> |
| <span data-ttu-id="8b587-2147">Senha</span><span class="sxs-lookup"><span data-stu-id="8b587-2147">password</span></span> |<span data-ttu-id="8b587-2148">Senha para a autenticação do Windows.</span><span class="sxs-lookup"><span data-stu-id="8b587-2148">Password for Windows authentication.</span></span> |<span data-ttu-id="8b587-2149">Sim (para a Autenticação do Windows)</span><span class="sxs-lookup"><span data-stu-id="8b587-2149">Yes (for Windows Authentication)</span></span> |
| <span data-ttu-id="8b587-2150">gatewayName</span><span class="sxs-lookup"><span data-stu-id="8b587-2150">gatewayName</span></span> |<span data-ttu-id="8b587-2151">O nome do gateway que o serviço Data Factory deve usar para se conectar ao HDFS.</span><span class="sxs-lookup"><span data-stu-id="8b587-2151">Name of the gateway that the Data Factory service should use to connect to the HDFS.</span></span> |<span data-ttu-id="8b587-2152">Sim</span><span class="sxs-lookup"><span data-stu-id="8b587-2152">Yes</span></span> |
| <span data-ttu-id="8b587-2153">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="8b587-2153">encryptedCredential</span></span> |<span data-ttu-id="8b587-2154">[New-AzureRMDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) da credencial de acesso.</span><span class="sxs-lookup"><span data-stu-id="8b587-2154">[New-AzureRMDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) output of the access credential.</span></span> |<span data-ttu-id="8b587-2155">Não</span><span class="sxs-lookup"><span data-stu-id="8b587-2155">No</span></span> |

#### <a name="example-using-anonymous-authentication"></a><span data-ttu-id="8b587-2156">Exemplo: Usando a autenticação anônima</span><span class="sxs-lookup"><span data-stu-id="8b587-2156">Example: Using Anonymous authentication</span></span>

```json
{
    "name": "HDFSLinkedService",
    "properties": {
        "type": "Hdfs",
        "typeProperties": {
            "authenticationType": "Anonymous",
            "userName": "hadoop",
            "url": "http://<machine>:50070/webhdfs/v1/",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

#### <a name="example-using-windows-authentication"></a><span data-ttu-id="8b587-2157">Exemplo: Usando a autenticação do Windows</span><span class="sxs-lookup"><span data-stu-id="8b587-2157">Example: Using Windows authentication</span></span>

```json
{
    "name": "HDFSLinkedService",
    "properties": {
        "type": "Hdfs",
        "typeProperties": {
            "authenticationType": "Windows",
            "userName": "Administrator",
            "password": "password",
            "url": "http://<machine>:50070/webhdfs/v1/",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

<span data-ttu-id="8b587-2158">Para obter mais informações, consulte o artigo [Conector do HDFS](#data-factory-hdfs-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="8b587-2158">For more information, see [HDFS connector](#data-factory-hdfs-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="8b587-2159">Conjunto de dados</span><span class="sxs-lookup"><span data-stu-id="8b587-2159">Dataset</span></span>
<span data-ttu-id="8b587-2160">Para definir um conjunto de dados do HDFS, defina o **type** do conjunto de dados para **FileShare** e especifique as propriedades a seguir na seção **typeProperties**:</span><span class="sxs-lookup"><span data-stu-id="8b587-2160">To define a HDFS dataset, set the **type** of the dataset to **FileShare**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="8b587-2161">Propriedade</span><span class="sxs-lookup"><span data-stu-id="8b587-2161">Property</span></span> | <span data-ttu-id="8b587-2162">Descrição</span><span class="sxs-lookup"><span data-stu-id="8b587-2162">Description</span></span> | <span data-ttu-id="8b587-2163">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="8b587-2163">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8b587-2164">folderPath</span><span class="sxs-lookup"><span data-stu-id="8b587-2164">folderPath</span></span> |<span data-ttu-id="8b587-2165">Caminho para a pasta.</span><span class="sxs-lookup"><span data-stu-id="8b587-2165">Path to the folder.</span></span> <span data-ttu-id="8b587-2166">Exemplo: `myfolder`</span><span class="sxs-lookup"><span data-stu-id="8b587-2166">Example: `myfolder`</span></span><br/><br/><span data-ttu-id="8b587-2167">Use o caractere de escape ' \ ' para caracteres especiais na cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="8b587-2167">Use escape character ‘ \ ’ for special characters in the string.</span></span> <span data-ttu-id="8b587-2168">Por exemplo: para pasta\subpasta, especifique a pasta\\\\subpasta e para d:\pastadeexemplo, especifique d:\\\\pastadeexemplo.</span><span class="sxs-lookup"><span data-stu-id="8b587-2168">For example: for folder\subfolder, specify folder\\\\subfolder and for d:\samplefolder, specify d:\\\\samplefolder.</span></span><br/><br/><span data-ttu-id="8b587-2169">Você pode combinar essa propriedade com **partitionBy** para ter caminhos de pastas com base na fatia de data/hora de início/término.</span><span class="sxs-lookup"><span data-stu-id="8b587-2169">You can combine this property with **partitionBy** to have folder paths based on slice start/end date-times.</span></span> |<span data-ttu-id="8b587-2170">Sim</span><span class="sxs-lookup"><span data-stu-id="8b587-2170">Yes</span></span> |
| <span data-ttu-id="8b587-2171">fileName</span><span class="sxs-lookup"><span data-stu-id="8b587-2171">fileName</span></span> |<span data-ttu-id="8b587-2172">Especifique o nome do arquivo no **folderPath** se quiser que a tabela se refira a um arquivo específico na pasta.</span><span class="sxs-lookup"><span data-stu-id="8b587-2172">Specify the name of the file in the **folderPath** if you want the table to refer to a specific file in the folder.</span></span> <span data-ttu-id="8b587-2173">Se você não especificar algum valor para essa propriedade, a tabela apontará para todos os arquivos na pasta.</span><span class="sxs-lookup"><span data-stu-id="8b587-2173">If you do not specify any value for this property, the table points to all files in the folder.</span></span><br/><br/><span data-ttu-id="8b587-2174">Quando o fileName não for especificado para um conjunto de dados de saída, o nome do arquivo gerado será no seguinte formato:</span><span class="sxs-lookup"><span data-stu-id="8b587-2174">When fileName is not specified for an output dataset, the name of the generated file would be in the following this format:</span></span> <br/><br/><span data-ttu-id="8b587-2175">Data<Guid>.txt (por exemplo: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span><span class="sxs-lookup"><span data-stu-id="8b587-2175">Data.<Guid>.txt (for example: : Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span></span> |<span data-ttu-id="8b587-2176">Não</span><span class="sxs-lookup"><span data-stu-id="8b587-2176">No</span></span> |
| <span data-ttu-id="8b587-2177">partitionedBy</span><span class="sxs-lookup"><span data-stu-id="8b587-2177">partitionedBy</span></span> |<span data-ttu-id="8b587-2178">partitionedBy pode usado para especificar um filename, folderPath dinâmico para dados de série temporal.</span><span class="sxs-lookup"><span data-stu-id="8b587-2178">partitionedBy can be used to specify a dynamic folderPath, filename for time series data.</span></span> <span data-ttu-id="8b587-2179">Exemplo: folderPath parametrizado para cada hora dos dados.</span><span class="sxs-lookup"><span data-stu-id="8b587-2179">Example: folderPath parameterized for every hour of data.</span></span> |<span data-ttu-id="8b587-2180">Não</span><span class="sxs-lookup"><span data-stu-id="8b587-2180">No</span></span> |
| <span data-ttu-id="8b587-2181">formato</span><span class="sxs-lookup"><span data-stu-id="8b587-2181">format</span></span> | <span data-ttu-id="8b587-2182">Há suporte para os seguintes tipos de formato: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat** e **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="8b587-2182">The following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="8b587-2183">Defina a propriedade **type** sob formato como um desses valores.</span><span class="sxs-lookup"><span data-stu-id="8b587-2183">Set the **type** property under format to one of these values.</span></span> <span data-ttu-id="8b587-2184">Para saber mais, veja as seções [Formato de texto](data-factory-supported-file-and-compression-formats.md#text-format), [Formato Json](data-factory-supported-file-and-compression-formats.md#json-format), [Formato Avro](data-factory-supported-file-and-compression-formats.md#avro-format), [Formato Orc](data-factory-supported-file-and-compression-formats.md#orc-format), e [Formato Parquet](data-factory-supported-file-and-compression-formats.md#parquet-format).</span><span class="sxs-lookup"><span data-stu-id="8b587-2184">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="8b587-2185">Se você quiser **copiar arquivos no estado em que se encontram** entre repositórios baseados em arquivo (cópia binária), ignore a seção de formato nas duas definições de conjunto de dados de entrada e de saída.</span><span class="sxs-lookup"><span data-stu-id="8b587-2185">If you want to **copy files as-is** between file-based stores (binary copy), skip the format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="8b587-2186">Não</span><span class="sxs-lookup"><span data-stu-id="8b587-2186">No</span></span> |
| <span data-ttu-id="8b587-2187">compactação</span><span class="sxs-lookup"><span data-stu-id="8b587-2187">compression</span></span> | <span data-ttu-id="8b587-2188">Especifique o tipo e o nível de compactação para os dados.</span><span class="sxs-lookup"><span data-stu-id="8b587-2188">Specify the type and level of compression for the data.</span></span> <span data-ttu-id="8b587-2189">Os tipos com suporte são: **GZip**, **Deflate**, **BZip2** e **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="8b587-2189">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="8b587-2190">Os níveis com suporte são **Ideal** e **O mais rápido**.</span><span class="sxs-lookup"><span data-stu-id="8b587-2190">Supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="8b587-2191">Para saber mais, confira [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support) (Formatos de arquivo e de compactação no Azure Data Factory).</span><span class="sxs-lookup"><span data-stu-id="8b587-2191">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="8b587-2192">Não</span><span class="sxs-lookup"><span data-stu-id="8b587-2192">No</span></span> |

> [!NOTE]
> <span data-ttu-id="8b587-2193">filename e fileFilter não podem ser usados simultaneamente.</span><span class="sxs-lookup"><span data-stu-id="8b587-2193">filename and fileFilter cannot be used simultaneously.</span></span>

#### <a name="example"></a><span data-ttu-id="8b587-2194">Exemplo</span><span class="sxs-lookup"><span data-stu-id="8b587-2194">Example</span></span>

```json
{
    "name": "InputDataset",
    "properties": {
        "type": "FileShare",
        "linkedServiceName": "HDFSLinkedService",
        "typeProperties": {
            "folderPath": "DataTransfer/UnitTest/"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

<span data-ttu-id="8b587-2195">Para obter mais informações, consulte o artigo [Conector do HDFS](#data-factory-hdfs-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="8b587-2195">For more information, see [HDFS connector](#data-factory-hdfs-connector.md#dataset-properties) article.</span></span> 

### <a name="file-system-source-in-copy-activity"></a><span data-ttu-id="8b587-2196">Origem do Sistema de Arquivos na Atividade de Cópia</span><span class="sxs-lookup"><span data-stu-id="8b587-2196">File System Source in Copy Activity</span></span>
<span data-ttu-id="8b587-2197">Se você estiver copiando dados do HDFS, defina o **source type** da atividade de cópia para **FileSystemSource** e especifique as propriedades a seguir na seção **source**:</span><span class="sxs-lookup"><span data-stu-id="8b587-2197">If you are copying data from HDFS, set the **source type** of the copy activity to **FileSystemSource**, and specify following properties in the **source** section:</span></span>

<span data-ttu-id="8b587-2198">**FileSystemSource** suporta as seguintes propriedades:</span><span class="sxs-lookup"><span data-stu-id="8b587-2198">**FileSystemSource** supports the following properties:</span></span>

| <span data-ttu-id="8b587-2199">Propriedade</span><span class="sxs-lookup"><span data-stu-id="8b587-2199">Property</span></span> | <span data-ttu-id="8b587-2200">Descrição</span><span class="sxs-lookup"><span data-stu-id="8b587-2200">Description</span></span> | <span data-ttu-id="8b587-2201">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="8b587-2201">Allowed values</span></span> | <span data-ttu-id="8b587-2202">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="8b587-2202">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="8b587-2203">recursiva</span><span class="sxs-lookup"><span data-stu-id="8b587-2203">recursive</span></span> |<span data-ttu-id="8b587-2204">Indica se os dados são lidos recursivamente a partir das subpastas ou somente da pasta especificada.</span><span class="sxs-lookup"><span data-stu-id="8b587-2204">Indicates whether the data is read recursively from the sub folders or only from the specified folder.</span></span> |<span data-ttu-id="8b587-2205">True, False (padrão)</span><span class="sxs-lookup"><span data-stu-id="8b587-2205">True, False (default)</span></span> |<span data-ttu-id="8b587-2206">Não</span><span class="sxs-lookup"><span data-stu-id="8b587-2206">No</span></span> |

#### <a name="example"></a><span data-ttu-id="8b587-2207">Exemplo</span><span class="sxs-lookup"><span data-stu-id="8b587-2207">Example</span></span>

```json
{
    "name": "pipeline",
    "properties": {
        "activities": [{
            "name": "HdfsToBlobCopy",
            "inputs": [{
                "name": "InputDataset"
            }],
            "outputs": [{
                "name": "OutputDataset"
            }],
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "FileSystemSource"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "NewestFirst",
                "retry": 1,
                "timeout": "00:05:00"
            }
        }],
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00"
    }
}
```

<span data-ttu-id="8b587-2208">Para obter mais informações, consulte o artigo [Conector do HDFS](#data-factory-hdfs-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="8b587-2208">For more information, see [HDFS connector](#data-factory-hdfs-connector.md#copy-activity-properties) article.</span></span>

## <a name="sftp"></a><span data-ttu-id="8b587-2209">SFTP</span><span class="sxs-lookup"><span data-stu-id="8b587-2209">SFTP</span></span>


### <a name="linked-service"></a><span data-ttu-id="8b587-2210">Serviço vinculado</span><span class="sxs-lookup"><span data-stu-id="8b587-2210">Linked service</span></span>
<span data-ttu-id="8b587-2211">Para definir um serviço vinculado do SFTP, defina o **type** do serviço vinculado para **Sftp** e especifique as propriedades a seguir na seção **typeProperties**:</span><span class="sxs-lookup"><span data-stu-id="8b587-2211">To define an SFTP linked service, set the **type** of the linked service to **Sftp**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="8b587-2212">Propriedade</span><span class="sxs-lookup"><span data-stu-id="8b587-2212">Property</span></span> | <span data-ttu-id="8b587-2213">Descrição</span><span class="sxs-lookup"><span data-stu-id="8b587-2213">Description</span></span> | <span data-ttu-id="8b587-2214">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="8b587-2214">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="8b587-2215">host</span><span class="sxs-lookup"><span data-stu-id="8b587-2215">host</span></span> | <span data-ttu-id="8b587-2216">Nome ou endereço IP do servidor SFTP.</span><span class="sxs-lookup"><span data-stu-id="8b587-2216">Name or IP address of the SFTP server.</span></span> |<span data-ttu-id="8b587-2217">Sim</span><span class="sxs-lookup"><span data-stu-id="8b587-2217">Yes</span></span> |
| <span data-ttu-id="8b587-2218">porta</span><span class="sxs-lookup"><span data-stu-id="8b587-2218">port</span></span> |<span data-ttu-id="8b587-2219">Porta na qual o servidor SFTP está escutando.</span><span class="sxs-lookup"><span data-stu-id="8b587-2219">Port on which the SFTP server is listening.</span></span> <span data-ttu-id="8b587-2220">O valor padrão é: 21</span><span class="sxs-lookup"><span data-stu-id="8b587-2220">The default value is: 21</span></span> |<span data-ttu-id="8b587-2221">Não</span><span class="sxs-lookup"><span data-stu-id="8b587-2221">No</span></span> |
| <span data-ttu-id="8b587-2222">authenticationType</span><span class="sxs-lookup"><span data-stu-id="8b587-2222">authenticationType</span></span> |<span data-ttu-id="8b587-2223">Especifique o tipo de autenticação.</span><span class="sxs-lookup"><span data-stu-id="8b587-2223">Specify authentication type.</span></span> <span data-ttu-id="8b587-2224">Valores permitidos: **Básica**, **SshPublicKey**.</span><span class="sxs-lookup"><span data-stu-id="8b587-2224">Allowed values: **Basic**, **SshPublicKey**.</span></span> <br><br> <span data-ttu-id="8b587-2225">Consulte as seções [Usando a autenticação Básica](#using-basic-authentication) e [Usando autenticação de chave pública SSH](#using-ssh-public-key-authentication) para ver mais propriedades e amostras do JSON, respectivamente.</span><span class="sxs-lookup"><span data-stu-id="8b587-2225">Refer to [Using basic authentication](#using-basic-authentication) and [Using SSH public key authentication](#using-ssh-public-key-authentication) sections on more properties and JSON samples respectively.</span></span> |<span data-ttu-id="8b587-2226">Sim</span><span class="sxs-lookup"><span data-stu-id="8b587-2226">Yes</span></span> |
| <span data-ttu-id="8b587-2227">skipHostKeyValidation</span><span class="sxs-lookup"><span data-stu-id="8b587-2227">skipHostKeyValidation</span></span> | <span data-ttu-id="8b587-2228">Especifique se deseja ignorar a validação da chave de host.</span><span class="sxs-lookup"><span data-stu-id="8b587-2228">Specify whether to skip host key validation.</span></span> | <span data-ttu-id="8b587-2229">Não.</span><span class="sxs-lookup"><span data-stu-id="8b587-2229">No.</span></span> <span data-ttu-id="8b587-2230">O valor padrão: false</span><span class="sxs-lookup"><span data-stu-id="8b587-2230">The default value: false</span></span> |
| <span data-ttu-id="8b587-2231">hostKeyFingerprint</span><span class="sxs-lookup"><span data-stu-id="8b587-2231">hostKeyFingerprint</span></span> | <span data-ttu-id="8b587-2232">Especifique a impressão digital da chave de host.</span><span class="sxs-lookup"><span data-stu-id="8b587-2232">Specify the finger print of the host key.</span></span> | <span data-ttu-id="8b587-2233">Sim se o `skipHostKeyValidation` estiver definido como false.</span><span class="sxs-lookup"><span data-stu-id="8b587-2233">Yes if the `skipHostKeyValidation` is set to false.</span></span>  |
| <span data-ttu-id="8b587-2234">gatewayName</span><span class="sxs-lookup"><span data-stu-id="8b587-2234">gatewayName</span></span> |<span data-ttu-id="8b587-2235">Nome do Gateway de Gerenciamento de Dados para se conectar a um servidor SFTP local.</span><span class="sxs-lookup"><span data-stu-id="8b587-2235">Name of the Data Management Gateway to connect to an on-premises SFTP server.</span></span> | <span data-ttu-id="8b587-2236">Sim se estiver copiando dados de um servidor SFTP local.</span><span class="sxs-lookup"><span data-stu-id="8b587-2236">Yes if copying data from an on-premises SFTP server.</span></span> |
| <span data-ttu-id="8b587-2237">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="8b587-2237">encryptedCredential</span></span> | <span data-ttu-id="8b587-2238">Credencial criptografada para acessar o servidor SFTP.</span><span class="sxs-lookup"><span data-stu-id="8b587-2238">Encrypted credential to access the SFTP server.</span></span> <span data-ttu-id="8b587-2239">Gerado automaticamente quando você especifica a autenticação Básica (nome de usuário + senha) ou autenticação SshPublicKey (nome de usuário + conteúdo ou caminho da chave privada) no assistente de cópia ou na caixa de diálogo de pop-up do ClickOnce.</span><span class="sxs-lookup"><span data-stu-id="8b587-2239">Auto-generated when you specify basic authentication (username + password) or SshPublicKey authentication (username + private key path or content) in copy wizard or the ClickOnce popup dialog.</span></span> | <span data-ttu-id="8b587-2240">Não.</span><span class="sxs-lookup"><span data-stu-id="8b587-2240">No.</span></span> <span data-ttu-id="8b587-2241">Aplique somente quando estiver copiando dados de um servidor SFTP local.</span><span class="sxs-lookup"><span data-stu-id="8b587-2241">Apply only when copying data from an on-premises SFTP server.</span></span> |

#### <a name="example-using-basic-authentication"></a><span data-ttu-id="8b587-2242">Exemplo: Usando a autenticação básica</span><span class="sxs-lookup"><span data-stu-id="8b587-2242">Example: Using basic authentication</span></span>

<span data-ttu-id="8b587-2243">Para usar a autenticação Básica, defina `authenticationType` como `Basic` e especifique as propriedades a seguir, além das genéricas do conector SFTP apresentadas na última seção:</span><span class="sxs-lookup"><span data-stu-id="8b587-2243">To use basic authentication, set `authenticationType` as `Basic`, and specify the following properties besides the SFTP connector generic ones introduced in the last section:</span></span>

| <span data-ttu-id="8b587-2244">Propriedade</span><span class="sxs-lookup"><span data-stu-id="8b587-2244">Property</span></span> | <span data-ttu-id="8b587-2245">Descrição</span><span class="sxs-lookup"><span data-stu-id="8b587-2245">Description</span></span> | <span data-ttu-id="8b587-2246">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="8b587-2246">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="8b587-2247">Nome de Usuário</span><span class="sxs-lookup"><span data-stu-id="8b587-2247">username</span></span> | <span data-ttu-id="8b587-2248">Usuário que tem acesso ao servidor SFTP.</span><span class="sxs-lookup"><span data-stu-id="8b587-2248">User who has access to the SFTP server.</span></span> |<span data-ttu-id="8b587-2249">Sim</span><span class="sxs-lookup"><span data-stu-id="8b587-2249">Yes</span></span> |
| <span data-ttu-id="8b587-2250">Senha</span><span class="sxs-lookup"><span data-stu-id="8b587-2250">password</span></span> | <span data-ttu-id="8b587-2251">Senha do usuário (nome de usuário).</span><span class="sxs-lookup"><span data-stu-id="8b587-2251">Password for the user (username).</span></span> | <span data-ttu-id="8b587-2252">Sim</span><span class="sxs-lookup"><span data-stu-id="8b587-2252">Yes</span></span> |

```json
{
    "name": "SftpLinkedService",
    "properties": {
        "type": "Sftp",
        "typeProperties": {
            "host": "<SFTP server name or IP address>",
            "port": 22,
            "authenticationType": "Basic",
            "username": "xxx",
            "password": "xxx",
            "skipHostKeyValidation": false,
            "hostKeyFingerPrint": "ssh-rsa 2048 xx:00:00:00:xx:00:x0:0x:0x:0x:0x:00:00:x0:x0:00",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

#### <a name="example-basic-authentication-with-encrypted-credential"></a><span data-ttu-id="8b587-2253">Exemplo: Autenticação básica com credencial criptografada**</span><span class="sxs-lookup"><span data-stu-id="8b587-2253">Example: Basic authentication with encrypted credential**</span></span>

```json
{
    "name": "SftpLinkedService",
    "properties": {
        "type": "Sftp",
        "typeProperties": {
            "host": "<FTP server name or IP address>",
            "port": 22,
            "authenticationType": "Basic",
            "username": "xxx",
            "encryptedCredential": "xxxxxxxxxxxxxxxxx",
            "skipHostKeyValidation": false,
            "hostKeyFingerPrint": "ssh-rsa 2048 xx:00:00:00:xx:00:x0:0x:0x:0x:0x:00:00:x0:x0:00",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

#### <a name="using-ssh-public-key-authentication"></a><span data-ttu-id="8b587-2254">Usando a autenticação de chave pública SSH:**</span><span class="sxs-lookup"><span data-stu-id="8b587-2254">Using SSH public key authentication:**</span></span>

<span data-ttu-id="8b587-2255">Para usar a autenticação Básica, defina `authenticationType` como `SshPublicKey` e especifique as propriedades a seguir, além das genéricas do conector SFTP apresentadas na última seção:</span><span class="sxs-lookup"><span data-stu-id="8b587-2255">To use basic authentication, set `authenticationType` as `SshPublicKey`, and specify the following properties besides the SFTP connector generic ones introduced in the last section:</span></span>

| <span data-ttu-id="8b587-2256">Propriedade</span><span class="sxs-lookup"><span data-stu-id="8b587-2256">Property</span></span> | <span data-ttu-id="8b587-2257">Descrição</span><span class="sxs-lookup"><span data-stu-id="8b587-2257">Description</span></span> | <span data-ttu-id="8b587-2258">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="8b587-2258">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="8b587-2259">Nome de Usuário</span><span class="sxs-lookup"><span data-stu-id="8b587-2259">username</span></span> |<span data-ttu-id="8b587-2260">Usuário que tem acesso ao servidor SFTP</span><span class="sxs-lookup"><span data-stu-id="8b587-2260">User who has access to the SFTP server</span></span> |<span data-ttu-id="8b587-2261">Sim</span><span class="sxs-lookup"><span data-stu-id="8b587-2261">Yes</span></span> |
| <span data-ttu-id="8b587-2262">privateKeyPath</span><span class="sxs-lookup"><span data-stu-id="8b587-2262">privateKeyPath</span></span> | <span data-ttu-id="8b587-2263">Especifique, para o arquivo de chave privada, um caminho absoluto que esse gateway possa acessar.</span><span class="sxs-lookup"><span data-stu-id="8b587-2263">Specify absolute path to the private key file that gateway can access.</span></span> | <span data-ttu-id="8b587-2264">Especifique `privateKeyPath` ou `privateKeyContent`.</span><span class="sxs-lookup"><span data-stu-id="8b587-2264">Specify either the `privateKeyPath` or `privateKeyContent`.</span></span> <br><br> <span data-ttu-id="8b587-2265">Aplique somente quando estiver copiando dados de um servidor SFTP local.</span><span class="sxs-lookup"><span data-stu-id="8b587-2265">Apply only when copying data from an on-premises SFTP server.</span></span> |
| <span data-ttu-id="8b587-2266">privateKeyContent</span><span class="sxs-lookup"><span data-stu-id="8b587-2266">privateKeyContent</span></span> | <span data-ttu-id="8b587-2267">Uma cadeia de caracteres serializada do conteúdo da chave privada.</span><span class="sxs-lookup"><span data-stu-id="8b587-2267">A serialized string of the private key content.</span></span> <span data-ttu-id="8b587-2268">O Assistente de Cópia pode ler o arquivo de chave privada e extrair o conteúdo da chave privada automaticamente.</span><span class="sxs-lookup"><span data-stu-id="8b587-2268">The Copy Wizard can read the private key file and extract the private key content automatically.</span></span> <span data-ttu-id="8b587-2269">Se você estiver usando qualquer outra ferramenta/SDK, use a propriedade privateKeyPath em seu lugar.</span><span class="sxs-lookup"><span data-stu-id="8b587-2269">If you are using any other tool/SDK, use the privateKeyPath property instead.</span></span> | <span data-ttu-id="8b587-2270">Especifique `privateKeyPath` ou `privateKeyContent`.</span><span class="sxs-lookup"><span data-stu-id="8b587-2270">Specify either the `privateKeyPath` or `privateKeyContent`.</span></span> |
| <span data-ttu-id="8b587-2271">Senha</span><span class="sxs-lookup"><span data-stu-id="8b587-2271">passPhrase</span></span> | <span data-ttu-id="8b587-2272">Especifique a senha/frase secreta para descriptografar a chave particular se o arquivo de chave for protegido por uma frase secreta.</span><span class="sxs-lookup"><span data-stu-id="8b587-2272">Specify the pass phrase/password to decrypt the private key if the key file is protected by a pass phrase.</span></span> | <span data-ttu-id="8b587-2273">Sim, se o arquivo de chave privada for protegido por uma frase secreta.</span><span class="sxs-lookup"><span data-stu-id="8b587-2273">Yes if the private key file is protected by a pass phrase.</span></span> |

```json
{
    "name": "SftpLinkedServiceWithPrivateKeyPath",
    "properties": {
        "type": "Sftp",
        "typeProperties": {
            "host": "<FTP server name or IP address>",
            "port": 22,
            "authenticationType": "SshPublicKey",
            "username": "xxx",
            "privateKeyPath": "D:\\privatekey_openssh",
            "passPhrase": "xxx",
            "skipHostKeyValidation": true,
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

#### <a name="example-sshpublickey-authentication-using-private-key-content"></a><span data-ttu-id="8b587-2274">Exemplo: autenticação de SshPublicKey usando o conteúdo da chave privada**</span><span class="sxs-lookup"><span data-stu-id="8b587-2274">Example: SshPublicKey authentication using private key content**</span></span>

```json
{
    "name": "SftpLinkedServiceWithPrivateKeyContent",
    "properties": {
        "type": "Sftp",
        "typeProperties": {
            "host": "mysftpserver.westus.cloudapp.azure.com",
            "port": 22,
            "authenticationType": "SshPublicKey",
            "username": "xxx",
            "privateKeyContent": "<base64 string of the private key content>",
            "passPhrase": "xxx",
            "skipHostKeyValidation": true
        }
    }
}
```

<span data-ttu-id="8b587-2275">Para obter mais informações, consulte o artigo [Conector do SFTP](data-factory-sftp-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="8b587-2275">For more information, see [SFTP connector](data-factory-sftp-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="8b587-2276">Conjunto de dados</span><span class="sxs-lookup"><span data-stu-id="8b587-2276">Dataset</span></span>
<span data-ttu-id="8b587-2277">Para definir um conjunto de dados do SFTP, defina o **type** do conjunto de dados para **FileShare** e especifique as propriedades a seguir na seção **typeProperties**:</span><span class="sxs-lookup"><span data-stu-id="8b587-2277">To define an SFTP dataset, set the **type** of the dataset to **FileShare**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="8b587-2278">Propriedade</span><span class="sxs-lookup"><span data-stu-id="8b587-2278">Property</span></span> | <span data-ttu-id="8b587-2279">Descrição</span><span class="sxs-lookup"><span data-stu-id="8b587-2279">Description</span></span> | <span data-ttu-id="8b587-2280">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="8b587-2280">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8b587-2281">folderPath</span><span class="sxs-lookup"><span data-stu-id="8b587-2281">folderPath</span></span> |<span data-ttu-id="8b587-2282">Subcaminho para a pasta.</span><span class="sxs-lookup"><span data-stu-id="8b587-2282">Sub path to the folder.</span></span> <span data-ttu-id="8b587-2283">Use o caractere de escape ' \ ' para caracteres especiais na cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="8b587-2283">Use escape character ‘ \ ’ for special characters in the string.</span></span> <span data-ttu-id="8b587-2284">Confira [Definições de conjunto de dados e serviço vinculado de exemplo](#sample-linked-service-and-dataset-definitions) para obter exemplos.</span><span class="sxs-lookup"><span data-stu-id="8b587-2284">See [Sample linked service and dataset definitions](#sample-linked-service-and-dataset-definitions) for examples.</span></span><br/><br/><span data-ttu-id="8b587-2285">Você pode combinar essa propriedade com **partitionBy** para ter caminhos de pastas com base na fatia de data/hora de início/término.</span><span class="sxs-lookup"><span data-stu-id="8b587-2285">You can combine this property with **partitionBy** to have folder paths based on slice start/end date-times.</span></span> |<span data-ttu-id="8b587-2286">Sim</span><span class="sxs-lookup"><span data-stu-id="8b587-2286">Yes</span></span> |
| <span data-ttu-id="8b587-2287">fileName</span><span class="sxs-lookup"><span data-stu-id="8b587-2287">fileName</span></span> |<span data-ttu-id="8b587-2288">Especifique o nome do arquivo no **folderPath** se quiser que a tabela se refira a um arquivo específico na pasta.</span><span class="sxs-lookup"><span data-stu-id="8b587-2288">Specify the name of the file in the **folderPath** if you want the table to refer to a specific file in the folder.</span></span> <span data-ttu-id="8b587-2289">Se você não especificar algum valor para essa propriedade, a tabela apontará para todos os arquivos na pasta.</span><span class="sxs-lookup"><span data-stu-id="8b587-2289">If you do not specify any value for this property, the table points to all files in the folder.</span></span><br/><br/><span data-ttu-id="8b587-2290">Quando o fileName não for especificado para um conjunto de dados de saída, o nome do arquivo gerado será no seguinte formato:</span><span class="sxs-lookup"><span data-stu-id="8b587-2290">When fileName is not specified for an output dataset, the name of the generated file would be in the following this format:</span></span> <br/><br/><span data-ttu-id="8b587-2291">Data.<Guid>.txt (por exemplo: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span><span class="sxs-lookup"><span data-stu-id="8b587-2291">Data.<Guid>.txt (Example: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span></span> |<span data-ttu-id="8b587-2292">Não</span><span class="sxs-lookup"><span data-stu-id="8b587-2292">No</span></span> |
| <span data-ttu-id="8b587-2293">fileFilter</span><span class="sxs-lookup"><span data-stu-id="8b587-2293">fileFilter</span></span> |<span data-ttu-id="8b587-2294">Especifique um filtro a ser usado para selecionar um subconjunto de arquivos no folderPath em vez de todos os arquivos.</span><span class="sxs-lookup"><span data-stu-id="8b587-2294">Specify a filter to be used to select a subset of files in the folderPath rather than all files.</span></span><br/><br/><span data-ttu-id="8b587-2295">Os valores permitidos são: `*` (vários caracteres) e `?` (um único caractere).</span><span class="sxs-lookup"><span data-stu-id="8b587-2295">Allowed values are: `*` (multiple characters) and `?` (single character).</span></span><br/><br/><span data-ttu-id="8b587-2296">Exemplo 1: `"fileFilter": "*.log"`</span><span class="sxs-lookup"><span data-stu-id="8b587-2296">Examples 1: `"fileFilter": "*.log"`</span></span><br/><span data-ttu-id="8b587-2297">Exemplo 2: `"fileFilter": 2016-1-?.txt"`</span><span class="sxs-lookup"><span data-stu-id="8b587-2297">Example 2: `"fileFilter": 2016-1-?.txt"`</span></span><br/><br/> <span data-ttu-id="8b587-2298">fileFilter é aplicável a um conjunto de dados FileShare de entrada.</span><span class="sxs-lookup"><span data-stu-id="8b587-2298">fileFilter is applicable for an input FileShare dataset.</span></span> <span data-ttu-id="8b587-2299">Essa propriedade não tem suporte com HDFS.</span><span class="sxs-lookup"><span data-stu-id="8b587-2299">This property is not supported with HDFS.</span></span> |<span data-ttu-id="8b587-2300">Não</span><span class="sxs-lookup"><span data-stu-id="8b587-2300">No</span></span> |
| <span data-ttu-id="8b587-2301">partitionedBy</span><span class="sxs-lookup"><span data-stu-id="8b587-2301">partitionedBy</span></span> |<span data-ttu-id="8b587-2302">partitionedBy pode usado para especificar um filename, folderPath dinâmico para dados de série temporal.</span><span class="sxs-lookup"><span data-stu-id="8b587-2302">partitionedBy can be used to specify a dynamic folderPath, filename for time series data.</span></span> <span data-ttu-id="8b587-2303">Por exemplo, folderPath parametrizado para cada hora dos dados.</span><span class="sxs-lookup"><span data-stu-id="8b587-2303">For example, folderPath parameterized for every hour of data.</span></span> |<span data-ttu-id="8b587-2304">Não</span><span class="sxs-lookup"><span data-stu-id="8b587-2304">No</span></span> |
| <span data-ttu-id="8b587-2305">formato</span><span class="sxs-lookup"><span data-stu-id="8b587-2305">format</span></span> | <span data-ttu-id="8b587-2306">Há suporte para os seguintes tipos de formato: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat** e **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="8b587-2306">The following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="8b587-2307">Defina a propriedade **type** sob formato como um desses valores.</span><span class="sxs-lookup"><span data-stu-id="8b587-2307">Set the **type** property under format to one of these values.</span></span> <span data-ttu-id="8b587-2308">Para saber mais, veja as seções [Formato de texto](data-factory-supported-file-and-compression-formats.md#text-format), [Formato Json](data-factory-supported-file-and-compression-formats.md#json-format), [Formato Avro](data-factory-supported-file-and-compression-formats.md#avro-format), [Formato Orc](data-factory-supported-file-and-compression-formats.md#orc-format), e [Formato Parquet](data-factory-supported-file-and-compression-formats.md#parquet-format).</span><span class="sxs-lookup"><span data-stu-id="8b587-2308">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="8b587-2309">Se você quiser **copiar arquivos no estado em que se encontram** entre repositórios baseados em arquivo (cópia binária), ignore a seção de formato nas duas definições de conjunto de dados de entrada e de saída.</span><span class="sxs-lookup"><span data-stu-id="8b587-2309">If you want to **copy files as-is** between file-based stores (binary copy), skip the format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="8b587-2310">Não</span><span class="sxs-lookup"><span data-stu-id="8b587-2310">No</span></span> |
| <span data-ttu-id="8b587-2311">compactação</span><span class="sxs-lookup"><span data-stu-id="8b587-2311">compression</span></span> | <span data-ttu-id="8b587-2312">Especifique o tipo e o nível de compactação para os dados.</span><span class="sxs-lookup"><span data-stu-id="8b587-2312">Specify the type and level of compression for the data.</span></span> <span data-ttu-id="8b587-2313">Os tipos com suporte são: **GZip**, **Deflate**, **BZip2** e **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="8b587-2313">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="8b587-2314">Os níveis com suporte são **Ideal** e **O mais rápido**.</span><span class="sxs-lookup"><span data-stu-id="8b587-2314">Supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="8b587-2315">Para saber mais, confira [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support) (Formatos de arquivo e de compactação no Azure Data Factory).</span><span class="sxs-lookup"><span data-stu-id="8b587-2315">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="8b587-2316">Não</span><span class="sxs-lookup"><span data-stu-id="8b587-2316">No</span></span> |
| <span data-ttu-id="8b587-2317">useBinaryTransfer</span><span class="sxs-lookup"><span data-stu-id="8b587-2317">useBinaryTransfer</span></span> |<span data-ttu-id="8b587-2318">Especifique se deve usar o modo de transferência Binário.</span><span class="sxs-lookup"><span data-stu-id="8b587-2318">Specify whether use Binary transfer mode.</span></span> <span data-ttu-id="8b587-2319">True para o modo binário e ASCII false.</span><span class="sxs-lookup"><span data-stu-id="8b587-2319">True for binary mode and false ASCII.</span></span> <span data-ttu-id="8b587-2320">Valor padrão: True.</span><span class="sxs-lookup"><span data-stu-id="8b587-2320">Default value: True.</span></span> <span data-ttu-id="8b587-2321">Essa propriedade só pode ser usada quando o tipo de serviço vinculado associado for do tipo: FtpServer.</span><span class="sxs-lookup"><span data-stu-id="8b587-2321">This property can only be used when associated linked service type is of type: FtpServer.</span></span> |<span data-ttu-id="8b587-2322">Não</span><span class="sxs-lookup"><span data-stu-id="8b587-2322">No</span></span> |

> [!NOTE]
> <span data-ttu-id="8b587-2323">filename e fileFilter não podem ser usados simultaneamente.</span><span class="sxs-lookup"><span data-stu-id="8b587-2323">filename and fileFilter cannot be used simultaneously.</span></span>

#### <a name="example"></a><span data-ttu-id="8b587-2324">Exemplo</span><span class="sxs-lookup"><span data-stu-id="8b587-2324">Example</span></span>

```json
{
    "name": "SFTPFileInput",
    "properties": {
        "type": "FileShare",
        "linkedServiceName": "SftpLinkedService",
        "typeProperties": {
            "folderPath": "<path to shared folder>",
            "fileName": "test.csv"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

<span data-ttu-id="8b587-2325">Para obter mais informações, consulte o artigo [Conector do SFTP](data-factory-sftp-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="8b587-2325">For more information, see [SFTP connector](data-factory-sftp-connector.md#dataset-properties) article.</span></span> 

### <a name="file-system-source-in-copy-activity"></a><span data-ttu-id="8b587-2326">Origem do Sistema de Arquivos na Atividade de Cópia</span><span class="sxs-lookup"><span data-stu-id="8b587-2326">File System Source in Copy Activity</span></span>
<span data-ttu-id="8b587-2327">Se você estiver copiando dados de uma origem do SFTP, defina o **source type** da atividade de cópia para **FileSystemSource** e especifique as propriedades a seguir na seção **source**:</span><span class="sxs-lookup"><span data-stu-id="8b587-2327">If you are copying data from an SFTP source, set the **source type** of the copy activity to **FileSystemSource**, and specify following properties in the **source** section:</span></span>

| <span data-ttu-id="8b587-2328">Propriedade</span><span class="sxs-lookup"><span data-stu-id="8b587-2328">Property</span></span> | <span data-ttu-id="8b587-2329">Descrição</span><span class="sxs-lookup"><span data-stu-id="8b587-2329">Description</span></span> | <span data-ttu-id="8b587-2330">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="8b587-2330">Allowed values</span></span> | <span data-ttu-id="8b587-2331">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="8b587-2331">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="8b587-2332">recursiva</span><span class="sxs-lookup"><span data-stu-id="8b587-2332">recursive</span></span> |<span data-ttu-id="8b587-2333">Indica se os dados são lidos recursivamente a partir das subpastas ou somente da pasta especificada.</span><span class="sxs-lookup"><span data-stu-id="8b587-2333">Indicates whether the data is read recursively from the sub folders or only from the specified folder.</span></span> |<span data-ttu-id="8b587-2334">True, False (padrão)</span><span class="sxs-lookup"><span data-stu-id="8b587-2334">True, False (default)</span></span> |<span data-ttu-id="8b587-2335">Não</span><span class="sxs-lookup"><span data-stu-id="8b587-2335">No</span></span> |



#### <a name="example"></a><span data-ttu-id="8b587-2336">Exemplo</span><span class="sxs-lookup"><span data-stu-id="8b587-2336">Example</span></span>

```json
{
    "name": "pipeline",
    "properties": {
        "activities": [{
            "name": "SFTPToBlobCopy",
            "inputs": [{
                "name": "SFTPFileInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "FileSystemSource"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "NewestFirst",
                "retry": 1,
                "timeout": "00:05:00"
            }
        }],
        "start": "2017-02-20T18:00:00",
        "end": "2017-02-20T19:00:00"
    }
}
```

<span data-ttu-id="8b587-2337">Para obter mais informações, consulte o artigo [Conector do SFTP](data-factory-sftp-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="8b587-2337">For more information, see [SFTP connector](data-factory-sftp-connector.md#copy-activity-properties) article.</span></span>


## <a name="http"></a><span data-ttu-id="8b587-2338">HTTP</span><span class="sxs-lookup"><span data-stu-id="8b587-2338">HTTP</span></span>

### <a name="linked-service"></a><span data-ttu-id="8b587-2339">Serviço vinculado</span><span class="sxs-lookup"><span data-stu-id="8b587-2339">Linked service</span></span>
<span data-ttu-id="8b587-2340">Para definir um serviço vinculado do HTTP, defina o **type** do serviço vinculado para **Http** e especifique as propriedades a seguir na seção **typeProperties**:</span><span class="sxs-lookup"><span data-stu-id="8b587-2340">To define a HTTP linked service, set the **type** of the linked service to **Http**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="8b587-2341">Propriedade</span><span class="sxs-lookup"><span data-stu-id="8b587-2341">Property</span></span> | <span data-ttu-id="8b587-2342">Descrição</span><span class="sxs-lookup"><span data-stu-id="8b587-2342">Description</span></span> | <span data-ttu-id="8b587-2343">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="8b587-2343">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8b587-2344">url</span><span class="sxs-lookup"><span data-stu-id="8b587-2344">url</span></span> | <span data-ttu-id="8b587-2345">URL base para o Servidor Web</span><span class="sxs-lookup"><span data-stu-id="8b587-2345">Base URL to the Web Server</span></span> | <span data-ttu-id="8b587-2346">Sim</span><span class="sxs-lookup"><span data-stu-id="8b587-2346">Yes</span></span> |
| <span data-ttu-id="8b587-2347">authenticationType</span><span class="sxs-lookup"><span data-stu-id="8b587-2347">authenticationType</span></span> | <span data-ttu-id="8b587-2348">Especifica o tipo de autenticação.</span><span class="sxs-lookup"><span data-stu-id="8b587-2348">Specifies the authentication type.</span></span> <span data-ttu-id="8b587-2349">Os valores permitidos são: **Anônimo**, **Básico**, **Digest**, **Windows** e **ClientCertificate**.</span><span class="sxs-lookup"><span data-stu-id="8b587-2349">Allowed values are: **Anonymous**, **Basic**, **Digest**, **Windows**, **ClientCertificate**.</span></span> <br><br> <span data-ttu-id="8b587-2350">Consulte as seções abaixo desta tabela para mais propriedades e amostras JSON para esses tipos de autenticação, respectivamente.</span><span class="sxs-lookup"><span data-stu-id="8b587-2350">Refer to sections below this table on more properties and JSON samples for those authentication types respectively.</span></span> | <span data-ttu-id="8b587-2351">Sim</span><span class="sxs-lookup"><span data-stu-id="8b587-2351">Yes</span></span> |
| <span data-ttu-id="8b587-2352">enableServerCertificateValidation</span><span class="sxs-lookup"><span data-stu-id="8b587-2352">enableServerCertificateValidation</span></span> | <span data-ttu-id="8b587-2353">Especifique se deseja habilitar a validação do certificado SSL do servidor se a origem for um servidor Web HTTPS</span><span class="sxs-lookup"><span data-stu-id="8b587-2353">Specify whether to enable server SSL certificate validation if source is HTTPS Web Server</span></span> | <span data-ttu-id="8b587-2354">Não, o padrão é true</span><span class="sxs-lookup"><span data-stu-id="8b587-2354">No, default is true</span></span> |
| <span data-ttu-id="8b587-2355">gatewayName</span><span class="sxs-lookup"><span data-stu-id="8b587-2355">gatewayName</span></span> | <span data-ttu-id="8b587-2356">Nome do Gateway de Gerenciamento de Dados para se conectar a uma origem HTTP local.</span><span class="sxs-lookup"><span data-stu-id="8b587-2356">Name of the Data Management Gateway to connect to an on-premises HTTP source.</span></span> | <span data-ttu-id="8b587-2357">Sim se estiver copiando dados de uma origem HTTP local.</span><span class="sxs-lookup"><span data-stu-id="8b587-2357">Yes if copying data from an on-premises HTTP source.</span></span> |
| <span data-ttu-id="8b587-2358">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="8b587-2358">encryptedCredential</span></span> | <span data-ttu-id="8b587-2359">Credencial criptografada para acessar o ponto de extremidade HTTP.</span><span class="sxs-lookup"><span data-stu-id="8b587-2359">Encrypted credential to access the HTTP endpoint.</span></span> <span data-ttu-id="8b587-2360">Gerado automaticamente quando você configura as informações de autenticação no assistente de cópia ou a caixa de diálogo pop-up do ClickOnce.</span><span class="sxs-lookup"><span data-stu-id="8b587-2360">Auto-generated when you configure the authentication information in copy wizard or the ClickOnce popup dialog.</span></span> | <span data-ttu-id="8b587-2361">Não.</span><span class="sxs-lookup"><span data-stu-id="8b587-2361">No.</span></span> <span data-ttu-id="8b587-2362">Aplique somente quando estiver copiando dados de um servidor HTTP local.</span><span class="sxs-lookup"><span data-stu-id="8b587-2362">Apply only when copying data from an on-premises HTTP server.</span></span> |

#### <a name="example-using-basic-digest-or-windows-authentication"></a><span data-ttu-id="8b587-2363">Exemplo: Usando a autenticação Básica, Digest ou Windows</span><span class="sxs-lookup"><span data-stu-id="8b587-2363">Example: Using Basic, Digest, or Windows authentication</span></span>
<span data-ttu-id="8b587-2364">Defina `authenticationType` como `Basic`, `Digest` ou `Windows` e especifique as propriedades a seguir, além das genéricas do conector HTTP apresentadas acima:</span><span class="sxs-lookup"><span data-stu-id="8b587-2364">Set `authenticationType` as `Basic`, `Digest`, or `Windows`, and specify the following properties besides the HTTP connector generic ones introduced above:</span></span>

| <span data-ttu-id="8b587-2365">Propriedade</span><span class="sxs-lookup"><span data-stu-id="8b587-2365">Property</span></span> | <span data-ttu-id="8b587-2366">Descrição</span><span class="sxs-lookup"><span data-stu-id="8b587-2366">Description</span></span> | <span data-ttu-id="8b587-2367">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="8b587-2367">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8b587-2368">Nome de Usuário</span><span class="sxs-lookup"><span data-stu-id="8b587-2368">username</span></span> | <span data-ttu-id="8b587-2369">Nome de usuário para acessar o ponto de extremidade HTTP.</span><span class="sxs-lookup"><span data-stu-id="8b587-2369">Username to access the HTTP endpoint.</span></span> | <span data-ttu-id="8b587-2370">Sim</span><span class="sxs-lookup"><span data-stu-id="8b587-2370">Yes</span></span> |
| <span data-ttu-id="8b587-2371">Senha</span><span class="sxs-lookup"><span data-stu-id="8b587-2371">password</span></span> | <span data-ttu-id="8b587-2372">Senha do usuário (nome de usuário).</span><span class="sxs-lookup"><span data-stu-id="8b587-2372">Password for the user (username).</span></span> | <span data-ttu-id="8b587-2373">Sim</span><span class="sxs-lookup"><span data-stu-id="8b587-2373">Yes</span></span> |

```json
{
    "name": "HttpLinkedService",
    "properties": {
        "type": "Http",
        "typeProperties": {
            "authenticationType": "basic",
            "url": "https://en.wikipedia.org/wiki/",
            "userName": "user name",
            "password": "password"
        }
    }
}
```

#### <a name="example-using-clientcertificate-authentication"></a><span data-ttu-id="8b587-2374">Exemplo: Usando a autenticação ClientCertificate</span><span class="sxs-lookup"><span data-stu-id="8b587-2374">Example: Using ClientCertificate authentication</span></span>

<span data-ttu-id="8b587-2375">Para usar a autenticação Básica, defina `authenticationType` como `ClientCertificate` e especifique as propriedades a seguir, além das genéricas do conector HTTP apresentadas acima:</span><span class="sxs-lookup"><span data-stu-id="8b587-2375">To use basic authentication, set `authenticationType` as `ClientCertificate`, and specify the following properties besides the HTTP connector generic ones introduced above:</span></span>

| <span data-ttu-id="8b587-2376">Propriedade</span><span class="sxs-lookup"><span data-stu-id="8b587-2376">Property</span></span> | <span data-ttu-id="8b587-2377">Descrição</span><span class="sxs-lookup"><span data-stu-id="8b587-2377">Description</span></span> | <span data-ttu-id="8b587-2378">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="8b587-2378">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8b587-2379">embeddedCertData</span><span class="sxs-lookup"><span data-stu-id="8b587-2379">embeddedCertData</span></span> | <span data-ttu-id="8b587-2380">O conteúdo codificado na Base64 de dados binários do arquivo Personal Information Exchange (PFX).</span><span class="sxs-lookup"><span data-stu-id="8b587-2380">The Base64-encoded contents of binary data of the Personal Information Exchange (PFX) file.</span></span> | <span data-ttu-id="8b587-2381">Especifique `embeddedCertData` ou `certThumbprint`.</span><span class="sxs-lookup"><span data-stu-id="8b587-2381">Specify either the `embeddedCertData` or `certThumbprint`.</span></span> |
| <span data-ttu-id="8b587-2382">certThumbprint</span><span class="sxs-lookup"><span data-stu-id="8b587-2382">certThumbprint</span></span> | <span data-ttu-id="8b587-2383">A impressão digital do certificado que foi instalado no repositório de certificados do computador do gateway.</span><span class="sxs-lookup"><span data-stu-id="8b587-2383">The thumbprint of the certificate that was installed on your gateway machine’s cert store.</span></span> <span data-ttu-id="8b587-2384">Aplique somente ao copiar dados de uma origem HTTP local.</span><span class="sxs-lookup"><span data-stu-id="8b587-2384">Apply only when copying data from an on-premises HTTP source.</span></span> | <span data-ttu-id="8b587-2385">Especifique `embeddedCertData` ou `certThumbprint`.</span><span class="sxs-lookup"><span data-stu-id="8b587-2385">Specify either the `embeddedCertData` or `certThumbprint`.</span></span> |
| <span data-ttu-id="8b587-2386">Senha</span><span class="sxs-lookup"><span data-stu-id="8b587-2386">password</span></span> | <span data-ttu-id="8b587-2387">Senha associada ao certificado.</span><span class="sxs-lookup"><span data-stu-id="8b587-2387">Password associated with the certificate.</span></span> | <span data-ttu-id="8b587-2388">Não</span><span class="sxs-lookup"><span data-stu-id="8b587-2388">No</span></span> |

<span data-ttu-id="8b587-2389">Se você usar `certThumbprint` para autenticação e o certificado estiver instalado no armazenamento pessoal do computador local, você precisará conceder a permissão de leitura para o serviço de gateway:</span><span class="sxs-lookup"><span data-stu-id="8b587-2389">If you use `certThumbprint` for authentication and the certificate is installed in the personal store of the local computer, you need to grant the read permission to the gateway service:</span></span>

1. <span data-ttu-id="8b587-2390">Iniciar o MMC (Console de Gerenciamento Microsoft).</span><span class="sxs-lookup"><span data-stu-id="8b587-2390">Launch Microsoft Management Console (MMC).</span></span> <span data-ttu-id="8b587-2391">Adicionar o snap-in **Certificados**, que tem como destino o **Computador Local**.</span><span class="sxs-lookup"><span data-stu-id="8b587-2391">Add the **Certificates** snap-in that targets the **Local Computer**.</span></span>
2. <span data-ttu-id="8b587-2392">Expanda **Certificados**, **Pessoal** e clique em **Certificados**.</span><span class="sxs-lookup"><span data-stu-id="8b587-2392">Expand **Certificates**, **Personal**, and click **Certificates**.</span></span>
3. <span data-ttu-id="8b587-2393">Clique com o botão direito do mouse no certificado do repositório pessoal e selecione **Todas as Tarefas**->**Gerenciar Chaves Particulares...**</span><span class="sxs-lookup"><span data-stu-id="8b587-2393">Right-click the certificate from the personal store, and select **All Tasks**->**Manage Private Keys...**</span></span>
3. <span data-ttu-id="8b587-2394">Na guia **Segurança**, adicione a conta de usuário sob a qual o serviço de Host de Gateway de Gerenciamento de Dados está em execução com o acesso de leitura para o certificado.</span><span class="sxs-lookup"><span data-stu-id="8b587-2394">On the **Security** tab, add the user account under which Data Management Gateway Host Service is running with the read access to the certificate.</span></span>  

<span data-ttu-id="8b587-2395">**Exemplo: usando o certificado do cliente:** Esse serviço vinculado vincula seu data factory a um servidor Web HTTP local.</span><span class="sxs-lookup"><span data-stu-id="8b587-2395">**Example: using client certificate:** This linked service links your data factory to an on-premises HTTP web server.</span></span> <span data-ttu-id="8b587-2396">Ele usa um certificado do cliente instalado no computador com o Gateway de Gerenciamento de Dados instalado.</span><span class="sxs-lookup"><span data-stu-id="8b587-2396">It uses a client certificate that is installed on the machine with Data Management Gateway installed.</span></span>

```json
{
    "name": "HttpLinkedService",
    "properties": {
        "type": "Http",
        "typeProperties": {
            "authenticationType": "ClientCertificate",
            "url": "https://en.wikipedia.org/wiki/",
            "certThumbprint": "thumbprint of certificate",
            "gatewayName": "gateway name"
        }
    }
}
```

#### <a name="example-using-client-certificate-in-a-file"></a><span data-ttu-id="8b587-2397">Exemplo: usando o certificado do cliente em um arquivo</span><span class="sxs-lookup"><span data-stu-id="8b587-2397">Example: using client certificate in a file</span></span>
<span data-ttu-id="8b587-2398">Esse serviço vinculado vincula seu data factory a um servidor Web HTTP local.</span><span class="sxs-lookup"><span data-stu-id="8b587-2398">This linked service links your data factory to an on-premises HTTP web server.</span></span> <span data-ttu-id="8b587-2399">Ele usa um certificado do cliente no computador com o Gateway de Gerenciamento de Dados instalado.</span><span class="sxs-lookup"><span data-stu-id="8b587-2399">It uses a client certificate file on the machine with Data Management Gateway installed.</span></span>

```json
{
    "name": "HttpLinkedService",
    "properties": {
        "type": "Http",
        "typeProperties": {
            "authenticationType": "ClientCertificate",
            "url": "https://en.wikipedia.org/wiki/",
            "embeddedCertData": "base64 encoded cert data",
            "password": "password of cert"
        }
    }
}
```

<span data-ttu-id="8b587-2400">Para obter mais informações, consulte o artigo [Conector do HTTP](data-factory-http-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="8b587-2400">For more information, see [HTTP connector](data-factory-http-connector.md#linked-service-properties) article.</span></span>

### <a name="dataset"></a><span data-ttu-id="8b587-2401">Conjunto de dados</span><span class="sxs-lookup"><span data-stu-id="8b587-2401">Dataset</span></span>
<span data-ttu-id="8b587-2402">Para definir um conjunto de dados do HDFS, defina o **type** do conjunto de dados para **Http** e especifique as propriedades a seguir na seção **typeProperties**:</span><span class="sxs-lookup"><span data-stu-id="8b587-2402">To define a HTTP dataset, set the **type** of the dataset to **Http**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="8b587-2403">Propriedade</span><span class="sxs-lookup"><span data-stu-id="8b587-2403">Property</span></span> | <span data-ttu-id="8b587-2404">Descrição</span><span class="sxs-lookup"><span data-stu-id="8b587-2404">Description</span></span> | <span data-ttu-id="8b587-2405">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="8b587-2405">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="8b587-2406">relativeUrl</span><span class="sxs-lookup"><span data-stu-id="8b587-2406">relativeUrl</span></span> | <span data-ttu-id="8b587-2407">Uma URL relativa para o recurso que contém os dados.</span><span class="sxs-lookup"><span data-stu-id="8b587-2407">A relative URL to the resource that contains the data.</span></span> <span data-ttu-id="8b587-2408">Quando o caminho não for especificado, apenas a URL especificada na definição do serviço vinculado será usada.</span><span class="sxs-lookup"><span data-stu-id="8b587-2408">When path is not specified, only the URL specified in the linked service definition is used.</span></span> <br><br> <span data-ttu-id="8b587-2409">Para construir um URL dinâmico, você pode usar [funções de Data Factory e variáveis de sistema](data-factory-functions-variables.md), Exemplo: `"relativeUrl": "$$Text.Format('/my/report?month={0:yyyy}-{0:MM}&fmt=csv', SliceStart)"`.</span><span class="sxs-lookup"><span data-stu-id="8b587-2409">To construct dynamic URL, you can use [Data Factory functions and system variables](data-factory-functions-variables.md), Example: `"relativeUrl": "$$Text.Format('/my/report?month={0:yyyy}-{0:MM}&fmt=csv', SliceStart)"`.</span></span> | <span data-ttu-id="8b587-2410">Não</span><span class="sxs-lookup"><span data-stu-id="8b587-2410">No</span></span> |
| <span data-ttu-id="8b587-2411">requestMethod</span><span class="sxs-lookup"><span data-stu-id="8b587-2411">requestMethod</span></span> | <span data-ttu-id="8b587-2412">Método Http.</span><span class="sxs-lookup"><span data-stu-id="8b587-2412">Http method.</span></span> <span data-ttu-id="8b587-2413">Os valores permitidos são **GET** ou **POST**.</span><span class="sxs-lookup"><span data-stu-id="8b587-2413">Allowed values are **GET** or **POST**.</span></span> | <span data-ttu-id="8b587-2414">Não.</span><span class="sxs-lookup"><span data-stu-id="8b587-2414">No.</span></span> <span data-ttu-id="8b587-2415">O padrão é `GET`.</span><span class="sxs-lookup"><span data-stu-id="8b587-2415">Default is `GET`.</span></span> |
| <span data-ttu-id="8b587-2416">additionalHeaders</span><span class="sxs-lookup"><span data-stu-id="8b587-2416">additionalHeaders</span></span> | <span data-ttu-id="8b587-2417">Cabeçalhos de solicitação HTTP adicionais.</span><span class="sxs-lookup"><span data-stu-id="8b587-2417">Additional HTTP request headers.</span></span> | <span data-ttu-id="8b587-2418">Não</span><span class="sxs-lookup"><span data-stu-id="8b587-2418">No</span></span> |
| <span data-ttu-id="8b587-2419">requestBody</span><span class="sxs-lookup"><span data-stu-id="8b587-2419">requestBody</span></span> | <span data-ttu-id="8b587-2420">O corpo da solicitação HTTP.</span><span class="sxs-lookup"><span data-stu-id="8b587-2420">Body for HTTP request.</span></span> | <span data-ttu-id="8b587-2421">Não</span><span class="sxs-lookup"><span data-stu-id="8b587-2421">No</span></span> |
| <span data-ttu-id="8b587-2422">formato</span><span class="sxs-lookup"><span data-stu-id="8b587-2422">format</span></span> | <span data-ttu-id="8b587-2423">Se você quiser simplesmente **recuperar os dados do ponto de extremidade HTTP como estão** sem analisá-los, ignore estas configurações de formato.</span><span class="sxs-lookup"><span data-stu-id="8b587-2423">If you want to simply **retrieve the data from HTTP endpoint as-is** without parsing it, skip this format settings.</span></span> <br><br> <span data-ttu-id="8b587-2424">Se você quiser analisar o conteúdo da resposta HTTP durante a cópia, há suporte para os seguintes tipos de formato: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat** e **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="8b587-2424">If you want to parse the HTTP response content during copy, the following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="8b587-2425">Para saber mais, veja as seções [Formato de texto](data-factory-supported-file-and-compression-formats.md#text-format), [Formato Json](data-factory-supported-file-and-compression-formats.md#json-format), [Formato Avro](data-factory-supported-file-and-compression-formats.md#avro-format), [Formato Orc](data-factory-supported-file-and-compression-formats.md#orc-format), e [Formato Parquet](data-factory-supported-file-and-compression-formats.md#parquet-format).</span><span class="sxs-lookup"><span data-stu-id="8b587-2425">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> |<span data-ttu-id="8b587-2426">Não</span><span class="sxs-lookup"><span data-stu-id="8b587-2426">No</span></span> |
| <span data-ttu-id="8b587-2427">compactação</span><span class="sxs-lookup"><span data-stu-id="8b587-2427">compression</span></span> | <span data-ttu-id="8b587-2428">Especifique o tipo e o nível de compactação para os dados.</span><span class="sxs-lookup"><span data-stu-id="8b587-2428">Specify the type and level of compression for the data.</span></span> <span data-ttu-id="8b587-2429">Os tipos com suporte são: **GZip**, **Deflate**, **BZip2** e **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="8b587-2429">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="8b587-2430">Os níveis com suporte são **Ideal** e **O mais rápido**.</span><span class="sxs-lookup"><span data-stu-id="8b587-2430">Supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="8b587-2431">Para saber mais, confira [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support) (Formatos de arquivo e de compactação no Azure Data Factory).</span><span class="sxs-lookup"><span data-stu-id="8b587-2431">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="8b587-2432">Não</span><span class="sxs-lookup"><span data-stu-id="8b587-2432">No</span></span> |

#### <a name="example-using-the-get-default-method"></a><span data-ttu-id="8b587-2433">Exemplo: usando o método GET (padrão)</span><span class="sxs-lookup"><span data-stu-id="8b587-2433">Example: using the GET (default) method</span></span>

```json
{
    "name": "HttpSourceDataInput",
    "properties": {
        "type": "Http",
        "linkedServiceName": "HttpLinkedService",
        "typeProperties": {
            "relativeUrl": "XXX/test.xml",
            "additionalHeaders": "Connection: keep-alive\nUser-Agent: Mozilla/5.0\n"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

#### <a name="example-using-the-post-method"></a><span data-ttu-id="8b587-2434">Exemplo: usando o método POST</span><span class="sxs-lookup"><span data-stu-id="8b587-2434">Example: using the POST method</span></span>

```json
{
    "name": "HttpSourceDataInput",
    "properties": {
        "type": "Http",
        "linkedServiceName": "HttpLinkedService",
        "typeProperties": {
            "relativeUrl": "/XXX/test.xml",
            "requestMethod": "Post",
            "requestBody": "body for POST HTTP request"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```
<span data-ttu-id="8b587-2435">Para obter mais informações, consulte o artigo [Conector do HTTP](data-factory-http-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="8b587-2435">For more information, see [HTTP connector](data-factory-http-connector.md#dataset-properties) article.</span></span>

### <a name="http-source-in-copy-activity"></a><span data-ttu-id="8b587-2436">Origem do HTTP na Atividade de Cópia</span><span class="sxs-lookup"><span data-stu-id="8b587-2436">HTTP Source in Copy Activity</span></span>
<span data-ttu-id="8b587-2437">Se você estiver copiando dados de uma origem do HTTP, defina o **source type** da atividade de cópia para **HttpSource** e especifique as propriedades a seguir na seção **source**:</span><span class="sxs-lookup"><span data-stu-id="8b587-2437">If you are copying data from a HTTP source, set the **source type** of the copy activity to **HttpSource**, and specify following properties in the **source** section:</span></span>

| <span data-ttu-id="8b587-2438">Propriedade</span><span class="sxs-lookup"><span data-stu-id="8b587-2438">Property</span></span> | <span data-ttu-id="8b587-2439">Descrição</span><span class="sxs-lookup"><span data-stu-id="8b587-2439">Description</span></span> | <span data-ttu-id="8b587-2440">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="8b587-2440">Required</span></span> |
| -------- | ----------- | -------- |
| <span data-ttu-id="8b587-2441">httpRequestTimeout</span><span class="sxs-lookup"><span data-stu-id="8b587-2441">httpRequestTimeout</span></span> | <span data-ttu-id="8b587-2442">O tempo limite (TimeSpan) para a solicitação HTTP obter uma resposta.</span><span class="sxs-lookup"><span data-stu-id="8b587-2442">The timeout (TimeSpan) for the HTTP request to get a response.</span></span> <span data-ttu-id="8b587-2443">É o tempo limite para obter uma resposta e não o tempo limite para ler dados de resposta.</span><span class="sxs-lookup"><span data-stu-id="8b587-2443">It is the timeout to get a response, not the timeout to read response data.</span></span> | <span data-ttu-id="8b587-2444">Não.</span><span class="sxs-lookup"><span data-stu-id="8b587-2444">No.</span></span> <span data-ttu-id="8b587-2445">Valor padrão: 00:01:40</span><span class="sxs-lookup"><span data-stu-id="8b587-2445">Default value: 00:01:40</span></span> |


#### <a name="example"></a><span data-ttu-id="8b587-2446">Exemplo</span><span class="sxs-lookup"><span data-stu-id="8b587-2446">Example</span></span>

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "HttpSourceToAzureBlob",
            "description": "Copy from an HTTP source to an Azure blob",
            "type": "Copy",
            "inputs": [{
                "name": "HttpSourceDataInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "HttpSource"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

<span data-ttu-id="8b587-2447">Para obter mais informações, consulte o artigo [Conector do HTTP](data-factory-http-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="8b587-2447">For more information, see [HTTP connector](data-factory-http-connector.md#copy-activity-properties) article.</span></span>

## <a name="odata"></a><span data-ttu-id="8b587-2448">OData</span><span class="sxs-lookup"><span data-stu-id="8b587-2448">OData</span></span>

### <a name="linked-service"></a><span data-ttu-id="8b587-2449">Serviço vinculado</span><span class="sxs-lookup"><span data-stu-id="8b587-2449">Linked service</span></span>
<span data-ttu-id="8b587-2450">Para definir um serviço vinculado do OData, defina o **type** do serviço vinculado para **OData** e especifique as propriedades a seguir na seção **typeProperties**:</span><span class="sxs-lookup"><span data-stu-id="8b587-2450">To define an OData linked service, set the **type** of the linked service to **OData**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="8b587-2451">Propriedade</span><span class="sxs-lookup"><span data-stu-id="8b587-2451">Property</span></span> | <span data-ttu-id="8b587-2452">Descrição</span><span class="sxs-lookup"><span data-stu-id="8b587-2452">Description</span></span> | <span data-ttu-id="8b587-2453">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="8b587-2453">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8b587-2454">url</span><span class="sxs-lookup"><span data-stu-id="8b587-2454">url</span></span> |<span data-ttu-id="8b587-2455">URL do serviço OData.</span><span class="sxs-lookup"><span data-stu-id="8b587-2455">Url of the OData service.</span></span> |<span data-ttu-id="8b587-2456">Sim</span><span class="sxs-lookup"><span data-stu-id="8b587-2456">Yes</span></span> |
| <span data-ttu-id="8b587-2457">authenticationType</span><span class="sxs-lookup"><span data-stu-id="8b587-2457">authenticationType</span></span> |<span data-ttu-id="8b587-2458">Tipo de autenticação usada para se conectar ao armazenamento de dados OData.</span><span class="sxs-lookup"><span data-stu-id="8b587-2458">Type of authentication used to connect to the OData source.</span></span> <br/><br/> <span data-ttu-id="8b587-2459">Para o OData de nuvem, os valores possíveis são Anônimo, Básico e OAuth (observe que o Azure Data Factory dá suporte no momento apenas a OAuth baseado no Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="8b587-2459">For cloud OData, possible values are Anonymous, Basic, and OAuth (note Azure Data Factory currently only support Azure Active Directory based OAuth).</span></span> <br/><br/> <span data-ttu-id="8b587-2460">Para OData local, os valores possíveis são Anonymous, Basic e Windows.</span><span class="sxs-lookup"><span data-stu-id="8b587-2460">For on-premises OData, possible values are Anonymous, Basic, and Windows.</span></span> |<span data-ttu-id="8b587-2461">Sim</span><span class="sxs-lookup"><span data-stu-id="8b587-2461">Yes</span></span> |
| <span data-ttu-id="8b587-2462">Nome de Usuário</span><span class="sxs-lookup"><span data-stu-id="8b587-2462">username</span></span> |<span data-ttu-id="8b587-2463">Especifique o nome de usuário se você estiver usando a autenticação Básica.</span><span class="sxs-lookup"><span data-stu-id="8b587-2463">Specify user name if you are using Basic authentication.</span></span> |<span data-ttu-id="8b587-2464">Sim (apenas se você estiver usando a autenticação Básica)</span><span class="sxs-lookup"><span data-stu-id="8b587-2464">Yes (only if you are using Basic authentication)</span></span> |
| <span data-ttu-id="8b587-2465">Senha</span><span class="sxs-lookup"><span data-stu-id="8b587-2465">password</span></span> |<span data-ttu-id="8b587-2466">Especifique a senha da conta de usuário que você especificou para o nome de usuário.</span><span class="sxs-lookup"><span data-stu-id="8b587-2466">Specify password for the user account you specified for the username.</span></span> |<span data-ttu-id="8b587-2467">Sim (apenas se você estiver usando a autenticação Básica)</span><span class="sxs-lookup"><span data-stu-id="8b587-2467">Yes (only if you are using Basic authentication)</span></span> |
| <span data-ttu-id="8b587-2468">authorizedCredential</span><span class="sxs-lookup"><span data-stu-id="8b587-2468">authorizedCredential</span></span> |<span data-ttu-id="8b587-2469">Se você estiver usando OAuth, clique no botão **Autorizar** no Editor ou Assistente de Cópia do Data Factory e digite suas credenciais. O valor dessa propriedade será gerado automaticamente.</span><span class="sxs-lookup"><span data-stu-id="8b587-2469">If you are using OAuth, click **Authorize** button in the Data Factory Copy Wizard or Editor and enter your credential, then the value of this property will be auto-generated.</span></span> |<span data-ttu-id="8b587-2470">Sim (apenas se você estiver usando a autenticação OAuth)</span><span class="sxs-lookup"><span data-stu-id="8b587-2470">Yes (only if you are using OAuth authentication)</span></span> |
| <span data-ttu-id="8b587-2471">gatewayName</span><span class="sxs-lookup"><span data-stu-id="8b587-2471">gatewayName</span></span> |<span data-ttu-id="8b587-2472">O nome do gateway que o serviço Data Factory deve usar para se conectar ao serviço OData local.</span><span class="sxs-lookup"><span data-stu-id="8b587-2472">Name of the gateway that the Data Factory service should use to connect to the on-premises OData service.</span></span> <span data-ttu-id="8b587-2473">Só especifique se você estiver copiando dados da fonte OData local.</span><span class="sxs-lookup"><span data-stu-id="8b587-2473">Specify only if you are copying data from on-prem OData source.</span></span> |<span data-ttu-id="8b587-2474">Não</span><span class="sxs-lookup"><span data-stu-id="8b587-2474">No</span></span> |

#### <a name="example---using-basic-authentication"></a><span data-ttu-id="8b587-2475">Exemplo - Usando a autenticação básica</span><span class="sxs-lookup"><span data-stu-id="8b587-2475">Example - Using Basic authentication</span></span>
```json
{
    "name": "inputLinkedService",
    "properties": {
        "type": "OData",
        "typeProperties": {
            "url": "http://services.odata.org/OData/OData.svc",
            "authenticationType": "Basic",
            "username": "username",
            "password": "password"
        }
    }
}
```

#### <a name="example---using-anonymous-authentication"></a><span data-ttu-id="8b587-2476">Exemplo - Usando a autenticação anônima</span><span class="sxs-lookup"><span data-stu-id="8b587-2476">Example - Using Anonymous authentication</span></span>

```json
{
    "name": "ODataLinkedService",
    "properties": {
        "type": "OData",
        "typeProperties": {
            "url": "http://services.odata.org/OData/OData.svc",
            "authenticationType": "Anonymous"
        }
    }
}
```

#### <a name="example---using-windows-authentication-accessing-on-premises-odata-source"></a><span data-ttu-id="8b587-2477">Exemplo - Usando a autenticação do Windows para acessar uma origem de OData local</span><span class="sxs-lookup"><span data-stu-id="8b587-2477">Example - Using Windows authentication accessing on-premises OData source</span></span>

```json
{
    "name": "inputLinkedService",
    "properties": {
        "type": "OData",
        "typeProperties": {
            "url": "<endpoint of on-premises OData source, for example, Dynamics CRM>",
            "authenticationType": "Windows",
            "username": "domain\\user",
            "password": "password",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

#### <a name="example---using-oauth-authentication-accessing-cloud-odata-source"></a><span data-ttu-id="8b587-2478">Exemplo - Usando autenticação OAuth para acessar a origem de OData da nuvem</span><span class="sxs-lookup"><span data-stu-id="8b587-2478">Example - Using OAuth authentication accessing cloud OData source</span></span>
```json
{
    "name": "inputLinkedService",
    "properties":
    {
        "type": "OData",
            "typeProperties":
        {
            "url": "<endpoint of cloud OData source, for example, https://<tenant>.crm.dynamics.com/XRMServices/2011/OrganizationData.svc>",
            "authenticationType": "OAuth",
            "authorizedCredential": "<auto generated by clicking the Authorize button on UI>"
        }
    }
}
```

<span data-ttu-id="8b587-2479">Para obter mais informações, consulte o artigo [Conector do OData](data-factory-odata-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="8b587-2479">For more information, see [OData connector](data-factory-odata-connector.md#linked-service-properties) article.</span></span>

### <a name="dataset"></a><span data-ttu-id="8b587-2480">Conjunto de dados</span><span class="sxs-lookup"><span data-stu-id="8b587-2480">Dataset</span></span>
<span data-ttu-id="8b587-2481">Para definir um conjunto de dados do OData, defina o **type** do conjunto de dados para **ODataResource** e especifique as propriedades a seguir na seção **typeProperties**:</span><span class="sxs-lookup"><span data-stu-id="8b587-2481">To define an OData dataset, set the **type** of the dataset to **ODataResource**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="8b587-2482">Propriedade</span><span class="sxs-lookup"><span data-stu-id="8b587-2482">Property</span></span> | <span data-ttu-id="8b587-2483">Descrição</span><span class="sxs-lookup"><span data-stu-id="8b587-2483">Description</span></span> | <span data-ttu-id="8b587-2484">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="8b587-2484">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8b587-2485">caminho</span><span class="sxs-lookup"><span data-stu-id="8b587-2485">path</span></span> |<span data-ttu-id="8b587-2486">Caminho para o recurso OData</span><span class="sxs-lookup"><span data-stu-id="8b587-2486">Path to the OData resource</span></span> |<span data-ttu-id="8b587-2487">Não</span><span class="sxs-lookup"><span data-stu-id="8b587-2487">No</span></span> |

#### <a name="example"></a><span data-ttu-id="8b587-2488">Exemplo</span><span class="sxs-lookup"><span data-stu-id="8b587-2488">Example</span></span>

```json
{
    "name": "ODataDataset",
    "properties": {
        "type": "ODataResource",
        "typeProperties": {
            "path": "Products"
        },
        "linkedServiceName": "ODataLinkedService",
        "structure": [],
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {
            "retryInterval": "00:01:00",
            "retryTimeout": "00:10:00",
            "maximumRetry": 3
        }
    }
}
```

<span data-ttu-id="8b587-2489">Para obter mais informações, consulte o artigo [Conector do OData](data-factory-odata-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="8b587-2489">For more information, see [OData connector](data-factory-odata-connector.md#dataset-properties) article.</span></span>

### <a name="relational-source-in-copy-activity"></a><span data-ttu-id="8b587-2490">Origem Relacional na Atividade de Cópia</span><span class="sxs-lookup"><span data-stu-id="8b587-2490">Relational Source in Copy Activity</span></span>
<span data-ttu-id="8b587-2491">Se você estiver copiando dados de uma origem de OData, defina o **source type** da atividade de cópia para **RelationalSource** e especifique as propriedades a seguir na seção **source**:</span><span class="sxs-lookup"><span data-stu-id="8b587-2491">If you are copying data from an OData source, set the **source type** of the copy activity to **RelationalSource**, and specify following properties in the **source** section:</span></span>

| <span data-ttu-id="8b587-2492">Propriedade</span><span class="sxs-lookup"><span data-stu-id="8b587-2492">Property</span></span> | <span data-ttu-id="8b587-2493">Descrição</span><span class="sxs-lookup"><span data-stu-id="8b587-2493">Description</span></span> | <span data-ttu-id="8b587-2494">Exemplo</span><span class="sxs-lookup"><span data-stu-id="8b587-2494">Example</span></span> | <span data-ttu-id="8b587-2495">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="8b587-2495">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="8b587-2496">query</span><span class="sxs-lookup"><span data-stu-id="8b587-2496">query</span></span> |<span data-ttu-id="8b587-2497">Utiliza a consulta personalizada para ler os dados.</span><span class="sxs-lookup"><span data-stu-id="8b587-2497">Use the custom query to read data.</span></span> |<span data-ttu-id="8b587-2498">"?$select=Name, Description&$top=5"</span><span class="sxs-lookup"><span data-stu-id="8b587-2498">"?$select=Name, Description&$top=5"</span></span> |<span data-ttu-id="8b587-2499">Não</span><span class="sxs-lookup"><span data-stu-id="8b587-2499">No</span></span> |

#### <a name="example"></a><span data-ttu-id="8b587-2500">Exemplo</span><span class="sxs-lookup"><span data-stu-id="8b587-2500">Example</span></span>

```json
{
    "name": "CopyODataToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "?$select=Name, Description&$top=5"
                },
                "sink": {
                    "type": "BlobSink",
                    "writeBatchSize": 0,
                    "writeBatchTimeout": "00:00:00"
                }
            },
            "inputs": [{
                "name": "ODataDataSet"
            }],
            "outputs": [{
                "name": "AzureBlobODataDataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "ODataToBlob"
        }],
        "start": "2017-02-01T18:00:00",
        "end": "2017-02-03T19:00:00"
    }
}
```

<span data-ttu-id="8b587-2501">Para obter mais informações, consulte o artigo [Conector do OData](data-factory-odata-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="8b587-2501">For more information, see [OData connector](data-factory-odata-connector.md#copy-activity-properties) article.</span></span>


## <a name="odbc"></a><span data-ttu-id="8b587-2502">ODBC</span><span class="sxs-lookup"><span data-stu-id="8b587-2502">ODBC</span></span>


### <a name="linked-service"></a><span data-ttu-id="8b587-2503">Serviço vinculado</span><span class="sxs-lookup"><span data-stu-id="8b587-2503">Linked service</span></span>
<span data-ttu-id="8b587-2504">Para definir um serviço vinculado do ODBC, defina o **type** do serviço vinculado para **OnPremisesOdbc** e especifique as propriedades a seguir na seção **typeProperties**:</span><span class="sxs-lookup"><span data-stu-id="8b587-2504">To define an ODBC linked service, set the **type** of the linked service to **OnPremisesOdbc**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="8b587-2505">Propriedade</span><span class="sxs-lookup"><span data-stu-id="8b587-2505">Property</span></span> | <span data-ttu-id="8b587-2506">Descrição</span><span class="sxs-lookup"><span data-stu-id="8b587-2506">Description</span></span> | <span data-ttu-id="8b587-2507">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="8b587-2507">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8b587-2508">connectionString</span><span class="sxs-lookup"><span data-stu-id="8b587-2508">connectionString</span></span> |<span data-ttu-id="8b587-2509">A parte da credencial que não está relacionada ao acesso da cadeia de conexão e uma credencial criptografada opcional.</span><span class="sxs-lookup"><span data-stu-id="8b587-2509">The non-access credential portion of the connection string and an optional encrypted credential.</span></span> <span data-ttu-id="8b587-2510">Veja os exemplos nas seções a seguir.</span><span class="sxs-lookup"><span data-stu-id="8b587-2510">See examples in the following sections.</span></span> |<span data-ttu-id="8b587-2511">Sim</span><span class="sxs-lookup"><span data-stu-id="8b587-2511">Yes</span></span> |
| <span data-ttu-id="8b587-2512">credencial</span><span class="sxs-lookup"><span data-stu-id="8b587-2512">credential</span></span> |<span data-ttu-id="8b587-2513">A parte da credencial de acesso da cadeia de conexão especificada no formato propriedade-valor específico do driver.</span><span class="sxs-lookup"><span data-stu-id="8b587-2513">The access credential portion of the connection string specified in driver-specific property-value format.</span></span> <span data-ttu-id="8b587-2514">Exemplo: "Uid=<user ID>;Pwd=<password>;RefreshToken=<secret refresh token>;".</span><span class="sxs-lookup"><span data-stu-id="8b587-2514">Example: “Uid=<user ID>;Pwd=<password>;RefreshToken=<secret refresh token>;”.</span></span> |<span data-ttu-id="8b587-2515">Não</span><span class="sxs-lookup"><span data-stu-id="8b587-2515">No</span></span> |
| <span data-ttu-id="8b587-2516">authenticationType</span><span class="sxs-lookup"><span data-stu-id="8b587-2516">authenticationType</span></span> |<span data-ttu-id="8b587-2517">Tipo de autenticação usado para se conectar ao armazenamento de dados ODBC.</span><span class="sxs-lookup"><span data-stu-id="8b587-2517">Type of authentication used to connect to the ODBC data store.</span></span> <span data-ttu-id="8b587-2518">Os valores possíveis são: Anonymous e Basic.</span><span class="sxs-lookup"><span data-stu-id="8b587-2518">Possible values are: Anonymous and Basic.</span></span> |<span data-ttu-id="8b587-2519">Sim</span><span class="sxs-lookup"><span data-stu-id="8b587-2519">Yes</span></span> |
| <span data-ttu-id="8b587-2520">Nome de Usuário</span><span class="sxs-lookup"><span data-stu-id="8b587-2520">username</span></span> |<span data-ttu-id="8b587-2521">Especifique o nome de usuário se você estiver usando a autenticação Básica.</span><span class="sxs-lookup"><span data-stu-id="8b587-2521">Specify user name if you are using Basic authentication.</span></span> |<span data-ttu-id="8b587-2522">Não</span><span class="sxs-lookup"><span data-stu-id="8b587-2522">No</span></span> |
| <span data-ttu-id="8b587-2523">Senha</span><span class="sxs-lookup"><span data-stu-id="8b587-2523">password</span></span> |<span data-ttu-id="8b587-2524">Especifique a senha da conta de usuário que você especificou para o nome de usuário.</span><span class="sxs-lookup"><span data-stu-id="8b587-2524">Specify password for the user account you specified for the username.</span></span> |<span data-ttu-id="8b587-2525">Não</span><span class="sxs-lookup"><span data-stu-id="8b587-2525">No</span></span> |
| <span data-ttu-id="8b587-2526">gatewayName</span><span class="sxs-lookup"><span data-stu-id="8b587-2526">gatewayName</span></span> |<span data-ttu-id="8b587-2527">O nome do gateway que o serviço Data Factory deve usar para se conectar ao armazenamento de dados ODBC.</span><span class="sxs-lookup"><span data-stu-id="8b587-2527">Name of the gateway that the Data Factory service should use to connect to the ODBC data store.</span></span> |<span data-ttu-id="8b587-2528">Sim</span><span class="sxs-lookup"><span data-stu-id="8b587-2528">Yes</span></span> |

#### <a name="example---using-basic-authentication"></a><span data-ttu-id="8b587-2529">Exemplo - Usando a autenticação básica</span><span class="sxs-lookup"><span data-stu-id="8b587-2529">Example - Using Basic authentication</span></span>

```json
{
    "name": "ODBCLinkedService",
    "properties": {
        "type": "OnPremisesOdbc",
        "typeProperties": {
            "authenticationType": "Basic",
            "connectionString": "Driver={SQL Server};Server=Server.database.windows.net; Database=TestDatabase;",
            "userName": "username",
            "password": "password",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```
#### <a name="example---using-basic-authentication-with-encrypted-credentials"></a><span data-ttu-id="8b587-2530">Exemplo - Usando a autenticação básica com credenciais criptografadas</span><span class="sxs-lookup"><span data-stu-id="8b587-2530">Example - Using Basic authentication with encrypted credentials</span></span>
<span data-ttu-id="8b587-2531">Você pode criptografar as credenciais usando o cmdlet [New-AzureRMDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) (versão 1.0 do Azure PowerShell) ou [New-AzureDataFactoryEncryptValue](https://msdn.microsoft.com/library/dn834940.aspx) (versão 0.9 ou anterior do Azure PowerShell).</span><span class="sxs-lookup"><span data-stu-id="8b587-2531">You can encrypt the credentials using the [New-AzureRMDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) (1.0 version of Azure PowerShell) cmdlet or [New-AzureDataFactoryEncryptValue](https://msdn.microsoft.com/library/dn834940.aspx) (0.9 or earlier version of the Azure PowerShell).</span></span>  

```json
{
    "name": "ODBCLinkedService",
    "properties": {
        "type": "OnPremisesOdbc",
        "typeProperties": {
            "authenticationType": "Basic",
            "connectionString": "Driver={SQL Server};Server=myserver.database.windows.net; Database=TestDatabase;;EncryptedCredential=eyJDb25uZWN0...........................",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

#### <a name="example-using-anonymous-authentication"></a><span data-ttu-id="8b587-2532">Exemplo: Usando a autenticação anônima</span><span class="sxs-lookup"><span data-stu-id="8b587-2532">Example: Using Anonymous authentication</span></span>

```json
{
    "name": "ODBCLinkedService",
    "properties": {
        "type": "OnPremisesOdbc",
        "typeProperties": {
            "authenticationType": "Anonymous",
            "connectionString": "Driver={SQL Server};Server={servername}.database.windows.net; Database=TestDatabase;",
            "credential": "UID={uid};PWD={pwd}",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

<span data-ttu-id="8b587-2533">Para obter mais informações, consulte o artigo [Conector do ODBC](data-factory-odbc-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="8b587-2533">For more information, see [ODBC connector](data-factory-odbc-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="8b587-2534">Conjunto de dados</span><span class="sxs-lookup"><span data-stu-id="8b587-2534">Dataset</span></span>
<span data-ttu-id="8b587-2535">Para definir um conjunto de dados do ODBC, defina o **type** do conjunto de dados para **RelationalTable** e especifique as propriedades a seguir na seção **typeProperties**:</span><span class="sxs-lookup"><span data-stu-id="8b587-2535">To define an ODBC dataset, set the **type** of the dataset to **RelationalTable**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="8b587-2536">Propriedade</span><span class="sxs-lookup"><span data-stu-id="8b587-2536">Property</span></span> | <span data-ttu-id="8b587-2537">Descrição</span><span class="sxs-lookup"><span data-stu-id="8b587-2537">Description</span></span> | <span data-ttu-id="8b587-2538">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="8b587-2538">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8b587-2539">tableName</span><span class="sxs-lookup"><span data-stu-id="8b587-2539">tableName</span></span> |<span data-ttu-id="8b587-2540">Nome da tabela no repositório de dados ODBC.</span><span class="sxs-lookup"><span data-stu-id="8b587-2540">Name of the table in the ODBC data store.</span></span> |<span data-ttu-id="8b587-2541">Sim</span><span class="sxs-lookup"><span data-stu-id="8b587-2541">Yes</span></span> |


#### <a name="example"></a><span data-ttu-id="8b587-2542">Exemplo</span><span class="sxs-lookup"><span data-stu-id="8b587-2542">Example</span></span>

```json
{
    "name": "ODBCDataSet",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "ODBCLinkedService",
        "typeProperties": {},
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```

<span data-ttu-id="8b587-2543">Para obter mais informações, consulte o artigo [Conector do ODBC](data-factory-odbc-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="8b587-2543">For more information, see [ODBC connector](data-factory-odbc-connector.md#dataset-properties) article.</span></span> 

### <a name="relational-source-in-copy-activity"></a><span data-ttu-id="8b587-2544">Origem Relacional na Atividade de Cópia</span><span class="sxs-lookup"><span data-stu-id="8b587-2544">Relational Source in Copy Activity</span></span>
<span data-ttu-id="8b587-2545">Se você estiver copiando dados de um armazenamento de dados do ODBC, defina o **source type** da atividade de cópia para **RelationalSource** e especifique as propriedades a seguir na seção **source**:</span><span class="sxs-lookup"><span data-stu-id="8b587-2545">If you are copying data from an ODBC data store, set the **source type** of the copy activity to **RelationalSource**, and specify following properties in the **source** section:</span></span>

| <span data-ttu-id="8b587-2546">Propriedade</span><span class="sxs-lookup"><span data-stu-id="8b587-2546">Property</span></span> | <span data-ttu-id="8b587-2547">Descrição</span><span class="sxs-lookup"><span data-stu-id="8b587-2547">Description</span></span> | <span data-ttu-id="8b587-2548">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="8b587-2548">Allowed values</span></span> | <span data-ttu-id="8b587-2549">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="8b587-2549">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="8b587-2550">query</span><span class="sxs-lookup"><span data-stu-id="8b587-2550">query</span></span> |<span data-ttu-id="8b587-2551">Utiliza a consulta personalizada para ler os dados.</span><span class="sxs-lookup"><span data-stu-id="8b587-2551">Use the custom query to read data.</span></span> |<span data-ttu-id="8b587-2552">Cadeia de caracteres de consulta SQL.</span><span class="sxs-lookup"><span data-stu-id="8b587-2552">SQL query string.</span></span> <span data-ttu-id="8b587-2553">Por exemplo: `select * from MyTable`.</span><span class="sxs-lookup"><span data-stu-id="8b587-2553">For example: `select * from MyTable`.</span></span> |<span data-ttu-id="8b587-2554">Sim</span><span class="sxs-lookup"><span data-stu-id="8b587-2554">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="8b587-2555">Exemplo</span><span class="sxs-lookup"><span data-stu-id="8b587-2555">Example</span></span>

```json
{
    "name": "CopyODBCToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "$$Text.Format('select * from MyTable where timestamp >= \\'{0:yyyy-MM-ddTHH:mm:ss}\\' AND timestamp < \\'{1:yyyy-MM-ddTHH:mm:ss}\\'', WindowStart, WindowEnd)"
                },
                "sink": {
                    "type": "BlobSink",
                    "writeBatchSize": 0,
                    "writeBatchTimeout": "00:00:00"
                }
            },
            "inputs": [{
                "name": "OdbcDataSet"
            }],
            "outputs": [{
                "name": "AzureBlobOdbcDataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "OdbcToBlob"
        }],
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00"
    }
}
``` 

<span data-ttu-id="8b587-2556">Para obter mais informações, consulte o artigo [Conector do ODBC](data-factory-odbc-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="8b587-2556">For more information, see [ODBC connector](data-factory-odbc-connector.md#copy-activity-properties) article.</span></span>

## <a name="salesforce"></a><span data-ttu-id="8b587-2557">Salesforce</span><span class="sxs-lookup"><span data-stu-id="8b587-2557">Salesforce</span></span>


### <a name="linked-service"></a><span data-ttu-id="8b587-2558">Serviço vinculado</span><span class="sxs-lookup"><span data-stu-id="8b587-2558">Linked service</span></span>
<span data-ttu-id="8b587-2559">Para definir um serviço vinculado da Salesforce, defina o **type** do serviço vinculado para **Salesforce** e especifique as propriedades a seguir na seção **typeProperties**:</span><span class="sxs-lookup"><span data-stu-id="8b587-2559">To define a Salesforce linked service, set the **type** of the linked service to **Salesforce**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="8b587-2560">Propriedade</span><span class="sxs-lookup"><span data-stu-id="8b587-2560">Property</span></span> | <span data-ttu-id="8b587-2561">Descrição</span><span class="sxs-lookup"><span data-stu-id="8b587-2561">Description</span></span> | <span data-ttu-id="8b587-2562">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="8b587-2562">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8b587-2563">environmentUrl</span><span class="sxs-lookup"><span data-stu-id="8b587-2563">environmentUrl</span></span> | <span data-ttu-id="8b587-2564">Especifica a URL da instância do Salesforce.</span><span class="sxs-lookup"><span data-stu-id="8b587-2564">Specify the URL of Salesforce instance.</span></span> <br><br> <span data-ttu-id="8b587-2565">– O padrão é "https://login.salesforce.com".</span><span class="sxs-lookup"><span data-stu-id="8b587-2565">- Default is "https://login.salesforce.com".</span></span> <br> <span data-ttu-id="8b587-2566">– Para copiar dados da área restrita, especifique "https://test.salesforce.com".</span><span class="sxs-lookup"><span data-stu-id="8b587-2566">- To copy data from sandbox, specify "https://test.salesforce.com".</span></span> <br> <span data-ttu-id="8b587-2567">– Para copiar dados do domínio personalizado, especifique, por exemplo, "https://[domínio].my.salesforce.com".</span><span class="sxs-lookup"><span data-stu-id="8b587-2567">- To copy data from custom domain, specify, for example, "https://[domain].my.salesforce.com".</span></span> |<span data-ttu-id="8b587-2568">Não</span><span class="sxs-lookup"><span data-stu-id="8b587-2568">No</span></span> |
| <span data-ttu-id="8b587-2569">Nome de Usuário</span><span class="sxs-lookup"><span data-stu-id="8b587-2569">username</span></span> |<span data-ttu-id="8b587-2570">Especifique um nome de usuário para a conta de usuário.</span><span class="sxs-lookup"><span data-stu-id="8b587-2570">Specify a user name for the user account.</span></span> |<span data-ttu-id="8b587-2571">Sim</span><span class="sxs-lookup"><span data-stu-id="8b587-2571">Yes</span></span> |
| <span data-ttu-id="8b587-2572">Senha</span><span class="sxs-lookup"><span data-stu-id="8b587-2572">password</span></span> |<span data-ttu-id="8b587-2573">Especifique um senha para a conta de usuário.</span><span class="sxs-lookup"><span data-stu-id="8b587-2573">Specify a password for the user account.</span></span> |<span data-ttu-id="8b587-2574">Sim</span><span class="sxs-lookup"><span data-stu-id="8b587-2574">Yes</span></span> |
| <span data-ttu-id="8b587-2575">securityToken</span><span class="sxs-lookup"><span data-stu-id="8b587-2575">securityToken</span></span> |<span data-ttu-id="8b587-2576">Especifique um token de segurança para a conta de usuário.</span><span class="sxs-lookup"><span data-stu-id="8b587-2576">Specify a security token for the user account.</span></span> <span data-ttu-id="8b587-2577">Veja [Obter token de segurança](https://help.salesforce.com/apex/HTViewHelpDoc?id=user_security_token.htm) para ver instruções sobre como redefinir/obter o token de segurança.</span><span class="sxs-lookup"><span data-stu-id="8b587-2577">See [Get security token](https://help.salesforce.com/apex/HTViewHelpDoc?id=user_security_token.htm) for instructions on how to reset/get a security token.</span></span> <span data-ttu-id="8b587-2578">Para saber mais sobre os tokens de segurança em geral, veja [Security and the API](https://developer.salesforce.com/docs/atlas.en-us.api.meta/api/sforce_api_concepts_security.htm) (Segurança e a API).</span><span class="sxs-lookup"><span data-stu-id="8b587-2578">To learn about security tokens in general, see [Security and the API](https://developer.salesforce.com/docs/atlas.en-us.api.meta/api/sforce_api_concepts_security.htm).</span></span> |<span data-ttu-id="8b587-2579">Sim</span><span class="sxs-lookup"><span data-stu-id="8b587-2579">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="8b587-2580">Exemplo</span><span class="sxs-lookup"><span data-stu-id="8b587-2580">Example</span></span>

```json
{
    "name": "SalesforceLinkedService",
    "properties": {
        "type": "Salesforce",
        "typeProperties": {
            "username": "<user name>",
            "password": "<password>",
            "securityToken": "<security token>"
        }
    }
}
```

<span data-ttu-id="8b587-2581">Para obter mais informações, consulte o artigo [Conector da Salesforce](data-factory-salesforce-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="8b587-2581">For more information, see [Salesforce connector](data-factory-salesforce-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="8b587-2582">Conjunto de dados</span><span class="sxs-lookup"><span data-stu-id="8b587-2582">Dataset</span></span>
<span data-ttu-id="8b587-2583">Para definir um conjunto de dados da Salesforce, defina o **type** do conjunto de dados para **RelationalTable** e especifique as propriedades a seguir na seção **typeProperties**:</span><span class="sxs-lookup"><span data-stu-id="8b587-2583">To define a Salesforce dataset, set the **type** of the dataset to **RelationalTable**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="8b587-2584">Propriedade</span><span class="sxs-lookup"><span data-stu-id="8b587-2584">Property</span></span> | <span data-ttu-id="8b587-2585">Descrição</span><span class="sxs-lookup"><span data-stu-id="8b587-2585">Description</span></span> | <span data-ttu-id="8b587-2586">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="8b587-2586">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8b587-2587">tableName</span><span class="sxs-lookup"><span data-stu-id="8b587-2587">tableName</span></span> |<span data-ttu-id="8b587-2588">Nome da tabela no Salesforce.</span><span class="sxs-lookup"><span data-stu-id="8b587-2588">Name of the table in Salesforce.</span></span> |<span data-ttu-id="8b587-2589">Não (se uma **consulta** de **RelationalSource** for especificada)</span><span class="sxs-lookup"><span data-stu-id="8b587-2589">No (if a **query** of **RelationalSource** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="8b587-2590">Exemplo</span><span class="sxs-lookup"><span data-stu-id="8b587-2590">Example</span></span>

```json
{
    "name": "SalesforceInput",
    "properties": {
        "linkedServiceName": "SalesforceLinkedService",
        "type": "RelationalTable",
        "typeProperties": {
            "tableName": "AllDataType__c"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```

<span data-ttu-id="8b587-2591">Para obter mais informações, consulte o artigo [Conector da Salesforce](data-factory-salesforce-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="8b587-2591">For more information, see [Salesforce connector](data-factory-salesforce-connector.md#dataset-properties) article.</span></span> 

### <a name="relational-source-in-copy-activity"></a><span data-ttu-id="8b587-2592">Origem Relacional na Atividade de Cópia</span><span class="sxs-lookup"><span data-stu-id="8b587-2592">Relational Source in Copy Activity</span></span>
<span data-ttu-id="8b587-2593">Se você estiver copiando dados da Salesforce, defina o **source type** da atividade de cópia para **RelationalSource** e especifique as propriedades a seguir na seção **source**:</span><span class="sxs-lookup"><span data-stu-id="8b587-2593">If you are copying data from Salesforce, set the **source type** of the copy activity to **RelationalSource**, and specify following properties in the **source** section:</span></span>

| <span data-ttu-id="8b587-2594">Propriedade</span><span class="sxs-lookup"><span data-stu-id="8b587-2594">Property</span></span> | <span data-ttu-id="8b587-2595">Descrição</span><span class="sxs-lookup"><span data-stu-id="8b587-2595">Description</span></span> | <span data-ttu-id="8b587-2596">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="8b587-2596">Allowed values</span></span> | <span data-ttu-id="8b587-2597">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="8b587-2597">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="8b587-2598">query</span><span class="sxs-lookup"><span data-stu-id="8b587-2598">query</span></span> |<span data-ttu-id="8b587-2599">Utiliza a consulta personalizada para ler os dados.</span><span class="sxs-lookup"><span data-stu-id="8b587-2599">Use the custom query to read data.</span></span> |<span data-ttu-id="8b587-2600">Uma consulta SQL-92 ou uma consulta [SOQL (Salesforce Object Query Language)](https://developer.salesforce.com/docs/atlas.en-us.soql_sosl.meta/soql_sosl/sforce_api_calls_soql.htm).</span><span class="sxs-lookup"><span data-stu-id="8b587-2600">A SQL-92 query or [Salesforce Object Query Language (SOQL)](https://developer.salesforce.com/docs/atlas.en-us.soql_sosl.meta/soql_sosl/sforce_api_calls_soql.htm) query.</span></span> <span data-ttu-id="8b587-2601">Por exemplo: `select * from MyTable__c`.</span><span class="sxs-lookup"><span data-stu-id="8b587-2601">For example:  `select * from MyTable__c`.</span></span> |<span data-ttu-id="8b587-2602">Não (se **tableName** do **conjunto de dados** for especificado)</span><span class="sxs-lookup"><span data-stu-id="8b587-2602">No (if the **tableName** of the **dataset** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="8b587-2603">Exemplo</span><span class="sxs-lookup"><span data-stu-id="8b587-2603">Example</span></span>  



```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "SalesforceToAzureBlob",
            "description": "Copy from Salesforce to an Azure blob",
            "type": "Copy",
            "inputs": [{
                "name": "SalesforceInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "SELECT Id, Col_AutoNumber__c, Col_Checkbox__c, Col_Currency__c, Col_Date__c, Col_DateTime__c, Col_Email__c, Col_Number__c, Col_Percent__c, Col_Phone__c, Col_Picklist__c, Col_Picklist_MultiSelect__c, Col_Text__c, Col_Text_Area__c, Col_Text_AreaLong__c, Col_Text_AreaRich__c, Col_URL__c, Col_Text_Encrypt__c, Col_Lookup__c FROM AllDataType__c"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

> [!IMPORTANT]
> <span data-ttu-id="8b587-2604">A parte "__c" do Nome da API é necessária para qualquer objeto personalizado.</span><span class="sxs-lookup"><span data-stu-id="8b587-2604">The "__c" part of the API Name is needed for any custom object.</span></span>

<span data-ttu-id="8b587-2605">Para obter mais informações, consulte o artigo [Conector da Salesforce](data-factory-salesforce-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="8b587-2605">For more information, see [Salesforce connector](data-factory-salesforce-connector.md#copy-activity-properties) article.</span></span> 

## <a name="web-data"></a><span data-ttu-id="8b587-2606">Dados da Web</span><span class="sxs-lookup"><span data-stu-id="8b587-2606">Web Data</span></span> 

### <a name="linked-service"></a><span data-ttu-id="8b587-2607">Serviço vinculado</span><span class="sxs-lookup"><span data-stu-id="8b587-2607">Linked service</span></span>
<span data-ttu-id="8b587-2608">Para definir um serviço vinculado da Web, defina o **type** do serviço vinculado para **Web** e especifique as propriedades a seguir na seção **typeProperties**:</span><span class="sxs-lookup"><span data-stu-id="8b587-2608">To define a Web linked service, set the **type** of the linked service to **Web**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="8b587-2609">Propriedade</span><span class="sxs-lookup"><span data-stu-id="8b587-2609">Property</span></span> | <span data-ttu-id="8b587-2610">Descrição</span><span class="sxs-lookup"><span data-stu-id="8b587-2610">Description</span></span> | <span data-ttu-id="8b587-2611">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="8b587-2611">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8b587-2612">Url</span><span class="sxs-lookup"><span data-stu-id="8b587-2612">Url</span></span> |<span data-ttu-id="8b587-2613">URL para a origem da Web</span><span class="sxs-lookup"><span data-stu-id="8b587-2613">URL to the Web source</span></span> |<span data-ttu-id="8b587-2614">Sim</span><span class="sxs-lookup"><span data-stu-id="8b587-2614">Yes</span></span> |
| <span data-ttu-id="8b587-2615">authenticationType</span><span class="sxs-lookup"><span data-stu-id="8b587-2615">authenticationType</span></span> |<span data-ttu-id="8b587-2616">Anônima.</span><span class="sxs-lookup"><span data-stu-id="8b587-2616">Anonymous.</span></span> |<span data-ttu-id="8b587-2617">Sim</span><span class="sxs-lookup"><span data-stu-id="8b587-2617">Yes</span></span> |
 

#### <a name="example"></a><span data-ttu-id="8b587-2618">Exemplo</span><span class="sxs-lookup"><span data-stu-id="8b587-2618">Example</span></span>


```json
{
    "name": "web",
    "properties": {
        "type": "Web",
        "typeProperties": {
            "authenticationType": "Anonymous",
            "url": "https://en.wikipedia.org/wiki/"
        }
    }
}
```

<span data-ttu-id="8b587-2619">Para obter mais informações, consulte o artigo [Conector da Tabela da Web](data-factory-web-table-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="8b587-2619">For more information, see [Web Table connector](data-factory-web-table-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="8b587-2620">Conjunto de dados</span><span class="sxs-lookup"><span data-stu-id="8b587-2620">Dataset</span></span>
<span data-ttu-id="8b587-2621">Para definir um conjunto de dados da Web, defina o **type** do conjunto de dados para **WebTable** e especifique as propriedades a seguir na seção **typeProperties**:</span><span class="sxs-lookup"><span data-stu-id="8b587-2621">To define a Web dataset, set the **type** of the dataset to **WebTable**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="8b587-2622">Propriedade</span><span class="sxs-lookup"><span data-stu-id="8b587-2622">Property</span></span> | <span data-ttu-id="8b587-2623">Descrição</span><span class="sxs-lookup"><span data-stu-id="8b587-2623">Description</span></span> | <span data-ttu-id="8b587-2624">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="8b587-2624">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="8b587-2625">type</span><span class="sxs-lookup"><span data-stu-id="8b587-2625">type</span></span> |<span data-ttu-id="8b587-2626">tipo do conjunto de dados.</span><span class="sxs-lookup"><span data-stu-id="8b587-2626">type of the dataset.</span></span> <span data-ttu-id="8b587-2627">Deve ser definido como **WebTable**</span><span class="sxs-lookup"><span data-stu-id="8b587-2627">must be set to **WebTable**</span></span> |<span data-ttu-id="8b587-2628">Sim</span><span class="sxs-lookup"><span data-stu-id="8b587-2628">Yes</span></span> |
| <span data-ttu-id="8b587-2629">path</span><span class="sxs-lookup"><span data-stu-id="8b587-2629">path</span></span> |<span data-ttu-id="8b587-2630">Uma URL relativa para o recurso que contém a tabela.</span><span class="sxs-lookup"><span data-stu-id="8b587-2630">A relative URL to the resource that contains the table.</span></span> |<span data-ttu-id="8b587-2631">Não.</span><span class="sxs-lookup"><span data-stu-id="8b587-2631">No.</span></span> <span data-ttu-id="8b587-2632">Quando o caminho não for especificado, apenas a URL especificada na definição do serviço vinculado será usada.</span><span class="sxs-lookup"><span data-stu-id="8b587-2632">When path is not specified, only the URL specified in the linked service definition is used.</span></span> |
| <span data-ttu-id="8b587-2633">índice</span><span class="sxs-lookup"><span data-stu-id="8b587-2633">index</span></span> |<span data-ttu-id="8b587-2634">O índice da tabela no recurso.</span><span class="sxs-lookup"><span data-stu-id="8b587-2634">The index of the table in the resource.</span></span> <span data-ttu-id="8b587-2635">Confira a seção [Obter índice de uma tabela em uma página HTML](#get-index-of-a-table-in-an-html-page) a fim de ver as etapas para obter o índice de uma tabela em uma página HTML.</span><span class="sxs-lookup"><span data-stu-id="8b587-2635">See [Get index of a table in an HTML page](#get-index-of-a-table-in-an-html-page) section for steps to getting index of a table in an HTML page.</span></span> |<span data-ttu-id="8b587-2636">Sim</span><span class="sxs-lookup"><span data-stu-id="8b587-2636">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="8b587-2637">Exemplo</span><span class="sxs-lookup"><span data-stu-id="8b587-2637">Example</span></span>

```json
{
    "name": "WebTableInput",
    "properties": {
        "type": "WebTable",
        "linkedServiceName": "WebLinkedService",
        "typeProperties": {
            "index": 1,
            "path": "AFI's_100_Years...100_Movies"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

<span data-ttu-id="8b587-2638">Para obter mais informações, consulte o artigo [Conector da Tabela da Web](data-factory-web-table-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="8b587-2638">For more information, see [Web Table connector](data-factory-web-table-connector.md#dataset-properties) article.</span></span> 

### <a name="web-source-in-copy-activity"></a><span data-ttu-id="8b587-2639">Origem da Web na Atividade de Cópia</span><span class="sxs-lookup"><span data-stu-id="8b587-2639">Web Source in Copy Activity</span></span>
<span data-ttu-id="8b587-2640">Se você estiver copiando dados de uma tabela da web, defina o **source type** de atividade de cópia para **WebSource**.</span><span class="sxs-lookup"><span data-stu-id="8b587-2640">If you are copying data from a web table, set the **source type** of the copy activity to **WebSource**.</span></span> <span data-ttu-id="8b587-2641">Atualmente, quando a origem na atividade de cópia é do tipo **WebSource**, não há suporte para propriedades adicionais.</span><span class="sxs-lookup"><span data-stu-id="8b587-2641">Currently, when the source in copy activity is of type **WebSource**, no additional properties are supported.</span></span>

#### <a name="example"></a><span data-ttu-id="8b587-2642">Exemplo</span><span class="sxs-lookup"><span data-stu-id="8b587-2642">Example</span></span>

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "WebTableToAzureBlob",
            "description": "Copy from a Web table to an Azure blob",
            "type": "Copy",
            "inputs": [{
                "name": "WebTableInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "WebSource"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

<span data-ttu-id="8b587-2643">Para obter mais informações, consulte o artigo [Conector da Tabela da Web](data-factory-web-table-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="8b587-2643">For more information, see [Web Table connector](data-factory-web-table-connector.md#copy-activity-properties) article.</span></span> 

## <a name="compute-environments"></a><span data-ttu-id="8b587-2644">AMBIENTES DE COMPUTAÇÃO</span><span class="sxs-lookup"><span data-stu-id="8b587-2644">COMPUTE ENVIRONMENTS</span></span>
<span data-ttu-id="8b587-2645">A tabela a seguir lista os ambientes de computação com suporte do Data Factory e as atividades de transformação que podem ser executadas neles.</span><span class="sxs-lookup"><span data-stu-id="8b587-2645">The following table lists the compute environments supported by Data Factory and the transformation activities that can run on them.</span></span> <span data-ttu-id="8b587-2646">Clique no link para a computação a qual você está interessado em ver os esquemas JSON para o serviço vinculado para vinculá-lo a um data factory.</span><span class="sxs-lookup"><span data-stu-id="8b587-2646">Click the link for the compute you are interested in to see the JSON schemas for linked service to link it to a data factory.</span></span> 

| <span data-ttu-id="8b587-2647">Ambiente de computação</span><span class="sxs-lookup"><span data-stu-id="8b587-2647">Compute environment</span></span> | <span data-ttu-id="8b587-2648">Atividades</span><span class="sxs-lookup"><span data-stu-id="8b587-2648">Activities</span></span> |
| --- | --- |
| <span data-ttu-id="8b587-2649">[Cluster HDInsight sob demanda](#on-demand-azure-hdinsight-cluster) ou [seu próprio cluster HDInsight](#existing-azure-hdinsight-cluster)</span><span class="sxs-lookup"><span data-stu-id="8b587-2649">[On-demand HDInsight cluster](#on-demand-azure-hdinsight-cluster) or [your own HDInsight cluster](#existing-azure-hdinsight-cluster)</span></span> |<span data-ttu-id="8b587-2650">[Atividade personalizada de .NET](#net-custom-activity), [Atividade de Hive](#hdinsight-hive-activity), [Pig activity](#hdinsight-pig-activity, [Atividade de MapReduce](#hdinsight-mapreduce-activity), [Atividade de transmissão do Hadoop](#hdinsight-streaming-activityd), [Atividade do Spark](#hdinsight-spark-activity)</span><span class="sxs-lookup"><span data-stu-id="8b587-2650">[.NET custom activity](#net-custom-activity), [Hive activity](#hdinsight-hive-activity), [Pig activity](#hdinsight-pig-activity, [MapReduce activity](#hdinsight-mapreduce-activity), [Hadoop streaming activity](#hdinsight-streaming-activityd), [Spark activity](#hdinsight-spark-activity)</span></span> |
| [<span data-ttu-id="8b587-2651">Lote do Azure</span><span class="sxs-lookup"><span data-stu-id="8b587-2651">Azure Batch</span></span>](#azure-batch) |[<span data-ttu-id="8b587-2652">Atividade personalizada do .NET</span><span class="sxs-lookup"><span data-stu-id="8b587-2652">.NET custom activity</span></span>](#net-custom-activity) |
| <span data-ttu-id="8b587-2653">
            [Azure Machine Learning](#azure-machine-learning)</span><span class="sxs-lookup"><span data-stu-id="8b587-2653">[Azure Machine Learning](#azure-machine-learning)</span></span> | <span data-ttu-id="8b587-2654">[Atividade de Execução de Lote de Machine Learning](#machine-learning-batch-execution-activity), [Atividade de Atualização de Recursos de Machine Learning](#machine-learning-update-resource-activity)</span><span class="sxs-lookup"><span data-stu-id="8b587-2654">[Machine Learning Batch Execution Activity](#machine-learning-batch-execution-activity), [Machine Learning Update Resource Activity](#machine-learning-update-resource-activity)</span></span> |
| [<span data-ttu-id="8b587-2655">Análise Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="8b587-2655">Azure Data Lake Analytics</span></span>](#azure-data-lake-analytics) |[<span data-ttu-id="8b587-2656">U-SQL da Análise Data Lake</span><span class="sxs-lookup"><span data-stu-id="8b587-2656">Data Lake Analytics U-SQL</span></span>](#data-lake-analytics-u-sql-activity) |
| <span data-ttu-id="8b587-2657">[Banco de Dados SQL do Azure](#azure-sql-database-1), [SQL Data Warehouse do Azure](#azure-sql-data-warehouse-1), [SQL Server](#sql-server-1)</span><span class="sxs-lookup"><span data-stu-id="8b587-2657">[Azure SQL Database](#azure-sql-database-1), [Azure SQL Data Warehouse](#azure-sql-data-warehouse-1), [SQL Server](#sql-server-1)</span></span> |[<span data-ttu-id="8b587-2658">Procedimento armazenado</span><span class="sxs-lookup"><span data-stu-id="8b587-2658">Stored Procedure</span></span>](#stored-procedure-activity) |

## <a name="on-demand-azure-hdinsight-cluster"></a><span data-ttu-id="8b587-2659">Cluster HDInsight do Azure sob demanda</span><span class="sxs-lookup"><span data-stu-id="8b587-2659">On-demand Azure HDInsight cluster</span></span>
<span data-ttu-id="8b587-2660">O serviço Azure Data Factory pode criar automaticamente um cluster HDInsight sob demanda baseado em Windows/Linux para processar dados.</span><span class="sxs-lookup"><span data-stu-id="8b587-2660">The Azure Data Factory service can automatically create a Windows/Linux-based on-demand HDInsight cluster to process data.</span></span> <span data-ttu-id="8b587-2661">O cluster é criado na mesma região que a conta de armazenamento (propriedade linkedServiceName em JSON) associada ao cluster.</span><span class="sxs-lookup"><span data-stu-id="8b587-2661">The cluster is created in the same region as the storage account (linkedServiceName property in the JSON) associated with the cluster.</span></span> <span data-ttu-id="8b587-2662">Você pode executar as seguintes atividades de transformação nesse serviço vinculado: [atividade personalizada do .NET](#net-custom-activity), [atividade de Hive](#hdinsight-hive-activity), [Pig activity] (#hdinsight-pig-activity, [atividade MapReduce](#hdinsight-mapreduce-activity), [atividade de transmissão do Hadoop](#hdinsight-streaming-activityd), [atividade Spark](#hdinsight-spark-activity).</span><span class="sxs-lookup"><span data-stu-id="8b587-2662">You can run the following transformation activities on this linked service: [.NET custom activity](#net-custom-activity), [Hive activity](#hdinsight-hive-activity), [Pig activity](#hdinsight-pig-activity, [MapReduce activity](#hdinsight-mapreduce-activity), [Hadoop streaming activity](#hdinsight-streaming-activityd), [Spark activity](#hdinsight-spark-activity).</span></span> 

### <a name="linked-service"></a><span data-ttu-id="8b587-2663">Serviço vinculado</span><span class="sxs-lookup"><span data-stu-id="8b587-2663">Linked service</span></span> 
<span data-ttu-id="8b587-2664">A tabela a seguir fornece as descrições das propriedades usadas na definição de JSON do Azure de um serviço vinculado do HDInsight sob demanda.</span><span class="sxs-lookup"><span data-stu-id="8b587-2664">The following table provides descriptions for the properties used in the Azure JSON definition of an on-demand HDInsight linked service.</span></span>

| <span data-ttu-id="8b587-2665">Propriedade</span><span class="sxs-lookup"><span data-stu-id="8b587-2665">Property</span></span> | <span data-ttu-id="8b587-2666">Descrição</span><span class="sxs-lookup"><span data-stu-id="8b587-2666">Description</span></span> | <span data-ttu-id="8b587-2667">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="8b587-2667">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8b587-2668">type</span><span class="sxs-lookup"><span data-stu-id="8b587-2668">type</span></span> |<span data-ttu-id="8b587-2669">A propriedade de tipo deve ser configurada como **HDInsightOnDemand**.</span><span class="sxs-lookup"><span data-stu-id="8b587-2669">The type property should be set to **HDInsightOnDemand**.</span></span> |<span data-ttu-id="8b587-2670">Sim</span><span class="sxs-lookup"><span data-stu-id="8b587-2670">Yes</span></span> |
| <span data-ttu-id="8b587-2671">clusterSize</span><span class="sxs-lookup"><span data-stu-id="8b587-2671">clusterSize</span></span> |<span data-ttu-id="8b587-2672">Número de nós de trabalho/dados no cluster.</span><span class="sxs-lookup"><span data-stu-id="8b587-2672">Number of worker/data nodes in the cluster.</span></span> <span data-ttu-id="8b587-2673">O cluster HDInsight é criado com 2 nós principais juntamente com o número de nós de trabalho que você especifica para esta propriedade.</span><span class="sxs-lookup"><span data-stu-id="8b587-2673">The HDInsight cluster is created with 2 head nodes along with the number of worker nodes you specify for this property.</span></span> <span data-ttu-id="8b587-2674">Os nós são do tamanho Standard_D3 que tem 4 núcleos; portanto, um cluster de 4 nós de trabalho usa 24 núcleos (4\*4 = 16 núcleos para nós de trabalho + 2\*4 = 8 núcleos para nós de cabeçalho).</span><span class="sxs-lookup"><span data-stu-id="8b587-2674">The nodes are of size Standard_D3 that has 4 cores, so a 4 worker node cluster takes 24 cores (4\*4 = 16 cores for worker nodes, plus 2\*4 = 8 cores for head nodes).</span></span> <span data-ttu-id="8b587-2675">Veja [Criar clusters do Hadoop baseados em Linux no HDInsight](../hdinsight/hdinsight-hadoop-provision-linux-clusters.md) para obter detalhes sobre a camada Standard_D3.</span><span class="sxs-lookup"><span data-stu-id="8b587-2675">See [Create Linux-based Hadoop clusters in HDInsight](../hdinsight/hdinsight-hadoop-provision-linux-clusters.md) for details about the Standard_D3 tier.</span></span> |<span data-ttu-id="8b587-2676">Sim</span><span class="sxs-lookup"><span data-stu-id="8b587-2676">Yes</span></span> |
| <span data-ttu-id="8b587-2677">timeToLive</span><span class="sxs-lookup"><span data-stu-id="8b587-2677">timetolive</span></span> |<span data-ttu-id="8b587-2678">O tempo ocioso permitido para o cluster HDInsight sob demanda.</span><span class="sxs-lookup"><span data-stu-id="8b587-2678">The allowed idle time for the on-demand HDInsight cluster.</span></span> <span data-ttu-id="8b587-2679">Especifica quanto tempo o cluster HDInsight sob demanda permanece ativo após a conclusão de uma atividade executada se não há nenhum outro trabalho ativo no cluster.</span><span class="sxs-lookup"><span data-stu-id="8b587-2679">Specifies how long the on-demand HDInsight cluster stays alive after completion of an activity run if there are no other active jobs in the cluster.</span></span><br/><br/><span data-ttu-id="8b587-2680">Por exemplo, se uma execução de atividade demora 6 minutos e o timetolive é definido como 5 minutos, o cluster fica ativo durante 5 minutos após a execução de 6 minutos de execução da atividade.</span><span class="sxs-lookup"><span data-stu-id="8b587-2680">For example, if an activity run takes 6 minutes and timetolive is set to 5 minutes, the cluster stays alive for 5 minutes after the 6 minutes of processing the activity run.</span></span> <span data-ttu-id="8b587-2681">Se outra atividade é executada com a janela de 6 minutos, ela é processada pelo mesmo cluster.</span><span class="sxs-lookup"><span data-stu-id="8b587-2681">If another activity run is executed with the 6 minutes window, it is processed by the same cluster.</span></span><br/><br/><span data-ttu-id="8b587-2682">A criação de um cluster HDInsight sob demanda é uma operação cara (pode demorar um pouco) e, portanto, use essa configuração conforme o necessário para melhorar o desempenho de um data factory com a reutilização de um cluster HDInsight sob demanda.</span><span class="sxs-lookup"><span data-stu-id="8b587-2682">Creating an on-demand HDInsight cluster is an expensive operation (could take a while), so use this setting as needed to improve performance of a data factory by reusing an on-demand HDInsight cluster.</span></span><br/><br/><span data-ttu-id="8b587-2683">Se você definir o valor de timetolive como 0, o cluster é excluído assim que a atividade executada é processada.</span><span class="sxs-lookup"><span data-stu-id="8b587-2683">If you set timetolive value to 0, the cluster is deleted as soon as the activity run in processed.</span></span> <span data-ttu-id="8b587-2684">Por outro lado, se você definir um valor alto, o cluster pode permanecer ocioso desnecessariamente resultando em altos custos.</span><span class="sxs-lookup"><span data-stu-id="8b587-2684">On the other hand, if you set a high value, the cluster may stay idle unnecessarily resulting in high costs.</span></span> <span data-ttu-id="8b587-2685">Portanto, é importante que você defina o valor apropriado com base em suas necessidades.</span><span class="sxs-lookup"><span data-stu-id="8b587-2685">Therefore, it is important that you set the appropriate value based on your needs.</span></span><br/><br/><span data-ttu-id="8b587-2686">Vários pipelines podem compartilhar a mesma instância do cluster do HDInsight sob demanda se o valor da propriedade timetolive estiver definido corretamente</span><span class="sxs-lookup"><span data-stu-id="8b587-2686">Multiple pipelines can share the same instance of the on-demand HDInsight cluster if the timetolive property value is appropriately set</span></span> |<span data-ttu-id="8b587-2687">Sim</span><span class="sxs-lookup"><span data-stu-id="8b587-2687">Yes</span></span> |
| <span data-ttu-id="8b587-2688">version</span><span class="sxs-lookup"><span data-stu-id="8b587-2688">version</span></span> |<span data-ttu-id="8b587-2689">Versão do cluster HDInsight</span><span class="sxs-lookup"><span data-stu-id="8b587-2689">Version of the HDInsight cluster.</span></span> <span data-ttu-id="8b587-2690">Para obter detalhes, confira [Versões com suporte do HDInsight no Azure Data Factory](data-factory-compute-linked-services.md#supported-hdinsight-versions-in-azure-data-factory).</span><span class="sxs-lookup"><span data-stu-id="8b587-2690">For details, see [supported HDInsight versions in Azure Data Factory](data-factory-compute-linked-services.md#supported-hdinsight-versions-in-azure-data-factory).</span></span> |<span data-ttu-id="8b587-2691">Não</span><span class="sxs-lookup"><span data-stu-id="8b587-2691">No</span></span> |
| <span data-ttu-id="8b587-2692">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="8b587-2692">linkedServiceName</span></span> |<span data-ttu-id="8b587-2693">Serviço vinculado do Armazenamento do Azure a ser usado pelo cluster sob demanda para armazenar e processar dados.</span><span class="sxs-lookup"><span data-stu-id="8b587-2693">Azure Storage linked service to be used by the on-demand cluster for storing and processing data.</span></span> <p><span data-ttu-id="8b587-2694">Atualmente, não é possível criar um cluster HDInsight sob demanda que use um Azure Data Lake Store como o armazenamento.</span><span class="sxs-lookup"><span data-stu-id="8b587-2694">Currently, you cannot create an on-demand HDInsight cluster that uses an Azure Data Lake Store as the storage.</span></span> <span data-ttu-id="8b587-2695">Se você quiser armazenar os dados resultantes do processamento do HDInsight em um Azure Data Lake Store, use uma Atividade de Cópia para copiar os dados do Armazenamento de Blobs do Azure para o Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="8b587-2695">If you want to store the result data from HDInsight processing in an Azure Data Lake Store, use a Copy Activity to copy the data from the Azure Blob Storage to the Azure Data Lake Store.</span></span></p>  | <span data-ttu-id="8b587-2696">Sim</span><span class="sxs-lookup"><span data-stu-id="8b587-2696">Yes</span></span> |
| <span data-ttu-id="8b587-2697">additionalLinkedServiceNames</span><span class="sxs-lookup"><span data-stu-id="8b587-2697">additionalLinkedServiceNames</span></span> |<span data-ttu-id="8b587-2698">Especifica as contas de armazenamento adicionais para o serviço vinculado do HDInsight para que o serviço do Data Factory possa registrá-los em seu nome.</span><span class="sxs-lookup"><span data-stu-id="8b587-2698">Specifies additional storage accounts for the HDInsight linked service so that the Data Factory service can register them on your behalf.</span></span> |<span data-ttu-id="8b587-2699">Não</span><span class="sxs-lookup"><span data-stu-id="8b587-2699">No</span></span> |
| <span data-ttu-id="8b587-2700">osType</span><span class="sxs-lookup"><span data-stu-id="8b587-2700">osType</span></span> |<span data-ttu-id="8b587-2701">Tipo do sistema operacional.</span><span class="sxs-lookup"><span data-stu-id="8b587-2701">Type of operating system.</span></span> <span data-ttu-id="8b587-2702">Valores permitidos são: Windows (padrão) e Linux</span><span class="sxs-lookup"><span data-stu-id="8b587-2702">Allowed values are: Windows (default) and Linux</span></span> |<span data-ttu-id="8b587-2703">Não</span><span class="sxs-lookup"><span data-stu-id="8b587-2703">No</span></span> |
| <span data-ttu-id="8b587-2704">hcatalogLinkedServiceName</span><span class="sxs-lookup"><span data-stu-id="8b587-2704">hcatalogLinkedServiceName</span></span> |<span data-ttu-id="8b587-2705">O nome do serviço vinculado do SQL Azure que aponta para o banco de dados HCatalog.</span><span class="sxs-lookup"><span data-stu-id="8b587-2705">The name of Azure SQL linked service that point to the HCatalog database.</span></span> <span data-ttu-id="8b587-2706">O cluster HDInsight sob demanda é criado usando o banco de dados SQL do Azure como o metastore.</span><span class="sxs-lookup"><span data-stu-id="8b587-2706">The on-demand HDInsight cluster is created by using the Azure SQL database as the metastore.</span></span> |<span data-ttu-id="8b587-2707">Não</span><span class="sxs-lookup"><span data-stu-id="8b587-2707">No</span></span> |

### <a name="json-example"></a><span data-ttu-id="8b587-2708">Exemplo de JSON</span><span class="sxs-lookup"><span data-stu-id="8b587-2708">JSON example</span></span>
<span data-ttu-id="8b587-2709">O JSON a seguir define um serviço vinculado HDInsight sob demanda baseado em Linux.</span><span class="sxs-lookup"><span data-stu-id="8b587-2709">The following JSON defines a Linux-based on-demand HDInsight linked service.</span></span> <span data-ttu-id="8b587-2710">O serviço Data Factory cria automaticamente um cluster HDInsight **baseado em Linux** ao processar uma fatia de dados.</span><span class="sxs-lookup"><span data-stu-id="8b587-2710">The Data Factory service automatically creates a **Linux-based** HDInsight cluster when processing a data slice.</span></span> 

```json
{
    "name": "HDInsightOnDemandLinkedService",
    "properties": {
        "type": "HDInsightOnDemand",
        "typeProperties": {
            "version": "3.5",
            "clusterSize": 1,
            "timeToLive": "00:05:00",
            "osType": "Linux",
            "linkedServiceName": "StorageLinkedService"
        }
    }
}
```

<span data-ttu-id="8b587-2711">Para obter mais informações, consulte o artigo [Serviços vinculados de computação](data-factory-compute-linked-services.md).</span><span class="sxs-lookup"><span data-stu-id="8b587-2711">For more information, see [Compute linked services](data-factory-compute-linked-services.md) article.</span></span> 

## <a name="existing-azure-hdinsight-cluster"></a><span data-ttu-id="8b587-2712">Cluster Azure HDInsight existente</span><span class="sxs-lookup"><span data-stu-id="8b587-2712">Existing Azure HDInsight cluster</span></span>
<span data-ttu-id="8b587-2713">Você pode criar um serviço vinculado Azure HDInsight para registrar seu próprio cluster HDInsight com o Data Factory.</span><span class="sxs-lookup"><span data-stu-id="8b587-2713">You can create an Azure HDInsight linked service to register your own HDInsight cluster with Data Factory.</span></span> <span data-ttu-id="8b587-2714">Você pode executar as seguintes atividades de transformação de dados nesse serviço vinculado: [atividade personalizada do .NET](#net-custom-activity), [atividade de Hive](#hdinsight-hive-activity), [Pig activity] (#hdinsight-pig-activity, [atividade MapReduce](#hdinsight-mapreduce-activity), [atividade de transmissão do Hadoop](#hdinsight-streaming-activityd), [atividade Spark](#hdinsight-spark-activity).</span><span class="sxs-lookup"><span data-stu-id="8b587-2714">You can run the following data transformation activities on this linked service: [.NET custom activity](#net-custom-activity), [Hive activity](#hdinsight-hive-activity), [Pig activity](#hdinsight-pig-activity, [MapReduce activity](#hdinsight-mapreduce-activity), [Hadoop streaming activity](#hdinsight-streaming-activityd), [Spark activity](#hdinsight-spark-activity).</span></span> 

### <a name="linked-service"></a><span data-ttu-id="8b587-2715">Serviço vinculado</span><span class="sxs-lookup"><span data-stu-id="8b587-2715">Linked service</span></span>
<span data-ttu-id="8b587-2716">A tabela a seguir fornece as descrições das propriedades usadas na definição de JSON do Azure de um serviço vinculado do Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="8b587-2716">The following table provides descriptions for the properties used in the Azure JSON definition of an Azure HDInsight linked service.</span></span>

| <span data-ttu-id="8b587-2717">Propriedade</span><span class="sxs-lookup"><span data-stu-id="8b587-2717">Property</span></span> | <span data-ttu-id="8b587-2718">Descrição</span><span class="sxs-lookup"><span data-stu-id="8b587-2718">Description</span></span> | <span data-ttu-id="8b587-2719">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="8b587-2719">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8b587-2720">type</span><span class="sxs-lookup"><span data-stu-id="8b587-2720">type</span></span> |<span data-ttu-id="8b587-2721">A propriedade de tipo deve ser configurada como **HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="8b587-2721">The type property should be set to **HDInsight**.</span></span> |<span data-ttu-id="8b587-2722">Sim</span><span class="sxs-lookup"><span data-stu-id="8b587-2722">Yes</span></span> |
| <span data-ttu-id="8b587-2723">clusterUri</span><span class="sxs-lookup"><span data-stu-id="8b587-2723">clusterUri</span></span> |<span data-ttu-id="8b587-2724">A URI do cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="8b587-2724">The URI of the HDInsight cluster.</span></span> |<span data-ttu-id="8b587-2725">Sim</span><span class="sxs-lookup"><span data-stu-id="8b587-2725">Yes</span></span> |
| <span data-ttu-id="8b587-2726">Nome de Usuário</span><span class="sxs-lookup"><span data-stu-id="8b587-2726">username</span></span> |<span data-ttu-id="8b587-2727">Especifique o nome do usuário a ser usado para se conectar a um cluster HDInsight existente.</span><span class="sxs-lookup"><span data-stu-id="8b587-2727">Specify the name of the user to be used to connect to an existing HDInsight cluster.</span></span> |<span data-ttu-id="8b587-2728">Sim</span><span class="sxs-lookup"><span data-stu-id="8b587-2728">Yes</span></span> |
| <span data-ttu-id="8b587-2729">Senha</span><span class="sxs-lookup"><span data-stu-id="8b587-2729">password</span></span> |<span data-ttu-id="8b587-2730">Especifique a senha para a conta de usuário.</span><span class="sxs-lookup"><span data-stu-id="8b587-2730">Specify password for the user account.</span></span> |<span data-ttu-id="8b587-2731">Sim</span><span class="sxs-lookup"><span data-stu-id="8b587-2731">Yes</span></span> |
| <span data-ttu-id="8b587-2732">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="8b587-2732">linkedServiceName</span></span> | <span data-ttu-id="8b587-2733">Nome do serviço vinculado do Armazenamento do Azure que faz referência ao Armazenamento de Blobs usado pelo cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="8b587-2733">Name of the Azure Storage linked service that refers to the Azure blob storage used by the HDInsight cluster.</span></span> <p><span data-ttu-id="8b587-2734">No momento, você não pode especificar um serviço vinculado do Azure Data Lake Store para essa propriedade.</span><span class="sxs-lookup"><span data-stu-id="8b587-2734">Currently, you cannot specify an Azure Data Lake Store linked service for this property.</span></span> <span data-ttu-id="8b587-2735">Você pode acessar dados no Azure Data Lake Store usando scripts Hive/Pig se o cluster HDInsight tiver acesso ao Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="8b587-2735">You may access data in the Azure Data Lake Store from Hive/Pig scripts if the HDInsight cluster has access to the Data Lake Store.</span></span> </p>  |<span data-ttu-id="8b587-2736">Sim</span><span class="sxs-lookup"><span data-stu-id="8b587-2736">Yes</span></span> |

<span data-ttu-id="8b587-2737">Para conferir as versões de clusters HDInsight com suporte, veja [Versões do HDInsight com suporte](data-factory-compute-linked-services.md#supported-hdinsight-versions-in-azure-data-factory).</span><span class="sxs-lookup"><span data-stu-id="8b587-2737">For versions of HDInsight clusters supported, see [supported HDInsight versions](data-factory-compute-linked-services.md#supported-hdinsight-versions-in-azure-data-factory).</span></span> 

#### <a name="json-example"></a><span data-ttu-id="8b587-2738">Exemplo de JSON</span><span class="sxs-lookup"><span data-stu-id="8b587-2738">JSON example</span></span>

```json
{
    "name": "HDInsightLinkedService",
    "properties": {
        "type": "HDInsight",
        "typeProperties": {
            "clusterUri": " https://<hdinsightclustername>.azurehdinsight.net/",
            "userName": "admin",
            "password": "<password>",
            "linkedServiceName": "MyHDInsightStoragelinkedService"
        }
    }
}
```

## <a name="azure-batch"></a><span data-ttu-id="8b587-2739">Lote do Azure</span><span class="sxs-lookup"><span data-stu-id="8b587-2739">Azure Batch</span></span>
<span data-ttu-id="8b587-2740">Você pode criar um serviço vinculado de Lote do Azure para registrar um pool de lote de máquinas virtuais (VMs) com uma fábrica de dados.</span><span class="sxs-lookup"><span data-stu-id="8b587-2740">You can create an Azure Batch linked service to register a Batch pool of virtual machines (VMs) with a data factory.</span></span> <span data-ttu-id="8b587-2741">Você pode executar atividades personalizadas do .NET usando o Lote do Azure ou o Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="8b587-2741">You can run .NET custom activities using either Azure Batch or Azure HDInsight.</span></span> <span data-ttu-id="8b587-2742">Você pode executar uma [atividade personalizada do .NET](#net-custom-activity) neste serviço vinculado.</span><span class="sxs-lookup"><span data-stu-id="8b587-2742">You can run a [.NET custom activity](#net-custom-activity) on this linked service.</span></span> 

### <a name="linked-service"></a><span data-ttu-id="8b587-2743">Serviço vinculado</span><span class="sxs-lookup"><span data-stu-id="8b587-2743">Linked service</span></span>
<span data-ttu-id="8b587-2744">A tabela a seguir fornece as descrições das propriedades usadas na definição de JSON do Azure de um serviço vinculado do Lote do Azure.</span><span class="sxs-lookup"><span data-stu-id="8b587-2744">The following table provides descriptions for the properties used in the Azure JSON definition of an Azure Batch linked service.</span></span>

| <span data-ttu-id="8b587-2745">Propriedade</span><span class="sxs-lookup"><span data-stu-id="8b587-2745">Property</span></span> | <span data-ttu-id="8b587-2746">Descrição</span><span class="sxs-lookup"><span data-stu-id="8b587-2746">Description</span></span> | <span data-ttu-id="8b587-2747">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="8b587-2747">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8b587-2748">type</span><span class="sxs-lookup"><span data-stu-id="8b587-2748">type</span></span> |<span data-ttu-id="8b587-2749">A propriedade de tipo deve ser definida como **AzureBatch**.</span><span class="sxs-lookup"><span data-stu-id="8b587-2749">The type property should be set to **AzureBatch**.</span></span> |<span data-ttu-id="8b587-2750">Sim</span><span class="sxs-lookup"><span data-stu-id="8b587-2750">Yes</span></span> |
| <span data-ttu-id="8b587-2751">accountName</span><span class="sxs-lookup"><span data-stu-id="8b587-2751">accountName</span></span> |<span data-ttu-id="8b587-2752">Nome da conta do Lote do Azure.</span><span class="sxs-lookup"><span data-stu-id="8b587-2752">Name of the Azure Batch account.</span></span> |<span data-ttu-id="8b587-2753">Sim</span><span class="sxs-lookup"><span data-stu-id="8b587-2753">Yes</span></span> |
| <span data-ttu-id="8b587-2754">accessKey</span><span class="sxs-lookup"><span data-stu-id="8b587-2754">accessKey</span></span> |<span data-ttu-id="8b587-2755">Tecla de acesso para a conta do Lote do Azure.</span><span class="sxs-lookup"><span data-stu-id="8b587-2755">Access key for the Azure Batch account.</span></span> |<span data-ttu-id="8b587-2756">Sim</span><span class="sxs-lookup"><span data-stu-id="8b587-2756">Yes</span></span> |
| <span data-ttu-id="8b587-2757">poolName</span><span class="sxs-lookup"><span data-stu-id="8b587-2757">poolName</span></span> |<span data-ttu-id="8b587-2758">Nome do pool de máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="8b587-2758">Name of the pool of virtual machines.</span></span> |<span data-ttu-id="8b587-2759">Sim</span><span class="sxs-lookup"><span data-stu-id="8b587-2759">Yes</span></span> |
| <span data-ttu-id="8b587-2760">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="8b587-2760">linkedServiceName</span></span> |<span data-ttu-id="8b587-2761">Nome do serviço vinculado do Armazenamento do Azure associado ao serviço vinculado de Lote do Azure.</span><span class="sxs-lookup"><span data-stu-id="8b587-2761">Name of the Azure Storage linked service associated with this Azure Batch linked service.</span></span> <span data-ttu-id="8b587-2762">Esse serviço vinculado é usado para arquivos de teste necessários para executar a atividade e armazenar os logs de execução da atividade.</span><span class="sxs-lookup"><span data-stu-id="8b587-2762">This linked service is used for staging files required to run the activity and storing the activity execution logs.</span></span> |<span data-ttu-id="8b587-2763">Sim</span><span class="sxs-lookup"><span data-stu-id="8b587-2763">Yes</span></span> |


#### <a name="json-example"></a><span data-ttu-id="8b587-2764">Exemplo de JSON</span><span class="sxs-lookup"><span data-stu-id="8b587-2764">JSON example</span></span>

```json
{
    "name": "AzureBatchLinkedService",
    "properties": {
        "type": "AzureBatch",
        "typeProperties": {
            "accountName": "<Azure Batch account name>",
            "accessKey": "<Azure Batch account key>",
            "poolName": "<Azure Batch pool name>",
            "linkedServiceName": "<Specify associated storage linked service reference here>"
        }
    }
}
```

## <a name="azure-machine-learning"></a><span data-ttu-id="8b587-2765">Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="8b587-2765">Azure Machine Learning</span></span>
<span data-ttu-id="8b587-2766">Criar um serviço vinculado do Azure Machine Learning para registrar um ponto de extremidade de pontuação do lote de Machine Learning com um data factory.</span><span class="sxs-lookup"><span data-stu-id="8b587-2766">You create an Azure Machine Learning linked service to register a Machine Learning batch scoring endpoint with a data factory.</span></span> <span data-ttu-id="8b587-2767">Duas atividades de transformação de dados podem ser executadas neste serviço vinculado: [Atividade de Execução de Lote de Machine Learning](#machine-learning-batch-execution-activity), [Atividade de Atualização de Recursos de Machine Learning](#machine-learning-update-resource-activity).</span><span class="sxs-lookup"><span data-stu-id="8b587-2767">Two data transformation activities that can run on this linked service: [Machine Learning Batch Execution Activity](#machine-learning-batch-execution-activity), [Machine Learning Update Resource Activity](#machine-learning-update-resource-activity).</span></span> 

### <a name="linked-service"></a><span data-ttu-id="8b587-2768">Serviço vinculado</span><span class="sxs-lookup"><span data-stu-id="8b587-2768">Linked service</span></span>
<span data-ttu-id="8b587-2769">A tabela a seguir fornece as descrições das propriedades usadas na definição de JSON do Azure de um serviço vinculado do Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="8b587-2769">The following table provides descriptions for the properties used in the Azure JSON definition of an Azure Machine Learning linked service.</span></span>

| <span data-ttu-id="8b587-2770">Propriedade</span><span class="sxs-lookup"><span data-stu-id="8b587-2770">Property</span></span> | <span data-ttu-id="8b587-2771">Descrição</span><span class="sxs-lookup"><span data-stu-id="8b587-2771">Description</span></span> | <span data-ttu-id="8b587-2772">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="8b587-2772">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8b587-2773">type</span><span class="sxs-lookup"><span data-stu-id="8b587-2773">Type</span></span> |<span data-ttu-id="8b587-2774">A propriedade de tipo deve ser configurada como **AzureML**.</span><span class="sxs-lookup"><span data-stu-id="8b587-2774">The type property should be set to: **AzureML**.</span></span> |<span data-ttu-id="8b587-2775">Sim</span><span class="sxs-lookup"><span data-stu-id="8b587-2775">Yes</span></span> |
| <span data-ttu-id="8b587-2776">mlEndpoint</span><span class="sxs-lookup"><span data-stu-id="8b587-2776">mlEndpoint</span></span> |<span data-ttu-id="8b587-2777">A URL de pontuação do lote.</span><span class="sxs-lookup"><span data-stu-id="8b587-2777">The batch scoring URL.</span></span> |<span data-ttu-id="8b587-2778">Sim</span><span class="sxs-lookup"><span data-stu-id="8b587-2778">Yes</span></span> |
| <span data-ttu-id="8b587-2779">apiKey</span><span class="sxs-lookup"><span data-stu-id="8b587-2779">apiKey</span></span> |<span data-ttu-id="8b587-2780">A API do modelo de espaço de trabalho publicada.</span><span class="sxs-lookup"><span data-stu-id="8b587-2780">The published workspace model’s API.</span></span> |<span data-ttu-id="8b587-2781">Sim</span><span class="sxs-lookup"><span data-stu-id="8b587-2781">Yes</span></span> |

#### <a name="json-example"></a><span data-ttu-id="8b587-2782">Exemplo de JSON</span><span class="sxs-lookup"><span data-stu-id="8b587-2782">JSON example</span></span>

```json
{
    "name": "AzureMLLinkedService",
    "properties": {
        "type": "AzureML",
        "typeProperties": {
            "mlEndpoint": "https://[batch scoring endpoint]/jobs",
            "apiKey": "<apikey>"
        }
    }
}
```

## <a name="azure-data-lake-analytics"></a><span data-ttu-id="8b587-2783">Análise Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="8b587-2783">Azure Data Lake Analytics</span></span>
<span data-ttu-id="8b587-2784">Você cria um serviço vinculado da **Análise Azure Data Lake** para vincular um serviço de computação da Análise do Azure Data Lake a um Azure Data Factory antes de usar a atividade do [U-SQL da Análise Data Lake](data-factory-usql-activity.md) em um pipeline.</span><span class="sxs-lookup"><span data-stu-id="8b587-2784">You create an **Azure Data Lake Analytics** linked service to link an Azure Data Lake Analytics compute service to an Azure data factory before using the [Data Lake Analytics U-SQL activity](data-factory-usql-activity.md) in a pipeline.</span></span>

### <a name="linked-service"></a><span data-ttu-id="8b587-2785">Serviço vinculado</span><span class="sxs-lookup"><span data-stu-id="8b587-2785">Linked service</span></span>

<span data-ttu-id="8b587-2786">A tabela a seguir fornece as descrições das propriedades usadas na definição de JSON de um serviço vinculado do Azure Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="8b587-2786">The following table provides descriptions for the properties used in the JSON definition of an Azure Data Lake Analytics linked service.</span></span> 

| <span data-ttu-id="8b587-2787">Propriedade</span><span class="sxs-lookup"><span data-stu-id="8b587-2787">Property</span></span> | <span data-ttu-id="8b587-2788">Descrição</span><span class="sxs-lookup"><span data-stu-id="8b587-2788">Description</span></span> | <span data-ttu-id="8b587-2789">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="8b587-2789">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8b587-2790">Tipo</span><span class="sxs-lookup"><span data-stu-id="8b587-2790">Type</span></span> |<span data-ttu-id="8b587-2791">A propriedade de tipo deve ser definida como: **AzureDataLakeAnalytics**.</span><span class="sxs-lookup"><span data-stu-id="8b587-2791">The type property should be set to: **AzureDataLakeAnalytics**.</span></span> |<span data-ttu-id="8b587-2792">Sim</span><span class="sxs-lookup"><span data-stu-id="8b587-2792">Yes</span></span> |
| <span data-ttu-id="8b587-2793">accountName</span><span class="sxs-lookup"><span data-stu-id="8b587-2793">accountName</span></span> |<span data-ttu-id="8b587-2794">Nome da conta da Análise Azure Data Lake.</span><span class="sxs-lookup"><span data-stu-id="8b587-2794">Azure Data Lake Analytics Account Name.</span></span> |<span data-ttu-id="8b587-2795">Sim</span><span class="sxs-lookup"><span data-stu-id="8b587-2795">Yes</span></span> |
| <span data-ttu-id="8b587-2796">dataLakeAnalyticsUri</span><span class="sxs-lookup"><span data-stu-id="8b587-2796">dataLakeAnalyticsUri</span></span> |<span data-ttu-id="8b587-2797">URI da Análise Azure Data Lake.</span><span class="sxs-lookup"><span data-stu-id="8b587-2797">Azure Data Lake Analytics URI.</span></span> |<span data-ttu-id="8b587-2798">Não</span><span class="sxs-lookup"><span data-stu-id="8b587-2798">No</span></span> |
| <span data-ttu-id="8b587-2799">autorização</span><span class="sxs-lookup"><span data-stu-id="8b587-2799">authorization</span></span> |<span data-ttu-id="8b587-2800">O código de autorização é recuperado automaticamente depois de clicar no botão **Autorizar** no Editor do Data Factory e concluir o logon OAuth.</span><span class="sxs-lookup"><span data-stu-id="8b587-2800">Authorization code is automatically retrieved after clicking **Authorize** button in the Data Factory Editor and completing the OAuth login.</span></span> |<span data-ttu-id="8b587-2801">Sim</span><span class="sxs-lookup"><span data-stu-id="8b587-2801">Yes</span></span> |
| <span data-ttu-id="8b587-2802">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="8b587-2802">subscriptionId</span></span> |<span data-ttu-id="8b587-2803">Id de assinatura do Azure</span><span class="sxs-lookup"><span data-stu-id="8b587-2803">Azure subscription id</span></span> |<span data-ttu-id="8b587-2804">Não (se não for especificado, a assinatura do Data Factory é usada).</span><span class="sxs-lookup"><span data-stu-id="8b587-2804">No (If not specified, subscription of the data factory is used).</span></span> |
| <span data-ttu-id="8b587-2805">resourceGroupName</span><span class="sxs-lookup"><span data-stu-id="8b587-2805">resourceGroupName</span></span> |<span data-ttu-id="8b587-2806">Nome do grupo de recursos do Azure</span><span class="sxs-lookup"><span data-stu-id="8b587-2806">Azure resource group name</span></span> |<span data-ttu-id="8b587-2807">Não (se não for especificado, o grupo de recursos do Data Factory é usado).</span><span class="sxs-lookup"><span data-stu-id="8b587-2807">No (If not specified, resource group of the data factory is used).</span></span> |
| <span data-ttu-id="8b587-2808">sessionId</span><span class="sxs-lookup"><span data-stu-id="8b587-2808">sessionId</span></span> |<span data-ttu-id="8b587-2809">ID da sessão de autorização OAuth.</span><span class="sxs-lookup"><span data-stu-id="8b587-2809">session id from the OAuth authorization session.</span></span> <span data-ttu-id="8b587-2810">Cada ID da sessão é exclusiva e pode ser usado somente uma vez.</span><span class="sxs-lookup"><span data-stu-id="8b587-2810">Each session id is unique and may only be used once.</span></span> <span data-ttu-id="8b587-2811">A ID é gerada automaticamente quando o Editor do Data Factory é usado.</span><span class="sxs-lookup"><span data-stu-id="8b587-2811">When you use the Data Factory Editor, this ID is auto-generated.</span></span> |<span data-ttu-id="8b587-2812">Sim</span><span class="sxs-lookup"><span data-stu-id="8b587-2812">Yes</span></span> |


#### <a name="json-example"></a><span data-ttu-id="8b587-2813">Exemplo de JSON</span><span class="sxs-lookup"><span data-stu-id="8b587-2813">JSON example</span></span>
<span data-ttu-id="8b587-2814">O exemplo a seguir fornece uma definição de JSON para um serviço vinculado da Análise Azure Data Lake.</span><span class="sxs-lookup"><span data-stu-id="8b587-2814">The following example provides JSON definition for an Azure Data Lake Analytics linked service.</span></span>

```json
{
    "name": "AzureDataLakeAnalyticsLinkedService",
    "properties": {
        "type": "AzureDataLakeAnalytics",
        "typeProperties": {
            "accountName": "<account name>",
            "dataLakeAnalyticsUri": "datalakeanalyticscompute.net",
            "authorization": "<authcode>",
            "sessionId": "<session ID>",
            "subscriptionId": "<subscription id>",
            "resourceGroupName": "<resource group name>"
        }
    }
}
```

## <a name="azure-sql-database"></a><span data-ttu-id="8b587-2815">Banco de Dados SQL do Azure</span><span class="sxs-lookup"><span data-stu-id="8b587-2815">Azure SQL Database</span></span>
<span data-ttu-id="8b587-2816">Você pode criar um serviço vinculado SQL do Azure e usá-lo com a [Atividade de Procedimento Armazenado](#stored-procedure-activity) para invocar um procedimento armazenado de um pipeline do Data Factory.</span><span class="sxs-lookup"><span data-stu-id="8b587-2816">You create an Azure SQL linked service and use it with the [Stored Procedure Activity](#stored-procedure-activity) to invoke a stored procedure from a Data Factory pipeline.</span></span> 

### <a name="linked-service"></a><span data-ttu-id="8b587-2817">Serviço vinculado</span><span class="sxs-lookup"><span data-stu-id="8b587-2817">Linked service</span></span>
<span data-ttu-id="8b587-2818">Para definir um serviço vinculado do Banco de Dados SQL do Azure, defina o **type** do serviço vinculado para **AzureSqlDatabase** e especifique as propriedades a seguir na seção **typeProperties**:</span><span class="sxs-lookup"><span data-stu-id="8b587-2818">To define an Azure SQL Database linked service, set the **type** of the linked service to **AzureSqlDatabase**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="8b587-2819">Propriedade</span><span class="sxs-lookup"><span data-stu-id="8b587-2819">Property</span></span> | <span data-ttu-id="8b587-2820">Descrição</span><span class="sxs-lookup"><span data-stu-id="8b587-2820">Description</span></span> | <span data-ttu-id="8b587-2821">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="8b587-2821">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8b587-2822">connectionString</span><span class="sxs-lookup"><span data-stu-id="8b587-2822">connectionString</span></span> |<span data-ttu-id="8b587-2823">Especifique as informações necessárias para se conectar à instância do Banco de Dados SQL Azure para a propriedade connectionString.</span><span class="sxs-lookup"><span data-stu-id="8b587-2823">Specify information needed to connect to the Azure SQL Database instance for the connectionString property.</span></span> |<span data-ttu-id="8b587-2824">Sim</span><span class="sxs-lookup"><span data-stu-id="8b587-2824">Yes</span></span> |

#### <a name="json-example"></a><span data-ttu-id="8b587-2825">Exemplo de JSON</span><span class="sxs-lookup"><span data-stu-id="8b587-2825">JSON example</span></span>

```json
{
    "name": "AzureSqlLinkedService",
    "properties": {
        "type": "AzureSqlDatabase",
        "typeProperties": {
            "connectionString": "Server=tcp:<servername>.database.windows.net,1433;Database=<databasename>;User ID=<username>@<servername>;Password=<password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
        }
    }
}
```

<span data-ttu-id="8b587-2826">Confira o artigo [Conector SQL do Azure](data-factory-azure-sql-connector.md#linked-service-properties) para saber mais sobre esse serviço vinculado.</span><span class="sxs-lookup"><span data-stu-id="8b587-2826">See [Azure SQL Connector](data-factory-azure-sql-connector.md#linked-service-properties) article for details about this linked service.</span></span>

## <a name="azure-sql-data-warehouse"></a><span data-ttu-id="8b587-2827">SQL Data Warehouse do Azure</span><span class="sxs-lookup"><span data-stu-id="8b587-2827">Azure SQL Data Warehouse</span></span>
<span data-ttu-id="8b587-2828">Você pode criar um serviço vinculado do SQL Data Warehouse do Azure e usá-lo com a [Atividade de Procedimento Armazenado](data-factory-stored-proc-activity.md) para invocar um procedimento armazenado de um pipeline do Data Factory.</span><span class="sxs-lookup"><span data-stu-id="8b587-2828">You create an Azure SQL Data Warehouse linked service and use it with the [Stored Procedure Activity](data-factory-stored-proc-activity.md) to invoke a stored procedure from a Data Factory pipeline.</span></span> 

### <a name="linked-service"></a><span data-ttu-id="8b587-2829">Serviço vinculado</span><span class="sxs-lookup"><span data-stu-id="8b587-2829">Linked service</span></span>
<span data-ttu-id="8b587-2830">Para definir um serviço vinculado do SQL Data Warehouse do Azure, defina o **type** do serviço vinculado para **AzureSqlDW** e especifique as propriedades a seguir na seção **typeProperties**:</span><span class="sxs-lookup"><span data-stu-id="8b587-2830">To define an Azure SQL Data Warehouse linked service, set the **type** of the linked service to **AzureSqlDW**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="8b587-2831">Propriedade</span><span class="sxs-lookup"><span data-stu-id="8b587-2831">Property</span></span> | <span data-ttu-id="8b587-2832">Descrição</span><span class="sxs-lookup"><span data-stu-id="8b587-2832">Description</span></span> | <span data-ttu-id="8b587-2833">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="8b587-2833">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8b587-2834">connectionString</span><span class="sxs-lookup"><span data-stu-id="8b587-2834">connectionString</span></span> |<span data-ttu-id="8b587-2835">Especifique as informações necessárias para se conectar à instância do SQL Data Warehouse do Azure para a propriedade connectionString.</span><span class="sxs-lookup"><span data-stu-id="8b587-2835">Specify information needed to connect to the Azure SQL Data Warehouse instance for the connectionString property.</span></span> |<span data-ttu-id="8b587-2836">Sim</span><span class="sxs-lookup"><span data-stu-id="8b587-2836">Yes</span></span> |

#### <a name="json-example"></a><span data-ttu-id="8b587-2837">Exemplo de JSON</span><span class="sxs-lookup"><span data-stu-id="8b587-2837">JSON example</span></span>

```json
{
    "name": "AzureSqlDWLinkedService",
    "properties": {
        "type": "AzureSqlDW",
        "typeProperties": {
            "connectionString": "Server=tcp:<servername>.database.windows.net,1433;Database=<databasename>;User ID=<username>@<servername>;Password=<password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
        }
    }
}
```

<span data-ttu-id="8b587-2838">Para obter mais informações, consulte o artigo [Conector do SQL Data Warehouse do Azure](data-factory-azure-sql-data-warehouse-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="8b587-2838">For more information, see [Azure SQL Data Warehouse connector](data-factory-azure-sql-data-warehouse-connector.md#linked-service-properties) article.</span></span> 

## <a name="sql-server"></a><span data-ttu-id="8b587-2839">SQL Server</span><span class="sxs-lookup"><span data-stu-id="8b587-2839">SQL Server</span></span> 
<span data-ttu-id="8b587-2840">Você pode criar um serviço vinculado do SQL Server e usá-lo com a [Atividade de Procedimento Armazenado](data-factory-stored-proc-activity.md) para invocar um procedimento armazenado de um pipeline do Data Factory.</span><span class="sxs-lookup"><span data-stu-id="8b587-2840">You create a SQL Server linked service and use it with the [Stored Procedure Activity](data-factory-stored-proc-activity.md) to invoke a stored procedure from a Data Factory pipeline.</span></span> 

### <a name="linked-service"></a><span data-ttu-id="8b587-2841">Serviço vinculado</span><span class="sxs-lookup"><span data-stu-id="8b587-2841">Linked service</span></span>
<span data-ttu-id="8b587-2842">Você cria um serviço vinculado do tipo **OnPremisesSqlServer** para vincular um banco de dados do SQL Server local a um data factory.</span><span class="sxs-lookup"><span data-stu-id="8b587-2842">You create a linked service of type **OnPremisesSqlServer** to link an on-premises SQL Server database to a data factory.</span></span> <span data-ttu-id="8b587-2843">A tabela a seguir fornece a descrição para elementos JSON específicos para o serviço vinculado do SQL Server local.</span><span class="sxs-lookup"><span data-stu-id="8b587-2843">The following table provides description for JSON elements specific to on-premises SQL Server linked service.</span></span>

<span data-ttu-id="8b587-2844">A tabela a seguir fornece a descrição para elementos JSON específicos para o serviço vinculado do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="8b587-2844">The following table provides description for JSON elements specific to SQL Server linked service.</span></span>

| <span data-ttu-id="8b587-2845">Propriedade</span><span class="sxs-lookup"><span data-stu-id="8b587-2845">Property</span></span> | <span data-ttu-id="8b587-2846">Descrição</span><span class="sxs-lookup"><span data-stu-id="8b587-2846">Description</span></span> | <span data-ttu-id="8b587-2847">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="8b587-2847">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8b587-2848">type</span><span class="sxs-lookup"><span data-stu-id="8b587-2848">type</span></span> |<span data-ttu-id="8b587-2849">A propriedade type deve ser definida como: **OnPremisesSqlServer**.</span><span class="sxs-lookup"><span data-stu-id="8b587-2849">The type property should be set to: **OnPremisesSqlServer**.</span></span> |<span data-ttu-id="8b587-2850">Sim</span><span class="sxs-lookup"><span data-stu-id="8b587-2850">Yes</span></span> |
| <span data-ttu-id="8b587-2851">connectionString</span><span class="sxs-lookup"><span data-stu-id="8b587-2851">connectionString</span></span> |<span data-ttu-id="8b587-2852">Especifique as informações de connectionString necessárias para conexão com o banco de dados do SQL Server local usando a autenticação do SQL ou então a autenticação do Windows.</span><span class="sxs-lookup"><span data-stu-id="8b587-2852">Specify connectionString information needed to connect to the on-premises SQL Server database using either SQL authentication or Windows authentication.</span></span> |<span data-ttu-id="8b587-2853">Sim</span><span class="sxs-lookup"><span data-stu-id="8b587-2853">Yes</span></span> |
| <span data-ttu-id="8b587-2854">gatewayName</span><span class="sxs-lookup"><span data-stu-id="8b587-2854">gatewayName</span></span> |<span data-ttu-id="8b587-2855">O nome do gateway que o serviço Data Factory deve usar para se conectar ao banco de dados do SQL Server local.</span><span class="sxs-lookup"><span data-stu-id="8b587-2855">Name of the gateway that the Data Factory service should use to connect to the on-premises SQL Server database.</span></span> |<span data-ttu-id="8b587-2856">Sim</span><span class="sxs-lookup"><span data-stu-id="8b587-2856">Yes</span></span> |
| <span data-ttu-id="8b587-2857">Nome de Usuário</span><span class="sxs-lookup"><span data-stu-id="8b587-2857">username</span></span> |<span data-ttu-id="8b587-2858">Especifique o nome de usuário se você estiver usando a Autenticação do Windows.</span><span class="sxs-lookup"><span data-stu-id="8b587-2858">Specify user name if you are using Windows Authentication.</span></span> <span data-ttu-id="8b587-2859">Exemplo: **domainname\\username**.</span><span class="sxs-lookup"><span data-stu-id="8b587-2859">Example: **domainname\\username**.</span></span> |<span data-ttu-id="8b587-2860">Não</span><span class="sxs-lookup"><span data-stu-id="8b587-2860">No</span></span> |
| <span data-ttu-id="8b587-2861">Senha</span><span class="sxs-lookup"><span data-stu-id="8b587-2861">password</span></span> |<span data-ttu-id="8b587-2862">Especifique a senha da conta de usuário que você especificou para o nome de usuário.</span><span class="sxs-lookup"><span data-stu-id="8b587-2862">Specify password for the user account you specified for the username.</span></span> |<span data-ttu-id="8b587-2863">Não</span><span class="sxs-lookup"><span data-stu-id="8b587-2863">No</span></span> |

<span data-ttu-id="8b587-2864">Criptografe as credenciais usando o cmdlet **New-AzureRmDataFactoryEncryptValue** e use-as na cadeia de conexão, como mostrado no seguinte exemplo (propriedade **EncryptedCredential**):</span><span class="sxs-lookup"><span data-stu-id="8b587-2864">You can encrypt credentials using the **New-AzureRmDataFactoryEncryptValue** cmdlet and use them in the connection string as shown in the following example (**EncryptedCredential** property):</span></span>  

```JSON
"connectionString": "Data Source=<servername>;Initial Catalog=<databasename>;Integrated Security=True;EncryptedCredential=<encrypted credential>",
```


#### <a name="example-json-for-using-sql-authentication"></a><span data-ttu-id="8b587-2865">Exemplo: JSON para usar Autenticação SQL</span><span class="sxs-lookup"><span data-stu-id="8b587-2865">Example: JSON for using SQL Authentication</span></span>

```json
{
    "name": "MyOnPremisesSQLDB",
    "properties": {
        "type": "OnPremisesSqlServer",
        "typeProperties": {
            "connectionString": "Data Source=<servername>;Initial Catalog=MarketingCampaigns;Integrated Security=False;User ID=<username>;Password=<password>;",
            "gatewayName": "<gateway name>"
        }
    }
}
```
#### <a name="example-json-for-using-windows-authentication"></a><span data-ttu-id="8b587-2866">Exemplo: JSON para usar Autenticação Windows</span><span class="sxs-lookup"><span data-stu-id="8b587-2866">Example: JSON for using Windows Authentication</span></span>

<span data-ttu-id="8b587-2867">Se o nome de usuário e a senha forem especificados, o gateway os usará para representar a conta de usuário especificada para se conectar ao banco de dados SQL Server local.</span><span class="sxs-lookup"><span data-stu-id="8b587-2867">If username and password are specified, gateway uses them to impersonate the specified user account to connect to the on-premises SQL Server database.</span></span> <span data-ttu-id="8b587-2868">Caso contrário, o gateway se conectará ao SQL Server diretamente com o contexto de segurança do Gateway (a sua conta de inicialização).</span><span class="sxs-lookup"><span data-stu-id="8b587-2868">Otherwise, gateway connects to the SQL Server directly with the security context of Gateway (its startup account).</span></span>

```json
{
    "Name": " MyOnPremisesSQLDB",
    "Properties": {
        "type": "OnPremisesSqlServer",
        "typeProperties": {
            "ConnectionString": "Data Source=<servername>;Initial Catalog=MarketingCampaigns;Integrated Security=True;",
            "username": "<domain\\username>",
            "password": "<password>",
            "gatewayName": "<gateway name>"
        }
    }
}
```

<span data-ttu-id="8b587-2869">Para obter mais informações, consulte o artigo [Conector de SQL Server](data-factory-sqlserver-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="8b587-2869">For more information, see [SQL Server connector](data-factory-sqlserver-connector.md#linked-service-properties) article.</span></span>

## <a name="data-transformation-activities"></a><span data-ttu-id="8b587-2870">ATIVIDADES DE TRANSFORMAÇÃO DE DADOS</span><span class="sxs-lookup"><span data-stu-id="8b587-2870">DATA TRANSFORMATION ACTIVITIES</span></span>

<span data-ttu-id="8b587-2871">Atividade</span><span class="sxs-lookup"><span data-stu-id="8b587-2871">Activity</span></span> | <span data-ttu-id="8b587-2872">Descrição</span><span class="sxs-lookup"><span data-stu-id="8b587-2872">Description</span></span>
-------- | -----------
[<span data-ttu-id="8b587-2873">Atividade de Hive do HDInsight</span><span class="sxs-lookup"><span data-stu-id="8b587-2873">HDInsight Hive activity</span></span>](#hdinsight-hive-activity) | <span data-ttu-id="8b587-2874">A atividade de Hive do HDInsight em um pipeline de Data Factory executa consultas de Hive em seu próprio cluster ou no cluster sob demanda do HDInsight baseado em Windows/Linux.</span><span class="sxs-lookup"><span data-stu-id="8b587-2874">The HDInsight Hive activity in a Data Factory pipeline executes Hive queries on your own or on-demand Windows/Linux-based HDInsight cluster.</span></span> 
[<span data-ttu-id="8b587-2875">Atividade de Pig do HDInsight</span><span class="sxs-lookup"><span data-stu-id="8b587-2875">HDInsight Pig activity</span></span>](#hdinsight-pig-activity) | <span data-ttu-id="8b587-2876">A atividade de Pig do HDInsight em um pipeline de Data Factory executa consultas de Pig em seu próprio cluster ou no cluster sob demanda do HDInsight baseado em Windows/Linux.</span><span class="sxs-lookup"><span data-stu-id="8b587-2876">The HDInsight Pig activity in a Data Factory pipeline executes Pig queries on your own or on-demand Windows/Linux-based HDInsight cluster.</span></span>
[<span data-ttu-id="8b587-2877">Atividade de MapReduce do HDInsight</span><span class="sxs-lookup"><span data-stu-id="8b587-2877">HDInsight MapReduce Activity</span></span>](#hdinsight-mapreduce-activity) | <span data-ttu-id="8b587-2878">A atividade de MapReduce do HDInsight em um pipeline do Data Factory executa programas MapReduce no seu próprio cluster HDInsight baseado em Windows/Linux, ou em um sob demanda.</span><span class="sxs-lookup"><span data-stu-id="8b587-2878">The HDInsight MapReduce activity in a Data Factory pipeline executes MapReduce programs on your own or on-demand Windows/Linux-based HDInsight cluster.</span></span>
[<span data-ttu-id="8b587-2879">Atividade de Streaming do HDInsight</span><span class="sxs-lookup"><span data-stu-id="8b587-2879">HDInsight Streaming Activity</span></span>](#hdinsight-streaming-activity) | <span data-ttu-id="8b587-2880">A Atividade de Streaming do HDInsight em um pipeline do Data Factory executa programas de Transmissão do Hadoop em seu próprio ou cluster HDInsight sob demanda baseado no Windows/Linux.</span><span class="sxs-lookup"><span data-stu-id="8b587-2880">The HDInsight Streaming Activity in a Data Factory pipeline executes Hadoop Streaming programs on your own or on-demand Windows/Linux-based HDInsight cluster.</span></span>
[<span data-ttu-id="8b587-2881">Atividade do HDInsight Spark</span><span class="sxs-lookup"><span data-stu-id="8b587-2881">HDInsight Spark Activity</span></span>](#hdinsight-spark-activity) | <span data-ttu-id="8b587-2882">A atividade do HDInsight Spark em um pipeline do Data Factory executa programas do Spark em seu próprio cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="8b587-2882">The HDInsight Spark activity in a Data Factory pipeline executes Spark programs on your own HDInsight cluster.</span></span> 
[<span data-ttu-id="8b587-2883">Atividade de Execução em Lote do Machine Learning</span><span class="sxs-lookup"><span data-stu-id="8b587-2883">Machine Learning Batch Execution Activity</span></span>](#machine-learning-batch-execution-activity) | <span data-ttu-id="8b587-2884">O Azure Data Factory permite que você crie facilmente pipelines que usam o serviço Web do Azure Machine Learning publicado para a análise preditiva.</span><span class="sxs-lookup"><span data-stu-id="8b587-2884">Azure Data Factory enables you to easily create pipelines that use a published Azure Machine Learning web service for predictive analytics.</span></span> <span data-ttu-id="8b587-2885">Usando a Atividade de Execução em Lote em um pipeline do Azure Data Factory, você pode invocar um serviço Web do Machine Learning para fazer previsões sobre dados em lote.</span><span class="sxs-lookup"><span data-stu-id="8b587-2885">Using the Batch Execution Activity in an Azure Data Factory pipeline, you can invoke a Machine Learning web service to make predictions on the data in batch.</span></span> 
[<span data-ttu-id="8b587-2886">Atividade do Recurso de Atualização do Machine Learning</span><span class="sxs-lookup"><span data-stu-id="8b587-2886">Machine Learning Update Resource Activity</span></span>](#machine-learning-update-resource-activity) | <span data-ttu-id="8b587-2887">Ao longo do tempo, os modelos de previsão nos testes de pontuação do Machine Learning precisam ser readaptados usando novos conjuntos de dados de entrada.</span><span class="sxs-lookup"><span data-stu-id="8b587-2887">Over time, the predictive models in the Machine Learning scoring experiments need to be retrained using new input datasets.</span></span> <span data-ttu-id="8b587-2888">Depois de concluir o novo treinamento, você deseja atualizar o serviço Web de pontuação com o modelo do Machine Learning readaptado.</span><span class="sxs-lookup"><span data-stu-id="8b587-2888">After you are done with retraining, you want to update the scoring web service with the retrained Machine Learning model.</span></span> <span data-ttu-id="8b587-2889">Você pode usar a Atividade de Recurso de Atualização para atualizar o serviço Web com o modelo recém-adaptado.</span><span class="sxs-lookup"><span data-stu-id="8b587-2889">You can use the Update Resource Activity to update the web service with the newly trained model.</span></span>
[<span data-ttu-id="8b587-2890">Atividade de Procedimento Armazenado</span><span class="sxs-lookup"><span data-stu-id="8b587-2890">Stored Procedure Activity</span></span>](#stored-procedure-activity) | <span data-ttu-id="8b587-2891">Você pode usar a atividade de Procedimento Armazenado em um pipeline de Data Factory para invocar um procedimento armazenado em um dos seguintes armazenamentos de dados: Banco de Dados SQL do Azrue, SQL Data Warehouse do Azure, Banco de Dados SQL Server na sua empresa ou uma VM do Azure.</span><span class="sxs-lookup"><span data-stu-id="8b587-2891">You can use the Stored Procedure activity in a Data Factory pipeline to invoke a stored procedure in one of the following data stores: Azure SQL Database, Azure SQL Data Warehouse, SQL Server Database in your enterprise or an Azure VM.</span></span> 
[<span data-ttu-id="8b587-2892">Atividade de U-SQL do Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="8b587-2892">Data Lake Analytics U-SQL activity</span></span>](#data-lake-analytics-u-sql-activity) | <span data-ttu-id="8b587-2893">A atividade de U-SQL do Data Lake Analytics executa um script U-SQL em um cluster do Azure Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="8b587-2893">Data Lake Analytics U-SQL Activity runs a U-SQL script on an Azure Data Lake Analytics cluster.</span></span>  
[<span data-ttu-id="8b587-2894">Atividade personalizada do .NET</span><span class="sxs-lookup"><span data-stu-id="8b587-2894">.NET custom activity</span></span>](#net-custom-activity) | <span data-ttu-id="8b587-2895">Se precisar transformar dados de uma maneira que não tenha suporte do Data Factory, você poderá criar uma atividade personalizada com sua própria lógica de processamento de dados e usar a atividade no pipeline.</span><span class="sxs-lookup"><span data-stu-id="8b587-2895">If you need to transform data in a way that is not supported by Data Factory, you can create a custom activity with your own data processing logic and use the activity in the pipeline.</span></span> <span data-ttu-id="8b587-2896">Você pode configurar a atividade personalizada do .NET para que seja executada usando um serviço de Lote do Azure ou um cluster do Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="8b587-2896">You can configure the custom .NET activity to run using either an Azure Batch service or an Azure HDInsight cluster.</span></span> 

     
## <a name="hdinsight-hive-activity"></a><span data-ttu-id="8b587-2897">Atividade de Hive do HDInsight</span><span class="sxs-lookup"><span data-stu-id="8b587-2897">HDInsight Hive Activity</span></span>
<span data-ttu-id="8b587-2898">Você pode especificar as seguintes propriedades em uma definição de JSON de atividade do Hive.</span><span class="sxs-lookup"><span data-stu-id="8b587-2898">You can specify the following properties in a Hive Activity JSON definition.</span></span> <span data-ttu-id="8b587-2899">A propriedade type para a atividade deve ser: **HDInsightHive**.</span><span class="sxs-lookup"><span data-stu-id="8b587-2899">The type property for the activity must be: **HDInsightHive**.</span></span> <span data-ttu-id="8b587-2900">Você deve primeiro criar um serviço vinculado do HDInsight e especificar o nome dele como um valor para a propriedade **linkedServiceName**.</span><span class="sxs-lookup"><span data-stu-id="8b587-2900">You must create a HDInsight linked service first and specify the name of it as a value for the **linkedServiceName** property.</span></span> <span data-ttu-id="8b587-2901">As propriedades a seguir possuem suporte na seção **typeProperties** quando você define o tipo de atividade para HDInsightHive:</span><span class="sxs-lookup"><span data-stu-id="8b587-2901">The following properties are supported in the **typeProperties** section when you set the type of activity to HDInsightHive:</span></span>

| <span data-ttu-id="8b587-2902">Propriedade</span><span class="sxs-lookup"><span data-stu-id="8b587-2902">Property</span></span> | <span data-ttu-id="8b587-2903">Descrição</span><span class="sxs-lookup"><span data-stu-id="8b587-2903">Description</span></span> | <span data-ttu-id="8b587-2904">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="8b587-2904">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8b587-2905">script</span><span class="sxs-lookup"><span data-stu-id="8b587-2905">script</span></span> |<span data-ttu-id="8b587-2906">Especifique o script de Hive embutido</span><span class="sxs-lookup"><span data-stu-id="8b587-2906">Specify the Hive script inline</span></span> |<span data-ttu-id="8b587-2907">Não</span><span class="sxs-lookup"><span data-stu-id="8b587-2907">No</span></span> |
| <span data-ttu-id="8b587-2908">script path</span><span class="sxs-lookup"><span data-stu-id="8b587-2908">script path</span></span> |<span data-ttu-id="8b587-2909">Armazene o script de Hive em um armazenamento de blob do Azure e forneça o caminho para o arquivo.</span><span class="sxs-lookup"><span data-stu-id="8b587-2909">Store the Hive script in an Azure blob storage and provide the path to the file.</span></span> <span data-ttu-id="8b587-2910">Use a propriedade 'script' ou 'scriptPath'.</span><span class="sxs-lookup"><span data-stu-id="8b587-2910">Use 'script' or 'scriptPath' property.</span></span> <span data-ttu-id="8b587-2911">As duas não podem ser usadas juntas.</span><span class="sxs-lookup"><span data-stu-id="8b587-2911">Both cannot be used together.</span></span> <span data-ttu-id="8b587-2912">O nome do arquivo diferencia maiúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="8b587-2912">The file name is case-sensitive.</span></span> |<span data-ttu-id="8b587-2913">Não</span><span class="sxs-lookup"><span data-stu-id="8b587-2913">No</span></span> |
| <span data-ttu-id="8b587-2914">defines</span><span class="sxs-lookup"><span data-stu-id="8b587-2914">defines</span></span> |<span data-ttu-id="8b587-2915">Especifique parâmetros como pares chave/valor para referenciar dentro do script de Hive usando 'hiveconf'</span><span class="sxs-lookup"><span data-stu-id="8b587-2915">Specify parameters as key/value pairs for referencing within the Hive script using 'hiveconf'</span></span> |<span data-ttu-id="8b587-2916">Não</span><span class="sxs-lookup"><span data-stu-id="8b587-2916">No</span></span> |

<span data-ttu-id="8b587-2917">Essas propriedades de tipo são específicas para a atividade de Hive.</span><span class="sxs-lookup"><span data-stu-id="8b587-2917">These type properties are specific to the Hive Activity.</span></span> <span data-ttu-id="8b587-2918">Outras propriedades (fora da seção typeProperties) possuem suporte para todas as atividades.</span><span class="sxs-lookup"><span data-stu-id="8b587-2918">Other properties (outside the typeProperties section) are supported for all activities.</span></span>   

### <a name="json-example"></a><span data-ttu-id="8b587-2919">Exemplo de JSON</span><span class="sxs-lookup"><span data-stu-id="8b587-2919">JSON example</span></span>
<span data-ttu-id="8b587-2920">O JSON a seguir define uma atividade de Hive do HDInsight em um pipeline.</span><span class="sxs-lookup"><span data-stu-id="8b587-2920">The following JSON defines a HDInsight Hive activity in a pipeline.</span></span>  

```json
{
    "name": "Hive Activity",
    "description": "description",
    "type": "HDInsightHive",
    "inputs": [
      {
        "name": "input tables"
      }
    ],
    "outputs": [
      {
        "name": "output tables"
      }
    ],
    "linkedServiceName": "MyHDInsightLinkedService",
    "typeProperties": {
      "script": "Hive script",
      "scriptPath": "<pathtotheHivescriptfileinAzureblobstorage>",
      "defines": {
        "param1": "param1Value"
      }
    },
   "scheduler": {
      "frequency": "Day",
      "interval": 1
    }
}
```

<span data-ttu-id="8b587-2921">Para saber mais, consulte o artigo [Atividade de Hive](data-factory-hive-activity.md).</span><span class="sxs-lookup"><span data-stu-id="8b587-2921">For more information, see [Hive Activity](data-factory-hive-activity.md) article.</span></span> 

## <a name="hdinsight-pig-activity"></a><span data-ttu-id="8b587-2922">Atividade de Pig do HDInsight</span><span class="sxs-lookup"><span data-stu-id="8b587-2922">HDInsight Pig Activity</span></span>
<span data-ttu-id="8b587-2923">Você pode especificar as seguintes propriedades em uma definição de JSON de atividade de Pig.</span><span class="sxs-lookup"><span data-stu-id="8b587-2923">You can specify the following properties in a Pig Activity JSON definition.</span></span> <span data-ttu-id="8b587-2924">A propriedade type para a atividade deve ser: **HDInsightPig**.</span><span class="sxs-lookup"><span data-stu-id="8b587-2924">The type property for the activity must be: **HDInsightPig**.</span></span> <span data-ttu-id="8b587-2925">Você deve primeiro criar um serviço vinculado do HDInsight e especificar o nome dele como um valor para a propriedade **linkedServiceName**.</span><span class="sxs-lookup"><span data-stu-id="8b587-2925">You must create a HDInsight linked service first and specify the name of it as a value for the **linkedServiceName** property.</span></span> <span data-ttu-id="8b587-2926">As propriedades a seguir possuem suporte na seção **typeProperties** quando você define o tipo de atividade para HDInsightPig:</span><span class="sxs-lookup"><span data-stu-id="8b587-2926">The following properties are supported in the **typeProperties** section when you set the type of activity to HDInsightPig:</span></span> 

| <span data-ttu-id="8b587-2927">Propriedade</span><span class="sxs-lookup"><span data-stu-id="8b587-2927">Property</span></span> | <span data-ttu-id="8b587-2928">Descrição</span><span class="sxs-lookup"><span data-stu-id="8b587-2928">Description</span></span> | <span data-ttu-id="8b587-2929">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="8b587-2929">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8b587-2930">script</span><span class="sxs-lookup"><span data-stu-id="8b587-2930">script</span></span> |<span data-ttu-id="8b587-2931">Especificar o script de Pig embutido</span><span class="sxs-lookup"><span data-stu-id="8b587-2931">Specify the Pig script inline</span></span> |<span data-ttu-id="8b587-2932">Não</span><span class="sxs-lookup"><span data-stu-id="8b587-2932">No</span></span> |
| <span data-ttu-id="8b587-2933">caminho do script</span><span class="sxs-lookup"><span data-stu-id="8b587-2933">script path</span></span> |<span data-ttu-id="8b587-2934">Armazenar o script de Pig em um armazenamento de blob do Azure e fornecer o caminho para o arquivo.</span><span class="sxs-lookup"><span data-stu-id="8b587-2934">Store the Pig script in an Azure blob storage and provide the path to the file.</span></span> <span data-ttu-id="8b587-2935">Use a propriedade 'script' ou 'scriptPath'.</span><span class="sxs-lookup"><span data-stu-id="8b587-2935">Use 'script' or 'scriptPath' property.</span></span> <span data-ttu-id="8b587-2936">As duas não podem ser usadas juntas.</span><span class="sxs-lookup"><span data-stu-id="8b587-2936">Both cannot be used together.</span></span> <span data-ttu-id="8b587-2937">O nome do arquivo diferencia maiúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="8b587-2937">The file name is case-sensitive.</span></span> |<span data-ttu-id="8b587-2938">Não</span><span class="sxs-lookup"><span data-stu-id="8b587-2938">No</span></span> |
| <span data-ttu-id="8b587-2939">define</span><span class="sxs-lookup"><span data-stu-id="8b587-2939">defines</span></span> |<span data-ttu-id="8b587-2940">Especificar parâmetros como pares chave/valor para referenciar dentro do script de Pig</span><span class="sxs-lookup"><span data-stu-id="8b587-2940">Specify parameters as key/value pairs for referencing within the Pig script</span></span> |<span data-ttu-id="8b587-2941">Não</span><span class="sxs-lookup"><span data-stu-id="8b587-2941">No</span></span> |

<span data-ttu-id="8b587-2942">Essas propriedades de tipo são específicas para a atividade de Pig.</span><span class="sxs-lookup"><span data-stu-id="8b587-2942">These type properties are specific to the Pig Activity.</span></span> <span data-ttu-id="8b587-2943">Outras propriedades (fora da seção typeProperties) possuem suporte para todas as atividades.</span><span class="sxs-lookup"><span data-stu-id="8b587-2943">Other properties (outside the typeProperties section) are supported for all activities.</span></span>   

### <a name="json-example"></a><span data-ttu-id="8b587-2944">Exemplo de JSON</span><span class="sxs-lookup"><span data-stu-id="8b587-2944">JSON example</span></span>

```json
{
    "name": "HiveActivitySamplePipeline",
      "properties": {
    "activities": [
        {
            "name": "Pig Activity",
            "description": "description",
            "type": "HDInsightPig",
            "inputs": [
                  {
                    "name": "input tables"
                  }
            ],
            "outputs": [
                  {
                    "name": "output tables"
                  }
            ],
            "linkedServiceName": "MyHDInsightLinkedService",
            "typeProperties": {
                  "script": "Pig script",
                  "scriptPath": "<pathtothePigscriptfileinAzureblobstorage>",
                  "defines": {
                    "param1": "param1Value"
                  }
            },
               "scheduler": {
                  "frequency": "Day",
                  "interval": 1
            }
          }
    ]
  }
}
```

<span data-ttu-id="8b587-2945">Para saber mais, consulte o artigo [Atividade de Pig](#data-factory-pig-activity.md).</span><span class="sxs-lookup"><span data-stu-id="8b587-2945">For more information, see [Pig Activity](#data-factory-pig-activity.md) article.</span></span> 

## <a name="hdinsight-mapreduce-activity"></a><span data-ttu-id="8b587-2946">Atividade de MapReduce do HDInsight</span><span class="sxs-lookup"><span data-stu-id="8b587-2946">HDInsight MapReduce Activity</span></span>
<span data-ttu-id="8b587-2947">Você pode especificar as seguintes propriedades em uma definição de JSON de Atividade MapReduce.</span><span class="sxs-lookup"><span data-stu-id="8b587-2947">You can specify the following properties in a MapReduce Activity JSON definition.</span></span> <span data-ttu-id="8b587-2948">A propriedade type para a atividade deve ser: **HDInsightMapReduce**.</span><span class="sxs-lookup"><span data-stu-id="8b587-2948">The type property for the activity must be: **HDInsightMapReduce**.</span></span> <span data-ttu-id="8b587-2949">Você deve primeiro criar um serviço vinculado do HDInsight e especificar o nome dele como um valor para a propriedade **linkedServiceName**.</span><span class="sxs-lookup"><span data-stu-id="8b587-2949">You must create a HDInsight linked service first and specify the name of it as a value for the **linkedServiceName** property.</span></span> <span data-ttu-id="8b587-2950">As propriedades a seguir possuem suporte na seção **typeProperties** quando você define o tipo de atividade para HDInsightMapReduce:</span><span class="sxs-lookup"><span data-stu-id="8b587-2950">The following properties are supported in the **typeProperties** section when you set the type of activity to HDInsightMapReduce:</span></span> 

| <span data-ttu-id="8b587-2951">Propriedade</span><span class="sxs-lookup"><span data-stu-id="8b587-2951">Property</span></span> | <span data-ttu-id="8b587-2952">Descrição</span><span class="sxs-lookup"><span data-stu-id="8b587-2952">Description</span></span> | <span data-ttu-id="8b587-2953">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="8b587-2953">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8b587-2954">jarLinkedService</span><span class="sxs-lookup"><span data-stu-id="8b587-2954">jarLinkedService</span></span> | <span data-ttu-id="8b587-2955">Nome do serviço vinculado do Armazenamento do Azure que contém o arquivo JAR.</span><span class="sxs-lookup"><span data-stu-id="8b587-2955">Name of the linked service for the Azure Storage that contains the JAR file.</span></span> | <span data-ttu-id="8b587-2956">Sim</span><span class="sxs-lookup"><span data-stu-id="8b587-2956">Yes</span></span> |
| <span data-ttu-id="8b587-2957">jarFilePath</span><span class="sxs-lookup"><span data-stu-id="8b587-2957">jarFilePath</span></span> | <span data-ttu-id="8b587-2958">Caminho para o arquivo JAR no Armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="8b587-2958">Path to the JAR file in the Azure Storage.</span></span> | <span data-ttu-id="8b587-2959">Sim</span><span class="sxs-lookup"><span data-stu-id="8b587-2959">Yes</span></span> | 
| <span data-ttu-id="8b587-2960">className</span><span class="sxs-lookup"><span data-stu-id="8b587-2960">className</span></span> | <span data-ttu-id="8b587-2961">Nome da classe principal no arquivo JAR.</span><span class="sxs-lookup"><span data-stu-id="8b587-2961">Name of the main class in the JAR file.</span></span> | <span data-ttu-id="8b587-2962">Sim</span><span class="sxs-lookup"><span data-stu-id="8b587-2962">Yes</span></span> | 
| <span data-ttu-id="8b587-2963">argumentos</span><span class="sxs-lookup"><span data-stu-id="8b587-2963">arguments</span></span> | <span data-ttu-id="8b587-2964">Uma lista de argumentos separados por vírgulas para o programa MapReduce.</span><span class="sxs-lookup"><span data-stu-id="8b587-2964">A list of comma-separated arguments for the MapReduce program.</span></span> <span data-ttu-id="8b587-2965">Em tempo de execução, você verá alguns argumentos extras (por exemplo: mapreduce.job.tags) da estrutura MapReduce.</span><span class="sxs-lookup"><span data-stu-id="8b587-2965">At runtime, you see a few extra arguments (for example: mapreduce.job.tags) from the MapReduce framework.</span></span> <span data-ttu-id="8b587-2966">Para diferenciar seus argumentos com os argumentos MapReduce, considere usar opção e valor como argumentos, conforme mostrado no exemplo a seguir (- s, --input - output etc... são opções seguidas imediatamente por seus valores)</span><span class="sxs-lookup"><span data-stu-id="8b587-2966">To differentiate your arguments with the MapReduce arguments, consider using both option and value as arguments as shown in the following example (-s, --input, --output etc., are options immediately followed by their values)</span></span> | <span data-ttu-id="8b587-2967">Não</span><span class="sxs-lookup"><span data-stu-id="8b587-2967">No</span></span> | 

### <a name="json-example"></a><span data-ttu-id="8b587-2968">Exemplo de JSON</span><span class="sxs-lookup"><span data-stu-id="8b587-2968">JSON example</span></span>

```json
{
    "name": "MahoutMapReduceSamplePipeline",
    "properties": {
        "description": "Sample Pipeline to Run a Mahout Custom Map Reduce Jar. This job calculates an Item Similarity Matrix to determine the similarity between two items",
        "activities": [
            {
                "type": "HDInsightMapReduce",
                "typeProperties": {
                    "className": "org.apache.mahout.cf.taste.hadoop.similarity.item.ItemSimilarityJob",
                    "jarFilePath": "adfsamples/Mahout/jars/mahout-examples-0.9.0.2.2.7.1-34.jar",
                    "jarLinkedService": "StorageLinkedService",
                    "arguments": ["-s", "SIMILARITY_LOGLIKELIHOOD", "--input", "wasb://adfsamples@spestore.blob.core.windows.net/Mahout/input", "--output", "wasb://adfsamples@spestore.blob.core.windows.net/Mahout/output/", "--maxSimilaritiesPerItem", "500", "--tempDir", "wasb://adfsamples@spestore.blob.core.windows.net/Mahout/temp/mahout"]
                },
                "inputs": [
                    {
                        "name": "MahoutInput"
                    }
                ],
                "outputs": [
                    {
                        "name": "MahoutOutput"
                    }
                ],
                "policy": {
                    "timeout": "01:00:00",
                    "concurrency": 1,
                    "retry": 3
                },
                "scheduler": {
                    "frequency": "Hour",
                    "interval": 1
                },
                "name": "MahoutActivity",
                "description": "Custom Map Reduce to generate Mahout result",
                "linkedServiceName": "HDInsightLinkedService"
            }
        ],
        "start": "2017-01-03T00:00:00",
        "end": "2017-01-04T00:00:00"
    }
}
```

<span data-ttu-id="8b587-2969">Para saber mais, consulte o artigo [Atividade MapReduce](data-factory-map-reduce.md).</span><span class="sxs-lookup"><span data-stu-id="8b587-2969">For more information, see [MapReduce Activity](data-factory-map-reduce.md) article.</span></span> 

## <a name="hdinsight-streaming-activity"></a><span data-ttu-id="8b587-2970">Atividade de Streaming do HDInsight</span><span class="sxs-lookup"><span data-stu-id="8b587-2970">HDInsight Streaming Activity</span></span>
<span data-ttu-id="8b587-2971">Você pode especificar as seguintes propriedades em uma definição de JSON de Atividade de Transmissão do Hadoop.</span><span class="sxs-lookup"><span data-stu-id="8b587-2971">You can specify the following properties in a Hadoop Streaming Activity JSON definition.</span></span> <span data-ttu-id="8b587-2972">A propriedade type para a atividade deve ser: **HDInsightStreaming**.</span><span class="sxs-lookup"><span data-stu-id="8b587-2972">The type property for the activity must be: **HDInsightStreaming**.</span></span> <span data-ttu-id="8b587-2973">Você deve primeiro criar um serviço vinculado do HDInsight e especificar o nome dele como um valor para a propriedade **linkedServiceName**.</span><span class="sxs-lookup"><span data-stu-id="8b587-2973">You must create a HDInsight linked service first and specify the name of it as a value for the **linkedServiceName** property.</span></span> <span data-ttu-id="8b587-2974">As propriedades a seguir possuem suporte na seção **typeProperties** quando você define o tipo de atividade para HDInsightStreaming:</span><span class="sxs-lookup"><span data-stu-id="8b587-2974">The following properties are supported in the **typeProperties** section when you set the type of activity to HDInsightStreaming:</span></span> 

| <span data-ttu-id="8b587-2975">Propriedade</span><span class="sxs-lookup"><span data-stu-id="8b587-2975">Property</span></span> | <span data-ttu-id="8b587-2976">Descrição</span><span class="sxs-lookup"><span data-stu-id="8b587-2976">Description</span></span> | 
| --- | --- |
| <span data-ttu-id="8b587-2977">mapper</span><span class="sxs-lookup"><span data-stu-id="8b587-2977">mapper</span></span> | <span data-ttu-id="8b587-2978">Nome do executável mapeador.</span><span class="sxs-lookup"><span data-stu-id="8b587-2978">Name of the mapper executable.</span></span> <span data-ttu-id="8b587-2979">No exemplo, cat.exe é o executável do mapeador.</span><span class="sxs-lookup"><span data-stu-id="8b587-2979">In the example, cat.exe is the mapper executable.</span></span>| 
| <span data-ttu-id="8b587-2980">reducer</span><span class="sxs-lookup"><span data-stu-id="8b587-2980">reducer</span></span> | <span data-ttu-id="8b587-2981">Nome do executável redutor.</span><span class="sxs-lookup"><span data-stu-id="8b587-2981">Name of the reducer executable.</span></span> <span data-ttu-id="8b587-2982">No exemplo, wc.exe é o executável do redutor.</span><span class="sxs-lookup"><span data-stu-id="8b587-2982">In the example, wc.exe is the reducer executable.</span></span> | 
| <span data-ttu-id="8b587-2983">input</span><span class="sxs-lookup"><span data-stu-id="8b587-2983">input</span></span> | <span data-ttu-id="8b587-2984">Arquivo de entrada (incluindo a localização) do mapeador.</span><span class="sxs-lookup"><span data-stu-id="8b587-2984">Input file (including location) for the mapper.</span></span> <span data-ttu-id="8b587-2985">No exemplo: "wasb://adfsample@<account name>.blob.core.windows.net/example/data/gutenberg/davinci.txt": adfsample é o contêiner de blob, example/data/Gutenberg é a pasta e davinci.txt é o blob.</span><span class="sxs-lookup"><span data-stu-id="8b587-2985">In the example: "wasb://adfsample@<account name>.blob.core.windows.net/example/data/gutenberg/davinci.txt": adfsample is the blob container, example/data/Gutenberg is the folder, and davinci.txt is the blob.</span></span> |
| <span data-ttu-id="8b587-2986">output</span><span class="sxs-lookup"><span data-stu-id="8b587-2986">output</span></span> | <span data-ttu-id="8b587-2987">Arquivo de saída (incluindo a localização) do redutor.</span><span class="sxs-lookup"><span data-stu-id="8b587-2987">Output file (including location) for the reducer.</span></span> <span data-ttu-id="8b587-2988">A saída do trabalho de Transmissão do Hadoop é gravada no local especificado para essa propriedade.</span><span class="sxs-lookup"><span data-stu-id="8b587-2988">The output of the Hadoop Streaming job is written to the location specified for this property.</span></span> |
| <span data-ttu-id="8b587-2989">filePaths</span><span class="sxs-lookup"><span data-stu-id="8b587-2989">filePaths</span></span> | <span data-ttu-id="8b587-2990">Caminhos para os executáveis do mapeador e do redutor.</span><span class="sxs-lookup"><span data-stu-id="8b587-2990">Paths for the mapper and reducer executables.</span></span> <span data-ttu-id="8b587-2991">No exemplo: "adfsample/example/apps/wc.exe", adfsample é o contêiner de blob, example/apps é a pasta e wc.exe é o executável.</span><span class="sxs-lookup"><span data-stu-id="8b587-2991">In the example: "adfsample/example/apps/wc.exe", adfsample is the blob container, example/apps is the folder, and wc.exe is the executable.</span></span> | 
| <span data-ttu-id="8b587-2992">fileLinkedService</span><span class="sxs-lookup"><span data-stu-id="8b587-2992">fileLinkedService</span></span> | <span data-ttu-id="8b587-2993">Serviço vinculado do Armazenamento do Azure que representa o armazenamento do Azure que contém os arquivos especificados na seção filePaths.</span><span class="sxs-lookup"><span data-stu-id="8b587-2993">Azure Storage linked service that represents the Azure storage that contains the files specified in the filePaths section.</span></span> | 
| <span data-ttu-id="8b587-2994">argumentos</span><span class="sxs-lookup"><span data-stu-id="8b587-2994">arguments</span></span> | <span data-ttu-id="8b587-2995">Uma lista de argumentos separados por vírgulas para o programa MapReduce.</span><span class="sxs-lookup"><span data-stu-id="8b587-2995">A list of comma-separated arguments for the MapReduce program.</span></span> <span data-ttu-id="8b587-2996">Em tempo de execução, você verá alguns argumentos extras (por exemplo: mapreduce.job.tags) da estrutura MapReduce.</span><span class="sxs-lookup"><span data-stu-id="8b587-2996">At runtime, you see a few extra arguments (for example: mapreduce.job.tags) from the MapReduce framework.</span></span> <span data-ttu-id="8b587-2997">Para diferenciar seus argumentos com os argumentos MapReduce, considere usar opção e valor como argumentos, conforme mostrado no exemplo a seguir (- s, --input - output etc... são opções seguidas imediatamente por seus valores)</span><span class="sxs-lookup"><span data-stu-id="8b587-2997">To differentiate your arguments with the MapReduce arguments, consider using both option and value as arguments as shown in the following example (-s, --input, --output etc., are options immediately followed by their values)</span></span> | 
| <span data-ttu-id="8b587-2998">getDebugInfo</span><span class="sxs-lookup"><span data-stu-id="8b587-2998">getDebugInfo</span></span> | <span data-ttu-id="8b587-2999">Um elemento opcional.</span><span class="sxs-lookup"><span data-stu-id="8b587-2999">An optional element.</span></span> <span data-ttu-id="8b587-3000">Quando ela é definida como Falha, os logs são baixados somente em caso de falha de execução.</span><span class="sxs-lookup"><span data-stu-id="8b587-3000">When it is set to Failure, the logs are downloaded only on failure.</span></span> <span data-ttu-id="8b587-3001">Quando ela é definida como Todos, os logs sempre são baixados, não importa o status de execução.</span><span class="sxs-lookup"><span data-stu-id="8b587-3001">When it is set to All, logs are always downloaded irrespective of the execution status.</span></span> | 

> [!NOTE]
> <span data-ttu-id="8b587-3002">Você deve especificar um conjunto de dados de saída da Atividade de Transmissão do Hadoop para a propriedade **outputs** .</span><span class="sxs-lookup"><span data-stu-id="8b587-3002">You must specify an output dataset for the Hadoop Streaming Activity for the **outputs** property.</span></span> <span data-ttu-id="8b587-3003">Esse conjunto de dados é apenas um conjunto fictício exigido para direcionar o agendamento de pipeline (a cada hora, diariamente, etc.).</span><span class="sxs-lookup"><span data-stu-id="8b587-3003">This dataset can be just a dummy dataset that is required to drive the pipeline schedule (hourly, daily, etc.).</span></span> <span data-ttu-id="8b587-3004">Se a atividade não aceita uma entrada, você pode ignorar a especificação de um conjunto de dados de entrada para a atividade para a propriedade **inputs**.</span><span class="sxs-lookup"><span data-stu-id="8b587-3004">If the activity doesn't take an input, you can skip specifying an input dataset for the activity for the **inputs** property.</span></span>  

## <a name="json-example"></a><span data-ttu-id="8b587-3005">Exemplo de JSON</span><span class="sxs-lookup"><span data-stu-id="8b587-3005">JSON example</span></span>

```json
{
    "name": "HadoopStreamingPipeline",
    "properties": {
        "description": "Hadoop Streaming Demo",
        "activities": [
            {
                "type": "HDInsightStreaming",
                "typeProperties": {
                    "mapper": "cat.exe",
                    "reducer": "wc.exe",
                    "input": "wasb://<nameofthecluster>@spestore.blob.core.windows.net/example/data/gutenberg/davinci.txt",
                    "output": "wasb://<nameofthecluster>@spestore.blob.core.windows.net/example/data/StreamingOutput/wc.txt",
                    "filePaths": ["<nameofthecluster>/example/apps/wc.exe","<nameofthecluster>/example/apps/cat.exe"],
                    "fileLinkedService": "StorageLinkedService",
                    "getDebugInfo": "Failure"
                },
                "outputs": [
                    {
                        "name": "StreamingOutputDataset"
                    }
                ],
                "policy": {
                    "timeout": "01:00:00",
                    "concurrency": 1,
                    "executionPriorityOrder": "NewestFirst",
                    "retry": 1
                },
                "scheduler": {
                    "frequency": "Day",
                    "interval": 1
                },
                "name": "RunHadoopStreamingJob",
                "description": "Run a Hadoop streaming job",
                "linkedServiceName": "HDInsightLinkedService"
            }
        ],
        "start": "2014-01-04T00:00:00",
        "end": "2014-01-05T00:00:00"
    }
}
```

<span data-ttu-id="8b587-3006">Para saber mais, consulte o artigo [Atividade de Transmissão do Hadoop](data-factory-hadoop-streaming-activity.md).</span><span class="sxs-lookup"><span data-stu-id="8b587-3006">For more information, see [Hadoop Streaming Activity](data-factory-hadoop-streaming-activity.md) article.</span></span> 

## <a name="hdinsight-spark-activity"></a><span data-ttu-id="8b587-3007">Atividade do HDInsight Spark</span><span class="sxs-lookup"><span data-stu-id="8b587-3007">HDInsight Spark Activity</span></span>
<span data-ttu-id="8b587-3008">Você pode especificar as seguintes propriedades em uma definição de JSON de Atividade de Spark.</span><span class="sxs-lookup"><span data-stu-id="8b587-3008">You can specify the following properties in a Spark Activity JSON definition.</span></span> <span data-ttu-id="8b587-3009">A propriedade type para a atividade deve ser: **HDInsightSpark**.</span><span class="sxs-lookup"><span data-stu-id="8b587-3009">The type property for the activity must be: **HDInsightSpark**.</span></span> <span data-ttu-id="8b587-3010">Você deve primeiro criar um serviço vinculado do HDInsight e especificar o nome dele como um valor para a propriedade **linkedServiceName**.</span><span class="sxs-lookup"><span data-stu-id="8b587-3010">You must create a HDInsight linked service first and specify the name of it as a value for the **linkedServiceName** property.</span></span> <span data-ttu-id="8b587-3011">As propriedades a seguir possuem suporte na seção **typeProperties** quando você define o tipo de atividade para HDInsightSpark:</span><span class="sxs-lookup"><span data-stu-id="8b587-3011">The following properties are supported in the **typeProperties** section when you set the type of activity to HDInsightSpark:</span></span> 

| <span data-ttu-id="8b587-3012">Propriedade</span><span class="sxs-lookup"><span data-stu-id="8b587-3012">Property</span></span> | <span data-ttu-id="8b587-3013">Descrição</span><span class="sxs-lookup"><span data-stu-id="8b587-3013">Description</span></span> | <span data-ttu-id="8b587-3014">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="8b587-3014">Required</span></span> |
| -------- | ----------- | -------- |
| <span data-ttu-id="8b587-3015">rootPath</span><span class="sxs-lookup"><span data-stu-id="8b587-3015">rootPath</span></span> | <span data-ttu-id="8b587-3016">O contêiner de Blob do Azure e a pasta que contém o arquivo Spark.</span><span class="sxs-lookup"><span data-stu-id="8b587-3016">The Azure Blob container and folder that contains the Spark file.</span></span> <span data-ttu-id="8b587-3017">O nome do arquivo diferencia maiúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="8b587-3017">The file name is case-sensitive.</span></span> | <span data-ttu-id="8b587-3018">Sim</span><span class="sxs-lookup"><span data-stu-id="8b587-3018">Yes</span></span> |
| <span data-ttu-id="8b587-3019">entryFilePath</span><span class="sxs-lookup"><span data-stu-id="8b587-3019">entryFilePath</span></span> | <span data-ttu-id="8b587-3020">Caminho relativo à pasta raiz do código/pacote Spark.</span><span class="sxs-lookup"><span data-stu-id="8b587-3020">Relative path to the root folder of the Spark code/package.</span></span> | <span data-ttu-id="8b587-3021">Sim</span><span class="sxs-lookup"><span data-stu-id="8b587-3021">Yes</span></span> |
| <span data-ttu-id="8b587-3022">className</span><span class="sxs-lookup"><span data-stu-id="8b587-3022">className</span></span> | <span data-ttu-id="8b587-3023">Classe principal de Java/Spark do aplicativo</span><span class="sxs-lookup"><span data-stu-id="8b587-3023">Application's Java/Spark main class</span></span> | <span data-ttu-id="8b587-3024">Não</span><span class="sxs-lookup"><span data-stu-id="8b587-3024">No</span></span> | 
| <span data-ttu-id="8b587-3025">argumentos</span><span class="sxs-lookup"><span data-stu-id="8b587-3025">arguments</span></span> | <span data-ttu-id="8b587-3026">Uma lista de argumentos de linha de comando para o programa Spark.</span><span class="sxs-lookup"><span data-stu-id="8b587-3026">A list of command-line arguments to the Spark program.</span></span> | <span data-ttu-id="8b587-3027">Não</span><span class="sxs-lookup"><span data-stu-id="8b587-3027">No</span></span> | 
| <span data-ttu-id="8b587-3028">proxyUser</span><span class="sxs-lookup"><span data-stu-id="8b587-3028">proxyUser</span></span> | <span data-ttu-id="8b587-3029">A conta de usuário a ser representada para execução do programa Spark</span><span class="sxs-lookup"><span data-stu-id="8b587-3029">The user account to impersonate to execute the Spark program</span></span> | <span data-ttu-id="8b587-3030">Não</span><span class="sxs-lookup"><span data-stu-id="8b587-3030">No</span></span> | 
| <span data-ttu-id="8b587-3031">sparkConfig</span><span class="sxs-lookup"><span data-stu-id="8b587-3031">sparkConfig</span></span> | <span data-ttu-id="8b587-3032">Propriedades de configuração do Spark.</span><span class="sxs-lookup"><span data-stu-id="8b587-3032">Spark configuration properties.</span></span> | <span data-ttu-id="8b587-3033">Não</span><span class="sxs-lookup"><span data-stu-id="8b587-3033">No</span></span> | 
| <span data-ttu-id="8b587-3034">getDebugInfo</span><span class="sxs-lookup"><span data-stu-id="8b587-3034">getDebugInfo</span></span> | <span data-ttu-id="8b587-3035">Especifica quando os arquivos de log do Spark são copiados no armazenamento do Azure usado pelo cluster HDInsight (ou) especificado por sparkJobLinkedService.</span><span class="sxs-lookup"><span data-stu-id="8b587-3035">Specifies when the Spark log files are copied to the Azure storage used by HDInsight cluster (or) specified by sparkJobLinkedService.</span></span> <span data-ttu-id="8b587-3036">Valores permitidos: Nenhum, Sempre ou Falha.</span><span class="sxs-lookup"><span data-stu-id="8b587-3036">Allowed values: None, Always, or Failure.</span></span> <span data-ttu-id="8b587-3037">Valor padrão: Nenhum.</span><span class="sxs-lookup"><span data-stu-id="8b587-3037">Default value: None.</span></span> | <span data-ttu-id="8b587-3038">Não</span><span class="sxs-lookup"><span data-stu-id="8b587-3038">No</span></span> | 
| <span data-ttu-id="8b587-3039">sparkJobLinkedService</span><span class="sxs-lookup"><span data-stu-id="8b587-3039">sparkJobLinkedService</span></span> | <span data-ttu-id="8b587-3040">O serviço vinculado ao Armazenamento do Azure que contém o arquivo de trabalho, dependências e os logs do Spark.</span><span class="sxs-lookup"><span data-stu-id="8b587-3040">The Azure Storage linked service that holds the Spark job file, dependencies, and logs.</span></span>  <span data-ttu-id="8b587-3041">Se você não especificar um valor para essa propriedade, o armazenamento associado ao cluster HDInsight será usado.</span><span class="sxs-lookup"><span data-stu-id="8b587-3041">If you do not specify a value for this property, the storage associated with HDInsight cluster is used.</span></span> | <span data-ttu-id="8b587-3042">Não</span><span class="sxs-lookup"><span data-stu-id="8b587-3042">No</span></span> |

### <a name="json-example"></a><span data-ttu-id="8b587-3043">Exemplo de JSON</span><span class="sxs-lookup"><span data-stu-id="8b587-3043">JSON example</span></span>

```json
{
    "name": "SparkPipeline",
    "properties": {
        "activities": [
            {
                "type": "HDInsightSpark",
                "typeProperties": {
                    "rootPath": "adfspark\\pyFiles",
                    "entryFilePath": "test.py",
                    "getDebugInfo": "Always"
                },
                "outputs": [
                    {
                        "name": "OutputDataset"
                    }
                ],
                "name": "MySparkActivity",
                "linkedServiceName": "HDInsightLinkedService"
            }
        ],
        "start": "2017-02-05T00:00:00",
        "end": "2017-02-06T00:00:00"
    }
}
```
<span data-ttu-id="8b587-3044">Observe os seguintes pontos:</span><span class="sxs-lookup"><span data-stu-id="8b587-3044">Note the following points:</span></span> 

- <span data-ttu-id="8b587-3045">A propriedade **type** é definida como **HDInsightSpark**.</span><span class="sxs-lookup"><span data-stu-id="8b587-3045">The **type** property is set to **HDInsightSpark**.</span></span>
- <span data-ttu-id="8b587-3046">O **rootPath** é definido como **adfspark\\pyFiles**, onde adfspark é o contêiner de Blob do Azure e pyFiles é a pasta de arquivos nesse contêiner.</span><span class="sxs-lookup"><span data-stu-id="8b587-3046">The **rootPath** is set to **adfspark\\pyFiles** where adfspark is the Azure Blob container and pyFiles is fine folder in that container.</span></span> <span data-ttu-id="8b587-3047">Neste exemplo, o Armazenamento de Blobs do Azure é aquele que está associado ao cluster Spark.</span><span class="sxs-lookup"><span data-stu-id="8b587-3047">In this example, the Azure Blob Storage is the one that is associated with the Spark cluster.</span></span> <span data-ttu-id="8b587-3048">Você pode carregar o arquivo em um Armazenamento do Azure diferente.</span><span class="sxs-lookup"><span data-stu-id="8b587-3048">You can upload the file to a different Azure Storage.</span></span> <span data-ttu-id="8b587-3049">Se você fizer isso, crie um serviço vinculado do Armazenamento do Azure para vincular essa conta de armazenamento ao data factory.</span><span class="sxs-lookup"><span data-stu-id="8b587-3049">If you do so, create an Azure Storage linked service to link that storage account to the data factory.</span></span> <span data-ttu-id="8b587-3050">Em seguida, especifique o nome do serviço vinculado como um valor para a propriedade **sparkJobLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="8b587-3050">Then, specify the name of the linked service as a value for the **sparkJobLinkedService** property.</span></span> <span data-ttu-id="8b587-3051">Consulte [Propriedades de Atividade Spark](#spark-activity-properties) para obter detalhes sobre essa propriedade e outras propriedades às quais a atividade Spark dá suporte.</span><span class="sxs-lookup"><span data-stu-id="8b587-3051">See [Spark Activity properties](#spark-activity-properties) for details about this property and other properties supported by the Spark Activity.</span></span>
- <span data-ttu-id="8b587-3052">O **entryFilePath** é definido como **test.py**, que é o arquivo Python.</span><span class="sxs-lookup"><span data-stu-id="8b587-3052">The **entryFilePath** is set to the **test.py**, which is the python file.</span></span> 
- <span data-ttu-id="8b587-3053">A propriedade **getDebugInfo** é definida como **Always**, o que significa que os arquivos de log são gerados sempre (sucesso ou falha).</span><span class="sxs-lookup"><span data-stu-id="8b587-3053">The **getDebugInfo** property is set to **Always**, which means the log files are always generated (success or failure).</span></span>  

    > [!IMPORTANT]
    > <span data-ttu-id="8b587-3054">É recomendável que você não defina essa propriedade como Always em um ambiente de produção a menos que você esteja solucionando um problema.</span><span class="sxs-lookup"><span data-stu-id="8b587-3054">We recommend that you do not set this property to Always in a production environment unless you are troubleshooting an issue.</span></span> 
- <span data-ttu-id="8b587-3055">A seção **outputs** possui um conjunto de dados de saída.</span><span class="sxs-lookup"><span data-stu-id="8b587-3055">The **outputs** section has one output dataset.</span></span> <span data-ttu-id="8b587-3056">Você deve especificar um conjunto de dados de saída mesmo que o programa spark não produza nenhuma saída.</span><span class="sxs-lookup"><span data-stu-id="8b587-3056">You must specify an output dataset even if the spark program does not produce any output.</span></span> <span data-ttu-id="8b587-3057">O conjunto de dados de saída orienta o agendamento para o pipeline (por hora, diariamente, etc.).</span><span class="sxs-lookup"><span data-stu-id="8b587-3057">The output dataset drives the schedule for the pipeline (hourly, daily, etc.).</span></span>

<span data-ttu-id="8b587-3058">Para obter mais informações sobre a atividade, consulte o artigo [Atividade Spark](data-factory-spark.md).</span><span class="sxs-lookup"><span data-stu-id="8b587-3058">For more information about the activity, see [Spark Activity](data-factory-spark.md) article.</span></span>  

## <a name="machine-learning-batch-execution-activity"></a><span data-ttu-id="8b587-3059">Atividade de Execução em Lote de Machine Learning</span><span class="sxs-lookup"><span data-stu-id="8b587-3059">Machine Learning Batch Execution Activity</span></span>
<span data-ttu-id="8b587-3060">Você pode especificar as seguintes propriedades em uma definição de JSON de Atividade de Execução de Lote do Azure ML.</span><span class="sxs-lookup"><span data-stu-id="8b587-3060">You can specify the following properties in a Azure ML Batch Execution Activity JSON definition.</span></span> <span data-ttu-id="8b587-3061">A propriedade type para a atividade deve ser: **AzureMLBatchExecution**.</span><span class="sxs-lookup"><span data-stu-id="8b587-3061">The type property for the activity must be: **AzureMLBatchExecution**.</span></span> <span data-ttu-id="8b587-3062">Você deve primeiro criar um serviço vinculado do Azure Machine Learning e especificar o nome dele como um valor para a propriedade **linkedServiceName**.</span><span class="sxs-lookup"><span data-stu-id="8b587-3062">You must create a Azure Machine Learning linked service first and specify the name of it as a value for the **linkedServiceName** property.</span></span> <span data-ttu-id="8b587-3063">As propriedades a seguir possuem suporte na seção **typeProperties** quando você define o tipo de atividade para AzureMLBatchExecution:</span><span class="sxs-lookup"><span data-stu-id="8b587-3063">The following properties are supported in the **typeProperties** section when you set the type of activity to AzureMLBatchExecution:</span></span>

<span data-ttu-id="8b587-3064">Propriedade</span><span class="sxs-lookup"><span data-stu-id="8b587-3064">Property</span></span> | <span data-ttu-id="8b587-3065">Descrição</span><span class="sxs-lookup"><span data-stu-id="8b587-3065">Description</span></span> | <span data-ttu-id="8b587-3066">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="8b587-3066">Required</span></span> 
-------- | ----------- | --------
<span data-ttu-id="8b587-3067">webServiceInput</span><span class="sxs-lookup"><span data-stu-id="8b587-3067">webServiceInput</span></span> | <span data-ttu-id="8b587-3068">O conjunto de dados a ser passado como entrada para o serviço Web Azure ML.</span><span class="sxs-lookup"><span data-stu-id="8b587-3068">The dataset to be passed as an input for the Azure ML web service.</span></span> <span data-ttu-id="8b587-3069">Esse conjunto de dados também deve ser incluído nas entradas para a atividade.</span><span class="sxs-lookup"><span data-stu-id="8b587-3069">This dataset must also be included in the inputs for the activity.</span></span> |<span data-ttu-id="8b587-3070">Use webServiceInput ou webServiceInputs.</span><span class="sxs-lookup"><span data-stu-id="8b587-3070">Use either webServiceInput or webServiceInputs.</span></span> | 
<span data-ttu-id="8b587-3071">webServiceInputs</span><span class="sxs-lookup"><span data-stu-id="8b587-3071">webServiceInputs</span></span> | <span data-ttu-id="8b587-3072">Especifica os conjuntos de dados a serem passados como entradas para o serviço Web do Azure ML.</span><span class="sxs-lookup"><span data-stu-id="8b587-3072">Specify datasets to be passed as inputs for the Azure ML web service.</span></span> <span data-ttu-id="8b587-3073">Se o serviço Web receber várias entradas, use a propriedade webServiceInputs em vez de usar a propriedade webServiceInput.</span><span class="sxs-lookup"><span data-stu-id="8b587-3073">If the web service takes multiple inputs, use the webServiceInputs property instead of using the webServiceInput property.</span></span> <span data-ttu-id="8b587-3074">Os conjuntos de dados referenciados por **webServiceInputs** também devem ser incluídos nas **entradas** da Atividade.</span><span class="sxs-lookup"><span data-stu-id="8b587-3074">Datasets that are referenced by the **webServiceInputs** must also be included in the Activity **inputs**.</span></span> | <span data-ttu-id="8b587-3075">Use webServiceInput ou webServiceInputs.</span><span class="sxs-lookup"><span data-stu-id="8b587-3075">Use either webServiceInput or webServiceInputs.</span></span> | 
<span data-ttu-id="8b587-3076">webServiceOutputs</span><span class="sxs-lookup"><span data-stu-id="8b587-3076">webServiceOutputs</span></span> | <span data-ttu-id="8b587-3077">Os conjuntos de dados que são atribuídos como saídas para o serviço Web do Azure ML.</span><span class="sxs-lookup"><span data-stu-id="8b587-3077">The datasets that are assigned as outputs for the Azure ML web service.</span></span> <span data-ttu-id="8b587-3078">O serviço Web retorna dados de saída neste conjunto de dados.</span><span class="sxs-lookup"><span data-stu-id="8b587-3078">The web service returns output data in this dataset.</span></span> | <span data-ttu-id="8b587-3079">Sim</span><span class="sxs-lookup"><span data-stu-id="8b587-3079">Yes</span></span> | 
<span data-ttu-id="8b587-3080">globalParameters</span><span class="sxs-lookup"><span data-stu-id="8b587-3080">globalParameters</span></span> | <span data-ttu-id="8b587-3081">Especifica valores para parâmetros de serviço Web nesta seção.</span><span class="sxs-lookup"><span data-stu-id="8b587-3081">Specify values for the web service parameters in this section.</span></span> | <span data-ttu-id="8b587-3082">Não</span><span class="sxs-lookup"><span data-stu-id="8b587-3082">No</span></span> | 

### <a name="json-example"></a><span data-ttu-id="8b587-3083">Exemplo de JSON</span><span class="sxs-lookup"><span data-stu-id="8b587-3083">JSON example</span></span>
<span data-ttu-id="8b587-3084">Neste exemplo, a atividade possui o conjunto de dados **MLSqlInput** como entrada e **MLSqlOutput** como a saída.</span><span class="sxs-lookup"><span data-stu-id="8b587-3084">In this example, the activity has the dataset **MLSqlInput** as input and **MLSqlOutput** as the output.</span></span> <span data-ttu-id="8b587-3085">O **MLSqlInput** é passado como uma entrada para o serviço Web usando a propriedade JSON **webServiceInput**.</span><span class="sxs-lookup"><span data-stu-id="8b587-3085">The **MLSqlInput** is passed as an input to the web service by using the **webServiceInput** JSON property.</span></span> <span data-ttu-id="8b587-3086">O **MLSqlOutput** é passado como uma entrada para o serviço Web usando a propriedade JSON **webServiceOutputs**.</span><span class="sxs-lookup"><span data-stu-id="8b587-3086">The **MLSqlOutput** is passed as an output to the Web service by using the **webServiceOutputs** JSON property.</span></span> 

```json
{
   "name": "MLWithSqlReaderSqlWriter",
   "properties": {
      "description": "Azure ML model with sql azure reader/writer",
      "activities": [{
         "name": "MLSqlReaderSqlWriterActivity",
         "type": "AzureMLBatchExecution",
         "description": "test",
         "inputs": [ { "name": "MLSqlInput" }],
         "outputs": [ { "name": "MLSqlOutput" } ],
         "linkedServiceName": "MLSqlReaderSqlWriterDecisionTreeModel",
         "typeProperties":
         {
            "webServiceInput": "MLSqlInput",
            "webServiceOutputs": {
               "output1": "MLSqlOutput"
            },
            "globalParameters": {
               "Database server name": "<myserver>.database.windows.net",
               "Database name": "<database>",
               "Server user account name": "<user name>",
               "Server user account password": "<password>"
            }              
         },
         "policy": {
            "concurrency": 1,
            "executionPriorityOrder": "NewestFirst",
            "retry": 1,
            "timeout": "02:00:00"
         }
      }],
      "start": "2016-02-13T00:00:00",
       "end": "2016-02-14T00:00:00"
   }
}
```

<span data-ttu-id="8b587-3087">No exemplo do JSON, o serviço Web do Machine Learning implantado usa um módulo leitor e gravador para ler/gravar dados de/para um Banco de Dados SQL do Azure.</span><span class="sxs-lookup"><span data-stu-id="8b587-3087">In the JSON example, the deployed Azure Machine Learning Web service uses a reader and a writer module to read/write data from/to an Azure SQL Database.</span></span> <span data-ttu-id="8b587-3088">Este serviço Web expõe os seguintes quatro parâmetros: Nome do servidor de banco de dados, Nome do banco de dados, Nome de conta de usuário do servidor e Senha de conta de usuário do servidor.</span><span class="sxs-lookup"><span data-stu-id="8b587-3088">This Web service exposes the following four parameters:  Database server name, Database name, Server user account name, and Server user account password.</span></span>

> [!NOTE]
> <span data-ttu-id="8b587-3089">Apenas as entradas e saídas da atividade AzureMLBatchExecution podem ser passadas como parâmetros para o serviço Web.</span><span class="sxs-lookup"><span data-stu-id="8b587-3089">Only inputs and outputs of the AzureMLBatchExecution activity can be passed as parameters to the Web service.</span></span> <span data-ttu-id="8b587-3090">Por exemplo, no trecho JSON acima, MLSqlInput é uma entrada para a atividade de AzureMLBatchExecution, que é passada como entrada para o serviço Web através do parâmetro webServiceInput.</span><span class="sxs-lookup"><span data-stu-id="8b587-3090">For example, in the above JSON snippet, MLSqlInput is an input to the AzureMLBatchExecution activity, which is passed as an input to the Web service via webServiceInput parameter.</span></span>

## <a name="machine-learning-update-resource-activity"></a><span data-ttu-id="8b587-3091">Atividade de Atualização de Recursos do Machine Learning</span><span class="sxs-lookup"><span data-stu-id="8b587-3091">Machine Learning Update Resource Activity</span></span>
<span data-ttu-id="8b587-3092">Você pode especificar as seguintes propriedades em uma definição de JSON de Atualização de Recursos do Azure ML.</span><span class="sxs-lookup"><span data-stu-id="8b587-3092">You can specify the following properties in a Azure ML Update Resource Activity JSON definition.</span></span> <span data-ttu-id="8b587-3093">A propriedade type para a atividade deve ser: **AzureMLUpdateResource**.</span><span class="sxs-lookup"><span data-stu-id="8b587-3093">The type property for the activity must be: **AzureMLUpdateResource**.</span></span> <span data-ttu-id="8b587-3094">Você deve primeiro criar um serviço vinculado do Azure Machine Learning e especificar o nome dele como um valor para a propriedade **linkedServiceName**.</span><span class="sxs-lookup"><span data-stu-id="8b587-3094">You must create a Azure Machine Learning linked service first and specify the name of it as a value for the **linkedServiceName** property.</span></span> <span data-ttu-id="8b587-3095">As propriedades a seguir possuem suporte na seção **typeProperties** quando você define o tipo de atividade para AzureMLUpdateResource:</span><span class="sxs-lookup"><span data-stu-id="8b587-3095">The following properties are supported in the **typeProperties** section when you set the type of activity to AzureMLUpdateResource:</span></span>

<span data-ttu-id="8b587-3096">Propriedade</span><span class="sxs-lookup"><span data-stu-id="8b587-3096">Property</span></span> | <span data-ttu-id="8b587-3097">Descrição</span><span class="sxs-lookup"><span data-stu-id="8b587-3097">Description</span></span> | <span data-ttu-id="8b587-3098">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="8b587-3098">Required</span></span> 
-------- | ----------- | --------
<span data-ttu-id="8b587-3099">trainedModelName</span><span class="sxs-lookup"><span data-stu-id="8b587-3099">trainedModelName</span></span> | <span data-ttu-id="8b587-3100">Nome do modelo treinado novamente.</span><span class="sxs-lookup"><span data-stu-id="8b587-3100">Name of the retrained model.</span></span> | <span data-ttu-id="8b587-3101">Sim</span><span class="sxs-lookup"><span data-stu-id="8b587-3101">Yes</span></span> |  
<span data-ttu-id="8b587-3102">trainedModelDatasetName</span><span class="sxs-lookup"><span data-stu-id="8b587-3102">trainedModelDatasetName</span></span> | <span data-ttu-id="8b587-3103">O conjunto de dados apontando para o arquivo iLearner retornado pela operação de novos treinamentos.</span><span class="sxs-lookup"><span data-stu-id="8b587-3103">Dataset pointing to the iLearner file returned by the retraining operation.</span></span> | <span data-ttu-id="8b587-3104">Sim</span><span class="sxs-lookup"><span data-stu-id="8b587-3104">Yes</span></span> | 

### <a name="json-example"></a><span data-ttu-id="8b587-3105">Exemplo de JSON</span><span class="sxs-lookup"><span data-stu-id="8b587-3105">JSON example</span></span>
<span data-ttu-id="8b587-3106">O pipeline tem duas atividades: **AzureMLBatchExecution** e **AzureMLUpdateResource**.</span><span class="sxs-lookup"><span data-stu-id="8b587-3106">The pipeline has two activities: **AzureMLBatchExecution** and **AzureMLUpdateResource**.</span></span> <span data-ttu-id="8b587-3107">A atividade de Execução em lote do AM do Azure usa os dados de treinamento como entrada e produz um arquivo iLearner como saída.</span><span class="sxs-lookup"><span data-stu-id="8b587-3107">The Azure ML Batch Execution activity takes the training data as input and produces an iLearner file as an output.</span></span> <span data-ttu-id="8b587-3108">A atividade invoca o serviço Web de treinamento (experimento de treinamento exposto como um serviço Web) com os dados de treinamento de entrada e recebe o arquivo ilearner do serviço Web.</span><span class="sxs-lookup"><span data-stu-id="8b587-3108">The activity invokes the training web service (training experiment exposed as a web service) with the input training data and receives the ilearner file from the webservice.</span></span> <span data-ttu-id="8b587-3109">O placeholderBlob é apenas um conjunto de dados de saída fictício necessário ao serviço Azure Data Factory para executar o pipeline.</span><span class="sxs-lookup"><span data-stu-id="8b587-3109">The placeholderBlob is just a dummy output dataset that is required by the Azure Data Factory service to run the pipeline.</span></span>


```json
{
    "name": "pipeline",
    "properties": {
        "activities": [
            {
                "name": "retraining",
                "type": "AzureMLBatchExecution",
                "inputs": [
                    {
                        "name": "trainingData"
                    }
                ],
                "outputs": [
                    {
                        "name": "trainedModelBlob"
                    }
                ],
                "typeProperties": {
                    "webServiceInput": "trainingData",
                    "webServiceOutputs": {
                        "output1": "trainedModelBlob"
                    }              
                 },
                "linkedServiceName": "trainingEndpoint",
                "policy": {
                    "concurrency": 1,
                    "executionPriorityOrder": "NewestFirst",
                    "retry": 1,
                    "timeout": "02:00:00"
                }
            },
            {
                "type": "AzureMLUpdateResource",
                "typeProperties": {
                    "trainedModelName": "trained model",
                    "trainedModelDatasetName" :  "trainedModelBlob"
                },
                "inputs": [{ "name": "trainedModelBlob" }],
                "outputs": [{ "name": "placeholderBlob" }],
                "policy": {
                    "timeout": "01:00:00",
                    "concurrency": 1,
                    "retry": 3
                },
                "name": "AzureML Update Resource",
                "linkedServiceName": "updatableScoringEndpoint2"
            }
        ],
        "start": "2016-02-13T00:00:00",
        "end": "2016-02-14T00:00:00"
    }
}
```

## <a name="data-lake-analytics-u-sql-activity"></a><span data-ttu-id="8b587-3110">Atividade do U-SQL da Análise Data Lake</span><span class="sxs-lookup"><span data-stu-id="8b587-3110">Data Lake Analytics U-SQL Activity</span></span>
<span data-ttu-id="8b587-3111">Você pode especificar as seguintes propriedades em uma definição de JSON de atividade de U-SQL.</span><span class="sxs-lookup"><span data-stu-id="8b587-3111">You can specify the following properties in a U-SQL Activity JSON definition.</span></span> <span data-ttu-id="8b587-3112">A propriedade type para a atividade deve ser: **DataLakeAnalyticsU-SQL**.</span><span class="sxs-lookup"><span data-stu-id="8b587-3112">The type property for the activity must be: **DataLakeAnalyticsU-SQL**.</span></span> <span data-ttu-id="8b587-3113">Você deve primeiro criar um serviço vinculado do Azure Data Lake Analytics e especificar o nome dele como um valor para a propriedade **linkedServiceName**.</span><span class="sxs-lookup"><span data-stu-id="8b587-3113">You must create an Azure Data Lake Analytics linked service and specify the name of it as a value for the **linkedServiceName** property.</span></span> <span data-ttu-id="8b587-3114">As propriedades a seguir possuem suporte na seção **typeProperties** quando você define o tipo de atividade para DataLakeAnalyticsU-SQL:</span><span class="sxs-lookup"><span data-stu-id="8b587-3114">The following properties are supported in the **typeProperties** section when you set the type of activity to DataLakeAnalyticsU-SQL:</span></span> 

| <span data-ttu-id="8b587-3115">Propriedade</span><span class="sxs-lookup"><span data-stu-id="8b587-3115">Property</span></span> | <span data-ttu-id="8b587-3116">Descrição</span><span class="sxs-lookup"><span data-stu-id="8b587-3116">Description</span></span> | <span data-ttu-id="8b587-3117">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="8b587-3117">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="8b587-3118">scriptPath</span><span class="sxs-lookup"><span data-stu-id="8b587-3118">scriptPath</span></span> |<span data-ttu-id="8b587-3119">Caminho para a pasta que contém o script U-SQL.</span><span class="sxs-lookup"><span data-stu-id="8b587-3119">Path to folder that contains the U-SQL script.</span></span> <span data-ttu-id="8b587-3120">O nome do arquivo diferencia maiúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="8b587-3120">Name of the file is case-sensitive.</span></span> |<span data-ttu-id="8b587-3121">Não (se você usar o script)</span><span class="sxs-lookup"><span data-stu-id="8b587-3121">No (if you use script)</span></span> |
| <span data-ttu-id="8b587-3122">scriptLinkedService</span><span class="sxs-lookup"><span data-stu-id="8b587-3122">scriptLinkedService</span></span> |<span data-ttu-id="8b587-3123">Serviço vinculado que vincula o armazenamento que contém o script para a fábrica de dados</span><span class="sxs-lookup"><span data-stu-id="8b587-3123">Linked service that links the storage that contains the script to the data factory</span></span> |<span data-ttu-id="8b587-3124">Não (se você usar o script)</span><span class="sxs-lookup"><span data-stu-id="8b587-3124">No (if you use script)</span></span> |
| <span data-ttu-id="8b587-3125">script</span><span class="sxs-lookup"><span data-stu-id="8b587-3125">script</span></span> |<span data-ttu-id="8b587-3126">Especificar script embutido em vez de especificar scriptPath e scriptLinkedService.</span><span class="sxs-lookup"><span data-stu-id="8b587-3126">Specify inline script instead of specifying scriptPath and scriptLinkedService.</span></span> <span data-ttu-id="8b587-3127">Por exemplo: "script": "CREATE DATABASE test".</span><span class="sxs-lookup"><span data-stu-id="8b587-3127">For example: "script": "CREATE DATABASE test".</span></span> |<span data-ttu-id="8b587-3128">Não (se você usar scriptPath e scriptLinkedService)</span><span class="sxs-lookup"><span data-stu-id="8b587-3128">No (if you use scriptPath and scriptLinkedService)</span></span> |
| <span data-ttu-id="8b587-3129">degreeOfParallelism</span><span class="sxs-lookup"><span data-stu-id="8b587-3129">degreeOfParallelism</span></span> |<span data-ttu-id="8b587-3130">O número máximo de nós usados simultaneamente para executar o trabalho.</span><span class="sxs-lookup"><span data-stu-id="8b587-3130">The maximum number of nodes simultaneously used to run the job.</span></span> |<span data-ttu-id="8b587-3131">Não</span><span class="sxs-lookup"><span data-stu-id="8b587-3131">No</span></span> |
| <span data-ttu-id="8b587-3132">prioridade</span><span class="sxs-lookup"><span data-stu-id="8b587-3132">priority</span></span> |<span data-ttu-id="8b587-3133">Determina quais trabalhos de todos os que estão na fila devem ser selecionados para serem executados primeiro.</span><span class="sxs-lookup"><span data-stu-id="8b587-3133">Determines which jobs out of all that are queued should be selected to run first.</span></span> <span data-ttu-id="8b587-3134">Quanto menor o número, maior a prioridade.</span><span class="sxs-lookup"><span data-stu-id="8b587-3134">The lower the number, the higher the priority.</span></span> |<span data-ttu-id="8b587-3135">Não</span><span class="sxs-lookup"><span data-stu-id="8b587-3135">No</span></span> |
| <span data-ttu-id="8b587-3136">parameters</span><span class="sxs-lookup"><span data-stu-id="8b587-3136">parameters</span></span> |<span data-ttu-id="8b587-3137">Parâmetros do script U-SQL</span><span class="sxs-lookup"><span data-stu-id="8b587-3137">Parameters for the U-SQL script</span></span> |<span data-ttu-id="8b587-3138">Não</span><span class="sxs-lookup"><span data-stu-id="8b587-3138">No</span></span> |

### <a name="json-example"></a><span data-ttu-id="8b587-3139">Exemplo de JSON</span><span class="sxs-lookup"><span data-stu-id="8b587-3139">JSON example</span></span>

```json
{
    "name": "ComputeEventsByRegionPipeline",
    "properties": {
        "description": "This pipeline computes events for en-gb locale and date less than Feb 19, 2012.",
        "activities": 
        [
            {
                "type": "DataLakeAnalyticsU-SQL",
                "typeProperties": {
                    "scriptPath": "scripts\\kona\\SearchLogProcessing.txt",
                    "scriptLinkedService": "StorageLinkedService",
                    "degreeOfParallelism": 3,
                    "priority": 100,
                    "parameters": {
                        "in": "/datalake/input/SearchLog.tsv",
                        "out": "/datalake/output/Result.tsv"
                    }
                },
                "inputs": [
                    {
                        "name": "DataLakeTable"
                    }
                ],
                "outputs": 
                [
                    {
                        "name": "EventsByRegionTable"
                    }
                ],
                "policy": {
                    "timeout": "06:00:00",
                    "concurrency": 1,
                    "executionPriorityOrder": "NewestFirst",
                    "retry": 1
                },
                "scheduler": {
                    "frequency": "Day",
                    "interval": 1
                },
                "name": "EventsByRegion",
                "linkedServiceName": "AzureDataLakeAnalyticsLinkedService"
            }
        ],
        "start": "2015-08-08T00:00:00",
        "end": "2015-08-08T01:00:00",
        "isPaused": false
    }
}
```

<span data-ttu-id="8b587-3140">Para saber mais, consulte [Atividade de U-SQL no Data Lake Analytics](data-factory-usql-activity.md).</span><span class="sxs-lookup"><span data-stu-id="8b587-3140">For more information, see [Data Lake Analytics U-SQL Activity](data-factory-usql-activity.md).</span></span> 

## <a name="stored-procedure-activity"></a><span data-ttu-id="8b587-3141">Atividade de Procedimento Armazenado</span><span class="sxs-lookup"><span data-stu-id="8b587-3141">Stored Procedure Activity</span></span>
<span data-ttu-id="8b587-3142">Você pode especificar as seguintes propriedades em uma definição de JSON de Atividade de Procedimento de Armazenado.</span><span class="sxs-lookup"><span data-stu-id="8b587-3142">You can specify the following properties in a Stored Procedure Activity JSON definition.</span></span> <span data-ttu-id="8b587-3143">A propriedade type para a atividade deve ser: **SqlServerStoredProcedure**.</span><span class="sxs-lookup"><span data-stu-id="8b587-3143">The type property for the activity must be: **SqlServerStoredProcedure**.</span></span> <span data-ttu-id="8b587-3144">Você deve primeiro criar um dos serviços vinculados a seguir e especificar o nome do serviço vinculado como um valor para a propriedade **linkedServiceName**.</span><span class="sxs-lookup"><span data-stu-id="8b587-3144">You must create an one of the following linked services and specify the name of the linked service as a value for the **linkedServiceName** property:</span></span>

- <span data-ttu-id="8b587-3145">SQL Server</span><span class="sxs-lookup"><span data-stu-id="8b587-3145">SQL Server</span></span> 
- <span data-ttu-id="8b587-3146">Banco de Dados SQL do Azure</span><span class="sxs-lookup"><span data-stu-id="8b587-3146">Azure SQL Database</span></span>
- <span data-ttu-id="8b587-3147">SQL Data Warehouse do Azure</span><span class="sxs-lookup"><span data-stu-id="8b587-3147">Azure SQL Data Warehouse</span></span>

<span data-ttu-id="8b587-3148">As propriedades a seguir possuem suporte na seção **typeProperties** quando você define o tipo de atividade para SqlServerStoredProcedure:</span><span class="sxs-lookup"><span data-stu-id="8b587-3148">The following properties are supported in the **typeProperties** section when you set the type of activity to SqlServerStoredProcedure:</span></span>

| <span data-ttu-id="8b587-3149">Propriedade</span><span class="sxs-lookup"><span data-stu-id="8b587-3149">Property</span></span> | <span data-ttu-id="8b587-3150">Descrição</span><span class="sxs-lookup"><span data-stu-id="8b587-3150">Description</span></span> | <span data-ttu-id="8b587-3151">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="8b587-3151">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8b587-3152">storedProcedureName</span><span class="sxs-lookup"><span data-stu-id="8b587-3152">storedProcedureName</span></span> |<span data-ttu-id="8b587-3153">Especifique o nome do procedimento armazenado no banco de dados SQL do Azure ou SQL Data Warehouse do Azure que é representado pelo serviço vinculado utilizado pela tabela de saída.</span><span class="sxs-lookup"><span data-stu-id="8b587-3153">Specify the name of the stored procedure in the Azure SQL database or Azure SQL Data Warehouse that is represented by the linked service that the output table uses.</span></span> |<span data-ttu-id="8b587-3154">Sim</span><span class="sxs-lookup"><span data-stu-id="8b587-3154">Yes</span></span> |
| <span data-ttu-id="8b587-3155">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="8b587-3155">storedProcedureParameters</span></span> |<span data-ttu-id="8b587-3156">Especifique valores para parâmetros de procedimento armazenado.</span><span class="sxs-lookup"><span data-stu-id="8b587-3156">Specify values for stored procedure parameters.</span></span> <span data-ttu-id="8b587-3157">Se você precisar passar null para um parâmetro, use a sintaxe: "param1": null (todas as letras minúsculas).</span><span class="sxs-lookup"><span data-stu-id="8b587-3157">If you need to pass null for a parameter, use the syntax: "param1": null (all lower case).</span></span> <span data-ttu-id="8b587-3158">Veja o exemplo a seguir para saber mais sobre como usar essa propriedade.</span><span class="sxs-lookup"><span data-stu-id="8b587-3158">See the following sample to learn about using this property.</span></span> |<span data-ttu-id="8b587-3159">Não</span><span class="sxs-lookup"><span data-stu-id="8b587-3159">No</span></span> |

<span data-ttu-id="8b587-3160">Se você especificar um conjunto de dados de entrada, ele deverá estar disponível (no status 'Pronto') para a atividade de procedimento armazenado a ser executada.</span><span class="sxs-lookup"><span data-stu-id="8b587-3160">If you do specify an input dataset, it must be available (in ‘Ready’ status) for the stored procedure activity to run.</span></span> <span data-ttu-id="8b587-3161">O conjunto de dados de entrada não pode ser consumido no procedimento armazenado como um parâmetro.</span><span class="sxs-lookup"><span data-stu-id="8b587-3161">The input dataset cannot be consumed in the stored procedure as a parameter.</span></span> <span data-ttu-id="8b587-3162">Ele só é usado para verificar a dependência antes de iniciar a atividade de procedimento armazenado.</span><span class="sxs-lookup"><span data-stu-id="8b587-3162">It is only used to check the dependency before starting the stored procedure activity.</span></span> <span data-ttu-id="8b587-3163">Você deve especificar um conjunto de dados de saída para uma atividade de procedimento armazenado.</span><span class="sxs-lookup"><span data-stu-id="8b587-3163">You must specify an output dataset for a stored procedure activity.</span></span> 

<span data-ttu-id="8b587-3164">O conjunto de dados de saída especifica a **agenda** da atividade de procedimento armazenado (por hora, semana, mês, etc.).</span><span class="sxs-lookup"><span data-stu-id="8b587-3164">Output dataset specifies the **schedule** for the stored procedure activity (hourly, weekly, monthly, etc.).</span></span> <span data-ttu-id="8b587-3165">O conjunto de dados de saída deve usar um **serviço vinculado** que se refere a um Banco de Dados SQL do Azure, ou SQL Data Warehouse do Azure, ou um Banco de Dados SQL Server no qual você quer que o procedimento armazenado seja executado.</span><span class="sxs-lookup"><span data-stu-id="8b587-3165">The output dataset must use a **linked service** that refers to an Azure SQL Database or an Azure SQL Data Warehouse or a SQL Server Database in which you want the stored procedure to run.</span></span> <span data-ttu-id="8b587-3166">O conjunto de dados de saída pode servir como uma maneira de passar o resultado do procedimento armazenado para processamento posterior de outra atividade ([atividades de encadeamento](data-factory-scheduling-and-execution.md##multiple-activities-in-a-pipeline)) no pipeline.</span><span class="sxs-lookup"><span data-stu-id="8b587-3166">The output dataset can serve as a way to pass the result of the stored procedure for subsequent processing by another activity ([chaining activities](data-factory-scheduling-and-execution.md##multiple-activities-in-a-pipeline)) in the pipeline.</span></span> <span data-ttu-id="8b587-3167">No entanto, o Data Factory não trava automaticamente a saída de um procedimento armazenado para esse conjunto de dados.</span><span class="sxs-lookup"><span data-stu-id="8b587-3167">However, Data Factory does not automatically write the output of a stored procedure to this dataset.</span></span> <span data-ttu-id="8b587-3168">É o procedimento armazenado que grava em uma tabela SQL para a qual o conjunto de dados de saída aponta.</span><span class="sxs-lookup"><span data-stu-id="8b587-3168">It is the stored procedure that writes to a SQL table that the output dataset points to.</span></span> <span data-ttu-id="8b587-3169">Em alguns casos, o conjunto de dados de saída pode ser um **conjunto de dados fictício**, que é usado apenas para especificar o agendamento para execução da atividade de procedimento armazenado.</span><span class="sxs-lookup"><span data-stu-id="8b587-3169">In some cases, the output dataset can be a **dummy dataset**, which is used only to specify the schedule for running the stored procedure activity.</span></span>  

### <a name="json-example"></a><span data-ttu-id="8b587-3170">Exemplo de JSON</span><span class="sxs-lookup"><span data-stu-id="8b587-3170">JSON example</span></span>

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
                "outputs": [{ "name": "sprocsampleout" }],
                "name": "SprocActivitySample"
            }
        ],
         "start": "2016-08-02T00:00:00",
         "end": "2016-08-02T05:00:00",
        "isPaused": false
    }
}
```

<span data-ttu-id="8b587-3171">Para saber mais, consulte o artigo [Atividade de Procedimento Armazenado](data-factory-stored-proc-activity.md).</span><span class="sxs-lookup"><span data-stu-id="8b587-3171">For more information, see [Stored Procedure Activity](data-factory-stored-proc-activity.md) article.</span></span> 

## <a name="net-custom-activity"></a><span data-ttu-id="8b587-3172">Atividade personalizada do .NET</span><span class="sxs-lookup"><span data-stu-id="8b587-3172">.NET custom activity</span></span>
<span data-ttu-id="8b587-3173">Você pode especificar as seguintes propriedades em uma definição de JSON de atividade personalizada de .NET.</span><span class="sxs-lookup"><span data-stu-id="8b587-3173">You can specify the following properties in a .NET custom activity JSON definition.</span></span> <span data-ttu-id="8b587-3174">A propriedade type para a atividade deve ser: **DotNetActivity**.</span><span class="sxs-lookup"><span data-stu-id="8b587-3174">The type property for the activity must be: **DotNetActivity**.</span></span> <span data-ttu-id="8b587-3175">Você deve primeiro criar um serviço vinculado do Azure HDInsight ou um serviço vinculado do Lote do Azure e especificar o nome do serviço vinculado como um valor para a propriedade **linkedServiceName**.</span><span class="sxs-lookup"><span data-stu-id="8b587-3175">You must create an Azure HDInsight linked service or an Azure Batch linked service, and specify the name of the linked service as a value for the **linkedServiceName** property.</span></span> <span data-ttu-id="8b587-3176">As propriedades a seguir possuem suporte na seção **typeProperties** quando você define o tipo de atividade para DotNetActivity:</span><span class="sxs-lookup"><span data-stu-id="8b587-3176">The following properties are supported in the **typeProperties** section when you set the type of activity to DotNetActivity:</span></span>
 
| <span data-ttu-id="8b587-3177">Propriedade</span><span class="sxs-lookup"><span data-stu-id="8b587-3177">Property</span></span> | <span data-ttu-id="8b587-3178">Descrição</span><span class="sxs-lookup"><span data-stu-id="8b587-3178">Description</span></span> | <span data-ttu-id="8b587-3179">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="8b587-3179">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="8b587-3180">AssemblyName</span><span class="sxs-lookup"><span data-stu-id="8b587-3180">AssemblyName</span></span> | <span data-ttu-id="8b587-3181">Nome do assembly.</span><span class="sxs-lookup"><span data-stu-id="8b587-3181">Name of the assembly.</span></span> <span data-ttu-id="8b587-3182">No exemplo, é: **MyDotnetActivity.dll**.</span><span class="sxs-lookup"><span data-stu-id="8b587-3182">In the example, it is: **MyDotnetActivity.dll**.</span></span> | <span data-ttu-id="8b587-3183">Sim</span><span class="sxs-lookup"><span data-stu-id="8b587-3183">Yes</span></span> |
| <span data-ttu-id="8b587-3184">EntryPoint</span><span class="sxs-lookup"><span data-stu-id="8b587-3184">EntryPoint</span></span> |<span data-ttu-id="8b587-3185">Nome da classe que implementa a interface IDotNetActivity.</span><span class="sxs-lookup"><span data-stu-id="8b587-3185">Name of the class that implements the IDotNetActivity interface.</span></span> <span data-ttu-id="8b587-3186">No exemplo, é: **MyDotNetActivityNS.MyDotNetActivity** onde MyDotNetActivityNS é o namespace e MyDotNetActivity é a classe.</span><span class="sxs-lookup"><span data-stu-id="8b587-3186">In the example, it is: **MyDotNetActivityNS.MyDotNetActivity** where MyDotNetActivityNS is the namespace and MyDotNetActivity is the class.</span></span>  | <span data-ttu-id="8b587-3187">Sim</span><span class="sxs-lookup"><span data-stu-id="8b587-3187">Yes</span></span> | 
| <span data-ttu-id="8b587-3188">PackageLinkedService</span><span class="sxs-lookup"><span data-stu-id="8b587-3188">PackageLinkedService</span></span> | <span data-ttu-id="8b587-3189">Nome do serviço vinculado do Armazenamento do Azure que aponta para o armazenamento de blobs que contém o arquivo zip da atividade personalizada.</span><span class="sxs-lookup"><span data-stu-id="8b587-3189">Name of the Azure Storage linked service that points to the blob storage that contains the custom activity zip file.</span></span> <span data-ttu-id="8b587-3190">No exemplo, é: **AzureStorageLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="8b587-3190">In the example, it is: **AzureStorageLinkedService**.</span></span>| <span data-ttu-id="8b587-3191">Sim</span><span class="sxs-lookup"><span data-stu-id="8b587-3191">Yes</span></span> |
| <span data-ttu-id="8b587-3192">PackageFile</span><span class="sxs-lookup"><span data-stu-id="8b587-3192">PackageFile</span></span> | <span data-ttu-id="8b587-3193">Nome do arquivo zip.</span><span class="sxs-lookup"><span data-stu-id="8b587-3193">Name of the zip file.</span></span> <span data-ttu-id="8b587-3194">No exemplo, é: **customactivitycontainer/MyDotNetActivity.zip**.</span><span class="sxs-lookup"><span data-stu-id="8b587-3194">In the example, it is: **customactivitycontainer/MyDotNetActivity.zip**.</span></span> | <span data-ttu-id="8b587-3195">Sim</span><span class="sxs-lookup"><span data-stu-id="8b587-3195">Yes</span></span> |
| <span data-ttu-id="8b587-3196">extendedProperties</span><span class="sxs-lookup"><span data-stu-id="8b587-3196">extendedProperties</span></span> | <span data-ttu-id="8b587-3197">Propriedades estendidas que você pode definir e passar para o código .NET.</span><span class="sxs-lookup"><span data-stu-id="8b587-3197">Extended properties that you can define and pass on to the .NET code.</span></span> <span data-ttu-id="8b587-3198">Neste exemplo, a variável **SliceStart** é definida para um valor baseado na variável de sistema SliceStart.</span><span class="sxs-lookup"><span data-stu-id="8b587-3198">In this example, the **SliceStart** variable is set to a value based on the SliceStart system variable.</span></span> | <span data-ttu-id="8b587-3199">Não</span><span class="sxs-lookup"><span data-stu-id="8b587-3199">No</span></span> | 

### <a name="json-example"></a><span data-ttu-id="8b587-3200">Exemplo de JSON</span><span class="sxs-lookup"><span data-stu-id="8b587-3200">JSON example</span></span>

```json
{
  "name": "ADFTutorialPipelineCustom",
  "properties": {
    "description": "Use custom activity",
    "activities": [
      {
        "Name": "MyDotNetActivity",
        "Type": "DotNetActivity",
        "Inputs": [
          {
            "Name": "InputDataset"
          }
        ],
        "Outputs": [
          {
            "Name": "OutputDataset"
          }
        ],
        "LinkedServiceName": "AzureBatchLinkedService",
        "typeProperties": {
          "AssemblyName": "MyDotNetActivity.dll",
          "EntryPoint": "MyDotNetActivityNS.MyDotNetActivity",
          "PackageLinkedService": "AzureStorageLinkedService",
          "PackageFile": "customactivitycontainer/MyDotNetActivity.zip",
          "extendedProperties": {
            "SliceStart": "$$Text.Format('{0:yyyyMMddHH-mm}', Time.AddMinutes(SliceStart, 0))"
          }
        },
        "Policy": {
          "Concurrency": 2,
          "ExecutionPriorityOrder": "OldestFirst",
          "Retry": 3,
          "Timeout": "00:30:00",
          "Delay": "00:00:00"
        }
      }
    ],
    "start": "2016-11-16T00:00:00",
    "end": "2016-11-16T05:00:00",
    "isPaused": false
  }
}
```

<span data-ttu-id="8b587-3201">Para saber informações detalhadas, consulte o artigo [Usar atividades personalizadas no Data Factory](data-factory-use-custom-activities.md).</span><span class="sxs-lookup"><span data-stu-id="8b587-3201">For detailed information, see [Use custom activities in Data Factory](data-factory-use-custom-activities.md) article.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="8b587-3202">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="8b587-3202">Next Steps</span></span>
<span data-ttu-id="8b587-3203">Consulte os seguintes tutoriais:</span><span class="sxs-lookup"><span data-stu-id="8b587-3203">See the following tutorials:</span></span> 

- [<span data-ttu-id="8b587-3204">Tutorial: Criar um pipeline com uma atividade de cópia</span><span class="sxs-lookup"><span data-stu-id="8b587-3204">Tutorial: create a pipeline with a copy activity</span></span>](data-factory-copy-activity-tutorial-using-azure-portal.md)
- [<span data-ttu-id="8b587-3205">Tutorial: Criar um pipeline com uma atividade de hive</span><span class="sxs-lookup"><span data-stu-id="8b587-3205">Tutorial: create a pipeline with a hive activity</span></span>](data-factory-build-your-first-pipeline-using-editor.md)