---
title: "aaaAzure Data Factory - referência de script JSON | Microsoft Docs"
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
ms.openlocfilehash: 813fd752bb0ecb1b513d022b9f302325105dac31
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-data-factory---json-scripting-reference"></a><span data-ttu-id="ed017-103">Azure Data Factory - Referência de Script do JSON</span><span class="sxs-lookup"><span data-stu-id="ed017-103">Azure Data Factory - JSON Scripting Reference</span></span>
<span data-ttu-id="ed017-104">Este artigo fornece esquemas JSON e exemplos para definir entidades do Azure Data Factory (pipeline, atividade, conjunto de dados e serviço vinculado).</span><span class="sxs-lookup"><span data-stu-id="ed017-104">This article provides JSON schemas and examples for defining Azure Data Factory entities (pipeline, activity, dataset, and linked service).</span></span>  

## <a name="pipeline"></a><span data-ttu-id="ed017-105">Pipeline</span><span class="sxs-lookup"><span data-stu-id="ed017-105">Pipeline</span></span> 
<span data-ttu-id="ed017-106">estrutura de alto nível Olá para uma definição de pipeline é o seguinte:</span><span class="sxs-lookup"><span data-stu-id="ed017-106">hello high-level structure for a pipeline definition is as follows:</span></span> 

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

<span data-ttu-id="ed017-107">Tabela a seguir descreve as propriedades de saudação no pipeline de saudação definição JSON:</span><span class="sxs-lookup"><span data-stu-id="ed017-107">Following table describes hello properties within hello pipeline JSON definition:</span></span>

| <span data-ttu-id="ed017-108">Propriedade</span><span class="sxs-lookup"><span data-stu-id="ed017-108">Property</span></span> | <span data-ttu-id="ed017-109">Descrição</span><span class="sxs-lookup"><span data-stu-id="ed017-109">Description</span></span> | <span data-ttu-id="ed017-110">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="ed017-110">Required</span></span>
-------- | ----------- | --------
| <span data-ttu-id="ed017-111">name</span><span class="sxs-lookup"><span data-stu-id="ed017-111">name</span></span> | <span data-ttu-id="ed017-112">Nome do pipeline de saudação.</span><span class="sxs-lookup"><span data-stu-id="ed017-112">Name of hello pipeline.</span></span> <span data-ttu-id="ed017-113">Especifique um nome que representa a ação Olá Olá atividade ou pipeline é toodo configurado</span><span class="sxs-lookup"><span data-stu-id="ed017-113">Specify a name that represents hello action that hello activity or pipeline is configured toodo</span></span><br/><ul><li><span data-ttu-id="ed017-114">Número máximo de caracteres: 260</span><span class="sxs-lookup"><span data-stu-id="ed017-114">Maximum number of characters: 260</span></span></li><li><span data-ttu-id="ed017-115">Deve começar com uma letra, um número ou um sublinhado (_)</span><span class="sxs-lookup"><span data-stu-id="ed017-115">Must start with a letter number, or an underscore (_)</span></span></li><li><span data-ttu-id="ed017-116">Os seguintes caracteres não são permitidos: “.”, “+”, “?”, “/”, “<”,”>”,”*”,”%”,”&”,”:”,”\\”</span><span class="sxs-lookup"><span data-stu-id="ed017-116">Following characters are not allowed: “.”, “+”, “?”, “/”, “<”,”>”,”*”,”%”,”&”,”:”,”\\”</span></span></li></ul> |<span data-ttu-id="ed017-117">Sim</span><span class="sxs-lookup"><span data-stu-id="ed017-117">Yes</span></span> |
| <span data-ttu-id="ed017-118">description</span><span class="sxs-lookup"><span data-stu-id="ed017-118">description</span></span> |<span data-ttu-id="ed017-119">Texto que descreve quais atividade hello ou pipeline é usado para</span><span class="sxs-lookup"><span data-stu-id="ed017-119">Text describing what hello activity or pipeline is used for</span></span> | <span data-ttu-id="ed017-120">Não</span><span class="sxs-lookup"><span data-stu-id="ed017-120">No</span></span> |
| <span data-ttu-id="ed017-121">atividades</span><span class="sxs-lookup"><span data-stu-id="ed017-121">activities</span></span> | <span data-ttu-id="ed017-122">Contém uma lista de atividades.</span><span class="sxs-lookup"><span data-stu-id="ed017-122">Contains a list of activities.</span></span> | <span data-ttu-id="ed017-123">Sim</span><span class="sxs-lookup"><span data-stu-id="ed017-123">Yes</span></span> |
| <span data-ttu-id="ed017-124">iniciar</span><span class="sxs-lookup"><span data-stu-id="ed017-124">start</span></span> |<span data-ttu-id="ed017-125">Data-hora de início para o pipeline de saudação.</span><span class="sxs-lookup"><span data-stu-id="ed017-125">Start date-time for hello pipeline.</span></span> <span data-ttu-id="ed017-126">Deve estar no [formato ISO](http://en.wikipedia.org/wiki/ISO_8601).</span><span class="sxs-lookup"><span data-stu-id="ed017-126">Must be in [ISO format](http://en.wikipedia.org/wiki/ISO_8601).</span></span> <span data-ttu-id="ed017-127">Por exemplo: 2014-10-14T16:32:41.</span><span class="sxs-lookup"><span data-stu-id="ed017-127">For example: 2014-10-14T16:32:41.</span></span> <br/><br/><span data-ttu-id="ed017-128">É possível toospecify a hora local, por exemplo um tempo estimado.</span><span class="sxs-lookup"><span data-stu-id="ed017-128">It is possible toospecify a local time, for example an EST time.</span></span> <span data-ttu-id="ed017-129">Aqui está um exemplo: `2016-02-27T06:00:00**-05:00`, que é 6 AM EST.</span><span class="sxs-lookup"><span data-stu-id="ed017-129">Here is an example: `2016-02-27T06:00:00**-05:00`, which is 6 AM EST.</span></span><br/><br/><span data-ttu-id="ed017-130">Hello propriedades de início e término juntas especificam o período ativo para o pipeline de saudação.</span><span class="sxs-lookup"><span data-stu-id="ed017-130">hello start and end properties together specify active period for hello pipeline.</span></span> <span data-ttu-id="ed017-131">Fatias de saída são produzidas somente nesse período ativo.</span><span class="sxs-lookup"><span data-stu-id="ed017-131">Output slices are only produced with in this active period.</span></span> |<span data-ttu-id="ed017-132">Não</span><span class="sxs-lookup"><span data-stu-id="ed017-132">No</span></span><br/><br/><span data-ttu-id="ed017-133">Se você especificar um valor para a propriedade end hello, você deve especificar o valor para a propriedade de início de saudação.</span><span class="sxs-lookup"><span data-stu-id="ed017-133">If you specify a value for hello end property, you must specify value for hello start property.</span></span><br/><br/><span data-ttu-id="ed017-134">Olá horários de início e término podem ser vazio toocreate um pipeline.</span><span class="sxs-lookup"><span data-stu-id="ed017-134">hello start and end times can both be empty toocreate a pipeline.</span></span> <span data-ttu-id="ed017-135">Você deve especificar os dois valores tooset um período ativo para Olá toorun de pipeline.</span><span class="sxs-lookup"><span data-stu-id="ed017-135">You must specify both values tooset an active period for hello pipeline toorun.</span></span> <span data-ttu-id="ed017-136">Se você não especificar horários de início e término durante a criação de um pipeline, você pode defini-las usando o cmdlet Olá AzureRmDataFactoryPipelineActivePeriod conjunto mais tarde.</span><span class="sxs-lookup"><span data-stu-id="ed017-136">If you do not specify start and end times when creating a pipeline, you can set them using hello Set-AzureRmDataFactoryPipelineActivePeriod cmdlet later.</span></span> |
| <span data-ttu-id="ed017-137">end</span><span class="sxs-lookup"><span data-stu-id="ed017-137">end</span></span> |<span data-ttu-id="ed017-138">Data-hora de término para o pipeline de saudação.</span><span class="sxs-lookup"><span data-stu-id="ed017-138">End date-time for hello pipeline.</span></span> <span data-ttu-id="ed017-139">Se especificado, deve estar no formato ISO.</span><span class="sxs-lookup"><span data-stu-id="ed017-139">If specified must be in ISO format.</span></span> <span data-ttu-id="ed017-140">Por exemplo: 2014-10-14T17:32:41.</span><span class="sxs-lookup"><span data-stu-id="ed017-140">For example: 2014-10-14T17:32:41</span></span> <br/><br/><span data-ttu-id="ed017-141">É possível toospecify a hora local, por exemplo um tempo estimado.</span><span class="sxs-lookup"><span data-stu-id="ed017-141">It is possible toospecify a local time, for example an EST time.</span></span> <span data-ttu-id="ed017-142">Aqui está um exemplo: `2016-02-27T06:00:00**-05:00`, que é 6 AM EST.</span><span class="sxs-lookup"><span data-stu-id="ed017-142">Here is an example: `2016-02-27T06:00:00**-05:00`, which is 6 AM EST.</span></span><br/><br/><span data-ttu-id="ed017-143">pipeline de saudação toorun indefinidamente, especificar 9999-09-09 como valor de saudação para a propriedade end hello.</span><span class="sxs-lookup"><span data-stu-id="ed017-143">toorun hello pipeline indefinitely, specify 9999-09-09 as hello value for hello end property.</span></span> |<span data-ttu-id="ed017-144">Não</span><span class="sxs-lookup"><span data-stu-id="ed017-144">No</span></span> <br/><br/><span data-ttu-id="ed017-145">Se você especificar um valor para a propriedade de início Olá, você deve especificar o valor para a propriedade end hello.</span><span class="sxs-lookup"><span data-stu-id="ed017-145">If you specify a value for hello start property, you must specify value for hello end property.</span></span><br/><br/><span data-ttu-id="ed017-146">Consulte as observações para Olá **iniciar** propriedade.</span><span class="sxs-lookup"><span data-stu-id="ed017-146">See notes for hello **start** property.</span></span> |
| <span data-ttu-id="ed017-147">isPaused</span><span class="sxs-lookup"><span data-stu-id="ed017-147">isPaused</span></span> |<span data-ttu-id="ed017-148">Se o conjunto tootrue Olá pipeline não é executado.</span><span class="sxs-lookup"><span data-stu-id="ed017-148">If set tootrue hello pipeline does not run.</span></span> <span data-ttu-id="ed017-149">Valor padrão = falso.</span><span class="sxs-lookup"><span data-stu-id="ed017-149">Default value = false.</span></span> <span data-ttu-id="ed017-150">Você pode usar essa propriedade tooenable ou desabilitar.</span><span class="sxs-lookup"><span data-stu-id="ed017-150">You can use this property tooenable or disable.</span></span> |<span data-ttu-id="ed017-151">Não</span><span class="sxs-lookup"><span data-stu-id="ed017-151">No</span></span> |
| <span data-ttu-id="ed017-152">pipelineMode</span><span class="sxs-lookup"><span data-stu-id="ed017-152">pipelineMode</span></span> |<span data-ttu-id="ed017-153">método Hello para o agendamento é executado para o pipeline de saudação.</span><span class="sxs-lookup"><span data-stu-id="ed017-153">hello method for scheduling runs for hello pipeline.</span></span> <span data-ttu-id="ed017-154">Os valores permitidos são: scheduled (padrão), onetime.</span><span class="sxs-lookup"><span data-stu-id="ed017-154">Allowed values are: scheduled (default), onetime.</span></span><br/><br/><span data-ttu-id="ed017-155">'Agendado' indica que esse pipeline Olá é executado em um intervalo de tempo especificado de acordo com o período ativo de tooits (hora de início e de término).</span><span class="sxs-lookup"><span data-stu-id="ed017-155">‘Scheduled’ indicates that hello pipeline runs at a specified time interval according tooits active period (start and end time).</span></span> <span data-ttu-id="ed017-156">'Única' indica que esse pipeline Olá é executado apenas uma vez.</span><span class="sxs-lookup"><span data-stu-id="ed017-156">‘Onetime’ indicates that hello pipeline runs only once.</span></span> <span data-ttu-id="ed017-157">Pipelines Onetime não podem ser modificados e atualizados depois de criados atualmente.</span><span class="sxs-lookup"><span data-stu-id="ed017-157">Onetime pipelines once created cannot be modified/updated currently.</span></span> <span data-ttu-id="ed017-158">Confira [Pipeline avulso](data-factory-create-pipelines.md#onetime-pipeline) para obter detalhes sobre a configuração única.</span><span class="sxs-lookup"><span data-stu-id="ed017-158">See [Onetime pipeline](data-factory-create-pipelines.md#onetime-pipeline) for details about onetime setting.</span></span> |<span data-ttu-id="ed017-159">Não</span><span class="sxs-lookup"><span data-stu-id="ed017-159">No</span></span> |
| <span data-ttu-id="ed017-160">expirationTime</span><span class="sxs-lookup"><span data-stu-id="ed017-160">expirationTime</span></span> |<span data-ttu-id="ed017-161">Duração de tempo após a criação para o qual Olá pipeline é válido e deve permanecer provisionado.</span><span class="sxs-lookup"><span data-stu-id="ed017-161">Duration of time after creation for which hello pipeline is valid and should remain provisioned.</span></span> <span data-ttu-id="ed017-162">Se ele não tem qualquer ativo, falha, ou pendente é executado, o pipeline de saudação será excluído automaticamente depois que ele atinge o tempo de expiração de saudação.</span><span class="sxs-lookup"><span data-stu-id="ed017-162">If it does not have any active, failed, or pending runs, hello pipeline is deleted automatically once it reaches hello expiration time.</span></span> |<span data-ttu-id="ed017-163">Não</span><span class="sxs-lookup"><span data-stu-id="ed017-163">No</span></span> |


## <a name="activity"></a><span data-ttu-id="ed017-164">Atividade</span><span class="sxs-lookup"><span data-stu-id="ed017-164">Activity</span></span> 
<span data-ttu-id="ed017-165">estrutura de alto nível Olá para uma atividade dentro de uma definição de pipeline (elemento de atividades) é o seguinte:</span><span class="sxs-lookup"><span data-stu-id="ed017-165">hello high-level structure for an activity within a pipeline definition (activities element) is as follows:</span></span>

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

<span data-ttu-id="ed017-166">Tabela a seguir descrevem as propriedades de hello atividade Olá definição JSON:</span><span class="sxs-lookup"><span data-stu-id="ed017-166">Following table describe hello properties within hello activity JSON definition:</span></span>

| <span data-ttu-id="ed017-167">Marca</span><span class="sxs-lookup"><span data-stu-id="ed017-167">Tag</span></span> | <span data-ttu-id="ed017-168">Descrição</span><span class="sxs-lookup"><span data-stu-id="ed017-168">Description</span></span> | <span data-ttu-id="ed017-169">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="ed017-169">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ed017-170">name</span><span class="sxs-lookup"><span data-stu-id="ed017-170">name</span></span> |<span data-ttu-id="ed017-171">Nome da atividade de saudação.</span><span class="sxs-lookup"><span data-stu-id="ed017-171">Name of hello activity.</span></span> <span data-ttu-id="ed017-172">Especifique um nome que representa a ação de hello atividade Olá configurado toodo</span><span class="sxs-lookup"><span data-stu-id="ed017-172">Specify a name that represents hello action that hello activity is configured toodo</span></span><br/><ul><li><span data-ttu-id="ed017-173">Número máximo de caracteres: 260</span><span class="sxs-lookup"><span data-stu-id="ed017-173">Maximum number of characters: 260</span></span></li><li><span data-ttu-id="ed017-174">Deve começar com uma letra, um número ou um sublinhado (_)</span><span class="sxs-lookup"><span data-stu-id="ed017-174">Must start with a letter number, or an underscore (_)</span></span></li><li><span data-ttu-id="ed017-175">Os seguintes caracteres não são permitidos: “.”, “+”, “?”, “/”, “<”,”>”,”*”,”%”,”&”,”:”,”\\”</span><span class="sxs-lookup"><span data-stu-id="ed017-175">Following characters are not allowed: “.”, “+”, “?”, “/”, “<”,”>”,”*”,”%”,”&”,”:”,”\\”</span></span></li></ul> |<span data-ttu-id="ed017-176">Sim</span><span class="sxs-lookup"><span data-stu-id="ed017-176">Yes</span></span> |
| <span data-ttu-id="ed017-177">description</span><span class="sxs-lookup"><span data-stu-id="ed017-177">description</span></span> |<span data-ttu-id="ed017-178">Texto que descreve quais hello atividade é usada.</span><span class="sxs-lookup"><span data-stu-id="ed017-178">Text describing what hello activity is used for.</span></span> |<span data-ttu-id="ed017-179">Sim</span><span class="sxs-lookup"><span data-stu-id="ed017-179">Yes</span></span> |
| <span data-ttu-id="ed017-180">type</span><span class="sxs-lookup"><span data-stu-id="ed017-180">type</span></span> |<span data-ttu-id="ed017-181">Especifica o tipo de saudação da atividade de saudação.</span><span class="sxs-lookup"><span data-stu-id="ed017-181">Specifies hello type of hello activity.</span></span> <span data-ttu-id="ed017-182">Consulte Olá [REPOSITÓRIOS de dados](#data-stores) e [atividades de TRANSFORMAÇÃO de dados](#data-transformation-activities) seções para diferentes tipos de atividades.</span><span class="sxs-lookup"><span data-stu-id="ed017-182">See hello [DATA STORES](#data-stores) and [DATA TRANSFORMATION ACTIVITIES](#data-transformation-activities) sections for different types of activities.</span></span> |<span data-ttu-id="ed017-183">Sim</span><span class="sxs-lookup"><span data-stu-id="ed017-183">Yes</span></span> |
| <span data-ttu-id="ed017-184">inputs</span><span class="sxs-lookup"><span data-stu-id="ed017-184">inputs</span></span> |<span data-ttu-id="ed017-185">Tabelas de entrada usadas pela atividade Olá</span><span class="sxs-lookup"><span data-stu-id="ed017-185">Input tables used by hello activity</span></span><br/><br/>`// one input table`<br/>`"inputs":  [ { "name": "inputtable1"  } ],`<br/><br/>`// two input tables` <br/>`"inputs":  [ { "name": "inputtable1"  }, { "name": "inputtable2"  } ],` |<span data-ttu-id="ed017-186">Sim</span><span class="sxs-lookup"><span data-stu-id="ed017-186">Yes</span></span> |
| <span data-ttu-id="ed017-187">outputs</span><span class="sxs-lookup"><span data-stu-id="ed017-187">outputs</span></span> |<span data-ttu-id="ed017-188">Tabelas de saída usadas pela atividade de saudação.</span><span class="sxs-lookup"><span data-stu-id="ed017-188">Output tables used by hello activity.</span></span><br/><br/>`// one output table`<br/>`"outputs":  [ { "name": “outputtable1” } ],`<br/><br/>`//two output tables`<br/>`"outputs":  [ { "name": “outputtable1” }, { "name": “outputtable2” }  ],` |<span data-ttu-id="ed017-189">Sim</span><span class="sxs-lookup"><span data-stu-id="ed017-189">Yes</span></span> |
| <span data-ttu-id="ed017-190">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="ed017-190">linkedServiceName</span></span> |<span data-ttu-id="ed017-191">Nome do serviço de saudação vinculado usado pela atividade de saudação.</span><span class="sxs-lookup"><span data-stu-id="ed017-191">Name of hello linked service used by hello activity.</span></span> <br/><br/><span data-ttu-id="ed017-192">Uma atividade pode exigir que você especifique que o serviço Olá vinculado que vincula o ambiente de computação necessária toohello.</span><span class="sxs-lookup"><span data-stu-id="ed017-192">An activity may require that you specify hello linked service that links toohello required compute environment.</span></span> |<span data-ttu-id="ed017-193">Sim para atividades de HDInsight, atividades de Azure Machine Learning e Atividade de Procedimento Armazenado.</span><span class="sxs-lookup"><span data-stu-id="ed017-193">Yes for HDInsight activities, Azure Machine Learning activities, and Stored Procedure Activity.</span></span> <br/><br/><span data-ttu-id="ed017-194">Não para todas as outros</span><span class="sxs-lookup"><span data-stu-id="ed017-194">No for all others</span></span> |
| <span data-ttu-id="ed017-195">typeProperties</span><span class="sxs-lookup"><span data-stu-id="ed017-195">typeProperties</span></span> |<span data-ttu-id="ed017-196">Propriedades na seção de typeProperties Olá dependem do tipo de atividade de saudação.</span><span class="sxs-lookup"><span data-stu-id="ed017-196">Properties in hello typeProperties section depend on type of hello activity.</span></span> |<span data-ttu-id="ed017-197">Não</span><span class="sxs-lookup"><span data-stu-id="ed017-197">No</span></span> |
| <span data-ttu-id="ed017-198">policy</span><span class="sxs-lookup"><span data-stu-id="ed017-198">policy</span></span> |<span data-ttu-id="ed017-199">Diretivas que afetam o comportamento de tempo de execução de saudação da atividade de saudação.</span><span class="sxs-lookup"><span data-stu-id="ed017-199">Policies that affect hello run-time behavior of hello activity.</span></span> <span data-ttu-id="ed017-200">Se não for especificado, as políticas padrão serão utilizadas.</span><span class="sxs-lookup"><span data-stu-id="ed017-200">If it is not specified, default policies are used.</span></span> |<span data-ttu-id="ed017-201">Não</span><span class="sxs-lookup"><span data-stu-id="ed017-201">No</span></span> |
| <span data-ttu-id="ed017-202">agendador</span><span class="sxs-lookup"><span data-stu-id="ed017-202">scheduler</span></span> |<span data-ttu-id="ed017-203">propriedade "Agendador" é usado toodefine desejado de agendamento para a atividade de saudação.</span><span class="sxs-lookup"><span data-stu-id="ed017-203">“scheduler” property is used toodefine desired scheduling for hello activity.</span></span> <span data-ttu-id="ed017-204">Seus subpropriedades são Olá mesmo Olá na Olá [propriedade de disponibilidade em um conjunto de dados](data-factory-create-datasets.md#dataset-availability).</span><span class="sxs-lookup"><span data-stu-id="ed017-204">Its subproperties are hello same as hello ones in hello [availability property in a dataset](data-factory-create-datasets.md#dataset-availability).</span></span> |<span data-ttu-id="ed017-205">Não</span><span class="sxs-lookup"><span data-stu-id="ed017-205">No</span></span> |

### <a name="policies"></a><span data-ttu-id="ed017-206">Políticas</span><span class="sxs-lookup"><span data-stu-id="ed017-206">Policies</span></span>
<span data-ttu-id="ed017-207">Políticas afetam o comportamento de tempo de execução de saudação de uma atividade, especialmente quando Olá fatia de uma tabela é processada.</span><span class="sxs-lookup"><span data-stu-id="ed017-207">Policies affect hello run-time behavior of an activity, specifically when hello slice of a table is processed.</span></span> <span data-ttu-id="ed017-208">Olá, a tabela a seguir fornece detalhes de saudação.</span><span class="sxs-lookup"><span data-stu-id="ed017-208">hello following table provides hello details.</span></span>

| <span data-ttu-id="ed017-209">Propriedade</span><span class="sxs-lookup"><span data-stu-id="ed017-209">Property</span></span> | <span data-ttu-id="ed017-210">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="ed017-210">Permitted values</span></span> | <span data-ttu-id="ed017-211">Valor Padrão</span><span class="sxs-lookup"><span data-stu-id="ed017-211">Default Value</span></span> | <span data-ttu-id="ed017-212">Descrição</span><span class="sxs-lookup"><span data-stu-id="ed017-212">Description</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="ed017-213">simultaneidade</span><span class="sxs-lookup"><span data-stu-id="ed017-213">concurrency</span></span> |<span data-ttu-id="ed017-214">Inteiro </span><span class="sxs-lookup"><span data-stu-id="ed017-214">Integer</span></span> <br/><br/><span data-ttu-id="ed017-215">Valor máximo: 10</span><span class="sxs-lookup"><span data-stu-id="ed017-215">Max value: 10</span></span> |<span data-ttu-id="ed017-216">1</span><span class="sxs-lookup"><span data-stu-id="ed017-216">1</span></span> |<span data-ttu-id="ed017-217">Número de execuções concorrentes da atividade de saudação.</span><span class="sxs-lookup"><span data-stu-id="ed017-217">Number of concurrent executions of hello activity.</span></span><br/><br/><span data-ttu-id="ed017-218">Ele determina o número de saudação de execuções de atividade paralela que pode ocorrer em intervalos diferentes.</span><span class="sxs-lookup"><span data-stu-id="ed017-218">It determines hello number of parallel activity executions that can happen on different slices.</span></span> <span data-ttu-id="ed017-219">Por exemplo, se precisar de uma atividade toogo por meio de um grande conjunto de dados disponíveis, ter um valor maior da simultaneidade acelera o processamento de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="ed017-219">For example, if an activity needs toogo through a large set of available data, having a larger concurrency value speeds up hello data processing.</span></span> |
| <span data-ttu-id="ed017-220">executionPriorityOrder</span><span class="sxs-lookup"><span data-stu-id="ed017-220">executionPriorityOrder</span></span> |<span data-ttu-id="ed017-221">NewestFirst</span><span class="sxs-lookup"><span data-stu-id="ed017-221">NewestFirst</span></span><br/><br/><span data-ttu-id="ed017-222">OldestFirst</span><span class="sxs-lookup"><span data-stu-id="ed017-222">OldestFirst</span></span> |<span data-ttu-id="ed017-223">OldestFirst</span><span class="sxs-lookup"><span data-stu-id="ed017-223">OldestFirst</span></span> |<span data-ttu-id="ed017-224">Determina a saudação ordenação de fatias de dados que estão sendo processadas.</span><span class="sxs-lookup"><span data-stu-id="ed017-224">Determines hello ordering of data slices that are being processed.</span></span><br/><br/><span data-ttu-id="ed017-225">Por exemplo, se houver duas fatias (uma ocorre às 16h e a outra às 17h),e ambas estiverem com a execução pendente.</span><span class="sxs-lookup"><span data-stu-id="ed017-225">For example, if you have 2 slices (one happening at 4pm, and another one at 5pm), and both are pending execution.</span></span> <span data-ttu-id="ed017-226">Se você definir Olá executionPriorityOrder toobe NewestFirst, a fatia Olá às 17H é processada primeiro.</span><span class="sxs-lookup"><span data-stu-id="ed017-226">If you set hello executionPriorityOrder toobe NewestFirst, hello slice at 5 PM is processed first.</span></span> <span data-ttu-id="ed017-227">Da mesma forma se você definir Olá executionPriorityORder toobe OldestFIrst, em seguida, Olá fatia às 16: 00 é processada.</span><span class="sxs-lookup"><span data-stu-id="ed017-227">Similarly if you set hello executionPriorityORder toobe OldestFIrst, then hello slice at 4 PM is processed.</span></span> |
| <span data-ttu-id="ed017-228">tentar novamente</span><span class="sxs-lookup"><span data-stu-id="ed017-228">retry</span></span> |<span data-ttu-id="ed017-229">Número inteiro</span><span class="sxs-lookup"><span data-stu-id="ed017-229">Integer</span></span><br/><br/><span data-ttu-id="ed017-230">O valor máximo pode ser 10</span><span class="sxs-lookup"><span data-stu-id="ed017-230">Max value can be 10</span></span> |<span data-ttu-id="ed017-231">0</span><span class="sxs-lookup"><span data-stu-id="ed017-231">0</span></span> |<span data-ttu-id="ed017-232">Número de tentativas antes do processamento de dados de saudação de fatia Olá é marcado como falha.</span><span class="sxs-lookup"><span data-stu-id="ed017-232">Number of retries before hello data processing for hello slice is marked as Failure.</span></span> <span data-ttu-id="ed017-233">A execução da atividade para uma fatia de dados é repetida backup toohello especificado contagem de repetição.</span><span class="sxs-lookup"><span data-stu-id="ed017-233">Activity execution for a data slice is retried up toohello specified retry count.</span></span> <span data-ttu-id="ed017-234">repetição de saudação é feita logo após a falha de saudação.</span><span class="sxs-lookup"><span data-stu-id="ed017-234">hello retry is done as soon as possible after hello failure.</span></span> |
| <span data-ttu-id="ed017-235">Tempo limite</span><span class="sxs-lookup"><span data-stu-id="ed017-235">timeout</span></span> |<span data-ttu-id="ed017-236">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="ed017-236">TimeSpan</span></span> |<span data-ttu-id="ed017-237">00:00:00</span><span class="sxs-lookup"><span data-stu-id="ed017-237">00:00:00</span></span> |<span data-ttu-id="ed017-238">Tempo limite para a atividade de saudação.</span><span class="sxs-lookup"><span data-stu-id="ed017-238">Timeout for hello activity.</span></span> <span data-ttu-id="ed017-239">Exemplo: 00:10:00 (implica o tempo limite de 10 minutos)</span><span class="sxs-lookup"><span data-stu-id="ed017-239">Example: 00:10:00 (implies timeout 10 mins)</span></span><br/><br/><span data-ttu-id="ed017-240">Se um valor não for especificado ou for 0, o tempo limite de saudação é infinito.</span><span class="sxs-lookup"><span data-stu-id="ed017-240">If a value is not specified or is 0, hello timeout is infinite.</span></span><br/><br/><span data-ttu-id="ed017-241">Se o tempo de processamento de dados de saudação em uma fatia exceder o valor de tempo limite de Olá, é cancelada e sistema Olá tentativas de processamento de saudação tooretry.</span><span class="sxs-lookup"><span data-stu-id="ed017-241">If hello data processing time on a slice exceeds hello timeout value, it is canceled, and hello system attempts tooretry hello processing.</span></span> <span data-ttu-id="ed017-242">o número de tentativas Olá depende da propriedade de repetição de saudação.</span><span class="sxs-lookup"><span data-stu-id="ed017-242">hello number of retries depends on hello retry property.</span></span> <span data-ttu-id="ed017-243">Quando o tempo limite ocorre, o status de saudação é definido tooTimedOut.</span><span class="sxs-lookup"><span data-stu-id="ed017-243">When timeout occurs, hello status is set tooTimedOut.</span></span> |
| <span data-ttu-id="ed017-244">atrasar</span><span class="sxs-lookup"><span data-stu-id="ed017-244">delay</span></span> |<span data-ttu-id="ed017-245">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="ed017-245">TimeSpan</span></span> |<span data-ttu-id="ed017-246">00:00:00</span><span class="sxs-lookup"><span data-stu-id="ed017-246">00:00:00</span></span> |<span data-ttu-id="ed017-247">Especifique o intervalo de saudação antes do processamento de dados de saudação fatia começar.</span><span class="sxs-lookup"><span data-stu-id="ed017-247">Specify hello delay before data processing of hello slice starts.</span></span><br/><br/><span data-ttu-id="ed017-248">execução de saudação da atividade de uma fatia de dados é iniciada depois Olá atraso é passado Olá esperado tempo de execução.</span><span class="sxs-lookup"><span data-stu-id="ed017-248">hello execution of activity for a data slice is started after hello Delay is past hello expected execution time.</span></span><br/><br/><span data-ttu-id="ed017-249">Exemplo: 00:10:00 (implica um atraso de 10 minutos)</span><span class="sxs-lookup"><span data-stu-id="ed017-249">Example: 00:10:00 (implies delay of 10 mins)</span></span> |
| <span data-ttu-id="ed017-250">longRetry</span><span class="sxs-lookup"><span data-stu-id="ed017-250">longRetry</span></span> |<span data-ttu-id="ed017-251">Inteiro </span><span class="sxs-lookup"><span data-stu-id="ed017-251">Integer</span></span><br/><br/><span data-ttu-id="ed017-252">Valor máximo: 10</span><span class="sxs-lookup"><span data-stu-id="ed017-252">Max value: 10</span></span> |<span data-ttu-id="ed017-253">1</span><span class="sxs-lookup"><span data-stu-id="ed017-253">1</span></span> |<span data-ttu-id="ed017-254">número de saudação de repetição longa tentativas antes da execução da fatia Olá falhou.</span><span class="sxs-lookup"><span data-stu-id="ed017-254">hello number of long retry attempts before hello slice execution is failed.</span></span><br/><br/><span data-ttu-id="ed017-255">Tentativas de longRetry são espaçadas por longRetryInterval.</span><span class="sxs-lookup"><span data-stu-id="ed017-255">longRetry attempts are spaced by longRetryInterval.</span></span> <span data-ttu-id="ed017-256">Portanto, se você precisar toospecify um tempo entre tentativas de repetição, use longRetry.</span><span class="sxs-lookup"><span data-stu-id="ed017-256">So if you need toospecify a time between retry attempts, use longRetry.</span></span> <span data-ttu-id="ed017-257">Se Retry e longRetry forem especificados, cada tentativa de longRetry inclui novas tentativas e Olá o número máximo de tentativas é repetir * longRetry.</span><span class="sxs-lookup"><span data-stu-id="ed017-257">If both Retry and longRetry are specified, each longRetry attempt includes Retry attempts and hello max number of attempts is Retry * longRetry.</span></span><br/><br/><span data-ttu-id="ed017-258">Por exemplo, se tivermos Olá configurações na política de atividade Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="ed017-258">For example, if we have hello following settings in hello activity policy:</span></span><br/><span data-ttu-id="ed017-259">Retry: 3</span><span class="sxs-lookup"><span data-stu-id="ed017-259">Retry: 3</span></span><br/><span data-ttu-id="ed017-260">longRetry: 2</span><span class="sxs-lookup"><span data-stu-id="ed017-260">longRetry: 2</span></span><br/><span data-ttu-id="ed017-261">longRetryInterval: 01:00:00</span><span class="sxs-lookup"><span data-stu-id="ed017-261">longRetryInterval: 01:00:00</span></span><br/><br/><span data-ttu-id="ed017-262">Pressupomos que haja apenas um tooexecute de fatia (status está esperando) e a execução da atividade Olá falha sempre.</span><span class="sxs-lookup"><span data-stu-id="ed017-262">Assume there is only one slice tooexecute (status is Waiting) and hello activity execution fails every time.</span></span> <span data-ttu-id="ed017-263">Inicialmente haveria três tentativas consecutivas de execução.</span><span class="sxs-lookup"><span data-stu-id="ed017-263">Initially there would be 3 consecutive execution attempts.</span></span> <span data-ttu-id="ed017-264">Após cada tentativa, o status da fatia Olá deve ser Retry.</span><span class="sxs-lookup"><span data-stu-id="ed017-264">After each attempt, hello slice status would be Retry.</span></span> <span data-ttu-id="ed017-265">Depois de tentativas primeiro 3 estão acima, o status da fatia Olá deve ser LongRetry.</span><span class="sxs-lookup"><span data-stu-id="ed017-265">After first 3 attempts are over, hello slice status would be LongRetry.</span></span><br/><br/><span data-ttu-id="ed017-266">Depois de uma hora (ou seja, valor de longRetryInteval), deve haver outro conjunto de três tentativas consecutivas de execução.</span><span class="sxs-lookup"><span data-stu-id="ed017-266">After an hour (that is, longRetryInteval’s value), there would be another set of 3 consecutive execution attempts.</span></span> <span data-ttu-id="ed017-267">Depois disso, o status da fatia Olá deve ser Failed e nenhuma outra tentativa será feita.</span><span class="sxs-lookup"><span data-stu-id="ed017-267">After that, hello slice status would be Failed and no more retries would be attempted.</span></span> <span data-ttu-id="ed017-268">Portanto, em geral, foram feitas seis tentativas.</span><span class="sxs-lookup"><span data-stu-id="ed017-268">Hence overall 6 attempts were made.</span></span><br/><br/><span data-ttu-id="ed017-269">Se qualquer execução for bem-sucedida, o status da fatia Olá seria pronto e não tentativa de nenhuma outra tentativa.</span><span class="sxs-lookup"><span data-stu-id="ed017-269">If any execution succeeds, hello slice status would be Ready and no more retries are attempted.</span></span><br/><br/><span data-ttu-id="ed017-270">longRetry pode ser usado em situações em que dados dependentes chegam em momentos não determinística ou hello ambiente geral é instável em ocorre o processamento de dados.</span><span class="sxs-lookup"><span data-stu-id="ed017-270">longRetry may be used in situations where dependent data arrives at non-deterministic times or hello overall environment is flaky under which data processing occurs.</span></span> <span data-ttu-id="ed017-271">Nesses casos, não pode ajudar a fazer tentativas após o outro e fazer isso após um intervalo de resultados de tempo de saudação desejado de saída.</span><span class="sxs-lookup"><span data-stu-id="ed017-271">In such cases, doing retries one after another may not help and doing so after an interval of time results in hello desired output.</span></span><br/><br/><span data-ttu-id="ed017-272">Advertência: não defina valores altos para longRetry ou longRetryInterval.</span><span class="sxs-lookup"><span data-stu-id="ed017-272">Word of caution: do not set high values for longRetry or longRetryInterval.</span></span> <span data-ttu-id="ed017-273">Normalmente, os valores mais altos implicam outros problemas sistêmicos.</span><span class="sxs-lookup"><span data-stu-id="ed017-273">Typically, higher values imply other systemic issues.</span></span> |
| <span data-ttu-id="ed017-274">longRetryInterval</span><span class="sxs-lookup"><span data-stu-id="ed017-274">longRetryInterval</span></span> |<span data-ttu-id="ed017-275">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="ed017-275">TimeSpan</span></span> |<span data-ttu-id="ed017-276">00:00:00</span><span class="sxs-lookup"><span data-stu-id="ed017-276">00:00:00</span></span> |<span data-ttu-id="ed017-277">atraso de saudação entre as tentativas de repetição longa</span><span class="sxs-lookup"><span data-stu-id="ed017-277">hello delay between long retry attempts</span></span> |

### <a name="typeproperties-section"></a><span data-ttu-id="ed017-278">Seção typeProperties</span><span class="sxs-lookup"><span data-stu-id="ed017-278">typeProperties section</span></span>
<span data-ttu-id="ed017-279">seção de typeProperties Olá é diferente para cada atividade.</span><span class="sxs-lookup"><span data-stu-id="ed017-279">hello typeProperties section is different for each activity.</span></span> <span data-ttu-id="ed017-280">Atividades de transformação tem apenas as propriedades de tipo hello.</span><span class="sxs-lookup"><span data-stu-id="ed017-280">Transformation activities have just hello type properties.</span></span> <span data-ttu-id="ed017-281">Consulte [ATIVIDADES DE TRANSFORMAÇÃO DE DADOS](#data-transformation-activities) neste artigo para obter exemplos de JSON que definem atividades de transformação em um pipeline.</span><span class="sxs-lookup"><span data-stu-id="ed017-281">See [DATA TRANSFORMATION ACTIVITIES](#data-transformation-activities) section in this article for JSON samples that define transformation activities in a pipeline.</span></span> 

<span data-ttu-id="ed017-282">**Atividade de cópia** tem duas subseções na seção de typeProperties Olá: **fonte** e **coletor**.</span><span class="sxs-lookup"><span data-stu-id="ed017-282">**Copy activity** has two subsections in hello typeProperties section: **source** and **sink**.</span></span> <span data-ttu-id="ed017-283">Consulte [REPOSITÓRIOS de dados](#data-stores) seção neste artigo para JSON exemplos que mostram como toouse um dados armazenados como uma origem e/ou o coletor.</span><span class="sxs-lookup"><span data-stu-id="ed017-283">See [DATA STORES](#data-stores) section in this article for JSON samples that show how toouse a data store as a source and/or sink.</span></span> 

### <a name="sample-copy-pipeline"></a><span data-ttu-id="ed017-284">Pipeline de cópia de exemplo</span><span class="sxs-lookup"><span data-stu-id="ed017-284">Sample copy pipeline</span></span>
<span data-ttu-id="ed017-285">Olá pipeline de exemplo a seguir, há uma atividade do tipo **cópia** em Olá **atividades** seção.</span><span class="sxs-lookup"><span data-stu-id="ed017-285">In hello following sample pipeline, there is one activity of type **Copy** in hello **activities** section.</span></span> <span data-ttu-id="ed017-286">Neste exemplo, Olá [atividade de cópia](data-factory-data-movement-activities.md) copia dados de um banco de dados de SQL do Azure de tooan do armazenamento de BLOBs do Azure.</span><span class="sxs-lookup"><span data-stu-id="ed017-286">In this sample, hello [Copy activity](data-factory-data-movement-activities.md) copies data from an Azure Blob storage tooan Azure SQL database.</span></span> 

```json
{
  "name": "CopyPipeline",
  "properties": {
    "description": "Copy data from a blob tooAzure SQL table",
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

<span data-ttu-id="ed017-287">Observe Olá pontos a seguir:</span><span class="sxs-lookup"><span data-stu-id="ed017-287">Note hello following points:</span></span>

* <span data-ttu-id="ed017-288">Na seção de atividades hello, há apenas uma atividade cuja **tipo** está definido muito**cópia**.</span><span class="sxs-lookup"><span data-stu-id="ed017-288">In hello activities section, there is only one activity whose **type** is set too**Copy**.</span></span>
* <span data-ttu-id="ed017-289">Entrada para atividade de saudação é definida muito**InputDataset** e de saída para o conjunto de hello atividade é muito**OutputDataset**.</span><span class="sxs-lookup"><span data-stu-id="ed017-289">Input for hello activity is set too**InputDataset** and output for hello activity is set too**OutputDataset**.</span></span>
* <span data-ttu-id="ed017-290">Em Olá **typeProperties** seção, **BlobSource** é especificado como tipo de fonte hello e **SqlSink** é especificado como tipo de coletor de saudação.</span><span class="sxs-lookup"><span data-stu-id="ed017-290">In hello **typeProperties** section, **BlobSource** is specified as hello source type and **SqlSink** is specified as hello sink type.</span></span>

<span data-ttu-id="ed017-291">Consulte [REPOSITÓRIOS de dados](#data-stores) seção neste artigo para JSON exemplos que mostram como toouse um dados armazenados como uma origem e/ou o coletor.</span><span class="sxs-lookup"><span data-stu-id="ed017-291">See [DATA STORES](#data-stores) section in this article for JSON samples that show how toouse a data store as a source and/or sink.</span></span>    

<span data-ttu-id="ed017-292">Para obter uma explicação completa de criar esse pipeline, consulte [Tutorial: copiar dados de armazenamento de Blob tooSQL banco de dados](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="ed017-292">For a complete walkthrough of creating this pipeline, see [Tutorial: Copy data from Blob Storage tooSQL Database](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span> 

### <a name="sample-transformation-pipeline"></a><span data-ttu-id="ed017-293">Pipeline de transformação de exemplo</span><span class="sxs-lookup"><span data-stu-id="ed017-293">Sample transformation pipeline</span></span>
<span data-ttu-id="ed017-294">Olá pipeline de exemplo a seguir, há uma atividade do tipo **HDInsightHive** em Olá **atividades** seção.</span><span class="sxs-lookup"><span data-stu-id="ed017-294">In hello following sample pipeline, there is one activity of type **HDInsightHive** in hello **activities** section.</span></span> <span data-ttu-id="ed017-295">Neste exemplo, Olá [atividade Hive do HDInsight](data-factory-hive-activity.md) transforma os dados de um armazenamento de BLOBs do Azure executando um arquivo de script do Hive em um cluster de Hadoop de HDInsight do Azure.</span><span class="sxs-lookup"><span data-stu-id="ed017-295">In this sample, hello [HDInsight Hive activity](data-factory-hive-activity.md) transforms data from an Azure Blob storage by running a Hive script file on an Azure HDInsight Hadoop cluster.</span></span> 

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

<span data-ttu-id="ed017-296">Observe Olá pontos a seguir:</span><span class="sxs-lookup"><span data-stu-id="ed017-296">Note hello following points:</span></span> 

* <span data-ttu-id="ed017-297">Na seção de atividades hello, há apenas uma atividade cuja **tipo** está definido muito**HDInsightHive**.</span><span class="sxs-lookup"><span data-stu-id="ed017-297">In hello activities section, there is only one activity whose **type** is set too**HDInsightHive**.</span></span>
* <span data-ttu-id="ed017-298">arquivo de script do Hive Hello, **partitionweblogs.hql**, é armazenado no hello conta de armazenamento do Azure (especificado por scriptLinkedService hello, chamado **AzureStorageLinkedService**) e em  **script** pasta no contêiner Olá **adfgetstarted**.</span><span class="sxs-lookup"><span data-stu-id="ed017-298">hello Hive script file, **partitionweblogs.hql**, is stored in hello Azure storage account (specified by hello scriptLinkedService, called **AzureStorageLinkedService**), and in **script** folder in hello container **adfgetstarted**.</span></span>
* <span data-ttu-id="ed017-299">Olá **define** seção é toospecify usadas configurações de tempo de execução de saudação que são passadas script do hive toohello como valores de configuração do Hive (por exemplo `${hiveconf:inputtable}`, `${hiveconf:partitionedtable}`).</span><span class="sxs-lookup"><span data-stu-id="ed017-299">hello **defines** section is used toospecify hello runtime settings that are passed toohello hive script as Hive configuration values (e.g `${hiveconf:inputtable}`, `${hiveconf:partitionedtable}`).</span></span>

<span data-ttu-id="ed017-300">Consulte [ATIVIDADES DE TRANSFORMAÇÃO DE DADOS](#data-transformation-activities) neste artigo para obter exemplos de JSON que definem atividades de transformação em um pipeline.</span><span class="sxs-lookup"><span data-stu-id="ed017-300">See [DATA TRANSFORMATION ACTIVITIES](#data-transformation-activities) section in this article for JSON samples that define transformation activities in a pipeline.</span></span>

<span data-ttu-id="ed017-301">Para obter uma explicação completa de criar esse pipeline, consulte [Tutorial: Crie sua primeira pipeline tooprocess de dados usando o cluster Hadoop](data-factory-build-your-first-pipeline.md).</span><span class="sxs-lookup"><span data-stu-id="ed017-301">For a complete walkthrough of creating this pipeline, see [Tutorial: Build your first pipeline tooprocess data using Hadoop cluster](data-factory-build-your-first-pipeline.md).</span></span> 

## <a name="linked-service"></a><span data-ttu-id="ed017-302">Serviço vinculado</span><span class="sxs-lookup"><span data-stu-id="ed017-302">Linked service</span></span>
<span data-ttu-id="ed017-303">estrutura de alto nível Olá para uma definição de serviço vinculado é o seguinte:</span><span class="sxs-lookup"><span data-stu-id="ed017-303">hello high-level structure for a linked service definition is as follows:</span></span>

```json
{
    "name": "<name of hello linked service>",
    "properties": {
        "type": "<type of hello linked service>",
        "typeProperties": {
        }
    }
}
```

<span data-ttu-id="ed017-304">Tabela a seguir descrevem as propriedades de hello atividade Olá definição JSON:</span><span class="sxs-lookup"><span data-stu-id="ed017-304">Following table describe hello properties within hello activity JSON definition:</span></span>

| <span data-ttu-id="ed017-305">Propriedade</span><span class="sxs-lookup"><span data-stu-id="ed017-305">Property</span></span> | <span data-ttu-id="ed017-306">Descrição</span><span class="sxs-lookup"><span data-stu-id="ed017-306">Description</span></span> | <span data-ttu-id="ed017-307">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="ed017-307">Required</span></span> |
| -------- | ----------- | -------- | 
| <span data-ttu-id="ed017-308">name</span><span class="sxs-lookup"><span data-stu-id="ed017-308">name</span></span> | <span data-ttu-id="ed017-309">Nome do serviço de saudação vinculado.</span><span class="sxs-lookup"><span data-stu-id="ed017-309">Name of hello linked service.</span></span> | <span data-ttu-id="ed017-310">Sim</span><span class="sxs-lookup"><span data-stu-id="ed017-310">Yes</span></span> | 
| <span data-ttu-id="ed017-311">properties - type</span><span class="sxs-lookup"><span data-stu-id="ed017-311">properties - type</span></span> | <span data-ttu-id="ed017-312">Serviço vinculado do tipo de saudação.</span><span class="sxs-lookup"><span data-stu-id="ed017-312">Type of hello linked service.</span></span> <span data-ttu-id="ed017-313">Por exemplo: Armazenamento do Azure, Banco de Dados SQL do Azure.</span><span class="sxs-lookup"><span data-stu-id="ed017-313">For example: Azure Storage, Azure SQL Database.</span></span> |
| <span data-ttu-id="ed017-314">typeProperties</span><span class="sxs-lookup"><span data-stu-id="ed017-314">typeProperties</span></span> | <span data-ttu-id="ed017-315">seção de typeProperties Olá tem elementos que são diferentes para cada repositório de dados ou ambiente de computação.</span><span class="sxs-lookup"><span data-stu-id="ed017-315">hello typeProperties section has elements that are different for each data store or compute environment.</span></span> <span data-ttu-id="ed017-316">Consulte [repositórios de dados](#datastores) seção de todos os dados de saudação serviços vinculados da loja e [ambientes de computação](#compute-environments) para Olá todos os serviços vinculados de computação</span><span class="sxs-lookup"><span data-stu-id="ed017-316">See [data stores](#datastores) section for all hello data store linked services and [compute environments](#compute-environments) for all hello compute linked services</span></span> |   

## <a name="dataset"></a><span data-ttu-id="ed017-317">Conjunto de dados</span><span class="sxs-lookup"><span data-stu-id="ed017-317">Dataset</span></span> 
<span data-ttu-id="ed017-318">Um conjunto de dados no Azure Data Factory é definido da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="ed017-318">A dataset in Azure Data Factory is defined as follows:</span></span>

```json
{
    "name": "<name of dataset>",
    "properties": {
        "type": "<type of dataset: AzureBlob, AzureSql etc...>",
        "external": <boolean flag tooindicate external data. only for input datasets>,
        "linkedServiceName": "<Name of hello linked service that refers tooa data store.>",
        "structure": [
            {
                "name": "<Name of hello column>",
                "type": "<Name of hello type>"
            }
        ],
        "typeProperties": {
            "<type specific property>": "<value>",
            "<type specific property 2>": "<value 2>",
        },
        "availability": {
            "frequency": "<Specifies hello time unit for data slice production. Supported frequency: Minute, Hour, Day, Week, Month>",
            "interval": "<Specifies hello interval within hello defined frequency. For example, frequency set too'Hour' and interval set too1 indicates that new data slices should be produced hourly>"
        },
       "policy":
        {      
        }
    }
}
```

<span data-ttu-id="ed017-319">Olá, a tabela a seguir descreve as propriedades no hello acima JSON:</span><span class="sxs-lookup"><span data-stu-id="ed017-319">hello following table describes properties in hello above JSON:</span></span>   

| <span data-ttu-id="ed017-320">Propriedade</span><span class="sxs-lookup"><span data-stu-id="ed017-320">Property</span></span> | <span data-ttu-id="ed017-321">Descrição</span><span class="sxs-lookup"><span data-stu-id="ed017-321">Description</span></span> | <span data-ttu-id="ed017-322">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="ed017-322">Required</span></span> | <span data-ttu-id="ed017-323">Padrão</span><span class="sxs-lookup"><span data-stu-id="ed017-323">Default</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="ed017-324">name</span><span class="sxs-lookup"><span data-stu-id="ed017-324">name</span></span> | <span data-ttu-id="ed017-325">Nome do conjunto de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="ed017-325">Name of hello dataset.</span></span> <span data-ttu-id="ed017-326">Confira [Azure Data Factory - Regras de nomenclatura](data-factory-naming-rules.md) para ver as regras de nomenclatura.</span><span class="sxs-lookup"><span data-stu-id="ed017-326">See [Azure Data Factory - Naming rules](data-factory-naming-rules.md) for naming rules.</span></span> |<span data-ttu-id="ed017-327">Sim</span><span class="sxs-lookup"><span data-stu-id="ed017-327">Yes</span></span> |<span data-ttu-id="ed017-328">ND</span><span class="sxs-lookup"><span data-stu-id="ed017-328">NA</span></span> |
| <span data-ttu-id="ed017-329">type</span><span class="sxs-lookup"><span data-stu-id="ed017-329">type</span></span> | <span data-ttu-id="ed017-330">Tipo de conjunto de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="ed017-330">Type of hello dataset.</span></span> <span data-ttu-id="ed017-331">Especifique um dos tipos de saudação com suporte pela fábrica de dados do Azure (por exemplo: AzureBlob, AzureSqlTable).</span><span class="sxs-lookup"><span data-stu-id="ed017-331">Specify one of hello types supported by Azure Data Factory (for example: AzureBlob, AzureSqlTable).</span></span> <span data-ttu-id="ed017-332">Consulte [REPOSITÓRIOS de dados](#data-stores) seção Olá a todos os repositórios de dados e tipos de conjunto de dados com suporte pela fábrica de dados.</span><span class="sxs-lookup"><span data-stu-id="ed017-332">See [DATA STORES](#data-stores) section for all hello data stores and dataset types supported by Data Factory.</span></span> | 
| <span data-ttu-id="ed017-333">estrutura</span><span class="sxs-lookup"><span data-stu-id="ed017-333">structure</span></span> | <span data-ttu-id="ed017-334">Esquema de conjunto de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="ed017-334">Schema of hello dataset.</span></span> <span data-ttu-id="ed017-335">Ela contém colunas, seus tipos, etc.</span><span class="sxs-lookup"><span data-stu-id="ed017-335">It contains columns, their types, etc.</span></span> | <span data-ttu-id="ed017-336">Não</span><span class="sxs-lookup"><span data-stu-id="ed017-336">No</span></span> |<span data-ttu-id="ed017-337">ND</span><span class="sxs-lookup"><span data-stu-id="ed017-337">NA</span></span> |
| <span data-ttu-id="ed017-338">typeProperties</span><span class="sxs-lookup"><span data-stu-id="ed017-338">typeProperties</span></span> | <span data-ttu-id="ed017-339">Propriedades correspondentes toohello tipo selecionado.</span><span class="sxs-lookup"><span data-stu-id="ed017-339">Properties corresponding toohello selected type.</span></span> <span data-ttu-id="ed017-340">Consulte a seção [ARMAZENAMENTOS DE DADOS](#data-stores) para saber quais são os tipos com suporte e suas propriedades.</span><span class="sxs-lookup"><span data-stu-id="ed017-340">See [DATA STORES](#data-stores) section for supported types and their properties.</span></span> |<span data-ttu-id="ed017-341">Sim</span><span class="sxs-lookup"><span data-stu-id="ed017-341">Yes</span></span> |<span data-ttu-id="ed017-342">ND</span><span class="sxs-lookup"><span data-stu-id="ed017-342">NA</span></span> |
| <span data-ttu-id="ed017-343">externo</span><span class="sxs-lookup"><span data-stu-id="ed017-343">external</span></span> | <span data-ttu-id="ed017-344">Booliano sinalizador toospecify se um conjunto de dados explicitamente produzido por um pipeline da fábrica de dados ou não.</span><span class="sxs-lookup"><span data-stu-id="ed017-344">Boolean flag toospecify whether a dataset is explicitly produced by a data factory pipeline or not.</span></span> |<span data-ttu-id="ed017-345">Não</span><span class="sxs-lookup"><span data-stu-id="ed017-345">No</span></span> |<span data-ttu-id="ed017-346">false</span><span class="sxs-lookup"><span data-stu-id="ed017-346">false</span></span> |
| <span data-ttu-id="ed017-347">disponibilidade</span><span class="sxs-lookup"><span data-stu-id="ed017-347">availability</span></span> | <span data-ttu-id="ed017-348">Define Olá processamento Olá dividindo o modelo para conjunto de dados de produção de hello ou janela.</span><span class="sxs-lookup"><span data-stu-id="ed017-348">Defines hello processing window or hello slicing model for hello dataset production.</span></span> <span data-ttu-id="ed017-349">Para obter detalhes sobre o dataset Olá dividindo o modelo, consulte [de agendamento e execução](data-factory-scheduling-and-execution.md) artigo.</span><span class="sxs-lookup"><span data-stu-id="ed017-349">For details on hello dataset slicing model, see [Scheduling and Execution](data-factory-scheduling-and-execution.md) article.</span></span> |<span data-ttu-id="ed017-350">Sim</span><span class="sxs-lookup"><span data-stu-id="ed017-350">Yes</span></span> |<span data-ttu-id="ed017-351">ND</span><span class="sxs-lookup"><span data-stu-id="ed017-351">NA</span></span> |
| <span data-ttu-id="ed017-352">policy</span><span class="sxs-lookup"><span data-stu-id="ed017-352">policy</span></span> |<span data-ttu-id="ed017-353">Define os critérios de saudação ou condição Olá que devem ser atendidos por fatias de conjunto de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="ed017-353">Defines hello criteria or hello condition that hello dataset slices must fulfill.</span></span> <br/><br/><span data-ttu-id="ed017-354">Para obter detalhes, consulte a seção [Política do Conjunto de Dados](#Policy) .</span><span class="sxs-lookup"><span data-stu-id="ed017-354">For details, see [Dataset Policy](#Policy) section.</span></span> |<span data-ttu-id="ed017-355">Não</span><span class="sxs-lookup"><span data-stu-id="ed017-355">No</span></span> |<span data-ttu-id="ed017-356">ND</span><span class="sxs-lookup"><span data-stu-id="ed017-356">NA</span></span> |

<span data-ttu-id="ed017-357">Cada coluna no hello **estrutura** seção contém Olá propriedades a seguir:</span><span class="sxs-lookup"><span data-stu-id="ed017-357">Each column in hello **structure** section contains hello following properties:</span></span>

| <span data-ttu-id="ed017-358">Propriedade</span><span class="sxs-lookup"><span data-stu-id="ed017-358">Property</span></span> | <span data-ttu-id="ed017-359">Descrição</span><span class="sxs-lookup"><span data-stu-id="ed017-359">Description</span></span> | <span data-ttu-id="ed017-360">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="ed017-360">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ed017-361">name</span><span class="sxs-lookup"><span data-stu-id="ed017-361">name</span></span> |<span data-ttu-id="ed017-362">Nome da coluna de saudação.</span><span class="sxs-lookup"><span data-stu-id="ed017-362">Name of hello column.</span></span> |<span data-ttu-id="ed017-363">Sim</span><span class="sxs-lookup"><span data-stu-id="ed017-363">Yes</span></span> |
| <span data-ttu-id="ed017-364">type</span><span class="sxs-lookup"><span data-stu-id="ed017-364">type</span></span> |<span data-ttu-id="ed017-365">Tipo de dados da coluna de saudação.</span><span class="sxs-lookup"><span data-stu-id="ed017-365">Data type of hello column.</span></span>  |<span data-ttu-id="ed017-366">Não</span><span class="sxs-lookup"><span data-stu-id="ed017-366">No</span></span> |
| <span data-ttu-id="ed017-367">culture</span><span class="sxs-lookup"><span data-stu-id="ed017-367">culture</span></span> |<span data-ttu-id="ed017-368">.NET com base em cultura toobe usado quando o tipo é especificado e é o tipo .NET `Datetime` ou `Datetimeoffset`.</span><span class="sxs-lookup"><span data-stu-id="ed017-368">.NET based culture toobe used when type is specified and is .NET type `Datetime` or `Datetimeoffset`.</span></span> <span data-ttu-id="ed017-369">O padrão é `en-us`.</span><span class="sxs-lookup"><span data-stu-id="ed017-369">Default is `en-us`.</span></span> |<span data-ttu-id="ed017-370">Não</span><span class="sxs-lookup"><span data-stu-id="ed017-370">No</span></span> |
| <span data-ttu-id="ed017-371">formato</span><span class="sxs-lookup"><span data-stu-id="ed017-371">format</span></span> |<span data-ttu-id="ed017-372">Formatar toobe de cadeia de caracteres usada quando o tipo é especificado e é o tipo .NET `Datetime` ou `Datetimeoffset`.</span><span class="sxs-lookup"><span data-stu-id="ed017-372">Format string toobe used when type is specified and is .NET type `Datetime` or `Datetimeoffset`.</span></span> |<span data-ttu-id="ed017-373">Não</span><span class="sxs-lookup"><span data-stu-id="ed017-373">No</span></span> |

<span data-ttu-id="ed017-374">Olá exemplo a seguir, Olá dataset tem três colunas `slicetimestamp`, `projectname`, e `pageviews` e eles são do tipo: cadeia de caracteres, cadeia de caracteres e decimais respectivamente.</span><span class="sxs-lookup"><span data-stu-id="ed017-374">In hello following example, hello dataset has three columns `slicetimestamp`, `projectname`, and `pageviews` and they are of type: String, String, and Decimal respectively.</span></span>

```json
structure:  
[
    { "name": "slicetimestamp", "type": "String"},
    { "name": "projectname", "type": "String"},
    { "name": "pageviews", "type": "Decimal"}
]
```

<span data-ttu-id="ed017-375">Olá tabela a seguir descreve as propriedades você pode usar em Olá **disponibilidade** seção:</span><span class="sxs-lookup"><span data-stu-id="ed017-375">hello following table describes properties you can use in hello **availability** section:</span></span>

| <span data-ttu-id="ed017-376">Propriedade</span><span class="sxs-lookup"><span data-stu-id="ed017-376">Property</span></span> | <span data-ttu-id="ed017-377">Descrição</span><span class="sxs-lookup"><span data-stu-id="ed017-377">Description</span></span> | <span data-ttu-id="ed017-378">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="ed017-378">Required</span></span> | <span data-ttu-id="ed017-379">Padrão</span><span class="sxs-lookup"><span data-stu-id="ed017-379">Default</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="ed017-380">frequência</span><span class="sxs-lookup"><span data-stu-id="ed017-380">frequency</span></span> |<span data-ttu-id="ed017-381">Especifica a unidade de tempo de saudação de produção de fatia do conjunto de dados.</span><span class="sxs-lookup"><span data-stu-id="ed017-381">Specifies hello time unit for dataset slice production.</span></span><br/><br/><span data-ttu-id="ed017-382"><b>Frequência com suporte</b>: Minuto, Hora, Dia, Semana, Mês</span><span class="sxs-lookup"><span data-stu-id="ed017-382"><b>Supported frequency</b>: Minute, Hour, Day, Week, Month</span></span> |<span data-ttu-id="ed017-383">Sim</span><span class="sxs-lookup"><span data-stu-id="ed017-383">Yes</span></span> |<span data-ttu-id="ed017-384">ND</span><span class="sxs-lookup"><span data-stu-id="ed017-384">NA</span></span> |
| <span data-ttu-id="ed017-385">intervalo</span><span class="sxs-lookup"><span data-stu-id="ed017-385">interval</span></span> |<span data-ttu-id="ed017-386">Especifica um multiplicador para frequência</span><span class="sxs-lookup"><span data-stu-id="ed017-386">Specifies a multiplier for frequency</span></span><br/><br/><span data-ttu-id="ed017-387">"Intervalo de frequência x" determina com que frequência hello fatia é produzida.</span><span class="sxs-lookup"><span data-stu-id="ed017-387">”Frequency x interval” determines how often hello slice is produced.</span></span><br/><br/><span data-ttu-id="ed017-388">Se você precisar hello toobe de conjunto de dados dividido por hora, defina <b>frequência</b> muito<b>hora</b>, e <b>intervalo</b> muito<b>1</b>.</span><span class="sxs-lookup"><span data-stu-id="ed017-388">If you need hello dataset toobe sliced on an hourly basis, you set <b>Frequency</b> too<b>Hour</b>, and <b>interval</b> too<b>1</b>.</span></span><br/><br/><span data-ttu-id="ed017-389"><b>Observação</b>: se você especificar a frequência como minuto, recomendamos que você defina Olá intervalo toono menor que 15</span><span class="sxs-lookup"><span data-stu-id="ed017-389"><b>Note</b>: If you specify Frequency as Minute, we recommend that you set hello interval toono less than 15</span></span> |<span data-ttu-id="ed017-390">Sim</span><span class="sxs-lookup"><span data-stu-id="ed017-390">Yes</span></span> |<span data-ttu-id="ed017-391">ND</span><span class="sxs-lookup"><span data-stu-id="ed017-391">NA</span></span> |
| <span data-ttu-id="ed017-392">estilo</span><span class="sxs-lookup"><span data-stu-id="ed017-392">style</span></span> |<span data-ttu-id="ed017-393">Especifica se a fatia Olá deve ser produzida no hello início/término do intervalo de saudação.</span><span class="sxs-lookup"><span data-stu-id="ed017-393">Specifies whether hello slice should be produced at hello start/end of hello interval.</span></span><ul><li><span data-ttu-id="ed017-394">StartOfInterval</span><span class="sxs-lookup"><span data-stu-id="ed017-394">StartOfInterval</span></span></li><li><span data-ttu-id="ed017-395">EndOfInterval</span><span class="sxs-lookup"><span data-stu-id="ed017-395">EndOfInterval</span></span></li></ul><br/><br/><span data-ttu-id="ed017-396">Quando frequência é definida tooMonth e o estilo definido tooEndOfInterval, fatia de saudação é produzida no último dia do mês de saudação.</span><span class="sxs-lookup"><span data-stu-id="ed017-396">If Frequency is set tooMonth and style is set tooEndOfInterval, hello slice is produced on hello last day of month.</span></span> <span data-ttu-id="ed017-397">Se o estilo de saudação é definido tooStartOfInterval, Olá fatia é produzida no hello primeiro dia do mês.</span><span class="sxs-lookup"><span data-stu-id="ed017-397">If hello style is set tooStartOfInterval, hello slice is produced on hello first day of month.</span></span><br/><br/><span data-ttu-id="ed017-398">Quando frequência é definida tooDay e o estilo definido tooEndOfInterval, fatia de Olá é produzida no hello última hora do dia de saudação.</span><span class="sxs-lookup"><span data-stu-id="ed017-398">If Frequency is set tooDay and style is set tooEndOfInterval, hello slice is produced in hello last hour of hello day.</span></span><br/><br/><span data-ttu-id="ed017-399">Quando frequência é definida tooHour e o estilo definido tooEndOfInterval, fatia de Olá é produzida no final de saudação de hora hello.</span><span class="sxs-lookup"><span data-stu-id="ed017-399">If Frequency is set tooHour and style is set tooEndOfInterval, hello slice is produced at hello end of hello hour.</span></span> <span data-ttu-id="ed017-400">Por exemplo, para uma fatia de período de 1 PM – 14: 00, a fatia de saudação é produzida às 14: 00.</span><span class="sxs-lookup"><span data-stu-id="ed017-400">For example, for a slice for 1 PM – 2 PM period, hello slice is produced at 2 PM.</span></span> |<span data-ttu-id="ed017-401">Não</span><span class="sxs-lookup"><span data-stu-id="ed017-401">No</span></span> |<span data-ttu-id="ed017-402">EndOfInterval</span><span class="sxs-lookup"><span data-stu-id="ed017-402">EndOfInterval</span></span> |
| <span data-ttu-id="ed017-403">anchorDateTime</span><span class="sxs-lookup"><span data-stu-id="ed017-403">anchorDateTime</span></span> |<span data-ttu-id="ed017-404">Define a posição absoluta Olá no tempo usado pelos limites de fatia do Agendador toocompute conjunto de dados.</span><span class="sxs-lookup"><span data-stu-id="ed017-404">Defines hello absolute position in time used by scheduler toocompute dataset slice boundaries.</span></span> <br/><br/><span data-ttu-id="ed017-405"><b>Observação</b>: se Olá AnchorDateTime tem partes de data mais granulares do que a frequência de hello, hello partes mais granulares são ignoradas.</span><span class="sxs-lookup"><span data-stu-id="ed017-405"><b>Note</b>: If hello AnchorDateTime has date parts that are more granular than hello frequency then hello more granular parts are ignored.</span></span> <br/><br/><span data-ttu-id="ed017-406">Por exemplo, se hello <b>intervalo</b> é <b>por hora</b> (frequência: hora e intervalo: 1) e hello <b>AnchorDateTime</b> contém <b>minutos e segundos</b>, em seguida, Olá <b>minutos e segundos</b> partes da saudação AnchorDateTime são ignoradas.</span><span class="sxs-lookup"><span data-stu-id="ed017-406">For example, if hello <b>interval</b> is <b>hourly</b> (frequency: hour and interval: 1) and hello <b>AnchorDateTime</b> contains <b>minutes and seconds</b> then hello <b>minutes and seconds</b> parts of hello AnchorDateTime are ignored.</span></span> |<span data-ttu-id="ed017-407">Não</span><span class="sxs-lookup"><span data-stu-id="ed017-407">No</span></span> |<span data-ttu-id="ed017-408">01/01/0001</span><span class="sxs-lookup"><span data-stu-id="ed017-408">01/01/0001</span></span> |
| <span data-ttu-id="ed017-409">deslocamento</span><span class="sxs-lookup"><span data-stu-id="ed017-409">offset</span></span> |<span data-ttu-id="ed017-410">O intervalo de tempo pelo qual saudação inicial e final de todas as fatias de conjunto de dados são transferidos.</span><span class="sxs-lookup"><span data-stu-id="ed017-410">Timespan by which hello start and end of all dataset slices are shifted.</span></span> <br/><br/><span data-ttu-id="ed017-411"><b>Observação</b>: se anchorDateTime e o deslocamento forem especificados, o resultado de saudação é shift Olá combinado.</span><span class="sxs-lookup"><span data-stu-id="ed017-411"><b>Note</b>: If both anchorDateTime and offset are specified, hello result is hello combined shift.</span></span> |<span data-ttu-id="ed017-412">Não</span><span class="sxs-lookup"><span data-stu-id="ed017-412">No</span></span> |<span data-ttu-id="ed017-413">ND</span><span class="sxs-lookup"><span data-stu-id="ed017-413">NA</span></span> |

<span data-ttu-id="ed017-414">Olá seção de disponibilidade a seguir especifica esse conjunto de dados de saída de saudação é produzido por hora (ou) entrada conjunto de dados está disponível por hora:</span><span class="sxs-lookup"><span data-stu-id="ed017-414">hello following availability section specifies that hello output dataset is either produced hourly (or) input dataset is available hourly:</span></span>

```json
"availability":    
{    
    "frequency": "Hour",        
    "interval": 1    
}
```

<span data-ttu-id="ed017-415">Olá **política** seção na definição de conjunto de dados define os critérios de saudação ou condição Olá Olá fatias de conjunto de dados deve ser atendidos.</span><span class="sxs-lookup"><span data-stu-id="ed017-415">hello **policy** section in dataset definition defines hello criteria or hello condition that hello dataset slices must fulfill.</span></span>

| <span data-ttu-id="ed017-416">Nome da política</span><span class="sxs-lookup"><span data-stu-id="ed017-416">Policy Name</span></span> | <span data-ttu-id="ed017-417">Descrição</span><span class="sxs-lookup"><span data-stu-id="ed017-417">Description</span></span> | <span data-ttu-id="ed017-418">Aplicado muito</span><span class="sxs-lookup"><span data-stu-id="ed017-418">Applied too</span></span>| <span data-ttu-id="ed017-419">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="ed017-419">Required</span></span> | <span data-ttu-id="ed017-420">Padrão</span><span class="sxs-lookup"><span data-stu-id="ed017-420">Default</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="ed017-421">minimumSizeMB</span><span class="sxs-lookup"><span data-stu-id="ed017-421">minimumSizeMB</span></span> |<span data-ttu-id="ed017-422">Valida que dados Olá em um **BLOBs do Azure** Olá de atende aos requisitos de tamanho mínimo (em megabytes).</span><span class="sxs-lookup"><span data-stu-id="ed017-422">Validates that hello data in an **Azure blob** meets hello minimum size requirements (in megabytes).</span></span> |<span data-ttu-id="ed017-423">Blob do Azure</span><span class="sxs-lookup"><span data-stu-id="ed017-423">Azure Blob</span></span> |<span data-ttu-id="ed017-424">Não</span><span class="sxs-lookup"><span data-stu-id="ed017-424">No</span></span> |<span data-ttu-id="ed017-425">ND</span><span class="sxs-lookup"><span data-stu-id="ed017-425">NA</span></span> |
| <span data-ttu-id="ed017-426">minimumRows</span><span class="sxs-lookup"><span data-stu-id="ed017-426">minimumRows</span></span> |<span data-ttu-id="ed017-427">Valida que dados Olá em um **banco de dados do SQL Azure** ou um **tabela do Azure** contém o número mínimo de saudação de linhas.</span><span class="sxs-lookup"><span data-stu-id="ed017-427">Validates that hello data in an **Azure SQL database** or an **Azure table** contains hello minimum number of rows.</span></span> |<ul><li><span data-ttu-id="ed017-428">Banco de Dados SQL do Azure</span><span class="sxs-lookup"><span data-stu-id="ed017-428">Azure SQL Database</span></span></li><li><span data-ttu-id="ed017-429">tabela do Azure</span><span class="sxs-lookup"><span data-stu-id="ed017-429">Azure Table</span></span></li></ul> |<span data-ttu-id="ed017-430">Não</span><span class="sxs-lookup"><span data-stu-id="ed017-430">No</span></span> |<span data-ttu-id="ed017-431">ND</span><span class="sxs-lookup"><span data-stu-id="ed017-431">NA</span></span> |

<span data-ttu-id="ed017-432">**Exemplo:**</span><span class="sxs-lookup"><span data-stu-id="ed017-432">**Example:**</span></span>

```json
"policy":

{
    "validation":
    {
        "minimumSizeMB": 10.0
    }
}
```

<span data-ttu-id="ed017-433">A menos que um conjunto de dados seja produzido pela Azure Data Factory, ele deverá ser marcado como **externo**.</span><span class="sxs-lookup"><span data-stu-id="ed017-433">Unless a dataset is being produced by Azure Data Factory, it should be marked as **external**.</span></span> <span data-ttu-id="ed017-434">Essa configuração geralmente se aplica a toohello entradas da primeira atividade em um pipeline, a menos que uma atividade ou o encadeamento de pipeline está sendo usado.</span><span class="sxs-lookup"><span data-stu-id="ed017-434">This setting generally applies toohello inputs of first activity in a pipeline unless activity or pipeline chaining is being used.</span></span>

| <span data-ttu-id="ed017-435">Nome</span><span class="sxs-lookup"><span data-stu-id="ed017-435">Name</span></span> | <span data-ttu-id="ed017-436">Descrição</span><span class="sxs-lookup"><span data-stu-id="ed017-436">Description</span></span> | <span data-ttu-id="ed017-437">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="ed017-437">Required</span></span> | <span data-ttu-id="ed017-438">Valor Padrão</span><span class="sxs-lookup"><span data-stu-id="ed017-438">Default Value</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="ed017-439">dataDelay</span><span class="sxs-lookup"><span data-stu-id="ed017-439">dataDelay</span></span> |<span data-ttu-id="ed017-440">Seleção de saudação toodelay tempo na disponibilidade de saudação de dados externa Olá Olá considerando a fatia.</span><span class="sxs-lookup"><span data-stu-id="ed017-440">Time toodelay hello check on hello availability of hello external data for hello given slice.</span></span> <span data-ttu-id="ed017-441">Por exemplo, se dados saudação estão disponíveis por hora, dados externos do Olá Olá seleção toosee estão disponíveis e fatia correspondente hello está pronto pode ser atrasado usando dataDelay.</span><span class="sxs-lookup"><span data-stu-id="ed017-441">For example, if hello data is available hourly, hello check toosee hello external data is available and hello corresponding slice is Ready can be delayed by using dataDelay.</span></span><br/><br/><span data-ttu-id="ed017-442">Aplica-se somente toohello a hora atual.</span><span class="sxs-lookup"><span data-stu-id="ed017-442">Only applies toohello present time.</span></span>  <span data-ttu-id="ed017-443">Por exemplo, se for 1:00 PM agora e esse valor é 10 minutos, validação Olá inicia às 13:10.</span><span class="sxs-lookup"><span data-stu-id="ed017-443">For example, if it is 1:00 PM right now and this value is 10 minutes, hello validation starts at 1:10 PM.</span></span><br/><br/><span data-ttu-id="ed017-444">Essa configuração não afeta fatias Olá passado (fatias com hora de término da fatia + dataDelay < agora) são processados sem atraso.</span><span class="sxs-lookup"><span data-stu-id="ed017-444">This setting does not affect slices in hello past (slices with Slice End Time + dataDelay < Now) are processed without any delay.</span></span><br/><br/><span data-ttu-id="ed017-445">Tempo maior que 23:59 horas necessário toospecified usando Olá `day.hours:minutes:seconds` formato.</span><span class="sxs-lookup"><span data-stu-id="ed017-445">Time greater than 23:59 hours need toospecified using hello `day.hours:minutes:seconds` format.</span></span> <span data-ttu-id="ed017-446">Por exemplo, toospecify 24 horas, não use 24:00:00; em vez disso, use 1.00:00:00.</span><span class="sxs-lookup"><span data-stu-id="ed017-446">For example, toospecify 24 hours, don't use 24:00:00; instead, use 1.00:00:00.</span></span> <span data-ttu-id="ed017-447">Se você usar 24:00:00, isso será tratado como 24 dias (24.00:00:00).</span><span class="sxs-lookup"><span data-stu-id="ed017-447">If you use 24:00:00, it is treated as 24 days (24.00:00:00).</span></span> <span data-ttu-id="ed017-448">Para 1 dia e 4 horas, especifique 1:04:00:00.</span><span class="sxs-lookup"><span data-stu-id="ed017-448">For 1 day and 4 hours, specify 1:04:00:00.</span></span> |<span data-ttu-id="ed017-449">Não</span><span class="sxs-lookup"><span data-stu-id="ed017-449">No</span></span> |<span data-ttu-id="ed017-450">0</span><span class="sxs-lookup"><span data-stu-id="ed017-450">0</span></span> |
| <span data-ttu-id="ed017-451">retryInterval</span><span class="sxs-lookup"><span data-stu-id="ed017-451">retryInterval</span></span> |<span data-ttu-id="ed017-452">tempo de espera de saudação entre uma falha e hello próxima tentativa.</span><span class="sxs-lookup"><span data-stu-id="ed017-452">hello wait time between a failure and hello next retry attempt.</span></span> <span data-ttu-id="ed017-453">Se uma tentativa falhar, a próxima tentativa de saudação é após retryInterval.</span><span class="sxs-lookup"><span data-stu-id="ed017-453">If a try fails, hello next try is after retryInterval.</span></span> <br/><br/><span data-ttu-id="ed017-454">Se for 1:00 PM agora, começamos Olá primeira tentativa.</span><span class="sxs-lookup"><span data-stu-id="ed017-454">If it is 1:00 PM right now, we begin hello first try.</span></span> <span data-ttu-id="ed017-455">Se Olá duração toocomplete Olá primeira verificação de validação é 1 minuto e Falha na operação de hello, Olá próxima tentativa é às 1:00 + 1 min (duração) + 1min (intervalo de repetição) = 1:02 PM.</span><span class="sxs-lookup"><span data-stu-id="ed017-455">If hello duration toocomplete hello first validation check is 1 minute and hello operation failed, hello next retry is at 1:00 + 1 min (duration) + 1 min (retry interval) = 1:02 PM.</span></span> <br/><br/><span data-ttu-id="ed017-456">Para fatias Olá anterior, não há nenhum atraso.</span><span class="sxs-lookup"><span data-stu-id="ed017-456">For slices in hello past, there is no delay.</span></span> <span data-ttu-id="ed017-457">repetição de saudação ocorre imediatamente.</span><span class="sxs-lookup"><span data-stu-id="ed017-457">hello retry happens immediately.</span></span> |<span data-ttu-id="ed017-458">Não</span><span class="sxs-lookup"><span data-stu-id="ed017-458">No</span></span> |<span data-ttu-id="ed017-459">00:01:00 (1 minuto)</span><span class="sxs-lookup"><span data-stu-id="ed017-459">00:01:00 (1 minute)</span></span> |
| <span data-ttu-id="ed017-460">retryTimeout</span><span class="sxs-lookup"><span data-stu-id="ed017-460">retryTimeout</span></span> |<span data-ttu-id="ed017-461">Olá tempo limite para cada tentativa de repetição.</span><span class="sxs-lookup"><span data-stu-id="ed017-461">hello timeout for each retry attempt.</span></span><br/><br/><span data-ttu-id="ed017-462">Se essa propriedade for definida too10 minutos, Olá toobe de necessidades de validação concluída em 10 minutos.</span><span class="sxs-lookup"><span data-stu-id="ed017-462">If this property is set too10 minutes, hello validation needs toobe completed within 10 minutes.</span></span> <span data-ttu-id="ed017-463">Se demorar mais de validação de saudação do tooperform de 10 minutos, Olá novamente o tempo limite.</span><span class="sxs-lookup"><span data-stu-id="ed017-463">If it takes longer than 10 minutes tooperform hello validation, hello retry times out.</span></span><br/><br/><span data-ttu-id="ed017-464">Se todas as tentativas de validação de saudação expira, fatia hello está marcada como TimedOut.</span><span class="sxs-lookup"><span data-stu-id="ed017-464">If all attempts for hello validation times out, hello slice is marked as TimedOut.</span></span> |<span data-ttu-id="ed017-465">Não</span><span class="sxs-lookup"><span data-stu-id="ed017-465">No</span></span> |<span data-ttu-id="ed017-466">00:10:00 (10 minutos)</span><span class="sxs-lookup"><span data-stu-id="ed017-466">00:10:00 (10 minutes)</span></span> |
| <span data-ttu-id="ed017-467">maximumRetry</span><span class="sxs-lookup"><span data-stu-id="ed017-467">maximumRetry</span></span> |<span data-ttu-id="ed017-468">Número de vezes toocheck para disponibilidade de saudação de dados externos de saudação.</span><span class="sxs-lookup"><span data-stu-id="ed017-468">Number of times toocheck for hello availability of hello external data.</span></span> <span data-ttu-id="ed017-469">Olá permitido valor máximo é 10.</span><span class="sxs-lookup"><span data-stu-id="ed017-469">hello allowed maximum value is 10.</span></span> |<span data-ttu-id="ed017-470">Não</span><span class="sxs-lookup"><span data-stu-id="ed017-470">No</span></span> |<span data-ttu-id="ed017-471">3</span><span class="sxs-lookup"><span data-stu-id="ed017-471">3</span></span> |


## <a name="data-stores"></a><span data-ttu-id="ed017-472">ARMAZENAMENTOS DE DADOS</span><span class="sxs-lookup"><span data-stu-id="ed017-472">DATA STORES</span></span>
<span data-ttu-id="ed017-473">Olá [serviço vinculado](#linked-service) descrições de seção fornecida para elementos JSON que são tipos comuns de tooall de serviços vinculados.</span><span class="sxs-lookup"><span data-stu-id="ed017-473">hello [Linked service](#linked-service) section provided descriptions for JSON elements that are common tooall types of linked services.</span></span> <span data-ttu-id="ed017-474">Esta seção fornece detalhes sobre os elementos JSON que são específicos tooeach repositório de dados.</span><span class="sxs-lookup"><span data-stu-id="ed017-474">This section provides details about JSON elements that are specific tooeach data store.</span></span>

<span data-ttu-id="ed017-475">Olá [Dataset](#dataset) descrições de seção fornecida para elementos JSON que são tipos comuns de tooall de conjuntos de dados.</span><span class="sxs-lookup"><span data-stu-id="ed017-475">hello [Dataset](#dataset) section provided descriptions for JSON elements that are common tooall types of datasets.</span></span> <span data-ttu-id="ed017-476">Esta seção fornece detalhes sobre os elementos JSON que são específicos tooeach repositório de dados.</span><span class="sxs-lookup"><span data-stu-id="ed017-476">This section provides details about JSON elements that are specific tooeach data store.</span></span>

<span data-ttu-id="ed017-477">Olá [atividade](#activity) descrições de seção fornecida para elementos JSON que são tipos de tooall comuns de atividades.</span><span class="sxs-lookup"><span data-stu-id="ed017-477">hello [Activity](#activity) section provided descriptions for JSON elements that are common tooall types of activities.</span></span> <span data-ttu-id="ed017-478">Esta seção fornece detalhes sobre os elementos JSON que são específicos tooeach repositório de dados quando ele é usado como um fonte/coletor em uma atividade de cópia.</span><span class="sxs-lookup"><span data-stu-id="ed017-478">This section provides details about JSON elements that are specific tooeach data store when it is used as a source/sink in a copy activity.</span></span>  

<span data-ttu-id="ed017-479">Clique Olá link armazenamento Olá você está interessado em esquemas JSON toosee Olá para o serviço vinculado, o conjunto de dados e Olá fonte/coletor de atividade de cópia de saudação.</span><span class="sxs-lookup"><span data-stu-id="ed017-479">Click hello link for hello store you are interested in toosee hello JSON schemas for linked service, dataset, and hello source/sink for hello copy activity.</span></span>

| <span data-ttu-id="ed017-480">Categoria</span><span class="sxs-lookup"><span data-stu-id="ed017-480">Category</span></span> | <span data-ttu-id="ed017-481">Armazenamento de dados</span><span class="sxs-lookup"><span data-stu-id="ed017-481">Data store</span></span> 
|:--- |:--- |
| <span data-ttu-id="ed017-482">**As tabelas**</span><span class="sxs-lookup"><span data-stu-id="ed017-482">**Azure**</span></span> |[<span data-ttu-id="ed017-483">Armazenamento de Blobs do Azure</span><span class="sxs-lookup"><span data-stu-id="ed017-483">Azure Blob storage</span></span>](#azure-blob-storage) |
| &nbsp; |[<span data-ttu-id="ed017-484">Repositório Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="ed017-484">Azure Data Lake Store</span></span>](#azure-datalake-store) |
| &nbsp; |[<span data-ttu-id="ed017-485">Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="ed017-485">Azure Cosmos DB</span></span>](#azure-cosmos-db) |
| &nbsp; |[<span data-ttu-id="ed017-486">Banco de Dados SQL do Azure</span><span class="sxs-lookup"><span data-stu-id="ed017-486">Azure SQL Database</span></span>](#azure-sql-database) |
| &nbsp; |[<span data-ttu-id="ed017-487">SQL Data Warehouse do Azure</span><span class="sxs-lookup"><span data-stu-id="ed017-487">Azure SQL Data Warehouse</span></span>](#azure-sql-data-warehouse) |
| &nbsp; |[<span data-ttu-id="ed017-488">Pesquisa do Azure</span><span class="sxs-lookup"><span data-stu-id="ed017-488">Azure Search</span></span>](#azure-search) |
| &nbsp; |[<span data-ttu-id="ed017-489">Armazenamento de Tabelas do Azure</span><span class="sxs-lookup"><span data-stu-id="ed017-489">Azure Table storage</span></span>](#azure-table-storage) |
| <span data-ttu-id="ed017-490">**Bancos de dados**</span><span class="sxs-lookup"><span data-stu-id="ed017-490">**Databases**</span></span> |[<span data-ttu-id="ed017-491">Amazon Redshift</span><span class="sxs-lookup"><span data-stu-id="ed017-491">Amazon Redshift</span></span>](#amazon-redshift) |
| &nbsp; |[<span data-ttu-id="ed017-492">IBM DB2</span><span class="sxs-lookup"><span data-stu-id="ed017-492">IBM DB2</span></span>](#ibm-db2) |
| &nbsp; |[<span data-ttu-id="ed017-493">MySQL</span><span class="sxs-lookup"><span data-stu-id="ed017-493">MySQL</span></span>](#mysql) |
| &nbsp; |[<span data-ttu-id="ed017-494">Oracle</span><span class="sxs-lookup"><span data-stu-id="ed017-494">Oracle</span></span>](#oracle) |
| &nbsp; |[<span data-ttu-id="ed017-495">PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="ed017-495">PostgreSQL</span></span>](#postgresql) |
| &nbsp; |[<span data-ttu-id="ed017-496">SAP Business Warehouse</span><span class="sxs-lookup"><span data-stu-id="ed017-496">SAP Business Warehouse</span></span>](#sap-business-warehouse) |
| &nbsp; |[<span data-ttu-id="ed017-497">SAP HANA</span><span class="sxs-lookup"><span data-stu-id="ed017-497">SAP HANA</span></span>](#sap-hana) |
| &nbsp; |[<span data-ttu-id="ed017-498">SQL Server</span><span class="sxs-lookup"><span data-stu-id="ed017-498">SQL Server</span></span>](#sql-server) |
| &nbsp; |[<span data-ttu-id="ed017-499">Sybase</span><span class="sxs-lookup"><span data-stu-id="ed017-499">Sybase</span></span>](#sybase) |
| &nbsp; |[<span data-ttu-id="ed017-500">Teradata</span><span class="sxs-lookup"><span data-stu-id="ed017-500">Teradata</span></span>](#teradata) |
| <span data-ttu-id="ed017-501">**NoSQL**</span><span class="sxs-lookup"><span data-stu-id="ed017-501">**NoSQL**</span></span> |[<span data-ttu-id="ed017-502">Cassandra</span><span class="sxs-lookup"><span data-stu-id="ed017-502">Cassandra</span></span>](#cassandra) |
| &nbsp; |[<span data-ttu-id="ed017-503">MongoDB</span><span class="sxs-lookup"><span data-stu-id="ed017-503">MongoDB</span></span>](#mongodb) |
| <span data-ttu-id="ed017-504">**Arquivo**</span><span class="sxs-lookup"><span data-stu-id="ed017-504">**File**</span></span> |[<span data-ttu-id="ed017-505">Amazon S3</span><span class="sxs-lookup"><span data-stu-id="ed017-505">Amazon S3</span></span>](#amazon-s3) |
| &nbsp; |[<span data-ttu-id="ed017-506">Sistema de Arquivos</span><span class="sxs-lookup"><span data-stu-id="ed017-506">File System</span></span>](#file-system) |
| &nbsp; |[<span data-ttu-id="ed017-507">FTP</span><span class="sxs-lookup"><span data-stu-id="ed017-507">FTP</span></span>](#ftp) |
| &nbsp; |[<span data-ttu-id="ed017-508">HDFS</span><span class="sxs-lookup"><span data-stu-id="ed017-508">HDFS</span></span>](#hdfs) |
| &nbsp; |[<span data-ttu-id="ed017-509">SFTP</span><span class="sxs-lookup"><span data-stu-id="ed017-509">SFTP</span></span>](#sftp) |
| <span data-ttu-id="ed017-510">**Outros**</span><span class="sxs-lookup"><span data-stu-id="ed017-510">**Others**</span></span> |[<span data-ttu-id="ed017-511">HTTP</span><span class="sxs-lookup"><span data-stu-id="ed017-511">HTTP</span></span>](#http) |
| &nbsp; |[<span data-ttu-id="ed017-512">OData</span><span class="sxs-lookup"><span data-stu-id="ed017-512">OData</span></span>](#odata) |
| &nbsp; |[<span data-ttu-id="ed017-513">ODBC</span><span class="sxs-lookup"><span data-stu-id="ed017-513">ODBC</span></span>](#odbc) |
| &nbsp; |[<span data-ttu-id="ed017-514">Salesforce</span><span class="sxs-lookup"><span data-stu-id="ed017-514">Salesforce</span></span>](#salesforce) |
| &nbsp; |[<span data-ttu-id="ed017-515">Tabela da Web</span><span class="sxs-lookup"><span data-stu-id="ed017-515">Web Table</span></span>](#web-table) |

## <a name="azure-blob-storage"></a><span data-ttu-id="ed017-516">Armazenamento do Blobs do Azure</span><span class="sxs-lookup"><span data-stu-id="ed017-516">Azure Blob Storage</span></span>

### <a name="linked-service"></a><span data-ttu-id="ed017-517">Serviço vinculado</span><span class="sxs-lookup"><span data-stu-id="ed017-517">Linked service</span></span>
<span data-ttu-id="ed017-518">Há dois tipos de serviços vinculados: serviço vinculado do Armazenamento do Azure e serviço vinculado do Armazenamento do Azure SAS.</span><span class="sxs-lookup"><span data-stu-id="ed017-518">There are two types of linked services: Azure Storage linked service and Azure Storage SAS linked service.</span></span>

#### <a name="azure-storage-linked-service"></a><span data-ttu-id="ed017-519">Serviço vinculado de armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="ed017-519">Azure Storage Linked Service</span></span>
<span data-ttu-id="ed017-520">toolink sua fábrica de dados de tooa da conta de armazenamento do Azure usando Olá **chave de conta**, crie um serviço vinculado do armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="ed017-520">toolink your Azure storage account tooa data factory by using hello **account key**, create an Azure Storage linked service.</span></span> <span data-ttu-id="ed017-521">toodefine um armazenamento do Azure vinculada serviço, Olá conjunto **tipo** de saudação serviço vinculado muito**AzureStorage**.</span><span class="sxs-lookup"><span data-stu-id="ed017-521">toodefine an Azure Storage linked service, set hello **type** of hello linked service too**AzureStorage**.</span></span> <span data-ttu-id="ed017-522">Em seguida, você pode especificar propriedades no Olá a seguir **typeProperties** seção:</span><span class="sxs-lookup"><span data-stu-id="ed017-522">Then, you can specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="ed017-523">Propriedade</span><span class="sxs-lookup"><span data-stu-id="ed017-523">Property</span></span> | <span data-ttu-id="ed017-524">Descrição</span><span class="sxs-lookup"><span data-stu-id="ed017-524">Description</span></span> | <span data-ttu-id="ed017-525">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="ed017-525">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="ed017-526">connectionString</span><span class="sxs-lookup"><span data-stu-id="ed017-526">connectionString</span></span> |<span data-ttu-id="ed017-527">Especifique informações necessárias tooconnect tooAzure armazenamento para a propriedade connectionString de saudação.</span><span class="sxs-lookup"><span data-stu-id="ed017-527">Specify information needed tooconnect tooAzure storage for hello connectionString property.</span></span> |<span data-ttu-id="ed017-528">Sim</span><span class="sxs-lookup"><span data-stu-id="ed017-528">Yes</span></span> |

##### <a name="example"></a><span data-ttu-id="ed017-529">Exemplo</span><span class="sxs-lookup"><span data-stu-id="ed017-529">Example</span></span>  

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

#### <a name="azure-storage-sas-linked-service"></a><span data-ttu-id="ed017-530">Serviço vinculado de SAS de Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="ed017-530">Azure Storage SAS Linked Service</span></span>
<span data-ttu-id="ed017-531">Olá SAS de armazenamento do Azure vinculada serviço permite que você toolink uma conta de armazenamento do Azure tooan data factory do Azure usando uma assinatura de acesso compartilhado (SAS).</span><span class="sxs-lookup"><span data-stu-id="ed017-531">hello Azure Storage SAS linked service allows you toolink an Azure Storage Account tooan Azure data factory by using a Shared Access Signature (SAS).</span></span> <span data-ttu-id="ed017-532">Ele fornece fábrica de dados Olá com acesso restrito/limite de tempo específicos/tooall recursos (blob/contêiner) no armazenamento de saudação.</span><span class="sxs-lookup"><span data-stu-id="ed017-532">It provides hello data factory with restricted/time-bound access tooall/specific resources (blob/container) in hello storage.</span></span> <span data-ttu-id="ed017-533">toolink sua fábrica de dados de tooa da conta de armazenamento do Azure usando a assinatura de acesso compartilhado, crie um serviço de SAS do armazenamento do Azure vinculado.</span><span class="sxs-lookup"><span data-stu-id="ed017-533">toolink your Azure storage account tooa data factory by using Shared Access Signature, create an Azure Storage SAS linked service.</span></span> <span data-ttu-id="ed017-534">toodefine um SAS de armazenamento do Azure vinculada serviço, Olá conjunto **tipo** de saudação serviço vinculado muito**o AzureStorageSas**.</span><span class="sxs-lookup"><span data-stu-id="ed017-534">toodefine an Azure Storage SAS linked service, set hello **type** of hello linked service too**AzureStorageSas**.</span></span> <span data-ttu-id="ed017-535">Em seguida, você pode especificar propriedades no Olá a seguir **typeProperties** seção:</span><span class="sxs-lookup"><span data-stu-id="ed017-535">Then, you can specify following properties in hello **typeProperties** section:</span></span>   

| <span data-ttu-id="ed017-536">Propriedade</span><span class="sxs-lookup"><span data-stu-id="ed017-536">Property</span></span> | <span data-ttu-id="ed017-537">Descrição</span><span class="sxs-lookup"><span data-stu-id="ed017-537">Description</span></span> | <span data-ttu-id="ed017-538">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="ed017-538">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="ed017-539">sasUri</span><span class="sxs-lookup"><span data-stu-id="ed017-539">sasUri</span></span> |<span data-ttu-id="ed017-540">Especifica os recursos de armazenamento do Azure do URI de assinatura de acesso compartilhado toohello como blob, contêiner ou tabela.</span><span class="sxs-lookup"><span data-stu-id="ed017-540">Specify Shared Access Signature URI toohello Azure Storage resources such as blob, container, or table.</span></span> |<span data-ttu-id="ed017-541">Sim</span><span class="sxs-lookup"><span data-stu-id="ed017-541">Yes</span></span> |

##### <a name="example"></a><span data-ttu-id="ed017-542">Exemplo</span><span class="sxs-lookup"><span data-stu-id="ed017-542">Example</span></span>

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

<span data-ttu-id="ed017-543">Para obter mais informações sobre esses serviços vinculados, consulte o artigo [Conector de Armazenamento de Blobs do Azure](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="ed017-543">For more information about these linked services, see [Azure Blob Storage connector](data-factory-azure-blob-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="ed017-544">Conjunto de dados</span><span class="sxs-lookup"><span data-stu-id="ed017-544">Dataset</span></span>
<span data-ttu-id="ed017-545">toodefine um conjunto de dados de Blob do Azure, Olá conjunto **tipo** do conjunto de dados de saudação muito**AzureBlob**.</span><span class="sxs-lookup"><span data-stu-id="ed017-545">toodefine an Azure Blob dataset, set hello **type** of hello dataset too**AzureBlob**.</span></span> <span data-ttu-id="ed017-546">Em seguida, especifique Olá seguintes propriedades específicas de BLOBs do Azure no hello **typeProperties** seção:</span><span class="sxs-lookup"><span data-stu-id="ed017-546">Then, specify hello following Azure Blob specific properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="ed017-547">Propriedade</span><span class="sxs-lookup"><span data-stu-id="ed017-547">Property</span></span> | <span data-ttu-id="ed017-548">Descrição</span><span class="sxs-lookup"><span data-stu-id="ed017-548">Description</span></span> | <span data-ttu-id="ed017-549">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="ed017-549">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ed017-550">folderPath</span><span class="sxs-lookup"><span data-stu-id="ed017-550">folderPath</span></span> |<span data-ttu-id="ed017-551">Contêiner de toohello do caminho e a pasta no armazenamento de blob hello.</span><span class="sxs-lookup"><span data-stu-id="ed017-551">Path toohello container and folder in hello blob storage.</span></span> <span data-ttu-id="ed017-552">Exemplo: myblobcontainer\myblobfolder\\</span><span class="sxs-lookup"><span data-stu-id="ed017-552">Example: myblobcontainer\myblobfolder\\</span></span> |<span data-ttu-id="ed017-553">Sim</span><span class="sxs-lookup"><span data-stu-id="ed017-553">Yes</span></span> |
| <span data-ttu-id="ed017-554">fileName</span><span class="sxs-lookup"><span data-stu-id="ed017-554">fileName</span></span> |<span data-ttu-id="ed017-555">Nome do blob hello.</span><span class="sxs-lookup"><span data-stu-id="ed017-555">Name of hello blob.</span></span> <span data-ttu-id="ed017-556">fileName é opcional e diferencia maiúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="ed017-556">fileName is optional and case-sensitive.</span></span><br/><br/><span data-ttu-id="ed017-557">Se você especificar um nome de arquivo, hello atividade (incluindo cópia) funciona em Olá Blob específico.</span><span class="sxs-lookup"><span data-stu-id="ed017-557">If you specify a filename, hello activity (including Copy) works on hello specific Blob.</span></span><br/><br/><span data-ttu-id="ed017-558">Quando o nome de arquivo não for especificado, cópia inclui todos os Blobs no folderPath Olá para o conjunto de dados de entrada.</span><span class="sxs-lookup"><span data-stu-id="ed017-558">When fileName is not specified, Copy includes all Blobs in hello folderPath for input dataset.</span></span><br/><br/><span data-ttu-id="ed017-559">Quando o nome de arquivo não for especificado para um conjunto de dados de saída, nome de saudação do arquivo hello gerado seria em Olá seguindo este formato: dados. <Guid>. txt (por exemplo:: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span><span class="sxs-lookup"><span data-stu-id="ed017-559">When fileName is not specified for an output dataset, hello name of hello generated file would be in hello following this format: Data.<Guid>.txt (for example: : Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span></span> |<span data-ttu-id="ed017-560">Não</span><span class="sxs-lookup"><span data-stu-id="ed017-560">No</span></span> |
| <span data-ttu-id="ed017-561">partitionedBy</span><span class="sxs-lookup"><span data-stu-id="ed017-561">partitionedBy</span></span> |<span data-ttu-id="ed017-562">partitionedBy é uma propriedade opcional.</span><span class="sxs-lookup"><span data-stu-id="ed017-562">partitionedBy is an optional property.</span></span> <span data-ttu-id="ed017-563">Você pode usar-ele toospecify um dinâmico folderPath e filename para dados de série temporal.</span><span class="sxs-lookup"><span data-stu-id="ed017-563">You can use it toospecify a dynamic folderPath and filename for time series data.</span></span> <span data-ttu-id="ed017-564">Por exemplo, folderPath pode ser parametrizado para cada hora dos dados.</span><span class="sxs-lookup"><span data-stu-id="ed017-564">For example, folderPath can be parameterized for every hour of data.</span></span> |<span data-ttu-id="ed017-565">Não</span><span class="sxs-lookup"><span data-stu-id="ed017-565">No</span></span> |
| <span data-ttu-id="ed017-566">formato</span><span class="sxs-lookup"><span data-stu-id="ed017-566">format</span></span> | <span data-ttu-id="ed017-567">Olá, tipos de formato a seguir têm suporte: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="ed017-567">hello following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="ed017-568">Saudação de conjunto **tipo** propriedade em formato tooone desses valores.</span><span class="sxs-lookup"><span data-stu-id="ed017-568">Set hello **type** property under format tooone of these values.</span></span> <span data-ttu-id="ed017-569">Para saber mais, veja as seções [Formato de texto](data-factory-supported-file-and-compression-formats.md#text-format), [Formato Json](data-factory-supported-file-and-compression-formats.md#json-format), [Formato Avro](data-factory-supported-file-and-compression-formats.md#avro-format), [Formato Orc](data-factory-supported-file-and-compression-formats.md#orc-format), e [Formato Parquet](data-factory-supported-file-and-compression-formats.md#parquet-format).</span><span class="sxs-lookup"><span data-stu-id="ed017-569">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="ed017-570">Se você quiser muito**copiar arquivos como-é** entre repositórios baseada em arquivo (cópia binário), ignore a seção de formato de saudação em ambas as definições de conjunto de dados de entrada e saída.</span><span class="sxs-lookup"><span data-stu-id="ed017-570">If you want too**copy files as-is** between file-based stores (binary copy), skip hello format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="ed017-571">Não</span><span class="sxs-lookup"><span data-stu-id="ed017-571">No</span></span> |
| <span data-ttu-id="ed017-572">compactação</span><span class="sxs-lookup"><span data-stu-id="ed017-572">compression</span></span> | <span data-ttu-id="ed017-573">Especifica tipo de saudação e nível de compactação de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="ed017-573">Specify hello type and level of compression for hello data.</span></span> <span data-ttu-id="ed017-574">Os tipos com suporte são: **GZip**, **Deflate**, **BZip2** e **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="ed017-574">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="ed017-575">Os níveis com suporte são **Ideal** e **O mais rápido**.</span><span class="sxs-lookup"><span data-stu-id="ed017-575">Supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="ed017-576">Para saber mais, confira [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support) (Formatos de arquivo e de compactação no Azure Data Factory).</span><span class="sxs-lookup"><span data-stu-id="ed017-576">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="ed017-577">Não</span><span class="sxs-lookup"><span data-stu-id="ed017-577">No</span></span> |

#### <a name="example"></a><span data-ttu-id="ed017-578">Exemplo</span><span class="sxs-lookup"><span data-stu-id="ed017-578">Example</span></span>

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


<span data-ttu-id="ed017-579">Para obter mais informações, consulte o artigo [Conector de Blob do Azure](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="ed017-579">For more information, see [Azure Blob connector](data-factory-azure-blob-connector.md#dataset-properties) article.</span></span>

### <a name="blobsource-in-copy-activity"></a><span data-ttu-id="ed017-580">BlobSource na Atividade de Cópia</span><span class="sxs-lookup"><span data-stu-id="ed017-580">BlobSource in Copy Activity</span></span>
<span data-ttu-id="ed017-581">Se você estiver copiando dados de um armazenamento de BLOBs do Azure, defina Olá **tipo de fonte** de hello atividade de cópia muito**BlobSource**e especificar propriedades no Olá a seguir * * fonte * * seção:</span><span class="sxs-lookup"><span data-stu-id="ed017-581">If you are copying data from an Azure Blob Storage, set hello **source type** of hello copy activity too**BlobSource**, and specify following properties in hello **source **section:</span></span>

| <span data-ttu-id="ed017-582">Propriedade</span><span class="sxs-lookup"><span data-stu-id="ed017-582">Property</span></span> | <span data-ttu-id="ed017-583">Descrição</span><span class="sxs-lookup"><span data-stu-id="ed017-583">Description</span></span> | <span data-ttu-id="ed017-584">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="ed017-584">Allowed values</span></span> | <span data-ttu-id="ed017-585">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="ed017-585">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="ed017-586">recursiva</span><span class="sxs-lookup"><span data-stu-id="ed017-586">recursive</span></span> |<span data-ttu-id="ed017-587">Indica se os dados saudação é lida recursivamente de subpastas de saudação ou somente de pasta especificado hello.</span><span class="sxs-lookup"><span data-stu-id="ed017-587">Indicates whether hello data is read recursively from hello sub folders or only from hello specified folder.</span></span> |<span data-ttu-id="ed017-588">True (valor padrão), False</span><span class="sxs-lookup"><span data-stu-id="ed017-588">True (default value), False</span></span> |<span data-ttu-id="ed017-589">Não</span><span class="sxs-lookup"><span data-stu-id="ed017-589">No</span></span> |

#### <a name="example-blobsource"></a><span data-ttu-id="ed017-590">Exemplo: BlobSource**</span><span class="sxs-lookup"><span data-stu-id="ed017-590">Example: BlobSource**</span></span>
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
### <a name="blobsink-in-copy-activity"></a><span data-ttu-id="ed017-591">BlobSink na Atividade de Cópia</span><span class="sxs-lookup"><span data-stu-id="ed017-591">BlobSink in Copy Activity</span></span>
<span data-ttu-id="ed017-592">Se você estiver copiando dados tooan armazenamento de BLOBs do Azure, defina Olá **tipo de coletor** de hello atividade de cópia muito**BlobSink**e especificar propriedades no Olá a seguir **coletor** seção:</span><span class="sxs-lookup"><span data-stu-id="ed017-592">If you are copying data tooan Azure Blob Storage, set hello **sink type** of hello copy activity too**BlobSink**, and specify following properties in hello **sink** section:</span></span>

| <span data-ttu-id="ed017-593">Propriedade</span><span class="sxs-lookup"><span data-stu-id="ed017-593">Property</span></span> | <span data-ttu-id="ed017-594">Descrição</span><span class="sxs-lookup"><span data-stu-id="ed017-594">Description</span></span> | <span data-ttu-id="ed017-595">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="ed017-595">Allowed values</span></span> | <span data-ttu-id="ed017-596">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="ed017-596">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="ed017-597">copyBehavior</span><span class="sxs-lookup"><span data-stu-id="ed017-597">copyBehavior</span></span> |<span data-ttu-id="ed017-598">Define o comportamento de cópia de saudação quando origem Olá é BlobSource ou sistema de arquivos.</span><span class="sxs-lookup"><span data-stu-id="ed017-598">Defines hello copy behavior when hello source is BlobSource or FileSystem.</span></span> |<span data-ttu-id="ed017-599"><b>PreserveHierarchy</b>: preserva Olá hierarquia de arquivos na pasta de destino de saudação.</span><span class="sxs-lookup"><span data-stu-id="ed017-599"><b>PreserveHierarchy</b>: preserves hello file hierarchy in hello target folder.</span></span> <span data-ttu-id="ed017-600">caminho relativo do Hello arquivo toosource da pasta de origem é idêntico toohello o caminho relativo da pasta de tootarget do arquivo de destino.</span><span class="sxs-lookup"><span data-stu-id="ed017-600">hello relative path of source file toosource folder is identical toohello relative path of target file tootarget folder.</span></span><br/><br/><span data-ttu-id="ed017-601"><b>FlattenHierarchy</b>: todos os arquivos da pasta de origem Olá estão em Olá primeiro níveis da pasta de destino.</span><span class="sxs-lookup"><span data-stu-id="ed017-601"><b>FlattenHierarchy</b>: all files from hello source folder are in hello first level of target folder.</span></span> <span data-ttu-id="ed017-602">os arquivos de destino de saudação têm nome gerado automaticamente.</span><span class="sxs-lookup"><span data-stu-id="ed017-602">hello target files have auto generated name.</span></span> <br/><br/><span data-ttu-id="ed017-603"><b>MergeFiles (padrão):</b> mescla todos os arquivos Olá pasta tooone do arquivo de origem.</span><span class="sxs-lookup"><span data-stu-id="ed017-603"><b>MergeFiles (default):</b> merges all files from hello source folder tooone file.</span></span> <span data-ttu-id="ed017-604">Se Olá nome de arquivo/Blob for especificado, o nome de arquivo mesclado de Olá seria nome especificado do hello. Caso contrário, seriam nome de arquivo gerado automaticamente.</span><span class="sxs-lookup"><span data-stu-id="ed017-604">If hello File/Blob Name is specified, hello merged file name would be hello specified name; otherwise, would be auto-generated file name.</span></span> |<span data-ttu-id="ed017-605">Não</span><span class="sxs-lookup"><span data-stu-id="ed017-605">No</span></span> |

#### <a name="example-blobsink"></a><span data-ttu-id="ed017-606">Exemplo: BlobSink</span><span class="sxs-lookup"><span data-stu-id="ed017-606">Example: BlobSink</span></span>

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

<span data-ttu-id="ed017-607">Para obter mais informações, consulte o artigo [Conector de Blob do Azure](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="ed017-607">For more information, see [Azure Blob connector](data-factory-azure-blob-connector.md#copy-activity-properties) article.</span></span> 

## <a name="azure-data-lake-store"></a><span data-ttu-id="ed017-608">Repositório Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="ed017-608">Azure Data Lake Store</span></span>

### <a name="linked-service"></a><span data-ttu-id="ed017-609">Serviço vinculado</span><span class="sxs-lookup"><span data-stu-id="ed017-609">Linked service</span></span>
<span data-ttu-id="ed017-610">toodefine um serviço de repositório Azure Data Lake vinculado, tipo de saudação do conjunto de saudação serviço vinculado muito**AzureDataLakeStore**e especificar propriedades no Olá a seguir **typeProperties** seção:</span><span class="sxs-lookup"><span data-stu-id="ed017-610">toodefine an Azure Data Lake Store linked service, set hello type of hello linked service too**AzureDataLakeStore**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="ed017-611">Propriedade</span><span class="sxs-lookup"><span data-stu-id="ed017-611">Property</span></span> | <span data-ttu-id="ed017-612">Descrição</span><span class="sxs-lookup"><span data-stu-id="ed017-612">Description</span></span> | <span data-ttu-id="ed017-613">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="ed017-613">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="ed017-614">type</span><span class="sxs-lookup"><span data-stu-id="ed017-614">type</span></span> | <span data-ttu-id="ed017-615">propriedade de tipo Hello deve ser definida como: **AzureDataLakeStore**</span><span class="sxs-lookup"><span data-stu-id="ed017-615">hello type property must be set to: **AzureDataLakeStore**</span></span> | <span data-ttu-id="ed017-616">Sim</span><span class="sxs-lookup"><span data-stu-id="ed017-616">Yes</span></span> |
| <span data-ttu-id="ed017-617">dataLakeStoreUri</span><span class="sxs-lookup"><span data-stu-id="ed017-617">dataLakeStoreUri</span></span> | <span data-ttu-id="ed017-618">Especifique informações sobre Olá conta do repositório Azure Data Lake.</span><span class="sxs-lookup"><span data-stu-id="ed017-618">Specify information about hello Azure Data Lake Store account.</span></span> <span data-ttu-id="ed017-619">É no hello formato a seguir: `https://[accountname].azuredatalakestore.net/webhdfs/v1` ou `adl://[accountname].azuredatalakestore.net/`.</span><span class="sxs-lookup"><span data-stu-id="ed017-619">It is in hello following format: `https://[accountname].azuredatalakestore.net/webhdfs/v1` or `adl://[accountname].azuredatalakestore.net/`.</span></span> | <span data-ttu-id="ed017-620">Sim</span><span class="sxs-lookup"><span data-stu-id="ed017-620">Yes</span></span> |
| <span data-ttu-id="ed017-621">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="ed017-621">subscriptionId</span></span> | <span data-ttu-id="ed017-622">Assinatura do Azure Id toowhich repositório Data Lake pertence.</span><span class="sxs-lookup"><span data-stu-id="ed017-622">Azure subscription Id toowhich Data Lake Store belongs.</span></span> | <span data-ttu-id="ed017-623">Obrigatório para coletor</span><span class="sxs-lookup"><span data-stu-id="ed017-623">Required for sink</span></span> |
| <span data-ttu-id="ed017-624">resourceGroupName</span><span class="sxs-lookup"><span data-stu-id="ed017-624">resourceGroupName</span></span> | <span data-ttu-id="ed017-625">Toowhich de nome de grupo de recursos do Azure repositório Data Lake pertence.</span><span class="sxs-lookup"><span data-stu-id="ed017-625">Azure resource group name toowhich Data Lake Store belongs.</span></span> | <span data-ttu-id="ed017-626">Obrigatório para coletor</span><span class="sxs-lookup"><span data-stu-id="ed017-626">Required for sink</span></span> |
| <span data-ttu-id="ed017-627">servicePrincipalId</span><span class="sxs-lookup"><span data-stu-id="ed017-627">servicePrincipalId</span></span> | <span data-ttu-id="ed017-628">Especifique a ID do cliente. do aplicativo hello</span><span class="sxs-lookup"><span data-stu-id="ed017-628">Specify hello application's client ID.</span></span> | <span data-ttu-id="ed017-629">Sim (para autenticação de entidade de serviço)</span><span class="sxs-lookup"><span data-stu-id="ed017-629">Yes (for service principal authentication)</span></span> |
| <span data-ttu-id="ed017-630">servicePrincipalKey</span><span class="sxs-lookup"><span data-stu-id="ed017-630">servicePrincipalKey</span></span> | <span data-ttu-id="ed017-631">Especifique a chave de aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="ed017-631">Specify hello application's key.</span></span> | <span data-ttu-id="ed017-632">Sim (para autenticação de entidade de serviço)</span><span class="sxs-lookup"><span data-stu-id="ed017-632">Yes (for service principal authentication)</span></span> |
| <span data-ttu-id="ed017-633">locatário</span><span class="sxs-lookup"><span data-stu-id="ed017-633">tenant</span></span> | <span data-ttu-id="ed017-634">Especifique as informações de locatário hello (ID de locatário ou de nome de domínio) em que o aplicativo reside.</span><span class="sxs-lookup"><span data-stu-id="ed017-634">Specify hello tenant information (domain name or tenant ID) under which your application resides.</span></span> <span data-ttu-id="ed017-635">Você pode recuperá-la por focalização mouse Olá no canto superior direito Olá Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="ed017-635">You can retrieve it by hovering hello mouse in hello top-right corner of hello Azure portal.</span></span> | <span data-ttu-id="ed017-636">Sim (para autenticação de entidade de serviço)</span><span class="sxs-lookup"><span data-stu-id="ed017-636">Yes (for service principal authentication)</span></span> |
| <span data-ttu-id="ed017-637">autorização</span><span class="sxs-lookup"><span data-stu-id="ed017-637">authorization</span></span> | <span data-ttu-id="ed017-638">Clique em **autorizar** botão Olá **Editor da fábrica de dados** e insira suas credenciais que atribui a propriedade de toothis de URL Olá autorização gerado automaticamente.</span><span class="sxs-lookup"><span data-stu-id="ed017-638">Click **Authorize** button in hello **Data Factory Editor** and enter your credential that assigns hello auto-generated authorization URL toothis property.</span></span> | <span data-ttu-id="ed017-639">Sim (para autenticação de credenciais de usuário)</span><span class="sxs-lookup"><span data-stu-id="ed017-639">Yes (for user credential authentication)</span></span>|
| <span data-ttu-id="ed017-640">sessionId</span><span class="sxs-lookup"><span data-stu-id="ed017-640">sessionId</span></span> | <span data-ttu-id="ed017-641">Id de sessão do OAuth da sessão de autorização de OAuth hello.</span><span class="sxs-lookup"><span data-stu-id="ed017-641">OAuth session id from hello OAuth authorization session.</span></span> <span data-ttu-id="ed017-642">Cada ID da sessão é exclusiva e pode ser usado somente uma vez.</span><span class="sxs-lookup"><span data-stu-id="ed017-642">Each session id is unique and may only be used once.</span></span> <span data-ttu-id="ed017-643">Essa configuração é gerada automaticamente quando você usa o Editor do Data Factory.</span><span class="sxs-lookup"><span data-stu-id="ed017-643">This setting is automatically generated when you use Data Factory Editor.</span></span> | <span data-ttu-id="ed017-644">Sim (para autenticação de credenciais de usuário)</span><span class="sxs-lookup"><span data-stu-id="ed017-644">Yes (for user credential authentication)</span></span> |

#### <a name="example-using-service-principal-authentication"></a><span data-ttu-id="ed017-645">Exemplo: usando a autenticação da entidade de serviço</span><span class="sxs-lookup"><span data-stu-id="ed017-645">Example: using service principal authentication</span></span>
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

#### <a name="example-using-user-credential-authentication"></a><span data-ttu-id="ed017-646">Exemplo: usando a autenticação de credenciais de usuário</span><span class="sxs-lookup"><span data-stu-id="ed017-646">Example: using user credential authentication</span></span>
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

<span data-ttu-id="ed017-647">Para saber mais, consulte o artigo [Conector do Azure Data Lake Store](data-factory-azure-datalake-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="ed017-647">For more information, see [Azure Data Lake Store connector](data-factory-azure-datalake-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="ed017-648">Conjunto de dados</span><span class="sxs-lookup"><span data-stu-id="ed017-648">Dataset</span></span>
<span data-ttu-id="ed017-649">toodefine um conjunto de dados do repositório Azure Data Lake conjunto Olá **tipo** do conjunto de dados de saudação muito**AzureDataLakeStore**e especifique Olá seguintes propriedades em Olá **typeProperties**seção:</span><span class="sxs-lookup"><span data-stu-id="ed017-649">toodefine an Azure Data Lake Store dataset, set hello **type** of hello dataset too**AzureDataLakeStore**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="ed017-650">Propriedade</span><span class="sxs-lookup"><span data-stu-id="ed017-650">Property</span></span> | <span data-ttu-id="ed017-651">Descrição</span><span class="sxs-lookup"><span data-stu-id="ed017-651">Description</span></span> | <span data-ttu-id="ed017-652">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="ed017-652">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="ed017-653">folderPath</span><span class="sxs-lookup"><span data-stu-id="ed017-653">folderPath</span></span> |<span data-ttu-id="ed017-654">Contêiner de toohello do caminho e a pasta em hello Azure Data Lake armazenam.</span><span class="sxs-lookup"><span data-stu-id="ed017-654">Path toohello container and folder in hello Azure Data Lake store.</span></span> |<span data-ttu-id="ed017-655">Sim</span><span class="sxs-lookup"><span data-stu-id="ed017-655">Yes</span></span> |
| <span data-ttu-id="ed017-656">fileName</span><span class="sxs-lookup"><span data-stu-id="ed017-656">fileName</span></span> |<span data-ttu-id="ed017-657">Nome do arquivo hello no armazenamento do Azure Data Lake hello.</span><span class="sxs-lookup"><span data-stu-id="ed017-657">Name of hello file in hello Azure Data Lake store.</span></span> <span data-ttu-id="ed017-658">fileName é opcional e diferencia maiúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="ed017-658">fileName is optional and case-sensitive.</span></span> <br/><br/><span data-ttu-id="ed017-659">Se você especificar um nome de arquivo, atividade de saudação (incluindo cópia) funciona em arquivos específicos da saudação.</span><span class="sxs-lookup"><span data-stu-id="ed017-659">If you specify a filename, hello activity (including Copy) works on hello specific file.</span></span><br/><br/><span data-ttu-id="ed017-660">Quando o nome de arquivo não for especificado, a cópia inclui todos os arquivos no folderPath Olá para o conjunto de dados de entrada.</span><span class="sxs-lookup"><span data-stu-id="ed017-660">When fileName is not specified, Copy includes all files in hello folderPath for input dataset.</span></span><br/><br/><span data-ttu-id="ed017-661">Quando o nome de arquivo não for especificado para um conjunto de dados de saída, nome de saudação do arquivo hello gerado seria em Olá seguindo este formato: dados. <Guid>. txt (por exemplo:: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span><span class="sxs-lookup"><span data-stu-id="ed017-661">When fileName is not specified for an output dataset, hello name of hello generated file would be in hello following this format: Data.<Guid>.txt (for example: : Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span></span> |<span data-ttu-id="ed017-662">Não</span><span class="sxs-lookup"><span data-stu-id="ed017-662">No</span></span> |
| <span data-ttu-id="ed017-663">partitionedBy</span><span class="sxs-lookup"><span data-stu-id="ed017-663">partitionedBy</span></span> |<span data-ttu-id="ed017-664">partitionedBy é uma propriedade opcional.</span><span class="sxs-lookup"><span data-stu-id="ed017-664">partitionedBy is an optional property.</span></span> <span data-ttu-id="ed017-665">Você pode usar-ele toospecify um dinâmico folderPath e filename para dados de série temporal.</span><span class="sxs-lookup"><span data-stu-id="ed017-665">You can use it toospecify a dynamic folderPath and filename for time series data.</span></span> <span data-ttu-id="ed017-666">Por exemplo, folderPath pode ser parametrizado para cada hora dos dados.</span><span class="sxs-lookup"><span data-stu-id="ed017-666">For example, folderPath can be parameterized for every hour of data.</span></span> |<span data-ttu-id="ed017-667">Não</span><span class="sxs-lookup"><span data-stu-id="ed017-667">No</span></span> |
| <span data-ttu-id="ed017-668">formato</span><span class="sxs-lookup"><span data-stu-id="ed017-668">format</span></span> | <span data-ttu-id="ed017-669">Olá, tipos de formato a seguir têm suporte: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="ed017-669">hello following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="ed017-670">Saudação de conjunto **tipo** propriedade em formato tooone desses valores.</span><span class="sxs-lookup"><span data-stu-id="ed017-670">Set hello **type** property under format tooone of these values.</span></span> <span data-ttu-id="ed017-671">Para saber mais, veja as seções [Formato de texto](data-factory-supported-file-and-compression-formats.md#text-format), [Formato Json](data-factory-supported-file-and-compression-formats.md#json-format), [Formato Avro](data-factory-supported-file-and-compression-formats.md#avro-format), [Formato Orc](data-factory-supported-file-and-compression-formats.md#orc-format), e [Formato Parquet](data-factory-supported-file-and-compression-formats.md#parquet-format).</span><span class="sxs-lookup"><span data-stu-id="ed017-671">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="ed017-672">Se você quiser muito**copiar arquivos como-é** entre repositórios baseada em arquivo (cópia binário), ignore a seção de formato de saudação em ambas as definições de conjunto de dados de entrada e saída.</span><span class="sxs-lookup"><span data-stu-id="ed017-672">If you want too**copy files as-is** between file-based stores (binary copy), skip hello format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="ed017-673">Não</span><span class="sxs-lookup"><span data-stu-id="ed017-673">No</span></span> |
| <span data-ttu-id="ed017-674">compactação</span><span class="sxs-lookup"><span data-stu-id="ed017-674">compression</span></span> | <span data-ttu-id="ed017-675">Especifica tipo de saudação e nível de compactação de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="ed017-675">Specify hello type and level of compression for hello data.</span></span> <span data-ttu-id="ed017-676">Os tipos com suporte são: **GZip**, **Deflate**, **BZip2** e **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="ed017-676">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="ed017-677">Os níveis com suporte são **Ideal** e **O mais rápido**.</span><span class="sxs-lookup"><span data-stu-id="ed017-677">Supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="ed017-678">Para saber mais, confira [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support) (Formatos de arquivo e de compactação no Azure Data Factory).</span><span class="sxs-lookup"><span data-stu-id="ed017-678">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="ed017-679">Não</span><span class="sxs-lookup"><span data-stu-id="ed017-679">No</span></span> |

#### <a name="example"></a><span data-ttu-id="ed017-680">Exemplo</span><span class="sxs-lookup"><span data-stu-id="ed017-680">Example</span></span>
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

<span data-ttu-id="ed017-681">Para saber mais, consulte o artigo [Conector do Azure Data Lake Store](data-factory-azure-datalake-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="ed017-681">For more information, see [Azure Data Lake Store connector](data-factory-azure-datalake-connector.md#dataset-properties) article.</span></span> 

### <a name="azure-data-lake-store-source-in-copy-activity"></a><span data-ttu-id="ed017-682">Fonte do Azure Data Lake Store na Atividade de Cópia</span><span class="sxs-lookup"><span data-stu-id="ed017-682">Azure Data Lake Store Source in Copy Activity</span></span>
<span data-ttu-id="ed017-683">Se você estiver copiando dados de um repositório Azure Data Lake, defina Olá **tipo de fonte** de hello atividade de cópia muito**AzureDataLakeStoreSource**e especificar propriedades no Olá a seguir **fonte**  seção:</span><span class="sxs-lookup"><span data-stu-id="ed017-683">If you are copying data from an Azure Data Lake Store, set hello **source type** of hello copy activity too**AzureDataLakeStoreSource**, and specify following properties in hello **source** section:</span></span>

<span data-ttu-id="ed017-684">**AzureDataLakeStoreSource** dá suporte a saudação seguintes propriedades **typeProperties** seção:</span><span class="sxs-lookup"><span data-stu-id="ed017-684">**AzureDataLakeStoreSource** supports hello following properties **typeProperties** section:</span></span>

| <span data-ttu-id="ed017-685">Propriedade</span><span class="sxs-lookup"><span data-stu-id="ed017-685">Property</span></span> | <span data-ttu-id="ed017-686">Descrição</span><span class="sxs-lookup"><span data-stu-id="ed017-686">Description</span></span> | <span data-ttu-id="ed017-687">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="ed017-687">Allowed values</span></span> | <span data-ttu-id="ed017-688">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="ed017-688">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="ed017-689">recursiva</span><span class="sxs-lookup"><span data-stu-id="ed017-689">recursive</span></span> |<span data-ttu-id="ed017-690">Indica se os dados saudação é lida recursivamente de subpastas de saudação ou somente de pasta especificado hello.</span><span class="sxs-lookup"><span data-stu-id="ed017-690">Indicates whether hello data is read recursively from hello sub folders or only from hello specified folder.</span></span> |<span data-ttu-id="ed017-691">True (valor padrão), False</span><span class="sxs-lookup"><span data-stu-id="ed017-691">True (default value), False</span></span> |<span data-ttu-id="ed017-692">Não</span><span class="sxs-lookup"><span data-stu-id="ed017-692">No</span></span> |

#### <a name="example-azuredatalakestoresource"></a><span data-ttu-id="ed017-693">Exemplo: AzureDataLakeStoreSource</span><span class="sxs-lookup"><span data-stu-id="ed017-693">Example: AzureDataLakeStoreSource</span></span>

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

<span data-ttu-id="ed017-694">Para saber mais, consulte o artigo [Conector do Azure Data Lake Store](data-factory-azure-datalake-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="ed017-694">For more information, see [Azure Data Lake Store connector](data-factory-azure-datalake-connector.md#copy-activity-properties) article.</span></span>

### <a name="azure-data-lake-store-sink-in-copy-activity"></a><span data-ttu-id="ed017-695">Coletor do Azure Data Lake Store na Atividade de Cópia</span><span class="sxs-lookup"><span data-stu-id="ed017-695">Azure Data Lake Store Sink in Copy Activity</span></span>
<span data-ttu-id="ed017-696">Se você estiver copiando o repositório de dados tooan Azure Data Lake, defina Olá **tipo de coletor** de hello atividade de cópia muito**AzureDataLakeStoreSink**e especificar propriedades no Olá a seguir **coletor**seção:</span><span class="sxs-lookup"><span data-stu-id="ed017-696">If you are copying data tooan Azure Data Lake Store, set hello **sink type** of hello copy activity too**AzureDataLakeStoreSink**, and specify following properties in hello **sink** section:</span></span>

| <span data-ttu-id="ed017-697">Propriedade</span><span class="sxs-lookup"><span data-stu-id="ed017-697">Property</span></span> | <span data-ttu-id="ed017-698">Descrição</span><span class="sxs-lookup"><span data-stu-id="ed017-698">Description</span></span> | <span data-ttu-id="ed017-699">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="ed017-699">Allowed values</span></span> | <span data-ttu-id="ed017-700">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="ed017-700">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="ed017-701">copyBehavior</span><span class="sxs-lookup"><span data-stu-id="ed017-701">copyBehavior</span></span> |<span data-ttu-id="ed017-702">Especifica o comportamento de cópia de saudação.</span><span class="sxs-lookup"><span data-stu-id="ed017-702">Specifies hello copy behavior.</span></span> |<span data-ttu-id="ed017-703"><b>PreserveHierarchy</b>: preserva Olá hierarquia de arquivos na pasta de destino de saudação.</span><span class="sxs-lookup"><span data-stu-id="ed017-703"><b>PreserveHierarchy</b>: preserves hello file hierarchy in hello target folder.</span></span> <span data-ttu-id="ed017-704">caminho relativo do Hello arquivo toosource da pasta de origem é idêntico toohello o caminho relativo da pasta de tootarget do arquivo de destino.</span><span class="sxs-lookup"><span data-stu-id="ed017-704">hello relative path of source file toosource folder is identical toohello relative path of target file tootarget folder.</span></span><br/><br/><span data-ttu-id="ed017-705"><b>FlattenHierarchy</b>: todos os arquivos da pasta de origem Olá são criados no primeiro nível saudação da pasta de destino.</span><span class="sxs-lookup"><span data-stu-id="ed017-705"><b>FlattenHierarchy</b>: all files from hello source folder are created in hello first level of target folder.</span></span> <span data-ttu-id="ed017-706">arquivos de destino de saudação são criados com o nome gerado automaticamente.</span><span class="sxs-lookup"><span data-stu-id="ed017-706">hello target files are created with auto generated name.</span></span><br/><br/><span data-ttu-id="ed017-707"><b>MergeFiles</b>: mescla todos os arquivos Olá pasta tooone do arquivo de origem.</span><span class="sxs-lookup"><span data-stu-id="ed017-707"><b>MergeFiles</b>: merges all files from hello source folder tooone file.</span></span> <span data-ttu-id="ed017-708">Se Olá nome de arquivo/Blob for especificado, o nome de arquivo mesclado de Olá seria nome especificado do hello. Caso contrário, seriam nome de arquivo gerado automaticamente.</span><span class="sxs-lookup"><span data-stu-id="ed017-708">If hello File/Blob Name is specified, hello merged file name would be hello specified name; otherwise, would be auto-generated file name.</span></span> |<span data-ttu-id="ed017-709">Não</span><span class="sxs-lookup"><span data-stu-id="ed017-709">No</span></span> |

#### <a name="example-azuredatalakestoresink"></a><span data-ttu-id="ed017-710">Exemplo: AzureDataLakeStoreSink</span><span class="sxs-lookup"><span data-stu-id="ed017-710">Example: AzureDataLakeStoreSink</span></span>
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

<span data-ttu-id="ed017-711">Para saber mais, consulte o artigo [Conector do Azure Data Lake Store](data-factory-azure-datalake-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="ed017-711">For more information, see [Azure Data Lake Store connector](data-factory-azure-datalake-connector.md#copy-activity-properties) article.</span></span> 

## <a name="azure-cosmos-db"></a><span data-ttu-id="ed017-712">Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="ed017-712">Azure Cosmos DB</span></span>  

### <a name="linked-service"></a><span data-ttu-id="ed017-713">Serviço vinculado</span><span class="sxs-lookup"><span data-stu-id="ed017-713">Linked service</span></span>
<span data-ttu-id="ed017-714">toodefine um banco de dados do Azure Cosmos o serviço saudação do conjunto vinculado **tipo** de saudação serviço vinculado muito**DocumentDb**e especificar propriedades no Olá a seguir **typeProperties** seção:</span><span class="sxs-lookup"><span data-stu-id="ed017-714">toodefine an Azure Cosmos DB linked service, set hello **type** of hello linked service too**DocumentDb**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="ed017-715">**Propriedade**</span><span class="sxs-lookup"><span data-stu-id="ed017-715">**Property**</span></span> | <span data-ttu-id="ed017-716">**Descrição**</span><span class="sxs-lookup"><span data-stu-id="ed017-716">**Description**</span></span> | <span data-ttu-id="ed017-717">**Obrigatório**</span><span class="sxs-lookup"><span data-stu-id="ed017-717">**Required**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ed017-718">connectionString</span><span class="sxs-lookup"><span data-stu-id="ed017-718">connectionString</span></span> |<span data-ttu-id="ed017-719">Especifique o banco de dados do banco de dados do Cosmos tooconnect tooAzure as informações necessárias.</span><span class="sxs-lookup"><span data-stu-id="ed017-719">Specify information needed tooconnect tooAzure Cosmos DB database.</span></span> |<span data-ttu-id="ed017-720">Sim</span><span class="sxs-lookup"><span data-stu-id="ed017-720">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="ed017-721">Exemplo</span><span class="sxs-lookup"><span data-stu-id="ed017-721">Example</span></span>

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
<span data-ttu-id="ed017-722">Para obter mais informações, consulte o artigo [Conector do Azure Cosmos DB](data-factory-azure-documentdb-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="ed017-722">For more information, see [Azure Cosmos DB connector](data-factory-azure-documentdb-connector.md#linked-service-properties) article.</span></span>

### <a name="dataset"></a><span data-ttu-id="ed017-723">Conjunto de dados</span><span class="sxs-lookup"><span data-stu-id="ed017-723">Dataset</span></span>
<span data-ttu-id="ed017-724">toodefine um conjunto de dados do banco de dados do Azure Cosmos conjunto Olá **tipo** do conjunto de dados de saudação muito**DocumentDbCollection**e especifique Olá seguintes propriedades em Olá **typeProperties** seção:</span><span class="sxs-lookup"><span data-stu-id="ed017-724">toodefine an Azure Cosmos DB dataset, set hello **type** of hello dataset too**DocumentDbCollection**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="ed017-725">**Propriedade**</span><span class="sxs-lookup"><span data-stu-id="ed017-725">**Property**</span></span> | <span data-ttu-id="ed017-726">**Descrição**</span><span class="sxs-lookup"><span data-stu-id="ed017-726">**Description**</span></span> | <span data-ttu-id="ed017-727">**Obrigatório**</span><span class="sxs-lookup"><span data-stu-id="ed017-727">**Required**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ed017-728">collectionName</span><span class="sxs-lookup"><span data-stu-id="ed017-728">collectionName</span></span> |<span data-ttu-id="ed017-729">Nome do hello Azure Cosmos DB coleção.</span><span class="sxs-lookup"><span data-stu-id="ed017-729">Name of hello Azure Cosmos DB collection.</span></span> |<span data-ttu-id="ed017-730">Sim</span><span class="sxs-lookup"><span data-stu-id="ed017-730">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="ed017-731">Exemplo</span><span class="sxs-lookup"><span data-stu-id="ed017-731">Example</span></span>

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
<span data-ttu-id="ed017-732">Para obter mais informações, consulte o artigo [Conector do Azure Cosmos DB](data-factory-azure-documentdb-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="ed017-732">For more information, see [Azure Cosmos DB connector](data-factory-azure-documentdb-connector.md#dataset-properties) article.</span></span>

### <a name="azure-cosmos-db-collection-source-in-copy-activity"></a><span data-ttu-id="ed017-733">Fonte de coleta do Azure Cosmos DB na Atividade de Cópia</span><span class="sxs-lookup"><span data-stu-id="ed017-733">Azure Cosmos DB Collection Source in Copy Activity</span></span>
<span data-ttu-id="ed017-734">Se você estiver copiando dados de um banco de dados do Azure Cosmos, defina Olá **tipo de fonte** de hello atividade de cópia muito**DocumentDbCollectionSource**e especificar propriedades no Olá a seguir **fonte** seção:</span><span class="sxs-lookup"><span data-stu-id="ed017-734">If you are copying data from an Azure Cosmos DB, set hello **source type** of hello copy activity too**DocumentDbCollectionSource**, and specify following properties in hello **source** section:</span></span>


| <span data-ttu-id="ed017-735">**Propriedade**</span><span class="sxs-lookup"><span data-stu-id="ed017-735">**Property**</span></span> | <span data-ttu-id="ed017-736">**Descrição**</span><span class="sxs-lookup"><span data-stu-id="ed017-736">**Description**</span></span> | <span data-ttu-id="ed017-737">**Valores permitidos**</span><span class="sxs-lookup"><span data-stu-id="ed017-737">**Allowed values**</span></span> | <span data-ttu-id="ed017-738">**Obrigatório**</span><span class="sxs-lookup"><span data-stu-id="ed017-738">**Required**</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="ed017-739">query</span><span class="sxs-lookup"><span data-stu-id="ed017-739">query</span></span> |<span data-ttu-id="ed017-740">Especifica Olá consulta tooread dados.</span><span class="sxs-lookup"><span data-stu-id="ed017-740">Specify hello query tooread data.</span></span> |<span data-ttu-id="ed017-741">Cadeia de consulta com suporte no Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="ed017-741">Query string supported by Azure Cosmos DB.</span></span> <br/><br/><span data-ttu-id="ed017-742">Exemplo: `SELECT c.BusinessEntityID, c.PersonType, c.NameStyle, c.Title, c.Name.First AS FirstName, c.Name.Last AS LastName, c.Suffix, c.EmailPromotion FROM c WHERE c.ModifiedDate > \"2009-01-01T00:00:00\"`</span><span class="sxs-lookup"><span data-stu-id="ed017-742">Example: `SELECT c.BusinessEntityID, c.PersonType, c.NameStyle, c.Title, c.Name.First AS FirstName, c.Name.Last AS LastName, c.Suffix, c.EmailPromotion FROM c WHERE c.ModifiedDate > \"2009-01-01T00:00:00\"`</span></span> |<span data-ttu-id="ed017-743">Não</span><span class="sxs-lookup"><span data-stu-id="ed017-743">No</span></span> <br/><br/><span data-ttu-id="ed017-744">Se não for especificado, Olá instrução SQL executada:`select <columns defined in structure> from mycollection`</span><span class="sxs-lookup"><span data-stu-id="ed017-744">If not specified, hello SQL statement that is executed: `select <columns defined in structure> from mycollection`</span></span> |
| <span data-ttu-id="ed017-745">nestingSeparator</span><span class="sxs-lookup"><span data-stu-id="ed017-745">nestingSeparator</span></span> |<span data-ttu-id="ed017-746">Caractere especial tooindicate que Olá documento está aninhado</span><span class="sxs-lookup"><span data-stu-id="ed017-746">Special character tooindicate that hello document is nested</span></span> |<span data-ttu-id="ed017-747">Qualquer caractere.</span><span class="sxs-lookup"><span data-stu-id="ed017-747">Any character.</span></span> <br/><br/><span data-ttu-id="ed017-748">O Azure Cosmos DB é um repositório NoSQL para documentos JSON, em que estruturas aninhadas são permitidas.</span><span class="sxs-lookup"><span data-stu-id="ed017-748">Azure Cosmos DB is a NoSQL store for JSON documents, where nested structures are allowed.</span></span> <span data-ttu-id="ed017-749">A fábrica de dados do Azure permite que a hierarquia de toodenote de usuário por meio de nestingSeparator, que é "."</span><span class="sxs-lookup"><span data-stu-id="ed017-749">Azure Data Factory enables user toodenote hierarchy via nestingSeparator, which is “.”</span></span> <span data-ttu-id="ed017-750">em hello acima exemplos.</span><span class="sxs-lookup"><span data-stu-id="ed017-750">in hello above examples.</span></span> <span data-ttu-id="ed017-751">Separador hello, atividade de cópia Olá irá gerar objeto de "Nome" hello com elementos de três filhos too"Name.First primeiro, intermediária e último, acordo", "Name.Middle" e ". Sobrenome" hello definição da tabela.</span><span class="sxs-lookup"><span data-stu-id="ed017-751">With hello separator, hello copy activity will generate hello “Name” object with three children elements First, Middle and Last, according too“Name.First”, “Name.Middle” and “Name.Last” in hello table definition.</span></span> |<span data-ttu-id="ed017-752">Não</span><span class="sxs-lookup"><span data-stu-id="ed017-752">No</span></span> |

#### <a name="example"></a><span data-ttu-id="ed017-753">Exemplo</span><span class="sxs-lookup"><span data-stu-id="ed017-753">Example</span></span>

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

### <a name="azure-cosmos-db-collection-sink-in-copy-activity"></a><span data-ttu-id="ed017-754">Coletor para coleta do Azure Cosmos DB na Atividade de Cópia</span><span class="sxs-lookup"><span data-stu-id="ed017-754">Azure Cosmos DB Collection Sink in Copy Activity</span></span>
<span data-ttu-id="ed017-755">Se você estiver copiando dados tooAzure Cosmos banco de dados, definir Olá **tipo de coletor** de hello atividade de cópia muito**DocumentDbCollectionSink**e especificar propriedades no Olá a seguir **coletor**seção:</span><span class="sxs-lookup"><span data-stu-id="ed017-755">If you are copying data tooAzure Cosmos DB, set hello **sink type** of hello copy activity too**DocumentDbCollectionSink**, and specify following properties in hello **sink** section:</span></span>

| <span data-ttu-id="ed017-756">**Propriedade**</span><span class="sxs-lookup"><span data-stu-id="ed017-756">**Property**</span></span> | <span data-ttu-id="ed017-757">**Descrição**</span><span class="sxs-lookup"><span data-stu-id="ed017-757">**Description**</span></span> | <span data-ttu-id="ed017-758">**Valores permitidos**</span><span class="sxs-lookup"><span data-stu-id="ed017-758">**Allowed values**</span></span> | <span data-ttu-id="ed017-759">**Obrigatório**</span><span class="sxs-lookup"><span data-stu-id="ed017-759">**Required**</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="ed017-760">nestingSeparator</span><span class="sxs-lookup"><span data-stu-id="ed017-760">nestingSeparator</span></span> |<span data-ttu-id="ed017-761">Um caractere especial em Olá fonte coluna Nome tooindicate que aninhada documento é necessário.</span><span class="sxs-lookup"><span data-stu-id="ed017-761">A special character in hello source column name tooindicate that nested document is needed.</span></span> <br/><br/><span data-ttu-id="ed017-762">Por exemplo acima: `Name.First` na saída de hello tabela produz Olá estrutura JSON no documento de banco de dados do Cosmos Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="ed017-762">For example above: `Name.First` in hello output table produces hello following JSON structure in hello Cosmos DB document:</span></span><br/><br/><span data-ttu-id="ed017-763">"Name": {</span><span class="sxs-lookup"><span data-stu-id="ed017-763">"Name": {</span></span><br/>    <span data-ttu-id="ed017-764">"First": "John"</span><span class="sxs-lookup"><span data-stu-id="ed017-764">"First": "John"</span></span><br/><span data-ttu-id="ed017-765">},</span><span class="sxs-lookup"><span data-stu-id="ed017-765">},</span></span> |<span data-ttu-id="ed017-766">Caractere usado tooseparate níveis de aninhamento.</span><span class="sxs-lookup"><span data-stu-id="ed017-766">Character that is used tooseparate nesting levels.</span></span><br/><br/><span data-ttu-id="ed017-767">O valor padrão é `.` (ponto).</span><span class="sxs-lookup"><span data-stu-id="ed017-767">Default value is `.` (dot).</span></span> |<span data-ttu-id="ed017-768">Caractere usado tooseparate níveis de aninhamento.</span><span class="sxs-lookup"><span data-stu-id="ed017-768">Character that is used tooseparate nesting levels.</span></span> <br/><br/><span data-ttu-id="ed017-769">O valor padrão é `.` (ponto).</span><span class="sxs-lookup"><span data-stu-id="ed017-769">Default value is `.` (dot).</span></span> |
| <span data-ttu-id="ed017-770">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="ed017-770">writeBatchSize</span></span> |<span data-ttu-id="ed017-771">Número de paralelo solicitações tooAzure documentos de toocreate do serviço de banco de dados do Cosmos.</span><span class="sxs-lookup"><span data-stu-id="ed017-771">Number of parallel requests tooAzure Cosmos DB service toocreate documents.</span></span><br/><br/><span data-ttu-id="ed017-772">Você pode ajustar o desempenho de saudação ao copiar dados de banco de dados do Azure Cosmos usando essa propriedade.</span><span class="sxs-lookup"><span data-stu-id="ed017-772">You can fine-tune hello performance when copying data to/from Azure Cosmos DB by using this property.</span></span> <span data-ttu-id="ed017-773">Você pode esperar um desempenho melhor quando você aumenta writeBatchSize porque mais solicitações paralelas tooAzure Cosmos banco de dados são enviados.</span><span class="sxs-lookup"><span data-stu-id="ed017-773">You can expect a better performance when you increase writeBatchSize because more parallel requests tooAzure Cosmos DB are sent.</span></span> <span data-ttu-id="ed017-774">No entanto, você precisará tooavoid limitação que pode gerar a mensagem de saudação do erro: "Solicitação de taxa for grande".</span><span class="sxs-lookup"><span data-stu-id="ed017-774">However you’ll need tooavoid throttling that can throw hello error message: "Request rate is large".</span></span><br/><br/><span data-ttu-id="ed017-775">A limitação é decida por uma série de fatores, incluindo o tamanho dos documentos, o número de termos incluídos, a política de indexação da coleção de destino, etc. Para operações de cópia, você pode usar uma saudação de toohave de coleção (por exemplo, S3) melhor taxa de transferência mais disponível (2.500 solicitação unidades/segundo).</span><span class="sxs-lookup"><span data-stu-id="ed017-775">Throttling is decided by a number of factors, including size of documents, number of terms in documents, indexing policy of target collection, etc. For copy operations, you can use a better collection (for example, S3) toohave hello most throughput available (2,500 request units/second).</span></span> |<span data-ttu-id="ed017-776">Número inteiro</span><span class="sxs-lookup"><span data-stu-id="ed017-776">Integer</span></span> |<span data-ttu-id="ed017-777">Não (padrão: 5)</span><span class="sxs-lookup"><span data-stu-id="ed017-777">No (default: 5)</span></span> |
| <span data-ttu-id="ed017-778">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="ed017-778">writeBatchTimeout</span></span> |<span data-ttu-id="ed017-779">Tempo de espera para Olá operação toocomplete antes de expirar.</span><span class="sxs-lookup"><span data-stu-id="ed017-779">Wait time for hello operation toocomplete before it times out.</span></span> |<span data-ttu-id="ed017-780">timespan</span><span class="sxs-lookup"><span data-stu-id="ed017-780">timespan</span></span><br/><br/> <span data-ttu-id="ed017-781">Exemplo: "00:30:00" (30 minutos).</span><span class="sxs-lookup"><span data-stu-id="ed017-781">Example: “00:30:00” (30 minutes).</span></span> |<span data-ttu-id="ed017-782">Não</span><span class="sxs-lookup"><span data-stu-id="ed017-782">No</span></span> |

#### <a name="example"></a><span data-ttu-id="ed017-783">Exemplo</span><span class="sxs-lookup"><span data-stu-id="ed017-783">Example</span></span>

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
                    "ColumnMappings": "FirstName: Name.First, MiddleName: Name.Middle, LastName: Name.Last, BusinessEntityID: BusinessEntityID, PersonType: PersonType, NameStyle: NameStyle, title: aaaTitle, Suffix: Suffix"
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

<span data-ttu-id="ed017-784">Para obter mais informações, consulte o artigo [Conector do Azure Cosmos DB](data-factory-azure-documentdb-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="ed017-784">For more information, see [Azure Cosmos DB connector](data-factory-azure-documentdb-connector.md#copy-activity-properties) article.</span></span>

## <a name="azure-sql-database"></a><span data-ttu-id="ed017-785">Banco de Dados SQL do Azure</span><span class="sxs-lookup"><span data-stu-id="ed017-785">Azure SQL Database</span></span>

### <a name="linked-service"></a><span data-ttu-id="ed017-786">Serviço vinculado</span><span class="sxs-lookup"><span data-stu-id="ed017-786">Linked service</span></span>
<span data-ttu-id="ed017-787">toodefine um banco de dados do SQL Azure vinculado serviço, Olá conjunto **tipo** de saudação serviço vinculado muito**AzureSqlDatabase**e especificar propriedades no Olá a seguir **typeProperties**seção:</span><span class="sxs-lookup"><span data-stu-id="ed017-787">toodefine an Azure SQL Database linked service, set hello **type** of hello linked service too**AzureSqlDatabase**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="ed017-788">Propriedade</span><span class="sxs-lookup"><span data-stu-id="ed017-788">Property</span></span> | <span data-ttu-id="ed017-789">Descrição</span><span class="sxs-lookup"><span data-stu-id="ed017-789">Description</span></span> | <span data-ttu-id="ed017-790">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="ed017-790">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ed017-791">connectionString</span><span class="sxs-lookup"><span data-stu-id="ed017-791">connectionString</span></span> |<span data-ttu-id="ed017-792">Especifique informações necessárias a instância de banco de dados do Azure SQL toohello tooconnect para a propriedade connectionString de saudação.</span><span class="sxs-lookup"><span data-stu-id="ed017-792">Specify information needed tooconnect toohello Azure SQL Database instance for hello connectionString property.</span></span> |<span data-ttu-id="ed017-793">Sim</span><span class="sxs-lookup"><span data-stu-id="ed017-793">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="ed017-794">Exemplo</span><span class="sxs-lookup"><span data-stu-id="ed017-794">Example</span></span>
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

<span data-ttu-id="ed017-795">Para obter mais informações, consulte o artigo [Conector de SQL do Azure](data-factory-azure-sql-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="ed017-795">For more information, see [Azure SQL connector](data-factory-azure-sql-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="ed017-796">Conjunto de dados</span><span class="sxs-lookup"><span data-stu-id="ed017-796">Dataset</span></span>
<span data-ttu-id="ed017-797">toodefine um conjunto de dados do banco de dados SQL, Olá conjunto **tipo** do conjunto de dados de saudação muito**AzureSqlTable**e especifique Olá seguintes propriedades em Olá **typeProperties** seção:</span><span class="sxs-lookup"><span data-stu-id="ed017-797">toodefine an Azure SQL Database dataset, set hello **type** of hello dataset too**AzureSqlTable**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="ed017-798">Propriedade</span><span class="sxs-lookup"><span data-stu-id="ed017-798">Property</span></span> | <span data-ttu-id="ed017-799">Descrição</span><span class="sxs-lookup"><span data-stu-id="ed017-799">Description</span></span> | <span data-ttu-id="ed017-800">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="ed017-800">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ed017-801">tableName</span><span class="sxs-lookup"><span data-stu-id="ed017-801">tableName</span></span> |<span data-ttu-id="ed017-802">Nome da tabela de saudação ou exibição na instância de banco de dados do Azure SQL Olá que serviço vinculado refere-se a.</span><span class="sxs-lookup"><span data-stu-id="ed017-802">Name of hello table or view in hello Azure SQL Database instance that linked service refers to.</span></span> |<span data-ttu-id="ed017-803">Sim</span><span class="sxs-lookup"><span data-stu-id="ed017-803">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="ed017-804">Exemplo</span><span class="sxs-lookup"><span data-stu-id="ed017-804">Example</span></span>

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
<span data-ttu-id="ed017-805">Para obter mais informações, consulte o artigo [Conector de SQL do Azure](data-factory-azure-sql-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="ed017-805">For more information, see [Azure SQL connector](data-factory-azure-sql-connector.md#dataset-properties) article.</span></span> 

### <a name="sql-source-in-copy-activity"></a><span data-ttu-id="ed017-806">Origem do SQL na atividade de cópia</span><span class="sxs-lookup"><span data-stu-id="ed017-806">SQL Source in Copy Activity</span></span>
<span data-ttu-id="ed017-807">Se você estiver copiando dados de um banco de dados do SQL Azure, defina Olá **tipo de fonte** de hello atividade de cópia muito**SqlSource**e especificar propriedades no Olá a seguir **fonte** seção:</span><span class="sxs-lookup"><span data-stu-id="ed017-807">If you are copying data from an Azure SQL Database, set hello **source type** of hello copy activity too**SqlSource**, and specify following properties in hello **source** section:</span></span>


| <span data-ttu-id="ed017-808">Propriedade</span><span class="sxs-lookup"><span data-stu-id="ed017-808">Property</span></span> | <span data-ttu-id="ed017-809">Descrição</span><span class="sxs-lookup"><span data-stu-id="ed017-809">Description</span></span> | <span data-ttu-id="ed017-810">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="ed017-810">Allowed values</span></span> | <span data-ttu-id="ed017-811">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="ed017-811">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="ed017-812">SqlReaderQuery</span><span class="sxs-lookup"><span data-stu-id="ed017-812">sqlReaderQuery</span></span> |<span data-ttu-id="ed017-813">Use dados de tooread Olá consulta personalizada.</span><span class="sxs-lookup"><span data-stu-id="ed017-813">Use hello custom query tooread data.</span></span> |<span data-ttu-id="ed017-814">Cadeia de caracteres de consulta SQL.</span><span class="sxs-lookup"><span data-stu-id="ed017-814">SQL query string.</span></span> <span data-ttu-id="ed017-815">Exemplo: `select * from MyTable`.</span><span class="sxs-lookup"><span data-stu-id="ed017-815">Example: `select * from MyTable`.</span></span> |<span data-ttu-id="ed017-816">Não</span><span class="sxs-lookup"><span data-stu-id="ed017-816">No</span></span> |
| <span data-ttu-id="ed017-817">sqlReaderStoredProcedureName</span><span class="sxs-lookup"><span data-stu-id="ed017-817">sqlReaderStoredProcedureName</span></span> |<span data-ttu-id="ed017-818">Nome da saudação procedimento armazenado que lê dados da tabela de origem hello.</span><span class="sxs-lookup"><span data-stu-id="ed017-818">Name of hello stored procedure that reads data from hello source table.</span></span> |<span data-ttu-id="ed017-819">Nome da saudação de procedimento armazenado.</span><span class="sxs-lookup"><span data-stu-id="ed017-819">Name of hello stored procedure.</span></span> |<span data-ttu-id="ed017-820">Não</span><span class="sxs-lookup"><span data-stu-id="ed017-820">No</span></span> |
| <span data-ttu-id="ed017-821">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="ed017-821">storedProcedureParameters</span></span> |<span data-ttu-id="ed017-822">Parâmetros de saudação de procedimento armazenado.</span><span class="sxs-lookup"><span data-stu-id="ed017-822">Parameters for hello stored procedure.</span></span> |<span data-ttu-id="ed017-823">Pares de nome/valor.</span><span class="sxs-lookup"><span data-stu-id="ed017-823">Name/value pairs.</span></span> <span data-ttu-id="ed017-824">Nomes e o uso de maiusculas e minúsculas dos parâmetros devem corresponder a nomes de saudação e uso de maiusculas e minúsculas dos parâmetros de procedimento armazenado de saudação.</span><span class="sxs-lookup"><span data-stu-id="ed017-824">Names and casing of parameters must match hello names and casing of hello stored procedure parameters.</span></span> |<span data-ttu-id="ed017-825">Não</span><span class="sxs-lookup"><span data-stu-id="ed017-825">No</span></span> |

#### <a name="example"></a><span data-ttu-id="ed017-826">Exemplo</span><span class="sxs-lookup"><span data-stu-id="ed017-826">Example</span></span>

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
<span data-ttu-id="ed017-827">Para obter mais informações, consulte o artigo [Conector de SQL do Azure](data-factory-azure-sql-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="ed017-827">For more information, see [Azure SQL connector](data-factory-azure-sql-connector.md#copy-activity-properties) article.</span></span> 

### <a name="sql-sink-in-copy-activity"></a><span data-ttu-id="ed017-828">Coletor do SQL na Atividade de Cópia</span><span class="sxs-lookup"><span data-stu-id="ed017-828">SQL Sink in Copy Activity</span></span>
<span data-ttu-id="ed017-829">Se você estiver copiando dados tooAzure banco de dados SQL, definir Olá **tipo de coletor** de hello atividade de cópia muito**SqlSink**e especificar propriedades no Olá a seguir **coletor** seção:</span><span class="sxs-lookup"><span data-stu-id="ed017-829">If you are copying data tooAzure SQL Database, set hello **sink type** of hello copy activity too**SqlSink**, and specify following properties in hello **sink** section:</span></span>

| <span data-ttu-id="ed017-830">Propriedade</span><span class="sxs-lookup"><span data-stu-id="ed017-830">Property</span></span> | <span data-ttu-id="ed017-831">Descrição</span><span class="sxs-lookup"><span data-stu-id="ed017-831">Description</span></span> | <span data-ttu-id="ed017-832">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="ed017-832">Allowed values</span></span> | <span data-ttu-id="ed017-833">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="ed017-833">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="ed017-834">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="ed017-834">writeBatchTimeout</span></span> |<span data-ttu-id="ed017-835">Tempo de espera para Olá toocomplete de operação de inserção de lote antes de expirar.</span><span class="sxs-lookup"><span data-stu-id="ed017-835">Wait time for hello batch insert operation toocomplete before it times out.</span></span> |<span data-ttu-id="ed017-836">timespan</span><span class="sxs-lookup"><span data-stu-id="ed017-836">timespan</span></span><br/><br/> <span data-ttu-id="ed017-837">Exemplo: "00:30:00" (30 minutos).</span><span class="sxs-lookup"><span data-stu-id="ed017-837">Example: “00:30:00” (30 minutes).</span></span> |<span data-ttu-id="ed017-838">Não</span><span class="sxs-lookup"><span data-stu-id="ed017-838">No</span></span> |
| <span data-ttu-id="ed017-839">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="ed017-839">writeBatchSize</span></span> |<span data-ttu-id="ed017-840">Insere dados na tabela do SQL hello quando o tamanho do buffer de saudação atingir writeBatchSize.</span><span class="sxs-lookup"><span data-stu-id="ed017-840">Inserts data into hello SQL table when hello buffer size reaches writeBatchSize.</span></span> |<span data-ttu-id="ed017-841">Inteiro (número de linhas)</span><span class="sxs-lookup"><span data-stu-id="ed017-841">Integer (number of rows)</span></span> |<span data-ttu-id="ed017-842">Não (padrão: 10000)</span><span class="sxs-lookup"><span data-stu-id="ed017-842">No (default: 10000)</span></span> |
| <span data-ttu-id="ed017-843">sqlWriterCleanupScript</span><span class="sxs-lookup"><span data-stu-id="ed017-843">sqlWriterCleanupScript</span></span> |<span data-ttu-id="ed017-844">Especifique uma consulta para a atividade de cópia tooexecute, de modo que os dados de uma fatia específica é limpa.</span><span class="sxs-lookup"><span data-stu-id="ed017-844">Specify a query for Copy Activity tooexecute such that data of a specific slice is cleaned up.</span></span> |<span data-ttu-id="ed017-845">Uma instrução de consulta.</span><span class="sxs-lookup"><span data-stu-id="ed017-845">A query statement.</span></span> |<span data-ttu-id="ed017-846">Não</span><span class="sxs-lookup"><span data-stu-id="ed017-846">No</span></span> |
| <span data-ttu-id="ed017-847">sliceIdentifierColumnName</span><span class="sxs-lookup"><span data-stu-id="ed017-847">sliceIdentifierColumnName</span></span> |<span data-ttu-id="ed017-848">Especifique um nome de coluna para a atividade de cópia toofill com identificador de fatia gerado automaticamente, que é usado tooclean os dados de uma fatia específica quando executada novamente.</span><span class="sxs-lookup"><span data-stu-id="ed017-848">Specify a column name for Copy Activity toofill with auto generated slice identifier, which is used tooclean up data of a specific slice when rerun.</span></span> |<span data-ttu-id="ed017-849">Nome de uma coluna com tipo de dados de binário (32).</span><span class="sxs-lookup"><span data-stu-id="ed017-849">Column name of a column with data type of binary(32).</span></span> |<span data-ttu-id="ed017-850">Não</span><span class="sxs-lookup"><span data-stu-id="ed017-850">No</span></span> |
| <span data-ttu-id="ed017-851">sqlWriterStoredProcedureName</span><span class="sxs-lookup"><span data-stu-id="ed017-851">sqlWriterStoredProcedureName</span></span> |<span data-ttu-id="ed017-852">Nome do hello procedimento armazenado dados upserts (atualizações/inserções) na tabela de destino de saudação.</span><span class="sxs-lookup"><span data-stu-id="ed017-852">Name of hello stored procedure that upserts (updates/inserts) data into hello target table.</span></span> |<span data-ttu-id="ed017-853">Nome da saudação de procedimento armazenado.</span><span class="sxs-lookup"><span data-stu-id="ed017-853">Name of hello stored procedure.</span></span> |<span data-ttu-id="ed017-854">Não</span><span class="sxs-lookup"><span data-stu-id="ed017-854">No</span></span> |
| <span data-ttu-id="ed017-855">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="ed017-855">storedProcedureParameters</span></span> |<span data-ttu-id="ed017-856">Parâmetros de saudação de procedimento armazenado.</span><span class="sxs-lookup"><span data-stu-id="ed017-856">Parameters for hello stored procedure.</span></span> |<span data-ttu-id="ed017-857">Pares de nome/valor.</span><span class="sxs-lookup"><span data-stu-id="ed017-857">Name/value pairs.</span></span> <span data-ttu-id="ed017-858">Nomes e o uso de maiusculas e minúsculas dos parâmetros devem corresponder a nomes de saudação e uso de maiusculas e minúsculas dos parâmetros de procedimento armazenado de saudação.</span><span class="sxs-lookup"><span data-stu-id="ed017-858">Names and casing of parameters must match hello names and casing of hello stored procedure parameters.</span></span> |<span data-ttu-id="ed017-859">Não</span><span class="sxs-lookup"><span data-stu-id="ed017-859">No</span></span> |
| <span data-ttu-id="ed017-860">sqlWriterTableType</span><span class="sxs-lookup"><span data-stu-id="ed017-860">sqlWriterTableType</span></span> |<span data-ttu-id="ed017-861">Especifique um toobe de nome de tipo de tabela usado no procedimento armazenado de saudação.</span><span class="sxs-lookup"><span data-stu-id="ed017-861">Specify a table type name toobe used in hello stored procedure.</span></span> <span data-ttu-id="ed017-862">Atividade de cópia disponibiliza dados Olá movidos em uma tabela temporária com esse tipo de tabela.</span><span class="sxs-lookup"><span data-stu-id="ed017-862">Copy activity makes hello data being moved available in a temp table with this table type.</span></span> <span data-ttu-id="ed017-863">Código do procedimento armazenado, em seguida, pode mesclar dados de saudação sejam copiados com os dados existentes.</span><span class="sxs-lookup"><span data-stu-id="ed017-863">Stored procedure code can then merge hello data being copied with existing data.</span></span> |<span data-ttu-id="ed017-864">Um nome de tipo de tabela.</span><span class="sxs-lookup"><span data-stu-id="ed017-864">A table type name.</span></span> |<span data-ttu-id="ed017-865">Não</span><span class="sxs-lookup"><span data-stu-id="ed017-865">No</span></span> |

#### <a name="example"></a><span data-ttu-id="ed017-866">Exemplo</span><span class="sxs-lookup"><span data-stu-id="ed017-866">Example</span></span>

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

<span data-ttu-id="ed017-867">Para obter mais informações, consulte o artigo [Conector de SQL do Azure](data-factory-azure-sql-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="ed017-867">For more information, see [Azure SQL connector](data-factory-azure-sql-connector.md#copy-activity-properties) article.</span></span> 

## <a name="azure-sql-data-warehouse"></a><span data-ttu-id="ed017-868">SQL Data Warehouse do Azure</span><span class="sxs-lookup"><span data-stu-id="ed017-868">Azure SQL Data Warehouse</span></span>

### <a name="linked-service"></a><span data-ttu-id="ed017-869">Serviço vinculado</span><span class="sxs-lookup"><span data-stu-id="ed017-869">Linked service</span></span>
<span data-ttu-id="ed017-870">toodefine um Azure SQL Data Warehouse vinculado serviço, Olá conjunto **tipo** de saudação serviço vinculado muito**AzureSqlDW**e especificar propriedades no Olá a seguir **typeProperties**seção:</span><span class="sxs-lookup"><span data-stu-id="ed017-870">toodefine an Azure SQL Data Warehouse linked service, set hello **type** of hello linked service too**AzureSqlDW**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="ed017-871">Propriedade</span><span class="sxs-lookup"><span data-stu-id="ed017-871">Property</span></span> | <span data-ttu-id="ed017-872">Descrição</span><span class="sxs-lookup"><span data-stu-id="ed017-872">Description</span></span> | <span data-ttu-id="ed017-873">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="ed017-873">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ed017-874">connectionString</span><span class="sxs-lookup"><span data-stu-id="ed017-874">connectionString</span></span> |<span data-ttu-id="ed017-875">Especifique informações necessárias a instância do tooconnect toohello Azure SQL Data Warehouse para a propriedade connectionString de saudação.</span><span class="sxs-lookup"><span data-stu-id="ed017-875">Specify information needed tooconnect toohello Azure SQL Data Warehouse instance for hello connectionString property.</span></span> |<span data-ttu-id="ed017-876">Sim</span><span class="sxs-lookup"><span data-stu-id="ed017-876">Yes</span></span> |



#### <a name="example"></a><span data-ttu-id="ed017-877">Exemplo</span><span class="sxs-lookup"><span data-stu-id="ed017-877">Example</span></span>

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

<span data-ttu-id="ed017-878">Para obter mais informações, consulte o artigo [Conector do SQL Data Warehouse do Azure](data-factory-azure-sql-data-warehouse-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="ed017-878">For more information, see [Azure SQL Data Warehouse connector](data-factory-azure-sql-data-warehouse-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="ed017-879">Conjunto de dados</span><span class="sxs-lookup"><span data-stu-id="ed017-879">Dataset</span></span>
<span data-ttu-id="ed017-880">toodefine um conjunto de dados do Azure SQL Data Warehouse, Olá conjunto **tipo** do conjunto de dados de saudação muito**AzureSqlDWTable**e especifique Olá seguintes propriedades em Olá **typeProperties**seção:</span><span class="sxs-lookup"><span data-stu-id="ed017-880">toodefine an Azure SQL Data Warehouse dataset, set hello **type** of hello dataset too**AzureSqlDWTable**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="ed017-881">Propriedade</span><span class="sxs-lookup"><span data-stu-id="ed017-881">Property</span></span> | <span data-ttu-id="ed017-882">Descrição</span><span class="sxs-lookup"><span data-stu-id="ed017-882">Description</span></span> | <span data-ttu-id="ed017-883">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="ed017-883">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ed017-884">tableName</span><span class="sxs-lookup"><span data-stu-id="ed017-884">tableName</span></span> |<span data-ttu-id="ed017-885">Nome da tabela de saudação ou exibição no banco de dados de Data warehouse do SQL Azure de saudação que Olá serviço vinculado refere-se a.</span><span class="sxs-lookup"><span data-stu-id="ed017-885">Name of hello table or view in hello Azure SQL Data Warehouse database that hello linked service refers to.</span></span> |<span data-ttu-id="ed017-886">Sim</span><span class="sxs-lookup"><span data-stu-id="ed017-886">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="ed017-887">Exemplo</span><span class="sxs-lookup"><span data-stu-id="ed017-887">Example</span></span>

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

<span data-ttu-id="ed017-888">Para obter mais informações, consulte o artigo [Conector do SQL Data Warehouse do Azure](data-factory-azure-sql-data-warehouse-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="ed017-888">For more information, see [Azure SQL Data Warehouse connector](data-factory-azure-sql-data-warehouse-connector.md#dataset-properties) article.</span></span> 

### <a name="sql-dw-source-in-copy-activity"></a><span data-ttu-id="ed017-889">Origem do SQL DW na Atividade de Cópia</span><span class="sxs-lookup"><span data-stu-id="ed017-889">SQL DW Source in Copy Activity</span></span>
<span data-ttu-id="ed017-890">Se você estiver copiando dados de Data warehouse do SQL Azure, defina Olá **tipo de fonte** de hello atividade de cópia muito**SqlDWSource**e especificar propriedades no Olá a seguir **fonte**seção:</span><span class="sxs-lookup"><span data-stu-id="ed017-890">If you are copying data from Azure SQL Data Warehouse, set hello **source type** of hello copy activity too**SqlDWSource**, and specify following properties in hello **source** section:</span></span>


| <span data-ttu-id="ed017-891">Propriedade</span><span class="sxs-lookup"><span data-stu-id="ed017-891">Property</span></span> | <span data-ttu-id="ed017-892">Descrição</span><span class="sxs-lookup"><span data-stu-id="ed017-892">Description</span></span> | <span data-ttu-id="ed017-893">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="ed017-893">Allowed values</span></span> | <span data-ttu-id="ed017-894">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="ed017-894">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="ed017-895">SqlReaderQuery</span><span class="sxs-lookup"><span data-stu-id="ed017-895">sqlReaderQuery</span></span> |<span data-ttu-id="ed017-896">Use dados de tooread Olá consulta personalizada.</span><span class="sxs-lookup"><span data-stu-id="ed017-896">Use hello custom query tooread data.</span></span> |<span data-ttu-id="ed017-897">Cadeia de caracteres de consulta SQL.</span><span class="sxs-lookup"><span data-stu-id="ed017-897">SQL query string.</span></span> <span data-ttu-id="ed017-898">Por exemplo: `select * from MyTable`.</span><span class="sxs-lookup"><span data-stu-id="ed017-898">For example: `select * from MyTable`.</span></span> |<span data-ttu-id="ed017-899">Não</span><span class="sxs-lookup"><span data-stu-id="ed017-899">No</span></span> |
| <span data-ttu-id="ed017-900">sqlReaderStoredProcedureName</span><span class="sxs-lookup"><span data-stu-id="ed017-900">sqlReaderStoredProcedureName</span></span> |<span data-ttu-id="ed017-901">Nome da saudação procedimento armazenado que lê dados da tabela de origem hello.</span><span class="sxs-lookup"><span data-stu-id="ed017-901">Name of hello stored procedure that reads data from hello source table.</span></span> |<span data-ttu-id="ed017-902">Nome da saudação de procedimento armazenado.</span><span class="sxs-lookup"><span data-stu-id="ed017-902">Name of hello stored procedure.</span></span> |<span data-ttu-id="ed017-903">Não</span><span class="sxs-lookup"><span data-stu-id="ed017-903">No</span></span> |
| <span data-ttu-id="ed017-904">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="ed017-904">storedProcedureParameters</span></span> |<span data-ttu-id="ed017-905">Parâmetros de saudação de procedimento armazenado.</span><span class="sxs-lookup"><span data-stu-id="ed017-905">Parameters for hello stored procedure.</span></span> |<span data-ttu-id="ed017-906">Pares de nome/valor.</span><span class="sxs-lookup"><span data-stu-id="ed017-906">Name/value pairs.</span></span> <span data-ttu-id="ed017-907">Nomes e o uso de maiusculas e minúsculas dos parâmetros devem corresponder a nomes de saudação e uso de maiusculas e minúsculas dos parâmetros de procedimento armazenado de saudação.</span><span class="sxs-lookup"><span data-stu-id="ed017-907">Names and casing of parameters must match hello names and casing of hello stored procedure parameters.</span></span> |<span data-ttu-id="ed017-908">Não</span><span class="sxs-lookup"><span data-stu-id="ed017-908">No</span></span> |

#### <a name="example"></a><span data-ttu-id="ed017-909">Exemplo</span><span class="sxs-lookup"><span data-stu-id="ed017-909">Example</span></span>

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

<span data-ttu-id="ed017-910">Para obter mais informações, consulte o artigo [Conector do SQL Data Warehouse do Azure](data-factory-azure-sql-data-warehouse-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="ed017-910">For more information, see [Azure SQL Data Warehouse connector](data-factory-azure-sql-data-warehouse-connector.md#copy-activity-properties) article.</span></span> 

### <a name="sql-dw-sink-in-copy-activity"></a><span data-ttu-id="ed017-911">Coletor do SQL DW na Atividade de Cópia</span><span class="sxs-lookup"><span data-stu-id="ed017-911">SQL DW Sink in Copy Activity</span></span>
<span data-ttu-id="ed017-912">Se você estiver copiando dados tooAzure SQL Data Warehouse, defina Olá **tipo de coletor** de hello atividade de cópia muito**SqlDWSink**e especificar propriedades no Olá a seguir **coletor** seção:</span><span class="sxs-lookup"><span data-stu-id="ed017-912">If you are copying data tooAzure SQL Data Warehouse, set hello **sink type** of hello copy activity too**SqlDWSink**, and specify following properties in hello **sink** section:</span></span>

| <span data-ttu-id="ed017-913">Propriedade</span><span class="sxs-lookup"><span data-stu-id="ed017-913">Property</span></span> | <span data-ttu-id="ed017-914">Descrição</span><span class="sxs-lookup"><span data-stu-id="ed017-914">Description</span></span> | <span data-ttu-id="ed017-915">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="ed017-915">Allowed values</span></span> | <span data-ttu-id="ed017-916">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="ed017-916">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="ed017-917">sqlWriterCleanupScript</span><span class="sxs-lookup"><span data-stu-id="ed017-917">sqlWriterCleanupScript</span></span> |<span data-ttu-id="ed017-918">Especifique uma consulta para a atividade de cópia tooexecute, de modo que os dados de uma fatia específica é limpa.</span><span class="sxs-lookup"><span data-stu-id="ed017-918">Specify a query for Copy Activity tooexecute such that data of a specific slice is cleaned up.</span></span> |<span data-ttu-id="ed017-919">Uma instrução de consulta.</span><span class="sxs-lookup"><span data-stu-id="ed017-919">A query statement.</span></span> |<span data-ttu-id="ed017-920">Não</span><span class="sxs-lookup"><span data-stu-id="ed017-920">No</span></span> |
| <span data-ttu-id="ed017-921">allowPolyBase</span><span class="sxs-lookup"><span data-stu-id="ed017-921">allowPolyBase</span></span> |<span data-ttu-id="ed017-922">Indica se toouse PolyBase (quando aplicável) em vez de mecanismo BULKINSERT.</span><span class="sxs-lookup"><span data-stu-id="ed017-922">Indicates whether toouse PolyBase (when applicable) instead of BULKINSERT mechanism.</span></span> <br/><br/> <span data-ttu-id="ed017-923">**Usar o PolyBase é hello recomendado a maneira como os dados tooload no SQL Data Warehouse.**</span><span class="sxs-lookup"><span data-stu-id="ed017-923">**Using PolyBase is hello recommended way tooload data into SQL Data Warehouse.**</span></span> |<span data-ttu-id="ed017-924">Verdadeiro</span><span class="sxs-lookup"><span data-stu-id="ed017-924">True</span></span> <br/><span data-ttu-id="ed017-925">False (padrão)</span><span class="sxs-lookup"><span data-stu-id="ed017-925">False (default)</span></span> |<span data-ttu-id="ed017-926">Não</span><span class="sxs-lookup"><span data-stu-id="ed017-926">No</span></span> |
| <span data-ttu-id="ed017-927">polyBaseSettings</span><span class="sxs-lookup"><span data-stu-id="ed017-927">polyBaseSettings</span></span> |<span data-ttu-id="ed017-928">Um grupo de propriedades que podem ser especificadas ao hello **allowPolybase** propriedade for definida muito**true**.</span><span class="sxs-lookup"><span data-stu-id="ed017-928">A group of properties that can be specified when hello **allowPolybase** property is set too**true**.</span></span> |&nbsp; |<span data-ttu-id="ed017-929">Não</span><span class="sxs-lookup"><span data-stu-id="ed017-929">No</span></span> |
| <span data-ttu-id="ed017-930">rejectValue</span><span class="sxs-lookup"><span data-stu-id="ed017-930">rejectValue</span></span> |<span data-ttu-id="ed017-931">Especifica o número de saudação ou a porcentagem de linhas que pode ser rejeitada antes Olá consulta falhe.</span><span class="sxs-lookup"><span data-stu-id="ed017-931">Specifies hello number or percentage of rows that can be rejected before hello query fails.</span></span> <br/><br/><span data-ttu-id="ed017-932">Saiba mais sobre do PolyBase Olá rejeitar opções Olá **argumentos** seção [CREATE EXTERNAL TABLE (Transact-SQL)](https://msdn.microsoft.com/library/dn935021.aspx) tópico.</span><span class="sxs-lookup"><span data-stu-id="ed017-932">Learn more about hello PolyBase’s reject options in hello **Arguments** section of [CREATE EXTERNAL TABLE (Transact-SQL)](https://msdn.microsoft.com/library/dn935021.aspx) topic.</span></span> |<span data-ttu-id="ed017-933">0 (padrão), 1, 2, …</span><span class="sxs-lookup"><span data-stu-id="ed017-933">0 (default), 1, 2, …</span></span> |<span data-ttu-id="ed017-934">Não</span><span class="sxs-lookup"><span data-stu-id="ed017-934">No</span></span> |
| <span data-ttu-id="ed017-935">rejectType</span><span class="sxs-lookup"><span data-stu-id="ed017-935">rejectType</span></span> |<span data-ttu-id="ed017-936">Especifica se a opção de rejectValue de saudação é especificada como um valor literal ou uma porcentagem.</span><span class="sxs-lookup"><span data-stu-id="ed017-936">Specifies whether hello rejectValue option is specified as a literal value or a percentage.</span></span> |<span data-ttu-id="ed017-937">Valor (padrão), Percentual</span><span class="sxs-lookup"><span data-stu-id="ed017-937">Value (default), Percentage</span></span> |<span data-ttu-id="ed017-938">Não</span><span class="sxs-lookup"><span data-stu-id="ed017-938">No</span></span> |
| <span data-ttu-id="ed017-939">rejectSampleValue</span><span class="sxs-lookup"><span data-stu-id="ed017-939">rejectSampleValue</span></span> |<span data-ttu-id="ed017-940">Determina o número de saudação de linhas tooretrieve antes Olá PolyBase recalcula a porcentagem de saudação de linhas rejeitadas.</span><span class="sxs-lookup"><span data-stu-id="ed017-940">Determines hello number of rows tooretrieve before hello PolyBase recalculates hello percentage of rejected rows.</span></span> |<span data-ttu-id="ed017-941">1, 2, …</span><span class="sxs-lookup"><span data-stu-id="ed017-941">1, 2, …</span></span> |<span data-ttu-id="ed017-942">Sim, se **rejectType** for **percentual**</span><span class="sxs-lookup"><span data-stu-id="ed017-942">Yes, if **rejectType** is **percentage**</span></span> |
| <span data-ttu-id="ed017-943">useTypeDefault</span><span class="sxs-lookup"><span data-stu-id="ed017-943">useTypeDefault</span></span> |<span data-ttu-id="ed017-944">Especifica como toohandle faltando valores delimitados por arquivos de texto quando PolyBase recupera dados do arquivo de texto de saudação.</span><span class="sxs-lookup"><span data-stu-id="ed017-944">Specifies how toohandle missing values in delimited text files when PolyBase retrieves data from hello text file.</span></span><br/><br/><span data-ttu-id="ed017-945">Saiba mais sobre essa propriedade da seção argumentos Olá [CREATE EXTERNAL FILE FORMAT (Transact-SQL)](https://msdn.microsoft.com/library/dn935026.aspx).</span><span class="sxs-lookup"><span data-stu-id="ed017-945">Learn more about this property from hello Arguments section in [CREATE EXTERNAL FILE FORMAT (Transact-SQL)](https://msdn.microsoft.com/library/dn935026.aspx).</span></span> |<span data-ttu-id="ed017-946">True, False (padrão)</span><span class="sxs-lookup"><span data-stu-id="ed017-946">True, False (default)</span></span> |<span data-ttu-id="ed017-947">Não</span><span class="sxs-lookup"><span data-stu-id="ed017-947">No</span></span> |
| <span data-ttu-id="ed017-948">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="ed017-948">writeBatchSize</span></span> |<span data-ttu-id="ed017-949">Insere dados na tabela do SQL hello quando o tamanho do buffer de saudação atingir writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="ed017-949">Inserts data into hello SQL table when hello buffer size reaches writeBatchSize</span></span> |<span data-ttu-id="ed017-950">Inteiro (número de linhas)</span><span class="sxs-lookup"><span data-stu-id="ed017-950">Integer (number of rows)</span></span> |<span data-ttu-id="ed017-951">Não (padrão: 10000)</span><span class="sxs-lookup"><span data-stu-id="ed017-951">No (default: 10000)</span></span> |
| <span data-ttu-id="ed017-952">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="ed017-952">writeBatchTimeout</span></span> |<span data-ttu-id="ed017-953">Tempo de espera para Olá toocomplete de operação de inserção de lote antes de expirar.</span><span class="sxs-lookup"><span data-stu-id="ed017-953">Wait time for hello batch insert operation toocomplete before it times out.</span></span> |<span data-ttu-id="ed017-954">timespan</span><span class="sxs-lookup"><span data-stu-id="ed017-954">timespan</span></span><br/><br/> <span data-ttu-id="ed017-955">Exemplo: "00:30:00" (30 minutos).</span><span class="sxs-lookup"><span data-stu-id="ed017-955">Example: “00:30:00” (30 minutes).</span></span> |<span data-ttu-id="ed017-956">Não</span><span class="sxs-lookup"><span data-stu-id="ed017-956">No</span></span> |

#### <a name="example"></a><span data-ttu-id="ed017-957">Exemplo</span><span class="sxs-lookup"><span data-stu-id="ed017-957">Example</span></span>

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

<span data-ttu-id="ed017-958">Para obter mais informações, consulte o artigo [Conector do SQL Data Warehouse do Azure](data-factory-azure-sql-data-warehouse-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="ed017-958">For more information, see [Azure SQL Data Warehouse connector](data-factory-azure-sql-data-warehouse-connector.md#copy-activity-properties) article.</span></span> 

## <a name="azure-search"></a><span data-ttu-id="ed017-959">Pesquisa do Azure</span><span class="sxs-lookup"><span data-stu-id="ed017-959">Azure Search</span></span>

### <a name="linked-service"></a><span data-ttu-id="ed017-960">Serviço vinculado</span><span class="sxs-lookup"><span data-stu-id="ed017-960">Linked service</span></span>
<span data-ttu-id="ed017-961">toodefine uma pesquisa do Azure vinculada serviço, Olá conjunto **tipo** de saudação serviço vinculado muito**AzureSearch**e especificar propriedades no Olá a seguir **typeProperties** seção:</span><span class="sxs-lookup"><span data-stu-id="ed017-961">toodefine an Azure Search linked service, set hello **type** of hello linked service too**AzureSearch**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="ed017-962">Propriedade</span><span class="sxs-lookup"><span data-stu-id="ed017-962">Property</span></span> | <span data-ttu-id="ed017-963">Descrição</span><span class="sxs-lookup"><span data-stu-id="ed017-963">Description</span></span> | <span data-ttu-id="ed017-964">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="ed017-964">Required</span></span> |
| -------- | ----------- | -------- |
| <span data-ttu-id="ed017-965">url</span><span class="sxs-lookup"><span data-stu-id="ed017-965">url</span></span> | <span data-ttu-id="ed017-966">URL de saudação serviço de pesquisa do Azure.</span><span class="sxs-lookup"><span data-stu-id="ed017-966">URL for hello Azure Search service.</span></span> | <span data-ttu-id="ed017-967">Sim</span><span class="sxs-lookup"><span data-stu-id="ed017-967">Yes</span></span> |
| <span data-ttu-id="ed017-968">chave</span><span class="sxs-lookup"><span data-stu-id="ed017-968">key</span></span> | <span data-ttu-id="ed017-969">Chave de administração de saudação serviço de pesquisa do Azure.</span><span class="sxs-lookup"><span data-stu-id="ed017-969">Admin key for hello Azure Search service.</span></span> | <span data-ttu-id="ed017-970">Sim</span><span class="sxs-lookup"><span data-stu-id="ed017-970">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="ed017-971">Exemplo</span><span class="sxs-lookup"><span data-stu-id="ed017-971">Example</span></span>

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

<span data-ttu-id="ed017-972">Para obter mais informações, consulte o artigo [Conector do Azure Search](data-factory-azure-search-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="ed017-972">For more information, see [Azure Search connector](data-factory-azure-search-connector.md#linked-service-properties) article.</span></span>

### <a name="dataset"></a><span data-ttu-id="ed017-973">Conjunto de dados</span><span class="sxs-lookup"><span data-stu-id="ed017-973">Dataset</span></span>
<span data-ttu-id="ed017-974">toodefine um conjunto de dados de pesquisa do Azure, Olá conjunto **tipo** do conjunto de dados de saudação muito**AzureSearchIndex**e especifique Olá seguintes propriedades em Olá **typeProperties** seção :</span><span class="sxs-lookup"><span data-stu-id="ed017-974">toodefine an Azure Search dataset, set hello **type** of hello dataset too**AzureSearchIndex**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="ed017-975">Propriedade</span><span class="sxs-lookup"><span data-stu-id="ed017-975">Property</span></span> | <span data-ttu-id="ed017-976">Descrição</span><span class="sxs-lookup"><span data-stu-id="ed017-976">Description</span></span> | <span data-ttu-id="ed017-977">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="ed017-977">Required</span></span> |
| -------- | ----------- | -------- |
| <span data-ttu-id="ed017-978">type</span><span class="sxs-lookup"><span data-stu-id="ed017-978">type</span></span> | <span data-ttu-id="ed017-979">propriedade do tipo Hello deve ser definida muito**AzureSearchIndex**.</span><span class="sxs-lookup"><span data-stu-id="ed017-979">hello type property must be set too**AzureSearchIndex**.</span></span>| <span data-ttu-id="ed017-980">Sim</span><span class="sxs-lookup"><span data-stu-id="ed017-980">Yes</span></span> |
| <span data-ttu-id="ed017-981">indexName</span><span class="sxs-lookup"><span data-stu-id="ed017-981">indexName</span></span> | <span data-ttu-id="ed017-982">Nome do índice de pesquisa do Azure hello.</span><span class="sxs-lookup"><span data-stu-id="ed017-982">Name of hello Azure Search index.</span></span> <span data-ttu-id="ed017-983">Fábrica de dados não cria o índice de saudação.</span><span class="sxs-lookup"><span data-stu-id="ed017-983">Data Factory does not create hello index.</span></span> <span data-ttu-id="ed017-984">Olá índice deve existir na pesquisa do Azure.</span><span class="sxs-lookup"><span data-stu-id="ed017-984">hello index must exist in Azure Search.</span></span> | <span data-ttu-id="ed017-985">Sim</span><span class="sxs-lookup"><span data-stu-id="ed017-985">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="ed017-986">Exemplo</span><span class="sxs-lookup"><span data-stu-id="ed017-986">Example</span></span>

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

<span data-ttu-id="ed017-987">Para obter mais informações, consulte o artigo [Conector do Azure Search](data-factory-azure-search-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="ed017-987">For more information, see [Azure Search connector](data-factory-azure-search-connector.md#dataset-properties) article.</span></span>

### <a name="azure-search-index-sink-in-copy-activity"></a><span data-ttu-id="ed017-988">Coletor do Índice do Azure Search na Atividade de Cópia</span><span class="sxs-lookup"><span data-stu-id="ed017-988">Azure Search Index Sink in Copy Activity</span></span>
<span data-ttu-id="ed017-989">Se você estiver copiando o índice de pesquisa do Azure tooan dados, definir Olá **tipo de coletor** de hello atividade de cópia muito**AzureSearchIndexSink**e especificar propriedades no Olá a seguir **coletor**seção:</span><span class="sxs-lookup"><span data-stu-id="ed017-989">If you are copying data tooan Azure Search index, set hello **sink type** of hello copy activity too**AzureSearchIndexSink**, and specify following properties in hello **sink** section:</span></span>

| <span data-ttu-id="ed017-990">Propriedade</span><span class="sxs-lookup"><span data-stu-id="ed017-990">Property</span></span> | <span data-ttu-id="ed017-991">Descrição</span><span class="sxs-lookup"><span data-stu-id="ed017-991">Description</span></span> | <span data-ttu-id="ed017-992">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="ed017-992">Allowed values</span></span> | <span data-ttu-id="ed017-993">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="ed017-993">Required</span></span> |
| -------- | ----------- | -------------- | -------- |
| <span data-ttu-id="ed017-994">WriteBehavior</span><span class="sxs-lookup"><span data-stu-id="ed017-994">WriteBehavior</span></span> | <span data-ttu-id="ed017-995">Especifica se toomerge ou substituição quando um documento já existe no índice de saudação.</span><span class="sxs-lookup"><span data-stu-id="ed017-995">Specifies whether toomerge or replace when a document already exists in hello index.</span></span> | <span data-ttu-id="ed017-996">Merge (padrão)</span><span class="sxs-lookup"><span data-stu-id="ed017-996">Merge (default)</span></span><br/><span data-ttu-id="ed017-997">Carregar</span><span class="sxs-lookup"><span data-stu-id="ed017-997">Upload</span></span>| <span data-ttu-id="ed017-998">Não</span><span class="sxs-lookup"><span data-stu-id="ed017-998">No</span></span> |
| <span data-ttu-id="ed017-999">WriteBatchSize</span><span class="sxs-lookup"><span data-stu-id="ed017-999">WriteBatchSize</span></span> | <span data-ttu-id="ed017-1000">Carrega dados no índice de pesquisa do Azure hello quando o tamanho do buffer de saudação atingir writeBatchSize.</span><span class="sxs-lookup"><span data-stu-id="ed017-1000">Uploads data into hello Azure Search index when hello buffer size reaches writeBatchSize.</span></span> | <span data-ttu-id="ed017-1001">1 too1, 000.</span><span class="sxs-lookup"><span data-stu-id="ed017-1001">1 too1,000.</span></span> <span data-ttu-id="ed017-1002">O valor padrão é 1000.</span><span class="sxs-lookup"><span data-stu-id="ed017-1002">Default value is 1000.</span></span> | <span data-ttu-id="ed017-1003">Não</span><span class="sxs-lookup"><span data-stu-id="ed017-1003">No</span></span> |

#### <a name="example"></a><span data-ttu-id="ed017-1004">Exemplo</span><span class="sxs-lookup"><span data-stu-id="ed017-1004">Example</span></span>

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

<span data-ttu-id="ed017-1005">Para obter mais informações, consulte o artigo [Conector do Azure Search](data-factory-azure-search-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="ed017-1005">For more information, see [Azure Search connector](data-factory-azure-search-connector.md#copy-activity-properties) article.</span></span>

## <a name="azure-table-storage"></a><span data-ttu-id="ed017-1006">Armazenamento de Tabelas do Azure</span><span class="sxs-lookup"><span data-stu-id="ed017-1006">Azure Table Storage</span></span>

### <a name="linked-service"></a><span data-ttu-id="ed017-1007">Serviço vinculado</span><span class="sxs-lookup"><span data-stu-id="ed017-1007">Linked service</span></span>
<span data-ttu-id="ed017-1008">Há dois tipos de serviços vinculados: serviço vinculado do Armazenamento do Azure e serviço vinculado do Armazenamento do Azure SAS.</span><span class="sxs-lookup"><span data-stu-id="ed017-1008">There are two types of linked services: Azure Storage linked service and Azure Storage SAS linked service.</span></span>

#### <a name="azure-storage-linked-service"></a><span data-ttu-id="ed017-1009">Serviço vinculado de armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="ed017-1009">Azure Storage Linked Service</span></span>
<span data-ttu-id="ed017-1010">toolink sua fábrica de dados de tooa da conta de armazenamento do Azure usando Olá **chave de conta**, crie um serviço vinculado do armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="ed017-1010">toolink your Azure storage account tooa data factory by using hello **account key**, create an Azure Storage linked service.</span></span> <span data-ttu-id="ed017-1011">toodefine um armazenamento do Azure vinculada serviço, Olá conjunto **tipo** de saudação serviço vinculado muito**AzureStorage**.</span><span class="sxs-lookup"><span data-stu-id="ed017-1011">toodefine an Azure Storage linked service, set hello **type** of hello linked service too**AzureStorage**.</span></span> <span data-ttu-id="ed017-1012">Em seguida, você pode especificar propriedades no Olá a seguir **typeProperties** seção:</span><span class="sxs-lookup"><span data-stu-id="ed017-1012">Then, you can specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="ed017-1013">Propriedade</span><span class="sxs-lookup"><span data-stu-id="ed017-1013">Property</span></span> | <span data-ttu-id="ed017-1014">Descrição</span><span class="sxs-lookup"><span data-stu-id="ed017-1014">Description</span></span> | <span data-ttu-id="ed017-1015">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="ed017-1015">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="ed017-1016">type</span><span class="sxs-lookup"><span data-stu-id="ed017-1016">type</span></span> |<span data-ttu-id="ed017-1017">propriedade de tipo Hello deve ser definida como: **AzureStorage**</span><span class="sxs-lookup"><span data-stu-id="ed017-1017">hello type property must be set to: **AzureStorage**</span></span> |<span data-ttu-id="ed017-1018">Sim</span><span class="sxs-lookup"><span data-stu-id="ed017-1018">Yes</span></span> |
| <span data-ttu-id="ed017-1019">connectionString</span><span class="sxs-lookup"><span data-stu-id="ed017-1019">connectionString</span></span> |<span data-ttu-id="ed017-1020">Especifique informações necessárias tooconnect tooAzure armazenamento para a propriedade connectionString de saudação.</span><span class="sxs-lookup"><span data-stu-id="ed017-1020">Specify information needed tooconnect tooAzure storage for hello connectionString property.</span></span> |<span data-ttu-id="ed017-1021">Sim</span><span class="sxs-lookup"><span data-stu-id="ed017-1021">Yes</span></span> |

<span data-ttu-id="ed017-1022">**Exemplo:**</span><span class="sxs-lookup"><span data-stu-id="ed017-1022">**Example:**</span></span>  

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

#### <a name="azure-storage-sas-linked-service"></a><span data-ttu-id="ed017-1023">Serviço vinculado de SAS de Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="ed017-1023">Azure Storage SAS Linked Service</span></span>
<span data-ttu-id="ed017-1024">Olá SAS de armazenamento do Azure vinculada serviço permite que você toolink uma conta de armazenamento do Azure tooan data factory do Azure usando uma assinatura de acesso compartilhado (SAS).</span><span class="sxs-lookup"><span data-stu-id="ed017-1024">hello Azure Storage SAS linked service allows you toolink an Azure Storage Account tooan Azure data factory by using a Shared Access Signature (SAS).</span></span> <span data-ttu-id="ed017-1025">Ele fornece fábrica de dados Olá com acesso restrito/limite de tempo específicos/tooall recursos (blob/contêiner) no armazenamento de saudação.</span><span class="sxs-lookup"><span data-stu-id="ed017-1025">It provides hello data factory with restricted/time-bound access tooall/specific resources (blob/container) in hello storage.</span></span> <span data-ttu-id="ed017-1026">toolink sua fábrica de dados de tooa da conta de armazenamento do Azure usando a assinatura de acesso compartilhado, crie um serviço de SAS do armazenamento do Azure vinculado.</span><span class="sxs-lookup"><span data-stu-id="ed017-1026">toolink your Azure storage account tooa data factory by using Shared Access Signature, create an Azure Storage SAS linked service.</span></span> <span data-ttu-id="ed017-1027">toodefine um SAS de armazenamento do Azure vinculada serviço, Olá conjunto **tipo** de saudação serviço vinculado muito**o AzureStorageSas**.</span><span class="sxs-lookup"><span data-stu-id="ed017-1027">toodefine an Azure Storage SAS linked service, set hello **type** of hello linked service too**AzureStorageSas**.</span></span> <span data-ttu-id="ed017-1028">Em seguida, você pode especificar propriedades no Olá a seguir **typeProperties** seção:</span><span class="sxs-lookup"><span data-stu-id="ed017-1028">Then, you can specify following properties in hello **typeProperties** section:</span></span>   

| <span data-ttu-id="ed017-1029">Propriedade</span><span class="sxs-lookup"><span data-stu-id="ed017-1029">Property</span></span> | <span data-ttu-id="ed017-1030">Descrição</span><span class="sxs-lookup"><span data-stu-id="ed017-1030">Description</span></span> | <span data-ttu-id="ed017-1031">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="ed017-1031">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="ed017-1032">type</span><span class="sxs-lookup"><span data-stu-id="ed017-1032">type</span></span> |<span data-ttu-id="ed017-1033">propriedade de tipo Hello deve ser definida como: **o AzureStorageSas**</span><span class="sxs-lookup"><span data-stu-id="ed017-1033">hello type property must be set to: **AzureStorageSas**</span></span> |<span data-ttu-id="ed017-1034">Sim</span><span class="sxs-lookup"><span data-stu-id="ed017-1034">Yes</span></span> |
| <span data-ttu-id="ed017-1035">sasUri</span><span class="sxs-lookup"><span data-stu-id="ed017-1035">sasUri</span></span> |<span data-ttu-id="ed017-1036">Especifica os recursos de armazenamento do Azure do URI de assinatura de acesso compartilhado toohello como blob, contêiner ou tabela.</span><span class="sxs-lookup"><span data-stu-id="ed017-1036">Specify Shared Access Signature URI toohello Azure Storage resources such as blob, container, or table.</span></span> |<span data-ttu-id="ed017-1037">Sim</span><span class="sxs-lookup"><span data-stu-id="ed017-1037">Yes</span></span> |

<span data-ttu-id="ed017-1038">**Exemplo:**</span><span class="sxs-lookup"><span data-stu-id="ed017-1038">**Example:**</span></span>

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

<span data-ttu-id="ed017-1039">Para obter mais informações sobre esses serviços vinculados, consulte o artigo [Conector de Armazenamento de Tabelas do Azure](data-factory-azure-table-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="ed017-1039">For more information about these linked services, see [Azure Table Storage connector](data-factory-azure-table-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="ed017-1040">Conjunto de dados</span><span class="sxs-lookup"><span data-stu-id="ed017-1040">Dataset</span></span>
<span data-ttu-id="ed017-1041">toodefine um conjunto de dados de tabela do Azure, Olá conjunto **tipo** do conjunto de dados de saudação muito**AzureTable**e especifique Olá seguintes propriedades em Olá **typeProperties** seção:</span><span class="sxs-lookup"><span data-stu-id="ed017-1041">toodefine an Azure Table dataset, set hello **type** of hello dataset too**AzureTable**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="ed017-1042">Propriedade</span><span class="sxs-lookup"><span data-stu-id="ed017-1042">Property</span></span> | <span data-ttu-id="ed017-1043">Descrição</span><span class="sxs-lookup"><span data-stu-id="ed017-1043">Description</span></span> | <span data-ttu-id="ed017-1044">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="ed017-1044">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ed017-1045">tableName</span><span class="sxs-lookup"><span data-stu-id="ed017-1045">tableName</span></span> |<span data-ttu-id="ed017-1046">Nome da tabela de saudação na instância de banco de dados de tabela do Azure Olá que serviço vinculado refere-se a.</span><span class="sxs-lookup"><span data-stu-id="ed017-1046">Name of hello table in hello Azure Table Database instance that linked service refers to.</span></span> |<span data-ttu-id="ed017-1047">Sim.</span><span class="sxs-lookup"><span data-stu-id="ed017-1047">Yes.</span></span> <span data-ttu-id="ed017-1048">Quando um nome de tabela é especificado sem um azureTableSourceQuery, todos os registros da tabela de saudação são copiados toohello destino.</span><span class="sxs-lookup"><span data-stu-id="ed017-1048">When a tableName is specified without an azureTableSourceQuery, all records from hello table are copied toohello destination.</span></span> <span data-ttu-id="ed017-1049">Se um azureTableSourceQuery também for especificado, registros da tabela de saudação que atenda a consulta de saudação são copiados toohello destino.</span><span class="sxs-lookup"><span data-stu-id="ed017-1049">If an azureTableSourceQuery is also specified, records from hello table that satisfies hello query are copied toohello destination.</span></span> |

#### <a name="example"></a><span data-ttu-id="ed017-1050">Exemplo</span><span class="sxs-lookup"><span data-stu-id="ed017-1050">Example</span></span>

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

<span data-ttu-id="ed017-1051">Para obter mais informações sobre esses serviços vinculados, consulte o artigo [Conector de Armazenamento de Tabelas do Azure](data-factory-azure-table-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="ed017-1051">For more information about these linked services, see [Azure Table Storage connector](data-factory-azure-table-connector.md#dataset-properties) article.</span></span> 

### <a name="azure-table-source-in-copy-activity"></a><span data-ttu-id="ed017-1052">Origem da Tabela do Azure na Atividade de Cópia</span><span class="sxs-lookup"><span data-stu-id="ed017-1052">Azure Table Source in Copy Activity</span></span>
<span data-ttu-id="ed017-1053">Se você estiver copiando dados de armazenamento de tabela do Azure, defina Olá **tipo de fonte** de hello atividade de cópia muito**AzureTableSource**e especificar propriedades no Olá a seguir **fonte**seção:</span><span class="sxs-lookup"><span data-stu-id="ed017-1053">If you are copying data from Azure Table Storage, set hello **source type** of hello copy activity too**AzureTableSource**, and specify following properties in hello **source** section:</span></span>

| <span data-ttu-id="ed017-1054">Propriedade</span><span class="sxs-lookup"><span data-stu-id="ed017-1054">Property</span></span> | <span data-ttu-id="ed017-1055">Descrição</span><span class="sxs-lookup"><span data-stu-id="ed017-1055">Description</span></span> | <span data-ttu-id="ed017-1056">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="ed017-1056">Allowed values</span></span> | <span data-ttu-id="ed017-1057">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="ed017-1057">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="ed017-1058">AzureTableSourceQuery</span><span class="sxs-lookup"><span data-stu-id="ed017-1058">azureTableSourceQuery</span></span> |<span data-ttu-id="ed017-1059">Use dados de tooread Olá consulta personalizada.</span><span class="sxs-lookup"><span data-stu-id="ed017-1059">Use hello custom query tooread data.</span></span> |<span data-ttu-id="ed017-1060">Cadeia de caracteres de consulta de tabela do Azure.</span><span class="sxs-lookup"><span data-stu-id="ed017-1060">Azure table query string.</span></span> <span data-ttu-id="ed017-1061">Consulte os exemplos na próxima seção, Olá.</span><span class="sxs-lookup"><span data-stu-id="ed017-1061">See examples in hello next section.</span></span> |<span data-ttu-id="ed017-1062">Não.</span><span class="sxs-lookup"><span data-stu-id="ed017-1062">No.</span></span> <span data-ttu-id="ed017-1063">Quando um nome de tabela é especificado sem um azureTableSourceQuery, todos os registros da tabela de saudação são copiados toohello destino.</span><span class="sxs-lookup"><span data-stu-id="ed017-1063">When a tableName is specified without an azureTableSourceQuery, all records from hello table are copied toohello destination.</span></span> <span data-ttu-id="ed017-1064">Se um azureTableSourceQuery também for especificado, registros da tabela de saudação que atenda a consulta de saudação são copiados toohello destino.</span><span class="sxs-lookup"><span data-stu-id="ed017-1064">If an azureTableSourceQuery is also specified, records from hello table that satisfies hello query are copied toohello destination.</span></span> |
| <span data-ttu-id="ed017-1065">azureTableSourceIgnoreTableNotFound</span><span class="sxs-lookup"><span data-stu-id="ed017-1065">azureTableSourceIgnoreTableNotFound</span></span> |<span data-ttu-id="ed017-1066">Indique se a exceção de Olá de assimilação da tabela não existe.</span><span class="sxs-lookup"><span data-stu-id="ed017-1066">Indicate whether swallow hello exception of table not exist.</span></span> |<span data-ttu-id="ed017-1067">TRUE</span><span class="sxs-lookup"><span data-stu-id="ed017-1067">TRUE</span></span><br/><span data-ttu-id="ed017-1068">FALSE</span><span class="sxs-lookup"><span data-stu-id="ed017-1068">FALSE</span></span> |<span data-ttu-id="ed017-1069">Não</span><span class="sxs-lookup"><span data-stu-id="ed017-1069">No</span></span> |

#### <a name="example"></a><span data-ttu-id="ed017-1070">Exemplo</span><span class="sxs-lookup"><span data-stu-id="ed017-1070">Example</span></span>

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

<span data-ttu-id="ed017-1071">Para obter mais informações sobre esses serviços vinculados, consulte o artigo [Conector de Armazenamento de Tabelas do Azure](data-factory-azure-table-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="ed017-1071">For more information about these linked services, see [Azure Table Storage connector](data-factory-azure-table-connector.md#copy-activity-properties) article.</span></span> 

### <a name="azure-table-sink-in-copy-activity"></a><span data-ttu-id="ed017-1072">Coletor da Tabela do Azure na Atividade de Cópia</span><span class="sxs-lookup"><span data-stu-id="ed017-1072">Azure Table Sink in Copy Activity</span></span>
<span data-ttu-id="ed017-1073">Se você estiver copiando dados tooAzure armazenamento de tabela, definir Olá **tipo de coletor** de hello atividade de cópia muito**AzureTableSink**e especificar propriedades no Olá a seguir **coletor** seção:</span><span class="sxs-lookup"><span data-stu-id="ed017-1073">If you are copying data tooAzure Table Storage, set hello **sink type** of hello copy activity too**AzureTableSink**, and specify following properties in hello **sink** section:</span></span>

| <span data-ttu-id="ed017-1074">Propriedade</span><span class="sxs-lookup"><span data-stu-id="ed017-1074">Property</span></span> | <span data-ttu-id="ed017-1075">Descrição</span><span class="sxs-lookup"><span data-stu-id="ed017-1075">Description</span></span> | <span data-ttu-id="ed017-1076">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="ed017-1076">Allowed values</span></span> | <span data-ttu-id="ed017-1077">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="ed017-1077">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="ed017-1078">azureTableDefaultPartitionKeyValue</span><span class="sxs-lookup"><span data-stu-id="ed017-1078">azureTableDefaultPartitionKeyValue</span></span> |<span data-ttu-id="ed017-1079">Partição chave valor padrão que pode ser usado pelo coletor de saudação.</span><span class="sxs-lookup"><span data-stu-id="ed017-1079">Default partition key value that can be used by hello sink.</span></span> |<span data-ttu-id="ed017-1080">Um valor de cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="ed017-1080">A string value.</span></span> |<span data-ttu-id="ed017-1081">Não</span><span class="sxs-lookup"><span data-stu-id="ed017-1081">No</span></span> |
| <span data-ttu-id="ed017-1082">azureTablePartitionKeyName</span><span class="sxs-lookup"><span data-stu-id="ed017-1082">azureTablePartitionKeyName</span></span> |<span data-ttu-id="ed017-1083">Especifique o nome da coluna Olá cujos valores são usados como chaves de partição.</span><span class="sxs-lookup"><span data-stu-id="ed017-1083">Specify name of hello column whose values are used as partition keys.</span></span> <span data-ttu-id="ed017-1084">Se não especificado, AzureTableDefaultPartitionKeyValue será usado como chave de partição hello.</span><span class="sxs-lookup"><span data-stu-id="ed017-1084">If not specified, AzureTableDefaultPartitionKeyValue is used as hello partition key.</span></span> |<span data-ttu-id="ed017-1085">Um nome de coluna.</span><span class="sxs-lookup"><span data-stu-id="ed017-1085">A column name.</span></span> |<span data-ttu-id="ed017-1086">Não</span><span class="sxs-lookup"><span data-stu-id="ed017-1086">No</span></span> |
| <span data-ttu-id="ed017-1087">azureTableRowKeyName</span><span class="sxs-lookup"><span data-stu-id="ed017-1087">azureTableRowKeyName</span></span> |<span data-ttu-id="ed017-1088">Especifique o nome da coluna Olá cujos valores de coluna são usados como chave de linha.</span><span class="sxs-lookup"><span data-stu-id="ed017-1088">Specify name of hello column whose column values are used as row key.</span></span> <span data-ttu-id="ed017-1089">Se não especificado, um GUID é usado para cada linha.</span><span class="sxs-lookup"><span data-stu-id="ed017-1089">If not specified, use a GUID for each row.</span></span> |<span data-ttu-id="ed017-1090">Um nome de coluna.</span><span class="sxs-lookup"><span data-stu-id="ed017-1090">A column name.</span></span> |<span data-ttu-id="ed017-1091">Não</span><span class="sxs-lookup"><span data-stu-id="ed017-1091">No</span></span> |
| <span data-ttu-id="ed017-1092">azureTableInsertType</span><span class="sxs-lookup"><span data-stu-id="ed017-1092">azureTableInsertType</span></span> |<span data-ttu-id="ed017-1093">dados de tooinsert de modo de saudação na tabela do Azure.</span><span class="sxs-lookup"><span data-stu-id="ed017-1093">hello mode tooinsert data into Azure table.</span></span><br/><br/><span data-ttu-id="ed017-1094">Essa propriedade controla se as linhas existentes na tabela de saída de hello com correspondência de chaves de partição e de linha têm seus valores substituídos ou mesclados.</span><span class="sxs-lookup"><span data-stu-id="ed017-1094">This property controls whether existing rows in hello output table with matching partition and row keys have their values replaced or merged.</span></span> <br/><br/><span data-ttu-id="ed017-1095">toolearn sobre como essas configurações (mesclagem e substituir) funcionam, consulte [inserir ou mesclar entidade](https://msdn.microsoft.com/library/azure/hh452241.aspx) e [inserir ou substituir entidade](https://msdn.microsoft.com/library/azure/hh452242.aspx) tópicos.</span><span class="sxs-lookup"><span data-stu-id="ed017-1095">toolearn about how these settings (merge and replace) work, see [Insert or Merge Entity](https://msdn.microsoft.com/library/azure/hh452241.aspx) and [Insert or Replace Entity](https://msdn.microsoft.com/library/azure/hh452242.aspx) topics.</span></span> <br/><br> <span data-ttu-id="ed017-1096">Essa configuração se aplica no nível de linha hello, não os nível de tabela Olá, e nenhuma opção exclui linhas na tabela de saída de saudação que não existem na entrada hello.</span><span class="sxs-lookup"><span data-stu-id="ed017-1096">This setting applies at hello row level, not hello table level, and neither option deletes rows in hello output table that do not exist in hello input.</span></span> |<span data-ttu-id="ed017-1097">mesclar (padrão)</span><span class="sxs-lookup"><span data-stu-id="ed017-1097">merge (default)</span></span><br/><span data-ttu-id="ed017-1098">substituir</span><span class="sxs-lookup"><span data-stu-id="ed017-1098">replace</span></span> |<span data-ttu-id="ed017-1099">Não</span><span class="sxs-lookup"><span data-stu-id="ed017-1099">No</span></span> |
| <span data-ttu-id="ed017-1100">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="ed017-1100">writeBatchSize</span></span> |<span data-ttu-id="ed017-1101">Insere dados em Olá tabela do Azure quando Olá writeBatchSize ou writeBatchTimeout é atingido.</span><span class="sxs-lookup"><span data-stu-id="ed017-1101">Inserts data into hello Azure table when hello writeBatchSize or writeBatchTimeout is hit.</span></span> |<span data-ttu-id="ed017-1102">Inteiro (número de linhas)</span><span class="sxs-lookup"><span data-stu-id="ed017-1102">Integer (number of rows)</span></span> |<span data-ttu-id="ed017-1103">Não (padrão: 10000)</span><span class="sxs-lookup"><span data-stu-id="ed017-1103">No (default: 10000)</span></span> |
| <span data-ttu-id="ed017-1104">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="ed017-1104">writeBatchTimeout</span></span> |<span data-ttu-id="ed017-1105">Insere dados na Olá tabela do Azure quando Olá writeBatchSize ou writeBatchTimeout é atingido</span><span class="sxs-lookup"><span data-stu-id="ed017-1105">Inserts data into hello Azure table when hello writeBatchSize or writeBatchTimeout is hit</span></span> |<span data-ttu-id="ed017-1106">timespan</span><span class="sxs-lookup"><span data-stu-id="ed017-1106">timespan</span></span><br/><br/><span data-ttu-id="ed017-1107">Exemplo: "00:20:00" (20 minutos)</span><span class="sxs-lookup"><span data-stu-id="ed017-1107">Example: “00:20:00” (20 minutes)</span></span> |<span data-ttu-id="ed017-1108">Não (valor de tempo limite padrão de cliente de toostorage padrão 90 segundos)</span><span class="sxs-lookup"><span data-stu-id="ed017-1108">No (Default toostorage client default timeout value 90 sec)</span></span> |

#### <a name="example"></a><span data-ttu-id="ed017-1109">Exemplo</span><span class="sxs-lookup"><span data-stu-id="ed017-1109">Example</span></span>

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
<span data-ttu-id="ed017-1110">Para obter mais informações sobre esses serviços vinculados, consulte o artigo [Conector de Armazenamento de Tabelas do Azure](data-factory-azure-table-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="ed017-1110">For more information about these linked services, see [Azure Table Storage connector](data-factory-azure-table-connector.md#copy-activity-properties) article.</span></span> 

## <a name="amazon-redshift"></a><span data-ttu-id="ed017-1111">Amazon RedShift</span><span class="sxs-lookup"><span data-stu-id="ed017-1111">Amazon RedShift</span></span>

### <a name="linked-service"></a><span data-ttu-id="ed017-1112">Serviço vinculado</span><span class="sxs-lookup"><span data-stu-id="ed017-1112">Linked service</span></span>
<span data-ttu-id="ed017-1113">toodefine um Amazon Redshift o serviço saudação do conjunto vinculado **tipo** de saudação serviço vinculado muito**AmazonRedshift**e especificar propriedades no Olá a seguir **typeProperties**seção:</span><span class="sxs-lookup"><span data-stu-id="ed017-1113">toodefine an Amazon Redshift linked service, set hello **type** of hello linked service too**AmazonRedshift**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="ed017-1114">Propriedade</span><span class="sxs-lookup"><span data-stu-id="ed017-1114">Property</span></span> | <span data-ttu-id="ed017-1115">Descrição</span><span class="sxs-lookup"><span data-stu-id="ed017-1115">Description</span></span> | <span data-ttu-id="ed017-1116">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="ed017-1116">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ed017-1117">server</span><span class="sxs-lookup"><span data-stu-id="ed017-1117">server</span></span> |<span data-ttu-id="ed017-1118">IP endereço ou nome de host do servidor do Amazon Redshift hello.</span><span class="sxs-lookup"><span data-stu-id="ed017-1118">IP address or host name of hello Amazon Redshift server.</span></span> |<span data-ttu-id="ed017-1119">Sim</span><span class="sxs-lookup"><span data-stu-id="ed017-1119">Yes</span></span> |
| <span data-ttu-id="ed017-1120">porta</span><span class="sxs-lookup"><span data-stu-id="ed017-1120">port</span></span> |<span data-ttu-id="ed017-1121">número de saudação de porta TCP Olá Olá Amazon Redshift server usa toolisten para conexões de cliente.</span><span class="sxs-lookup"><span data-stu-id="ed017-1121">hello number of hello TCP port that hello Amazon Redshift server uses toolisten for client connections.</span></span> |<span data-ttu-id="ed017-1122">Não, valor padrão: 5439</span><span class="sxs-lookup"><span data-stu-id="ed017-1122">No, default value: 5439</span></span> |
| <span data-ttu-id="ed017-1123">database</span><span class="sxs-lookup"><span data-stu-id="ed017-1123">database</span></span> |<span data-ttu-id="ed017-1124">Nome do banco de dados do Amazon Redshift hello.</span><span class="sxs-lookup"><span data-stu-id="ed017-1124">Name of hello Amazon Redshift database.</span></span> |<span data-ttu-id="ed017-1125">Sim</span><span class="sxs-lookup"><span data-stu-id="ed017-1125">Yes</span></span> |
| <span data-ttu-id="ed017-1126">Nome de Usuário</span><span class="sxs-lookup"><span data-stu-id="ed017-1126">username</span></span> |<span data-ttu-id="ed017-1127">Nome de usuário que tem o banco de dados do access toohello.</span><span class="sxs-lookup"><span data-stu-id="ed017-1127">Name of user who has access toohello database.</span></span> |<span data-ttu-id="ed017-1128">Sim</span><span class="sxs-lookup"><span data-stu-id="ed017-1128">Yes</span></span> |
| <span data-ttu-id="ed017-1129">Senha</span><span class="sxs-lookup"><span data-stu-id="ed017-1129">password</span></span> |<span data-ttu-id="ed017-1130">Senha da conta de usuário de saudação.</span><span class="sxs-lookup"><span data-stu-id="ed017-1130">Password for hello user account.</span></span> |<span data-ttu-id="ed017-1131">Sim</span><span class="sxs-lookup"><span data-stu-id="ed017-1131">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="ed017-1132">Exemplo</span><span class="sxs-lookup"><span data-stu-id="ed017-1132">Example</span></span>

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

<span data-ttu-id="ed017-1133">Para obter mais informações, consulte o artigo [Conector do Amazon Redshift](#data-factory-amazon-redshift-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="ed017-1133">For more information, see [Amazon Redshift connector](#data-factory-amazon-redshift-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="ed017-1134">Conjunto de dados</span><span class="sxs-lookup"><span data-stu-id="ed017-1134">Dataset</span></span>
<span data-ttu-id="ed017-1135">toodefine um conjunto de dados do Amazon Redshift conjunto Olá **tipo** do conjunto de dados de saudação muito**RelationalTable**e especifique Olá seguintes propriedades em Olá **typeProperties** seção:</span><span class="sxs-lookup"><span data-stu-id="ed017-1135">toodefine an Amazon Redshift dataset, set hello **type** of hello dataset too**RelationalTable**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="ed017-1136">Propriedade</span><span class="sxs-lookup"><span data-stu-id="ed017-1136">Property</span></span> | <span data-ttu-id="ed017-1137">Descrição</span><span class="sxs-lookup"><span data-stu-id="ed017-1137">Description</span></span> | <span data-ttu-id="ed017-1138">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="ed017-1138">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ed017-1139">tableName</span><span class="sxs-lookup"><span data-stu-id="ed017-1139">tableName</span></span> |<span data-ttu-id="ed017-1140">Nome de tabela Olá Olá Amazon Redshift banco de dados do qual o serviço vinculado se refere.</span><span class="sxs-lookup"><span data-stu-id="ed017-1140">Name of hello table in hello Amazon Redshift database that linked service refers to.</span></span> |<span data-ttu-id="ed017-1141">Não (se **query** de **RelationalSource** for especificado)</span><span class="sxs-lookup"><span data-stu-id="ed017-1141">No (if **query** of **RelationalSource** is specified)</span></span> |


#### <a name="example"></a><span data-ttu-id="ed017-1142">Exemplo</span><span class="sxs-lookup"><span data-stu-id="ed017-1142">Example</span></span>

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
<span data-ttu-id="ed017-1143">Para obter mais informações, consulte o artigo [Conector do Amazon Redshift](#data-factory-amazon-redshift-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="ed017-1143">For more information, see [Amazon Redshift connector](#data-factory-amazon-redshift-connector.md#dataset-properties) article.</span></span>

### <a name="relational-source-in-copy-activity"></a><span data-ttu-id="ed017-1144">Origem Relacional na Atividade de Cópia</span><span class="sxs-lookup"><span data-stu-id="ed017-1144">Relational Source in Copy Activity</span></span> 
<span data-ttu-id="ed017-1145">Se você estiver copiando dados do Amazon Redshift, defina Olá **tipo de fonte** de hello atividade de cópia muito**RelationalSource**e especificar propriedades no Olá a seguir **fonte** seção:</span><span class="sxs-lookup"><span data-stu-id="ed017-1145">If you are copying data from Amazon Redshift, set hello **source type** of hello copy activity too**RelationalSource**, and specify following properties in hello **source** section:</span></span>

| <span data-ttu-id="ed017-1146">Propriedade</span><span class="sxs-lookup"><span data-stu-id="ed017-1146">Property</span></span> | <span data-ttu-id="ed017-1147">Descrição</span><span class="sxs-lookup"><span data-stu-id="ed017-1147">Description</span></span> | <span data-ttu-id="ed017-1148">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="ed017-1148">Allowed values</span></span> | <span data-ttu-id="ed017-1149">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="ed017-1149">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="ed017-1150">query</span><span class="sxs-lookup"><span data-stu-id="ed017-1150">query</span></span> |<span data-ttu-id="ed017-1151">Use dados de tooread Olá consulta personalizada.</span><span class="sxs-lookup"><span data-stu-id="ed017-1151">Use hello custom query tooread data.</span></span> |<span data-ttu-id="ed017-1152">Cadeia de caracteres de consulta SQL.</span><span class="sxs-lookup"><span data-stu-id="ed017-1152">SQL query string.</span></span> <span data-ttu-id="ed017-1153">Por exemplo: `select * from MyTable`.</span><span class="sxs-lookup"><span data-stu-id="ed017-1153">For example: `select * from MyTable`.</span></span> |<span data-ttu-id="ed017-1154">Não (se **tableName** de **dataset** for especificado)</span><span class="sxs-lookup"><span data-stu-id="ed017-1154">No (if **tableName** of **dataset** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="ed017-1155">Exemplo</span><span class="sxs-lookup"><span data-stu-id="ed017-1155">Example</span></span>

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
<span data-ttu-id="ed017-1156">Para obter mais informações, consulte o artigo [Conector do Amazon Redshift](#data-factory-amazon-redshift-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="ed017-1156">For more information, see [Amazon Redshift connector](#data-factory-amazon-redshift-connector.md#copy-activity-properties) article.</span></span>

## <a name="ibm-db2"></a><span data-ttu-id="ed017-1157">IBM DB2</span><span class="sxs-lookup"><span data-stu-id="ed017-1157">IBM DB2</span></span>

### <a name="linked-service"></a><span data-ttu-id="ed017-1158">Serviço vinculado</span><span class="sxs-lookup"><span data-stu-id="ed017-1158">Linked service</span></span>
<span data-ttu-id="ed017-1159">toodefine um IBM DB2 vinculada serviço, Olá conjunto **tipo** de saudação serviço vinculado muito**OnPremisesDB2**e especificar propriedades no Olá a seguir **typeProperties** seção:</span><span class="sxs-lookup"><span data-stu-id="ed017-1159">toodefine an IBM DB2 linked service, set hello **type** of hello linked service too**OnPremisesDB2**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="ed017-1160">Propriedade</span><span class="sxs-lookup"><span data-stu-id="ed017-1160">Property</span></span> | <span data-ttu-id="ed017-1161">Descrição</span><span class="sxs-lookup"><span data-stu-id="ed017-1161">Description</span></span> | <span data-ttu-id="ed017-1162">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="ed017-1162">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ed017-1163">server</span><span class="sxs-lookup"><span data-stu-id="ed017-1163">server</span></span> |<span data-ttu-id="ed017-1164">Nome do servidor de saudação DB2.</span><span class="sxs-lookup"><span data-stu-id="ed017-1164">Name of hello DB2 server.</span></span> |<span data-ttu-id="ed017-1165">Sim</span><span class="sxs-lookup"><span data-stu-id="ed017-1165">Yes</span></span> |
| <span data-ttu-id="ed017-1166">database</span><span class="sxs-lookup"><span data-stu-id="ed017-1166">database</span></span> |<span data-ttu-id="ed017-1167">Nome do banco de dados de saudação DB2.</span><span class="sxs-lookup"><span data-stu-id="ed017-1167">Name of hello DB2 database.</span></span> |<span data-ttu-id="ed017-1168">Sim</span><span class="sxs-lookup"><span data-stu-id="ed017-1168">Yes</span></span> |
| <span data-ttu-id="ed017-1169">schema</span><span class="sxs-lookup"><span data-stu-id="ed017-1169">schema</span></span> |<span data-ttu-id="ed017-1170">Nome do esquema de saudação no banco de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="ed017-1170">Name of hello schema in hello database.</span></span> <span data-ttu-id="ed017-1171">nome do esquema Olá diferencia maiusculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="ed017-1171">hello schema name is case-sensitive.</span></span> |<span data-ttu-id="ed017-1172">Não</span><span class="sxs-lookup"><span data-stu-id="ed017-1172">No</span></span> |
| <span data-ttu-id="ed017-1173">authenticationType</span><span class="sxs-lookup"><span data-stu-id="ed017-1173">authenticationType</span></span> |<span data-ttu-id="ed017-1174">Tipo de autenticação usado o banco de dados do DB2 tooconnect toohello.</span><span class="sxs-lookup"><span data-stu-id="ed017-1174">Type of authentication used tooconnect toohello DB2 database.</span></span> <span data-ttu-id="ed017-1175">Os valores possíveis são: Anonymous, Basic e Windows.</span><span class="sxs-lookup"><span data-stu-id="ed017-1175">Possible values are: Anonymous, Basic, and Windows.</span></span> |<span data-ttu-id="ed017-1176">Sim</span><span class="sxs-lookup"><span data-stu-id="ed017-1176">Yes</span></span> |
| <span data-ttu-id="ed017-1177">Nome de Usuário</span><span class="sxs-lookup"><span data-stu-id="ed017-1177">username</span></span> |<span data-ttu-id="ed017-1178">Especifique o nome de usuário se você estiver usando a autenticação Basic ou Windows.</span><span class="sxs-lookup"><span data-stu-id="ed017-1178">Specify user name if you are using Basic or Windows authentication.</span></span> |<span data-ttu-id="ed017-1179">Não</span><span class="sxs-lookup"><span data-stu-id="ed017-1179">No</span></span> |
| <span data-ttu-id="ed017-1180">Senha</span><span class="sxs-lookup"><span data-stu-id="ed017-1180">password</span></span> |<span data-ttu-id="ed017-1181">Especifique a senha da conta de usuário de saudação especificado para nome de usuário de saudação.</span><span class="sxs-lookup"><span data-stu-id="ed017-1181">Specify password for hello user account you specified for hello username.</span></span> |<span data-ttu-id="ed017-1182">Não</span><span class="sxs-lookup"><span data-stu-id="ed017-1182">No</span></span> |
| <span data-ttu-id="ed017-1183">gatewayName</span><span class="sxs-lookup"><span data-stu-id="ed017-1183">gatewayName</span></span> |<span data-ttu-id="ed017-1184">Nome do gateway Olá Olá serviço da fábrica de dados deve usar o banco de dados do tooconnect toohello local DB2.</span><span class="sxs-lookup"><span data-stu-id="ed017-1184">Name of hello gateway that hello Data Factory service should use tooconnect toohello on-premises DB2 database.</span></span> |<span data-ttu-id="ed017-1185">Sim</span><span class="sxs-lookup"><span data-stu-id="ed017-1185">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="ed017-1186">Exemplo</span><span class="sxs-lookup"><span data-stu-id="ed017-1186">Example</span></span>
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
<span data-ttu-id="ed017-1187">Para obter mais informações, consulte o artigo [Conector do IBM DB2](#data-factory-onprem-db2-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="ed017-1187">For more information, see [IBM DB2 connector](#data-factory-onprem-db2-connector.md#linked-service-properties) article.</span></span>

### <a name="dataset"></a><span data-ttu-id="ed017-1188">Conjunto de dados</span><span class="sxs-lookup"><span data-stu-id="ed017-1188">Dataset</span></span>
<span data-ttu-id="ed017-1189">conjunto de dados toodefine um DB2, Olá conjunto **tipo** do conjunto de dados de saudação muito**RelationalTable**e especifique Olá Olá propriedades a seguir **typeProperties** seção:</span><span class="sxs-lookup"><span data-stu-id="ed017-1189">toodefine a DB2 dataset, set hello **type** of hello dataset too**RelationalTable**, and specify hello following properties in hello **typeProperties** section:</span></span>

| <span data-ttu-id="ed017-1190">Propriedade</span><span class="sxs-lookup"><span data-stu-id="ed017-1190">Property</span></span> | <span data-ttu-id="ed017-1191">Descrição</span><span class="sxs-lookup"><span data-stu-id="ed017-1191">Description</span></span> | <span data-ttu-id="ed017-1192">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="ed017-1192">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ed017-1193">tableName</span><span class="sxs-lookup"><span data-stu-id="ed017-1193">tableName</span></span> |<span data-ttu-id="ed017-1194">Nome da tabela de saudação na instância de banco de dados DB2 Olá que serviço vinculado refere-se a.</span><span class="sxs-lookup"><span data-stu-id="ed017-1194">Name of hello table in hello DB2 Database instance that linked service refers to.</span></span> <span data-ttu-id="ed017-1195">Olá tableName diferencia maiusculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="ed017-1195">hello tableName is case-sensitive.</span></span> |<span data-ttu-id="ed017-1196">Não (se **query** de **RelationalSource** for especificado)</span><span class="sxs-lookup"><span data-stu-id="ed017-1196">No (if **query** of **RelationalSource** is specified)</span></span> 

#### <a name="example"></a><span data-ttu-id="ed017-1197">Exemplo</span><span class="sxs-lookup"><span data-stu-id="ed017-1197">Example</span></span>
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

<span data-ttu-id="ed017-1198">Para obter mais informações, consulte o artigo [Conector do IBM DB2](#data-factory-onprem-db2-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="ed017-1198">For more information, see [IBM DB2 connector](#data-factory-onprem-db2-connector.md#dataset-properties) article.</span></span>

### <a name="relational-source-in-copy-activity"></a><span data-ttu-id="ed017-1199">Origem Relacional na Atividade de Cópia</span><span class="sxs-lookup"><span data-stu-id="ed017-1199">Relational Source in Copy Activity</span></span>
<span data-ttu-id="ed017-1200">Se você estiver copiando dados do IBM DB2, defina Olá **tipo de fonte** de hello atividade de cópia muito**RelationalSource**e especificar propriedades no Olá a seguir **fonte** seção:</span><span class="sxs-lookup"><span data-stu-id="ed017-1200">If you are copying data from IBM DB2, set hello **source type** of hello copy activity too**RelationalSource**, and specify following properties in hello **source** section:</span></span>


| <span data-ttu-id="ed017-1201">Propriedade</span><span class="sxs-lookup"><span data-stu-id="ed017-1201">Property</span></span> | <span data-ttu-id="ed017-1202">Descrição</span><span class="sxs-lookup"><span data-stu-id="ed017-1202">Description</span></span> | <span data-ttu-id="ed017-1203">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="ed017-1203">Allowed values</span></span> | <span data-ttu-id="ed017-1204">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="ed017-1204">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="ed017-1205">query</span><span class="sxs-lookup"><span data-stu-id="ed017-1205">query</span></span> |<span data-ttu-id="ed017-1206">Use dados de tooread Olá consulta personalizada.</span><span class="sxs-lookup"><span data-stu-id="ed017-1206">Use hello custom query tooread data.</span></span> |<span data-ttu-id="ed017-1207">Cadeia de caracteres de consulta SQL.</span><span class="sxs-lookup"><span data-stu-id="ed017-1207">SQL query string.</span></span> <span data-ttu-id="ed017-1208">Por exemplo: `"query": "select * from "MySchema"."MyTable""`.</span><span class="sxs-lookup"><span data-stu-id="ed017-1208">For example: `"query": "select * from "MySchema"."MyTable""`.</span></span> |<span data-ttu-id="ed017-1209">Não (se **tableName** de **dataset** for especificado)</span><span class="sxs-lookup"><span data-stu-id="ed017-1209">No (if **tableName** of **dataset** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="ed017-1210">Exemplo</span><span class="sxs-lookup"><span data-stu-id="ed017-1210">Example</span></span>
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
<span data-ttu-id="ed017-1211">Para obter mais informações, consulte o artigo [Conector do IBM DB2](#data-factory-onprem-db2-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="ed017-1211">For more information, see [IBM DB2 connector](#data-factory-onprem-db2-connector.md#copy-activity-properties) article.</span></span>

## <a name="mysql"></a><span data-ttu-id="ed017-1212">MySQL</span><span class="sxs-lookup"><span data-stu-id="ed017-1212">MySQL</span></span>

### <a name="linked-service"></a><span data-ttu-id="ed017-1213">Serviço vinculado</span><span class="sxs-lookup"><span data-stu-id="ed017-1213">Linked service</span></span>
<span data-ttu-id="ed017-1214">toodefine um MySQL vinculados serviço, Olá conjunto **tipo** de saudação serviço vinculado muito**OnPremisesMySql**e especificar propriedades no Olá a seguir **typeProperties** seção:</span><span class="sxs-lookup"><span data-stu-id="ed017-1214">toodefine a MySQL linked service, set hello **type** of hello linked service too**OnPremisesMySql**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="ed017-1215">Propriedade</span><span class="sxs-lookup"><span data-stu-id="ed017-1215">Property</span></span> | <span data-ttu-id="ed017-1216">Descrição</span><span class="sxs-lookup"><span data-stu-id="ed017-1216">Description</span></span> | <span data-ttu-id="ed017-1217">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="ed017-1217">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ed017-1218">server</span><span class="sxs-lookup"><span data-stu-id="ed017-1218">server</span></span> |<span data-ttu-id="ed017-1219">Nome do servidor MySQL de saudação.</span><span class="sxs-lookup"><span data-stu-id="ed017-1219">Name of hello MySQL server.</span></span> |<span data-ttu-id="ed017-1220">Sim</span><span class="sxs-lookup"><span data-stu-id="ed017-1220">Yes</span></span> |
| <span data-ttu-id="ed017-1221">database</span><span class="sxs-lookup"><span data-stu-id="ed017-1221">database</span></span> |<span data-ttu-id="ed017-1222">Nome do banco de dados do hello MySQL.</span><span class="sxs-lookup"><span data-stu-id="ed017-1222">Name of hello MySQL database.</span></span> |<span data-ttu-id="ed017-1223">Sim</span><span class="sxs-lookup"><span data-stu-id="ed017-1223">Yes</span></span> |
| <span data-ttu-id="ed017-1224">schema</span><span class="sxs-lookup"><span data-stu-id="ed017-1224">schema</span></span> |<span data-ttu-id="ed017-1225">Nome do esquema de saudação no banco de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="ed017-1225">Name of hello schema in hello database.</span></span> |<span data-ttu-id="ed017-1226">Não</span><span class="sxs-lookup"><span data-stu-id="ed017-1226">No</span></span> |
| <span data-ttu-id="ed017-1227">authenticationType</span><span class="sxs-lookup"><span data-stu-id="ed017-1227">authenticationType</span></span> |<span data-ttu-id="ed017-1228">Tipo de autenticação usado o banco de dados do tooconnect toohello MySQL.</span><span class="sxs-lookup"><span data-stu-id="ed017-1228">Type of authentication used tooconnect toohello MySQL database.</span></span> <span data-ttu-id="ed017-1229">Os valores possíveis são: `Basic`.</span><span class="sxs-lookup"><span data-stu-id="ed017-1229">Possible values are: `Basic`.</span></span> |<span data-ttu-id="ed017-1230">Sim</span><span class="sxs-lookup"><span data-stu-id="ed017-1230">Yes</span></span> |
| <span data-ttu-id="ed017-1231">Nome de Usuário</span><span class="sxs-lookup"><span data-stu-id="ed017-1231">username</span></span> |<span data-ttu-id="ed017-1232">Especifique o banco de dados do usuário nome tooconnect toohello MySQL.</span><span class="sxs-lookup"><span data-stu-id="ed017-1232">Specify user name tooconnect toohello MySQL database.</span></span> |<span data-ttu-id="ed017-1233">Sim</span><span class="sxs-lookup"><span data-stu-id="ed017-1233">Yes</span></span> |
| <span data-ttu-id="ed017-1234">Senha</span><span class="sxs-lookup"><span data-stu-id="ed017-1234">password</span></span> |<span data-ttu-id="ed017-1235">Especifique a senha da conta de usuário de saudação especificado.</span><span class="sxs-lookup"><span data-stu-id="ed017-1235">Specify password for hello user account you specified.</span></span> |<span data-ttu-id="ed017-1236">Sim</span><span class="sxs-lookup"><span data-stu-id="ed017-1236">Yes</span></span> |
| <span data-ttu-id="ed017-1237">gatewayName</span><span class="sxs-lookup"><span data-stu-id="ed017-1237">gatewayName</span></span> |<span data-ttu-id="ed017-1238">Nome do gateway Olá Olá serviço da fábrica de dados deve usar o banco de dados do tooconnect toohello local MySQL.</span><span class="sxs-lookup"><span data-stu-id="ed017-1238">Name of hello gateway that hello Data Factory service should use tooconnect toohello on-premises MySQL database.</span></span> |<span data-ttu-id="ed017-1239">Sim</span><span class="sxs-lookup"><span data-stu-id="ed017-1239">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="ed017-1240">Exemplo</span><span class="sxs-lookup"><span data-stu-id="ed017-1240">Example</span></span>

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

<span data-ttu-id="ed017-1241">Para obter mais informações, consulte o artigo [Conector do MySQL](data-factory-onprem-mysql-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="ed017-1241">For more information, see [MySQL connector](data-factory-onprem-mysql-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="ed017-1242">Conjunto de dados</span><span class="sxs-lookup"><span data-stu-id="ed017-1242">Dataset</span></span>
<span data-ttu-id="ed017-1243">toodefine um conjunto de dados MySQL, Olá conjunto **tipo** do conjunto de dados de saudação muito**RelationalTable**e especifique Olá seguintes propriedades em Olá **typeProperties** seção:</span><span class="sxs-lookup"><span data-stu-id="ed017-1243">toodefine a MySQL dataset, set hello **type** of hello dataset too**RelationalTable**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="ed017-1244">Propriedade</span><span class="sxs-lookup"><span data-stu-id="ed017-1244">Property</span></span> | <span data-ttu-id="ed017-1245">Descrição</span><span class="sxs-lookup"><span data-stu-id="ed017-1245">Description</span></span> | <span data-ttu-id="ed017-1246">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="ed017-1246">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ed017-1247">tableName</span><span class="sxs-lookup"><span data-stu-id="ed017-1247">tableName</span></span> |<span data-ttu-id="ed017-1248">Nome da tabela de saudação em Olá instância de banco de dados MySQL serviço vinculado refere-se a.</span><span class="sxs-lookup"><span data-stu-id="ed017-1248">Name of hello table in hello MySQL Database instance that linked service refers to.</span></span> |<span data-ttu-id="ed017-1249">Não (se **query** de **RelationalSource** for especificado)</span><span class="sxs-lookup"><span data-stu-id="ed017-1249">No (if **query** of **RelationalSource** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="ed017-1250">Exemplo</span><span class="sxs-lookup"><span data-stu-id="ed017-1250">Example</span></span>

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
<span data-ttu-id="ed017-1251">Para obter mais informações, consulte o artigo [Conector do MySQL](data-factory-onprem-mysql-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="ed017-1251">For more information, see [MySQL connector](data-factory-onprem-mysql-connector.md#dataset-properties) article.</span></span> 

### <a name="relational-source-in-copy-activity"></a><span data-ttu-id="ed017-1252">Origem Relacional na Atividade de Cópia</span><span class="sxs-lookup"><span data-stu-id="ed017-1252">Relational Source in Copy Activity</span></span>
<span data-ttu-id="ed017-1253">Se você estiver copiando dados de um banco de dados MySQL, defina Olá **tipo de fonte** de hello atividade de cópia muito**RelationalSource**e especificar propriedades no Olá a seguir **fonte** seção:</span><span class="sxs-lookup"><span data-stu-id="ed017-1253">If you are copying data from a MySQL database, set hello **source type** of hello copy activity too**RelationalSource**, and specify following properties in hello **source** section:</span></span>


| <span data-ttu-id="ed017-1254">Propriedade</span><span class="sxs-lookup"><span data-stu-id="ed017-1254">Property</span></span> | <span data-ttu-id="ed017-1255">Descrição</span><span class="sxs-lookup"><span data-stu-id="ed017-1255">Description</span></span> | <span data-ttu-id="ed017-1256">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="ed017-1256">Allowed values</span></span> | <span data-ttu-id="ed017-1257">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="ed017-1257">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="ed017-1258">query</span><span class="sxs-lookup"><span data-stu-id="ed017-1258">query</span></span> |<span data-ttu-id="ed017-1259">Use dados de tooread Olá consulta personalizada.</span><span class="sxs-lookup"><span data-stu-id="ed017-1259">Use hello custom query tooread data.</span></span> |<span data-ttu-id="ed017-1260">Cadeia de caracteres de consulta SQL.</span><span class="sxs-lookup"><span data-stu-id="ed017-1260">SQL query string.</span></span> <span data-ttu-id="ed017-1261">Por exemplo: `select * from MyTable`.</span><span class="sxs-lookup"><span data-stu-id="ed017-1261">For example: `select * from MyTable`.</span></span> |<span data-ttu-id="ed017-1262">Não (se **tableName** de **dataset** for especificado)</span><span class="sxs-lookup"><span data-stu-id="ed017-1262">No (if **tableName** of **dataset** is specified)</span></span> |


#### <a name="example"></a><span data-ttu-id="ed017-1263">Exemplo</span><span class="sxs-lookup"><span data-stu-id="ed017-1263">Example</span></span>
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

<span data-ttu-id="ed017-1264">Para obter mais informações, consulte o artigo [Conector do MySQL](data-factory-onprem-mysql-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="ed017-1264">For more information, see [MySQL connector](data-factory-onprem-mysql-connector.md#copy-activity-properties) article.</span></span> 

## <a name="oracle"></a><span data-ttu-id="ed017-1265">Oracle</span><span class="sxs-lookup"><span data-stu-id="ed017-1265">Oracle</span></span> 

### <a name="linked-service"></a><span data-ttu-id="ed017-1266">Serviço vinculado</span><span class="sxs-lookup"><span data-stu-id="ed017-1266">Linked service</span></span>
<span data-ttu-id="ed017-1267">toodefine um Oracle o serviço saudação do conjunto vinculado **tipo** de saudação serviço vinculado muito**OnPremisesOracle**e especificar propriedades no Olá a seguir **typeProperties** seção:</span><span class="sxs-lookup"><span data-stu-id="ed017-1267">toodefine an Oracle linked service, set hello **type** of hello linked service too**OnPremisesOracle**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="ed017-1268">Propriedade</span><span class="sxs-lookup"><span data-stu-id="ed017-1268">Property</span></span> | <span data-ttu-id="ed017-1269">Descrição</span><span class="sxs-lookup"><span data-stu-id="ed017-1269">Description</span></span> | <span data-ttu-id="ed017-1270">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="ed017-1270">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ed017-1271">driverType</span><span class="sxs-lookup"><span data-stu-id="ed017-1271">driverType</span></span> | <span data-ttu-id="ed017-1272">Especifique quais dados do driver toouse toocopy de / tooOracle banco de dados.</span><span class="sxs-lookup"><span data-stu-id="ed017-1272">Specify which driver toouse toocopy data from/tooOracle Database.</span></span> <span data-ttu-id="ed017-1273">Valores permitidos são **Microsoft** ou **ODP** (padrão).</span><span class="sxs-lookup"><span data-stu-id="ed017-1273">Allowed values are **Microsoft** or **ODP** (default).</span></span> <span data-ttu-id="ed017-1274">Consulte [suporte para instalação e da versão](#supported-versions-and-installation) seção detalhes do driver.</span><span class="sxs-lookup"><span data-stu-id="ed017-1274">See [Supported version and installation](#supported-versions-and-installation) section on driver details.</span></span> | <span data-ttu-id="ed017-1275">Não</span><span class="sxs-lookup"><span data-stu-id="ed017-1275">No</span></span> |
| <span data-ttu-id="ed017-1276">connectionString</span><span class="sxs-lookup"><span data-stu-id="ed017-1276">connectionString</span></span> | <span data-ttu-id="ed017-1277">Especifique informações necessárias a instância de banco de dados Oracle toohello tooconnect para a propriedade connectionString de saudação.</span><span class="sxs-lookup"><span data-stu-id="ed017-1277">Specify information needed tooconnect toohello Oracle Database instance for hello connectionString property.</span></span> | <span data-ttu-id="ed017-1278">Sim</span><span class="sxs-lookup"><span data-stu-id="ed017-1278">Yes</span></span> |
| <span data-ttu-id="ed017-1279">gatewayName</span><span class="sxs-lookup"><span data-stu-id="ed017-1279">gatewayName</span></span> | <span data-ttu-id="ed017-1280">Nome do gateway de saudação que é usado tooconnect toohello servidor Oracle local</span><span class="sxs-lookup"><span data-stu-id="ed017-1280">Name of hello gateway that that is used tooconnect toohello on-premises Oracle server</span></span> |<span data-ttu-id="ed017-1281">Sim</span><span class="sxs-lookup"><span data-stu-id="ed017-1281">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="ed017-1282">Exemplo</span><span class="sxs-lookup"><span data-stu-id="ed017-1282">Example</span></span>
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

<span data-ttu-id="ed017-1283">Para obter mais informações, consulte o artigo [Conector do Oracle](data-factory-onprem-oracle-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="ed017-1283">For more information, see [Oracle connector](data-factory-onprem-oracle-connector.md#linked-service-properties) article.</span></span>

### <a name="dataset"></a><span data-ttu-id="ed017-1284">Conjunto de dados</span><span class="sxs-lookup"><span data-stu-id="ed017-1284">Dataset</span></span>
<span data-ttu-id="ed017-1285">toodefine um conjunto de dados Oracle, Olá conjunto **tipo** do conjunto de dados de saudação muito**OracleTable**e especifique Olá seguintes propriedades em Olá **typeProperties** seção:</span><span class="sxs-lookup"><span data-stu-id="ed017-1285">toodefine an Oracle dataset, set hello **type** of hello dataset too**OracleTable**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="ed017-1286">Propriedade</span><span class="sxs-lookup"><span data-stu-id="ed017-1286">Property</span></span> | <span data-ttu-id="ed017-1287">Descrição</span><span class="sxs-lookup"><span data-stu-id="ed017-1287">Description</span></span> | <span data-ttu-id="ed017-1288">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="ed017-1288">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ed017-1289">tableName</span><span class="sxs-lookup"><span data-stu-id="ed017-1289">tableName</span></span> |<span data-ttu-id="ed017-1290">Nome da tabela de saudação na Olá banco de dados Oracle que Olá serviço vinculado refere-se a.</span><span class="sxs-lookup"><span data-stu-id="ed017-1290">Name of hello table in hello Oracle Database that hello linked service refers to.</span></span> |<span data-ttu-id="ed017-1291">Não (se **oracleReaderQuery** de **OracleSource** for especificado)</span><span class="sxs-lookup"><span data-stu-id="ed017-1291">No (if **oracleReaderQuery** of **OracleSource** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="ed017-1292">Exemplo</span><span class="sxs-lookup"><span data-stu-id="ed017-1292">Example</span></span>

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
<span data-ttu-id="ed017-1293">Para obter mais informações, consulte o artigo [Conector do Oracle](data-factory-onprem-oracle-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="ed017-1293">For more information, see [Oracle connector](data-factory-onprem-oracle-connector.md#dataset-properties) article.</span></span>

### <a name="oracle-source-in-copy-activity"></a><span data-ttu-id="ed017-1294">Origem do Oracle na Atividade de Cópia</span><span class="sxs-lookup"><span data-stu-id="ed017-1294">Oracle Source in Copy Activity</span></span>
<span data-ttu-id="ed017-1295">Se você estiver copiando dados de um banco de dados Oracle, defina Olá **tipo de fonte** de hello atividade de cópia muito**OracleSource**e especificar propriedades no Olá a seguir **fonte** seção:</span><span class="sxs-lookup"><span data-stu-id="ed017-1295">If you are copying data from an Oracle database, set hello **source type** of hello copy activity too**OracleSource**, and specify following properties in hello **source** section:</span></span>

| <span data-ttu-id="ed017-1296">Propriedade</span><span class="sxs-lookup"><span data-stu-id="ed017-1296">Property</span></span> | <span data-ttu-id="ed017-1297">Descrição</span><span class="sxs-lookup"><span data-stu-id="ed017-1297">Description</span></span> | <span data-ttu-id="ed017-1298">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="ed017-1298">Allowed values</span></span> | <span data-ttu-id="ed017-1299">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="ed017-1299">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="ed017-1300">oracleReaderQuery</span><span class="sxs-lookup"><span data-stu-id="ed017-1300">oracleReaderQuery</span></span> |<span data-ttu-id="ed017-1301">Use dados de tooread Olá consulta personalizada.</span><span class="sxs-lookup"><span data-stu-id="ed017-1301">Use hello custom query tooread data.</span></span> |<span data-ttu-id="ed017-1302">Cadeia de caracteres de consulta SQL.</span><span class="sxs-lookup"><span data-stu-id="ed017-1302">SQL query string.</span></span> <span data-ttu-id="ed017-1303">Por exemplo: `select * from MyTable`</span><span class="sxs-lookup"><span data-stu-id="ed017-1303">For example: `select * from MyTable`</span></span> <br/><br/><span data-ttu-id="ed017-1304">Se não for especificado, Olá instrução SQL executada:`select * from MyTable`</span><span class="sxs-lookup"><span data-stu-id="ed017-1304">If not specified, hello SQL statement that is executed: `select * from MyTable`</span></span> |<span data-ttu-id="ed017-1305">Não (se **tableName** de **dataset** for especificado)</span><span class="sxs-lookup"><span data-stu-id="ed017-1305">No (if **tableName** of **dataset** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="ed017-1306">Exemplo</span><span class="sxs-lookup"><span data-stu-id="ed017-1306">Example</span></span>

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

<span data-ttu-id="ed017-1307">Para obter mais informações, consulte o artigo [Conector do Oracle](data-factory-onprem-oracle-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="ed017-1307">For more information, see [Oracle connector](data-factory-onprem-oracle-connector.md#copy-activity-properties) article.</span></span>

### <a name="oracle-sink-in-copy-activity"></a><span data-ttu-id="ed017-1308">Coletor do Oracle na Atividade de Cópia</span><span class="sxs-lookup"><span data-stu-id="ed017-1308">Oracle Sink in Copy Activity</span></span>
<span data-ttu-id="ed017-1309">Se você estiver copiando o banco de dados do Oracle data tooam, defina Olá **tipo de coletor** de hello atividade de cópia muito**OracleSink**e especificar propriedades no Olá a seguir **coletor** seção:</span><span class="sxs-lookup"><span data-stu-id="ed017-1309">If you are copying data tooam Oracle database, set hello **sink type** of hello copy activity too**OracleSink**, and specify following properties in hello **sink** section:</span></span>

| <span data-ttu-id="ed017-1310">Propriedade</span><span class="sxs-lookup"><span data-stu-id="ed017-1310">Property</span></span> | <span data-ttu-id="ed017-1311">Descrição</span><span class="sxs-lookup"><span data-stu-id="ed017-1311">Description</span></span> | <span data-ttu-id="ed017-1312">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="ed017-1312">Allowed values</span></span> | <span data-ttu-id="ed017-1313">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="ed017-1313">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="ed017-1314">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="ed017-1314">writeBatchTimeout</span></span> |<span data-ttu-id="ed017-1315">Tempo de espera para Olá toocomplete de operação de inserção de lote antes de expirar.</span><span class="sxs-lookup"><span data-stu-id="ed017-1315">Wait time for hello batch insert operation toocomplete before it times out.</span></span> |<span data-ttu-id="ed017-1316">timespan</span><span class="sxs-lookup"><span data-stu-id="ed017-1316">timespan</span></span><br/><br/> <span data-ttu-id="ed017-1317">Exemplo: "00:30:00" (30 minutos).</span><span class="sxs-lookup"><span data-stu-id="ed017-1317">Example: 00:30:00 (30 minutes).</span></span> |<span data-ttu-id="ed017-1318">Não</span><span class="sxs-lookup"><span data-stu-id="ed017-1318">No</span></span> |
| <span data-ttu-id="ed017-1319">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="ed017-1319">writeBatchSize</span></span> |<span data-ttu-id="ed017-1320">Insere dados na tabela do SQL hello quando o tamanho do buffer de saudação atingir writeBatchSize.</span><span class="sxs-lookup"><span data-stu-id="ed017-1320">Inserts data into hello SQL table when hello buffer size reaches writeBatchSize.</span></span> |<span data-ttu-id="ed017-1321">Inteiro (número de linhas)</span><span class="sxs-lookup"><span data-stu-id="ed017-1321">Integer (number of rows)</span></span> |<span data-ttu-id="ed017-1322">Não (padrão: 100)</span><span class="sxs-lookup"><span data-stu-id="ed017-1322">No (default: 100)</span></span> |
| <span data-ttu-id="ed017-1323">sqlWriterCleanupScript</span><span class="sxs-lookup"><span data-stu-id="ed017-1323">sqlWriterCleanupScript</span></span> |<span data-ttu-id="ed017-1324">Especifique uma consulta para a atividade de cópia tooexecute, de modo que os dados de uma fatia específica é limpa.</span><span class="sxs-lookup"><span data-stu-id="ed017-1324">Specify a query for Copy Activity tooexecute such that data of a specific slice is cleaned up.</span></span> |<span data-ttu-id="ed017-1325">Uma instrução de consulta.</span><span class="sxs-lookup"><span data-stu-id="ed017-1325">A query statement.</span></span> |<span data-ttu-id="ed017-1326">Não</span><span class="sxs-lookup"><span data-stu-id="ed017-1326">No</span></span> |
| <span data-ttu-id="ed017-1327">sliceIdentifierColumnName</span><span class="sxs-lookup"><span data-stu-id="ed017-1327">sliceIdentifierColumnName</span></span> |<span data-ttu-id="ed017-1328">Especifique o nome de coluna para a atividade de cópia toofill com identificador de fatia gerado automaticamente, que é usado tooclean os dados de uma fatia específica quando executada novamente.</span><span class="sxs-lookup"><span data-stu-id="ed017-1328">Specify column name for Copy Activity toofill with auto generated slice identifier, which is used tooclean up data of a specific slice when rerun.</span></span> |<span data-ttu-id="ed017-1329">Nome de uma coluna com tipo de dados de binário (32).</span><span class="sxs-lookup"><span data-stu-id="ed017-1329">Column name of a column with data type of binary(32).</span></span> |<span data-ttu-id="ed017-1330">Não</span><span class="sxs-lookup"><span data-stu-id="ed017-1330">No</span></span> |

#### <a name="example"></a><span data-ttu-id="ed017-1331">Exemplo</span><span class="sxs-lookup"><span data-stu-id="ed017-1331">Example</span></span>
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
<span data-ttu-id="ed017-1332">Para obter mais informações, consulte o artigo [Conector do Oracle](data-factory-onprem-oracle-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="ed017-1332">For more information, see [Oracle connector](data-factory-onprem-oracle-connector.md#copy-activity-properties) article.</span></span>

## <a name="postgresql"></a><span data-ttu-id="ed017-1333">PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="ed017-1333">PostgreSQL</span></span>

### <a name="linked-service"></a><span data-ttu-id="ed017-1334">Serviço vinculado</span><span class="sxs-lookup"><span data-stu-id="ed017-1334">Linked service</span></span>
<span data-ttu-id="ed017-1335">toodefine um PostgreSQL vinculado serviço, Olá conjunto **tipo** de saudação serviço vinculado muito**OnPremisesPostgreSql**e especificar propriedades no Olá a seguir **typeProperties**seção:</span><span class="sxs-lookup"><span data-stu-id="ed017-1335">toodefine a PostgreSQL linked service, set hello **type** of hello linked service too**OnPremisesPostgreSql**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="ed017-1336">Propriedade</span><span class="sxs-lookup"><span data-stu-id="ed017-1336">Property</span></span> | <span data-ttu-id="ed017-1337">Descrição</span><span class="sxs-lookup"><span data-stu-id="ed017-1337">Description</span></span> | <span data-ttu-id="ed017-1338">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="ed017-1338">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ed017-1339">server</span><span class="sxs-lookup"><span data-stu-id="ed017-1339">server</span></span> |<span data-ttu-id="ed017-1340">Nome do servidor do hello PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="ed017-1340">Name of hello PostgreSQL server.</span></span> |<span data-ttu-id="ed017-1341">Sim</span><span class="sxs-lookup"><span data-stu-id="ed017-1341">Yes</span></span> |
| <span data-ttu-id="ed017-1342">database</span><span class="sxs-lookup"><span data-stu-id="ed017-1342">database</span></span> |<span data-ttu-id="ed017-1343">Nome do banco de dados PostgreSQL hello.</span><span class="sxs-lookup"><span data-stu-id="ed017-1343">Name of hello PostgreSQL database.</span></span> |<span data-ttu-id="ed017-1344">Sim</span><span class="sxs-lookup"><span data-stu-id="ed017-1344">Yes</span></span> |
| <span data-ttu-id="ed017-1345">schema</span><span class="sxs-lookup"><span data-stu-id="ed017-1345">schema</span></span> |<span data-ttu-id="ed017-1346">Nome do esquema de saudação no banco de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="ed017-1346">Name of hello schema in hello database.</span></span> <span data-ttu-id="ed017-1347">nome do esquema Olá diferencia maiusculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="ed017-1347">hello schema name is case-sensitive.</span></span> |<span data-ttu-id="ed017-1348">Não</span><span class="sxs-lookup"><span data-stu-id="ed017-1348">No</span></span> |
| <span data-ttu-id="ed017-1349">authenticationType</span><span class="sxs-lookup"><span data-stu-id="ed017-1349">authenticationType</span></span> |<span data-ttu-id="ed017-1350">Tipo de autenticação usado o banco de dados PostgreSQL toohello tooconnect.</span><span class="sxs-lookup"><span data-stu-id="ed017-1350">Type of authentication used tooconnect toohello PostgreSQL database.</span></span> <span data-ttu-id="ed017-1351">Os valores possíveis são: Anonymous, Basic e Windows.</span><span class="sxs-lookup"><span data-stu-id="ed017-1351">Possible values are: Anonymous, Basic, and Windows.</span></span> |<span data-ttu-id="ed017-1352">Sim</span><span class="sxs-lookup"><span data-stu-id="ed017-1352">Yes</span></span> |
| <span data-ttu-id="ed017-1353">Nome de Usuário</span><span class="sxs-lookup"><span data-stu-id="ed017-1353">username</span></span> |<span data-ttu-id="ed017-1354">Especifique o nome de usuário se você estiver usando a autenticação Basic ou Windows.</span><span class="sxs-lookup"><span data-stu-id="ed017-1354">Specify user name if you are using Basic or Windows authentication.</span></span> |<span data-ttu-id="ed017-1355">Não</span><span class="sxs-lookup"><span data-stu-id="ed017-1355">No</span></span> |
| <span data-ttu-id="ed017-1356">Senha</span><span class="sxs-lookup"><span data-stu-id="ed017-1356">password</span></span> |<span data-ttu-id="ed017-1357">Especifique a senha da conta de usuário de saudação especificado para nome de usuário de saudação.</span><span class="sxs-lookup"><span data-stu-id="ed017-1357">Specify password for hello user account you specified for hello username.</span></span> |<span data-ttu-id="ed017-1358">Não</span><span class="sxs-lookup"><span data-stu-id="ed017-1358">No</span></span> |
| <span data-ttu-id="ed017-1359">gatewayName</span><span class="sxs-lookup"><span data-stu-id="ed017-1359">gatewayName</span></span> |<span data-ttu-id="ed017-1360">Nome do gateway Olá Olá serviço da fábrica de dados deve usar tooconnect toohello local banco de dados PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="ed017-1360">Name of hello gateway that hello Data Factory service should use tooconnect toohello on-premises PostgreSQL database.</span></span> |<span data-ttu-id="ed017-1361">Sim</span><span class="sxs-lookup"><span data-stu-id="ed017-1361">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="ed017-1362">Exemplo</span><span class="sxs-lookup"><span data-stu-id="ed017-1362">Example</span></span>

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
<span data-ttu-id="ed017-1363">Para obter mais informações, consulte o artigo [Conector do PostgreSQL](data-factory-onprem-postgresql-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="ed017-1363">For more information, see [PostgreSQL connector](data-factory-onprem-postgresql-connector.md#linked-service-properties) article.</span></span>

### <a name="dataset"></a><span data-ttu-id="ed017-1364">Conjunto de dados</span><span class="sxs-lookup"><span data-stu-id="ed017-1364">Dataset</span></span>
<span data-ttu-id="ed017-1365">toodefine um conjunto de dados PostgreSQL, Olá conjunto **tipo** do conjunto de dados de saudação muito**RelationalTable**e especifique Olá seguintes propriedades em Olá **typeProperties** seção:</span><span class="sxs-lookup"><span data-stu-id="ed017-1365">toodefine a PostgreSQL dataset, set hello **type** of hello dataset too**RelationalTable**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="ed017-1366">Propriedade</span><span class="sxs-lookup"><span data-stu-id="ed017-1366">Property</span></span> | <span data-ttu-id="ed017-1367">Descrição</span><span class="sxs-lookup"><span data-stu-id="ed017-1367">Description</span></span> | <span data-ttu-id="ed017-1368">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="ed017-1368">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ed017-1369">tableName</span><span class="sxs-lookup"><span data-stu-id="ed017-1369">tableName</span></span> |<span data-ttu-id="ed017-1370">Nome da tabela de saudação em Olá instância de banco de dados PostgreSQL serviço vinculado refere-se a.</span><span class="sxs-lookup"><span data-stu-id="ed017-1370">Name of hello table in hello PostgreSQL Database instance that linked service refers to.</span></span> <span data-ttu-id="ed017-1371">Olá tableName diferencia maiusculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="ed017-1371">hello tableName is case-sensitive.</span></span> |<span data-ttu-id="ed017-1372">Não (se **query** de **RelationalSource** for especificado)</span><span class="sxs-lookup"><span data-stu-id="ed017-1372">No (if **query** of **RelationalSource** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="ed017-1373">Exemplo</span><span class="sxs-lookup"><span data-stu-id="ed017-1373">Example</span></span>
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
<span data-ttu-id="ed017-1374">Para obter mais informações, consulte o artigo [Conector do PostgreSQL](data-factory-onprem-postgresql-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="ed017-1374">For more information, see [PostgreSQL connector](data-factory-onprem-postgresql-connector.md#dataset-properties) article.</span></span>

### <a name="relational-source-in-copy-activity"></a><span data-ttu-id="ed017-1375">Origem Relacional na Atividade de Cópia</span><span class="sxs-lookup"><span data-stu-id="ed017-1375">Relational Source in Copy Activity</span></span>
<span data-ttu-id="ed017-1376">Se você estiver copiando dados de um banco de dados PostgreSQL, defina Olá **tipo de fonte** de hello atividade de cópia muito**RelationalSource**e especificar propriedades no Olá a seguir **fonte**seção:</span><span class="sxs-lookup"><span data-stu-id="ed017-1376">If you are copying data from a PostgreSQL database, set hello **source type** of hello copy activity too**RelationalSource**, and specify following properties in hello **source** section:</span></span>


| <span data-ttu-id="ed017-1377">Propriedade</span><span class="sxs-lookup"><span data-stu-id="ed017-1377">Property</span></span> | <span data-ttu-id="ed017-1378">Descrição</span><span class="sxs-lookup"><span data-stu-id="ed017-1378">Description</span></span> | <span data-ttu-id="ed017-1379">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="ed017-1379">Allowed values</span></span> | <span data-ttu-id="ed017-1380">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="ed017-1380">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="ed017-1381">query</span><span class="sxs-lookup"><span data-stu-id="ed017-1381">query</span></span> |<span data-ttu-id="ed017-1382">Use dados de tooread Olá consulta personalizada.</span><span class="sxs-lookup"><span data-stu-id="ed017-1382">Use hello custom query tooread data.</span></span> |<span data-ttu-id="ed017-1383">Cadeia de caracteres de consulta SQL.</span><span class="sxs-lookup"><span data-stu-id="ed017-1383">SQL query string.</span></span> <span data-ttu-id="ed017-1384">Por exemplo: "query": "select * from \"MySchema\".\"MyTable\"".</span><span class="sxs-lookup"><span data-stu-id="ed017-1384">For example: "query": "select * from \"MySchema\".\"MyTable\"".</span></span> |<span data-ttu-id="ed017-1385">Não (se **tableName** de **dataset** for especificado)</span><span class="sxs-lookup"><span data-stu-id="ed017-1385">No (if **tableName** of **dataset** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="ed017-1386">Exemplo</span><span class="sxs-lookup"><span data-stu-id="ed017-1386">Example</span></span>

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

<span data-ttu-id="ed017-1387">Para obter mais informações, consulte o artigo [Conector do PostgreSQL](data-factory-onprem-postgresql-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="ed017-1387">For more information, see [PostgreSQL connector](data-factory-onprem-postgresql-connector.md#copy-activity-properties) article.</span></span>

## <a name="sap-business-warehouse"></a><span data-ttu-id="ed017-1388">SAP Business Warehouse</span><span class="sxs-lookup"><span data-stu-id="ed017-1388">SAP Business Warehouse</span></span>


### <a name="linked-service"></a><span data-ttu-id="ed017-1389">Serviço vinculado</span><span class="sxs-lookup"><span data-stu-id="ed017-1389">Linked service</span></span>
<span data-ttu-id="ed017-1390">toodefine um SAP Business Warehouse (BW) o serviço saudação do conjunto vinculado **tipo** de saudação serviço vinculado muito**SapBw**e especificar propriedades no Olá a seguir **typeProperties**seção:</span><span class="sxs-lookup"><span data-stu-id="ed017-1390">toodefine a SAP Business Warehouse (BW) linked service, set hello **type** of hello linked service too**SapBw**, and specify following properties in hello **typeProperties** section:</span></span>  

<span data-ttu-id="ed017-1391">Propriedade</span><span class="sxs-lookup"><span data-stu-id="ed017-1391">Property</span></span> | <span data-ttu-id="ed017-1392">Descrição</span><span class="sxs-lookup"><span data-stu-id="ed017-1392">Description</span></span> | <span data-ttu-id="ed017-1393">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="ed017-1393">Allowed values</span></span> | <span data-ttu-id="ed017-1394">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="ed017-1394">Required</span></span>
-------- | ----------- | -------------- | --------
<span data-ttu-id="ed017-1395">server</span><span class="sxs-lookup"><span data-stu-id="ed017-1395">server</span></span> | <span data-ttu-id="ed017-1396">Nome do servidor de saudação no qual Olá SAP BW instância reside.</span><span class="sxs-lookup"><span data-stu-id="ed017-1396">Name of hello server on which hello SAP BW instance resides.</span></span> | <span data-ttu-id="ed017-1397">string</span><span class="sxs-lookup"><span data-stu-id="ed017-1397">string</span></span> | <span data-ttu-id="ed017-1398">Sim</span><span class="sxs-lookup"><span data-stu-id="ed017-1398">Yes</span></span>
<span data-ttu-id="ed017-1399">systemNumber</span><span class="sxs-lookup"><span data-stu-id="ed017-1399">systemNumber</span></span> | <span data-ttu-id="ed017-1400">Número de sistema de saudação sistema SAP BW.</span><span class="sxs-lookup"><span data-stu-id="ed017-1400">System number of hello SAP BW system.</span></span> | <span data-ttu-id="ed017-1401">Número decimal de dois dígitos representado como uma cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="ed017-1401">Two-digit decimal number represented as a string.</span></span> | <span data-ttu-id="ed017-1402">Sim</span><span class="sxs-lookup"><span data-stu-id="ed017-1402">Yes</span></span>
<span data-ttu-id="ed017-1403">clientId</span><span class="sxs-lookup"><span data-stu-id="ed017-1403">clientId</span></span> | <span data-ttu-id="ed017-1404">ID do cliente do cliente Olá Olá sistema SAP W.</span><span class="sxs-lookup"><span data-stu-id="ed017-1404">Client ID of hello client in hello SAP W system.</span></span> | <span data-ttu-id="ed017-1405">Número decimal de três dígitos representado como uma cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="ed017-1405">Three-digit decimal number represented as a string.</span></span> | <span data-ttu-id="ed017-1406">Sim</span><span class="sxs-lookup"><span data-stu-id="ed017-1406">Yes</span></span>
<span data-ttu-id="ed017-1407">Nome de Usuário</span><span class="sxs-lookup"><span data-stu-id="ed017-1407">username</span></span> | <span data-ttu-id="ed017-1408">Nome de usuário de saudação que tem acesso toohello SAP server</span><span class="sxs-lookup"><span data-stu-id="ed017-1408">Name of hello user who has access toohello SAP server</span></span> | <span data-ttu-id="ed017-1409">string</span><span class="sxs-lookup"><span data-stu-id="ed017-1409">string</span></span> | <span data-ttu-id="ed017-1410">Sim</span><span class="sxs-lookup"><span data-stu-id="ed017-1410">Yes</span></span>
<span data-ttu-id="ed017-1411">Senha</span><span class="sxs-lookup"><span data-stu-id="ed017-1411">password</span></span> | <span data-ttu-id="ed017-1412">Senha do usuário hello.</span><span class="sxs-lookup"><span data-stu-id="ed017-1412">Password for hello user.</span></span> | <span data-ttu-id="ed017-1413">string</span><span class="sxs-lookup"><span data-stu-id="ed017-1413">string</span></span> | <span data-ttu-id="ed017-1414">Sim</span><span class="sxs-lookup"><span data-stu-id="ed017-1414">Yes</span></span>
<span data-ttu-id="ed017-1415">gatewayName</span><span class="sxs-lookup"><span data-stu-id="ed017-1415">gatewayName</span></span> | <span data-ttu-id="ed017-1416">Nome do gateway Olá Olá serviço da fábrica de dados deve usar a instância de SAP BW tooconnect toohello local.</span><span class="sxs-lookup"><span data-stu-id="ed017-1416">Name of hello gateway that hello Data Factory service should use tooconnect toohello on-premises SAP BW instance.</span></span> | <span data-ttu-id="ed017-1417">string</span><span class="sxs-lookup"><span data-stu-id="ed017-1417">string</span></span> | <span data-ttu-id="ed017-1418">Sim</span><span class="sxs-lookup"><span data-stu-id="ed017-1418">Yes</span></span>
<span data-ttu-id="ed017-1419">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="ed017-1419">encryptedCredential</span></span> | <span data-ttu-id="ed017-1420">cadeia de caracteres de credencial Olá criptografado.</span><span class="sxs-lookup"><span data-stu-id="ed017-1420">hello encrypted credential string.</span></span> | <span data-ttu-id="ed017-1421">string</span><span class="sxs-lookup"><span data-stu-id="ed017-1421">string</span></span> | <span data-ttu-id="ed017-1422">Não</span><span class="sxs-lookup"><span data-stu-id="ed017-1422">No</span></span>

#### <a name="example"></a><span data-ttu-id="ed017-1423">Exemplo</span><span class="sxs-lookup"><span data-stu-id="ed017-1423">Example</span></span>

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

<span data-ttu-id="ed017-1424">Para obter mais informações, consulte o artigo [Conector do SAP Business Warehouse](data-factory-sap-business-warehouse-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="ed017-1424">For more information, see [SAP Business Warehouse connector](data-factory-sap-business-warehouse-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="ed017-1425">Conjunto de dados</span><span class="sxs-lookup"><span data-stu-id="ed017-1425">Dataset</span></span>
<span data-ttu-id="ed017-1426">toodefine um conjunto de dados do SAP BW, Olá conjunto **tipo** do conjunto de dados de saudação muito**RelationalTable**.</span><span class="sxs-lookup"><span data-stu-id="ed017-1426">toodefine a SAP BW dataset, set hello **type** of hello dataset too**RelationalTable**.</span></span> <span data-ttu-id="ed017-1427">Não existem propriedades específicas do tipo de suporte para o conjunto de dados de SAP BW de saudação do tipo **RelationalTable**.</span><span class="sxs-lookup"><span data-stu-id="ed017-1427">There are no type-specific properties supported for hello SAP BW dataset of type **RelationalTable**.</span></span>  

#### <a name="example"></a><span data-ttu-id="ed017-1428">Exemplo</span><span class="sxs-lookup"><span data-stu-id="ed017-1428">Example</span></span>

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
<span data-ttu-id="ed017-1429">Para obter mais informações, consulte o artigo [Conector do SAP Business Warehouse](data-factory-sap-business-warehouse-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="ed017-1429">For more information, see [SAP Business Warehouse connector](data-factory-sap-business-warehouse-connector.md#dataset-properties) article.</span></span> 

### <a name="relational-source-in-copy-activity"></a><span data-ttu-id="ed017-1430">Origem Relacional na Atividade de Cópia</span><span class="sxs-lookup"><span data-stu-id="ed017-1430">Relational Source in Copy Activity</span></span>
<span data-ttu-id="ed017-1431">Se você estiver copiando dados do SAP Business Warehouse, defina Olá **tipo de fonte** de hello atividade de cópia muito**RelationalSource**e especificar propriedades no Olá a seguir **fonte**seção:</span><span class="sxs-lookup"><span data-stu-id="ed017-1431">If you are copying data from SAP Business Warehouse, set hello **source type** of hello copy activity too**RelationalSource**, and specify following properties in hello **source** section:</span></span>


| <span data-ttu-id="ed017-1432">Propriedade</span><span class="sxs-lookup"><span data-stu-id="ed017-1432">Property</span></span> | <span data-ttu-id="ed017-1433">Descrição</span><span class="sxs-lookup"><span data-stu-id="ed017-1433">Description</span></span> | <span data-ttu-id="ed017-1434">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="ed017-1434">Allowed values</span></span> | <span data-ttu-id="ed017-1435">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="ed017-1435">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="ed017-1436">query</span><span class="sxs-lookup"><span data-stu-id="ed017-1436">query</span></span> | <span data-ttu-id="ed017-1437">Especifica Olá MDX consulta tooread dados da instância do SAP BW hello.</span><span class="sxs-lookup"><span data-stu-id="ed017-1437">Specifies hello MDX query tooread data from hello SAP BW instance.</span></span> | <span data-ttu-id="ed017-1438">Consulta MDX.</span><span class="sxs-lookup"><span data-stu-id="ed017-1438">MDX query.</span></span> | <span data-ttu-id="ed017-1439">Sim</span><span class="sxs-lookup"><span data-stu-id="ed017-1439">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="ed017-1440">Exemplo</span><span class="sxs-lookup"><span data-stu-id="ed017-1440">Example</span></span>

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

<span data-ttu-id="ed017-1441">Para obter mais informações, consulte o artigo [Conector do SAP Business Warehouse](data-factory-sap-business-warehouse-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="ed017-1441">For more information, see [SAP Business Warehouse connector](data-factory-sap-business-warehouse-connector.md#copy-activity-properties) article.</span></span> 

## <a name="sap-hana"></a><span data-ttu-id="ed017-1442">SAP HANA</span><span class="sxs-lookup"><span data-stu-id="ed017-1442">SAP HANA</span></span>

### <a name="linked-service"></a><span data-ttu-id="ed017-1443">Serviço vinculado</span><span class="sxs-lookup"><span data-stu-id="ed017-1443">Linked service</span></span>
<span data-ttu-id="ed017-1444">toodefine um SAP HANA vinculado serviço, Olá conjunto **tipo** de saudação serviço vinculado muito**SapHana**e especificar propriedades no Olá a seguir **typeProperties** seção:</span><span class="sxs-lookup"><span data-stu-id="ed017-1444">toodefine a SAP HANA linked service, set hello **type** of hello linked service too**SapHana**, and specify following properties in hello **typeProperties** section:</span></span>  

<span data-ttu-id="ed017-1445">Propriedade</span><span class="sxs-lookup"><span data-stu-id="ed017-1445">Property</span></span> | <span data-ttu-id="ed017-1446">Descrição</span><span class="sxs-lookup"><span data-stu-id="ed017-1446">Description</span></span> | <span data-ttu-id="ed017-1447">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="ed017-1447">Allowed values</span></span> | <span data-ttu-id="ed017-1448">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="ed017-1448">Required</span></span>
-------- | ----------- | -------------- | --------
<span data-ttu-id="ed017-1449">server</span><span class="sxs-lookup"><span data-stu-id="ed017-1449">server</span></span> | <span data-ttu-id="ed017-1450">Nome do servidor de saudação no qual Olá SAP HANA instância reside.</span><span class="sxs-lookup"><span data-stu-id="ed017-1450">Name of hello server on which hello SAP HANA instance resides.</span></span> <span data-ttu-id="ed017-1451">Se o servidor estiver usando uma porta personalizada, especifique `server:port`.</span><span class="sxs-lookup"><span data-stu-id="ed017-1451">If your server is using a customized port, specify `server:port`.</span></span> | <span data-ttu-id="ed017-1452">string</span><span class="sxs-lookup"><span data-stu-id="ed017-1452">string</span></span> | <span data-ttu-id="ed017-1453">Sim</span><span class="sxs-lookup"><span data-stu-id="ed017-1453">Yes</span></span>
<span data-ttu-id="ed017-1454">authenticationType</span><span class="sxs-lookup"><span data-stu-id="ed017-1454">authenticationType</span></span> | <span data-ttu-id="ed017-1455">Tipo de autenticação.</span><span class="sxs-lookup"><span data-stu-id="ed017-1455">Type of authentication.</span></span> | <span data-ttu-id="ed017-1456">cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="ed017-1456">string.</span></span> <span data-ttu-id="ed017-1457">"Básico" ou "Windows"</span><span class="sxs-lookup"><span data-stu-id="ed017-1457">"Basic" or "Windows"</span></span> | <span data-ttu-id="ed017-1458">Sim</span><span class="sxs-lookup"><span data-stu-id="ed017-1458">Yes</span></span> 
<span data-ttu-id="ed017-1459">Nome de Usuário</span><span class="sxs-lookup"><span data-stu-id="ed017-1459">username</span></span> | <span data-ttu-id="ed017-1460">Nome de usuário de saudação que tem acesso toohello SAP server</span><span class="sxs-lookup"><span data-stu-id="ed017-1460">Name of hello user who has access toohello SAP server</span></span> | <span data-ttu-id="ed017-1461">string</span><span class="sxs-lookup"><span data-stu-id="ed017-1461">string</span></span> | <span data-ttu-id="ed017-1462">Sim</span><span class="sxs-lookup"><span data-stu-id="ed017-1462">Yes</span></span>
<span data-ttu-id="ed017-1463">Senha</span><span class="sxs-lookup"><span data-stu-id="ed017-1463">password</span></span> | <span data-ttu-id="ed017-1464">Senha do usuário hello.</span><span class="sxs-lookup"><span data-stu-id="ed017-1464">Password for hello user.</span></span> | <span data-ttu-id="ed017-1465">string</span><span class="sxs-lookup"><span data-stu-id="ed017-1465">string</span></span> | <span data-ttu-id="ed017-1466">Sim</span><span class="sxs-lookup"><span data-stu-id="ed017-1466">Yes</span></span>
<span data-ttu-id="ed017-1467">gatewayName</span><span class="sxs-lookup"><span data-stu-id="ed017-1467">gatewayName</span></span> | <span data-ttu-id="ed017-1468">Nome do gateway Olá Olá serviço da fábrica de dados deve usar a instância de SAP HANA tooconnect toohello local.</span><span class="sxs-lookup"><span data-stu-id="ed017-1468">Name of hello gateway that hello Data Factory service should use tooconnect toohello on-premises SAP HANA instance.</span></span> | <span data-ttu-id="ed017-1469">string</span><span class="sxs-lookup"><span data-stu-id="ed017-1469">string</span></span> | <span data-ttu-id="ed017-1470">Sim</span><span class="sxs-lookup"><span data-stu-id="ed017-1470">Yes</span></span>
<span data-ttu-id="ed017-1471">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="ed017-1471">encryptedCredential</span></span> | <span data-ttu-id="ed017-1472">cadeia de caracteres de credencial Olá criptografado.</span><span class="sxs-lookup"><span data-stu-id="ed017-1472">hello encrypted credential string.</span></span> | <span data-ttu-id="ed017-1473">string</span><span class="sxs-lookup"><span data-stu-id="ed017-1473">string</span></span> | <span data-ttu-id="ed017-1474">Não</span><span class="sxs-lookup"><span data-stu-id="ed017-1474">No</span></span>

#### <a name="example"></a><span data-ttu-id="ed017-1475">Exemplo</span><span class="sxs-lookup"><span data-stu-id="ed017-1475">Example</span></span>

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
<span data-ttu-id="ed017-1476">Para obter mais informações, consulte o artigo [Conector do SAP HANA](data-factory-sap-hana-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="ed017-1476">For more information, see [SAP HANA connector](data-factory-sap-hana-connector.md#linked-service-properties) article.</span></span>
 
### <a name="dataset"></a><span data-ttu-id="ed017-1477">Conjunto de dados</span><span class="sxs-lookup"><span data-stu-id="ed017-1477">Dataset</span></span>
<span data-ttu-id="ed017-1478">toodefine um conjunto de dados do SAP HANA, Olá conjunto **tipo** do conjunto de dados de saudação muito**RelationalTable**.</span><span class="sxs-lookup"><span data-stu-id="ed017-1478">toodefine a SAP HANA dataset, set hello **type** of hello dataset too**RelationalTable**.</span></span> <span data-ttu-id="ed017-1479">Não existem propriedades específicas do tipo de suporte para o dataset do SAP HANA saudação do tipo **RelationalTable**.</span><span class="sxs-lookup"><span data-stu-id="ed017-1479">There are no type-specific properties supported for hello SAP HANA dataset of type **RelationalTable**.</span></span> 

#### <a name="example"></a><span data-ttu-id="ed017-1480">Exemplo</span><span class="sxs-lookup"><span data-stu-id="ed017-1480">Example</span></span>

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
<span data-ttu-id="ed017-1481">Para obter mais informações, consulte o artigo [Conector do SAP HANA](data-factory-sap-hana-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="ed017-1481">For more information, see [SAP HANA connector](data-factory-sap-hana-connector.md#dataset-properties) article.</span></span> 

### <a name="relational-source-in-copy-activity"></a><span data-ttu-id="ed017-1482">Origem Relacional na Atividade de Cópia</span><span class="sxs-lookup"><span data-stu-id="ed017-1482">Relational Source in Copy Activity</span></span>
<span data-ttu-id="ed017-1483">Se você estiver copiando dados de um repositório de dados do SAP HANA, defina Olá **tipo de fonte** de hello atividade de cópia muito**RelationalSource**e especificar propriedades no Olá a seguir **fonte**seção:</span><span class="sxs-lookup"><span data-stu-id="ed017-1483">If you are copying data from a SAP HANA data store, set hello **source type** of hello copy activity too**RelationalSource**, and specify following properties in hello **source** section:</span></span>

| <span data-ttu-id="ed017-1484">Propriedade</span><span class="sxs-lookup"><span data-stu-id="ed017-1484">Property</span></span> | <span data-ttu-id="ed017-1485">Descrição</span><span class="sxs-lookup"><span data-stu-id="ed017-1485">Description</span></span> | <span data-ttu-id="ed017-1486">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="ed017-1486">Allowed values</span></span> | <span data-ttu-id="ed017-1487">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="ed017-1487">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="ed017-1488">query</span><span class="sxs-lookup"><span data-stu-id="ed017-1488">query</span></span> | <span data-ttu-id="ed017-1489">Especifica Olá SQL consulta tooread dados da instância do SAP HANA hello.</span><span class="sxs-lookup"><span data-stu-id="ed017-1489">Specifies hello SQL query tooread data from hello SAP HANA instance.</span></span> | <span data-ttu-id="ed017-1490">Consulta SQL.</span><span class="sxs-lookup"><span data-stu-id="ed017-1490">SQL query.</span></span> | <span data-ttu-id="ed017-1491">Sim</span><span class="sxs-lookup"><span data-stu-id="ed017-1491">Yes</span></span> |


#### <a name="example"></a><span data-ttu-id="ed017-1492">Exemplo</span><span class="sxs-lookup"><span data-stu-id="ed017-1492">Example</span></span>


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

<span data-ttu-id="ed017-1493">Para obter mais informações, consulte o artigo [Conector do SAP HANA](data-factory-sap-hana-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="ed017-1493">For more information, see [SAP HANA connector](data-factory-sap-hana-connector.md#copy-activity-properties) article.</span></span>


## <a name="sql-server"></a><span data-ttu-id="ed017-1494">SQL Server</span><span class="sxs-lookup"><span data-stu-id="ed017-1494">SQL Server</span></span>

### <a name="linked-service"></a><span data-ttu-id="ed017-1495">Serviço vinculado</span><span class="sxs-lookup"><span data-stu-id="ed017-1495">Linked service</span></span>
<span data-ttu-id="ed017-1496">Criar um serviço vinculado do tipo **OnPremisesSqlServer** toolink uma fábrica de dados tooa de banco de dados do local do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="ed017-1496">You create a linked service of type **OnPremisesSqlServer** toolink an on-premises SQL Server database tooa data factory.</span></span> <span data-ttu-id="ed017-1497">Olá a tabela a seguir fornece uma descrição para o serviço vinculado do SQL Server do JSON elementos tooon local específico.</span><span class="sxs-lookup"><span data-stu-id="ed017-1497">hello following table provides description for JSON elements specific tooon-premises SQL Server linked service.</span></span>

<span data-ttu-id="ed017-1498">Olá, a tabela a seguir fornece uma descrição para o JSON de elementos específico tooSQL serviço do servidor vinculado.</span><span class="sxs-lookup"><span data-stu-id="ed017-1498">hello following table provides description for JSON elements specific tooSQL Server linked service.</span></span>

| <span data-ttu-id="ed017-1499">Propriedade</span><span class="sxs-lookup"><span data-stu-id="ed017-1499">Property</span></span> | <span data-ttu-id="ed017-1500">Descrição</span><span class="sxs-lookup"><span data-stu-id="ed017-1500">Description</span></span> | <span data-ttu-id="ed017-1501">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="ed017-1501">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ed017-1502">type</span><span class="sxs-lookup"><span data-stu-id="ed017-1502">type</span></span> |<span data-ttu-id="ed017-1503">propriedade de tipo Hello deve ser definida como: **OnPremisesSqlServer**.</span><span class="sxs-lookup"><span data-stu-id="ed017-1503">hello type property should be set to: **OnPremisesSqlServer**.</span></span> |<span data-ttu-id="ed017-1504">Sim</span><span class="sxs-lookup"><span data-stu-id="ed017-1504">Yes</span></span> |
| <span data-ttu-id="ed017-1505">connectionString</span><span class="sxs-lookup"><span data-stu-id="ed017-1505">connectionString</span></span> |<span data-ttu-id="ed017-1506">Especifica informações de connectionString necessárias tooconnect toohello no SQL Server banco de dados local usando a autenticação do Windows ou autenticação do SQL.</span><span class="sxs-lookup"><span data-stu-id="ed017-1506">Specify connectionString information needed tooconnect toohello on-premises SQL Server database using either SQL authentication or Windows authentication.</span></span> |<span data-ttu-id="ed017-1507">Sim</span><span class="sxs-lookup"><span data-stu-id="ed017-1507">Yes</span></span> |
| <span data-ttu-id="ed017-1508">gatewayName</span><span class="sxs-lookup"><span data-stu-id="ed017-1508">gatewayName</span></span> |<span data-ttu-id="ed017-1509">Nome do gateway Olá Olá serviço da fábrica de dados deve usar o banco de dados do tooconnect toohello no local do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="ed017-1509">Name of hello gateway that hello Data Factory service should use tooconnect toohello on-premises SQL Server database.</span></span> |<span data-ttu-id="ed017-1510">Sim</span><span class="sxs-lookup"><span data-stu-id="ed017-1510">Yes</span></span> |
| <span data-ttu-id="ed017-1511">Nome de Usuário</span><span class="sxs-lookup"><span data-stu-id="ed017-1511">username</span></span> |<span data-ttu-id="ed017-1512">Especifique o nome de usuário se você estiver usando a Autenticação do Windows.</span><span class="sxs-lookup"><span data-stu-id="ed017-1512">Specify user name if you are using Windows Authentication.</span></span> <span data-ttu-id="ed017-1513">Exemplo: **domainname\\username**.</span><span class="sxs-lookup"><span data-stu-id="ed017-1513">Example: **domainname\\username**.</span></span> |<span data-ttu-id="ed017-1514">Não</span><span class="sxs-lookup"><span data-stu-id="ed017-1514">No</span></span> |
| <span data-ttu-id="ed017-1515">Senha</span><span class="sxs-lookup"><span data-stu-id="ed017-1515">password</span></span> |<span data-ttu-id="ed017-1516">Especifique a senha da conta de usuário de saudação especificado para nome de usuário de saudação.</span><span class="sxs-lookup"><span data-stu-id="ed017-1516">Specify password for hello user account you specified for hello username.</span></span> |<span data-ttu-id="ed017-1517">Não</span><span class="sxs-lookup"><span data-stu-id="ed017-1517">No</span></span> |

<span data-ttu-id="ed017-1518">Você pode criptografar credenciais usando Olá **New-AzureRmDataFactoryEncryptValue** cmdlet e usá-los na cadeia de caracteres de conexão hello, conforme mostrado no exemplo a seguir de saudação (**EncryptedCredential** propriedade):</span><span class="sxs-lookup"><span data-stu-id="ed017-1518">You can encrypt credentials using hello **New-AzureRmDataFactoryEncryptValue** cmdlet and use them in hello connection string as shown in hello following example (**EncryptedCredential** property):</span></span>  

```json
"connectionString": "Data Source=<servername>;Initial Catalog=<databasename>;Integrated Security=True;EncryptedCredential=<encrypted credential>",
```


#### <a name="example-json-for-using-sql-authentication"></a><span data-ttu-id="ed017-1519">Exemplo: JSON para usar Autenticação SQL</span><span class="sxs-lookup"><span data-stu-id="ed017-1519">Example: JSON for using SQL Authentication</span></span>

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
#### <a name="example-json-for-using-windows-authentication"></a><span data-ttu-id="ed017-1520">Exemplo: JSON para usar Autenticação Windows</span><span class="sxs-lookup"><span data-stu-id="ed017-1520">Example: JSON for using Windows Authentication</span></span>

<span data-ttu-id="ed017-1521">Se o nome de usuário e senha forem especificados, gateway usa tooimpersonate Olá dados do usuário especificado conta tooconnect toohello local do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="ed017-1521">If username and password are specified, gateway uses them tooimpersonate hello specified user account tooconnect toohello on-premises SQL Server database.</span></span> <span data-ttu-id="ed017-1522">Caso contrário, o gateway conecta toohello do SQL Server diretamente com o contexto de segurança de saudação do Gateway (sua conta de inicialização).</span><span class="sxs-lookup"><span data-stu-id="ed017-1522">Otherwise, gateway connects toohello SQL Server directly with hello security context of Gateway (its startup account).</span></span>

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

<span data-ttu-id="ed017-1523">Para obter mais informações, consulte o artigo [Conector de SQL Server](data-factory-sqlserver-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="ed017-1523">For more information, see [SQL Server connector](data-factory-sqlserver-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="ed017-1524">Conjunto de dados</span><span class="sxs-lookup"><span data-stu-id="ed017-1524">Dataset</span></span>
<span data-ttu-id="ed017-1525">toodefine um conjunto de dados do SQL Server, Olá conjunto **tipo** do conjunto de dados de saudação muito**SqlServerTable**e especifique Olá seguintes propriedades em Olá **typeProperties** seção:</span><span class="sxs-lookup"><span data-stu-id="ed017-1525">toodefine a SQL Server dataset, set hello **type** of hello dataset too**SqlServerTable**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="ed017-1526">Propriedade</span><span class="sxs-lookup"><span data-stu-id="ed017-1526">Property</span></span> | <span data-ttu-id="ed017-1527">Descrição</span><span class="sxs-lookup"><span data-stu-id="ed017-1527">Description</span></span> | <span data-ttu-id="ed017-1528">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="ed017-1528">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ed017-1529">tableName</span><span class="sxs-lookup"><span data-stu-id="ed017-1529">tableName</span></span> |<span data-ttu-id="ed017-1530">Nome da tabela de saudação ou exibição na instância de banco de dados do SQL Server Olá que serviço vinculado refere-se a.</span><span class="sxs-lookup"><span data-stu-id="ed017-1530">Name of hello table or view in hello SQL Server Database instance that linked service refers to.</span></span> |<span data-ttu-id="ed017-1531">Sim</span><span class="sxs-lookup"><span data-stu-id="ed017-1531">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="ed017-1532">Exemplo</span><span class="sxs-lookup"><span data-stu-id="ed017-1532">Example</span></span>
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

<span data-ttu-id="ed017-1533">Para obter mais informações, consulte o artigo [Conector de SQL Server](data-factory-sqlserver-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="ed017-1533">For more information, see [SQL Server connector](data-factory-sqlserver-connector.md#dataset-properties) article.</span></span> 

### <a name="sql-source-in-copy-activity"></a><span data-ttu-id="ed017-1534">Origem do SQL na Atividade de Cópia</span><span class="sxs-lookup"><span data-stu-id="ed017-1534">Sql Source in Copy Activity</span></span>
<span data-ttu-id="ed017-1535">Se você estiver copiando dados de um banco de dados do SQL Server, defina Olá **tipo de fonte** de hello atividade de cópia muito**SqlSource**e especificar propriedades no Olá a seguir **fonte** seção:</span><span class="sxs-lookup"><span data-stu-id="ed017-1535">If you are copying data from a SQL Server database, set hello **source type** of hello copy activity too**SqlSource**, and specify following properties in hello **source** section:</span></span>


| <span data-ttu-id="ed017-1536">Propriedade</span><span class="sxs-lookup"><span data-stu-id="ed017-1536">Property</span></span> | <span data-ttu-id="ed017-1537">Descrição</span><span class="sxs-lookup"><span data-stu-id="ed017-1537">Description</span></span> | <span data-ttu-id="ed017-1538">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="ed017-1538">Allowed values</span></span> | <span data-ttu-id="ed017-1539">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="ed017-1539">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="ed017-1540">SqlReaderQuery</span><span class="sxs-lookup"><span data-stu-id="ed017-1540">sqlReaderQuery</span></span> |<span data-ttu-id="ed017-1541">Use dados de tooread Olá consulta personalizada.</span><span class="sxs-lookup"><span data-stu-id="ed017-1541">Use hello custom query tooread data.</span></span> |<span data-ttu-id="ed017-1542">Cadeia de caracteres de consulta SQL.</span><span class="sxs-lookup"><span data-stu-id="ed017-1542">SQL query string.</span></span> <span data-ttu-id="ed017-1543">Por exemplo: `select * from MyTable`.</span><span class="sxs-lookup"><span data-stu-id="ed017-1543">For example: `select * from MyTable`.</span></span> <span data-ttu-id="ed017-1544">Pode fazer referência a várias tabelas de banco de dados de saudação referenciado pelo conjunto de dados de entrada hello.</span><span class="sxs-lookup"><span data-stu-id="ed017-1544">May reference multiple tables from hello database referenced by hello input dataset.</span></span> <span data-ttu-id="ed017-1545">Se não for especificado, Olá instrução SQL executada: selecione MyTable.</span><span class="sxs-lookup"><span data-stu-id="ed017-1545">If not specified, hello SQL statement that is executed: select from MyTable.</span></span> |<span data-ttu-id="ed017-1546">Não</span><span class="sxs-lookup"><span data-stu-id="ed017-1546">No</span></span> |
| <span data-ttu-id="ed017-1547">sqlReaderStoredProcedureName</span><span class="sxs-lookup"><span data-stu-id="ed017-1547">sqlReaderStoredProcedureName</span></span> |<span data-ttu-id="ed017-1548">Nome da saudação procedimento armazenado que lê dados da tabela de origem hello.</span><span class="sxs-lookup"><span data-stu-id="ed017-1548">Name of hello stored procedure that reads data from hello source table.</span></span> |<span data-ttu-id="ed017-1549">Nome da saudação de procedimento armazenado.</span><span class="sxs-lookup"><span data-stu-id="ed017-1549">Name of hello stored procedure.</span></span> |<span data-ttu-id="ed017-1550">Não</span><span class="sxs-lookup"><span data-stu-id="ed017-1550">No</span></span> |
| <span data-ttu-id="ed017-1551">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="ed017-1551">storedProcedureParameters</span></span> |<span data-ttu-id="ed017-1552">Parâmetros de saudação de procedimento armazenado.</span><span class="sxs-lookup"><span data-stu-id="ed017-1552">Parameters for hello stored procedure.</span></span> |<span data-ttu-id="ed017-1553">Pares de nome/valor.</span><span class="sxs-lookup"><span data-stu-id="ed017-1553">Name/value pairs.</span></span> <span data-ttu-id="ed017-1554">Nomes e o uso de maiusculas e minúsculas dos parâmetros devem corresponder a nomes de saudação e uso de maiusculas e minúsculas dos parâmetros de procedimento armazenado de saudação.</span><span class="sxs-lookup"><span data-stu-id="ed017-1554">Names and casing of parameters must match hello names and casing of hello stored procedure parameters.</span></span> |<span data-ttu-id="ed017-1555">Não</span><span class="sxs-lookup"><span data-stu-id="ed017-1555">No</span></span> |

<span data-ttu-id="ed017-1556">Se hello **sqlReaderQuery** é especificada para Olá SqlSource, hello atividade de cópia executa esta consulta em relação aos dados de Olá Olá banco de dados do SQL Server fonte tooget.</span><span class="sxs-lookup"><span data-stu-id="ed017-1556">If hello **sqlReaderQuery** is specified for hello SqlSource, hello Copy Activity runs this query against hello SQL Server Database source tooget hello data.</span></span>

<span data-ttu-id="ed017-1557">Como alternativa, você pode especificar um procedimento armazenado especificando Olá **sqlReaderStoredProcedureName** e **storedProcedureParameters** (se hello procedimento armazenado usa parâmetros).</span><span class="sxs-lookup"><span data-stu-id="ed017-1557">Alternatively, you can specify a stored procedure by specifying hello **sqlReaderStoredProcedureName** and **storedProcedureParameters** (if hello stored procedure takes parameters).</span></span>

<span data-ttu-id="ed017-1558">Se você não especificar sqlReaderQuery ou sqlReaderStoredProcedureName, colunas de Olá definidas na seção de estrutura hello são usada toobuild toorun uma consulta select contra Olá banco de dados do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="ed017-1558">If you do not specify either sqlReaderQuery or sqlReaderStoredProcedureName, hello columns defined in hello structure section are used toobuild a select query toorun against hello SQL Server Database.</span></span> <span data-ttu-id="ed017-1559">Se definição de conjunto de dados de saudação não tem estrutura Olá, todas as colunas da tabela de hello estão selecionadas.</span><span class="sxs-lookup"><span data-stu-id="ed017-1559">If hello dataset definition does not have hello structure, all columns are selected from hello table.</span></span>

> [!NOTE]
> <span data-ttu-id="ed017-1560">Quando você usa **sqlReaderStoredProcedureName**, você ainda precisa toospecify um valor para Olá **tableName** propriedade no conjunto de dados Olá JSON.</span><span class="sxs-lookup"><span data-stu-id="ed017-1560">When you use **sqlReaderStoredProcedureName**, you still need toospecify a value for hello **tableName** property in hello dataset JSON.</span></span> <span data-ttu-id="ed017-1561">Contudo, não há nenhuma validação executada nessa tabela.</span><span class="sxs-lookup"><span data-stu-id="ed017-1561">There are no validations performed against this table though.</span></span>


#### <a name="example"></a><span data-ttu-id="ed017-1562">Exemplo</span><span class="sxs-lookup"><span data-stu-id="ed017-1562">Example</span></span>
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

<span data-ttu-id="ed017-1563">Neste exemplo, **sqlReaderQuery** é especificado para Olá SqlSource.</span><span class="sxs-lookup"><span data-stu-id="ed017-1563">In this example, **sqlReaderQuery** is specified for hello SqlSource.</span></span> <span data-ttu-id="ed017-1564">Hello atividade de cópia executa esta consulta Olá dados do banco de dados do SQL Server origem tooget hello.</span><span class="sxs-lookup"><span data-stu-id="ed017-1564">hello Copy Activity runs this query against hello SQL Server Database source tooget hello data.</span></span> <span data-ttu-id="ed017-1565">Como alternativa, você pode especificar um procedimento armazenado especificando Olá **sqlReaderStoredProcedureName** e **storedProcedureParameters** (se hello procedimento armazenado usa parâmetros).</span><span class="sxs-lookup"><span data-stu-id="ed017-1565">Alternatively, you can specify a stored procedure by specifying hello **sqlReaderStoredProcedureName** and **storedProcedureParameters** (if hello stored procedure takes parameters).</span></span> <span data-ttu-id="ed017-1566">Olá sqlReaderQuery pode fazer referência a várias tabelas no banco de dados de saudação referenciado pelo conjunto de dados de entrada hello.</span><span class="sxs-lookup"><span data-stu-id="ed017-1566">hello sqlReaderQuery can reference multiple tables within hello database referenced by hello input dataset.</span></span> <span data-ttu-id="ed017-1567">Ele não é limitado tooonly Olá definido como Olá typeProperty de tableName do conjunto de dados.</span><span class="sxs-lookup"><span data-stu-id="ed017-1567">It is not limited tooonly hello table set as hello dataset's tableName typeProperty.</span></span>

<span data-ttu-id="ed017-1568">Se você não especificar sqlReaderQuery ou sqlReaderStoredProcedureName, colunas de Olá definidas na seção de estrutura hello são usada toobuild toorun uma consulta select contra Olá banco de dados do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="ed017-1568">If you do not specify sqlReaderQuery or sqlReaderStoredProcedureName, hello columns defined in hello structure section are used toobuild a select query toorun against hello SQL Server Database.</span></span> <span data-ttu-id="ed017-1569">Se definição de conjunto de dados de saudação não tem estrutura Olá, todas as colunas da tabela de hello estão selecionadas.</span><span class="sxs-lookup"><span data-stu-id="ed017-1569">If hello dataset definition does not have hello structure, all columns are selected from hello table.</span></span>

<span data-ttu-id="ed017-1570">Para obter mais informações, consulte o artigo [Conector de SQL Server](data-factory-sqlserver-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="ed017-1570">For more information, see [SQL Server connector](data-factory-sqlserver-connector.md#copy-activity-properties) article.</span></span> 

### <a name="sql-sink-in-copy-activity"></a><span data-ttu-id="ed017-1571">Coletor do Sql na Atividade de Cópia</span><span class="sxs-lookup"><span data-stu-id="ed017-1571">Sql Sink in Copy Activity</span></span>
<span data-ttu-id="ed017-1572">Se você estiver copiando o banco de dados do SQL Server data tooa, defina Olá **tipo de coletor** de hello atividade de cópia muito**SqlSink**e especificar propriedades no Olá a seguir **coletor** seção:</span><span class="sxs-lookup"><span data-stu-id="ed017-1572">If you are copying data tooa SQL Server database, set hello **sink type** of hello copy activity too**SqlSink**, and specify following properties in hello **sink** section:</span></span>

| <span data-ttu-id="ed017-1573">Propriedade</span><span class="sxs-lookup"><span data-stu-id="ed017-1573">Property</span></span> | <span data-ttu-id="ed017-1574">Descrição</span><span class="sxs-lookup"><span data-stu-id="ed017-1574">Description</span></span> | <span data-ttu-id="ed017-1575">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="ed017-1575">Allowed values</span></span> | <span data-ttu-id="ed017-1576">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="ed017-1576">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="ed017-1577">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="ed017-1577">writeBatchTimeout</span></span> |<span data-ttu-id="ed017-1578">Tempo de espera para Olá toocomplete de operação de inserção de lote antes de expirar.</span><span class="sxs-lookup"><span data-stu-id="ed017-1578">Wait time for hello batch insert operation toocomplete before it times out.</span></span> |<span data-ttu-id="ed017-1579">timespan</span><span class="sxs-lookup"><span data-stu-id="ed017-1579">timespan</span></span><br/><br/> <span data-ttu-id="ed017-1580">Exemplo: "00:30:00" (30 minutos).</span><span class="sxs-lookup"><span data-stu-id="ed017-1580">Example: “00:30:00” (30 minutes).</span></span> |<span data-ttu-id="ed017-1581">Não</span><span class="sxs-lookup"><span data-stu-id="ed017-1581">No</span></span> |
| <span data-ttu-id="ed017-1582">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="ed017-1582">writeBatchSize</span></span> |<span data-ttu-id="ed017-1583">Insere dados na tabela do SQL hello quando o tamanho do buffer de saudação atingir writeBatchSize.</span><span class="sxs-lookup"><span data-stu-id="ed017-1583">Inserts data into hello SQL table when hello buffer size reaches writeBatchSize.</span></span> |<span data-ttu-id="ed017-1584">Inteiro (número de linhas)</span><span class="sxs-lookup"><span data-stu-id="ed017-1584">Integer (number of rows)</span></span> |<span data-ttu-id="ed017-1585">Não (padrão: 10000)</span><span class="sxs-lookup"><span data-stu-id="ed017-1585">No (default: 10000)</span></span> |
| <span data-ttu-id="ed017-1586">sqlWriterCleanupScript</span><span class="sxs-lookup"><span data-stu-id="ed017-1586">sqlWriterCleanupScript</span></span> |<span data-ttu-id="ed017-1587">Especifique a consulta para a atividade de cópia tooexecute, de modo que os dados de uma fatia específica é limpa.</span><span class="sxs-lookup"><span data-stu-id="ed017-1587">Specify query for Copy Activity tooexecute such that data of a specific slice is cleaned up.</span></span> <span data-ttu-id="ed017-1588">Para saber mais, confira a seção de [repetição](#repeatability-during-copy) .</span><span class="sxs-lookup"><span data-stu-id="ed017-1588">For more information, see [repeatability](#repeatability-during-copy) section.</span></span> |<span data-ttu-id="ed017-1589">Uma instrução de consulta.</span><span class="sxs-lookup"><span data-stu-id="ed017-1589">A query statement.</span></span> |<span data-ttu-id="ed017-1590">Não</span><span class="sxs-lookup"><span data-stu-id="ed017-1590">No</span></span> |
| <span data-ttu-id="ed017-1591">sliceIdentifierColumnName</span><span class="sxs-lookup"><span data-stu-id="ed017-1591">sliceIdentifierColumnName</span></span> |<span data-ttu-id="ed017-1592">Especifique o nome de coluna para a atividade de cópia toofill com identificador de fatia gerado automaticamente, que é usado tooclean os dados de uma fatia específica quando executada novamente.</span><span class="sxs-lookup"><span data-stu-id="ed017-1592">Specify column name for Copy Activity toofill with auto generated slice identifier, which is used tooclean up data of a specific slice when rerun.</span></span> <span data-ttu-id="ed017-1593">Para saber mais, confira a seção de [repetição](#repeatability-during-copy) .</span><span class="sxs-lookup"><span data-stu-id="ed017-1593">For more information, see [repeatability](#repeatability-during-copy) section.</span></span> |<span data-ttu-id="ed017-1594">Nome de uma coluna com tipo de dados de binário (32).</span><span class="sxs-lookup"><span data-stu-id="ed017-1594">Column name of a column with data type of binary(32).</span></span> |<span data-ttu-id="ed017-1595">Não</span><span class="sxs-lookup"><span data-stu-id="ed017-1595">No</span></span> |
| <span data-ttu-id="ed017-1596">sqlWriterStoredProcedureName</span><span class="sxs-lookup"><span data-stu-id="ed017-1596">sqlWriterStoredProcedureName</span></span> |<span data-ttu-id="ed017-1597">Nome do hello procedimento armazenado dados upserts (atualizações/inserções) na tabela de destino de saudação.</span><span class="sxs-lookup"><span data-stu-id="ed017-1597">Name of hello stored procedure that upserts (updates/inserts) data into hello target table.</span></span> |<span data-ttu-id="ed017-1598">Nome da saudação de procedimento armazenado.</span><span class="sxs-lookup"><span data-stu-id="ed017-1598">Name of hello stored procedure.</span></span> |<span data-ttu-id="ed017-1599">Não</span><span class="sxs-lookup"><span data-stu-id="ed017-1599">No</span></span> |
| <span data-ttu-id="ed017-1600">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="ed017-1600">storedProcedureParameters</span></span> |<span data-ttu-id="ed017-1601">Parâmetros de saudação de procedimento armazenado.</span><span class="sxs-lookup"><span data-stu-id="ed017-1601">Parameters for hello stored procedure.</span></span> |<span data-ttu-id="ed017-1602">Pares de nome/valor.</span><span class="sxs-lookup"><span data-stu-id="ed017-1602">Name/value pairs.</span></span> <span data-ttu-id="ed017-1603">Nomes e o uso de maiusculas e minúsculas dos parâmetros devem corresponder a nomes de saudação e uso de maiusculas e minúsculas dos parâmetros de procedimento armazenado de saudação.</span><span class="sxs-lookup"><span data-stu-id="ed017-1603">Names and casing of parameters must match hello names and casing of hello stored procedure parameters.</span></span> |<span data-ttu-id="ed017-1604">Não</span><span class="sxs-lookup"><span data-stu-id="ed017-1604">No</span></span> |
| <span data-ttu-id="ed017-1605">sqlWriterTableType</span><span class="sxs-lookup"><span data-stu-id="ed017-1605">sqlWriterTableType</span></span> |<span data-ttu-id="ed017-1606">Especifique toobe de nome de tipo de tabela usado no procedimento armazenado de saudação.</span><span class="sxs-lookup"><span data-stu-id="ed017-1606">Specify table type name toobe used in hello stored procedure.</span></span> <span data-ttu-id="ed017-1607">Atividade de cópia disponibiliza dados Olá movidos em uma tabela temporária com esse tipo de tabela.</span><span class="sxs-lookup"><span data-stu-id="ed017-1607">Copy activity makes hello data being moved available in a temp table with this table type.</span></span> <span data-ttu-id="ed017-1608">Código do procedimento armazenado, em seguida, pode mesclar dados de saudação sejam copiados com os dados existentes.</span><span class="sxs-lookup"><span data-stu-id="ed017-1608">Stored procedure code can then merge hello data being copied with existing data.</span></span> |<span data-ttu-id="ed017-1609">Um nome de tipo de tabela.</span><span class="sxs-lookup"><span data-stu-id="ed017-1609">A table type name.</span></span> |<span data-ttu-id="ed017-1610">Não</span><span class="sxs-lookup"><span data-stu-id="ed017-1610">No</span></span> |

#### <a name="example"></a><span data-ttu-id="ed017-1611">Exemplo</span><span class="sxs-lookup"><span data-stu-id="ed017-1611">Example</span></span>
<span data-ttu-id="ed017-1612">pipeline de saudação contém uma atividade de cópia que esteja configurado toouse esses conjuntos de dados de entrada e saídos e toorun agendado a cada hora.</span><span class="sxs-lookup"><span data-stu-id="ed017-1612">hello pipeline contains a Copy Activity that is configured toouse these input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="ed017-1613">Na definição JSON de pipeline hello, Olá **fonte** tipo está definido muito**BlobSource** e **coletor** tipo está definido muito**SqlSink**.</span><span class="sxs-lookup"><span data-stu-id="ed017-1613">In hello pipeline JSON definition, hello **source** type is set too**BlobSource** and **sink** type is set too**SqlSink**.</span></span>

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

<span data-ttu-id="ed017-1614">Para obter mais informações, consulte o artigo [Conector de SQL Server](data-factory-sqlserver-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="ed017-1614">For more information, see [SQL Server connector](data-factory-sqlserver-connector.md#copy-activity-properties) article.</span></span> 

## <a name="sybase"></a><span data-ttu-id="ed017-1615">Sybase</span><span class="sxs-lookup"><span data-stu-id="ed017-1615">Sybase</span></span>

### <a name="linked-service"></a><span data-ttu-id="ed017-1616">Serviço vinculado</span><span class="sxs-lookup"><span data-stu-id="ed017-1616">Linked service</span></span>
<span data-ttu-id="ed017-1617">toodefine um Sybase vinculado serviço, Olá conjunto **tipo** de saudação serviço vinculado muito**OnPremisesSybase**e especificar propriedades no Olá a seguir **typeProperties** seção:</span><span class="sxs-lookup"><span data-stu-id="ed017-1617">toodefine a Sybase linked service, set hello **type** of hello linked service too**OnPremisesSybase**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="ed017-1618">Propriedade</span><span class="sxs-lookup"><span data-stu-id="ed017-1618">Property</span></span> | <span data-ttu-id="ed017-1619">Descrição</span><span class="sxs-lookup"><span data-stu-id="ed017-1619">Description</span></span> | <span data-ttu-id="ed017-1620">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="ed017-1620">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ed017-1621">server</span><span class="sxs-lookup"><span data-stu-id="ed017-1621">server</span></span> |<span data-ttu-id="ed017-1622">Nome do servidor do Sybase hello.</span><span class="sxs-lookup"><span data-stu-id="ed017-1622">Name of hello Sybase server.</span></span> |<span data-ttu-id="ed017-1623">Sim</span><span class="sxs-lookup"><span data-stu-id="ed017-1623">Yes</span></span> |
| <span data-ttu-id="ed017-1624">database</span><span class="sxs-lookup"><span data-stu-id="ed017-1624">database</span></span> |<span data-ttu-id="ed017-1625">Nome do banco de dados do Sybase hello.</span><span class="sxs-lookup"><span data-stu-id="ed017-1625">Name of hello Sybase database.</span></span> |<span data-ttu-id="ed017-1626">Sim</span><span class="sxs-lookup"><span data-stu-id="ed017-1626">Yes</span></span> |
| <span data-ttu-id="ed017-1627">schema</span><span class="sxs-lookup"><span data-stu-id="ed017-1627">schema</span></span> |<span data-ttu-id="ed017-1628">Nome do esquema de saudação no banco de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="ed017-1628">Name of hello schema in hello database.</span></span> |<span data-ttu-id="ed017-1629">Não</span><span class="sxs-lookup"><span data-stu-id="ed017-1629">No</span></span> |
| <span data-ttu-id="ed017-1630">authenticationType</span><span class="sxs-lookup"><span data-stu-id="ed017-1630">authenticationType</span></span> |<span data-ttu-id="ed017-1631">Tipo de autenticação usado o banco de dados do Sybase tooconnect toohello.</span><span class="sxs-lookup"><span data-stu-id="ed017-1631">Type of authentication used tooconnect toohello Sybase database.</span></span> <span data-ttu-id="ed017-1632">Os valores possíveis são: Anonymous, Basic e Windows.</span><span class="sxs-lookup"><span data-stu-id="ed017-1632">Possible values are: Anonymous, Basic, and Windows.</span></span> |<span data-ttu-id="ed017-1633">Sim</span><span class="sxs-lookup"><span data-stu-id="ed017-1633">Yes</span></span> |
| <span data-ttu-id="ed017-1634">Nome de Usuário</span><span class="sxs-lookup"><span data-stu-id="ed017-1634">username</span></span> |<span data-ttu-id="ed017-1635">Especifique o nome de usuário se você estiver usando a autenticação Basic ou Windows.</span><span class="sxs-lookup"><span data-stu-id="ed017-1635">Specify user name if you are using Basic or Windows authentication.</span></span> |<span data-ttu-id="ed017-1636">Não</span><span class="sxs-lookup"><span data-stu-id="ed017-1636">No</span></span> |
| <span data-ttu-id="ed017-1637">Senha</span><span class="sxs-lookup"><span data-stu-id="ed017-1637">password</span></span> |<span data-ttu-id="ed017-1638">Especifique a senha da conta de usuário de saudação especificado para nome de usuário de saudação.</span><span class="sxs-lookup"><span data-stu-id="ed017-1638">Specify password for hello user account you specified for hello username.</span></span> |<span data-ttu-id="ed017-1639">Não</span><span class="sxs-lookup"><span data-stu-id="ed017-1639">No</span></span> |
| <span data-ttu-id="ed017-1640">gatewayName</span><span class="sxs-lookup"><span data-stu-id="ed017-1640">gatewayName</span></span> |<span data-ttu-id="ed017-1641">Nome do gateway Olá Olá serviço da fábrica de dados deve usar o banco de dados Sybase local de toohello de tooconnect.</span><span class="sxs-lookup"><span data-stu-id="ed017-1641">Name of hello gateway that hello Data Factory service should use tooconnect toohello on-premises Sybase database.</span></span> |<span data-ttu-id="ed017-1642">Sim</span><span class="sxs-lookup"><span data-stu-id="ed017-1642">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="ed017-1643">Exemplo</span><span class="sxs-lookup"><span data-stu-id="ed017-1643">Example</span></span>
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

<span data-ttu-id="ed017-1644">Para obter mais informações, consulte o artigo [Conector do Sybase](data-factory-onprem-sybase-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="ed017-1644">For more information, see [Sybase connector](data-factory-onprem-sybase-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="ed017-1645">Conjunto de dados</span><span class="sxs-lookup"><span data-stu-id="ed017-1645">Dataset</span></span>
<span data-ttu-id="ed017-1646">toodefine um conjunto de dados Sybase, Olá conjunto **tipo** do conjunto de dados de saudação muito**RelationalTable**e especifique Olá seguintes propriedades em Olá **typeProperties** seção:</span><span class="sxs-lookup"><span data-stu-id="ed017-1646">toodefine a Sybase dataset, set hello **type** of hello dataset too**RelationalTable**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="ed017-1647">Propriedade</span><span class="sxs-lookup"><span data-stu-id="ed017-1647">Property</span></span> | <span data-ttu-id="ed017-1648">Descrição</span><span class="sxs-lookup"><span data-stu-id="ed017-1648">Description</span></span> | <span data-ttu-id="ed017-1649">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="ed017-1649">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ed017-1650">tableName</span><span class="sxs-lookup"><span data-stu-id="ed017-1650">tableName</span></span> |<span data-ttu-id="ed017-1651">Nome da tabela de saudação em Olá instância de banco de dados Sybase serviço vinculado refere-se a.</span><span class="sxs-lookup"><span data-stu-id="ed017-1651">Name of hello table in hello Sybase Database instance that linked service refers to.</span></span> |<span data-ttu-id="ed017-1652">Não (se **query** de **RelationalSource** for especificado)</span><span class="sxs-lookup"><span data-stu-id="ed017-1652">No (if **query** of **RelationalSource** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="ed017-1653">Exemplo</span><span class="sxs-lookup"><span data-stu-id="ed017-1653">Example</span></span>

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

<span data-ttu-id="ed017-1654">Para obter mais informações, consulte o artigo [Conector do Sybase](data-factory-onprem-sybase-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="ed017-1654">For more information, see [Sybase connector](data-factory-onprem-sybase-connector.md#dataset-properties) article.</span></span> 

### <a name="relational-source-in-copy-activity"></a><span data-ttu-id="ed017-1655">Origem Relacional na Atividade de Cópia</span><span class="sxs-lookup"><span data-stu-id="ed017-1655">Relational Source in Copy Activity</span></span>
<span data-ttu-id="ed017-1656">Se você estiver copiando dados de um banco de dados Sybase, defina Olá **tipo de fonte** de hello atividade de cópia muito**RelationalSource**e especificar propriedades no Olá a seguir **fonte** seção:</span><span class="sxs-lookup"><span data-stu-id="ed017-1656">If you are copying data from a Sybase database, set hello **source type** of hello copy activity too**RelationalSource**, and specify following properties in hello **source** section:</span></span>


| <span data-ttu-id="ed017-1657">Propriedade</span><span class="sxs-lookup"><span data-stu-id="ed017-1657">Property</span></span> | <span data-ttu-id="ed017-1658">Descrição</span><span class="sxs-lookup"><span data-stu-id="ed017-1658">Description</span></span> | <span data-ttu-id="ed017-1659">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="ed017-1659">Allowed values</span></span> | <span data-ttu-id="ed017-1660">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="ed017-1660">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="ed017-1661">query</span><span class="sxs-lookup"><span data-stu-id="ed017-1661">query</span></span> |<span data-ttu-id="ed017-1662">Use dados de tooread Olá consulta personalizada.</span><span class="sxs-lookup"><span data-stu-id="ed017-1662">Use hello custom query tooread data.</span></span> |<span data-ttu-id="ed017-1663">Cadeia de caracteres de consulta SQL.</span><span class="sxs-lookup"><span data-stu-id="ed017-1663">SQL query string.</span></span> <span data-ttu-id="ed017-1664">Por exemplo: `select * from MyTable`.</span><span class="sxs-lookup"><span data-stu-id="ed017-1664">For example: `select * from MyTable`.</span></span> |<span data-ttu-id="ed017-1665">Não (se **tableName** de **dataset** for especificado)</span><span class="sxs-lookup"><span data-stu-id="ed017-1665">No (if **tableName** of **dataset** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="ed017-1666">Exemplo</span><span class="sxs-lookup"><span data-stu-id="ed017-1666">Example</span></span>

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

<span data-ttu-id="ed017-1667">Para obter mais informações, consulte o artigo [Conector do Sybase](data-factory-onprem-sybase-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="ed017-1667">For more information, see [Sybase connector](data-factory-onprem-sybase-connector.md#copy-activity-properties) article.</span></span>

## <a name="teradata"></a><span data-ttu-id="ed017-1668">Teradata</span><span class="sxs-lookup"><span data-stu-id="ed017-1668">Teradata</span></span>

### <a name="linked-service"></a><span data-ttu-id="ed017-1669">Serviço vinculado</span><span class="sxs-lookup"><span data-stu-id="ed017-1669">Linked service</span></span>
<span data-ttu-id="ed017-1670">toodefine um Teradata vinculado serviço, Olá conjunto **tipo** de saudação serviço vinculado muito**OnPremisesTeradata**e especificar propriedades no Olá a seguir **typeProperties** seção:</span><span class="sxs-lookup"><span data-stu-id="ed017-1670">toodefine a Teradata linked service, set hello **type** of hello linked service too**OnPremisesTeradata**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="ed017-1671">Propriedade</span><span class="sxs-lookup"><span data-stu-id="ed017-1671">Property</span></span> | <span data-ttu-id="ed017-1672">Descrição</span><span class="sxs-lookup"><span data-stu-id="ed017-1672">Description</span></span> | <span data-ttu-id="ed017-1673">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="ed017-1673">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ed017-1674">server</span><span class="sxs-lookup"><span data-stu-id="ed017-1674">server</span></span> |<span data-ttu-id="ed017-1675">Nome do servidor de Teradata hello.</span><span class="sxs-lookup"><span data-stu-id="ed017-1675">Name of hello Teradata server.</span></span> |<span data-ttu-id="ed017-1676">Sim</span><span class="sxs-lookup"><span data-stu-id="ed017-1676">Yes</span></span> |
| <span data-ttu-id="ed017-1677">authenticationType</span><span class="sxs-lookup"><span data-stu-id="ed017-1677">authenticationType</span></span> |<span data-ttu-id="ed017-1678">Tipo de autenticação usado o banco de dados do tooconnect toohello Teradata.</span><span class="sxs-lookup"><span data-stu-id="ed017-1678">Type of authentication used tooconnect toohello Teradata database.</span></span> <span data-ttu-id="ed017-1679">Os valores possíveis são: Anonymous, Basic e Windows.</span><span class="sxs-lookup"><span data-stu-id="ed017-1679">Possible values are: Anonymous, Basic, and Windows.</span></span> |<span data-ttu-id="ed017-1680">Sim</span><span class="sxs-lookup"><span data-stu-id="ed017-1680">Yes</span></span> |
| <span data-ttu-id="ed017-1681">Nome de Usuário</span><span class="sxs-lookup"><span data-stu-id="ed017-1681">username</span></span> |<span data-ttu-id="ed017-1682">Especifique o nome de usuário se você estiver usando a autenticação Basic ou Windows.</span><span class="sxs-lookup"><span data-stu-id="ed017-1682">Specify user name if you are using Basic or Windows authentication.</span></span> |<span data-ttu-id="ed017-1683">Não</span><span class="sxs-lookup"><span data-stu-id="ed017-1683">No</span></span> |
| <span data-ttu-id="ed017-1684">Senha</span><span class="sxs-lookup"><span data-stu-id="ed017-1684">password</span></span> |<span data-ttu-id="ed017-1685">Especifique a senha da conta de usuário de saudação especificado para nome de usuário de saudação.</span><span class="sxs-lookup"><span data-stu-id="ed017-1685">Specify password for hello user account you specified for hello username.</span></span> |<span data-ttu-id="ed017-1686">Não</span><span class="sxs-lookup"><span data-stu-id="ed017-1686">No</span></span> |
| <span data-ttu-id="ed017-1687">gatewayName</span><span class="sxs-lookup"><span data-stu-id="ed017-1687">gatewayName</span></span> |<span data-ttu-id="ed017-1688">Nome do gateway Olá Olá serviço da fábrica de dados deve usar o banco de dados do tooconnect toohello local Teradata.</span><span class="sxs-lookup"><span data-stu-id="ed017-1688">Name of hello gateway that hello Data Factory service should use tooconnect toohello on-premises Teradata database.</span></span> |<span data-ttu-id="ed017-1689">Sim</span><span class="sxs-lookup"><span data-stu-id="ed017-1689">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="ed017-1690">Exemplo</span><span class="sxs-lookup"><span data-stu-id="ed017-1690">Example</span></span>
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

<span data-ttu-id="ed017-1691">Para obter mais informações, consulte o artigo [Conector do Teradata](data-factory-onprem-teradata-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="ed017-1691">For more information, see [Teradata connector](data-factory-onprem-teradata-connector.md#linked-service-properties) article.</span></span>

### <a name="dataset"></a><span data-ttu-id="ed017-1692">Conjunto de dados</span><span class="sxs-lookup"><span data-stu-id="ed017-1692">Dataset</span></span>
<span data-ttu-id="ed017-1693">toodefine um conjunto de dados de Teradata Blob, Olá conjunto **tipo** do conjunto de dados de saudação muito**RelationalTable**.</span><span class="sxs-lookup"><span data-stu-id="ed017-1693">toodefine a Teradata Blob dataset, set hello **type** of hello dataset too**RelationalTable**.</span></span> <span data-ttu-id="ed017-1694">No momento, não há nenhuma propriedade de tipo com suporte para o conjunto de dados de Teradata hello.</span><span class="sxs-lookup"><span data-stu-id="ed017-1694">Currently, there are no type properties supported for hello Teradata dataset.</span></span> 

#### <a name="example"></a><span data-ttu-id="ed017-1695">Exemplo</span><span class="sxs-lookup"><span data-stu-id="ed017-1695">Example</span></span>
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

<span data-ttu-id="ed017-1696">Para obter mais informações, consulte o artigo [Conector do Teradata](data-factory-onprem-teradata-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="ed017-1696">For more information, see [Teradata connector](data-factory-onprem-teradata-connector.md#dataset-properties) article.</span></span>

### <a name="relational-source-in-copy-activity"></a><span data-ttu-id="ed017-1697">Origem Relacional na Atividade de Cópia</span><span class="sxs-lookup"><span data-stu-id="ed017-1697">Relational Source in Copy Activity</span></span>
<span data-ttu-id="ed017-1698">Se você estiver copiando dados de um banco de dados Teradata, defina Olá **tipo de fonte** de hello atividade de cópia muito**RelationalSource**e especificar propriedades no Olá a seguir **fonte**seção:</span><span class="sxs-lookup"><span data-stu-id="ed017-1698">If you are copying data from a Teradata database, set hello **source type** of hello copy activity too**RelationalSource**, and specify following properties in hello **source** section:</span></span>

| <span data-ttu-id="ed017-1699">Propriedade</span><span class="sxs-lookup"><span data-stu-id="ed017-1699">Property</span></span> | <span data-ttu-id="ed017-1700">Descrição</span><span class="sxs-lookup"><span data-stu-id="ed017-1700">Description</span></span> | <span data-ttu-id="ed017-1701">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="ed017-1701">Allowed values</span></span> | <span data-ttu-id="ed017-1702">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="ed017-1702">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="ed017-1703">query</span><span class="sxs-lookup"><span data-stu-id="ed017-1703">query</span></span> |<span data-ttu-id="ed017-1704">Use dados de tooread Olá consulta personalizada.</span><span class="sxs-lookup"><span data-stu-id="ed017-1704">Use hello custom query tooread data.</span></span> |<span data-ttu-id="ed017-1705">Cadeia de caracteres de consulta SQL.</span><span class="sxs-lookup"><span data-stu-id="ed017-1705">SQL query string.</span></span> <span data-ttu-id="ed017-1706">Por exemplo: `select * from MyTable`.</span><span class="sxs-lookup"><span data-stu-id="ed017-1706">For example: `select * from MyTable`.</span></span> |<span data-ttu-id="ed017-1707">Sim</span><span class="sxs-lookup"><span data-stu-id="ed017-1707">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="ed017-1708">Exemplo</span><span class="sxs-lookup"><span data-stu-id="ed017-1708">Example</span></span>

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

<span data-ttu-id="ed017-1709">Para obter mais informações, consulte o artigo [Conector do Teradata](data-factory-onprem-teradata-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="ed017-1709">For more information, see [Teradata connector](data-factory-onprem-teradata-connector.md#copy-activity-properties) article.</span></span>

## <a name="cassandra"></a><span data-ttu-id="ed017-1710">Cassandra</span><span class="sxs-lookup"><span data-stu-id="ed017-1710">Cassandra</span></span>


### <a name="linked-service"></a><span data-ttu-id="ed017-1711">Serviço vinculado</span><span class="sxs-lookup"><span data-stu-id="ed017-1711">Linked service</span></span>
<span data-ttu-id="ed017-1712">toodefine um Cassandra vinculado serviço, Olá conjunto **tipo** de saudação serviço vinculado muito**OnPremisesCassandra**e especificar propriedades no Olá a seguir **typeProperties** seção:</span><span class="sxs-lookup"><span data-stu-id="ed017-1712">toodefine a Cassandra linked service, set hello **type** of hello linked service too**OnPremisesCassandra**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="ed017-1713">Propriedade</span><span class="sxs-lookup"><span data-stu-id="ed017-1713">Property</span></span> | <span data-ttu-id="ed017-1714">Descrição</span><span class="sxs-lookup"><span data-stu-id="ed017-1714">Description</span></span> | <span data-ttu-id="ed017-1715">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="ed017-1715">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ed017-1716">host</span><span class="sxs-lookup"><span data-stu-id="ed017-1716">host</span></span> |<span data-ttu-id="ed017-1717">Um ou mais endereços IP ou nomes de host dos servidores Cassandra.</span><span class="sxs-lookup"><span data-stu-id="ed017-1717">One or more IP addresses or host names of Cassandra servers.</span></span><br/><br/><span data-ttu-id="ed017-1718">Especifique uma lista separada por vírgulas de endereços IP ou host nomes tooconnect tooall servidores simultaneamente.</span><span class="sxs-lookup"><span data-stu-id="ed017-1718">Specify a comma-separated list of IP addresses or host names tooconnect tooall servers concurrently.</span></span> |<span data-ttu-id="ed017-1719">Sim</span><span class="sxs-lookup"><span data-stu-id="ed017-1719">Yes</span></span> |
| <span data-ttu-id="ed017-1720">porta</span><span class="sxs-lookup"><span data-stu-id="ed017-1720">port</span></span> |<span data-ttu-id="ed017-1721">Olá porta TCP que Olá servidor Cassandra usa toolisten para conexões de cliente.</span><span class="sxs-lookup"><span data-stu-id="ed017-1721">hello TCP port that hello Cassandra server uses toolisten for client connections.</span></span> |<span data-ttu-id="ed017-1722">Não, valor padrão: 9042</span><span class="sxs-lookup"><span data-stu-id="ed017-1722">No, default value: 9042</span></span> |
| <span data-ttu-id="ed017-1723">authenticationType</span><span class="sxs-lookup"><span data-stu-id="ed017-1723">authenticationType</span></span> |<span data-ttu-id="ed017-1724">Básica, ou Anônima</span><span class="sxs-lookup"><span data-stu-id="ed017-1724">Basic, or Anonymous</span></span> |<span data-ttu-id="ed017-1725">Sim</span><span class="sxs-lookup"><span data-stu-id="ed017-1725">Yes</span></span> |
| <span data-ttu-id="ed017-1726">Nome de Usuário</span><span class="sxs-lookup"><span data-stu-id="ed017-1726">username</span></span> |<span data-ttu-id="ed017-1727">Especifique o nome de usuário para a conta de usuário de saudação.</span><span class="sxs-lookup"><span data-stu-id="ed017-1727">Specify user name for hello user account.</span></span> |<span data-ttu-id="ed017-1728">Sim, se authenticationType é definido tooBasic.</span><span class="sxs-lookup"><span data-stu-id="ed017-1728">Yes, if authenticationType is set tooBasic.</span></span> |
| <span data-ttu-id="ed017-1729">Senha</span><span class="sxs-lookup"><span data-stu-id="ed017-1729">password</span></span> |<span data-ttu-id="ed017-1730">Especifique a senha da conta de usuário de saudação.</span><span class="sxs-lookup"><span data-stu-id="ed017-1730">Specify password for hello user account.</span></span> |<span data-ttu-id="ed017-1731">Sim, se authenticationType é definido tooBasic.</span><span class="sxs-lookup"><span data-stu-id="ed017-1731">Yes, if authenticationType is set tooBasic.</span></span> |
| <span data-ttu-id="ed017-1732">gatewayName</span><span class="sxs-lookup"><span data-stu-id="ed017-1732">gatewayName</span></span> |<span data-ttu-id="ed017-1733">nome de saudação do gateway de saudação que é usado tooconnect toohello Cassandra banco de dados no local.</span><span class="sxs-lookup"><span data-stu-id="ed017-1733">hello name of hello gateway that is used tooconnect toohello on-premises Cassandra database.</span></span> |<span data-ttu-id="ed017-1734">Sim</span><span class="sxs-lookup"><span data-stu-id="ed017-1734">Yes</span></span> |
| <span data-ttu-id="ed017-1735">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="ed017-1735">encryptedCredential</span></span> |<span data-ttu-id="ed017-1736">Credencial criptografada pelo gateway hello.</span><span class="sxs-lookup"><span data-stu-id="ed017-1736">Credential encrypted by hello gateway.</span></span> |<span data-ttu-id="ed017-1737">Não</span><span class="sxs-lookup"><span data-stu-id="ed017-1737">No</span></span> |

#### <a name="example"></a><span data-ttu-id="ed017-1738">Exemplo</span><span class="sxs-lookup"><span data-stu-id="ed017-1738">Example</span></span>

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

<span data-ttu-id="ed017-1739">Para obter mais informações, consulte o artigo [Conector do Cassandra](data-factory-onprem-cassandra-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="ed017-1739">For more information, see [Cassandra connector](data-factory-onprem-cassandra-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="ed017-1740">Conjunto de dados</span><span class="sxs-lookup"><span data-stu-id="ed017-1740">Dataset</span></span>
<span data-ttu-id="ed017-1741">toodefine um conjunto de dados Cassandra, Olá conjunto **tipo** do conjunto de dados de saudação muito**CassandraTable**e especifique Olá seguintes propriedades em Olá **typeProperties** seção:</span><span class="sxs-lookup"><span data-stu-id="ed017-1741">toodefine a Cassandra dataset, set hello **type** of hello dataset too**CassandraTable**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="ed017-1742">Propriedade</span><span class="sxs-lookup"><span data-stu-id="ed017-1742">Property</span></span> | <span data-ttu-id="ed017-1743">Descrição</span><span class="sxs-lookup"><span data-stu-id="ed017-1743">Description</span></span> | <span data-ttu-id="ed017-1744">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="ed017-1744">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ed017-1745">keyspace</span><span class="sxs-lookup"><span data-stu-id="ed017-1745">keyspace</span></span> |<span data-ttu-id="ed017-1746">Nome da saudação keyspace ou esquema Cassandra banco de dados.</span><span class="sxs-lookup"><span data-stu-id="ed017-1746">Name of hello keyspace or schema in Cassandra database.</span></span> |<span data-ttu-id="ed017-1747">Sim (se a **consulta** para **CassandraSource** não estiver definida).</span><span class="sxs-lookup"><span data-stu-id="ed017-1747">Yes (If **query** for **CassandraSource** is not defined).</span></span> |
| <span data-ttu-id="ed017-1748">tableName</span><span class="sxs-lookup"><span data-stu-id="ed017-1748">tableName</span></span> |<span data-ttu-id="ed017-1749">Nome da tabela de saudação no banco de dados Cassandra.</span><span class="sxs-lookup"><span data-stu-id="ed017-1749">Name of hello table in Cassandra database.</span></span> |<span data-ttu-id="ed017-1750">Sim (se a **consulta** para **CassandraSource** não estiver definida).</span><span class="sxs-lookup"><span data-stu-id="ed017-1750">Yes (If **query** for **CassandraSource** is not defined).</span></span> |

#### <a name="example"></a><span data-ttu-id="ed017-1751">Exemplo</span><span class="sxs-lookup"><span data-stu-id="ed017-1751">Example</span></span>

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

<span data-ttu-id="ed017-1752">Para obter mais informações, consulte o artigo [Conector do Cassandra](data-factory-onprem-cassandra-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="ed017-1752">For more information, see [Cassandra connector](data-factory-onprem-cassandra-connector.md#dataset-properties) article.</span></span> 

### <a name="cassandra-source-in-copy-activity"></a><span data-ttu-id="ed017-1753">Origem do Cassandra na Atividade de Cópia</span><span class="sxs-lookup"><span data-stu-id="ed017-1753">Cassandra Source in Copy Activity</span></span>
<span data-ttu-id="ed017-1754">Se você estiver copiando dados de Cassandra, defina Olá **tipo de fonte** de hello atividade de cópia muito**CassandraSource**e especificar propriedades no Olá a seguir **fonte** seção :</span><span class="sxs-lookup"><span data-stu-id="ed017-1754">If you are copying data from Cassandra, set hello **source type** of hello copy activity too**CassandraSource**, and specify following properties in hello **source** section:</span></span>

| <span data-ttu-id="ed017-1755">Propriedade</span><span class="sxs-lookup"><span data-stu-id="ed017-1755">Property</span></span> | <span data-ttu-id="ed017-1756">Descrição</span><span class="sxs-lookup"><span data-stu-id="ed017-1756">Description</span></span> | <span data-ttu-id="ed017-1757">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="ed017-1757">Allowed values</span></span> | <span data-ttu-id="ed017-1758">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="ed017-1758">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="ed017-1759">query</span><span class="sxs-lookup"><span data-stu-id="ed017-1759">query</span></span> |<span data-ttu-id="ed017-1760">Use dados de tooread Olá consulta personalizada.</span><span class="sxs-lookup"><span data-stu-id="ed017-1760">Use hello custom query tooread data.</span></span> |<span data-ttu-id="ed017-1761">Consulta SQL-92 ou consulta CQL.</span><span class="sxs-lookup"><span data-stu-id="ed017-1761">SQL-92 query or CQL query.</span></span> <span data-ttu-id="ed017-1762">Veja [Referência ao CQL](https://docs.datastax.com/en/cql/3.1/cql/cql_reference/cqlReferenceTOC.html).</span><span class="sxs-lookup"><span data-stu-id="ed017-1762">See [CQL reference](https://docs.datastax.com/en/cql/3.1/cql/cql_reference/cqlReferenceTOC.html).</span></span> <br/><br/><span data-ttu-id="ed017-1763">Ao usar a consulta SQL, especifique **keyspace name.table nome** toorepresent Olá tabela tooquery.</span><span class="sxs-lookup"><span data-stu-id="ed017-1763">When using SQL query, specify **keyspace name.table name** toorepresent hello table you want tooquery.</span></span> |<span data-ttu-id="ed017-1764">Não (se tableName e keyspace no conjunto de dados estiverem definidos).</span><span class="sxs-lookup"><span data-stu-id="ed017-1764">No (if tableName and keyspace on dataset are defined).</span></span> |
| <span data-ttu-id="ed017-1765">consistencyLevel</span><span class="sxs-lookup"><span data-stu-id="ed017-1765">consistencyLevel</span></span> |<span data-ttu-id="ed017-1766">nível de consistência de saudação especifica quantas réplicas deve responder a solicitação de leitura de tooa antes de retornar o aplicativo de cliente de toohello de dados.</span><span class="sxs-lookup"><span data-stu-id="ed017-1766">hello consistency level specifies how many replicas must respond tooa read request before returning data toohello client application.</span></span> <span data-ttu-id="ed017-1767">Verificações de Cassandra Olá número especificado de réplicas para a solicitação de leitura de saudação do toosatisfy de dados.</span><span class="sxs-lookup"><span data-stu-id="ed017-1767">Cassandra checks hello specified number of replicas for data toosatisfy hello read request.</span></span> |<span data-ttu-id="ed017-1768">ONE, TWO, THREE, QUORUM, ALL, LOCAL_QUORUM, EACH_QUORUM, LOCAL_ONE.</span><span class="sxs-lookup"><span data-stu-id="ed017-1768">ONE, TWO, THREE, QUORUM, ALL, LOCAL_QUORUM, EACH_QUORUM, LOCAL_ONE.</span></span> <span data-ttu-id="ed017-1769">Confira [Configuring data consistency (Configurando a consistência de dados)](http://docs.datastax.com/en//cassandra/2.0/cassandra/dml/dml_config_consistency_c.html) para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="ed017-1769">See [Configuring data consistency](http://docs.datastax.com/en//cassandra/2.0/cassandra/dml/dml_config_consistency_c.html) for details.</span></span> |<span data-ttu-id="ed017-1770">Não.</span><span class="sxs-lookup"><span data-stu-id="ed017-1770">No.</span></span> <span data-ttu-id="ed017-1771">O valor padrão é ONE.</span><span class="sxs-lookup"><span data-stu-id="ed017-1771">Default value is ONE.</span></span> |

#### <a name="example"></a><span data-ttu-id="ed017-1772">Exemplo</span><span class="sxs-lookup"><span data-stu-id="ed017-1772">Example</span></span>
  
```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "CassandraToAzureBlob",
            "description": "Copy from Cassandra tooan Azure blob",
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

<span data-ttu-id="ed017-1773">Para obter mais informações, consulte o artigo [Conector do Cassandra](data-factory-onprem-cassandra-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="ed017-1773">For more information, see [Cassandra connector](data-factory-onprem-cassandra-connector.md#copy-activity-properties) article.</span></span>

## <a name="mongodb"></a><span data-ttu-id="ed017-1774">MongoDB</span><span class="sxs-lookup"><span data-stu-id="ed017-1774">MongoDB</span></span>

### <a name="linked-service"></a><span data-ttu-id="ed017-1775">Serviço vinculado</span><span class="sxs-lookup"><span data-stu-id="ed017-1775">Linked service</span></span>
<span data-ttu-id="ed017-1776">toodefine um MongoDB vinculado serviço, Olá conjunto **tipo** de saudação serviço vinculado muito**OnPremisesMongoDB**e especificar propriedades no Olá a seguir **typeProperties** seção:</span><span class="sxs-lookup"><span data-stu-id="ed017-1776">toodefine a MongoDB linked service, set hello **type** of hello linked service too**OnPremisesMongoDB**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="ed017-1777">Propriedade</span><span class="sxs-lookup"><span data-stu-id="ed017-1777">Property</span></span> | <span data-ttu-id="ed017-1778">Descrição</span><span class="sxs-lookup"><span data-stu-id="ed017-1778">Description</span></span> | <span data-ttu-id="ed017-1779">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="ed017-1779">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ed017-1780">server</span><span class="sxs-lookup"><span data-stu-id="ed017-1780">server</span></span> |<span data-ttu-id="ed017-1781">IP endereço ou nome de host do servidor do MongoDB hello.</span><span class="sxs-lookup"><span data-stu-id="ed017-1781">IP address or host name of hello MongoDB server.</span></span> |<span data-ttu-id="ed017-1782">Sim</span><span class="sxs-lookup"><span data-stu-id="ed017-1782">Yes</span></span> |
| <span data-ttu-id="ed017-1783">porta</span><span class="sxs-lookup"><span data-stu-id="ed017-1783">port</span></span> |<span data-ttu-id="ed017-1784">Porta TCP que Olá MongoDB server usa toolisten para conexões de cliente.</span><span class="sxs-lookup"><span data-stu-id="ed017-1784">TCP port that hello MongoDB server uses toolisten for client connections.</span></span> |<span data-ttu-id="ed017-1785">Opcional, valor padrão: 27017</span><span class="sxs-lookup"><span data-stu-id="ed017-1785">Optional, default value: 27017</span></span> |
| <span data-ttu-id="ed017-1786">authenticationType</span><span class="sxs-lookup"><span data-stu-id="ed017-1786">authenticationType</span></span> |<span data-ttu-id="ed017-1787">Básica ou Anônima.</span><span class="sxs-lookup"><span data-stu-id="ed017-1787">Basic, or Anonymous.</span></span> |<span data-ttu-id="ed017-1788">Sim</span><span class="sxs-lookup"><span data-stu-id="ed017-1788">Yes</span></span> |
| <span data-ttu-id="ed017-1789">Nome de Usuário</span><span class="sxs-lookup"><span data-stu-id="ed017-1789">username</span></span> |<span data-ttu-id="ed017-1790">Conta de usuário tooaccess MongoDB.</span><span class="sxs-lookup"><span data-stu-id="ed017-1790">User account tooaccess MongoDB.</span></span> |<span data-ttu-id="ed017-1791">Sim (se a autenticação básica for usada).</span><span class="sxs-lookup"><span data-stu-id="ed017-1791">Yes (if basic authentication is used).</span></span> |
| <span data-ttu-id="ed017-1792">Senha</span><span class="sxs-lookup"><span data-stu-id="ed017-1792">password</span></span> |<span data-ttu-id="ed017-1793">Senha do usuário hello.</span><span class="sxs-lookup"><span data-stu-id="ed017-1793">Password for hello user.</span></span> |<span data-ttu-id="ed017-1794">Sim (se a autenticação básica for usada).</span><span class="sxs-lookup"><span data-stu-id="ed017-1794">Yes (if basic authentication is used).</span></span> |
| <span data-ttu-id="ed017-1795">authSource</span><span class="sxs-lookup"><span data-stu-id="ed017-1795">authSource</span></span> |<span data-ttu-id="ed017-1796">Nome do banco de dados do MongoDB Olá que você deseja toouse toocheck suas credenciais para autenticação.</span><span class="sxs-lookup"><span data-stu-id="ed017-1796">Name of hello MongoDB database that you want toouse toocheck your credentials for authentication.</span></span> |<span data-ttu-id="ed017-1797">Opcional (se a autenticação básica for usada).</span><span class="sxs-lookup"><span data-stu-id="ed017-1797">Optional (if basic authentication is used).</span></span> <span data-ttu-id="ed017-1798">padrão: usa a conta de administrador hello e banco de dados de saudação especificado usando a propriedade databaseName.</span><span class="sxs-lookup"><span data-stu-id="ed017-1798">default: uses hello admin account and hello database specified using databaseName property.</span></span> |
| <span data-ttu-id="ed017-1799">databaseName</span><span class="sxs-lookup"><span data-stu-id="ed017-1799">databaseName</span></span> |<span data-ttu-id="ed017-1800">Nome do banco de dados do MongoDB Olá que você deseja tooaccess.</span><span class="sxs-lookup"><span data-stu-id="ed017-1800">Name of hello MongoDB database that you want tooaccess.</span></span> |<span data-ttu-id="ed017-1801">Sim</span><span class="sxs-lookup"><span data-stu-id="ed017-1801">Yes</span></span> |
| <span data-ttu-id="ed017-1802">gatewayName</span><span class="sxs-lookup"><span data-stu-id="ed017-1802">gatewayName</span></span> |<span data-ttu-id="ed017-1803">Nome do gateway de saudação que acessa o repositório de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="ed017-1803">Name of hello gateway that accesses hello data store.</span></span> |<span data-ttu-id="ed017-1804">Sim</span><span class="sxs-lookup"><span data-stu-id="ed017-1804">Yes</span></span> |
| <span data-ttu-id="ed017-1805">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="ed017-1805">encryptedCredential</span></span> |<span data-ttu-id="ed017-1806">Credencial criptografada pelo gateway.</span><span class="sxs-lookup"><span data-stu-id="ed017-1806">Credential encrypted by gateway.</span></span> |<span data-ttu-id="ed017-1807">Opcional</span><span class="sxs-lookup"><span data-stu-id="ed017-1807">Optional</span></span> |

#### <a name="example"></a><span data-ttu-id="ed017-1808">Exemplo</span><span class="sxs-lookup"><span data-stu-id="ed017-1808">Example</span></span>

```json
{
    "name": "OnPremisesMongoDbLinkedService",
    "properties": {
        "type": "OnPremisesMongoDb",
        "typeProperties": {
            "authenticationType": "<Basic or Anonymous>",
            "server": "< hello IP address or host name of hello MongoDB server >",
            "port": "<hello number of hello TCP port that hello MongoDB server uses toolisten for client connections.>",
            "username": "<username>",
            "password": "<password>",
            "authSource": "< hello database that you want toouse toocheck your credentials for authentication. >",
            "databaseName": "<database name>",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

<span data-ttu-id="ed017-1809">Para obter mais informações, consulte o artigo [Conector do MongoDB](data-factory-on-premises-mongodb-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="ed017-1809">For more information, see [MongoDB connector article](data-factory-on-premises-mongodb-connector.md#linked-service-properties)</span></span>

### <a name="dataset"></a><span data-ttu-id="ed017-1810">Conjunto de dados</span><span class="sxs-lookup"><span data-stu-id="ed017-1810">Dataset</span></span>
<span data-ttu-id="ed017-1811">toodefine um conjunto de dados do MongoDB, Olá conjunto **tipo** do conjunto de dados de saudação muito**MongoDbCollection**e especifique Olá seguintes propriedades em Olá **typeProperties** seção:</span><span class="sxs-lookup"><span data-stu-id="ed017-1811">toodefine a MongoDB dataset, set hello **type** of hello dataset too**MongoDbCollection**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="ed017-1812">Propriedade</span><span class="sxs-lookup"><span data-stu-id="ed017-1812">Property</span></span> | <span data-ttu-id="ed017-1813">Descrição</span><span class="sxs-lookup"><span data-stu-id="ed017-1813">Description</span></span> | <span data-ttu-id="ed017-1814">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="ed017-1814">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ed017-1815">collectionName</span><span class="sxs-lookup"><span data-stu-id="ed017-1815">collectionName</span></span> |<span data-ttu-id="ed017-1816">Nome da coleção de saudação no banco de dados do MongoDB.</span><span class="sxs-lookup"><span data-stu-id="ed017-1816">Name of hello collection in MongoDB database.</span></span> |<span data-ttu-id="ed017-1817">Sim</span><span class="sxs-lookup"><span data-stu-id="ed017-1817">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="ed017-1818">Exemplo</span><span class="sxs-lookup"><span data-stu-id="ed017-1818">Example</span></span>

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

<span data-ttu-id="ed017-1819">Para obter mais informações, consulte o artigo [Conector do MongoDB](data-factory-on-premises-mongodb-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="ed017-1819">For more information, see [MongoDB connector article](data-factory-on-premises-mongodb-connector.md#dataset-properties)</span></span>

#### <a name="mongodb-source-in-copy-activity"></a><span data-ttu-id="ed017-1820">Origem do MongoDB na Atividade de Cópia</span><span class="sxs-lookup"><span data-stu-id="ed017-1820">MongoDB Source in Copy Activity</span></span>
<span data-ttu-id="ed017-1821">Se você estiver copiando dados do MongoDB, defina Olá **tipo de fonte** de hello atividade de cópia muito**MongoDbSource**e especificar propriedades no Olá a seguir **fonte** seção:</span><span class="sxs-lookup"><span data-stu-id="ed017-1821">If you are copying data from MongoDB, set hello **source type** of hello copy activity too**MongoDbSource**, and specify following properties in hello **source** section:</span></span>

| <span data-ttu-id="ed017-1822">Propriedade</span><span class="sxs-lookup"><span data-stu-id="ed017-1822">Property</span></span> | <span data-ttu-id="ed017-1823">Descrição</span><span class="sxs-lookup"><span data-stu-id="ed017-1823">Description</span></span> | <span data-ttu-id="ed017-1824">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="ed017-1824">Allowed values</span></span> | <span data-ttu-id="ed017-1825">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="ed017-1825">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="ed017-1826">query</span><span class="sxs-lookup"><span data-stu-id="ed017-1826">query</span></span> |<span data-ttu-id="ed017-1827">Use dados de tooread Olá consulta personalizada.</span><span class="sxs-lookup"><span data-stu-id="ed017-1827">Use hello custom query tooread data.</span></span> |<span data-ttu-id="ed017-1828">Cadeia de consulta SQL-92.</span><span class="sxs-lookup"><span data-stu-id="ed017-1828">SQL-92 query string.</span></span> <span data-ttu-id="ed017-1829">Por exemplo: `select * from MyTable`.</span><span class="sxs-lookup"><span data-stu-id="ed017-1829">For example: `select * from MyTable`.</span></span> |<span data-ttu-id="ed017-1830">Não (se **collectionName** de **dataset** for especificado)</span><span class="sxs-lookup"><span data-stu-id="ed017-1830">No (if **collectionName** of **dataset** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="ed017-1831">Exemplo</span><span class="sxs-lookup"><span data-stu-id="ed017-1831">Example</span></span>

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

<span data-ttu-id="ed017-1832">Para obter mais informações, consulte o artigo [Conector do MongoDB](data-factory-on-premises-mongodb-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="ed017-1832">For more information, see [MongoDB connector article](data-factory-on-premises-mongodb-connector.md#copy-activity-properties)</span></span>

## <a name="amazon-s3"></a><span data-ttu-id="ed017-1833">Amazon S3</span><span class="sxs-lookup"><span data-stu-id="ed017-1833">Amazon S3</span></span>


### <a name="linked-service"></a><span data-ttu-id="ed017-1834">Serviço vinculado</span><span class="sxs-lookup"><span data-stu-id="ed017-1834">Linked service</span></span>
<span data-ttu-id="ed017-1835">toodefine um S3 Amazon vinculado serviço, Olá conjunto **tipo** de saudação serviço vinculado muito**AwsAccessKey**e especificar propriedades no Olá a seguir **typeProperties** seção :</span><span class="sxs-lookup"><span data-stu-id="ed017-1835">toodefine an Amazon S3 linked service, set hello **type** of hello linked service too**AwsAccessKey**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="ed017-1836">Propriedade</span><span class="sxs-lookup"><span data-stu-id="ed017-1836">Property</span></span> | <span data-ttu-id="ed017-1837">Descrição</span><span class="sxs-lookup"><span data-stu-id="ed017-1837">Description</span></span> | <span data-ttu-id="ed017-1838">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="ed017-1838">Allowed values</span></span> | <span data-ttu-id="ed017-1839">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="ed017-1839">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="ed017-1840">accessKeyID</span><span class="sxs-lookup"><span data-stu-id="ed017-1840">accessKeyID</span></span> |<span data-ttu-id="ed017-1841">ID da chave de acesso ao segredo hello.</span><span class="sxs-lookup"><span data-stu-id="ed017-1841">ID of hello secret access key.</span></span> |<span data-ttu-id="ed017-1842">string</span><span class="sxs-lookup"><span data-stu-id="ed017-1842">string</span></span> |<span data-ttu-id="ed017-1843">Sim</span><span class="sxs-lookup"><span data-stu-id="ed017-1843">Yes</span></span> |
| <span data-ttu-id="ed017-1844">secretAccessKey</span><span class="sxs-lookup"><span data-stu-id="ed017-1844">secretAccessKey</span></span> |<span data-ttu-id="ed017-1845">chave de acesso ao segredo Olá em si.</span><span class="sxs-lookup"><span data-stu-id="ed017-1845">hello secret access key itself.</span></span> |<span data-ttu-id="ed017-1846">Cadeia de caracteres secreta criptografada</span><span class="sxs-lookup"><span data-stu-id="ed017-1846">Encrypted secret string</span></span> |<span data-ttu-id="ed017-1847">Sim</span><span class="sxs-lookup"><span data-stu-id="ed017-1847">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="ed017-1848">Exemplo</span><span class="sxs-lookup"><span data-stu-id="ed017-1848">Example</span></span>
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

<span data-ttu-id="ed017-1849">Para obter mais informações, consulte o artigo [Conector do Amazon S3](data-factory-amazon-simple-storage-service-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="ed017-1849">For more information, see [Amazon S3 connector article](data-factory-amazon-simple-storage-service-connector.md#linked-service-properties).</span></span>

### <a name="dataset"></a><span data-ttu-id="ed017-1850">Conjunto de dados</span><span class="sxs-lookup"><span data-stu-id="ed017-1850">Dataset</span></span>
<span data-ttu-id="ed017-1851">toodefine um S3 Amazon o conjunto de dados, conjunto Olá **tipo** do conjunto de dados de saudação muito**AmazonS3**e especifique Olá seguintes propriedades em Olá **typeProperties** seção:</span><span class="sxs-lookup"><span data-stu-id="ed017-1851">toodefine an Amazon S3 dataset, set hello **type** of hello dataset too**AmazonS3**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="ed017-1852">Propriedade</span><span class="sxs-lookup"><span data-stu-id="ed017-1852">Property</span></span> | <span data-ttu-id="ed017-1853">Descrição</span><span class="sxs-lookup"><span data-stu-id="ed017-1853">Description</span></span> | <span data-ttu-id="ed017-1854">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="ed017-1854">Allowed values</span></span> | <span data-ttu-id="ed017-1855">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="ed017-1855">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="ed017-1856">bucketName</span><span class="sxs-lookup"><span data-stu-id="ed017-1856">bucketName</span></span> |<span data-ttu-id="ed017-1857">nome de bucket Olá S3.</span><span class="sxs-lookup"><span data-stu-id="ed017-1857">hello S3 bucket name.</span></span> |<span data-ttu-id="ed017-1858">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="ed017-1858">String</span></span> |<span data-ttu-id="ed017-1859">Sim</span><span class="sxs-lookup"><span data-stu-id="ed017-1859">Yes</span></span> |
| <span data-ttu-id="ed017-1860">chave</span><span class="sxs-lookup"><span data-stu-id="ed017-1860">key</span></span> |<span data-ttu-id="ed017-1861">chave do objeto Olá S3.</span><span class="sxs-lookup"><span data-stu-id="ed017-1861">hello S3 object key.</span></span> |<span data-ttu-id="ed017-1862">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="ed017-1862">String</span></span> |<span data-ttu-id="ed017-1863">Não</span><span class="sxs-lookup"><span data-stu-id="ed017-1863">No</span></span> |
| <span data-ttu-id="ed017-1864">prefixo</span><span class="sxs-lookup"><span data-stu-id="ed017-1864">prefix</span></span> |<span data-ttu-id="ed017-1865">Prefixo da chave do objeto Olá S3.</span><span class="sxs-lookup"><span data-stu-id="ed017-1865">Prefix for hello S3 object key.</span></span> <span data-ttu-id="ed017-1866">Objetos cujas chaves começam com esse prefixo serão selecionados.</span><span class="sxs-lookup"><span data-stu-id="ed017-1866">Objects whose keys start with this prefix are selected.</span></span> <span data-ttu-id="ed017-1867">Aplica-se apenas quando a chave está vazia.</span><span class="sxs-lookup"><span data-stu-id="ed017-1867">Applies only when key is empty.</span></span> |<span data-ttu-id="ed017-1868">string</span><span class="sxs-lookup"><span data-stu-id="ed017-1868">String</span></span> |<span data-ttu-id="ed017-1869">Não</span><span class="sxs-lookup"><span data-stu-id="ed017-1869">No</span></span> |
| <span data-ttu-id="ed017-1870">version</span><span class="sxs-lookup"><span data-stu-id="ed017-1870">version</span></span> |<span data-ttu-id="ed017-1871">versão de saudação do objeto de S3 se o controle de versão S3 estiver habilitado.</span><span class="sxs-lookup"><span data-stu-id="ed017-1871">hello version of S3 object if S3 versioning is enabled.</span></span> |<span data-ttu-id="ed017-1872">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="ed017-1872">String</span></span> |<span data-ttu-id="ed017-1873">Não</span><span class="sxs-lookup"><span data-stu-id="ed017-1873">No</span></span> |
| <span data-ttu-id="ed017-1874">formato</span><span class="sxs-lookup"><span data-stu-id="ed017-1874">format</span></span> | <span data-ttu-id="ed017-1875">Olá, tipos de formato a seguir têm suporte: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="ed017-1875">hello following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="ed017-1876">Saudação de conjunto **tipo** propriedade em formato tooone desses valores.</span><span class="sxs-lookup"><span data-stu-id="ed017-1876">Set hello **type** property under format tooone of these values.</span></span> <span data-ttu-id="ed017-1877">Para saber mais, veja as seções [Formato de texto](data-factory-supported-file-and-compression-formats.md#text-format), [Formato Json](data-factory-supported-file-and-compression-formats.md#json-format), [Formato Avro](data-factory-supported-file-and-compression-formats.md#avro-format), [Formato Orc](data-factory-supported-file-and-compression-formats.md#orc-format), e [Formato Parquet](data-factory-supported-file-and-compression-formats.md#parquet-format).</span><span class="sxs-lookup"><span data-stu-id="ed017-1877">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="ed017-1878">Se você quiser muito**copiar arquivos como-é** entre repositórios baseada em arquivo (cópia binário), ignore a seção de formato de saudação em ambas as definições de conjunto de dados de entrada e saída.</span><span class="sxs-lookup"><span data-stu-id="ed017-1878">If you want too**copy files as-is** between file-based stores (binary copy), skip hello format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="ed017-1879">Não</span><span class="sxs-lookup"><span data-stu-id="ed017-1879">No</span></span> | |
| <span data-ttu-id="ed017-1880">compactação</span><span class="sxs-lookup"><span data-stu-id="ed017-1880">compression</span></span> | <span data-ttu-id="ed017-1881">Especifica tipo de saudação e nível de compactação de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="ed017-1881">Specify hello type and level of compression for hello data.</span></span> <span data-ttu-id="ed017-1882">Os tipos com suporte são: **GZip**, **Deflate**, **BZip2** e **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="ed017-1882">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="ed017-1883">níveis de saudação com suporte são: **ideal** e **mais rápido**.</span><span class="sxs-lookup"><span data-stu-id="ed017-1883">hello supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="ed017-1884">Para saber mais, confira [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support) (Formatos de arquivo e de compactação no Azure Data Factory).</span><span class="sxs-lookup"><span data-stu-id="ed017-1884">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="ed017-1885">Não</span><span class="sxs-lookup"><span data-stu-id="ed017-1885">No</span></span> | |


> [!NOTE]
> <span data-ttu-id="ed017-1886">bucketName + chave especifica o local de saudação do objeto Olá S3 onde bucket é recipiente raiz Olá S3 objetos e a chave é Olá caminho completo tooS3 objeto.</span><span class="sxs-lookup"><span data-stu-id="ed017-1886">bucketName + key specifies hello location of hello S3 object where bucket is hello root container for S3 objects and key is hello full path tooS3 object.</span></span>

#### <a name="example-sample-dataset-with-prefix"></a><span data-ttu-id="ed017-1887">Exemplo: Conjunto de dados de exemplo com o prefixo</span><span class="sxs-lookup"><span data-stu-id="ed017-1887">Example: Sample dataset with prefix</span></span>

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
#### <a name="example-sample-data-set-with-version"></a><span data-ttu-id="ed017-1888">Exemplo: Conjunto de dados de exemplo (com a versão)</span><span class="sxs-lookup"><span data-stu-id="ed017-1888">Example: Sample data set (with version)</span></span>

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

#### <a name="example-dynamic-paths-for-s3"></a><span data-ttu-id="ed017-1889">Exemplo: Caminhos dinâmicos para S3</span><span class="sxs-lookup"><span data-stu-id="ed017-1889">Example: Dynamic paths for S3</span></span>
<span data-ttu-id="ed017-1890">Exemplo hello, usamos valores fixos para propriedades de chave e bucketName no conjunto de dados Olá Amazon S3.</span><span class="sxs-lookup"><span data-stu-id="ed017-1890">In hello sample, we use fixed values for key and bucketName properties in hello Amazon S3 dataset.</span></span>

```json
"key": "testFolder/test.orc",
"bucketName": "<S3 bucket name>",
```

<span data-ttu-id="ed017-1891">Você pode fazer com que o Data Factory calcular chave hello e bucketName dinamicamente em tempo de execução usando variáveis de sistema como SliceStart.</span><span class="sxs-lookup"><span data-stu-id="ed017-1891">You can have Data Factory calculate hello key and bucketName dynamically at runtime by using system variables such as SliceStart.</span></span>

```json
"key": "$$Text.Format('{0:MM}/{0:dd}/test.orc', SliceStart)"
"bucketName": "$$Text.Format('{0:yyyy}', SliceStart)"
```

<span data-ttu-id="ed017-1892">Você pode fazer Olá mesmo para a propriedade de prefixo de saudação de um conjunto de dados do Amazon S3.</span><span class="sxs-lookup"><span data-stu-id="ed017-1892">You can do hello same for hello prefix property of an Amazon S3 dataset.</span></span> <span data-ttu-id="ed017-1893">Veja [Funções e variáveis do sistema do Data Factory](data-factory-functions-variables.md) para obter uma lista das funções e variáveis com suporte.</span><span class="sxs-lookup"><span data-stu-id="ed017-1893">See [Data Factory functions and system variables](data-factory-functions-variables.md) for a list of supported functions and variables.</span></span>

<span data-ttu-id="ed017-1894">Para obter mais informações, consulte o artigo [Conector do Amazon S3](data-factory-amazon-simple-storage-service-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="ed017-1894">For more information, see [Amazon S3 connector article](data-factory-amazon-simple-storage-service-connector.md#dataset-properties).</span></span>

### <a name="file-system-source-in-copy-activity"></a><span data-ttu-id="ed017-1895">Origem do Sistema de Arquivos na Atividade de Cópia</span><span class="sxs-lookup"><span data-stu-id="ed017-1895">File System Source in Copy Activity</span></span>
<span data-ttu-id="ed017-1896">Se você estiver copiando dados do Amazon S3, defina Olá **tipo de fonte** de hello atividade de cópia muito**FileSystemSource**e especificar propriedades no Olá a seguir **fonte** seção :</span><span class="sxs-lookup"><span data-stu-id="ed017-1896">If you are copying data from Amazon S3, set hello **source type** of hello copy activity too**FileSystemSource**, and specify following properties in hello **source** section:</span></span>


| <span data-ttu-id="ed017-1897">Propriedade</span><span class="sxs-lookup"><span data-stu-id="ed017-1897">Property</span></span> | <span data-ttu-id="ed017-1898">Descrição</span><span class="sxs-lookup"><span data-stu-id="ed017-1898">Description</span></span> | <span data-ttu-id="ed017-1899">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="ed017-1899">Allowed values</span></span> | <span data-ttu-id="ed017-1900">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="ed017-1900">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="ed017-1901">recursiva</span><span class="sxs-lookup"><span data-stu-id="ed017-1901">recursive</span></span> |<span data-ttu-id="ed017-1902">Especifica se a lista de toorecursively S3 objetos no diretório de saudação.</span><span class="sxs-lookup"><span data-stu-id="ed017-1902">Specifies whether toorecursively list S3 objects under hello directory.</span></span> |<span data-ttu-id="ed017-1903">true/false</span><span class="sxs-lookup"><span data-stu-id="ed017-1903">true/false</span></span> |<span data-ttu-id="ed017-1904">Não</span><span class="sxs-lookup"><span data-stu-id="ed017-1904">No</span></span> |


#### <a name="example"></a><span data-ttu-id="ed017-1905">Exemplo</span><span class="sxs-lookup"><span data-stu-id="ed017-1905">Example</span></span>


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

<span data-ttu-id="ed017-1906">Para obter mais informações, consulte o artigo [Conector do Amazon S3](data-factory-amazon-simple-storage-service-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="ed017-1906">For more information, see [Amazon S3 connector article](data-factory-amazon-simple-storage-service-connector.md#copy-activity-properties).</span></span>

## <a name="file-system"></a><span data-ttu-id="ed017-1907">Sistema de Arquivos</span><span class="sxs-lookup"><span data-stu-id="ed017-1907">File System</span></span>


### <a name="linked-service"></a><span data-ttu-id="ed017-1908">Serviço vinculado</span><span class="sxs-lookup"><span data-stu-id="ed017-1908">Linked service</span></span>
<span data-ttu-id="ed017-1909">Você pode vincular uma fábrica de dados do Azure local arquivo sistema tooan com hello **o servidor de arquivos local** serviço vinculado.</span><span class="sxs-lookup"><span data-stu-id="ed017-1909">You can link an on-premises file system tooan Azure data factory with hello **On-Premises File Server** linked service.</span></span> <span data-ttu-id="ed017-1910">Olá a tabela a seguir fornece descrições dos elementos JSON que são específico toohello serviço vinculado de servidor de arquivos local.</span><span class="sxs-lookup"><span data-stu-id="ed017-1910">hello following table provides descriptions for JSON elements that are specific toohello On-Premises File Server linked service.</span></span>

| <span data-ttu-id="ed017-1911">Propriedade</span><span class="sxs-lookup"><span data-stu-id="ed017-1911">Property</span></span> | <span data-ttu-id="ed017-1912">Descrição</span><span class="sxs-lookup"><span data-stu-id="ed017-1912">Description</span></span> | <span data-ttu-id="ed017-1913">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="ed017-1913">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ed017-1914">type</span><span class="sxs-lookup"><span data-stu-id="ed017-1914">type</span></span> |<span data-ttu-id="ed017-1915">Verifique se a propriedade de tipo hello está definida muito**OnPremisesFileServer**.</span><span class="sxs-lookup"><span data-stu-id="ed017-1915">Ensure that hello type property is set too**OnPremisesFileServer**.</span></span> |<span data-ttu-id="ed017-1916">Sim</span><span class="sxs-lookup"><span data-stu-id="ed017-1916">Yes</span></span> |
| <span data-ttu-id="ed017-1917">host</span><span class="sxs-lookup"><span data-stu-id="ed017-1917">host</span></span> |<span data-ttu-id="ed017-1918">Especifica o caminho de raiz de saudação da pasta Olá que você deseja toocopy.</span><span class="sxs-lookup"><span data-stu-id="ed017-1918">Specifies hello root path of hello folder that you want toocopy.</span></span> <span data-ttu-id="ed017-1919">Use o caractere de escape de saudação ' \ ' para caracteres especiais na cadeia de caracteres de saudação.</span><span class="sxs-lookup"><span data-stu-id="ed017-1919">Use hello escape character ‘ \ ’ for special characters in hello string.</span></span> <span data-ttu-id="ed017-1920">Confira [Definições de conjunto de dados e serviço vinculado de exemplo](#sample-linked-service-and-dataset-definitions) para obter exemplos.</span><span class="sxs-lookup"><span data-stu-id="ed017-1920">See [Sample linked service and dataset definitions](#sample-linked-service-and-dataset-definitions) for examples.</span></span> |<span data-ttu-id="ed017-1921">Sim</span><span class="sxs-lookup"><span data-stu-id="ed017-1921">Yes</span></span> |
| <span data-ttu-id="ed017-1922">userid</span><span class="sxs-lookup"><span data-stu-id="ed017-1922">userid</span></span> |<span data-ttu-id="ed017-1923">Especifique a ID de saudação do usuário de saudação que tem acesso toohello server.</span><span class="sxs-lookup"><span data-stu-id="ed017-1923">Specify hello ID of hello user who has access toohello server.</span></span> |<span data-ttu-id="ed017-1924">Não (se você escolher encryptedcredential)</span><span class="sxs-lookup"><span data-stu-id="ed017-1924">No (if you choose encryptedCredential)</span></span> |
| <span data-ttu-id="ed017-1925">Senha</span><span class="sxs-lookup"><span data-stu-id="ed017-1925">password</span></span> |<span data-ttu-id="ed017-1926">Especifique a senha de saudação para usuário hello (userid).</span><span class="sxs-lookup"><span data-stu-id="ed017-1926">Specify hello password for hello user (userid).</span></span> |<span data-ttu-id="ed017-1927">Não (se você escolher encryptedcredential</span><span class="sxs-lookup"><span data-stu-id="ed017-1927">No (if you choose encryptedCredential</span></span> |
| <span data-ttu-id="ed017-1928">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="ed017-1928">encryptedCredential</span></span> |<span data-ttu-id="ed017-1929">Especifique credenciais Olá criptografado que você pode obter executando Olá AzureRmDataFactoryEncryptValue novo cmdlet.</span><span class="sxs-lookup"><span data-stu-id="ed017-1929">Specify hello encrypted credentials that you can get by running hello New-AzureRmDataFactoryEncryptValue cmdlet.</span></span> |<span data-ttu-id="ed017-1930">Não (se você escolher toospecify ID de usuário e senha em texto sem formatação)</span><span class="sxs-lookup"><span data-stu-id="ed017-1930">No (if you choose toospecify userid and password in plain text)</span></span> |
| <span data-ttu-id="ed017-1931">gatewayName</span><span class="sxs-lookup"><span data-stu-id="ed017-1931">gatewayName</span></span> |<span data-ttu-id="ed017-1932">Especifica o nome de saudação do gateway de saudação que Data Factory deve usar o servidor de arquivos tooconnect toohello local.</span><span class="sxs-lookup"><span data-stu-id="ed017-1932">Specifies hello name of hello gateway that Data Factory should use tooconnect toohello on-premises file server.</span></span> |<span data-ttu-id="ed017-1933">Sim</span><span class="sxs-lookup"><span data-stu-id="ed017-1933">Yes</span></span> |

#### <a name="sample-folder-path-definitions"></a><span data-ttu-id="ed017-1934">Exemplos de definições de caminho de pasta</span><span class="sxs-lookup"><span data-stu-id="ed017-1934">Sample folder path definitions</span></span> 
| <span data-ttu-id="ed017-1935">Cenário</span><span class="sxs-lookup"><span data-stu-id="ed017-1935">Scenario</span></span> | <span data-ttu-id="ed017-1936">Host em definição de serviço vinculado</span><span class="sxs-lookup"><span data-stu-id="ed017-1936">Host in linked service definition</span></span> | <span data-ttu-id="ed017-1937">folderPath em definição de conjunto de dados</span><span class="sxs-lookup"><span data-stu-id="ed017-1937">folderPath in dataset definition</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ed017-1938">Pasta local no computador do Gateway de Gerenciamento de Dados </span><span class="sxs-lookup"><span data-stu-id="ed017-1938">Local folder on Data Management Gateway machine:</span></span> <br/><br/><span data-ttu-id="ed017-1939">Exemplos: D:\\\* ou D:\pasta\subpasta\\*</span><span class="sxs-lookup"><span data-stu-id="ed017-1939">Examples: D:\\\* or D:\folder\subfolder\\*</span></span> |<span data-ttu-id="ed017-1940">D:\\\\ (para o Gateway de Gerenciamento de Dados 2.0 e versões posteriores)</span><span class="sxs-lookup"><span data-stu-id="ed017-1940">D:\\\\ (for Data Management Gateway 2.0 and later versions)</span></span> <br/><br/> <span data-ttu-id="ed017-1941">localhost (para versões anteriores do Gateway de Gerenciamento de Dados 2.0)</span><span class="sxs-lookup"><span data-stu-id="ed017-1941">localhost (for earlier versions than Data Management Gateway 2.0)</span></span> |<span data-ttu-id="ed017-1942">.\\\\ ou pasta\\\\subpasta (para o Gateway de Gerenciamento de Dados 2.0 e versões posteriores)</span><span class="sxs-lookup"><span data-stu-id="ed017-1942">.\\\\ or folder\\\\subfolder (for Data Management Gateway 2.0 and later versions)</span></span> <br/><br/><span data-ttu-id="ed017-1943">D:\\\\ ou D:\\\\pasta\\\\subpasta (para a versão de gateway abaixo de 2.0)</span><span class="sxs-lookup"><span data-stu-id="ed017-1943">D:\\\\ or D:\\\\folder\\\\subfolder (for gateway version below 2.0)</span></span> |
| <span data-ttu-id="ed017-1944">Pasta compartilhada remota: </span><span class="sxs-lookup"><span data-stu-id="ed017-1944">Remote shared folder:</span></span> <br/><br/><span data-ttu-id="ed017-1945">Exemplos: \\\\meuservidor\\compartilhar\\\* ou \\\\meuservidor\\compartilhar\\pasta\\subpasta\\*</span><span class="sxs-lookup"><span data-stu-id="ed017-1945">Examples: \\\\myserver\\share\\\* or \\\\myserver\\share\\folder\\subfolder\\*</span></span> |<span data-ttu-id="ed017-1946">\\\\\\\\meuservidor\\\\compartilhar</span><span class="sxs-lookup"><span data-stu-id="ed017-1946">\\\\\\\\myserver\\\\share</span></span> |<span data-ttu-id="ed017-1947">.\\\\ ou pasta\\\\subpasta</span><span class="sxs-lookup"><span data-stu-id="ed017-1947">.\\\\ or folder\\\\subfolder</span></span> |


#### <a name="example-using-username-and-password-in-plain-text"></a><span data-ttu-id="ed017-1948">Exemplo: usando username e password em texto sem formatação</span><span class="sxs-lookup"><span data-stu-id="ed017-1948">Example: Using username and password in plain text</span></span>

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

#### <a name="example-using-encryptedcredential"></a><span data-ttu-id="ed017-1949">Exemplo: usando encryptedcredential</span><span class="sxs-lookup"><span data-stu-id="ed017-1949">Example: Using encryptedcredential</span></span>

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

<span data-ttu-id="ed017-1950">Para obter mais informações, consulte o [artigo Conector do Sistema de Arquivos](data-factory-onprem-file-system-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="ed017-1950">For more information, see [File System connector article](data-factory-onprem-file-system-connector.md#linked-service-properties).</span></span>

### <a name="dataset"></a><span data-ttu-id="ed017-1951">Conjunto de dados</span><span class="sxs-lookup"><span data-stu-id="ed017-1951">Dataset</span></span>
<span data-ttu-id="ed017-1952">toodefine um conjunto de dados do sistema de arquivos, Olá conjunto **tipo** do conjunto de dados de saudação muito**FileShare**e especifique Olá seguintes propriedades em Olá **typeProperties** seção:</span><span class="sxs-lookup"><span data-stu-id="ed017-1952">toodefine a File System dataset, set hello **type** of hello dataset too**FileShare**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="ed017-1953">Propriedade</span><span class="sxs-lookup"><span data-stu-id="ed017-1953">Property</span></span> | <span data-ttu-id="ed017-1954">Descrição</span><span class="sxs-lookup"><span data-stu-id="ed017-1954">Description</span></span> | <span data-ttu-id="ed017-1955">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="ed017-1955">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ed017-1956">folderPath</span><span class="sxs-lookup"><span data-stu-id="ed017-1956">folderPath</span></span> |<span data-ttu-id="ed017-1957">Especifica a pasta de toohello subcaminho hello.</span><span class="sxs-lookup"><span data-stu-id="ed017-1957">Specifies hello subpath toohello folder.</span></span> <span data-ttu-id="ed017-1958">Use o caractere de escape de saudação ' \' para caracteres especiais na cadeia de caracteres de saudação.</span><span class="sxs-lookup"><span data-stu-id="ed017-1958">Use hello escape character ‘\’ for special characters in hello string.</span></span> <span data-ttu-id="ed017-1959">Confira [Definições de conjunto de dados e serviço vinculado de exemplo](#sample-linked-service-and-dataset-definitions) para obter exemplos.</span><span class="sxs-lookup"><span data-stu-id="ed017-1959">See [Sample linked service and dataset definitions](#sample-linked-service-and-dataset-definitions) for examples.</span></span><br/><br/><span data-ttu-id="ed017-1960">Você pode combinar essa propriedade com **partitionBy** toohave caminhos de pastas com base na fatia datas / horas de início/término.</span><span class="sxs-lookup"><span data-stu-id="ed017-1960">You can combine this property with **partitionBy** toohave folder paths based on slice start/end date-times.</span></span> |<span data-ttu-id="ed017-1961">Sim</span><span class="sxs-lookup"><span data-stu-id="ed017-1961">Yes</span></span> |
| <span data-ttu-id="ed017-1962">fileName</span><span class="sxs-lookup"><span data-stu-id="ed017-1962">fileName</span></span> |<span data-ttu-id="ed017-1963">Especifique o nome de saudação do arquivo de saudação em Olá **folderPath** se você quiser Olá tabela toorefer tooa arquivo específico na pasta hello.</span><span class="sxs-lookup"><span data-stu-id="ed017-1963">Specify hello name of hello file in hello **folderPath** if you want hello table toorefer tooa specific file in hello folder.</span></span> <span data-ttu-id="ed017-1964">Se você não especificar qualquer valor para essa propriedade, a tabela de saudação aponta tooall arquivos na pasta hello.</span><span class="sxs-lookup"><span data-stu-id="ed017-1964">If you do not specify any value for this property, hello table points tooall files in hello folder.</span></span><br/><br/><span data-ttu-id="ed017-1965">Quando o nome de arquivo não for especificado para um conjunto de dados de saída, o nome de saudação do arquivo hello gerado está em Olá formato a seguir:</span><span class="sxs-lookup"><span data-stu-id="ed017-1965">When fileName is not specified for an output dataset, hello name of hello generated file is in hello following format:</span></span> <br/><br/><span data-ttu-id="ed017-1966">`Data.<Guid>.txt` (Exemplo: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt)</span><span class="sxs-lookup"><span data-stu-id="ed017-1966">`Data.<Guid>.txt` (Example: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt)</span></span> |<span data-ttu-id="ed017-1967">Não</span><span class="sxs-lookup"><span data-stu-id="ed017-1967">No</span></span> |
| <span data-ttu-id="ed017-1968">fileFilter</span><span class="sxs-lookup"><span data-stu-id="ed017-1968">fileFilter</span></span> |<span data-ttu-id="ed017-1969">Especifique um filtro toobe usado tooselect um subconjunto de arquivos no hello folderPath em vez de todos os arquivos.</span><span class="sxs-lookup"><span data-stu-id="ed017-1969">Specify a filter toobe used tooselect a subset of files in hello folderPath rather than all files.</span></span> <br/><br/><span data-ttu-id="ed017-1970">Os valores permitidos são: `*` (vários caracteres) e `?` (um único caractere).</span><span class="sxs-lookup"><span data-stu-id="ed017-1970">Allowed values are: `*` (multiple characters) and `?` (single character).</span></span><br/><br/><span data-ttu-id="ed017-1971">Exemplo 1: "fileFilter": "*.log"</span><span class="sxs-lookup"><span data-stu-id="ed017-1971">Example 1: "fileFilter": "*.log"</span></span><br/><span data-ttu-id="ed017-1972">Exemplo 2: "fileFilter": 2016-1-?.txt"</span><span class="sxs-lookup"><span data-stu-id="ed017-1972">Example 2: "fileFilter": 2016-1-?.txt"</span></span><br/><br/><span data-ttu-id="ed017-1973">Observe que fileFilter é aplicável a um conjunto de dados FileShare de entrada.</span><span class="sxs-lookup"><span data-stu-id="ed017-1973">Note that fileFilter is applicable for an input FileShare dataset.</span></span> |<span data-ttu-id="ed017-1974">Não</span><span class="sxs-lookup"><span data-stu-id="ed017-1974">No</span></span> |
| <span data-ttu-id="ed017-1975">partitionedBy</span><span class="sxs-lookup"><span data-stu-id="ed017-1975">partitionedBy</span></span> |<span data-ttu-id="ed017-1976">Você pode usar partitionedBy toospecify um dinâmico folderPath/nome do arquivo de dados da série temporal.</span><span class="sxs-lookup"><span data-stu-id="ed017-1976">You can use partitionedBy toospecify a dynamic folderPath/fileName for time-series data.</span></span> <span data-ttu-id="ed017-1977">Um exemplo é folderPath parametrizado para cada hora dos dados.</span><span class="sxs-lookup"><span data-stu-id="ed017-1977">An example is folderPath parameterized for every hour of data.</span></span> |<span data-ttu-id="ed017-1978">Não</span><span class="sxs-lookup"><span data-stu-id="ed017-1978">No</span></span> |
| <span data-ttu-id="ed017-1979">formato</span><span class="sxs-lookup"><span data-stu-id="ed017-1979">format</span></span> | <span data-ttu-id="ed017-1980">Olá, tipos de formato a seguir têm suporte: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="ed017-1980">hello following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="ed017-1981">Saudação de conjunto **tipo** propriedade em formato tooone desses valores.</span><span class="sxs-lookup"><span data-stu-id="ed017-1981">Set hello **type** property under format tooone of these values.</span></span> <span data-ttu-id="ed017-1982">Para saber mais, veja as seções [Formato de texto](data-factory-supported-file-and-compression-formats.md#text-format), [Formato Json](data-factory-supported-file-and-compression-formats.md#json-format), [Formato Avro](data-factory-supported-file-and-compression-formats.md#avro-format), [Formato Orc](data-factory-supported-file-and-compression-formats.md#orc-format), e [Formato Parquet](data-factory-supported-file-and-compression-formats.md#parquet-format).</span><span class="sxs-lookup"><span data-stu-id="ed017-1982">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="ed017-1983">Se você quiser muito**copiar arquivos como-é** entre repositórios baseada em arquivo (cópia binário), ignore a seção de formato de saudação em ambas as definições de conjunto de dados de entrada e saída.</span><span class="sxs-lookup"><span data-stu-id="ed017-1983">If you want too**copy files as-is** between file-based stores (binary copy), skip hello format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="ed017-1984">Não</span><span class="sxs-lookup"><span data-stu-id="ed017-1984">No</span></span> |
| <span data-ttu-id="ed017-1985">compactação</span><span class="sxs-lookup"><span data-stu-id="ed017-1985">compression</span></span> | <span data-ttu-id="ed017-1986">Especifica tipo de saudação e nível de compactação de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="ed017-1986">Specify hello type and level of compression for hello data.</span></span> <span data-ttu-id="ed017-1987">Os tipos compatíveis são: **GZip**, **Deflate**, **BZip2** e **ZipDeflate**; e os níveis permitidos são: **Ideal** e **Mais rápido**.</span><span class="sxs-lookup"><span data-stu-id="ed017-1987">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**; and supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="ed017-1988">confira [Formatos de arquivo e de compactação no Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="ed017-1988">see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="ed017-1989">Não</span><span class="sxs-lookup"><span data-stu-id="ed017-1989">No</span></span> |

> [!NOTE]
> <span data-ttu-id="ed017-1990">Você não pode usar fileName e fileFilter simultaneamente.</span><span class="sxs-lookup"><span data-stu-id="ed017-1990">You cannot use fileName and fileFilter simultaneously.</span></span>

#### <a name="example"></a><span data-ttu-id="ed017-1991">Exemplo</span><span class="sxs-lookup"><span data-stu-id="ed017-1991">Example</span></span>

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

<span data-ttu-id="ed017-1992">Para obter mais informações, consulte o [artigo Conector do Sistema de Arquivos](data-factory-onprem-file-system-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="ed017-1992">For more information, see [File System connector article](data-factory-onprem-file-system-connector.md#dataset-properties).</span></span>

### <a name="file-system-source-in-copy-activity"></a><span data-ttu-id="ed017-1993">Origem do Sistema de Arquivos na Atividade de Cópia</span><span class="sxs-lookup"><span data-stu-id="ed017-1993">File System Source in Copy Activity</span></span>
<span data-ttu-id="ed017-1994">Se você estiver copiando dados de sistema de arquivos, defina Olá **tipo de fonte** de hello atividade de cópia muito**FileSystemSource**e especificar propriedades no Olá a seguir **fonte** seção:</span><span class="sxs-lookup"><span data-stu-id="ed017-1994">If you are copying data from File System, set hello **source type** of hello copy activity too**FileSystemSource**, and specify following properties in hello **source** section:</span></span>

| <span data-ttu-id="ed017-1995">Propriedade</span><span class="sxs-lookup"><span data-stu-id="ed017-1995">Property</span></span> | <span data-ttu-id="ed017-1996">Descrição</span><span class="sxs-lookup"><span data-stu-id="ed017-1996">Description</span></span> | <span data-ttu-id="ed017-1997">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="ed017-1997">Allowed values</span></span> | <span data-ttu-id="ed017-1998">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="ed017-1998">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="ed017-1999">recursiva</span><span class="sxs-lookup"><span data-stu-id="ed017-1999">recursive</span></span> |<span data-ttu-id="ed017-2000">Indica se os dados saudação é lida recursivamente de subpastas de saudação ou somente de pasta especificado hello.</span><span class="sxs-lookup"><span data-stu-id="ed017-2000">Indicates whether hello data is read recursively from hello subfolders or only from hello specified folder.</span></span> |<span data-ttu-id="ed017-2001">True, False (padrão)</span><span class="sxs-lookup"><span data-stu-id="ed017-2001">True, False (default)</span></span> |<span data-ttu-id="ed017-2002">Não</span><span class="sxs-lookup"><span data-stu-id="ed017-2002">No</span></span> |

#### <a name="example"></a><span data-ttu-id="ed017-2003">Exemplo</span><span class="sxs-lookup"><span data-stu-id="ed017-2003">Example</span></span>

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
<span data-ttu-id="ed017-2004">Para obter mais informações, consulte o [artigo Conector do Sistema de Arquivos](data-factory-onprem-file-system-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="ed017-2004">For more information, see [File System connector article](data-factory-onprem-file-system-connector.md#copy-activity-properties).</span></span>

### <a name="file-system-sink-in-copy-activity"></a><span data-ttu-id="ed017-2005">Coletor do Sistema de Arquivos na Atividade de Cópia</span><span class="sxs-lookup"><span data-stu-id="ed017-2005">File System Sink in Copy Activity</span></span>
<span data-ttu-id="ed017-2006">Se você estiver copiando dados tooFile sistema, definir Olá **tipo de coletor** de hello atividade de cópia muito**FileSystemSink**e especificar propriedades no Olá a seguir **coletor** seção:</span><span class="sxs-lookup"><span data-stu-id="ed017-2006">If you are copying data tooFile System, set hello **sink type** of hello copy activity too**FileSystemSink**, and specify following properties in hello **sink** section:</span></span>

| <span data-ttu-id="ed017-2007">Propriedade</span><span class="sxs-lookup"><span data-stu-id="ed017-2007">Property</span></span> | <span data-ttu-id="ed017-2008">Descrição</span><span class="sxs-lookup"><span data-stu-id="ed017-2008">Description</span></span> | <span data-ttu-id="ed017-2009">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="ed017-2009">Allowed values</span></span> | <span data-ttu-id="ed017-2010">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="ed017-2010">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="ed017-2011">copyBehavior</span><span class="sxs-lookup"><span data-stu-id="ed017-2011">copyBehavior</span></span> |<span data-ttu-id="ed017-2012">Define o comportamento de cópia de saudação quando origem Olá é BlobSource ou sistema de arquivos.</span><span class="sxs-lookup"><span data-stu-id="ed017-2012">Defines hello copy behavior when hello source is BlobSource or FileSystem.</span></span> |<span data-ttu-id="ed017-2013">**PreserveHierarchy:** preserva a hierarquia de arquivo hello na pasta de destino de saudação.</span><span class="sxs-lookup"><span data-stu-id="ed017-2013">**PreserveHierarchy:** Preserves hello file hierarchy in hello target folder.</span></span> <span data-ttu-id="ed017-2014">Ou seja, caminho relativo do Olá Olá arquivo toohello origem da pasta de origem é Olá igual Olá o caminho relativo da pasta de destino toohello do arquivo de destino hello.</span><span class="sxs-lookup"><span data-stu-id="ed017-2014">That is, hello relative path of hello source file toohello source folder is hello same as hello relative path of hello target file toohello target folder.</span></span><br/><br/><span data-ttu-id="ed017-2015">**FlattenHierarchy:** todos os arquivos da pasta de origem Olá são criados no primeiro nível saudação da pasta de destino.</span><span class="sxs-lookup"><span data-stu-id="ed017-2015">**FlattenHierarchy:** All files from hello source folder are created in hello first level of target folder.</span></span> <span data-ttu-id="ed017-2016">arquivos de destino de saudação são criados com um nome gerado automaticamente.</span><span class="sxs-lookup"><span data-stu-id="ed017-2016">hello target files are created with an autogenerated name.</span></span><br/><br/><span data-ttu-id="ed017-2017">**MergeFiles:** mescla todos os arquivos Olá pasta tooone do arquivo de origem.</span><span class="sxs-lookup"><span data-stu-id="ed017-2017">**MergeFiles:** Merges all files from hello source folder tooone file.</span></span> <span data-ttu-id="ed017-2018">Se o nome do blob/nome de arquivo hello for especificado, o nome mesclado Olá é nome especificado da saudação.</span><span class="sxs-lookup"><span data-stu-id="ed017-2018">If hello file name/blob name is specified, hello merged file name is hello specified name.</span></span> <span data-ttu-id="ed017-2019">Caso contrário, ele será um nome de arquivo gerado automaticamente.</span><span class="sxs-lookup"><span data-stu-id="ed017-2019">Otherwise, it is an auto-generated file name.</span></span> |<span data-ttu-id="ed017-2020">Não</span><span class="sxs-lookup"><span data-stu-id="ed017-2020">No</span></span> |
<span data-ttu-id="ed017-2021">auto-</span><span class="sxs-lookup"><span data-stu-id="ed017-2021">auto-</span></span>

#### <a name="example"></a><span data-ttu-id="ed017-2022">Exemplo</span><span class="sxs-lookup"><span data-stu-id="ed017-2022">Example</span></span>

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

<span data-ttu-id="ed017-2023">Para obter mais informações, consulte o [artigo Conector do Sistema de Arquivos](data-factory-onprem-file-system-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="ed017-2023">For more information, see [File System connector article](data-factory-onprem-file-system-connector.md#copy-activity-properties).</span></span>

## <a name="ftp"></a><span data-ttu-id="ed017-2024">FTP</span><span class="sxs-lookup"><span data-stu-id="ed017-2024">FTP</span></span>

### <a name="linked-service"></a><span data-ttu-id="ed017-2025">Serviço vinculado</span><span class="sxs-lookup"><span data-stu-id="ed017-2025">Linked service</span></span>
<span data-ttu-id="ed017-2026">toodefine um FTP o serviço saudação do conjunto vinculado **tipo** de saudação serviço vinculado muito**FtpServer**e especificar propriedades no Olá a seguir **typeProperties** seção:</span><span class="sxs-lookup"><span data-stu-id="ed017-2026">toodefine an FTP linked service, set hello **type** of hello linked service too**FtpServer**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="ed017-2027">Propriedade</span><span class="sxs-lookup"><span data-stu-id="ed017-2027">Property</span></span> | <span data-ttu-id="ed017-2028">Descrição</span><span class="sxs-lookup"><span data-stu-id="ed017-2028">Description</span></span> | <span data-ttu-id="ed017-2029">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="ed017-2029">Required</span></span> | <span data-ttu-id="ed017-2030">Padrão</span><span class="sxs-lookup"><span data-stu-id="ed017-2030">Default</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="ed017-2031">host</span><span class="sxs-lookup"><span data-stu-id="ed017-2031">host</span></span> |<span data-ttu-id="ed017-2032">Nome ou endereço IP do servidor FTP de saudação</span><span class="sxs-lookup"><span data-stu-id="ed017-2032">Name or IP address of hello FTP Server</span></span> |<span data-ttu-id="ed017-2033">Sim</span><span class="sxs-lookup"><span data-stu-id="ed017-2033">Yes</span></span> |&nbsp; |
| <span data-ttu-id="ed017-2034">authenticationType</span><span class="sxs-lookup"><span data-stu-id="ed017-2034">authenticationType</span></span> |<span data-ttu-id="ed017-2035">Especificar tipo de autenticação</span><span class="sxs-lookup"><span data-stu-id="ed017-2035">Specify authentication type</span></span> |<span data-ttu-id="ed017-2036">Sim</span><span class="sxs-lookup"><span data-stu-id="ed017-2036">Yes</span></span> |<span data-ttu-id="ed017-2037">Básica, Anônima</span><span class="sxs-lookup"><span data-stu-id="ed017-2037">Basic, Anonymous</span></span> |
| <span data-ttu-id="ed017-2038">Nome de Usuário</span><span class="sxs-lookup"><span data-stu-id="ed017-2038">username</span></span> |<span data-ttu-id="ed017-2039">Usuário que tem acesso toohello FTP servidor</span><span class="sxs-lookup"><span data-stu-id="ed017-2039">User who has access toohello FTP server</span></span> |<span data-ttu-id="ed017-2040">Não</span><span class="sxs-lookup"><span data-stu-id="ed017-2040">No</span></span> |&nbsp; |
| <span data-ttu-id="ed017-2041">Senha</span><span class="sxs-lookup"><span data-stu-id="ed017-2041">password</span></span> |<span data-ttu-id="ed017-2042">Senha do usuário da saudação (nome de usuário)</span><span class="sxs-lookup"><span data-stu-id="ed017-2042">Password for hello user (username)</span></span> |<span data-ttu-id="ed017-2043">Não</span><span class="sxs-lookup"><span data-stu-id="ed017-2043">No</span></span> |&nbsp; |
| <span data-ttu-id="ed017-2044">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="ed017-2044">encryptedCredential</span></span> |<span data-ttu-id="ed017-2045">Servidor FTP credencial criptografada tooaccess Olá</span><span class="sxs-lookup"><span data-stu-id="ed017-2045">Encrypted credential tooaccess hello FTP server</span></span> |<span data-ttu-id="ed017-2046">Não</span><span class="sxs-lookup"><span data-stu-id="ed017-2046">No</span></span> |&nbsp; |
| <span data-ttu-id="ed017-2047">gatewayName</span><span class="sxs-lookup"><span data-stu-id="ed017-2047">gatewayName</span></span> |<span data-ttu-id="ed017-2048">Nome da saudação Data Management Gateway gateway tooconnect tooan servidor FTP local</span><span class="sxs-lookup"><span data-stu-id="ed017-2048">Name of hello Data Management Gateway gateway tooconnect tooan on-premises FTP server</span></span> |<span data-ttu-id="ed017-2049">Não</span><span class="sxs-lookup"><span data-stu-id="ed017-2049">No</span></span> |&nbsp; |
| <span data-ttu-id="ed017-2050">porta</span><span class="sxs-lookup"><span data-stu-id="ed017-2050">port</span></span> |<span data-ttu-id="ed017-2051">Porta na qual Olá FTP server está escutando</span><span class="sxs-lookup"><span data-stu-id="ed017-2051">Port on which hello FTP server is listening</span></span> |<span data-ttu-id="ed017-2052">Não</span><span class="sxs-lookup"><span data-stu-id="ed017-2052">No</span></span> |<span data-ttu-id="ed017-2053">21</span><span class="sxs-lookup"><span data-stu-id="ed017-2053">21</span></span> |
| <span data-ttu-id="ed017-2054">enableSsl</span><span class="sxs-lookup"><span data-stu-id="ed017-2054">enableSsl</span></span> |<span data-ttu-id="ed017-2055">Especifique se toouse FTP por canal SSL/TLS</span><span class="sxs-lookup"><span data-stu-id="ed017-2055">Specify whether toouse FTP over SSL/TLS channel</span></span> |<span data-ttu-id="ed017-2056">Não</span><span class="sxs-lookup"><span data-stu-id="ed017-2056">No</span></span> |<span data-ttu-id="ed017-2057">verdadeiro</span><span class="sxs-lookup"><span data-stu-id="ed017-2057">true</span></span> |
| <span data-ttu-id="ed017-2058">enableServerCertificateValidation</span><span class="sxs-lookup"><span data-stu-id="ed017-2058">enableServerCertificateValidation</span></span> |<span data-ttu-id="ed017-2059">Especifique se o servidor de tooenable SSL a validação de certificado ao usar o FTP no canal SSL/TLS</span><span class="sxs-lookup"><span data-stu-id="ed017-2059">Specify whether tooenable server SSL certificate validation when using FTP over SSL/TLS channel</span></span> |<span data-ttu-id="ed017-2060">Não</span><span class="sxs-lookup"><span data-stu-id="ed017-2060">No</span></span> |<span data-ttu-id="ed017-2061">verdadeiro</span><span class="sxs-lookup"><span data-stu-id="ed017-2061">true</span></span> |

#### <a name="example-using-anonymous-authentication"></a><span data-ttu-id="ed017-2062">Exemplo: Usando a autenticação anônima</span><span class="sxs-lookup"><span data-stu-id="ed017-2062">Example: Using Anonymous authentication</span></span>

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

#### <a name="example-using-username-and-password-in-plain-text-for-basic-authentication"></a><span data-ttu-id="ed017-2063">Exemplo: Usando o nome de usuário e a senha em texto sem formatação para autenticação básica</span><span class="sxs-lookup"><span data-stu-id="ed017-2063">Example: Using username and password in plain text for basic authentication</span></span>

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

#### <a name="example-using-port-enablessl-enableservercertificatevalidation"></a><span data-ttu-id="ed017-2064">Exemplo: Usando a porta, enableSsl, enableServerCertificateValidation</span><span class="sxs-lookup"><span data-stu-id="ed017-2064">Example: Using port, enableSsl, enableServerCertificateValidation</span></span>

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

#### <a name="example-using-encryptedcredential-for-authentication-and-gateway"></a><span data-ttu-id="ed017-2065">Exemplo: Usando encryptedCredential para autenticação e gateway</span><span class="sxs-lookup"><span data-stu-id="ed017-2065">Example: Using encryptedCredential for authentication and gateway</span></span>

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

<span data-ttu-id="ed017-2066">Para obter mais informações, consulte o artigo [Conector do FTP](data-factory-ftp-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="ed017-2066">For more information, see [FTP connector](data-factory-ftp-connector.md#linked-service-properties) article.</span></span>

### <a name="dataset"></a><span data-ttu-id="ed017-2067">Conjunto de dados</span><span class="sxs-lookup"><span data-stu-id="ed017-2067">Dataset</span></span>
<span data-ttu-id="ed017-2068">toodefine um FTP de conjunto de dados, conjunto Olá **tipo** do conjunto de dados de saudação muito**FileShare**e especifique Olá seguintes propriedades em Olá **typeProperties** seção:</span><span class="sxs-lookup"><span data-stu-id="ed017-2068">toodefine an FTP dataset, set hello **type** of hello dataset too**FileShare**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="ed017-2069">Propriedade</span><span class="sxs-lookup"><span data-stu-id="ed017-2069">Property</span></span> | <span data-ttu-id="ed017-2070">Descrição</span><span class="sxs-lookup"><span data-stu-id="ed017-2070">Description</span></span> | <span data-ttu-id="ed017-2071">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="ed017-2071">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ed017-2072">folderPath</span><span class="sxs-lookup"><span data-stu-id="ed017-2072">folderPath</span></span> |<span data-ttu-id="ed017-2073">Subpasta toohello mais recente para o caminho.</span><span class="sxs-lookup"><span data-stu-id="ed017-2073">Sub path toohello folder.</span></span> <span data-ttu-id="ed017-2074">Use o caractere de escape ' \ ' para caracteres especiais na cadeia de caracteres de saudação.</span><span class="sxs-lookup"><span data-stu-id="ed017-2074">Use escape character ‘ \ ’ for special characters in hello string.</span></span> <span data-ttu-id="ed017-2075">Confira [Definições de conjunto de dados e serviço vinculado de exemplo](#sample-linked-service-and-dataset-definitions) para obter exemplos.</span><span class="sxs-lookup"><span data-stu-id="ed017-2075">See [Sample linked service and dataset definitions](#sample-linked-service-and-dataset-definitions) for examples.</span></span><br/><br/><span data-ttu-id="ed017-2076">Você pode combinar essa propriedade com **partitionBy** toohave caminhos de pastas com base na fatia datas / horas de início/término.</span><span class="sxs-lookup"><span data-stu-id="ed017-2076">You can combine this property with **partitionBy** toohave folder paths based on slice start/end date-times.</span></span> |<span data-ttu-id="ed017-2077">Sim</span><span class="sxs-lookup"><span data-stu-id="ed017-2077">Yes</span></span> 
| <span data-ttu-id="ed017-2078">fileName</span><span class="sxs-lookup"><span data-stu-id="ed017-2078">fileName</span></span> |<span data-ttu-id="ed017-2079">Especifique o nome de saudação do arquivo de saudação em Olá **folderPath** se você quiser Olá tabela toorefer tooa arquivo específico na pasta hello.</span><span class="sxs-lookup"><span data-stu-id="ed017-2079">Specify hello name of hello file in hello **folderPath** if you want hello table toorefer tooa specific file in hello folder.</span></span> <span data-ttu-id="ed017-2080">Se você não especificar qualquer valor para essa propriedade, a tabela de saudação aponta tooall arquivos na pasta hello.</span><span class="sxs-lookup"><span data-stu-id="ed017-2080">If you do not specify any value for this property, hello table points tooall files in hello folder.</span></span><br/><br/><span data-ttu-id="ed017-2081">Quando o nome de arquivo não for especificado para um conjunto de dados de saída, o nome de saudação do arquivo hello gerado aparecerá em Olá esse formato a seguir:</span><span class="sxs-lookup"><span data-stu-id="ed017-2081">When fileName is not specified for an output dataset, hello name of hello generated file would be in hello following this format:</span></span> <br/><br/><span data-ttu-id="ed017-2082">Data.<Guid>.txt (por exemplo: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span><span class="sxs-lookup"><span data-stu-id="ed017-2082">Data.<Guid>.txt (Example: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span></span> |<span data-ttu-id="ed017-2083">Não</span><span class="sxs-lookup"><span data-stu-id="ed017-2083">No</span></span> |
| <span data-ttu-id="ed017-2084">fileFilter</span><span class="sxs-lookup"><span data-stu-id="ed017-2084">fileFilter</span></span> |<span data-ttu-id="ed017-2085">Especifique um filtro toobe usado tooselect um subconjunto de arquivos no hello folderPath em vez de todos os arquivos.</span><span class="sxs-lookup"><span data-stu-id="ed017-2085">Specify a filter toobe used tooselect a subset of files in hello folderPath rather than all files.</span></span><br/><br/><span data-ttu-id="ed017-2086">Os valores permitidos são: `*` (vários caracteres) e `?` (um único caractere).</span><span class="sxs-lookup"><span data-stu-id="ed017-2086">Allowed values are: `*` (multiple characters) and `?` (single character).</span></span><br/><br/><span data-ttu-id="ed017-2087">Exemplo 1: `"fileFilter": "*.log"`</span><span class="sxs-lookup"><span data-stu-id="ed017-2087">Examples 1: `"fileFilter": "*.log"`</span></span><br/><span data-ttu-id="ed017-2088">Exemplo 2: `"fileFilter": 2016-1-?.txt"`</span><span class="sxs-lookup"><span data-stu-id="ed017-2088">Example 2: `"fileFilter": 2016-1-?.txt"`</span></span><br/><br/> <span data-ttu-id="ed017-2089">fileFilter é aplicável a um conjunto de dados FileShare de entrada.</span><span class="sxs-lookup"><span data-stu-id="ed017-2089">fileFilter is applicable for an input FileShare dataset.</span></span> <span data-ttu-id="ed017-2090">Essa propriedade não tem suporte com HDFS.</span><span class="sxs-lookup"><span data-stu-id="ed017-2090">This property is not supported with HDFS.</span></span> |<span data-ttu-id="ed017-2091">Não</span><span class="sxs-lookup"><span data-stu-id="ed017-2091">No</span></span> |
| <span data-ttu-id="ed017-2092">partitionedBy</span><span class="sxs-lookup"><span data-stu-id="ed017-2092">partitionedBy</span></span> |<span data-ttu-id="ed017-2093">partitionedBy pode ser usado toospecify um folderPath dinâmico, nome de arquivo para dados de série temporal.</span><span class="sxs-lookup"><span data-stu-id="ed017-2093">partitionedBy can be used toospecify a dynamic folderPath, filename for time series data.</span></span> <span data-ttu-id="ed017-2094">Por exemplo, folderPath parametrizado para cada hora dos dados.</span><span class="sxs-lookup"><span data-stu-id="ed017-2094">For example, folderPath parameterized for every hour of data.</span></span> |<span data-ttu-id="ed017-2095">Não</span><span class="sxs-lookup"><span data-stu-id="ed017-2095">No</span></span> |
| <span data-ttu-id="ed017-2096">formato</span><span class="sxs-lookup"><span data-stu-id="ed017-2096">format</span></span> | <span data-ttu-id="ed017-2097">Olá, tipos de formato a seguir têm suporte: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="ed017-2097">hello following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="ed017-2098">Saudação de conjunto **tipo** propriedade em formato tooone desses valores.</span><span class="sxs-lookup"><span data-stu-id="ed017-2098">Set hello **type** property under format tooone of these values.</span></span> <span data-ttu-id="ed017-2099">Para saber mais, veja as seções [Formato de texto](data-factory-supported-file-and-compression-formats.md#text-format), [Formato Json](data-factory-supported-file-and-compression-formats.md#json-format), [Formato Avro](data-factory-supported-file-and-compression-formats.md#avro-format), [Formato Orc](data-factory-supported-file-and-compression-formats.md#orc-format), e [Formato Parquet](data-factory-supported-file-and-compression-formats.md#parquet-format).</span><span class="sxs-lookup"><span data-stu-id="ed017-2099">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="ed017-2100">Se você quiser muito**copiar arquivos como-é** entre repositórios baseada em arquivo (cópia binário), ignore a seção de formato de saudação em ambas as definições de conjunto de dados de entrada e saída.</span><span class="sxs-lookup"><span data-stu-id="ed017-2100">If you want too**copy files as-is** between file-based stores (binary copy), skip hello format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="ed017-2101">Não</span><span class="sxs-lookup"><span data-stu-id="ed017-2101">No</span></span> |
| <span data-ttu-id="ed017-2102">compactação</span><span class="sxs-lookup"><span data-stu-id="ed017-2102">compression</span></span> | <span data-ttu-id="ed017-2103">Especifica tipo de saudação e nível de compactação de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="ed017-2103">Specify hello type and level of compression for hello data.</span></span> <span data-ttu-id="ed017-2104">Os tipos compatíveis são: **GZip**, **Deflate**, **BZip2** e **ZipDeflate**; e os níveis permitidos são: **Ideal** e **Mais rápido**.</span><span class="sxs-lookup"><span data-stu-id="ed017-2104">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**; and supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="ed017-2105">Para saber mais, confira [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support) (Formatos de arquivo e de compactação no Azure Data Factory).</span><span class="sxs-lookup"><span data-stu-id="ed017-2105">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="ed017-2106">Não</span><span class="sxs-lookup"><span data-stu-id="ed017-2106">No</span></span> |
| <span data-ttu-id="ed017-2107">useBinaryTransfer</span><span class="sxs-lookup"><span data-stu-id="ed017-2107">useBinaryTransfer</span></span> |<span data-ttu-id="ed017-2108">Especifique se deve usar o modo de transferência Binário.</span><span class="sxs-lookup"><span data-stu-id="ed017-2108">Specify whether use Binary transfer mode.</span></span> <span data-ttu-id="ed017-2109">True para o modo binário e ASCII false.</span><span class="sxs-lookup"><span data-stu-id="ed017-2109">True for binary mode and false ASCII.</span></span> <span data-ttu-id="ed017-2110">Valor padrão: True.</span><span class="sxs-lookup"><span data-stu-id="ed017-2110">Default value: True.</span></span> <span data-ttu-id="ed017-2111">Essa propriedade só pode ser usada quando o tipo de serviço vinculado associado for do tipo: FtpServer.</span><span class="sxs-lookup"><span data-stu-id="ed017-2111">This property can only be used when associated linked service type is of type: FtpServer.</span></span> |<span data-ttu-id="ed017-2112">Não</span><span class="sxs-lookup"><span data-stu-id="ed017-2112">No</span></span> |

> [!NOTE]
> <span data-ttu-id="ed017-2113">filename e fileFilter não podem ser usados simultaneamente.</span><span class="sxs-lookup"><span data-stu-id="ed017-2113">filename and fileFilter cannot be used simultaneously.</span></span>

#### <a name="example"></a><span data-ttu-id="ed017-2114">Exemplo</span><span class="sxs-lookup"><span data-stu-id="ed017-2114">Example</span></span>

```json
{
    "name": "FTPFileInput",
    "properties": {
        "type": "FileShare",
        "linkedServiceName": "FTPLinkedService",
        "typeProperties": {
            "folderPath": "<path tooshared folder>",
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

<span data-ttu-id="ed017-2115">Para obter mais informações, consulte o artigo [Conector do FTP](data-factory-ftp-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="ed017-2115">For more information, see [FTP connector](data-factory-ftp-connector.md#dataset-properties) article.</span></span>

### <a name="file-system-source-in-copy-activity"></a><span data-ttu-id="ed017-2116">Origem do Sistema de Arquivos na Atividade de Cópia</span><span class="sxs-lookup"><span data-stu-id="ed017-2116">File System Source in Copy Activity</span></span>
<span data-ttu-id="ed017-2117">Se você estiver copiando dados de um servidor FTP, defina Olá **tipo de fonte** de hello atividade de cópia muito**FileSystemSource**e especificar propriedades no Olá a seguir **fonte** seção:</span><span class="sxs-lookup"><span data-stu-id="ed017-2117">If you are copying data from an FTP server, set hello **source type** of hello copy activity too**FileSystemSource**, and specify following properties in hello **source** section:</span></span>

| <span data-ttu-id="ed017-2118">Propriedade</span><span class="sxs-lookup"><span data-stu-id="ed017-2118">Property</span></span> | <span data-ttu-id="ed017-2119">Descrição</span><span class="sxs-lookup"><span data-stu-id="ed017-2119">Description</span></span> | <span data-ttu-id="ed017-2120">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="ed017-2120">Allowed values</span></span> | <span data-ttu-id="ed017-2121">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="ed017-2121">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="ed017-2122">recursiva</span><span class="sxs-lookup"><span data-stu-id="ed017-2122">recursive</span></span> |<span data-ttu-id="ed017-2123">Indica se os dados saudação é lida recursivamente de subpastas de saudação ou somente de pasta especificado hello.</span><span class="sxs-lookup"><span data-stu-id="ed017-2123">Indicates whether hello data is read recursively from hello sub folders or only from hello specified folder.</span></span> |<span data-ttu-id="ed017-2124">True, False (padrão)</span><span class="sxs-lookup"><span data-stu-id="ed017-2124">True, False (default)</span></span> |<span data-ttu-id="ed017-2125">Não</span><span class="sxs-lookup"><span data-stu-id="ed017-2125">No</span></span> |

#### <a name="example"></a><span data-ttu-id="ed017-2126">Exemplo</span><span class="sxs-lookup"><span data-stu-id="ed017-2126">Example</span></span>

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

<span data-ttu-id="ed017-2127">Para obter mais informações, consulte o artigo [Conector do FTP](data-factory-ftp-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="ed017-2127">For more information, see [FTP connector](data-factory-ftp-connector.md#copy-activity-properties) article.</span></span>


## <a name="hdfs"></a><span data-ttu-id="ed017-2128">HDFS</span><span class="sxs-lookup"><span data-stu-id="ed017-2128">HDFS</span></span>

### <a name="linked-service"></a><span data-ttu-id="ed017-2129">Serviço vinculado</span><span class="sxs-lookup"><span data-stu-id="ed017-2129">Linked service</span></span>
<span data-ttu-id="ed017-2130">toodefine um HDFS o serviço saudação do conjunto vinculado **tipo** de saudação serviço vinculado muito**Hdfs**e especificar propriedades no Olá a seguir **typeProperties** seção:</span><span class="sxs-lookup"><span data-stu-id="ed017-2130">toodefine a HDFS linked service, set hello **type** of hello linked service too**Hdfs**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="ed017-2131">Propriedade</span><span class="sxs-lookup"><span data-stu-id="ed017-2131">Property</span></span> | <span data-ttu-id="ed017-2132">Descrição</span><span class="sxs-lookup"><span data-stu-id="ed017-2132">Description</span></span> | <span data-ttu-id="ed017-2133">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="ed017-2133">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ed017-2134">type</span><span class="sxs-lookup"><span data-stu-id="ed017-2134">type</span></span> |<span data-ttu-id="ed017-2135">propriedade de tipo Hello deve ser definida como: **Hdfs**</span><span class="sxs-lookup"><span data-stu-id="ed017-2135">hello type property must be set to: **Hdfs**</span></span> |<span data-ttu-id="ed017-2136">Sim</span><span class="sxs-lookup"><span data-stu-id="ed017-2136">Yes</span></span> |
| <span data-ttu-id="ed017-2137">Url</span><span class="sxs-lookup"><span data-stu-id="ed017-2137">Url</span></span> |<span data-ttu-id="ed017-2138">URL toohello HDFS</span><span class="sxs-lookup"><span data-stu-id="ed017-2138">URL toohello HDFS</span></span> |<span data-ttu-id="ed017-2139">Sim</span><span class="sxs-lookup"><span data-stu-id="ed017-2139">Yes</span></span> |
| <span data-ttu-id="ed017-2140">authenticationType</span><span class="sxs-lookup"><span data-stu-id="ed017-2140">authenticationType</span></span> |<span data-ttu-id="ed017-2141">Anônimo ou Windows.</span><span class="sxs-lookup"><span data-stu-id="ed017-2141">Anonymous, or Windows.</span></span> <br><br> <span data-ttu-id="ed017-2142">toouse **a autenticação Kerberos** para conector HDFS, consulte muito[nesta seção](#use-kerberos-authentication-for-hdfs-connector) tooset seu ambiente local adequadamente.</span><span class="sxs-lookup"><span data-stu-id="ed017-2142">toouse **Kerberos authentication** for HDFS connector, refer too[this section](#use-kerberos-authentication-for-hdfs-connector) tooset up your on-premises environment accordingly.</span></span> |<span data-ttu-id="ed017-2143">Sim</span><span class="sxs-lookup"><span data-stu-id="ed017-2143">Yes</span></span> |
| <span data-ttu-id="ed017-2144">userName</span><span class="sxs-lookup"><span data-stu-id="ed017-2144">userName</span></span> |<span data-ttu-id="ed017-2145">Nome de usuário para a autenticação do Windows.</span><span class="sxs-lookup"><span data-stu-id="ed017-2145">Username for Windows authentication.</span></span> |<span data-ttu-id="ed017-2146">Sim (para a Autenticação do Windows)</span><span class="sxs-lookup"><span data-stu-id="ed017-2146">Yes (for Windows Authentication)</span></span> |
| <span data-ttu-id="ed017-2147">Senha</span><span class="sxs-lookup"><span data-stu-id="ed017-2147">password</span></span> |<span data-ttu-id="ed017-2148">Senha para a autenticação do Windows.</span><span class="sxs-lookup"><span data-stu-id="ed017-2148">Password for Windows authentication.</span></span> |<span data-ttu-id="ed017-2149">Sim (para a Autenticação do Windows)</span><span class="sxs-lookup"><span data-stu-id="ed017-2149">Yes (for Windows Authentication)</span></span> |
| <span data-ttu-id="ed017-2150">gatewayName</span><span class="sxs-lookup"><span data-stu-id="ed017-2150">gatewayName</span></span> |<span data-ttu-id="ed017-2151">Nome do gateway Olá Olá serviço da fábrica de dados deve usar tooconnect toohello HDFS.</span><span class="sxs-lookup"><span data-stu-id="ed017-2151">Name of hello gateway that hello Data Factory service should use tooconnect toohello HDFS.</span></span> |<span data-ttu-id="ed017-2152">Sim</span><span class="sxs-lookup"><span data-stu-id="ed017-2152">Yes</span></span> |
| <span data-ttu-id="ed017-2153">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="ed017-2153">encryptedCredential</span></span> |<span data-ttu-id="ed017-2154">[Novo AzureRMDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) saída de credencial de acesso de saudação.</span><span class="sxs-lookup"><span data-stu-id="ed017-2154">[New-AzureRMDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) output of hello access credential.</span></span> |<span data-ttu-id="ed017-2155">Não</span><span class="sxs-lookup"><span data-stu-id="ed017-2155">No</span></span> |

#### <a name="example-using-anonymous-authentication"></a><span data-ttu-id="ed017-2156">Exemplo: Usando a autenticação anônima</span><span class="sxs-lookup"><span data-stu-id="ed017-2156">Example: Using Anonymous authentication</span></span>

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

#### <a name="example-using-windows-authentication"></a><span data-ttu-id="ed017-2157">Exemplo: Usando a autenticação do Windows</span><span class="sxs-lookup"><span data-stu-id="ed017-2157">Example: Using Windows authentication</span></span>

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

<span data-ttu-id="ed017-2158">Para obter mais informações, consulte o artigo [Conector do HDFS](#data-factory-hdfs-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="ed017-2158">For more information, see [HDFS connector](#data-factory-hdfs-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="ed017-2159">Conjunto de dados</span><span class="sxs-lookup"><span data-stu-id="ed017-2159">Dataset</span></span>
<span data-ttu-id="ed017-2160">toodefine um conjunto de dados do HDFS, Olá conjunto **tipo** do conjunto de dados de saudação muito**FileShare**e especifique Olá seguintes propriedades em Olá **typeProperties** seção:</span><span class="sxs-lookup"><span data-stu-id="ed017-2160">toodefine a HDFS dataset, set hello **type** of hello dataset too**FileShare**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="ed017-2161">Propriedade</span><span class="sxs-lookup"><span data-stu-id="ed017-2161">Property</span></span> | <span data-ttu-id="ed017-2162">Descrição</span><span class="sxs-lookup"><span data-stu-id="ed017-2162">Description</span></span> | <span data-ttu-id="ed017-2163">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="ed017-2163">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ed017-2164">folderPath</span><span class="sxs-lookup"><span data-stu-id="ed017-2164">folderPath</span></span> |<span data-ttu-id="ed017-2165">Pasta de toohello de caminho.</span><span class="sxs-lookup"><span data-stu-id="ed017-2165">Path toohello folder.</span></span> <span data-ttu-id="ed017-2166">Exemplo: `myfolder`</span><span class="sxs-lookup"><span data-stu-id="ed017-2166">Example: `myfolder`</span></span><br/><br/><span data-ttu-id="ed017-2167">Use o caractere de escape ' \ ' para caracteres especiais na cadeia de caracteres de saudação.</span><span class="sxs-lookup"><span data-stu-id="ed017-2167">Use escape character ‘ \ ’ for special characters in hello string.</span></span> <span data-ttu-id="ed017-2168">Por exemplo: para pasta\subpasta, especifique a pasta\\\\subpasta e para d:\pastadeexemplo, especifique d:\\\\pastadeexemplo.</span><span class="sxs-lookup"><span data-stu-id="ed017-2168">For example: for folder\subfolder, specify folder\\\\subfolder and for d:\samplefolder, specify d:\\\\samplefolder.</span></span><br/><br/><span data-ttu-id="ed017-2169">Você pode combinar essa propriedade com **partitionBy** toohave caminhos de pastas com base na fatia datas / horas de início/término.</span><span class="sxs-lookup"><span data-stu-id="ed017-2169">You can combine this property with **partitionBy** toohave folder paths based on slice start/end date-times.</span></span> |<span data-ttu-id="ed017-2170">Sim</span><span class="sxs-lookup"><span data-stu-id="ed017-2170">Yes</span></span> |
| <span data-ttu-id="ed017-2171">fileName</span><span class="sxs-lookup"><span data-stu-id="ed017-2171">fileName</span></span> |<span data-ttu-id="ed017-2172">Especifique o nome de saudação do arquivo de saudação em Olá **folderPath** se você quiser Olá tabela toorefer tooa arquivo específico na pasta hello.</span><span class="sxs-lookup"><span data-stu-id="ed017-2172">Specify hello name of hello file in hello **folderPath** if you want hello table toorefer tooa specific file in hello folder.</span></span> <span data-ttu-id="ed017-2173">Se você não especificar qualquer valor para essa propriedade, a tabela de saudação aponta tooall arquivos na pasta hello.</span><span class="sxs-lookup"><span data-stu-id="ed017-2173">If you do not specify any value for this property, hello table points tooall files in hello folder.</span></span><br/><br/><span data-ttu-id="ed017-2174">Quando o nome de arquivo não for especificado para um conjunto de dados de saída, o nome de saudação do arquivo hello gerado aparecerá em Olá esse formato a seguir:</span><span class="sxs-lookup"><span data-stu-id="ed017-2174">When fileName is not specified for an output dataset, hello name of hello generated file would be in hello following this format:</span></span> <br/><br/><span data-ttu-id="ed017-2175">Data<Guid>.txt (por exemplo: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span><span class="sxs-lookup"><span data-stu-id="ed017-2175">Data.<Guid>.txt (for example: : Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span></span> |<span data-ttu-id="ed017-2176">Não</span><span class="sxs-lookup"><span data-stu-id="ed017-2176">No</span></span> |
| <span data-ttu-id="ed017-2177">partitionedBy</span><span class="sxs-lookup"><span data-stu-id="ed017-2177">partitionedBy</span></span> |<span data-ttu-id="ed017-2178">partitionedBy pode ser usado toospecify um folderPath dinâmico, nome de arquivo para dados de série temporal.</span><span class="sxs-lookup"><span data-stu-id="ed017-2178">partitionedBy can be used toospecify a dynamic folderPath, filename for time series data.</span></span> <span data-ttu-id="ed017-2179">Exemplo: folderPath parametrizado para cada hora dos dados.</span><span class="sxs-lookup"><span data-stu-id="ed017-2179">Example: folderPath parameterized for every hour of data.</span></span> |<span data-ttu-id="ed017-2180">Não</span><span class="sxs-lookup"><span data-stu-id="ed017-2180">No</span></span> |
| <span data-ttu-id="ed017-2181">formato</span><span class="sxs-lookup"><span data-stu-id="ed017-2181">format</span></span> | <span data-ttu-id="ed017-2182">Olá, tipos de formato a seguir têm suporte: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="ed017-2182">hello following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="ed017-2183">Saudação de conjunto **tipo** propriedade em formato tooone desses valores.</span><span class="sxs-lookup"><span data-stu-id="ed017-2183">Set hello **type** property under format tooone of these values.</span></span> <span data-ttu-id="ed017-2184">Para saber mais, veja as seções [Formato de texto](data-factory-supported-file-and-compression-formats.md#text-format), [Formato Json](data-factory-supported-file-and-compression-formats.md#json-format), [Formato Avro](data-factory-supported-file-and-compression-formats.md#avro-format), [Formato Orc](data-factory-supported-file-and-compression-formats.md#orc-format), e [Formato Parquet](data-factory-supported-file-and-compression-formats.md#parquet-format).</span><span class="sxs-lookup"><span data-stu-id="ed017-2184">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="ed017-2185">Se você quiser muito**copiar arquivos como-é** entre repositórios baseada em arquivo (cópia binário), ignore a seção de formato de saudação em ambas as definições de conjunto de dados de entrada e saída.</span><span class="sxs-lookup"><span data-stu-id="ed017-2185">If you want too**copy files as-is** between file-based stores (binary copy), skip hello format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="ed017-2186">Não</span><span class="sxs-lookup"><span data-stu-id="ed017-2186">No</span></span> |
| <span data-ttu-id="ed017-2187">compactação</span><span class="sxs-lookup"><span data-stu-id="ed017-2187">compression</span></span> | <span data-ttu-id="ed017-2188">Especifica tipo de saudação e nível de compactação de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="ed017-2188">Specify hello type and level of compression for hello data.</span></span> <span data-ttu-id="ed017-2189">Os tipos com suporte são: **GZip**, **Deflate**, **BZip2** e **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="ed017-2189">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="ed017-2190">Os níveis com suporte são **Ideal** e **O mais rápido**.</span><span class="sxs-lookup"><span data-stu-id="ed017-2190">Supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="ed017-2191">Para saber mais, confira [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support) (Formatos de arquivo e de compactação no Azure Data Factory).</span><span class="sxs-lookup"><span data-stu-id="ed017-2191">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="ed017-2192">Não</span><span class="sxs-lookup"><span data-stu-id="ed017-2192">No</span></span> |

> [!NOTE]
> <span data-ttu-id="ed017-2193">filename e fileFilter não podem ser usados simultaneamente.</span><span class="sxs-lookup"><span data-stu-id="ed017-2193">filename and fileFilter cannot be used simultaneously.</span></span>

#### <a name="example"></a><span data-ttu-id="ed017-2194">Exemplo</span><span class="sxs-lookup"><span data-stu-id="ed017-2194">Example</span></span>

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

<span data-ttu-id="ed017-2195">Para obter mais informações, consulte o artigo [Conector do HDFS](#data-factory-hdfs-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="ed017-2195">For more information, see [HDFS connector](#data-factory-hdfs-connector.md#dataset-properties) article.</span></span> 

### <a name="file-system-source-in-copy-activity"></a><span data-ttu-id="ed017-2196">Origem do Sistema de Arquivos na Atividade de Cópia</span><span class="sxs-lookup"><span data-stu-id="ed017-2196">File System Source in Copy Activity</span></span>
<span data-ttu-id="ed017-2197">Se você estiver copiando dados do HDFS, defina Olá **tipo de fonte** de hello atividade de cópia muito**FileSystemSource**e especificar propriedades no Olá a seguir **fonte** seção:</span><span class="sxs-lookup"><span data-stu-id="ed017-2197">If you are copying data from HDFS, set hello **source type** of hello copy activity too**FileSystemSource**, and specify following properties in hello **source** section:</span></span>

<span data-ttu-id="ed017-2198">**FileSystemSource** dá suporte a saudação propriedades a seguir:</span><span class="sxs-lookup"><span data-stu-id="ed017-2198">**FileSystemSource** supports hello following properties:</span></span>

| <span data-ttu-id="ed017-2199">Propriedade</span><span class="sxs-lookup"><span data-stu-id="ed017-2199">Property</span></span> | <span data-ttu-id="ed017-2200">Descrição</span><span class="sxs-lookup"><span data-stu-id="ed017-2200">Description</span></span> | <span data-ttu-id="ed017-2201">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="ed017-2201">Allowed values</span></span> | <span data-ttu-id="ed017-2202">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="ed017-2202">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="ed017-2203">recursiva</span><span class="sxs-lookup"><span data-stu-id="ed017-2203">recursive</span></span> |<span data-ttu-id="ed017-2204">Indica se os dados saudação é lida recursivamente de subpastas de saudação ou somente de pasta especificado hello.</span><span class="sxs-lookup"><span data-stu-id="ed017-2204">Indicates whether hello data is read recursively from hello sub folders or only from hello specified folder.</span></span> |<span data-ttu-id="ed017-2205">True, False (padrão)</span><span class="sxs-lookup"><span data-stu-id="ed017-2205">True, False (default)</span></span> |<span data-ttu-id="ed017-2206">Não</span><span class="sxs-lookup"><span data-stu-id="ed017-2206">No</span></span> |

#### <a name="example"></a><span data-ttu-id="ed017-2207">Exemplo</span><span class="sxs-lookup"><span data-stu-id="ed017-2207">Example</span></span>

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

<span data-ttu-id="ed017-2208">Para obter mais informações, consulte o artigo [Conector do HDFS](#data-factory-hdfs-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="ed017-2208">For more information, see [HDFS connector](#data-factory-hdfs-connector.md#copy-activity-properties) article.</span></span>

## <a name="sftp"></a><span data-ttu-id="ed017-2209">SFTP</span><span class="sxs-lookup"><span data-stu-id="ed017-2209">SFTP</span></span>


### <a name="linked-service"></a><span data-ttu-id="ed017-2210">Serviço vinculado</span><span class="sxs-lookup"><span data-stu-id="ed017-2210">Linked service</span></span>
<span data-ttu-id="ed017-2211">toodefine um SFTP vinculado serviço, Olá conjunto **tipo** de saudação serviço vinculado muito**Sftp**e especificar propriedades no Olá a seguir **typeProperties** seção:</span><span class="sxs-lookup"><span data-stu-id="ed017-2211">toodefine an SFTP linked service, set hello **type** of hello linked service too**Sftp**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="ed017-2212">Propriedade</span><span class="sxs-lookup"><span data-stu-id="ed017-2212">Property</span></span> | <span data-ttu-id="ed017-2213">Descrição</span><span class="sxs-lookup"><span data-stu-id="ed017-2213">Description</span></span> | <span data-ttu-id="ed017-2214">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="ed017-2214">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="ed017-2215">host</span><span class="sxs-lookup"><span data-stu-id="ed017-2215">host</span></span> | <span data-ttu-id="ed017-2216">Nome ou endereço IP do servidor SFTP hello.</span><span class="sxs-lookup"><span data-stu-id="ed017-2216">Name or IP address of hello SFTP server.</span></span> |<span data-ttu-id="ed017-2217">Sim</span><span class="sxs-lookup"><span data-stu-id="ed017-2217">Yes</span></span> |
| <span data-ttu-id="ed017-2218">porta</span><span class="sxs-lookup"><span data-stu-id="ed017-2218">port</span></span> |<span data-ttu-id="ed017-2219">Porta na qual Olá SFTP server está escutando.</span><span class="sxs-lookup"><span data-stu-id="ed017-2219">Port on which hello SFTP server is listening.</span></span> <span data-ttu-id="ed017-2220">valor padrão de saudação é: 21</span><span class="sxs-lookup"><span data-stu-id="ed017-2220">hello default value is: 21</span></span> |<span data-ttu-id="ed017-2221">Não</span><span class="sxs-lookup"><span data-stu-id="ed017-2221">No</span></span> |
| <span data-ttu-id="ed017-2222">authenticationType</span><span class="sxs-lookup"><span data-stu-id="ed017-2222">authenticationType</span></span> |<span data-ttu-id="ed017-2223">Especifique o tipo de autenticação.</span><span class="sxs-lookup"><span data-stu-id="ed017-2223">Specify authentication type.</span></span> <span data-ttu-id="ed017-2224">Valores permitidos: **Básica**, **SshPublicKey**.</span><span class="sxs-lookup"><span data-stu-id="ed017-2224">Allowed values: **Basic**, **SshPublicKey**.</span></span> <br><br> <span data-ttu-id="ed017-2225">Consulte também[usando a autenticação básica](#using-basic-authentication) e [usando SSH autenticação de chave pública](#using-ssh-public-key-authentication) seções em mais propriedades e exemplos JSON, respectivamente.</span><span class="sxs-lookup"><span data-stu-id="ed017-2225">Refer too[Using basic authentication](#using-basic-authentication) and [Using SSH public key authentication](#using-ssh-public-key-authentication) sections on more properties and JSON samples respectively.</span></span> |<span data-ttu-id="ed017-2226">Sim</span><span class="sxs-lookup"><span data-stu-id="ed017-2226">Yes</span></span> |
| <span data-ttu-id="ed017-2227">skipHostKeyValidation</span><span class="sxs-lookup"><span data-stu-id="ed017-2227">skipHostKeyValidation</span></span> | <span data-ttu-id="ed017-2228">Especifique se tooskip validação de chave do host.</span><span class="sxs-lookup"><span data-stu-id="ed017-2228">Specify whether tooskip host key validation.</span></span> | <span data-ttu-id="ed017-2229">Não.</span><span class="sxs-lookup"><span data-stu-id="ed017-2229">No.</span></span> <span data-ttu-id="ed017-2230">Olá valor padrão: false</span><span class="sxs-lookup"><span data-stu-id="ed017-2230">hello default value: false</span></span> |
| <span data-ttu-id="ed017-2231">hostKeyFingerprint</span><span class="sxs-lookup"><span data-stu-id="ed017-2231">hostKeyFingerprint</span></span> | <span data-ttu-id="ed017-2232">Especifique a impressão digital de saudação da chave de host hello.</span><span class="sxs-lookup"><span data-stu-id="ed017-2232">Specify hello finger print of hello host key.</span></span> | <span data-ttu-id="ed017-2233">Sim se hello `skipHostKeyValidation` é definido toofalse.</span><span class="sxs-lookup"><span data-stu-id="ed017-2233">Yes if hello `skipHostKeyValidation` is set toofalse.</span></span>  |
| <span data-ttu-id="ed017-2234">gatewayName</span><span class="sxs-lookup"><span data-stu-id="ed017-2234">gatewayName</span></span> |<span data-ttu-id="ed017-2235">Nome da saudação Data Management Gateway tooconnect tooan local do servidor SFTP.</span><span class="sxs-lookup"><span data-stu-id="ed017-2235">Name of hello Data Management Gateway tooconnect tooan on-premises SFTP server.</span></span> | <span data-ttu-id="ed017-2236">Sim se estiver copiando dados de um servidor SFTP local.</span><span class="sxs-lookup"><span data-stu-id="ed017-2236">Yes if copying data from an on-premises SFTP server.</span></span> |
| <span data-ttu-id="ed017-2237">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="ed017-2237">encryptedCredential</span></span> | <span data-ttu-id="ed017-2238">Servidor SFTP saudação do tooaccess credencial criptografada.</span><span class="sxs-lookup"><span data-stu-id="ed017-2238">Encrypted credential tooaccess hello SFTP server.</span></span> <span data-ttu-id="ed017-2239">Gerado automaticamente quando você especificar a autenticação básica (nome de usuário + senha) ou parâmetros SshPublicKey (nome de usuário + caminho da chave privado ou conteúdo) no diálogo de pop-up de ClickOnce de assistente ou saudação de cópia.</span><span class="sxs-lookup"><span data-stu-id="ed017-2239">Auto-generated when you specify basic authentication (username + password) or SshPublicKey authentication (username + private key path or content) in copy wizard or hello ClickOnce popup dialog.</span></span> | <span data-ttu-id="ed017-2240">Não.</span><span class="sxs-lookup"><span data-stu-id="ed017-2240">No.</span></span> <span data-ttu-id="ed017-2241">Aplique somente quando estiver copiando dados de um servidor SFTP local.</span><span class="sxs-lookup"><span data-stu-id="ed017-2241">Apply only when copying data from an on-premises SFTP server.</span></span> |

#### <a name="example-using-basic-authentication"></a><span data-ttu-id="ed017-2242">Exemplo: Usando a autenticação básica</span><span class="sxs-lookup"><span data-stu-id="ed017-2242">Example: Using basic authentication</span></span>

<span data-ttu-id="ed017-2243">Definir toouse a autenticação básica, `authenticationType` como `Basic`e especifique Olá seguintes propriedades além Olá conector SFTP genérico aqueles introduzidos na última seção do hello:</span><span class="sxs-lookup"><span data-stu-id="ed017-2243">toouse basic authentication, set `authenticationType` as `Basic`, and specify hello following properties besides hello SFTP connector generic ones introduced in hello last section:</span></span>

| <span data-ttu-id="ed017-2244">Propriedade</span><span class="sxs-lookup"><span data-stu-id="ed017-2244">Property</span></span> | <span data-ttu-id="ed017-2245">Descrição</span><span class="sxs-lookup"><span data-stu-id="ed017-2245">Description</span></span> | <span data-ttu-id="ed017-2246">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="ed017-2246">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="ed017-2247">Nome de Usuário</span><span class="sxs-lookup"><span data-stu-id="ed017-2247">username</span></span> | <span data-ttu-id="ed017-2248">Usuário que possui o servidor do acesso toohello SFTP.</span><span class="sxs-lookup"><span data-stu-id="ed017-2248">User who has access toohello SFTP server.</span></span> |<span data-ttu-id="ed017-2249">Sim</span><span class="sxs-lookup"><span data-stu-id="ed017-2249">Yes</span></span> |
| <span data-ttu-id="ed017-2250">Senha</span><span class="sxs-lookup"><span data-stu-id="ed017-2250">password</span></span> | <span data-ttu-id="ed017-2251">Senha do usuário da saudação (nome de usuário).</span><span class="sxs-lookup"><span data-stu-id="ed017-2251">Password for hello user (username).</span></span> | <span data-ttu-id="ed017-2252">Sim</span><span class="sxs-lookup"><span data-stu-id="ed017-2252">Yes</span></span> |

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

#### <a name="example-basic-authentication-with-encrypted-credential"></a><span data-ttu-id="ed017-2253">Exemplo: Autenticação básica com credencial criptografada**</span><span class="sxs-lookup"><span data-stu-id="ed017-2253">Example: Basic authentication with encrypted credential**</span></span>

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

#### <a name="using-ssh-public-key-authentication"></a><span data-ttu-id="ed017-2254">Usando a autenticação de chave pública SSH:**</span><span class="sxs-lookup"><span data-stu-id="ed017-2254">Using SSH public key authentication:**</span></span>

<span data-ttu-id="ed017-2255">Definir toouse a autenticação básica, `authenticationType` como `SshPublicKey`e especifique Olá seguintes propriedades além Olá conector SFTP genérico aqueles introduzidos na última seção do hello:</span><span class="sxs-lookup"><span data-stu-id="ed017-2255">toouse basic authentication, set `authenticationType` as `SshPublicKey`, and specify hello following properties besides hello SFTP connector generic ones introduced in hello last section:</span></span>

| <span data-ttu-id="ed017-2256">Propriedade</span><span class="sxs-lookup"><span data-stu-id="ed017-2256">Property</span></span> | <span data-ttu-id="ed017-2257">Descrição</span><span class="sxs-lookup"><span data-stu-id="ed017-2257">Description</span></span> | <span data-ttu-id="ed017-2258">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="ed017-2258">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="ed017-2259">Nome de Usuário</span><span class="sxs-lookup"><span data-stu-id="ed017-2259">username</span></span> |<span data-ttu-id="ed017-2260">Usuário que tem acesso toohello SFTP servidor</span><span class="sxs-lookup"><span data-stu-id="ed017-2260">User who has access toohello SFTP server</span></span> |<span data-ttu-id="ed017-2261">Sim</span><span class="sxs-lookup"><span data-stu-id="ed017-2261">Yes</span></span> |
| <span data-ttu-id="ed017-2262">privateKeyPath</span><span class="sxs-lookup"><span data-stu-id="ed017-2262">privateKeyPath</span></span> | <span data-ttu-id="ed017-2263">Especifique o caminho absoluto toohello arquivo de chave privada pode acessar o gateway.</span><span class="sxs-lookup"><span data-stu-id="ed017-2263">Specify absolute path toohello private key file that gateway can access.</span></span> | <span data-ttu-id="ed017-2264">Especifique a saudação `privateKeyPath` ou `privateKeyContent`.</span><span class="sxs-lookup"><span data-stu-id="ed017-2264">Specify either hello `privateKeyPath` or `privateKeyContent`.</span></span> <br><br> <span data-ttu-id="ed017-2265">Aplique somente quando estiver copiando dados de um servidor SFTP local.</span><span class="sxs-lookup"><span data-stu-id="ed017-2265">Apply only when copying data from an on-premises SFTP server.</span></span> |
| <span data-ttu-id="ed017-2266">privateKeyContent</span><span class="sxs-lookup"><span data-stu-id="ed017-2266">privateKeyContent</span></span> | <span data-ttu-id="ed017-2267">Uma cadeia de caracteres serializada de conteúdo da chave privada hello.</span><span class="sxs-lookup"><span data-stu-id="ed017-2267">A serialized string of hello private key content.</span></span> <span data-ttu-id="ed017-2268">Olá Assistente para cópia pode ler o arquivo de chave privada hello e extrair o conteúdo da chave privada Olá automaticamente.</span><span class="sxs-lookup"><span data-stu-id="ed017-2268">hello Copy Wizard can read hello private key file and extract hello private key content automatically.</span></span> <span data-ttu-id="ed017-2269">Se você estiver usando qualquer outra ferramenta/SDK, use a propriedade de privateKeyPath de saudação em vez disso.</span><span class="sxs-lookup"><span data-stu-id="ed017-2269">If you are using any other tool/SDK, use hello privateKeyPath property instead.</span></span> | <span data-ttu-id="ed017-2270">Especifique a saudação `privateKeyPath` ou `privateKeyContent`.</span><span class="sxs-lookup"><span data-stu-id="ed017-2270">Specify either hello `privateKeyPath` or `privateKeyContent`.</span></span> |
| <span data-ttu-id="ed017-2271">Senha</span><span class="sxs-lookup"><span data-stu-id="ed017-2271">passPhrase</span></span> | <span data-ttu-id="ed017-2272">Especifique Olá senha/frase toodecrypt Olá privada chave de acesso de se o arquivo de chave Olá estiver protegido por uma frase secreta.</span><span class="sxs-lookup"><span data-stu-id="ed017-2272">Specify hello pass phrase/password toodecrypt hello private key if hello key file is protected by a pass phrase.</span></span> | <span data-ttu-id="ed017-2273">Sim, se o arquivo de chave privada Olá é protegido por uma frase secreta.</span><span class="sxs-lookup"><span data-stu-id="ed017-2273">Yes if hello private key file is protected by a pass phrase.</span></span> |

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

#### <a name="example-sshpublickey-authentication-using-private-key-content"></a><span data-ttu-id="ed017-2274">Exemplo: autenticação de SshPublicKey usando o conteúdo da chave privada**</span><span class="sxs-lookup"><span data-stu-id="ed017-2274">Example: SshPublicKey authentication using private key content**</span></span>

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
            "privateKeyContent": "<base64 string of hello private key content>",
            "passPhrase": "xxx",
            "skipHostKeyValidation": true
        }
    }
}
```

<span data-ttu-id="ed017-2275">Para obter mais informações, consulte o artigo [Conector do SFTP](data-factory-sftp-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="ed017-2275">For more information, see [SFTP connector](data-factory-sftp-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="ed017-2276">Conjunto de dados</span><span class="sxs-lookup"><span data-stu-id="ed017-2276">Dataset</span></span>
<span data-ttu-id="ed017-2277">toodefine um conjunto de dados SFTP, Olá conjunto **tipo** do conjunto de dados de saudação muito**FileShare**e especifique Olá seguintes propriedades em Olá **typeProperties** seção:</span><span class="sxs-lookup"><span data-stu-id="ed017-2277">toodefine an SFTP dataset, set hello **type** of hello dataset too**FileShare**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="ed017-2278">Propriedade</span><span class="sxs-lookup"><span data-stu-id="ed017-2278">Property</span></span> | <span data-ttu-id="ed017-2279">Descrição</span><span class="sxs-lookup"><span data-stu-id="ed017-2279">Description</span></span> | <span data-ttu-id="ed017-2280">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="ed017-2280">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ed017-2281">folderPath</span><span class="sxs-lookup"><span data-stu-id="ed017-2281">folderPath</span></span> |<span data-ttu-id="ed017-2282">Subpasta toohello mais recente para o caminho.</span><span class="sxs-lookup"><span data-stu-id="ed017-2282">Sub path toohello folder.</span></span> <span data-ttu-id="ed017-2283">Use o caractere de escape ' \ ' para caracteres especiais na cadeia de caracteres de saudação.</span><span class="sxs-lookup"><span data-stu-id="ed017-2283">Use escape character ‘ \ ’ for special characters in hello string.</span></span> <span data-ttu-id="ed017-2284">Confira [Definições de conjunto de dados e serviço vinculado de exemplo](#sample-linked-service-and-dataset-definitions) para obter exemplos.</span><span class="sxs-lookup"><span data-stu-id="ed017-2284">See [Sample linked service and dataset definitions](#sample-linked-service-and-dataset-definitions) for examples.</span></span><br/><br/><span data-ttu-id="ed017-2285">Você pode combinar essa propriedade com **partitionBy** toohave caminhos de pastas com base na fatia datas / horas de início/término.</span><span class="sxs-lookup"><span data-stu-id="ed017-2285">You can combine this property with **partitionBy** toohave folder paths based on slice start/end date-times.</span></span> |<span data-ttu-id="ed017-2286">Sim</span><span class="sxs-lookup"><span data-stu-id="ed017-2286">Yes</span></span> |
| <span data-ttu-id="ed017-2287">fileName</span><span class="sxs-lookup"><span data-stu-id="ed017-2287">fileName</span></span> |<span data-ttu-id="ed017-2288">Especifique o nome de saudação do arquivo de saudação em Olá **folderPath** se você quiser Olá tabela toorefer tooa arquivo específico na pasta hello.</span><span class="sxs-lookup"><span data-stu-id="ed017-2288">Specify hello name of hello file in hello **folderPath** if you want hello table toorefer tooa specific file in hello folder.</span></span> <span data-ttu-id="ed017-2289">Se você não especificar qualquer valor para essa propriedade, a tabela de saudação aponta tooall arquivos na pasta hello.</span><span class="sxs-lookup"><span data-stu-id="ed017-2289">If you do not specify any value for this property, hello table points tooall files in hello folder.</span></span><br/><br/><span data-ttu-id="ed017-2290">Quando o nome de arquivo não for especificado para um conjunto de dados de saída, o nome de saudação do arquivo hello gerado aparecerá em Olá esse formato a seguir:</span><span class="sxs-lookup"><span data-stu-id="ed017-2290">When fileName is not specified for an output dataset, hello name of hello generated file would be in hello following this format:</span></span> <br/><br/><span data-ttu-id="ed017-2291">Data.<Guid>.txt (por exemplo: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span><span class="sxs-lookup"><span data-stu-id="ed017-2291">Data.<Guid>.txt (Example: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span></span> |<span data-ttu-id="ed017-2292">Não</span><span class="sxs-lookup"><span data-stu-id="ed017-2292">No</span></span> |
| <span data-ttu-id="ed017-2293">fileFilter</span><span class="sxs-lookup"><span data-stu-id="ed017-2293">fileFilter</span></span> |<span data-ttu-id="ed017-2294">Especifique um filtro toobe usado tooselect um subconjunto de arquivos no hello folderPath em vez de todos os arquivos.</span><span class="sxs-lookup"><span data-stu-id="ed017-2294">Specify a filter toobe used tooselect a subset of files in hello folderPath rather than all files.</span></span><br/><br/><span data-ttu-id="ed017-2295">Os valores permitidos são: `*` (vários caracteres) e `?` (um único caractere).</span><span class="sxs-lookup"><span data-stu-id="ed017-2295">Allowed values are: `*` (multiple characters) and `?` (single character).</span></span><br/><br/><span data-ttu-id="ed017-2296">Exemplo 1: `"fileFilter": "*.log"`</span><span class="sxs-lookup"><span data-stu-id="ed017-2296">Examples 1: `"fileFilter": "*.log"`</span></span><br/><span data-ttu-id="ed017-2297">Exemplo 2: `"fileFilter": 2016-1-?.txt"`</span><span class="sxs-lookup"><span data-stu-id="ed017-2297">Example 2: `"fileFilter": 2016-1-?.txt"`</span></span><br/><br/> <span data-ttu-id="ed017-2298">fileFilter é aplicável a um conjunto de dados FileShare de entrada.</span><span class="sxs-lookup"><span data-stu-id="ed017-2298">fileFilter is applicable for an input FileShare dataset.</span></span> <span data-ttu-id="ed017-2299">Essa propriedade não tem suporte com HDFS.</span><span class="sxs-lookup"><span data-stu-id="ed017-2299">This property is not supported with HDFS.</span></span> |<span data-ttu-id="ed017-2300">Não</span><span class="sxs-lookup"><span data-stu-id="ed017-2300">No</span></span> |
| <span data-ttu-id="ed017-2301">partitionedBy</span><span class="sxs-lookup"><span data-stu-id="ed017-2301">partitionedBy</span></span> |<span data-ttu-id="ed017-2302">partitionedBy pode ser usado toospecify um folderPath dinâmico, nome de arquivo para dados de série temporal.</span><span class="sxs-lookup"><span data-stu-id="ed017-2302">partitionedBy can be used toospecify a dynamic folderPath, filename for time series data.</span></span> <span data-ttu-id="ed017-2303">Por exemplo, folderPath parametrizado para cada hora dos dados.</span><span class="sxs-lookup"><span data-stu-id="ed017-2303">For example, folderPath parameterized for every hour of data.</span></span> |<span data-ttu-id="ed017-2304">Não</span><span class="sxs-lookup"><span data-stu-id="ed017-2304">No</span></span> |
| <span data-ttu-id="ed017-2305">formato</span><span class="sxs-lookup"><span data-stu-id="ed017-2305">format</span></span> | <span data-ttu-id="ed017-2306">Olá, tipos de formato a seguir têm suporte: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="ed017-2306">hello following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="ed017-2307">Saudação de conjunto **tipo** propriedade em formato tooone desses valores.</span><span class="sxs-lookup"><span data-stu-id="ed017-2307">Set hello **type** property under format tooone of these values.</span></span> <span data-ttu-id="ed017-2308">Para saber mais, veja as seções [Formato de texto](data-factory-supported-file-and-compression-formats.md#text-format), [Formato Json](data-factory-supported-file-and-compression-formats.md#json-format), [Formato Avro](data-factory-supported-file-and-compression-formats.md#avro-format), [Formato Orc](data-factory-supported-file-and-compression-formats.md#orc-format), e [Formato Parquet](data-factory-supported-file-and-compression-formats.md#parquet-format).</span><span class="sxs-lookup"><span data-stu-id="ed017-2308">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="ed017-2309">Se você quiser muito**copiar arquivos como-é** entre repositórios baseada em arquivo (cópia binário), ignore a seção de formato de saudação em ambas as definições de conjunto de dados de entrada e saída.</span><span class="sxs-lookup"><span data-stu-id="ed017-2309">If you want too**copy files as-is** between file-based stores (binary copy), skip hello format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="ed017-2310">Não</span><span class="sxs-lookup"><span data-stu-id="ed017-2310">No</span></span> |
| <span data-ttu-id="ed017-2311">compactação</span><span class="sxs-lookup"><span data-stu-id="ed017-2311">compression</span></span> | <span data-ttu-id="ed017-2312">Especifica tipo de saudação e nível de compactação de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="ed017-2312">Specify hello type and level of compression for hello data.</span></span> <span data-ttu-id="ed017-2313">Os tipos com suporte são: **GZip**, **Deflate**, **BZip2** e **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="ed017-2313">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="ed017-2314">Os níveis com suporte são **Ideal** e **O mais rápido**.</span><span class="sxs-lookup"><span data-stu-id="ed017-2314">Supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="ed017-2315">Para saber mais, confira [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support) (Formatos de arquivo e de compactação no Azure Data Factory).</span><span class="sxs-lookup"><span data-stu-id="ed017-2315">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="ed017-2316">Não</span><span class="sxs-lookup"><span data-stu-id="ed017-2316">No</span></span> |
| <span data-ttu-id="ed017-2317">useBinaryTransfer</span><span class="sxs-lookup"><span data-stu-id="ed017-2317">useBinaryTransfer</span></span> |<span data-ttu-id="ed017-2318">Especifique se deve usar o modo de transferência Binário.</span><span class="sxs-lookup"><span data-stu-id="ed017-2318">Specify whether use Binary transfer mode.</span></span> <span data-ttu-id="ed017-2319">True para o modo binário e ASCII false.</span><span class="sxs-lookup"><span data-stu-id="ed017-2319">True for binary mode and false ASCII.</span></span> <span data-ttu-id="ed017-2320">Valor padrão: True.</span><span class="sxs-lookup"><span data-stu-id="ed017-2320">Default value: True.</span></span> <span data-ttu-id="ed017-2321">Essa propriedade só pode ser usada quando o tipo de serviço vinculado associado for do tipo: FtpServer.</span><span class="sxs-lookup"><span data-stu-id="ed017-2321">This property can only be used when associated linked service type is of type: FtpServer.</span></span> |<span data-ttu-id="ed017-2322">Não</span><span class="sxs-lookup"><span data-stu-id="ed017-2322">No</span></span> |

> [!NOTE]
> <span data-ttu-id="ed017-2323">filename e fileFilter não podem ser usados simultaneamente.</span><span class="sxs-lookup"><span data-stu-id="ed017-2323">filename and fileFilter cannot be used simultaneously.</span></span>

#### <a name="example"></a><span data-ttu-id="ed017-2324">Exemplo</span><span class="sxs-lookup"><span data-stu-id="ed017-2324">Example</span></span>

```json
{
    "name": "SFTPFileInput",
    "properties": {
        "type": "FileShare",
        "linkedServiceName": "SftpLinkedService",
        "typeProperties": {
            "folderPath": "<path tooshared folder>",
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

<span data-ttu-id="ed017-2325">Para obter mais informações, consulte o artigo [Conector do SFTP](data-factory-sftp-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="ed017-2325">For more information, see [SFTP connector](data-factory-sftp-connector.md#dataset-properties) article.</span></span> 

### <a name="file-system-source-in-copy-activity"></a><span data-ttu-id="ed017-2326">Origem do Sistema de Arquivos na Atividade de Cópia</span><span class="sxs-lookup"><span data-stu-id="ed017-2326">File System Source in Copy Activity</span></span>
<span data-ttu-id="ed017-2327">Se você estiver copiando dados de uma fonte SFTP, defina Olá **tipo de fonte** de hello atividade de cópia muito**FileSystemSource**e especificar propriedades no Olá a seguir **fonte** seção:</span><span class="sxs-lookup"><span data-stu-id="ed017-2327">If you are copying data from an SFTP source, set hello **source type** of hello copy activity too**FileSystemSource**, and specify following properties in hello **source** section:</span></span>

| <span data-ttu-id="ed017-2328">Propriedade</span><span class="sxs-lookup"><span data-stu-id="ed017-2328">Property</span></span> | <span data-ttu-id="ed017-2329">Descrição</span><span class="sxs-lookup"><span data-stu-id="ed017-2329">Description</span></span> | <span data-ttu-id="ed017-2330">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="ed017-2330">Allowed values</span></span> | <span data-ttu-id="ed017-2331">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="ed017-2331">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="ed017-2332">recursiva</span><span class="sxs-lookup"><span data-stu-id="ed017-2332">recursive</span></span> |<span data-ttu-id="ed017-2333">Indica se os dados saudação é lida recursivamente de subpastas de saudação ou somente de pasta especificado hello.</span><span class="sxs-lookup"><span data-stu-id="ed017-2333">Indicates whether hello data is read recursively from hello sub folders or only from hello specified folder.</span></span> |<span data-ttu-id="ed017-2334">True, False (padrão)</span><span class="sxs-lookup"><span data-stu-id="ed017-2334">True, False (default)</span></span> |<span data-ttu-id="ed017-2335">Não</span><span class="sxs-lookup"><span data-stu-id="ed017-2335">No</span></span> |



#### <a name="example"></a><span data-ttu-id="ed017-2336">Exemplo</span><span class="sxs-lookup"><span data-stu-id="ed017-2336">Example</span></span>

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

<span data-ttu-id="ed017-2337">Para obter mais informações, consulte o artigo [Conector do SFTP](data-factory-sftp-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="ed017-2337">For more information, see [SFTP connector](data-factory-sftp-connector.md#copy-activity-properties) article.</span></span>


## <a name="http"></a><span data-ttu-id="ed017-2338">HTTP</span><span class="sxs-lookup"><span data-stu-id="ed017-2338">HTTP</span></span>

### <a name="linked-service"></a><span data-ttu-id="ed017-2339">Serviço vinculado</span><span class="sxs-lookup"><span data-stu-id="ed017-2339">Linked service</span></span>
<span data-ttu-id="ed017-2340">serviço saudação do conjunto vinculado do toodefine um HTTP **tipo** de saudação serviço vinculado muito**Http**e especificar propriedades no Olá a seguir **typeProperties** seção:</span><span class="sxs-lookup"><span data-stu-id="ed017-2340">toodefine a HTTP linked service, set hello **type** of hello linked service too**Http**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="ed017-2341">Propriedade</span><span class="sxs-lookup"><span data-stu-id="ed017-2341">Property</span></span> | <span data-ttu-id="ed017-2342">Descrição</span><span class="sxs-lookup"><span data-stu-id="ed017-2342">Description</span></span> | <span data-ttu-id="ed017-2343">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="ed017-2343">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ed017-2344">url</span><span class="sxs-lookup"><span data-stu-id="ed017-2344">url</span></span> | <span data-ttu-id="ed017-2345">Base de URL toohello servidor Web</span><span class="sxs-lookup"><span data-stu-id="ed017-2345">Base URL toohello Web Server</span></span> | <span data-ttu-id="ed017-2346">Sim</span><span class="sxs-lookup"><span data-stu-id="ed017-2346">Yes</span></span> |
| <span data-ttu-id="ed017-2347">authenticationType</span><span class="sxs-lookup"><span data-stu-id="ed017-2347">authenticationType</span></span> | <span data-ttu-id="ed017-2348">Especifica o tipo de autenticação de saudação.</span><span class="sxs-lookup"><span data-stu-id="ed017-2348">Specifies hello authentication type.</span></span> <span data-ttu-id="ed017-2349">Os valores permitidos são: **Anônimo**, **Básico**, **Digest**, **Windows** e **ClientCertificate**.</span><span class="sxs-lookup"><span data-stu-id="ed017-2349">Allowed values are: **Anonymous**, **Basic**, **Digest**, **Windows**, **ClientCertificate**.</span></span> <br><br> <span data-ttu-id="ed017-2350">Consulte toosections abaixo da tabela em mais propriedades e exemplos JSON para esses tipos de autenticação, respectivamente.</span><span class="sxs-lookup"><span data-stu-id="ed017-2350">Refer toosections below this table on more properties and JSON samples for those authentication types respectively.</span></span> | <span data-ttu-id="ed017-2351">Sim</span><span class="sxs-lookup"><span data-stu-id="ed017-2351">Yes</span></span> |
| <span data-ttu-id="ed017-2352">enableServerCertificateValidation</span><span class="sxs-lookup"><span data-stu-id="ed017-2352">enableServerCertificateValidation</span></span> | <span data-ttu-id="ed017-2353">Especifique se tooenable servidor SSL a validação de certificado se origem for o servidor da Web HTTPS</span><span class="sxs-lookup"><span data-stu-id="ed017-2353">Specify whether tooenable server SSL certificate validation if source is HTTPS Web Server</span></span> | <span data-ttu-id="ed017-2354">Não, o padrão é true</span><span class="sxs-lookup"><span data-stu-id="ed017-2354">No, default is true</span></span> |
| <span data-ttu-id="ed017-2355">gatewayName</span><span class="sxs-lookup"><span data-stu-id="ed017-2355">gatewayName</span></span> | <span data-ttu-id="ed017-2356">Nome da saudação Data Management Gateway tooconnect tooan origem HTTP no local.</span><span class="sxs-lookup"><span data-stu-id="ed017-2356">Name of hello Data Management Gateway tooconnect tooan on-premises HTTP source.</span></span> | <span data-ttu-id="ed017-2357">Sim se estiver copiando dados de uma origem HTTP local.</span><span class="sxs-lookup"><span data-stu-id="ed017-2357">Yes if copying data from an on-premises HTTP source.</span></span> |
| <span data-ttu-id="ed017-2358">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="ed017-2358">encryptedCredential</span></span> | <span data-ttu-id="ed017-2359">Credencial criptografada tooaccess Olá ponto de extremidade HTTP.</span><span class="sxs-lookup"><span data-stu-id="ed017-2359">Encrypted credential tooaccess hello HTTP endpoint.</span></span> <span data-ttu-id="ed017-2360">Gerado automaticamente quando você configura as informações de autenticação de saudação no diálogo de pop-up de ClickOnce de assistente ou saudação de cópia.</span><span class="sxs-lookup"><span data-stu-id="ed017-2360">Auto-generated when you configure hello authentication information in copy wizard or hello ClickOnce popup dialog.</span></span> | <span data-ttu-id="ed017-2361">Não.</span><span class="sxs-lookup"><span data-stu-id="ed017-2361">No.</span></span> <span data-ttu-id="ed017-2362">Aplique somente quando estiver copiando dados de um servidor HTTP local.</span><span class="sxs-lookup"><span data-stu-id="ed017-2362">Apply only when copying data from an on-premises HTTP server.</span></span> |

#### <a name="example-using-basic-digest-or-windows-authentication"></a><span data-ttu-id="ed017-2363">Exemplo: Usando a autenticação Básica, Digest ou Windows</span><span class="sxs-lookup"><span data-stu-id="ed017-2363">Example: Using Basic, Digest, or Windows authentication</span></span>
<span data-ttu-id="ed017-2364">Definir `authenticationType` como `Basic`, `Digest`, ou `Windows`e especifique Olá seguintes propriedades além Olá conector HTTP genérico aqueles introduzido acima:</span><span class="sxs-lookup"><span data-stu-id="ed017-2364">Set `authenticationType` as `Basic`, `Digest`, or `Windows`, and specify hello following properties besides hello HTTP connector generic ones introduced above:</span></span>

| <span data-ttu-id="ed017-2365">Propriedade</span><span class="sxs-lookup"><span data-stu-id="ed017-2365">Property</span></span> | <span data-ttu-id="ed017-2366">Descrição</span><span class="sxs-lookup"><span data-stu-id="ed017-2366">Description</span></span> | <span data-ttu-id="ed017-2367">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="ed017-2367">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ed017-2368">Nome de Usuário</span><span class="sxs-lookup"><span data-stu-id="ed017-2368">username</span></span> | <span data-ttu-id="ed017-2369">Nome de usuário tooaccess Olá ponto de extremidade HTTP.</span><span class="sxs-lookup"><span data-stu-id="ed017-2369">Username tooaccess hello HTTP endpoint.</span></span> | <span data-ttu-id="ed017-2370">Sim</span><span class="sxs-lookup"><span data-stu-id="ed017-2370">Yes</span></span> |
| <span data-ttu-id="ed017-2371">Senha</span><span class="sxs-lookup"><span data-stu-id="ed017-2371">password</span></span> | <span data-ttu-id="ed017-2372">Senha do usuário da saudação (nome de usuário).</span><span class="sxs-lookup"><span data-stu-id="ed017-2372">Password for hello user (username).</span></span> | <span data-ttu-id="ed017-2373">Sim</span><span class="sxs-lookup"><span data-stu-id="ed017-2373">Yes</span></span> |

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

#### <a name="example-using-clientcertificate-authentication"></a><span data-ttu-id="ed017-2374">Exemplo: Usando a autenticação ClientCertificate</span><span class="sxs-lookup"><span data-stu-id="ed017-2374">Example: Using ClientCertificate authentication</span></span>

<span data-ttu-id="ed017-2375">Definir toouse a autenticação básica, `authenticationType` como `ClientCertificate`e especifique Olá seguintes propriedades além Olá conector HTTP genérico aqueles introduzido acima:</span><span class="sxs-lookup"><span data-stu-id="ed017-2375">toouse basic authentication, set `authenticationType` as `ClientCertificate`, and specify hello following properties besides hello HTTP connector generic ones introduced above:</span></span>

| <span data-ttu-id="ed017-2376">Propriedade</span><span class="sxs-lookup"><span data-stu-id="ed017-2376">Property</span></span> | <span data-ttu-id="ed017-2377">Descrição</span><span class="sxs-lookup"><span data-stu-id="ed017-2377">Description</span></span> | <span data-ttu-id="ed017-2378">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="ed017-2378">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ed017-2379">embeddedCertData</span><span class="sxs-lookup"><span data-stu-id="ed017-2379">embeddedCertData</span></span> | <span data-ttu-id="ed017-2380">conteúdo codificado com Base64 Olá de dados binários do arquivo de troca de informações pessoais (PFX) hello.</span><span class="sxs-lookup"><span data-stu-id="ed017-2380">hello Base64-encoded contents of binary data of hello Personal Information Exchange (PFX) file.</span></span> | <span data-ttu-id="ed017-2381">Especifique a saudação `embeddedCertData` ou `certThumbprint`.</span><span class="sxs-lookup"><span data-stu-id="ed017-2381">Specify either hello `embeddedCertData` or `certThumbprint`.</span></span> |
| <span data-ttu-id="ed017-2382">certThumbprint</span><span class="sxs-lookup"><span data-stu-id="ed017-2382">certThumbprint</span></span> | <span data-ttu-id="ed017-2383">Olá a impressão digital do certificado Olá foi instalado no repositório de certificados do computador do gateway.</span><span class="sxs-lookup"><span data-stu-id="ed017-2383">hello thumbprint of hello certificate that was installed on your gateway machine’s cert store.</span></span> <span data-ttu-id="ed017-2384">Aplique somente ao copiar dados de uma origem HTTP local.</span><span class="sxs-lookup"><span data-stu-id="ed017-2384">Apply only when copying data from an on-premises HTTP source.</span></span> | <span data-ttu-id="ed017-2385">Especifique a saudação `embeddedCertData` ou `certThumbprint`.</span><span class="sxs-lookup"><span data-stu-id="ed017-2385">Specify either hello `embeddedCertData` or `certThumbprint`.</span></span> |
| <span data-ttu-id="ed017-2386">Senha</span><span class="sxs-lookup"><span data-stu-id="ed017-2386">password</span></span> | <span data-ttu-id="ed017-2387">Senha associada com o certificado de saudação.</span><span class="sxs-lookup"><span data-stu-id="ed017-2387">Password associated with hello certificate.</span></span> | <span data-ttu-id="ed017-2388">Não</span><span class="sxs-lookup"><span data-stu-id="ed017-2388">No</span></span> |

<span data-ttu-id="ed017-2389">Se você usar `certThumbprint` para certificado de autenticação e hello está instalado no repositório pessoal de saudação do computador local hello, você precisa que o serviço de gateway do toogrant Olá permissão de leitura toohello:</span><span class="sxs-lookup"><span data-stu-id="ed017-2389">If you use `certThumbprint` for authentication and hello certificate is installed in hello personal store of hello local computer, you need toogrant hello read permission toohello gateway service:</span></span>

1. <span data-ttu-id="ed017-2390">Iniciar o MMC (Console de Gerenciamento Microsoft).</span><span class="sxs-lookup"><span data-stu-id="ed017-2390">Launch Microsoft Management Console (MMC).</span></span> <span data-ttu-id="ed017-2391">Adicionar Olá **certificados** snap-in que Olá destinos **computador Local**.</span><span class="sxs-lookup"><span data-stu-id="ed017-2391">Add hello **Certificates** snap-in that targets hello **Local Computer**.</span></span>
2. <span data-ttu-id="ed017-2392">Expanda **Certificados**, **Pessoal** e clique em **Certificados**.</span><span class="sxs-lookup"><span data-stu-id="ed017-2392">Expand **Certificates**, **Personal**, and click **Certificates**.</span></span>
3. <span data-ttu-id="ed017-2393">Certificado de saudação do armazenamento pessoal hello e selecione **todas as tarefas**->**gerenciar chaves particulares...**</span><span class="sxs-lookup"><span data-stu-id="ed017-2393">Right-click hello certificate from hello personal store, and select **All Tasks**->**Manage Private Keys...**</span></span>
3. <span data-ttu-id="ed017-2394">Em Olá **segurança** guia, adicione a conta de usuário Olá sob a qual o serviço de Host do Gateway de gerenciamento de dados está em execução com certificado de toohello Olá acesso de leitura.</span><span class="sxs-lookup"><span data-stu-id="ed017-2394">On hello **Security** tab, add hello user account under which Data Management Gateway Host Service is running with hello read access toohello certificate.</span></span>  

<span data-ttu-id="ed017-2395">**Exemplo: usando o certificado de cliente:** isso vinculado links serviço seu servidor de web data factory tooan locais HTTP.</span><span class="sxs-lookup"><span data-stu-id="ed017-2395">**Example: using client certificate:** This linked service links your data factory tooan on-premises HTTP web server.</span></span> <span data-ttu-id="ed017-2396">Ele usa um certificado de cliente é instalado na máquina de saudação com Gateway de gerenciamento de dados instalado.</span><span class="sxs-lookup"><span data-stu-id="ed017-2396">It uses a client certificate that is installed on hello machine with Data Management Gateway installed.</span></span>

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

#### <a name="example-using-client-certificate-in-a-file"></a><span data-ttu-id="ed017-2397">Exemplo: usando o certificado do cliente em um arquivo</span><span class="sxs-lookup"><span data-stu-id="ed017-2397">Example: using client certificate in a file</span></span>
<span data-ttu-id="ed017-2398">Isso vinculado links serviço seu servidor de web data factory tooan locais HTTP.</span><span class="sxs-lookup"><span data-stu-id="ed017-2398">This linked service links your data factory tooan on-premises HTTP web server.</span></span> <span data-ttu-id="ed017-2399">Ele usa um arquivo de certificado de cliente no computador de saudação com Gateway de gerenciamento de dados instalado.</span><span class="sxs-lookup"><span data-stu-id="ed017-2399">It uses a client certificate file on hello machine with Data Management Gateway installed.</span></span>

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

<span data-ttu-id="ed017-2400">Para obter mais informações, consulte o artigo [Conector do HTTP](data-factory-http-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="ed017-2400">For more information, see [HTTP connector](data-factory-http-connector.md#linked-service-properties) article.</span></span>

### <a name="dataset"></a><span data-ttu-id="ed017-2401">Conjunto de dados</span><span class="sxs-lookup"><span data-stu-id="ed017-2401">Dataset</span></span>
<span data-ttu-id="ed017-2402">toodefine um HTTP de conjunto de dados, conjunto Olá **tipo** do conjunto de dados de saudação muito**Http**e especifique Olá seguintes propriedades em Olá **typeProperties** seção:</span><span class="sxs-lookup"><span data-stu-id="ed017-2402">toodefine a HTTP dataset, set hello **type** of hello dataset too**Http**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="ed017-2403">Propriedade</span><span class="sxs-lookup"><span data-stu-id="ed017-2403">Property</span></span> | <span data-ttu-id="ed017-2404">Descrição</span><span class="sxs-lookup"><span data-stu-id="ed017-2404">Description</span></span> | <span data-ttu-id="ed017-2405">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="ed017-2405">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="ed017-2406">relativeUrl</span><span class="sxs-lookup"><span data-stu-id="ed017-2406">relativeUrl</span></span> | <span data-ttu-id="ed017-2407">Um relativa URL toohello de recursos que contém dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="ed017-2407">A relative URL toohello resource that contains hello data.</span></span> <span data-ttu-id="ed017-2408">Quando não for especificado, somente URL Olá especificado na definição de serviço vinculada de saudação é usado.</span><span class="sxs-lookup"><span data-stu-id="ed017-2408">When path is not specified, only hello URL specified in hello linked service definition is used.</span></span> <br><br> <span data-ttu-id="ed017-2409">URL do tooconstruct dinâmico, você pode usar [funções da fábrica de dados e variáveis de sistema](data-factory-functions-variables.md), exemplo: `"relativeUrl": "$$Text.Format('/my/report?month={0:yyyy}-{0:MM}&fmt=csv', SliceStart)"`.</span><span class="sxs-lookup"><span data-stu-id="ed017-2409">tooconstruct dynamic URL, you can use [Data Factory functions and system variables](data-factory-functions-variables.md), Example: `"relativeUrl": "$$Text.Format('/my/report?month={0:yyyy}-{0:MM}&fmt=csv', SliceStart)"`.</span></span> | <span data-ttu-id="ed017-2410">Não</span><span class="sxs-lookup"><span data-stu-id="ed017-2410">No</span></span> |
| <span data-ttu-id="ed017-2411">requestMethod</span><span class="sxs-lookup"><span data-stu-id="ed017-2411">requestMethod</span></span> | <span data-ttu-id="ed017-2412">Método Http.</span><span class="sxs-lookup"><span data-stu-id="ed017-2412">Http method.</span></span> <span data-ttu-id="ed017-2413">Os valores permitidos são **GET** ou **POST**.</span><span class="sxs-lookup"><span data-stu-id="ed017-2413">Allowed values are **GET** or **POST**.</span></span> | <span data-ttu-id="ed017-2414">Não.</span><span class="sxs-lookup"><span data-stu-id="ed017-2414">No.</span></span> <span data-ttu-id="ed017-2415">O padrão é `GET`.</span><span class="sxs-lookup"><span data-stu-id="ed017-2415">Default is `GET`.</span></span> |
| <span data-ttu-id="ed017-2416">additionalHeaders</span><span class="sxs-lookup"><span data-stu-id="ed017-2416">additionalHeaders</span></span> | <span data-ttu-id="ed017-2417">Cabeçalhos de solicitação HTTP adicionais.</span><span class="sxs-lookup"><span data-stu-id="ed017-2417">Additional HTTP request headers.</span></span> | <span data-ttu-id="ed017-2418">Não</span><span class="sxs-lookup"><span data-stu-id="ed017-2418">No</span></span> |
| <span data-ttu-id="ed017-2419">requestBody</span><span class="sxs-lookup"><span data-stu-id="ed017-2419">requestBody</span></span> | <span data-ttu-id="ed017-2420">O corpo da solicitação HTTP.</span><span class="sxs-lookup"><span data-stu-id="ed017-2420">Body for HTTP request.</span></span> | <span data-ttu-id="ed017-2421">Não</span><span class="sxs-lookup"><span data-stu-id="ed017-2421">No</span></span> |
| <span data-ttu-id="ed017-2422">formato</span><span class="sxs-lookup"><span data-stu-id="ed017-2422">format</span></span> | <span data-ttu-id="ed017-2423">Se você quiser toosimply **recuperar dados de saudação do ponto de extremidade HTTP como-é** sem analisá-lo, ignore essa configuração de formato.</span><span class="sxs-lookup"><span data-stu-id="ed017-2423">If you want toosimply **retrieve hello data from HTTP endpoint as-is** without parsing it, skip this format settings.</span></span> <br><br> <span data-ttu-id="ed017-2424">Se você quiser resposta HTTP de saudação tooparse conteúdo durante a cópia, Olá tipos de formato a seguir têm suporte: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="ed017-2424">If you want tooparse hello HTTP response content during copy, hello following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="ed017-2425">Para saber mais, veja as seções [Formato de texto](data-factory-supported-file-and-compression-formats.md#text-format), [Formato Json](data-factory-supported-file-and-compression-formats.md#json-format), [Formato Avro](data-factory-supported-file-and-compression-formats.md#avro-format), [Formato Orc](data-factory-supported-file-and-compression-formats.md#orc-format), e [Formato Parquet](data-factory-supported-file-and-compression-formats.md#parquet-format).</span><span class="sxs-lookup"><span data-stu-id="ed017-2425">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> |<span data-ttu-id="ed017-2426">Não</span><span class="sxs-lookup"><span data-stu-id="ed017-2426">No</span></span> |
| <span data-ttu-id="ed017-2427">compactação</span><span class="sxs-lookup"><span data-stu-id="ed017-2427">compression</span></span> | <span data-ttu-id="ed017-2428">Especifica tipo de saudação e nível de compactação de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="ed017-2428">Specify hello type and level of compression for hello data.</span></span> <span data-ttu-id="ed017-2429">Os tipos com suporte são: **GZip**, **Deflate**, **BZip2** e **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="ed017-2429">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="ed017-2430">Os níveis com suporte são **Ideal** e **O mais rápido**.</span><span class="sxs-lookup"><span data-stu-id="ed017-2430">Supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="ed017-2431">Para saber mais, confira [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support) (Formatos de arquivo e de compactação no Azure Data Factory).</span><span class="sxs-lookup"><span data-stu-id="ed017-2431">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="ed017-2432">Não</span><span class="sxs-lookup"><span data-stu-id="ed017-2432">No</span></span> |

#### <a name="example-using-hello-get-default-method"></a><span data-ttu-id="ed017-2433">Exemplo: usando o método do hello GET (padrão)</span><span class="sxs-lookup"><span data-stu-id="ed017-2433">Example: using hello GET (default) method</span></span>

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

#### <a name="example-using-hello-post-method"></a><span data-ttu-id="ed017-2434">Exemplo: usando o método POST de saudação</span><span class="sxs-lookup"><span data-stu-id="ed017-2434">Example: using hello POST method</span></span>

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
<span data-ttu-id="ed017-2435">Para obter mais informações, consulte o artigo [Conector do HTTP](data-factory-http-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="ed017-2435">For more information, see [HTTP connector](data-factory-http-connector.md#dataset-properties) article.</span></span>

### <a name="http-source-in-copy-activity"></a><span data-ttu-id="ed017-2436">Origem do HTTP na Atividade de Cópia</span><span class="sxs-lookup"><span data-stu-id="ed017-2436">HTTP Source in Copy Activity</span></span>
<span data-ttu-id="ed017-2437">Se você estiver copiando dados de uma fonte HTTP, defina Olá **tipo de fonte** de hello atividade de cópia muito**HttpSource**e especificar propriedades no Olá a seguir **fonte** seção:</span><span class="sxs-lookup"><span data-stu-id="ed017-2437">If you are copying data from a HTTP source, set hello **source type** of hello copy activity too**HttpSource**, and specify following properties in hello **source** section:</span></span>

| <span data-ttu-id="ed017-2438">Propriedade</span><span class="sxs-lookup"><span data-stu-id="ed017-2438">Property</span></span> | <span data-ttu-id="ed017-2439">Descrição</span><span class="sxs-lookup"><span data-stu-id="ed017-2439">Description</span></span> | <span data-ttu-id="ed017-2440">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="ed017-2440">Required</span></span> |
| -------- | ----------- | -------- |
| <span data-ttu-id="ed017-2441">httpRequestTimeout</span><span class="sxs-lookup"><span data-stu-id="ed017-2441">httpRequestTimeout</span></span> | <span data-ttu-id="ed017-2442">Olá tempo limite (TimeSpan) para tooget de solicitação HTTP Olá uma resposta.</span><span class="sxs-lookup"><span data-stu-id="ed017-2442">hello timeout (TimeSpan) for hello HTTP request tooget a response.</span></span> <span data-ttu-id="ed017-2443">É Olá timeout tooget uma resposta não Olá timeout tooread dados de resposta.</span><span class="sxs-lookup"><span data-stu-id="ed017-2443">It is hello timeout tooget a response, not hello timeout tooread response data.</span></span> | <span data-ttu-id="ed017-2444">Não.</span><span class="sxs-lookup"><span data-stu-id="ed017-2444">No.</span></span> <span data-ttu-id="ed017-2445">Valor padrão: 00:01:40</span><span class="sxs-lookup"><span data-stu-id="ed017-2445">Default value: 00:01:40</span></span> |


#### <a name="example"></a><span data-ttu-id="ed017-2446">Exemplo</span><span class="sxs-lookup"><span data-stu-id="ed017-2446">Example</span></span>

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "HttpSourceToAzureBlob",
            "description": "Copy from an HTTP source tooan Azure blob",
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

<span data-ttu-id="ed017-2447">Para obter mais informações, consulte o artigo [Conector do HTTP](data-factory-http-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="ed017-2447">For more information, see [HTTP connector](data-factory-http-connector.md#copy-activity-properties) article.</span></span>

## <a name="odata"></a><span data-ttu-id="ed017-2448">OData</span><span class="sxs-lookup"><span data-stu-id="ed017-2448">OData</span></span>

### <a name="linked-service"></a><span data-ttu-id="ed017-2449">Serviço vinculado</span><span class="sxs-lookup"><span data-stu-id="ed017-2449">Linked service</span></span>
<span data-ttu-id="ed017-2450">toodefine OData vinculado serviço, Olá conjunto **tipo** de saudação serviço vinculado muito**OData**e especificar propriedades no Olá a seguir **typeProperties** seção:</span><span class="sxs-lookup"><span data-stu-id="ed017-2450">toodefine an OData linked service, set hello **type** of hello linked service too**OData**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="ed017-2451">Propriedade</span><span class="sxs-lookup"><span data-stu-id="ed017-2451">Property</span></span> | <span data-ttu-id="ed017-2452">Descrição</span><span class="sxs-lookup"><span data-stu-id="ed017-2452">Description</span></span> | <span data-ttu-id="ed017-2453">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="ed017-2453">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ed017-2454">url</span><span class="sxs-lookup"><span data-stu-id="ed017-2454">url</span></span> |<span data-ttu-id="ed017-2455">URL da saudação serviço OData.</span><span class="sxs-lookup"><span data-stu-id="ed017-2455">Url of hello OData service.</span></span> |<span data-ttu-id="ed017-2456">Sim</span><span class="sxs-lookup"><span data-stu-id="ed017-2456">Yes</span></span> |
| <span data-ttu-id="ed017-2457">authenticationType</span><span class="sxs-lookup"><span data-stu-id="ed017-2457">authenticationType</span></span> |<span data-ttu-id="ed017-2458">Tipo de autenticação usado tooconnect toohello OData source.</span><span class="sxs-lookup"><span data-stu-id="ed017-2458">Type of authentication used tooconnect toohello OData source.</span></span> <br/><br/> <span data-ttu-id="ed017-2459">Para o OData de nuvem, os valores possíveis são Anônimo, Básico e OAuth (observe que o Azure Data Factory dá suporte no momento apenas a OAuth baseado no Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="ed017-2459">For cloud OData, possible values are Anonymous, Basic, and OAuth (note Azure Data Factory currently only support Azure Active Directory based OAuth).</span></span> <br/><br/> <span data-ttu-id="ed017-2460">Para OData local, os valores possíveis são Anonymous, Basic e Windows.</span><span class="sxs-lookup"><span data-stu-id="ed017-2460">For on-premises OData, possible values are Anonymous, Basic, and Windows.</span></span> |<span data-ttu-id="ed017-2461">Sim</span><span class="sxs-lookup"><span data-stu-id="ed017-2461">Yes</span></span> |
| <span data-ttu-id="ed017-2462">Nome de Usuário</span><span class="sxs-lookup"><span data-stu-id="ed017-2462">username</span></span> |<span data-ttu-id="ed017-2463">Especifique o nome de usuário se você estiver usando a autenticação Básica.</span><span class="sxs-lookup"><span data-stu-id="ed017-2463">Specify user name if you are using Basic authentication.</span></span> |<span data-ttu-id="ed017-2464">Sim (apenas se você estiver usando a autenticação Básica)</span><span class="sxs-lookup"><span data-stu-id="ed017-2464">Yes (only if you are using Basic authentication)</span></span> |
| <span data-ttu-id="ed017-2465">Senha</span><span class="sxs-lookup"><span data-stu-id="ed017-2465">password</span></span> |<span data-ttu-id="ed017-2466">Especifique a senha da conta de usuário de saudação especificado para nome de usuário de saudação.</span><span class="sxs-lookup"><span data-stu-id="ed017-2466">Specify password for hello user account you specified for hello username.</span></span> |<span data-ttu-id="ed017-2467">Sim (apenas se você estiver usando a autenticação Básica)</span><span class="sxs-lookup"><span data-stu-id="ed017-2467">Yes (only if you are using Basic authentication)</span></span> |
| <span data-ttu-id="ed017-2468">authorizedCredential</span><span class="sxs-lookup"><span data-stu-id="ed017-2468">authorizedCredential</span></span> |<span data-ttu-id="ed017-2469">Se você estiver usando o OAuth, clique em **autorizar** botão no hello Assistente para cópia de fábrica de dados ou no Editor e insira suas credenciais, valor Olá dessa propriedade será gerado automaticamente.</span><span class="sxs-lookup"><span data-stu-id="ed017-2469">If you are using OAuth, click **Authorize** button in hello Data Factory Copy Wizard or Editor and enter your credential, then hello value of this property will be auto-generated.</span></span> |<span data-ttu-id="ed017-2470">Sim (apenas se você estiver usando a autenticação OAuth)</span><span class="sxs-lookup"><span data-stu-id="ed017-2470">Yes (only if you are using OAuth authentication)</span></span> |
| <span data-ttu-id="ed017-2471">gatewayName</span><span class="sxs-lookup"><span data-stu-id="ed017-2471">gatewayName</span></span> |<span data-ttu-id="ed017-2472">Nome do gateway Olá Olá serviço da fábrica de dados deve usar um serviço OData do tooconnect toohello local.</span><span class="sxs-lookup"><span data-stu-id="ed017-2472">Name of hello gateway that hello Data Factory service should use tooconnect toohello on-premises OData service.</span></span> <span data-ttu-id="ed017-2473">Só especifique se você estiver copiando dados da fonte OData local.</span><span class="sxs-lookup"><span data-stu-id="ed017-2473">Specify only if you are copying data from on-prem OData source.</span></span> |<span data-ttu-id="ed017-2474">Não</span><span class="sxs-lookup"><span data-stu-id="ed017-2474">No</span></span> |

#### <a name="example---using-basic-authentication"></a><span data-ttu-id="ed017-2475">Exemplo - Usando a autenticação básica</span><span class="sxs-lookup"><span data-stu-id="ed017-2475">Example - Using Basic authentication</span></span>
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

#### <a name="example---using-anonymous-authentication"></a><span data-ttu-id="ed017-2476">Exemplo - Usando a autenticação anônima</span><span class="sxs-lookup"><span data-stu-id="ed017-2476">Example - Using Anonymous authentication</span></span>

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

#### <a name="example---using-windows-authentication-accessing-on-premises-odata-source"></a><span data-ttu-id="ed017-2477">Exemplo - Usando a autenticação do Windows para acessar uma origem de OData local</span><span class="sxs-lookup"><span data-stu-id="ed017-2477">Example - Using Windows authentication accessing on-premises OData source</span></span>

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

#### <a name="example---using-oauth-authentication-accessing-cloud-odata-source"></a><span data-ttu-id="ed017-2478">Exemplo - Usando autenticação OAuth para acessar a origem de OData da nuvem</span><span class="sxs-lookup"><span data-stu-id="ed017-2478">Example - Using OAuth authentication accessing cloud OData source</span></span>
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
            "authorizedCredential": "<auto generated by clicking hello Authorize button on UI>"
        }
    }
}
```

<span data-ttu-id="ed017-2479">Para obter mais informações, consulte o artigo [Conector do OData](data-factory-odata-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="ed017-2479">For more information, see [OData connector](data-factory-odata-connector.md#linked-service-properties) article.</span></span>

### <a name="dataset"></a><span data-ttu-id="ed017-2480">Conjunto de dados</span><span class="sxs-lookup"><span data-stu-id="ed017-2480">Dataset</span></span>
<span data-ttu-id="ed017-2481">toodefine um conjunto de dados OData, Olá conjunto **tipo** do conjunto de dados de saudação muito**ODataResource**e especifique Olá seguintes propriedades em Olá **typeProperties** seção:</span><span class="sxs-lookup"><span data-stu-id="ed017-2481">toodefine an OData dataset, set hello **type** of hello dataset too**ODataResource**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="ed017-2482">Propriedade</span><span class="sxs-lookup"><span data-stu-id="ed017-2482">Property</span></span> | <span data-ttu-id="ed017-2483">Descrição</span><span class="sxs-lookup"><span data-stu-id="ed017-2483">Description</span></span> | <span data-ttu-id="ed017-2484">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="ed017-2484">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ed017-2485">path</span><span class="sxs-lookup"><span data-stu-id="ed017-2485">path</span></span> |<span data-ttu-id="ed017-2486">Caminho toohello recurso do OData</span><span class="sxs-lookup"><span data-stu-id="ed017-2486">Path toohello OData resource</span></span> |<span data-ttu-id="ed017-2487">Não</span><span class="sxs-lookup"><span data-stu-id="ed017-2487">No</span></span> |

#### <a name="example"></a><span data-ttu-id="ed017-2488">Exemplo</span><span class="sxs-lookup"><span data-stu-id="ed017-2488">Example</span></span>

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

<span data-ttu-id="ed017-2489">Para obter mais informações, consulte o artigo [Conector do OData](data-factory-odata-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="ed017-2489">For more information, see [OData connector](data-factory-odata-connector.md#dataset-properties) article.</span></span>

### <a name="relational-source-in-copy-activity"></a><span data-ttu-id="ed017-2490">Origem Relacional na Atividade de Cópia</span><span class="sxs-lookup"><span data-stu-id="ed017-2490">Relational Source in Copy Activity</span></span>
<span data-ttu-id="ed017-2491">Se você estiver copiando dados de uma fonte OData, defina Olá **tipo de fonte** de hello atividade de cópia muito**RelationalSource**e especificar propriedades no Olá a seguir **fonte** seção:</span><span class="sxs-lookup"><span data-stu-id="ed017-2491">If you are copying data from an OData source, set hello **source type** of hello copy activity too**RelationalSource**, and specify following properties in hello **source** section:</span></span>

| <span data-ttu-id="ed017-2492">Propriedade</span><span class="sxs-lookup"><span data-stu-id="ed017-2492">Property</span></span> | <span data-ttu-id="ed017-2493">Descrição</span><span class="sxs-lookup"><span data-stu-id="ed017-2493">Description</span></span> | <span data-ttu-id="ed017-2494">Exemplo</span><span class="sxs-lookup"><span data-stu-id="ed017-2494">Example</span></span> | <span data-ttu-id="ed017-2495">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="ed017-2495">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="ed017-2496">query</span><span class="sxs-lookup"><span data-stu-id="ed017-2496">query</span></span> |<span data-ttu-id="ed017-2497">Use dados de tooread Olá consulta personalizada.</span><span class="sxs-lookup"><span data-stu-id="ed017-2497">Use hello custom query tooread data.</span></span> |<span data-ttu-id="ed017-2498">"?$select=Name, Description&$top=5"</span><span class="sxs-lookup"><span data-stu-id="ed017-2498">"?$select=Name, Description&$top=5"</span></span> |<span data-ttu-id="ed017-2499">Não</span><span class="sxs-lookup"><span data-stu-id="ed017-2499">No</span></span> |

#### <a name="example"></a><span data-ttu-id="ed017-2500">Exemplo</span><span class="sxs-lookup"><span data-stu-id="ed017-2500">Example</span></span>

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

<span data-ttu-id="ed017-2501">Para obter mais informações, consulte o artigo [Conector do OData](data-factory-odata-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="ed017-2501">For more information, see [OData connector](data-factory-odata-connector.md#copy-activity-properties) article.</span></span>


## <a name="odbc"></a><span data-ttu-id="ed017-2502">ODBC</span><span class="sxs-lookup"><span data-stu-id="ed017-2502">ODBC</span></span>


### <a name="linked-service"></a><span data-ttu-id="ed017-2503">Serviço vinculado</span><span class="sxs-lookup"><span data-stu-id="ed017-2503">Linked service</span></span>
<span data-ttu-id="ed017-2504">toodefine ODBC vinculado serviço, Olá conjunto **tipo** de saudação serviço vinculado muito**OnPremisesOdbc**e especificar propriedades no Olá a seguir **typeProperties** seção:</span><span class="sxs-lookup"><span data-stu-id="ed017-2504">toodefine an ODBC linked service, set hello **type** of hello linked service too**OnPremisesOdbc**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="ed017-2505">Propriedade</span><span class="sxs-lookup"><span data-stu-id="ed017-2505">Property</span></span> | <span data-ttu-id="ed017-2506">Descrição</span><span class="sxs-lookup"><span data-stu-id="ed017-2506">Description</span></span> | <span data-ttu-id="ed017-2507">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="ed017-2507">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ed017-2508">connectionString</span><span class="sxs-lookup"><span data-stu-id="ed017-2508">connectionString</span></span> |<span data-ttu-id="ed017-2509">Olá credencial de acesso não parte de cadeia de caracteres de conexão hello e opcional criptografados credencial.</span><span class="sxs-lookup"><span data-stu-id="ed017-2509">hello non-access credential portion of hello connection string and an optional encrypted credential.</span></span> <span data-ttu-id="ed017-2510">Consulte exemplos Olá seções a seguir.</span><span class="sxs-lookup"><span data-stu-id="ed017-2510">See examples in hello following sections.</span></span> |<span data-ttu-id="ed017-2511">Sim</span><span class="sxs-lookup"><span data-stu-id="ed017-2511">Yes</span></span> |
| <span data-ttu-id="ed017-2512">credencial</span><span class="sxs-lookup"><span data-stu-id="ed017-2512">credential</span></span> |<span data-ttu-id="ed017-2513">parte de credencial de acesso Olá de cadeia de caracteres de conexão de saudação especificada no formato de valor de propriedade específica do driver.</span><span class="sxs-lookup"><span data-stu-id="ed017-2513">hello access credential portion of hello connection string specified in driver-specific property-value format.</span></span> <span data-ttu-id="ed017-2514">Exemplo: "Uid=<user ID>;Pwd=<password>;RefreshToken=<secret refresh token>;".</span><span class="sxs-lookup"><span data-stu-id="ed017-2514">Example: “Uid=<user ID>;Pwd=<password>;RefreshToken=<secret refresh token>;”.</span></span> |<span data-ttu-id="ed017-2515">Não</span><span class="sxs-lookup"><span data-stu-id="ed017-2515">No</span></span> |
| <span data-ttu-id="ed017-2516">authenticationType</span><span class="sxs-lookup"><span data-stu-id="ed017-2516">authenticationType</span></span> |<span data-ttu-id="ed017-2517">Tipo de autenticação usado o repositório de dados ODBC tooconnect toohello.</span><span class="sxs-lookup"><span data-stu-id="ed017-2517">Type of authentication used tooconnect toohello ODBC data store.</span></span> <span data-ttu-id="ed017-2518">Os valores possíveis são: Anonymous e Basic.</span><span class="sxs-lookup"><span data-stu-id="ed017-2518">Possible values are: Anonymous and Basic.</span></span> |<span data-ttu-id="ed017-2519">Sim</span><span class="sxs-lookup"><span data-stu-id="ed017-2519">Yes</span></span> |
| <span data-ttu-id="ed017-2520">Nome de Usuário</span><span class="sxs-lookup"><span data-stu-id="ed017-2520">username</span></span> |<span data-ttu-id="ed017-2521">Especifique o nome de usuário se você estiver usando a autenticação Básica.</span><span class="sxs-lookup"><span data-stu-id="ed017-2521">Specify user name if you are using Basic authentication.</span></span> |<span data-ttu-id="ed017-2522">Não</span><span class="sxs-lookup"><span data-stu-id="ed017-2522">No</span></span> |
| <span data-ttu-id="ed017-2523">Senha</span><span class="sxs-lookup"><span data-stu-id="ed017-2523">password</span></span> |<span data-ttu-id="ed017-2524">Especifique a senha da conta de usuário de saudação especificado para nome de usuário de saudação.</span><span class="sxs-lookup"><span data-stu-id="ed017-2524">Specify password for hello user account you specified for hello username.</span></span> |<span data-ttu-id="ed017-2525">Não</span><span class="sxs-lookup"><span data-stu-id="ed017-2525">No</span></span> |
| <span data-ttu-id="ed017-2526">gatewayName</span><span class="sxs-lookup"><span data-stu-id="ed017-2526">gatewayName</span></span> |<span data-ttu-id="ed017-2527">Nome do gateway Olá Olá serviço da fábrica de dados deve usar armazenamento de dados ODBC tooconnect toohello.</span><span class="sxs-lookup"><span data-stu-id="ed017-2527">Name of hello gateway that hello Data Factory service should use tooconnect toohello ODBC data store.</span></span> |<span data-ttu-id="ed017-2528">Sim</span><span class="sxs-lookup"><span data-stu-id="ed017-2528">Yes</span></span> |

#### <a name="example---using-basic-authentication"></a><span data-ttu-id="ed017-2529">Exemplo - Usando a autenticação básica</span><span class="sxs-lookup"><span data-stu-id="ed017-2529">Example - Using Basic authentication</span></span>

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
#### <a name="example---using-basic-authentication-with-encrypted-credentials"></a><span data-ttu-id="ed017-2530">Exemplo - Usando a autenticação básica com credenciais criptografadas</span><span class="sxs-lookup"><span data-stu-id="ed017-2530">Example - Using Basic authentication with encrypted credentials</span></span>
<span data-ttu-id="ed017-2531">Você pode criptografar credenciais Olá Olá [New-AzureRMDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) cmdlet (1.0 versão do Azure PowerShell) ou [New-AzureDataFactoryEncryptValue](https://msdn.microsoft.com/library/dn834940.aspx) (0,9 versão ou anterior do hello PowerShell do Azure).</span><span class="sxs-lookup"><span data-stu-id="ed017-2531">You can encrypt hello credentials using hello [New-AzureRMDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) (1.0 version of Azure PowerShell) cmdlet or [New-AzureDataFactoryEncryptValue](https://msdn.microsoft.com/library/dn834940.aspx) (0.9 or earlier version of hello Azure PowerShell).</span></span>  

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

#### <a name="example-using-anonymous-authentication"></a><span data-ttu-id="ed017-2532">Exemplo: Usando a autenticação anônima</span><span class="sxs-lookup"><span data-stu-id="ed017-2532">Example: Using Anonymous authentication</span></span>

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

<span data-ttu-id="ed017-2533">Para obter mais informações, consulte o artigo [Conector do ODBC](data-factory-odbc-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="ed017-2533">For more information, see [ODBC connector](data-factory-odbc-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="ed017-2534">Conjunto de dados</span><span class="sxs-lookup"><span data-stu-id="ed017-2534">Dataset</span></span>
<span data-ttu-id="ed017-2535">toodefine um conjunto de dados ODBC, Olá conjunto **tipo** do conjunto de dados de saudação muito**RelationalTable**e especifique Olá seguintes propriedades em Olá **typeProperties** seção:</span><span class="sxs-lookup"><span data-stu-id="ed017-2535">toodefine an ODBC dataset, set hello **type** of hello dataset too**RelationalTable**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="ed017-2536">Propriedade</span><span class="sxs-lookup"><span data-stu-id="ed017-2536">Property</span></span> | <span data-ttu-id="ed017-2537">Descrição</span><span class="sxs-lookup"><span data-stu-id="ed017-2537">Description</span></span> | <span data-ttu-id="ed017-2538">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="ed017-2538">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ed017-2539">tableName</span><span class="sxs-lookup"><span data-stu-id="ed017-2539">tableName</span></span> |<span data-ttu-id="ed017-2540">Nome da tabela de saudação no repositório de dados ODBC hello.</span><span class="sxs-lookup"><span data-stu-id="ed017-2540">Name of hello table in hello ODBC data store.</span></span> |<span data-ttu-id="ed017-2541">Sim</span><span class="sxs-lookup"><span data-stu-id="ed017-2541">Yes</span></span> |


#### <a name="example"></a><span data-ttu-id="ed017-2542">Exemplo</span><span class="sxs-lookup"><span data-stu-id="ed017-2542">Example</span></span>

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

<span data-ttu-id="ed017-2543">Para obter mais informações, consulte o artigo [Conector do ODBC](data-factory-odbc-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="ed017-2543">For more information, see [ODBC connector](data-factory-odbc-connector.md#dataset-properties) article.</span></span> 

### <a name="relational-source-in-copy-activity"></a><span data-ttu-id="ed017-2544">Origem Relacional na Atividade de Cópia</span><span class="sxs-lookup"><span data-stu-id="ed017-2544">Relational Source in Copy Activity</span></span>
<span data-ttu-id="ed017-2545">Se você estiver copiando dados de um repositório de dados ODBC, defina Olá **tipo de fonte** de hello atividade de cópia muito**RelationalSource**e especificar propriedades no Olá a seguir **fonte** seção:</span><span class="sxs-lookup"><span data-stu-id="ed017-2545">If you are copying data from an ODBC data store, set hello **source type** of hello copy activity too**RelationalSource**, and specify following properties in hello **source** section:</span></span>

| <span data-ttu-id="ed017-2546">Propriedade</span><span class="sxs-lookup"><span data-stu-id="ed017-2546">Property</span></span> | <span data-ttu-id="ed017-2547">Descrição</span><span class="sxs-lookup"><span data-stu-id="ed017-2547">Description</span></span> | <span data-ttu-id="ed017-2548">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="ed017-2548">Allowed values</span></span> | <span data-ttu-id="ed017-2549">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="ed017-2549">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="ed017-2550">query</span><span class="sxs-lookup"><span data-stu-id="ed017-2550">query</span></span> |<span data-ttu-id="ed017-2551">Use dados de tooread Olá consulta personalizada.</span><span class="sxs-lookup"><span data-stu-id="ed017-2551">Use hello custom query tooread data.</span></span> |<span data-ttu-id="ed017-2552">Cadeia de caracteres de consulta SQL.</span><span class="sxs-lookup"><span data-stu-id="ed017-2552">SQL query string.</span></span> <span data-ttu-id="ed017-2553">Por exemplo: `select * from MyTable`.</span><span class="sxs-lookup"><span data-stu-id="ed017-2553">For example: `select * from MyTable`.</span></span> |<span data-ttu-id="ed017-2554">Sim</span><span class="sxs-lookup"><span data-stu-id="ed017-2554">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="ed017-2555">Exemplo</span><span class="sxs-lookup"><span data-stu-id="ed017-2555">Example</span></span>

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

<span data-ttu-id="ed017-2556">Para obter mais informações, consulte o artigo [Conector do ODBC](data-factory-odbc-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="ed017-2556">For more information, see [ODBC connector](data-factory-odbc-connector.md#copy-activity-properties) article.</span></span>

## <a name="salesforce"></a><span data-ttu-id="ed017-2557">Salesforce</span><span class="sxs-lookup"><span data-stu-id="ed017-2557">Salesforce</span></span>


### <a name="linked-service"></a><span data-ttu-id="ed017-2558">Serviço vinculado</span><span class="sxs-lookup"><span data-stu-id="ed017-2558">Linked service</span></span>
<span data-ttu-id="ed017-2559">toodefine Salesforce o serviço saudação do conjunto vinculado **tipo** de saudação serviço vinculado muito**Salesforce**e especificar propriedades no Olá a seguir **typeProperties** seção:</span><span class="sxs-lookup"><span data-stu-id="ed017-2559">toodefine a Salesforce linked service, set hello **type** of hello linked service too**Salesforce**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="ed017-2560">Propriedade</span><span class="sxs-lookup"><span data-stu-id="ed017-2560">Property</span></span> | <span data-ttu-id="ed017-2561">Descrição</span><span class="sxs-lookup"><span data-stu-id="ed017-2561">Description</span></span> | <span data-ttu-id="ed017-2562">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="ed017-2562">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ed017-2563">environmentUrl</span><span class="sxs-lookup"><span data-stu-id="ed017-2563">environmentUrl</span></span> | <span data-ttu-id="ed017-2564">Especifique a instância de URL da equipe de vendas de saudação.</span><span class="sxs-lookup"><span data-stu-id="ed017-2564">Specify hello URL of Salesforce instance.</span></span> <br><br> <span data-ttu-id="ed017-2565">– O padrão é "https://login.salesforce.com".</span><span class="sxs-lookup"><span data-stu-id="ed017-2565">- Default is "https://login.salesforce.com".</span></span> <br> <span data-ttu-id="ed017-2566">-toocopy dados de área restrita, especifique "https://test.salesforce.com".</span><span class="sxs-lookup"><span data-stu-id="ed017-2566">- toocopy data from sandbox, specify "https://test.salesforce.com".</span></span> <br> <span data-ttu-id="ed017-2567">-toocopy dados do domínio personalizado, especificar, por exemplo, "https://[domain].my.salesforce.com".</span><span class="sxs-lookup"><span data-stu-id="ed017-2567">- toocopy data from custom domain, specify, for example, "https://[domain].my.salesforce.com".</span></span> |<span data-ttu-id="ed017-2568">Não</span><span class="sxs-lookup"><span data-stu-id="ed017-2568">No</span></span> |
| <span data-ttu-id="ed017-2569">Nome de Usuário</span><span class="sxs-lookup"><span data-stu-id="ed017-2569">username</span></span> |<span data-ttu-id="ed017-2570">Especifique um nome de usuário para a conta de usuário de saudação.</span><span class="sxs-lookup"><span data-stu-id="ed017-2570">Specify a user name for hello user account.</span></span> |<span data-ttu-id="ed017-2571">Sim</span><span class="sxs-lookup"><span data-stu-id="ed017-2571">Yes</span></span> |
| <span data-ttu-id="ed017-2572">Senha</span><span class="sxs-lookup"><span data-stu-id="ed017-2572">password</span></span> |<span data-ttu-id="ed017-2573">Especifique uma senha para a conta de usuário de saudação.</span><span class="sxs-lookup"><span data-stu-id="ed017-2573">Specify a password for hello user account.</span></span> |<span data-ttu-id="ed017-2574">Sim</span><span class="sxs-lookup"><span data-stu-id="ed017-2574">Yes</span></span> |
| <span data-ttu-id="ed017-2575">securityToken</span><span class="sxs-lookup"><span data-stu-id="ed017-2575">securityToken</span></span> |<span data-ttu-id="ed017-2576">Especifique um token de segurança para a conta de usuário de saudação.</span><span class="sxs-lookup"><span data-stu-id="ed017-2576">Specify a security token for hello user account.</span></span> <span data-ttu-id="ed017-2577">Consulte [obter token de segurança](https://help.salesforce.com/apex/HTViewHelpDoc?id=user_security_token.htm) para obter instruções sobre como tooreset/obter um token de segurança.</span><span class="sxs-lookup"><span data-stu-id="ed017-2577">See [Get security token](https://help.salesforce.com/apex/HTViewHelpDoc?id=user_security_token.htm) for instructions on how tooreset/get a security token.</span></span> <span data-ttu-id="ed017-2578">em geral, consulte toolearn sobre tokens de segurança [API de segurança e hello](https://developer.salesforce.com/docs/atlas.en-us.api.meta/api/sforce_api_concepts_security.htm).</span><span class="sxs-lookup"><span data-stu-id="ed017-2578">toolearn about security tokens in general, see [Security and hello API](https://developer.salesforce.com/docs/atlas.en-us.api.meta/api/sforce_api_concepts_security.htm).</span></span> |<span data-ttu-id="ed017-2579">Sim</span><span class="sxs-lookup"><span data-stu-id="ed017-2579">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="ed017-2580">Exemplo</span><span class="sxs-lookup"><span data-stu-id="ed017-2580">Example</span></span>

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

<span data-ttu-id="ed017-2581">Para obter mais informações, consulte o artigo [Conector da Salesforce](data-factory-salesforce-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="ed017-2581">For more information, see [Salesforce connector](data-factory-salesforce-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="ed017-2582">Conjunto de dados</span><span class="sxs-lookup"><span data-stu-id="ed017-2582">Dataset</span></span>
<span data-ttu-id="ed017-2583">toodefine um conjunto de dados do Salesforce, Olá conjunto **tipo** do conjunto de dados de saudação muito**RelationalTable**e especifique Olá seguintes propriedades em Olá **typeProperties** seção:</span><span class="sxs-lookup"><span data-stu-id="ed017-2583">toodefine a Salesforce dataset, set hello **type** of hello dataset too**RelationalTable**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="ed017-2584">Propriedade</span><span class="sxs-lookup"><span data-stu-id="ed017-2584">Property</span></span> | <span data-ttu-id="ed017-2585">Descrição</span><span class="sxs-lookup"><span data-stu-id="ed017-2585">Description</span></span> | <span data-ttu-id="ed017-2586">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="ed017-2586">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ed017-2587">tableName</span><span class="sxs-lookup"><span data-stu-id="ed017-2587">tableName</span></span> |<span data-ttu-id="ed017-2588">Nome da tabela de saudação na equipe de vendas.</span><span class="sxs-lookup"><span data-stu-id="ed017-2588">Name of hello table in Salesforce.</span></span> |<span data-ttu-id="ed017-2589">Não (se uma **consulta** de **RelationalSource** for especificada)</span><span class="sxs-lookup"><span data-stu-id="ed017-2589">No (if a **query** of **RelationalSource** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="ed017-2590">Exemplo</span><span class="sxs-lookup"><span data-stu-id="ed017-2590">Example</span></span>

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

<span data-ttu-id="ed017-2591">Para obter mais informações, consulte o artigo [Conector da Salesforce](data-factory-salesforce-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="ed017-2591">For more information, see [Salesforce connector](data-factory-salesforce-connector.md#dataset-properties) article.</span></span> 

### <a name="relational-source-in-copy-activity"></a><span data-ttu-id="ed017-2592">Origem Relacional na Atividade de Cópia</span><span class="sxs-lookup"><span data-stu-id="ed017-2592">Relational Source in Copy Activity</span></span>
<span data-ttu-id="ed017-2593">Se você estiver copiando dados do Salesforce, defina Olá **tipo de fonte** de hello atividade de cópia muito**RelationalSource**e especificar propriedades no Olá a seguir **fonte** seção:</span><span class="sxs-lookup"><span data-stu-id="ed017-2593">If you are copying data from Salesforce, set hello **source type** of hello copy activity too**RelationalSource**, and specify following properties in hello **source** section:</span></span>

| <span data-ttu-id="ed017-2594">Propriedade</span><span class="sxs-lookup"><span data-stu-id="ed017-2594">Property</span></span> | <span data-ttu-id="ed017-2595">Descrição</span><span class="sxs-lookup"><span data-stu-id="ed017-2595">Description</span></span> | <span data-ttu-id="ed017-2596">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="ed017-2596">Allowed values</span></span> | <span data-ttu-id="ed017-2597">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="ed017-2597">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="ed017-2598">query</span><span class="sxs-lookup"><span data-stu-id="ed017-2598">query</span></span> |<span data-ttu-id="ed017-2599">Use dados de tooread Olá consulta personalizada.</span><span class="sxs-lookup"><span data-stu-id="ed017-2599">Use hello custom query tooread data.</span></span> |<span data-ttu-id="ed017-2600">Uma consulta SQL-92 ou uma consulta [SOQL (Salesforce Object Query Language)](https://developer.salesforce.com/docs/atlas.en-us.soql_sosl.meta/soql_sosl/sforce_api_calls_soql.htm).</span><span class="sxs-lookup"><span data-stu-id="ed017-2600">A SQL-92 query or [Salesforce Object Query Language (SOQL)](https://developer.salesforce.com/docs/atlas.en-us.soql_sosl.meta/soql_sosl/sforce_api_calls_soql.htm) query.</span></span> <span data-ttu-id="ed017-2601">Por exemplo: `select * from MyTable__c`.</span><span class="sxs-lookup"><span data-stu-id="ed017-2601">For example:  `select * from MyTable__c`.</span></span> |<span data-ttu-id="ed017-2602">Não (se hello **tableName** de saudação **dataset** for especificado)</span><span class="sxs-lookup"><span data-stu-id="ed017-2602">No (if hello **tableName** of hello **dataset** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="ed017-2603">Exemplo</span><span class="sxs-lookup"><span data-stu-id="ed017-2603">Example</span></span>  



```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "SalesforceToAzureBlob",
            "description": "Copy from Salesforce tooan Azure blob",
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
> <span data-ttu-id="ed017-2604">parte "__c" Olá Olá nome da API é necessária para qualquer objeto personalizado.</span><span class="sxs-lookup"><span data-stu-id="ed017-2604">hello "__c" part of hello API Name is needed for any custom object.</span></span>

<span data-ttu-id="ed017-2605">Para obter mais informações, consulte o artigo [Conector da Salesforce](data-factory-salesforce-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="ed017-2605">For more information, see [Salesforce connector](data-factory-salesforce-connector.md#copy-activity-properties) article.</span></span> 

## <a name="web-data"></a><span data-ttu-id="ed017-2606">Dados da Web</span><span class="sxs-lookup"><span data-stu-id="ed017-2606">Web Data</span></span> 

### <a name="linked-service"></a><span data-ttu-id="ed017-2607">Serviço vinculado</span><span class="sxs-lookup"><span data-stu-id="ed017-2607">Linked service</span></span>
<span data-ttu-id="ed017-2608">toodefine uma Web vinculado serviço, Olá conjunto **tipo** de saudação serviço vinculado muito**Web**e especificar propriedades no Olá a seguir **typeProperties** seção:</span><span class="sxs-lookup"><span data-stu-id="ed017-2608">toodefine a Web linked service, set hello **type** of hello linked service too**Web**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="ed017-2609">Propriedade</span><span class="sxs-lookup"><span data-stu-id="ed017-2609">Property</span></span> | <span data-ttu-id="ed017-2610">Descrição</span><span class="sxs-lookup"><span data-stu-id="ed017-2610">Description</span></span> | <span data-ttu-id="ed017-2611">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="ed017-2611">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ed017-2612">Url</span><span class="sxs-lookup"><span data-stu-id="ed017-2612">Url</span></span> |<span data-ttu-id="ed017-2613">Origem da URL toohello da Web</span><span class="sxs-lookup"><span data-stu-id="ed017-2613">URL toohello Web source</span></span> |<span data-ttu-id="ed017-2614">Sim</span><span class="sxs-lookup"><span data-stu-id="ed017-2614">Yes</span></span> |
| <span data-ttu-id="ed017-2615">authenticationType</span><span class="sxs-lookup"><span data-stu-id="ed017-2615">authenticationType</span></span> |<span data-ttu-id="ed017-2616">Anônima.</span><span class="sxs-lookup"><span data-stu-id="ed017-2616">Anonymous.</span></span> |<span data-ttu-id="ed017-2617">Sim</span><span class="sxs-lookup"><span data-stu-id="ed017-2617">Yes</span></span> |
 

#### <a name="example"></a><span data-ttu-id="ed017-2618">Exemplo</span><span class="sxs-lookup"><span data-stu-id="ed017-2618">Example</span></span>


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

<span data-ttu-id="ed017-2619">Para obter mais informações, consulte o artigo [Conector da Tabela da Web](data-factory-web-table-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="ed017-2619">For more information, see [Web Table connector](data-factory-web-table-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="ed017-2620">Conjunto de dados</span><span class="sxs-lookup"><span data-stu-id="ed017-2620">Dataset</span></span>
<span data-ttu-id="ed017-2621">toodefine um conjunto de dados da Web, Olá conjunto **tipo** do conjunto de dados de saudação muito**WebTable**e especifique Olá seguintes propriedades em Olá **typeProperties** seção:</span><span class="sxs-lookup"><span data-stu-id="ed017-2621">toodefine a Web dataset, set hello **type** of hello dataset too**WebTable**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="ed017-2622">Propriedade</span><span class="sxs-lookup"><span data-stu-id="ed017-2622">Property</span></span> | <span data-ttu-id="ed017-2623">Descrição</span><span class="sxs-lookup"><span data-stu-id="ed017-2623">Description</span></span> | <span data-ttu-id="ed017-2624">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="ed017-2624">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="ed017-2625">type</span><span class="sxs-lookup"><span data-stu-id="ed017-2625">type</span></span> |<span data-ttu-id="ed017-2626">Tipo de conjunto de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="ed017-2626">type of hello dataset.</span></span> <span data-ttu-id="ed017-2627">deve ser definido muito**WebTable**</span><span class="sxs-lookup"><span data-stu-id="ed017-2627">must be set too**WebTable**</span></span> |<span data-ttu-id="ed017-2628">Sim</span><span class="sxs-lookup"><span data-stu-id="ed017-2628">Yes</span></span> |
| <span data-ttu-id="ed017-2629">path</span><span class="sxs-lookup"><span data-stu-id="ed017-2629">path</span></span> |<span data-ttu-id="ed017-2630">Um relativa URL toohello de recursos que contém a tabela de saudação.</span><span class="sxs-lookup"><span data-stu-id="ed017-2630">A relative URL toohello resource that contains hello table.</span></span> |<span data-ttu-id="ed017-2631">Não.</span><span class="sxs-lookup"><span data-stu-id="ed017-2631">No.</span></span> <span data-ttu-id="ed017-2632">Quando não for especificado, somente URL Olá especificado na definição de serviço vinculada de saudação é usado.</span><span class="sxs-lookup"><span data-stu-id="ed017-2632">When path is not specified, only hello URL specified in hello linked service definition is used.</span></span> |
| <span data-ttu-id="ed017-2633">índice</span><span class="sxs-lookup"><span data-stu-id="ed017-2633">index</span></span> |<span data-ttu-id="ed017-2634">índice de saudação da tabela de saudação no recurso de saudação.</span><span class="sxs-lookup"><span data-stu-id="ed017-2634">hello index of hello table in hello resource.</span></span> <span data-ttu-id="ed017-2635">Consulte [índice de obtenção de uma tabela em uma página HTML](#get-index-of-a-table-in-an-html-page) seção de índice de toogetting de etapas de uma tabela em uma página HTML.</span><span class="sxs-lookup"><span data-stu-id="ed017-2635">See [Get index of a table in an HTML page](#get-index-of-a-table-in-an-html-page) section for steps toogetting index of a table in an HTML page.</span></span> |<span data-ttu-id="ed017-2636">Sim</span><span class="sxs-lookup"><span data-stu-id="ed017-2636">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="ed017-2637">Exemplo</span><span class="sxs-lookup"><span data-stu-id="ed017-2637">Example</span></span>

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

<span data-ttu-id="ed017-2638">Para obter mais informações, consulte o artigo [Conector da Tabela da Web](data-factory-web-table-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="ed017-2638">For more information, see [Web Table connector](data-factory-web-table-connector.md#dataset-properties) article.</span></span> 

### <a name="web-source-in-copy-activity"></a><span data-ttu-id="ed017-2639">Origem da Web na Atividade de Cópia</span><span class="sxs-lookup"><span data-stu-id="ed017-2639">Web Source in Copy Activity</span></span>
<span data-ttu-id="ed017-2640">Se você estiver copiando dados de uma tabela da web, defina Olá **tipo de fonte** de hello atividade de cópia muito**WebSource**.</span><span class="sxs-lookup"><span data-stu-id="ed017-2640">If you are copying data from a web table, set hello **source type** of hello copy activity too**WebSource**.</span></span> <span data-ttu-id="ed017-2641">Atualmente, quando a fonte de saudação na atividade de cópia é do tipo **WebSource**, sem propriedades adicionais são suportadas.</span><span class="sxs-lookup"><span data-stu-id="ed017-2641">Currently, when hello source in copy activity is of type **WebSource**, no additional properties are supported.</span></span>

#### <a name="example"></a><span data-ttu-id="ed017-2642">Exemplo</span><span class="sxs-lookup"><span data-stu-id="ed017-2642">Example</span></span>

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "WebTableToAzureBlob",
            "description": "Copy from a Web table tooan Azure blob",
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

<span data-ttu-id="ed017-2643">Para obter mais informações, consulte o artigo [Conector da Tabela da Web](data-factory-web-table-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="ed017-2643">For more information, see [Web Table connector](data-factory-web-table-connector.md#copy-activity-properties) article.</span></span> 

## <a name="compute-environments"></a><span data-ttu-id="ed017-2644">AMBIENTES DE COMPUTAÇÃO</span><span class="sxs-lookup"><span data-stu-id="ed017-2644">COMPUTE ENVIRONMENTS</span></span>
<span data-ttu-id="ed017-2645">Olá tabela a seguir lista os ambientes de computação de saudação suportados por Data Factory e hello atividades de transformação que podem ser executados neles.</span><span class="sxs-lookup"><span data-stu-id="ed017-2645">hello following table lists hello compute environments supported by Data Factory and hello transformation activities that can run on them.</span></span> <span data-ttu-id="ed017-2646">Clique Olá link para a computação Olá você está interessado em esquemas JSON toosee Olá para o serviço vinculado toolink-tooa fábrica de dados.</span><span class="sxs-lookup"><span data-stu-id="ed017-2646">Click hello link for hello compute you are interested in toosee hello JSON schemas for linked service toolink it tooa data factory.</span></span> 

| <span data-ttu-id="ed017-2647">Ambiente de computação</span><span class="sxs-lookup"><span data-stu-id="ed017-2647">Compute environment</span></span> | <span data-ttu-id="ed017-2648">Atividades</span><span class="sxs-lookup"><span data-stu-id="ed017-2648">Activities</span></span> |
| --- | --- |
| <span data-ttu-id="ed017-2649">[Cluster HDInsight sob demanda](#on-demand-azure-hdinsight-cluster) ou [seu próprio cluster HDInsight](#existing-azure-hdinsight-cluster)</span><span class="sxs-lookup"><span data-stu-id="ed017-2649">[On-demand HDInsight cluster](#on-demand-azure-hdinsight-cluster) or [your own HDInsight cluster](#existing-azure-hdinsight-cluster)</span></span> |<span data-ttu-id="ed017-2650">[Atividade personalizada de .NET](#net-custom-activity), [Atividade de Hive](#hdinsight-hive-activity), [Pig activity](#hdinsight-pig-activity, [Atividade de MapReduce](#hdinsight-mapreduce-activity), [Atividade de transmissão do Hadoop](#hdinsight-streaming-activityd), [Atividade do Spark](#hdinsight-spark-activity)</span><span class="sxs-lookup"><span data-stu-id="ed017-2650">[.NET custom activity](#net-custom-activity), [Hive activity](#hdinsight-hive-activity), [Pig activity](#hdinsight-pig-activity, [MapReduce activity](#hdinsight-mapreduce-activity), [Hadoop streaming activity](#hdinsight-streaming-activityd), [Spark activity](#hdinsight-spark-activity)</span></span> |
| [<span data-ttu-id="ed017-2651">Lote do Azure</span><span class="sxs-lookup"><span data-stu-id="ed017-2651">Azure Batch</span></span>](#azure-batch) |[<span data-ttu-id="ed017-2652">Atividade personalizada do .NET</span><span class="sxs-lookup"><span data-stu-id="ed017-2652">.NET custom activity</span></span>](#net-custom-activity) |
| <span data-ttu-id="ed017-2653">
            [Azure Machine Learning](#azure-machine-learning)</span><span class="sxs-lookup"><span data-stu-id="ed017-2653">[Azure Machine Learning](#azure-machine-learning)</span></span> | <span data-ttu-id="ed017-2654">[Atividade de Execução de Lote de Machine Learning](#machine-learning-batch-execution-activity), [Atividade de Atualização de Recursos de Machine Learning](#machine-learning-update-resource-activity)</span><span class="sxs-lookup"><span data-stu-id="ed017-2654">[Machine Learning Batch Execution Activity](#machine-learning-batch-execution-activity), [Machine Learning Update Resource Activity](#machine-learning-update-resource-activity)</span></span> |
| [<span data-ttu-id="ed017-2655">Análise Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="ed017-2655">Azure Data Lake Analytics</span></span>](#azure-data-lake-analytics) |[<span data-ttu-id="ed017-2656">U-SQL da Análise Data Lake</span><span class="sxs-lookup"><span data-stu-id="ed017-2656">Data Lake Analytics U-SQL</span></span>](#data-lake-analytics-u-sql-activity) |
| <span data-ttu-id="ed017-2657">[Banco de Dados SQL do Azure](#azure-sql-database-1), [SQL Data Warehouse do Azure](#azure-sql-data-warehouse-1), [SQL Server](#sql-server-1)</span><span class="sxs-lookup"><span data-stu-id="ed017-2657">[Azure SQL Database](#azure-sql-database-1), [Azure SQL Data Warehouse](#azure-sql-data-warehouse-1), [SQL Server](#sql-server-1)</span></span> |[<span data-ttu-id="ed017-2658">Procedimento armazenado</span><span class="sxs-lookup"><span data-stu-id="ed017-2658">Stored Procedure</span></span>](#stored-procedure-activity) |

## <a name="on-demand-azure-hdinsight-cluster"></a><span data-ttu-id="ed017-2659">Cluster HDInsight do Azure sob demanda</span><span class="sxs-lookup"><span data-stu-id="ed017-2659">On-demand Azure HDInsight cluster</span></span>
<span data-ttu-id="ed017-2660">Olá serviço fábrica de dados do Azure pode criar automaticamente um dados sob demanda baseados no Windows/Linux de tooprocess de cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="ed017-2660">hello Azure Data Factory service can automatically create a Windows/Linux-based on-demand HDInsight cluster tooprocess data.</span></span> <span data-ttu-id="ed017-2661">Olá cluster é criado no hello mesma região da conta de armazenamento da saudação (propriedade linkedServiceName em JSON de saudação) associado com cluster hello.</span><span class="sxs-lookup"><span data-stu-id="ed017-2661">hello cluster is created in hello same region as hello storage account (linkedServiceName property in hello JSON) associated with hello cluster.</span></span> <span data-ttu-id="ed017-2662">Você pode executar Olá seguintes atividades de transformação nesse serviço vinculado: [atividade personalizada do .NET](#net-custom-activity), [atividade de Hive](#hdinsight-hive-activity), [atividade de Pig] (#-pig-atividade de hdinsight, [atividade MapReduce ](#hdinsight-mapreduce-activity), [Hadoop streaming atividade](#hdinsight-streaming-activityd), [despertar atividade](#hdinsight-spark-activity).</span><span class="sxs-lookup"><span data-stu-id="ed017-2662">You can run hello following transformation activities on this linked service: [.NET custom activity](#net-custom-activity), [Hive activity](#hdinsight-hive-activity), [Pig activity](#hdinsight-pig-activity, [MapReduce activity](#hdinsight-mapreduce-activity), [Hadoop streaming activity](#hdinsight-streaming-activityd), [Spark activity](#hdinsight-spark-activity).</span></span> 

### <a name="linked-service"></a><span data-ttu-id="ed017-2663">Serviço vinculado</span><span class="sxs-lookup"><span data-stu-id="ed017-2663">Linked service</span></span> 
<span data-ttu-id="ed017-2664">Olá, a tabela a seguir fornece descrições para propriedades de saudação usadas na definição do hello Azure JSON de um serviço de vinculado do HDInsight sob demanda.</span><span class="sxs-lookup"><span data-stu-id="ed017-2664">hello following table provides descriptions for hello properties used in hello Azure JSON definition of an on-demand HDInsight linked service.</span></span>

| <span data-ttu-id="ed017-2665">Propriedade</span><span class="sxs-lookup"><span data-stu-id="ed017-2665">Property</span></span> | <span data-ttu-id="ed017-2666">Descrição</span><span class="sxs-lookup"><span data-stu-id="ed017-2666">Description</span></span> | <span data-ttu-id="ed017-2667">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="ed017-2667">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ed017-2668">type</span><span class="sxs-lookup"><span data-stu-id="ed017-2668">type</span></span> |<span data-ttu-id="ed017-2669">propriedade do tipo Hello deve ser definida muito**HDInsightOnDemand**.</span><span class="sxs-lookup"><span data-stu-id="ed017-2669">hello type property should be set too**HDInsightOnDemand**.</span></span> |<span data-ttu-id="ed017-2670">Sim</span><span class="sxs-lookup"><span data-stu-id="ed017-2670">Yes</span></span> |
| <span data-ttu-id="ed017-2671">clusterSize</span><span class="sxs-lookup"><span data-stu-id="ed017-2671">clusterSize</span></span> |<span data-ttu-id="ed017-2672">Número de nós de dados do trabalhador em cluster hello.</span><span class="sxs-lookup"><span data-stu-id="ed017-2672">Number of worker/data nodes in hello cluster.</span></span> <span data-ttu-id="ed017-2673">cluster do HDInsight Olá é criado com 2 nós de cabeçalho junto com o número de saudação de nós de trabalho que você especifica para esta propriedade.</span><span class="sxs-lookup"><span data-stu-id="ed017-2673">hello HDInsight cluster is created with 2 head nodes along with hello number of worker nodes you specify for this property.</span></span> <span data-ttu-id="ed017-2674">nós Olá são de tamanho Standard_D3 que tem 4 núcleos, assim, um cluster de nó do 4 operador leva 24 núcleos (4\*4 = 16 núcleos para nós de trabalho, mais 2\*4 = 8 núcleos para nós de cabeçalho).</span><span class="sxs-lookup"><span data-stu-id="ed017-2674">hello nodes are of size Standard_D3 that has 4 cores, so a 4 worker node cluster takes 24 cores (4\*4 = 16 cores for worker nodes, plus 2\*4 = 8 cores for head nodes).</span></span> <span data-ttu-id="ed017-2675">Consulte [Hadoop baseado em Linux criar clusters de HDInsight](../hdinsight/hdinsight-hadoop-provision-linux-clusters.md) para obter detalhes sobre a camada de saudação Standard_D3.</span><span class="sxs-lookup"><span data-stu-id="ed017-2675">See [Create Linux-based Hadoop clusters in HDInsight](../hdinsight/hdinsight-hadoop-provision-linux-clusters.md) for details about hello Standard_D3 tier.</span></span> |<span data-ttu-id="ed017-2676">Sim</span><span class="sxs-lookup"><span data-stu-id="ed017-2676">Yes</span></span> |
| <span data-ttu-id="ed017-2677">timeToLive</span><span class="sxs-lookup"><span data-stu-id="ed017-2677">timetolive</span></span> |<span data-ttu-id="ed017-2678">Olá permitido tempo ocioso do cluster do HDInsight sob demanda hello.</span><span class="sxs-lookup"><span data-stu-id="ed017-2678">hello allowed idle time for hello on-demand HDInsight cluster.</span></span> <span data-ttu-id="ed017-2679">Especifica quanto tempo cluster do HDInsight sob demanda Olá permanece ativo após a conclusão de uma atividade executar se não houver nenhum outro trabalho ativo no cluster hello.</span><span class="sxs-lookup"><span data-stu-id="ed017-2679">Specifies how long hello on-demand HDInsight cluster stays alive after completion of an activity run if there are no other active jobs in hello cluster.</span></span><br/><br/><span data-ttu-id="ed017-2680">Por exemplo, se uma atividade executar levar 6 minutos e timetolive é definir too5 minutos, Olá cluster permanece ativo por 5 minutos após a saudação 6 minutos de processamento de execução da atividade hello.</span><span class="sxs-lookup"><span data-stu-id="ed017-2680">For example, if an activity run takes 6 minutes and timetolive is set too5 minutes, hello cluster stays alive for 5 minutes after hello 6 minutes of processing hello activity run.</span></span> <span data-ttu-id="ed017-2681">Se outra execução da atividade é executada com uma janela de 6 minutos hello, ela é processada pelo Olá mesmo cluster.</span><span class="sxs-lookup"><span data-stu-id="ed017-2681">If another activity run is executed with hello 6 minutes window, it is processed by hello same cluster.</span></span><br/><br/><span data-ttu-id="ed017-2682">A criação de um cluster do HDInsight sob demanda é uma operação cara (pode demorar um pouco), então use essa configuração como desempenho tooimprove necessários de uma fábrica de dados com a reutilização de um cluster do HDInsight sob demanda.</span><span class="sxs-lookup"><span data-stu-id="ed017-2682">Creating an on-demand HDInsight cluster is an expensive operation (could take a while), so use this setting as needed tooimprove performance of a data factory by reusing an on-demand HDInsight cluster.</span></span><br/><br/><span data-ttu-id="ed017-2683">Se você definir timetolive valor too0, cluster Olá é excluído, assim como hello atividade executada em processados.</span><span class="sxs-lookup"><span data-stu-id="ed017-2683">If you set timetolive value too0, hello cluster is deleted as soon as hello activity run in processed.</span></span> <span data-ttu-id="ed017-2684">Em Olá outro lado, se você definir um valor alto, cluster Olá pode permanecer ocioso desnecessariamente, resultando em altos custos.</span><span class="sxs-lookup"><span data-stu-id="ed017-2684">On hello other hand, if you set a high value, hello cluster may stay idle unnecessarily resulting in high costs.</span></span> <span data-ttu-id="ed017-2685">Portanto, é importante que você defina o valor apropriado de saudação com base em suas necessidades.</span><span class="sxs-lookup"><span data-stu-id="ed017-2685">Therefore, it is important that you set hello appropriate value based on your needs.</span></span><br/><br/><span data-ttu-id="ed017-2686">Vários pipelines podem compartilhar Olá a mesma instância de cluster do HDInsight sob demanda Olá se o valor da propriedade timetolive hello está definido corretamente</span><span class="sxs-lookup"><span data-stu-id="ed017-2686">Multiple pipelines can share hello same instance of hello on-demand HDInsight cluster if hello timetolive property value is appropriately set</span></span> |<span data-ttu-id="ed017-2687">Sim</span><span class="sxs-lookup"><span data-stu-id="ed017-2687">Yes</span></span> |
| <span data-ttu-id="ed017-2688">version</span><span class="sxs-lookup"><span data-stu-id="ed017-2688">version</span></span> |<span data-ttu-id="ed017-2689">Versão do cluster do HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="ed017-2689">Version of hello HDInsight cluster.</span></span> <span data-ttu-id="ed017-2690">Para obter detalhes, confira [Versões com suporte do HDInsight no Azure Data Factory](data-factory-compute-linked-services.md#supported-hdinsight-versions-in-azure-data-factory).</span><span class="sxs-lookup"><span data-stu-id="ed017-2690">For details, see [supported HDInsight versions in Azure Data Factory](data-factory-compute-linked-services.md#supported-hdinsight-versions-in-azure-data-factory).</span></span> |<span data-ttu-id="ed017-2691">Não</span><span class="sxs-lookup"><span data-stu-id="ed017-2691">No</span></span> |
| <span data-ttu-id="ed017-2692">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="ed017-2692">linkedServiceName</span></span> |<span data-ttu-id="ed017-2693">Armazenamento do Azure vinculada toobe de serviço usado pelo cluster sob demanda de saudação para armazenar e processar dados.</span><span class="sxs-lookup"><span data-stu-id="ed017-2693">Azure Storage linked service toobe used by hello on-demand cluster for storing and processing data.</span></span> <p><span data-ttu-id="ed017-2694">No momento, você não pode criar um cluster HDInsight sob demanda que usa um repositório Azure Data Lake como armazenamento hello.</span><span class="sxs-lookup"><span data-stu-id="ed017-2694">Currently, you cannot create an on-demand HDInsight cluster that uses an Azure Data Lake Store as hello storage.</span></span> <span data-ttu-id="ed017-2695">Se desejar que os dados de resultado de saudação toostore do HDInsight de processamento em um repositório Azure Data Lake, use um atividade de cópia toocopy Olá os dados de armazenamento de BLOBs do Azure de saudação toohello repositório Azure Data Lake.</span><span class="sxs-lookup"><span data-stu-id="ed017-2695">If you want toostore hello result data from HDInsight processing in an Azure Data Lake Store, use a Copy Activity toocopy hello data from hello Azure Blob Storage toohello Azure Data Lake Store.</span></span></p>  | <span data-ttu-id="ed017-2696">Sim</span><span class="sxs-lookup"><span data-stu-id="ed017-2696">Yes</span></span> |
| <span data-ttu-id="ed017-2697">additionalLinkedServiceNames</span><span class="sxs-lookup"><span data-stu-id="ed017-2697">additionalLinkedServiceNames</span></span> |<span data-ttu-id="ed017-2698">Especifica o serviço vinculado de contas de armazenamento adicionais para Olá HDInsight para que o serviço do Data Factory Olá pode registrá-los em seu nome.</span><span class="sxs-lookup"><span data-stu-id="ed017-2698">Specifies additional storage accounts for hello HDInsight linked service so that hello Data Factory service can register them on your behalf.</span></span> |<span data-ttu-id="ed017-2699">Não</span><span class="sxs-lookup"><span data-stu-id="ed017-2699">No</span></span> |
| <span data-ttu-id="ed017-2700">osType</span><span class="sxs-lookup"><span data-stu-id="ed017-2700">osType</span></span> |<span data-ttu-id="ed017-2701">Tipo do sistema operacional.</span><span class="sxs-lookup"><span data-stu-id="ed017-2701">Type of operating system.</span></span> <span data-ttu-id="ed017-2702">Valores permitidos são: Windows (padrão) e Linux</span><span class="sxs-lookup"><span data-stu-id="ed017-2702">Allowed values are: Windows (default) and Linux</span></span> |<span data-ttu-id="ed017-2703">Não</span><span class="sxs-lookup"><span data-stu-id="ed017-2703">No</span></span> |
| <span data-ttu-id="ed017-2704">hcatalogLinkedServiceName</span><span class="sxs-lookup"><span data-stu-id="ed017-2704">hcatalogLinkedServiceName</span></span> |<span data-ttu-id="ed017-2705">nome de saudação do vinculado do SQL Azure ponto toohello HCatalog banco de dados do serviço.</span><span class="sxs-lookup"><span data-stu-id="ed017-2705">hello name of Azure SQL linked service that point toohello HCatalog database.</span></span> <span data-ttu-id="ed017-2706">cluster do HDInsight sob demanda Olá é criado usando o banco de dados do SQL Azure hello como Olá metastore.</span><span class="sxs-lookup"><span data-stu-id="ed017-2706">hello on-demand HDInsight cluster is created by using hello Azure SQL database as hello metastore.</span></span> |<span data-ttu-id="ed017-2707">Não</span><span class="sxs-lookup"><span data-stu-id="ed017-2707">No</span></span> |

### <a name="json-example"></a><span data-ttu-id="ed017-2708">Exemplo de JSON</span><span class="sxs-lookup"><span data-stu-id="ed017-2708">JSON example</span></span>
<span data-ttu-id="ed017-2709">Olá JSON a seguir define um serviço vinculado do HDInsight de sob demanda com base em Linux.</span><span class="sxs-lookup"><span data-stu-id="ed017-2709">hello following JSON defines a Linux-based on-demand HDInsight linked service.</span></span> <span data-ttu-id="ed017-2710">Olá serviço da fábrica de dados cria automaticamente um **baseados em Linux** cluster HDInsight durante o processamento de uma fatia de dados.</span><span class="sxs-lookup"><span data-stu-id="ed017-2710">hello Data Factory service automatically creates a **Linux-based** HDInsight cluster when processing a data slice.</span></span> 

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

<span data-ttu-id="ed017-2711">Para obter mais informações, consulte o artigo [Serviços vinculados de computação](data-factory-compute-linked-services.md).</span><span class="sxs-lookup"><span data-stu-id="ed017-2711">For more information, see [Compute linked services](data-factory-compute-linked-services.md) article.</span></span> 

## <a name="existing-azure-hdinsight-cluster"></a><span data-ttu-id="ed017-2712">Cluster Azure HDInsight existente</span><span class="sxs-lookup"><span data-stu-id="ed017-2712">Existing Azure HDInsight cluster</span></span>
<span data-ttu-id="ed017-2713">Você pode criar um tooregister de serviço vinculado do Azure HDInsight seu próprio cluster HDInsight com a fábrica de dados.</span><span class="sxs-lookup"><span data-stu-id="ed017-2713">You can create an Azure HDInsight linked service tooregister your own HDInsight cluster with Data Factory.</span></span> <span data-ttu-id="ed017-2714">Você pode executar Olá atividades de transformação de dados a seguir sobre esse serviço vinculado: [atividade personalizada do .NET](#net-custom-activity), [atividade de Hive](#hdinsight-hive-activity), [atividade de Pig] (#-pig-atividade de hdinsight, [MapReduce atividade](#hdinsight-mapreduce-activity), [Hadoop streaming atividade](#hdinsight-streaming-activityd), [despertar atividade](#hdinsight-spark-activity).</span><span class="sxs-lookup"><span data-stu-id="ed017-2714">You can run hello following data transformation activities on this linked service: [.NET custom activity](#net-custom-activity), [Hive activity](#hdinsight-hive-activity), [Pig activity](#hdinsight-pig-activity, [MapReduce activity](#hdinsight-mapreduce-activity), [Hadoop streaming activity](#hdinsight-streaming-activityd), [Spark activity](#hdinsight-spark-activity).</span></span> 

### <a name="linked-service"></a><span data-ttu-id="ed017-2715">Serviço vinculado</span><span class="sxs-lookup"><span data-stu-id="ed017-2715">Linked service</span></span>
<span data-ttu-id="ed017-2716">Olá, a tabela a seguir fornece descrições para propriedades de saudação usadas na definição do hello Azure JSON de um serviço vinculado do HDInsight do Azure.</span><span class="sxs-lookup"><span data-stu-id="ed017-2716">hello following table provides descriptions for hello properties used in hello Azure JSON definition of an Azure HDInsight linked service.</span></span>

| <span data-ttu-id="ed017-2717">Propriedade</span><span class="sxs-lookup"><span data-stu-id="ed017-2717">Property</span></span> | <span data-ttu-id="ed017-2718">Descrição</span><span class="sxs-lookup"><span data-stu-id="ed017-2718">Description</span></span> | <span data-ttu-id="ed017-2719">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="ed017-2719">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ed017-2720">type</span><span class="sxs-lookup"><span data-stu-id="ed017-2720">type</span></span> |<span data-ttu-id="ed017-2721">propriedade do tipo Hello deve ser definida muito**HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="ed017-2721">hello type property should be set too**HDInsight**.</span></span> |<span data-ttu-id="ed017-2722">Sim</span><span class="sxs-lookup"><span data-stu-id="ed017-2722">Yes</span></span> |
| <span data-ttu-id="ed017-2723">clusterUri</span><span class="sxs-lookup"><span data-stu-id="ed017-2723">clusterUri</span></span> |<span data-ttu-id="ed017-2724">Olá URI do cluster do HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="ed017-2724">hello URI of hello HDInsight cluster.</span></span> |<span data-ttu-id="ed017-2725">Sim</span><span class="sxs-lookup"><span data-stu-id="ed017-2725">Yes</span></span> |
| <span data-ttu-id="ed017-2726">Nome de Usuário</span><span class="sxs-lookup"><span data-stu-id="ed017-2726">username</span></span> |<span data-ttu-id="ed017-2727">Especifique o nome Olá Olá usuário toobe usado cluster do HDInsight tooconnect tooan existente.</span><span class="sxs-lookup"><span data-stu-id="ed017-2727">Specify hello name of hello user toobe used tooconnect tooan existing HDInsight cluster.</span></span> |<span data-ttu-id="ed017-2728">Sim</span><span class="sxs-lookup"><span data-stu-id="ed017-2728">Yes</span></span> |
| <span data-ttu-id="ed017-2729">Senha</span><span class="sxs-lookup"><span data-stu-id="ed017-2729">password</span></span> |<span data-ttu-id="ed017-2730">Especifique a senha da conta de usuário de saudação.</span><span class="sxs-lookup"><span data-stu-id="ed017-2730">Specify password for hello user account.</span></span> |<span data-ttu-id="ed017-2731">Sim</span><span class="sxs-lookup"><span data-stu-id="ed017-2731">Yes</span></span> |
| <span data-ttu-id="ed017-2732">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="ed017-2732">linkedServiceName</span></span> | <span data-ttu-id="ed017-2733">Nome do serviço vinculado do armazenamento do Azure que se refere o armazenamento de BLOBs do Azure toohello de saudação usado por Olá cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="ed017-2733">Name of hello Azure Storage linked service that refers toohello Azure blob storage used by hello HDInsight cluster.</span></span> <p><span data-ttu-id="ed017-2734">No momento, você não pode especificar um serviço vinculado do Azure Data Lake Store para essa propriedade.</span><span class="sxs-lookup"><span data-stu-id="ed017-2734">Currently, you cannot specify an Azure Data Lake Store linked service for this property.</span></span> <span data-ttu-id="ed017-2735">Você pode acessar dados em Olá repositório Azure Data Lake de scripts de Pig/Hive se o cluster do HDInsight Olá tem acesso toohello repositório Data Lake.</span><span class="sxs-lookup"><span data-stu-id="ed017-2735">You may access data in hello Azure Data Lake Store from Hive/Pig scripts if hello HDInsight cluster has access toohello Data Lake Store.</span></span> </p>  |<span data-ttu-id="ed017-2736">Sim</span><span class="sxs-lookup"><span data-stu-id="ed017-2736">Yes</span></span> |

<span data-ttu-id="ed017-2737">Para conferir as versões de clusters HDInsight com suporte, veja [Versões do HDInsight com suporte](data-factory-compute-linked-services.md#supported-hdinsight-versions-in-azure-data-factory).</span><span class="sxs-lookup"><span data-stu-id="ed017-2737">For versions of HDInsight clusters supported, see [supported HDInsight versions](data-factory-compute-linked-services.md#supported-hdinsight-versions-in-azure-data-factory).</span></span> 

#### <a name="json-example"></a><span data-ttu-id="ed017-2738">Exemplo de JSON</span><span class="sxs-lookup"><span data-stu-id="ed017-2738">JSON example</span></span>

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

## <a name="azure-batch"></a><span data-ttu-id="ed017-2739">Lote do Azure</span><span class="sxs-lookup"><span data-stu-id="ed017-2739">Azure Batch</span></span>
<span data-ttu-id="ed017-2740">Você pode criar um pool de lote de máquinas virtuais (VMs) de um tooregister de serviço vinculado do Azure Batch com uma fábrica de dados.</span><span class="sxs-lookup"><span data-stu-id="ed017-2740">You can create an Azure Batch linked service tooregister a Batch pool of virtual machines (VMs) with a data factory.</span></span> <span data-ttu-id="ed017-2741">Você pode executar atividades personalizadas do .NET usando o Lote do Azure ou o Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="ed017-2741">You can run .NET custom activities using either Azure Batch or Azure HDInsight.</span></span> <span data-ttu-id="ed017-2742">Você pode executar uma [atividade personalizada do .NET](#net-custom-activity) neste serviço vinculado.</span><span class="sxs-lookup"><span data-stu-id="ed017-2742">You can run a [.NET custom activity](#net-custom-activity) on this linked service.</span></span> 

### <a name="linked-service"></a><span data-ttu-id="ed017-2743">Serviço vinculado</span><span class="sxs-lookup"><span data-stu-id="ed017-2743">Linked service</span></span>
<span data-ttu-id="ed017-2744">Olá, a tabela a seguir fornece descrições para propriedades de saudação usadas na definição do hello Azure JSON de um serviço vinculado do Azure Batch.</span><span class="sxs-lookup"><span data-stu-id="ed017-2744">hello following table provides descriptions for hello properties used in hello Azure JSON definition of an Azure Batch linked service.</span></span>

| <span data-ttu-id="ed017-2745">Propriedade</span><span class="sxs-lookup"><span data-stu-id="ed017-2745">Property</span></span> | <span data-ttu-id="ed017-2746">Descrição</span><span class="sxs-lookup"><span data-stu-id="ed017-2746">Description</span></span> | <span data-ttu-id="ed017-2747">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="ed017-2747">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ed017-2748">type</span><span class="sxs-lookup"><span data-stu-id="ed017-2748">type</span></span> |<span data-ttu-id="ed017-2749">propriedade do tipo Hello deve ser definida muito**AzureBatch**.</span><span class="sxs-lookup"><span data-stu-id="ed017-2749">hello type property should be set too**AzureBatch**.</span></span> |<span data-ttu-id="ed017-2750">Sim</span><span class="sxs-lookup"><span data-stu-id="ed017-2750">Yes</span></span> |
| <span data-ttu-id="ed017-2751">accountName</span><span class="sxs-lookup"><span data-stu-id="ed017-2751">accountName</span></span> |<span data-ttu-id="ed017-2752">Nome da saudação conta de lote do Azure.</span><span class="sxs-lookup"><span data-stu-id="ed017-2752">Name of hello Azure Batch account.</span></span> |<span data-ttu-id="ed017-2753">Sim</span><span class="sxs-lookup"><span data-stu-id="ed017-2753">Yes</span></span> |
| <span data-ttu-id="ed017-2754">accessKey</span><span class="sxs-lookup"><span data-stu-id="ed017-2754">accessKey</span></span> |<span data-ttu-id="ed017-2755">Chave de acesso para Olá conta de lote do Azure.</span><span class="sxs-lookup"><span data-stu-id="ed017-2755">Access key for hello Azure Batch account.</span></span> |<span data-ttu-id="ed017-2756">Sim</span><span class="sxs-lookup"><span data-stu-id="ed017-2756">Yes</span></span> |
| <span data-ttu-id="ed017-2757">poolName</span><span class="sxs-lookup"><span data-stu-id="ed017-2757">poolName</span></span> |<span data-ttu-id="ed017-2758">Nome do pool de saudação de máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="ed017-2758">Name of hello pool of virtual machines.</span></span> |<span data-ttu-id="ed017-2759">Sim</span><span class="sxs-lookup"><span data-stu-id="ed017-2759">Yes</span></span> |
| <span data-ttu-id="ed017-2760">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="ed017-2760">linkedServiceName</span></span> |<span data-ttu-id="ed017-2761">Nome do serviço vinculado do armazenamento do Azure associada ao serviço vinculado do Azure Batch de saudação.</span><span class="sxs-lookup"><span data-stu-id="ed017-2761">Name of hello Azure Storage linked service associated with this Azure Batch linked service.</span></span> <span data-ttu-id="ed017-2762">Esse serviço vinculado é usado para arquivos de teste toorun atividade de saudação e armazenar os logs de execução de atividade Olá necessários.</span><span class="sxs-lookup"><span data-stu-id="ed017-2762">This linked service is used for staging files required toorun hello activity and storing hello activity execution logs.</span></span> |<span data-ttu-id="ed017-2763">Sim</span><span class="sxs-lookup"><span data-stu-id="ed017-2763">Yes</span></span> |


#### <a name="json-example"></a><span data-ttu-id="ed017-2764">Exemplo de JSON</span><span class="sxs-lookup"><span data-stu-id="ed017-2764">JSON example</span></span>

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

## <a name="azure-machine-learning"></a><span data-ttu-id="ed017-2765">Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="ed017-2765">Azure Machine Learning</span></span>
<span data-ttu-id="ed017-2766">Você cria um tooregister de serviço vinculado do aprendizado de máquina do Azure para um ponto de extremidade com uma fábrica de dados de pontuação do lote de aprendizado de máquina.</span><span class="sxs-lookup"><span data-stu-id="ed017-2766">You create an Azure Machine Learning linked service tooregister a Machine Learning batch scoring endpoint with a data factory.</span></span> <span data-ttu-id="ed017-2767">Duas atividades de transformação de dados podem ser executadas neste serviço vinculado: [Atividade de Execução de Lote de Machine Learning](#machine-learning-batch-execution-activity), [Atividade de Atualização de Recursos de Machine Learning](#machine-learning-update-resource-activity).</span><span class="sxs-lookup"><span data-stu-id="ed017-2767">Two data transformation activities that can run on this linked service: [Machine Learning Batch Execution Activity](#machine-learning-batch-execution-activity), [Machine Learning Update Resource Activity](#machine-learning-update-resource-activity).</span></span> 

### <a name="linked-service"></a><span data-ttu-id="ed017-2768">Serviço vinculado</span><span class="sxs-lookup"><span data-stu-id="ed017-2768">Linked service</span></span>
<span data-ttu-id="ed017-2769">Olá, a tabela a seguir fornece descrições para propriedades de saudação usadas na definição do hello Azure JSON de um serviço vinculado do aprendizado de máquina do Azure.</span><span class="sxs-lookup"><span data-stu-id="ed017-2769">hello following table provides descriptions for hello properties used in hello Azure JSON definition of an Azure Machine Learning linked service.</span></span>

| <span data-ttu-id="ed017-2770">Propriedade</span><span class="sxs-lookup"><span data-stu-id="ed017-2770">Property</span></span> | <span data-ttu-id="ed017-2771">Descrição</span><span class="sxs-lookup"><span data-stu-id="ed017-2771">Description</span></span> | <span data-ttu-id="ed017-2772">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="ed017-2772">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ed017-2773">Tipo</span><span class="sxs-lookup"><span data-stu-id="ed017-2773">Type</span></span> |<span data-ttu-id="ed017-2774">propriedade de tipo Hello deve ser definida como: **AzureML**.</span><span class="sxs-lookup"><span data-stu-id="ed017-2774">hello type property should be set to: **AzureML**.</span></span> |<span data-ttu-id="ed017-2775">Sim</span><span class="sxs-lookup"><span data-stu-id="ed017-2775">Yes</span></span> |
| <span data-ttu-id="ed017-2776">mlEndpoint</span><span class="sxs-lookup"><span data-stu-id="ed017-2776">mlEndpoint</span></span> |<span data-ttu-id="ed017-2777">URL de pontuação de lote de saudação.</span><span class="sxs-lookup"><span data-stu-id="ed017-2777">hello batch scoring URL.</span></span> |<span data-ttu-id="ed017-2778">Sim</span><span class="sxs-lookup"><span data-stu-id="ed017-2778">Yes</span></span> |
| <span data-ttu-id="ed017-2779">apiKey</span><span class="sxs-lookup"><span data-stu-id="ed017-2779">apiKey</span></span> |<span data-ttu-id="ed017-2780">Olá publicados API do modelo de espaço de trabalho.</span><span class="sxs-lookup"><span data-stu-id="ed017-2780">hello published workspace model’s API.</span></span> |<span data-ttu-id="ed017-2781">Sim</span><span class="sxs-lookup"><span data-stu-id="ed017-2781">Yes</span></span> |

#### <a name="json-example"></a><span data-ttu-id="ed017-2782">Exemplo de JSON</span><span class="sxs-lookup"><span data-stu-id="ed017-2782">JSON example</span></span>

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

## <a name="azure-data-lake-analytics"></a><span data-ttu-id="ed017-2783">Análise Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="ed017-2783">Azure Data Lake Analytics</span></span>
<span data-ttu-id="ed017-2784">Você cria um **análise Azure Data Lake** vinculado serviço toolink uma análise do Azure Data Lake computação serviço tooan data factory do Azure antes de usar o hello [atividade U-SQL do Data Lake análise](data-factory-usql-activity.md) em um pipeline .</span><span class="sxs-lookup"><span data-stu-id="ed017-2784">You create an **Azure Data Lake Analytics** linked service toolink an Azure Data Lake Analytics compute service tooan Azure data factory before using hello [Data Lake Analytics U-SQL activity](data-factory-usql-activity.md) in a pipeline.</span></span>

### <a name="linked-service"></a><span data-ttu-id="ed017-2785">Serviço vinculado</span><span class="sxs-lookup"><span data-stu-id="ed017-2785">Linked service</span></span>

<span data-ttu-id="ed017-2786">Olá, a tabela a seguir fornece descrições para propriedades de saudação usadas na definição de JSON de saudação de um serviço vinculado de análise do Azure Data Lake.</span><span class="sxs-lookup"><span data-stu-id="ed017-2786">hello following table provides descriptions for hello properties used in hello JSON definition of an Azure Data Lake Analytics linked service.</span></span> 

| <span data-ttu-id="ed017-2787">Propriedade</span><span class="sxs-lookup"><span data-stu-id="ed017-2787">Property</span></span> | <span data-ttu-id="ed017-2788">Descrição</span><span class="sxs-lookup"><span data-stu-id="ed017-2788">Description</span></span> | <span data-ttu-id="ed017-2789">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="ed017-2789">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ed017-2790">Tipo</span><span class="sxs-lookup"><span data-stu-id="ed017-2790">Type</span></span> |<span data-ttu-id="ed017-2791">propriedade de tipo Hello deve ser definida como: **AzureDataLakeAnalytics**.</span><span class="sxs-lookup"><span data-stu-id="ed017-2791">hello type property should be set to: **AzureDataLakeAnalytics**.</span></span> |<span data-ttu-id="ed017-2792">Sim</span><span class="sxs-lookup"><span data-stu-id="ed017-2792">Yes</span></span> |
| <span data-ttu-id="ed017-2793">accountName</span><span class="sxs-lookup"><span data-stu-id="ed017-2793">accountName</span></span> |<span data-ttu-id="ed017-2794">Nome da conta da Análise Azure Data Lake.</span><span class="sxs-lookup"><span data-stu-id="ed017-2794">Azure Data Lake Analytics Account Name.</span></span> |<span data-ttu-id="ed017-2795">Sim</span><span class="sxs-lookup"><span data-stu-id="ed017-2795">Yes</span></span> |
| <span data-ttu-id="ed017-2796">dataLakeAnalyticsUri</span><span class="sxs-lookup"><span data-stu-id="ed017-2796">dataLakeAnalyticsUri</span></span> |<span data-ttu-id="ed017-2797">URI da Análise Azure Data Lake.</span><span class="sxs-lookup"><span data-stu-id="ed017-2797">Azure Data Lake Analytics URI.</span></span> |<span data-ttu-id="ed017-2798">Não</span><span class="sxs-lookup"><span data-stu-id="ed017-2798">No</span></span> |
| <span data-ttu-id="ed017-2799">autorização</span><span class="sxs-lookup"><span data-stu-id="ed017-2799">authorization</span></span> |<span data-ttu-id="ed017-2800">Código de autorização é recuperado automaticamente depois de clicar em **autorizar** botão hello Editor da fábrica de dados e logon do OAuth Olá concluído.</span><span class="sxs-lookup"><span data-stu-id="ed017-2800">Authorization code is automatically retrieved after clicking **Authorize** button in hello Data Factory Editor and completing hello OAuth login.</span></span> |<span data-ttu-id="ed017-2801">Sim</span><span class="sxs-lookup"><span data-stu-id="ed017-2801">Yes</span></span> |
| <span data-ttu-id="ed017-2802">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="ed017-2802">subscriptionId</span></span> |<span data-ttu-id="ed017-2803">Id de assinatura do Azure</span><span class="sxs-lookup"><span data-stu-id="ed017-2803">Azure subscription id</span></span> |<span data-ttu-id="ed017-2804">Não (se não especificado, a assinatura de saudação fábrica de dados é usada).</span><span class="sxs-lookup"><span data-stu-id="ed017-2804">No (If not specified, subscription of hello data factory is used).</span></span> |
| <span data-ttu-id="ed017-2805">resourceGroupName</span><span class="sxs-lookup"><span data-stu-id="ed017-2805">resourceGroupName</span></span> |<span data-ttu-id="ed017-2806">Nome do grupo de recursos do Azure</span><span class="sxs-lookup"><span data-stu-id="ed017-2806">Azure resource group name</span></span> |<span data-ttu-id="ed017-2807">Não (se não especificado, o grupo de recursos de saudação fábrica de dados é usada).</span><span class="sxs-lookup"><span data-stu-id="ed017-2807">No (If not specified, resource group of hello data factory is used).</span></span> |
| <span data-ttu-id="ed017-2808">sessionId</span><span class="sxs-lookup"><span data-stu-id="ed017-2808">sessionId</span></span> |<span data-ttu-id="ed017-2809">id de sessão da sessão de autorização de OAuth hello.</span><span class="sxs-lookup"><span data-stu-id="ed017-2809">session id from hello OAuth authorization session.</span></span> <span data-ttu-id="ed017-2810">Cada ID da sessão é exclusiva e pode ser usado somente uma vez.</span><span class="sxs-lookup"><span data-stu-id="ed017-2810">Each session id is unique and may only be used once.</span></span> <span data-ttu-id="ed017-2811">Quando você usa Olá Editor da fábrica de dados, essa ID é gerada automaticamente.</span><span class="sxs-lookup"><span data-stu-id="ed017-2811">When you use hello Data Factory Editor, this ID is auto-generated.</span></span> |<span data-ttu-id="ed017-2812">Sim</span><span class="sxs-lookup"><span data-stu-id="ed017-2812">Yes</span></span> |


#### <a name="json-example"></a><span data-ttu-id="ed017-2813">Exemplo de JSON</span><span class="sxs-lookup"><span data-stu-id="ed017-2813">JSON example</span></span>
<span data-ttu-id="ed017-2814">saudação de exemplo a seguir fornece a definição de JSON para um serviço vinculado de análise do Azure Data Lake.</span><span class="sxs-lookup"><span data-stu-id="ed017-2814">hello following example provides JSON definition for an Azure Data Lake Analytics linked service.</span></span>

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

## <a name="azure-sql-database"></a><span data-ttu-id="ed017-2815">Banco de Dados SQL do Azure</span><span class="sxs-lookup"><span data-stu-id="ed017-2815">Azure SQL Database</span></span>
<span data-ttu-id="ed017-2816">Criar um serviço vinculado do SQL Azure e usá-lo com hello [atividade de procedimento armazenado](#stored-procedure-activity) tooinvoke um procedimento armazenado de um pipeline da fábrica de dados.</span><span class="sxs-lookup"><span data-stu-id="ed017-2816">You create an Azure SQL linked service and use it with hello [Stored Procedure Activity](#stored-procedure-activity) tooinvoke a stored procedure from a Data Factory pipeline.</span></span> 

### <a name="linked-service"></a><span data-ttu-id="ed017-2817">Serviço vinculado</span><span class="sxs-lookup"><span data-stu-id="ed017-2817">Linked service</span></span>
<span data-ttu-id="ed017-2818">toodefine um banco de dados do SQL Azure vinculado serviço, Olá conjunto **tipo** de saudação serviço vinculado muito**AzureSqlDatabase**e especificar propriedades no Olá a seguir **typeProperties**seção:</span><span class="sxs-lookup"><span data-stu-id="ed017-2818">toodefine an Azure SQL Database linked service, set hello **type** of hello linked service too**AzureSqlDatabase**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="ed017-2819">Propriedade</span><span class="sxs-lookup"><span data-stu-id="ed017-2819">Property</span></span> | <span data-ttu-id="ed017-2820">Descrição</span><span class="sxs-lookup"><span data-stu-id="ed017-2820">Description</span></span> | <span data-ttu-id="ed017-2821">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="ed017-2821">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ed017-2822">connectionString</span><span class="sxs-lookup"><span data-stu-id="ed017-2822">connectionString</span></span> |<span data-ttu-id="ed017-2823">Especifique informações necessárias a instância de banco de dados do Azure SQL toohello tooconnect para a propriedade connectionString de saudação.</span><span class="sxs-lookup"><span data-stu-id="ed017-2823">Specify information needed tooconnect toohello Azure SQL Database instance for hello connectionString property.</span></span> |<span data-ttu-id="ed017-2824">Sim</span><span class="sxs-lookup"><span data-stu-id="ed017-2824">Yes</span></span> |

#### <a name="json-example"></a><span data-ttu-id="ed017-2825">Exemplo de JSON</span><span class="sxs-lookup"><span data-stu-id="ed017-2825">JSON example</span></span>

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

<span data-ttu-id="ed017-2826">Confira o artigo [Conector SQL do Azure](data-factory-azure-sql-connector.md#linked-service-properties) para saber mais sobre esse serviço vinculado.</span><span class="sxs-lookup"><span data-stu-id="ed017-2826">See [Azure SQL Connector](data-factory-azure-sql-connector.md#linked-service-properties) article for details about this linked service.</span></span>

## <a name="azure-sql-data-warehouse"></a><span data-ttu-id="ed017-2827">SQL Data Warehouse do Azure</span><span class="sxs-lookup"><span data-stu-id="ed017-2827">Azure SQL Data Warehouse</span></span>
<span data-ttu-id="ed017-2828">Criar um serviço vinculado do Azure SQL Data Warehouse e usá-lo com hello [atividade de procedimento armazenado](data-factory-stored-proc-activity.md) tooinvoke um procedimento armazenado de um pipeline da fábrica de dados.</span><span class="sxs-lookup"><span data-stu-id="ed017-2828">You create an Azure SQL Data Warehouse linked service and use it with hello [Stored Procedure Activity](data-factory-stored-proc-activity.md) tooinvoke a stored procedure from a Data Factory pipeline.</span></span> 

### <a name="linked-service"></a><span data-ttu-id="ed017-2829">Serviço vinculado</span><span class="sxs-lookup"><span data-stu-id="ed017-2829">Linked service</span></span>
<span data-ttu-id="ed017-2830">toodefine um Azure SQL Data Warehouse vinculado serviço, Olá conjunto **tipo** de saudação serviço vinculado muito**AzureSqlDW**e especificar propriedades no Olá a seguir **typeProperties**seção:</span><span class="sxs-lookup"><span data-stu-id="ed017-2830">toodefine an Azure SQL Data Warehouse linked service, set hello **type** of hello linked service too**AzureSqlDW**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="ed017-2831">Propriedade</span><span class="sxs-lookup"><span data-stu-id="ed017-2831">Property</span></span> | <span data-ttu-id="ed017-2832">Descrição</span><span class="sxs-lookup"><span data-stu-id="ed017-2832">Description</span></span> | <span data-ttu-id="ed017-2833">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="ed017-2833">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ed017-2834">connectionString</span><span class="sxs-lookup"><span data-stu-id="ed017-2834">connectionString</span></span> |<span data-ttu-id="ed017-2835">Especifique informações necessárias a instância do tooconnect toohello Azure SQL Data Warehouse para a propriedade connectionString de saudação.</span><span class="sxs-lookup"><span data-stu-id="ed017-2835">Specify information needed tooconnect toohello Azure SQL Data Warehouse instance for hello connectionString property.</span></span> |<span data-ttu-id="ed017-2836">Sim</span><span class="sxs-lookup"><span data-stu-id="ed017-2836">Yes</span></span> |

#### <a name="json-example"></a><span data-ttu-id="ed017-2837">Exemplo de JSON</span><span class="sxs-lookup"><span data-stu-id="ed017-2837">JSON example</span></span>

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

<span data-ttu-id="ed017-2838">Para obter mais informações, consulte o artigo [Conector do SQL Data Warehouse do Azure](data-factory-azure-sql-data-warehouse-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="ed017-2838">For more information, see [Azure SQL Data Warehouse connector](data-factory-azure-sql-data-warehouse-connector.md#linked-service-properties) article.</span></span> 

## <a name="sql-server"></a><span data-ttu-id="ed017-2839">SQL Server</span><span class="sxs-lookup"><span data-stu-id="ed017-2839">SQL Server</span></span> 
<span data-ttu-id="ed017-2840">Criar um serviço vinculado do SQL Server e usá-lo com hello [atividade de procedimento armazenado](data-factory-stored-proc-activity.md) tooinvoke um procedimento armazenado de um pipeline da fábrica de dados.</span><span class="sxs-lookup"><span data-stu-id="ed017-2840">You create a SQL Server linked service and use it with hello [Stored Procedure Activity](data-factory-stored-proc-activity.md) tooinvoke a stored procedure from a Data Factory pipeline.</span></span> 

### <a name="linked-service"></a><span data-ttu-id="ed017-2841">Serviço vinculado</span><span class="sxs-lookup"><span data-stu-id="ed017-2841">Linked service</span></span>
<span data-ttu-id="ed017-2842">Criar um serviço vinculado do tipo **OnPremisesSqlServer** toolink uma fábrica de dados tooa de banco de dados do local do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="ed017-2842">You create a linked service of type **OnPremisesSqlServer** toolink an on-premises SQL Server database tooa data factory.</span></span> <span data-ttu-id="ed017-2843">Olá a tabela a seguir fornece uma descrição para o serviço vinculado do SQL Server do JSON elementos tooon local específico.</span><span class="sxs-lookup"><span data-stu-id="ed017-2843">hello following table provides description for JSON elements specific tooon-premises SQL Server linked service.</span></span>

<span data-ttu-id="ed017-2844">Olá, a tabela a seguir fornece uma descrição para o JSON de elementos específico tooSQL serviço do servidor vinculado.</span><span class="sxs-lookup"><span data-stu-id="ed017-2844">hello following table provides description for JSON elements specific tooSQL Server linked service.</span></span>

| <span data-ttu-id="ed017-2845">Propriedade</span><span class="sxs-lookup"><span data-stu-id="ed017-2845">Property</span></span> | <span data-ttu-id="ed017-2846">Descrição</span><span class="sxs-lookup"><span data-stu-id="ed017-2846">Description</span></span> | <span data-ttu-id="ed017-2847">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="ed017-2847">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ed017-2848">type</span><span class="sxs-lookup"><span data-stu-id="ed017-2848">type</span></span> |<span data-ttu-id="ed017-2849">propriedade de tipo Hello deve ser definida como: **OnPremisesSqlServer**.</span><span class="sxs-lookup"><span data-stu-id="ed017-2849">hello type property should be set to: **OnPremisesSqlServer**.</span></span> |<span data-ttu-id="ed017-2850">Sim</span><span class="sxs-lookup"><span data-stu-id="ed017-2850">Yes</span></span> |
| <span data-ttu-id="ed017-2851">connectionString</span><span class="sxs-lookup"><span data-stu-id="ed017-2851">connectionString</span></span> |<span data-ttu-id="ed017-2852">Especifica informações de connectionString necessárias tooconnect toohello no SQL Server banco de dados local usando a autenticação do Windows ou autenticação do SQL.</span><span class="sxs-lookup"><span data-stu-id="ed017-2852">Specify connectionString information needed tooconnect toohello on-premises SQL Server database using either SQL authentication or Windows authentication.</span></span> |<span data-ttu-id="ed017-2853">Sim</span><span class="sxs-lookup"><span data-stu-id="ed017-2853">Yes</span></span> |
| <span data-ttu-id="ed017-2854">gatewayName</span><span class="sxs-lookup"><span data-stu-id="ed017-2854">gatewayName</span></span> |<span data-ttu-id="ed017-2855">Nome do gateway Olá Olá serviço da fábrica de dados deve usar o banco de dados do tooconnect toohello no local do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="ed017-2855">Name of hello gateway that hello Data Factory service should use tooconnect toohello on-premises SQL Server database.</span></span> |<span data-ttu-id="ed017-2856">Sim</span><span class="sxs-lookup"><span data-stu-id="ed017-2856">Yes</span></span> |
| <span data-ttu-id="ed017-2857">Nome de Usuário</span><span class="sxs-lookup"><span data-stu-id="ed017-2857">username</span></span> |<span data-ttu-id="ed017-2858">Especifique o nome de usuário se você estiver usando a Autenticação do Windows.</span><span class="sxs-lookup"><span data-stu-id="ed017-2858">Specify user name if you are using Windows Authentication.</span></span> <span data-ttu-id="ed017-2859">Exemplo: **domainname\\username**.</span><span class="sxs-lookup"><span data-stu-id="ed017-2859">Example: **domainname\\username**.</span></span> |<span data-ttu-id="ed017-2860">Não</span><span class="sxs-lookup"><span data-stu-id="ed017-2860">No</span></span> |
| <span data-ttu-id="ed017-2861">Senha</span><span class="sxs-lookup"><span data-stu-id="ed017-2861">password</span></span> |<span data-ttu-id="ed017-2862">Especifique a senha da conta de usuário de saudação especificado para nome de usuário de saudação.</span><span class="sxs-lookup"><span data-stu-id="ed017-2862">Specify password for hello user account you specified for hello username.</span></span> |<span data-ttu-id="ed017-2863">Não</span><span class="sxs-lookup"><span data-stu-id="ed017-2863">No</span></span> |

<span data-ttu-id="ed017-2864">Você pode criptografar credenciais usando Olá **New-AzureRmDataFactoryEncryptValue** cmdlet e usá-los na cadeia de caracteres de conexão hello, conforme mostrado no exemplo a seguir de saudação (**EncryptedCredential** propriedade):</span><span class="sxs-lookup"><span data-stu-id="ed017-2864">You can encrypt credentials using hello **New-AzureRmDataFactoryEncryptValue** cmdlet and use them in hello connection string as shown in hello following example (**EncryptedCredential** property):</span></span>  

```JSON
"connectionString": "Data Source=<servername>;Initial Catalog=<databasename>;Integrated Security=True;EncryptedCredential=<encrypted credential>",
```


#### <a name="example-json-for-using-sql-authentication"></a><span data-ttu-id="ed017-2865">Exemplo: JSON para usar Autenticação SQL</span><span class="sxs-lookup"><span data-stu-id="ed017-2865">Example: JSON for using SQL Authentication</span></span>

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
#### <a name="example-json-for-using-windows-authentication"></a><span data-ttu-id="ed017-2866">Exemplo: JSON para usar Autenticação Windows</span><span class="sxs-lookup"><span data-stu-id="ed017-2866">Example: JSON for using Windows Authentication</span></span>

<span data-ttu-id="ed017-2867">Se o nome de usuário e senha forem especificados, gateway usa tooimpersonate Olá dados do usuário especificado conta tooconnect toohello local do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="ed017-2867">If username and password are specified, gateway uses them tooimpersonate hello specified user account tooconnect toohello on-premises SQL Server database.</span></span> <span data-ttu-id="ed017-2868">Caso contrário, o gateway conecta toohello do SQL Server diretamente com o contexto de segurança de saudação do Gateway (sua conta de inicialização).</span><span class="sxs-lookup"><span data-stu-id="ed017-2868">Otherwise, gateway connects toohello SQL Server directly with hello security context of Gateway (its startup account).</span></span>

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

<span data-ttu-id="ed017-2869">Para obter mais informações, consulte o artigo [Conector de SQL Server](data-factory-sqlserver-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="ed017-2869">For more information, see [SQL Server connector](data-factory-sqlserver-connector.md#linked-service-properties) article.</span></span>

## <a name="data-transformation-activities"></a><span data-ttu-id="ed017-2870">ATIVIDADES DE TRANSFORMAÇÃO DE DADOS</span><span class="sxs-lookup"><span data-stu-id="ed017-2870">DATA TRANSFORMATION ACTIVITIES</span></span>

<span data-ttu-id="ed017-2871">Atividade</span><span class="sxs-lookup"><span data-stu-id="ed017-2871">Activity</span></span> | <span data-ttu-id="ed017-2872">Descrição</span><span class="sxs-lookup"><span data-stu-id="ed017-2872">Description</span></span>
-------- | -----------
[<span data-ttu-id="ed017-2873">Atividade de Hive do HDInsight</span><span class="sxs-lookup"><span data-stu-id="ed017-2873">HDInsight Hive activity</span></span>](#hdinsight-hive-activity) | <span data-ttu-id="ed017-2874">Hello atividade Hive do HDInsight em um pipeline da fábrica de dados executa consultas de Hive por conta própria ou cluster do HDInsight baseados no Windows/Linux sob demanda.</span><span class="sxs-lookup"><span data-stu-id="ed017-2874">hello HDInsight Hive activity in a Data Factory pipeline executes Hive queries on your own or on-demand Windows/Linux-based HDInsight cluster.</span></span> 
[<span data-ttu-id="ed017-2875">Atividade de Pig do HDInsight</span><span class="sxs-lookup"><span data-stu-id="ed017-2875">HDInsight Pig activity</span></span>](#hdinsight-pig-activity) | <span data-ttu-id="ed017-2876">Hello atividade de Pig de HDInsight em um pipeline da fábrica de dados executa consultas de Pig por conta própria ou cluster do HDInsight baseados no Windows/Linux sob demanda.</span><span class="sxs-lookup"><span data-stu-id="ed017-2876">hello HDInsight Pig activity in a Data Factory pipeline executes Pig queries on your own or on-demand Windows/Linux-based HDInsight cluster.</span></span>
[<span data-ttu-id="ed017-2877">Atividade de MapReduce do HDInsight</span><span class="sxs-lookup"><span data-stu-id="ed017-2877">HDInsight MapReduce Activity</span></span>](#hdinsight-mapreduce-activity) | <span data-ttu-id="ed017-2878">Hello atividade MapReduce do HDInsight em um pipeline da fábrica de dados executa programas de MapReduce por conta própria ou cluster do HDInsight baseados no Windows/Linux sob demanda.</span><span class="sxs-lookup"><span data-stu-id="ed017-2878">hello HDInsight MapReduce activity in a Data Factory pipeline executes MapReduce programs on your own or on-demand Windows/Linux-based HDInsight cluster.</span></span>
[<span data-ttu-id="ed017-2879">Atividade de Streaming do HDInsight</span><span class="sxs-lookup"><span data-stu-id="ed017-2879">HDInsight Streaming Activity</span></span>](#hdinsight-streaming-activity) | <span data-ttu-id="ed017-2880">Hello atividade de transmissão do HDInsight em um pipeline da fábrica de dados executa programas de transmissão do Hadoop por conta própria ou cluster do HDInsight baseados no Windows/Linux sob demanda.</span><span class="sxs-lookup"><span data-stu-id="ed017-2880">hello HDInsight Streaming Activity in a Data Factory pipeline executes Hadoop Streaming programs on your own or on-demand Windows/Linux-based HDInsight cluster.</span></span>
[<span data-ttu-id="ed017-2881">Atividade do HDInsight Spark</span><span class="sxs-lookup"><span data-stu-id="ed017-2881">HDInsight Spark Activity</span></span>](#hdinsight-spark-activity) | <span data-ttu-id="ed017-2882">Hello atividade de HDInsight Spark em um pipeline da fábrica de dados executa programas Spark no seu próprio cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="ed017-2882">hello HDInsight Spark activity in a Data Factory pipeline executes Spark programs on your own HDInsight cluster.</span></span> 
[<span data-ttu-id="ed017-2883">Atividade de Execução em Lote do Machine Learning</span><span class="sxs-lookup"><span data-stu-id="ed017-2883">Machine Learning Batch Execution Activity</span></span>](#machine-learning-batch-execution-activity) | <span data-ttu-id="ed017-2884">Habilita de fábrica de dados do Azure tooeasily você criar pipelines que usam o aprendizado de máquina publicado web service para análise preditiva.</span><span class="sxs-lookup"><span data-stu-id="ed017-2884">Azure Data Factory enables you tooeasily create pipelines that use a published Azure Machine Learning web service for predictive analytics.</span></span> <span data-ttu-id="ed017-2885">Usando hello atividade de execução em lote em um pipeline da fábrica de dados do Azure, você pode invocar um toomake previsões do aprendizado de máquina web serviço nos dados de saudação em lote.</span><span class="sxs-lookup"><span data-stu-id="ed017-2885">Using hello Batch Execution Activity in an Azure Data Factory pipeline, you can invoke a Machine Learning web service toomake predictions on hello data in batch.</span></span> 
[<span data-ttu-id="ed017-2886">Atividade do Recurso de Atualização do Machine Learning</span><span class="sxs-lookup"><span data-stu-id="ed017-2886">Machine Learning Update Resource Activity</span></span>](#machine-learning-update-resource-activity) | <span data-ttu-id="ed017-2887">Ao longo do tempo, modelos de previsão de saudação em Olá aprendizado de máquina experiências de pontuação necessário toobe treinados novamente usando novos conjuntos de dados de entrada.</span><span class="sxs-lookup"><span data-stu-id="ed017-2887">Over time, hello predictive models in hello Machine Learning scoring experiments need toobe retrained using new input datasets.</span></span> <span data-ttu-id="ed017-2888">Depois que você treinamento, você deseja tooupdate Olá pontuação serviço web com hello treinados novamente o modelo de aprendizado de máquina.</span><span class="sxs-lookup"><span data-stu-id="ed017-2888">After you are done with retraining, you want tooupdate hello scoring web service with hello retrained Machine Learning model.</span></span> <span data-ttu-id="ed017-2889">Você pode usar o hello serviço web do atividade do recurso de atualização tooupdate Olá com modelo Olá recentemente treinado.</span><span class="sxs-lookup"><span data-stu-id="ed017-2889">You can use hello Update Resource Activity tooupdate hello web service with hello newly trained model.</span></span>
[<span data-ttu-id="ed017-2890">Atividade de Procedimento Armazenado</span><span class="sxs-lookup"><span data-stu-id="ed017-2890">Stored Procedure Activity</span></span>](#stored-procedure-activity) | <span data-ttu-id="ed017-2891">Você pode usar a atividade de procedimento armazenado de saudação em um pipeline de fábrica de dados tooinvoke um procedimento armazenado em uma saudação armazenamentos de dados a seguir: Azure SQL Database, Azure SQL Data Warehouse, banco de dados do SQL Server em sua empresa ou de uma VM do Azure.</span><span class="sxs-lookup"><span data-stu-id="ed017-2891">You can use hello Stored Procedure activity in a Data Factory pipeline tooinvoke a stored procedure in one of hello following data stores: Azure SQL Database, Azure SQL Data Warehouse, SQL Server Database in your enterprise or an Azure VM.</span></span> 
[<span data-ttu-id="ed017-2892">Atividade de U-SQL do Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="ed017-2892">Data Lake Analytics U-SQL activity</span></span>](#data-lake-analytics-u-sql-activity) | <span data-ttu-id="ed017-2893">A atividade de U-SQL do Data Lake Analytics executa um script U-SQL em um cluster do Azure Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="ed017-2893">Data Lake Analytics U-SQL Activity runs a U-SQL script on an Azure Data Lake Analytics cluster.</span></span>  
[<span data-ttu-id="ed017-2894">Atividade personalizada do .NET</span><span class="sxs-lookup"><span data-stu-id="ed017-2894">.NET custom activity</span></span>](#net-custom-activity) | <span data-ttu-id="ed017-2895">Se você precisar tootransform dados de forma que não é suportada pela fábrica de dados, você pode criar uma atividade personalizada com sua própria lógica de processamento de dados e usar atividade Olá no pipeline de saudação.</span><span class="sxs-lookup"><span data-stu-id="ed017-2895">If you need tootransform data in a way that is not supported by Data Factory, you can create a custom activity with your own data processing logic and use hello activity in hello pipeline.</span></span> <span data-ttu-id="ed017-2896">Você pode configurar Olá personalizado .NET atividade toorun usando um serviço de lote do Azure ou um cluster Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="ed017-2896">You can configure hello custom .NET activity toorun using either an Azure Batch service or an Azure HDInsight cluster.</span></span> 

     
## <a name="hdinsight-hive-activity"></a><span data-ttu-id="ed017-2897">Atividade de Hive do HDInsight</span><span class="sxs-lookup"><span data-stu-id="ed017-2897">HDInsight Hive Activity</span></span>
<span data-ttu-id="ed017-2898">Você pode especificar Olá seguintes propriedades em uma definição de JSON da atividade de Hive.</span><span class="sxs-lookup"><span data-stu-id="ed017-2898">You can specify hello following properties in a Hive Activity JSON definition.</span></span> <span data-ttu-id="ed017-2899">a propriedade de tipo Hello atividade Olá deve ser: **HDInsightHive**.</span><span class="sxs-lookup"><span data-stu-id="ed017-2899">hello type property for hello activity must be: **HDInsightHive**.</span></span> <span data-ttu-id="ed017-2900">Você deve primeiro criar um serviço vinculado do HDInsight e especificar o nome de saudação-lo como um valor para Olá **linkedServiceName** propriedade.</span><span class="sxs-lookup"><span data-stu-id="ed017-2900">You must create a HDInsight linked service first and specify hello name of it as a value for hello **linkedServiceName** property.</span></span> <span data-ttu-id="ed017-2901">Olá propriedades a seguir têm suporte no hello **typeProperties** seção quando você define o tipo de saudação do tooHDInsightHive de atividade:</span><span class="sxs-lookup"><span data-stu-id="ed017-2901">hello following properties are supported in hello **typeProperties** section when you set hello type of activity tooHDInsightHive:</span></span>

| <span data-ttu-id="ed017-2902">Propriedade</span><span class="sxs-lookup"><span data-stu-id="ed017-2902">Property</span></span> | <span data-ttu-id="ed017-2903">Descrição</span><span class="sxs-lookup"><span data-stu-id="ed017-2903">Description</span></span> | <span data-ttu-id="ed017-2904">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="ed017-2904">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ed017-2905">script</span><span class="sxs-lookup"><span data-stu-id="ed017-2905">script</span></span> |<span data-ttu-id="ed017-2906">Especifique o script de Hive Olá embutido</span><span class="sxs-lookup"><span data-stu-id="ed017-2906">Specify hello Hive script inline</span></span> |<span data-ttu-id="ed017-2907">Não</span><span class="sxs-lookup"><span data-stu-id="ed017-2907">No</span></span> |
| <span data-ttu-id="ed017-2908">caminho do script</span><span class="sxs-lookup"><span data-stu-id="ed017-2908">script path</span></span> |<span data-ttu-id="ed017-2909">Saudação de repositório Hive script em um armazenamento de BLOBs do Azure e fornecer Olá caminho toohello arquivo.</span><span class="sxs-lookup"><span data-stu-id="ed017-2909">Store hello Hive script in an Azure blob storage and provide hello path toohello file.</span></span> <span data-ttu-id="ed017-2910">Use a propriedade 'script' ou 'scriptPath'.</span><span class="sxs-lookup"><span data-stu-id="ed017-2910">Use 'script' or 'scriptPath' property.</span></span> <span data-ttu-id="ed017-2911">As duas não podem ser usadas juntas.</span><span class="sxs-lookup"><span data-stu-id="ed017-2911">Both cannot be used together.</span></span> <span data-ttu-id="ed017-2912">nome do arquivo Hello diferencia maiusculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="ed017-2912">hello file name is case-sensitive.</span></span> |<span data-ttu-id="ed017-2913">Não</span><span class="sxs-lookup"><span data-stu-id="ed017-2913">No</span></span> |
| <span data-ttu-id="ed017-2914">define</span><span class="sxs-lookup"><span data-stu-id="ed017-2914">defines</span></span> |<span data-ttu-id="ed017-2915">Especifique parâmetros como pares chave/valor para fazer referência a no script do Hive hello usando 'hiveconf'</span><span class="sxs-lookup"><span data-stu-id="ed017-2915">Specify parameters as key/value pairs for referencing within hello Hive script using 'hiveconf'</span></span> |<span data-ttu-id="ed017-2916">Não</span><span class="sxs-lookup"><span data-stu-id="ed017-2916">No</span></span> |

<span data-ttu-id="ed017-2917">Essas propriedades de tipo são específico toohello atividade de Hive.</span><span class="sxs-lookup"><span data-stu-id="ed017-2917">These type properties are specific toohello Hive Activity.</span></span> <span data-ttu-id="ed017-2918">Há suporte para todas as atividades de outras propriedades (fora de saudação typeProperties seção).</span><span class="sxs-lookup"><span data-stu-id="ed017-2918">Other properties (outside hello typeProperties section) are supported for all activities.</span></span>   

### <a name="json-example"></a><span data-ttu-id="ed017-2919">Exemplo de JSON</span><span class="sxs-lookup"><span data-stu-id="ed017-2919">JSON example</span></span>
<span data-ttu-id="ed017-2920">Olá JSON a seguir define uma atividade de HDInsight Hive em um pipeline.</span><span class="sxs-lookup"><span data-stu-id="ed017-2920">hello following JSON defines a HDInsight Hive activity in a pipeline.</span></span>  

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

<span data-ttu-id="ed017-2921">Para saber mais, consulte o artigo [Atividade de Hive](data-factory-hive-activity.md).</span><span class="sxs-lookup"><span data-stu-id="ed017-2921">For more information, see [Hive Activity](data-factory-hive-activity.md) article.</span></span> 

## <a name="hdinsight-pig-activity"></a><span data-ttu-id="ed017-2922">Atividade de Pig do HDInsight</span><span class="sxs-lookup"><span data-stu-id="ed017-2922">HDInsight Pig Activity</span></span>
<span data-ttu-id="ed017-2923">Você pode especificar Olá seguintes propriedades em uma definição de JSON da atividade de Pig.</span><span class="sxs-lookup"><span data-stu-id="ed017-2923">You can specify hello following properties in a Pig Activity JSON definition.</span></span> <span data-ttu-id="ed017-2924">a propriedade de tipo Hello atividade Olá deve ser: **HDInsightPig**.</span><span class="sxs-lookup"><span data-stu-id="ed017-2924">hello type property for hello activity must be: **HDInsightPig**.</span></span> <span data-ttu-id="ed017-2925">Você deve primeiro criar um serviço vinculado do HDInsight e especificar o nome de saudação-lo como um valor para Olá **linkedServiceName** propriedade.</span><span class="sxs-lookup"><span data-stu-id="ed017-2925">You must create a HDInsight linked service first and specify hello name of it as a value for hello **linkedServiceName** property.</span></span> <span data-ttu-id="ed017-2926">Olá propriedades a seguir têm suporte no hello **typeProperties** seção quando você define o tipo de saudação do tooHDInsightPig de atividade:</span><span class="sxs-lookup"><span data-stu-id="ed017-2926">hello following properties are supported in hello **typeProperties** section when you set hello type of activity tooHDInsightPig:</span></span> 

| <span data-ttu-id="ed017-2927">Propriedade</span><span class="sxs-lookup"><span data-stu-id="ed017-2927">Property</span></span> | <span data-ttu-id="ed017-2928">Descrição</span><span class="sxs-lookup"><span data-stu-id="ed017-2928">Description</span></span> | <span data-ttu-id="ed017-2929">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="ed017-2929">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ed017-2930">script</span><span class="sxs-lookup"><span data-stu-id="ed017-2930">script</span></span> |<span data-ttu-id="ed017-2931">Especificar Olá Pig script embutido</span><span class="sxs-lookup"><span data-stu-id="ed017-2931">Specify hello Pig script inline</span></span> |<span data-ttu-id="ed017-2932">Não</span><span class="sxs-lookup"><span data-stu-id="ed017-2932">No</span></span> |
| <span data-ttu-id="ed017-2933">caminho do script</span><span class="sxs-lookup"><span data-stu-id="ed017-2933">script path</span></span> |<span data-ttu-id="ed017-2934">Armazenar o script de Pig de saudação em um armazenamento de BLOBs do Azure e fornecer Olá caminho toohello arquivo.</span><span class="sxs-lookup"><span data-stu-id="ed017-2934">Store hello Pig script in an Azure blob storage and provide hello path toohello file.</span></span> <span data-ttu-id="ed017-2935">Use a propriedade 'script' ou 'scriptPath'.</span><span class="sxs-lookup"><span data-stu-id="ed017-2935">Use 'script' or 'scriptPath' property.</span></span> <span data-ttu-id="ed017-2936">As duas não podem ser usadas juntas.</span><span class="sxs-lookup"><span data-stu-id="ed017-2936">Both cannot be used together.</span></span> <span data-ttu-id="ed017-2937">nome do arquivo Hello diferencia maiusculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="ed017-2937">hello file name is case-sensitive.</span></span> |<span data-ttu-id="ed017-2938">Não</span><span class="sxs-lookup"><span data-stu-id="ed017-2938">No</span></span> |
| <span data-ttu-id="ed017-2939">define</span><span class="sxs-lookup"><span data-stu-id="ed017-2939">defines</span></span> |<span data-ttu-id="ed017-2940">Especifique parâmetros como pares chave/valor para fazer referência a no script de Pig de saudação</span><span class="sxs-lookup"><span data-stu-id="ed017-2940">Specify parameters as key/value pairs for referencing within hello Pig script</span></span> |<span data-ttu-id="ed017-2941">Não</span><span class="sxs-lookup"><span data-stu-id="ed017-2941">No</span></span> |

<span data-ttu-id="ed017-2942">Essas propriedades de tipo são específico toohello atividade de Pig.</span><span class="sxs-lookup"><span data-stu-id="ed017-2942">These type properties are specific toohello Pig Activity.</span></span> <span data-ttu-id="ed017-2943">Há suporte para todas as atividades de outras propriedades (fora de saudação typeProperties seção).</span><span class="sxs-lookup"><span data-stu-id="ed017-2943">Other properties (outside hello typeProperties section) are supported for all activities.</span></span>   

### <a name="json-example"></a><span data-ttu-id="ed017-2944">Exemplo de JSON</span><span class="sxs-lookup"><span data-stu-id="ed017-2944">JSON example</span></span>

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

<span data-ttu-id="ed017-2945">Para saber mais, consulte o artigo [Atividade de Pig](#data-factory-pig-activity.md).</span><span class="sxs-lookup"><span data-stu-id="ed017-2945">For more information, see [Pig Activity](#data-factory-pig-activity.md) article.</span></span> 

## <a name="hdinsight-mapreduce-activity"></a><span data-ttu-id="ed017-2946">Atividade de MapReduce do HDInsight</span><span class="sxs-lookup"><span data-stu-id="ed017-2946">HDInsight MapReduce Activity</span></span>
<span data-ttu-id="ed017-2947">Você pode especificar Olá seguintes propriedades em uma definição de JSON da atividade MapReduce.</span><span class="sxs-lookup"><span data-stu-id="ed017-2947">You can specify hello following properties in a MapReduce Activity JSON definition.</span></span> <span data-ttu-id="ed017-2948">a propriedade de tipo Hello atividade Olá deve ser: **HDInsightMapReduce**.</span><span class="sxs-lookup"><span data-stu-id="ed017-2948">hello type property for hello activity must be: **HDInsightMapReduce**.</span></span> <span data-ttu-id="ed017-2949">Você deve primeiro criar um serviço vinculado do HDInsight e especificar o nome de saudação-lo como um valor para Olá **linkedServiceName** propriedade.</span><span class="sxs-lookup"><span data-stu-id="ed017-2949">You must create a HDInsight linked service first and specify hello name of it as a value for hello **linkedServiceName** property.</span></span> <span data-ttu-id="ed017-2950">Olá propriedades a seguir têm suporte no hello **typeProperties** seção quando você define o tipo de saudação do tooHDInsightMapReduce de atividade:</span><span class="sxs-lookup"><span data-stu-id="ed017-2950">hello following properties are supported in hello **typeProperties** section when you set hello type of activity tooHDInsightMapReduce:</span></span> 

| <span data-ttu-id="ed017-2951">Propriedade</span><span class="sxs-lookup"><span data-stu-id="ed017-2951">Property</span></span> | <span data-ttu-id="ed017-2952">Descrição</span><span class="sxs-lookup"><span data-stu-id="ed017-2952">Description</span></span> | <span data-ttu-id="ed017-2953">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="ed017-2953">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ed017-2954">jarLinkedService</span><span class="sxs-lookup"><span data-stu-id="ed017-2954">jarLinkedService</span></span> | <span data-ttu-id="ed017-2955">Nome do hello vinculado de serviço para Olá armazenamento do Azure que contém o arquivo JAR de saudação.</span><span class="sxs-lookup"><span data-stu-id="ed017-2955">Name of hello linked service for hello Azure Storage that contains hello JAR file.</span></span> | <span data-ttu-id="ed017-2956">Sim</span><span class="sxs-lookup"><span data-stu-id="ed017-2956">Yes</span></span> |
| <span data-ttu-id="ed017-2957">jarFilePath</span><span class="sxs-lookup"><span data-stu-id="ed017-2957">jarFilePath</span></span> | <span data-ttu-id="ed017-2958">Caminho toohello JAR arquivo no armazenamento do Azure de saudação.</span><span class="sxs-lookup"><span data-stu-id="ed017-2958">Path toohello JAR file in hello Azure Storage.</span></span> | <span data-ttu-id="ed017-2959">Sim</span><span class="sxs-lookup"><span data-stu-id="ed017-2959">Yes</span></span> | 
| <span data-ttu-id="ed017-2960">className</span><span class="sxs-lookup"><span data-stu-id="ed017-2960">className</span></span> | <span data-ttu-id="ed017-2961">Nome da classe principal do hello no arquivo JAR de saudação.</span><span class="sxs-lookup"><span data-stu-id="ed017-2961">Name of hello main class in hello JAR file.</span></span> | <span data-ttu-id="ed017-2962">Sim</span><span class="sxs-lookup"><span data-stu-id="ed017-2962">Yes</span></span> | 
| <span data-ttu-id="ed017-2963">argumentos</span><span class="sxs-lookup"><span data-stu-id="ed017-2963">arguments</span></span> | <span data-ttu-id="ed017-2964">Uma lista de argumentos separados por vírgulas para programas de MapReduce hello.</span><span class="sxs-lookup"><span data-stu-id="ed017-2964">A list of comma-separated arguments for hello MapReduce program.</span></span> <span data-ttu-id="ed017-2965">Em tempo de execução, você ver alguns argumentos adicionais (por exemplo: mapreduce.job.tags) da estrutura de MapReduce hello.</span><span class="sxs-lookup"><span data-stu-id="ed017-2965">At runtime, you see a few extra arguments (for example: mapreduce.job.tags) from hello MapReduce framework.</span></span> <span data-ttu-id="ed017-2966">toodifferentiate seus argumentos com argumentos de MapReduce hello, considere o uso de opção e valor como argumentos conforme mostrado no exemplo a seguir de saudação (- s, - entrada, --saída etc., são imediatamente seguidas por seus valores de opções)</span><span class="sxs-lookup"><span data-stu-id="ed017-2966">toodifferentiate your arguments with hello MapReduce arguments, consider using both option and value as arguments as shown in hello following example (-s, --input, --output etc., are options immediately followed by their values)</span></span> | <span data-ttu-id="ed017-2967">Não</span><span class="sxs-lookup"><span data-stu-id="ed017-2967">No</span></span> | 

### <a name="json-example"></a><span data-ttu-id="ed017-2968">Exemplo de JSON</span><span class="sxs-lookup"><span data-stu-id="ed017-2968">JSON example</span></span>

```json
{
    "name": "MahoutMapReduceSamplePipeline",
    "properties": {
        "description": "Sample Pipeline tooRun a Mahout Custom Map Reduce Jar. This job calculates an Item Similarity Matrix toodetermine hello similarity between two items",
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
                "description": "Custom Map Reduce toogenerate Mahout result",
                "linkedServiceName": "HDInsightLinkedService"
            }
        ],
        "start": "2017-01-03T00:00:00",
        "end": "2017-01-04T00:00:00"
    }
}
```

<span data-ttu-id="ed017-2969">Para saber mais, consulte o artigo [Atividade MapReduce](data-factory-map-reduce.md).</span><span class="sxs-lookup"><span data-stu-id="ed017-2969">For more information, see [MapReduce Activity](data-factory-map-reduce.md) article.</span></span> 

## <a name="hdinsight-streaming-activity"></a><span data-ttu-id="ed017-2970">Atividade de Streaming do HDInsight</span><span class="sxs-lookup"><span data-stu-id="ed017-2970">HDInsight Streaming Activity</span></span>
<span data-ttu-id="ed017-2971">Você pode especificar Olá seguintes propriedades em uma definição de Hadoop Streaming JSON da atividade.</span><span class="sxs-lookup"><span data-stu-id="ed017-2971">You can specify hello following properties in a Hadoop Streaming Activity JSON definition.</span></span> <span data-ttu-id="ed017-2972">a propriedade de tipo Hello atividade Olá deve ser: **HDInsightStreaming**.</span><span class="sxs-lookup"><span data-stu-id="ed017-2972">hello type property for hello activity must be: **HDInsightStreaming**.</span></span> <span data-ttu-id="ed017-2973">Você deve primeiro criar um serviço vinculado do HDInsight e especificar o nome de saudação-lo como um valor para Olá **linkedServiceName** propriedade.</span><span class="sxs-lookup"><span data-stu-id="ed017-2973">You must create a HDInsight linked service first and specify hello name of it as a value for hello **linkedServiceName** property.</span></span> <span data-ttu-id="ed017-2974">Olá propriedades a seguir têm suporte no hello **typeProperties** seção quando você define o tipo de saudação do tooHDInsightStreaming de atividade:</span><span class="sxs-lookup"><span data-stu-id="ed017-2974">hello following properties are supported in hello **typeProperties** section when you set hello type of activity tooHDInsightStreaming:</span></span> 

| <span data-ttu-id="ed017-2975">Propriedade</span><span class="sxs-lookup"><span data-stu-id="ed017-2975">Property</span></span> | <span data-ttu-id="ed017-2976">Descrição</span><span class="sxs-lookup"><span data-stu-id="ed017-2976">Description</span></span> | 
| --- | --- |
| <span data-ttu-id="ed017-2977">mapper</span><span class="sxs-lookup"><span data-stu-id="ed017-2977">mapper</span></span> | <span data-ttu-id="ed017-2978">Nome do executável do mapeador de saudação.</span><span class="sxs-lookup"><span data-stu-id="ed017-2978">Name of hello mapper executable.</span></span> <span data-ttu-id="ed017-2979">Exemplo hello, cat.exe é executável do mapeador de saudação.</span><span class="sxs-lookup"><span data-stu-id="ed017-2979">In hello example, cat.exe is hello mapper executable.</span></span>| 
| <span data-ttu-id="ed017-2980">reducer</span><span class="sxs-lookup"><span data-stu-id="ed017-2980">reducer</span></span> | <span data-ttu-id="ed017-2981">Nome de saudação do executável do Redutor.</span><span class="sxs-lookup"><span data-stu-id="ed017-2981">Name of hello reducer executable.</span></span> <span data-ttu-id="ed017-2982">Exemplo hello, wc.exe é Redutor de saudação executável.</span><span class="sxs-lookup"><span data-stu-id="ed017-2982">In hello example, wc.exe is hello reducer executable.</span></span> | 
| <span data-ttu-id="ed017-2983">input</span><span class="sxs-lookup"><span data-stu-id="ed017-2983">input</span></span> | <span data-ttu-id="ed017-2984">Arquivo de entrada (incluindo local) para o mapeador de saudação.</span><span class="sxs-lookup"><span data-stu-id="ed017-2984">Input file (including location) for hello mapper.</span></span> <span data-ttu-id="ed017-2985">No exemplo hello: "wasb<account name>.blob.core.windows.net/example/data/gutenberg/davinci.txt": adfsample é o contêiner de blob hello, example/data/Gutenberg é a pasta de saudação e davinci.txt é Olá blob.</span><span class="sxs-lookup"><span data-stu-id="ed017-2985">In hello example: "wasb://adfsample@<account name>.blob.core.windows.net/example/data/gutenberg/davinci.txt": adfsample is hello blob container, example/data/Gutenberg is hello folder, and davinci.txt is hello blob.</span></span> |
| <span data-ttu-id="ed017-2986">output</span><span class="sxs-lookup"><span data-stu-id="ed017-2986">output</span></span> | <span data-ttu-id="ed017-2987">Arquivo de saída (incluindo local) para Redutor hello.</span><span class="sxs-lookup"><span data-stu-id="ed017-2987">Output file (including location) for hello reducer.</span></span> <span data-ttu-id="ed017-2988">saída de saudação do trabalho de transmissão do Hadoop Olá é gravada toohello local especificado para esta propriedade.</span><span class="sxs-lookup"><span data-stu-id="ed017-2988">hello output of hello Hadoop Streaming job is written toohello location specified for this property.</span></span> |
| <span data-ttu-id="ed017-2989">filePaths</span><span class="sxs-lookup"><span data-stu-id="ed017-2989">filePaths</span></span> | <span data-ttu-id="ed017-2990">Caminhos para executáveis do mapeador e Redutor hello.</span><span class="sxs-lookup"><span data-stu-id="ed017-2990">Paths for hello mapper and reducer executables.</span></span> <span data-ttu-id="ed017-2991">No exemplo hello: "adfsample/example/apps/wc.exe", adfsample é o contêiner de blob hello, example/apps é a pasta hello e wc.exe é hello executável.</span><span class="sxs-lookup"><span data-stu-id="ed017-2991">In hello example: "adfsample/example/apps/wc.exe", adfsample is hello blob container, example/apps is hello folder, and wc.exe is hello executable.</span></span> | 
| <span data-ttu-id="ed017-2992">fileLinkedService</span><span class="sxs-lookup"><span data-stu-id="ed017-2992">fileLinkedService</span></span> | <span data-ttu-id="ed017-2993">Serviço vinculado do armazenamento do Azure que representa Olá armazenamento do Azure que contém arquivos de saudação especificados na seção de filePaths hello.</span><span class="sxs-lookup"><span data-stu-id="ed017-2993">Azure Storage linked service that represents hello Azure storage that contains hello files specified in hello filePaths section.</span></span> | 
| <span data-ttu-id="ed017-2994">argumentos</span><span class="sxs-lookup"><span data-stu-id="ed017-2994">arguments</span></span> | <span data-ttu-id="ed017-2995">Uma lista de argumentos separados por vírgulas para programas de MapReduce hello.</span><span class="sxs-lookup"><span data-stu-id="ed017-2995">A list of comma-separated arguments for hello MapReduce program.</span></span> <span data-ttu-id="ed017-2996">Em tempo de execução, você ver alguns argumentos adicionais (por exemplo: mapreduce.job.tags) da estrutura de MapReduce hello.</span><span class="sxs-lookup"><span data-stu-id="ed017-2996">At runtime, you see a few extra arguments (for example: mapreduce.job.tags) from hello MapReduce framework.</span></span> <span data-ttu-id="ed017-2997">toodifferentiate seus argumentos com argumentos de MapReduce hello, considere o uso de opção e valor como argumentos conforme mostrado no exemplo a seguir de saudação (- s, - entrada, --saída etc., são imediatamente seguidas por seus valores de opções)</span><span class="sxs-lookup"><span data-stu-id="ed017-2997">toodifferentiate your arguments with hello MapReduce arguments, consider using both option and value as arguments as shown in hello following example (-s, --input, --output etc., are options immediately followed by their values)</span></span> | 
| <span data-ttu-id="ed017-2998">getDebugInfo</span><span class="sxs-lookup"><span data-stu-id="ed017-2998">getDebugInfo</span></span> | <span data-ttu-id="ed017-2999">Um elemento opcional.</span><span class="sxs-lookup"><span data-stu-id="ed017-2999">An optional element.</span></span> <span data-ttu-id="ed017-3000">Quando estiver definido como tooFailure, Olá logs são baixadas apenas em caso de falha.</span><span class="sxs-lookup"><span data-stu-id="ed017-3000">When it is set tooFailure, hello logs are downloaded only on failure.</span></span> <span data-ttu-id="ed017-3001">Quando estiver definido como tooAll, logs são sempre baixados independentemente do status de execução de saudação.</span><span class="sxs-lookup"><span data-stu-id="ed017-3001">When it is set tooAll, logs are always downloaded irrespective of hello execution status.</span></span> | 

> [!NOTE]
> <span data-ttu-id="ed017-3002">Você deve especificar um conjunto de dados de saída para hello Hadoop Streaming Activity para Olá **gera** propriedade.</span><span class="sxs-lookup"><span data-stu-id="ed017-3002">You must specify an output dataset for hello Hadoop Streaming Activity for hello **outputs** property.</span></span> <span data-ttu-id="ed017-3003">Este conjunto de dados pode ser um dataset fictício que é necessário toodrive Olá pipeline agenda (por hora, diariamente, etc.).</span><span class="sxs-lookup"><span data-stu-id="ed017-3003">This dataset can be just a dummy dataset that is required toodrive hello pipeline schedule (hourly, daily, etc.).</span></span> <span data-ttu-id="ed017-3004">Se a atividade de saudação não tem uma entrada, você pode ignorar especificando um conjunto de dados de entrada para a atividade de saudação para Olá **entradas** propriedade.</span><span class="sxs-lookup"><span data-stu-id="ed017-3004">If hello activity doesn't take an input, you can skip specifying an input dataset for hello activity for hello **inputs** property.</span></span>  

## <a name="json-example"></a><span data-ttu-id="ed017-3005">Exemplo de JSON</span><span class="sxs-lookup"><span data-stu-id="ed017-3005">JSON example</span></span>

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

<span data-ttu-id="ed017-3006">Para saber mais, consulte o artigo [Atividade de Transmissão do Hadoop](data-factory-hadoop-streaming-activity.md).</span><span class="sxs-lookup"><span data-stu-id="ed017-3006">For more information, see [Hadoop Streaming Activity](data-factory-hadoop-streaming-activity.md) article.</span></span> 

## <a name="hdinsight-spark-activity"></a><span data-ttu-id="ed017-3007">Atividade do HDInsight Spark</span><span class="sxs-lookup"><span data-stu-id="ed017-3007">HDInsight Spark Activity</span></span>
<span data-ttu-id="ed017-3008">Você pode especificar Olá seguintes propriedades em uma definição de JSON da atividade Spark.</span><span class="sxs-lookup"><span data-stu-id="ed017-3008">You can specify hello following properties in a Spark Activity JSON definition.</span></span> <span data-ttu-id="ed017-3009">a propriedade de tipo Hello atividade Olá deve ser: **HDInsightSpark**.</span><span class="sxs-lookup"><span data-stu-id="ed017-3009">hello type property for hello activity must be: **HDInsightSpark**.</span></span> <span data-ttu-id="ed017-3010">Você deve primeiro criar um serviço vinculado do HDInsight e especificar o nome de saudação-lo como um valor para Olá **linkedServiceName** propriedade.</span><span class="sxs-lookup"><span data-stu-id="ed017-3010">You must create a HDInsight linked service first and specify hello name of it as a value for hello **linkedServiceName** property.</span></span> <span data-ttu-id="ed017-3011">Olá propriedades a seguir têm suporte no hello **typeProperties** seção quando você define o tipo de saudação do tooHDInsightSpark de atividade:</span><span class="sxs-lookup"><span data-stu-id="ed017-3011">hello following properties are supported in hello **typeProperties** section when you set hello type of activity tooHDInsightSpark:</span></span> 

| <span data-ttu-id="ed017-3012">Propriedade</span><span class="sxs-lookup"><span data-stu-id="ed017-3012">Property</span></span> | <span data-ttu-id="ed017-3013">Descrição</span><span class="sxs-lookup"><span data-stu-id="ed017-3013">Description</span></span> | <span data-ttu-id="ed017-3014">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="ed017-3014">Required</span></span> |
| -------- | ----------- | -------- |
| <span data-ttu-id="ed017-3015">rootPath</span><span class="sxs-lookup"><span data-stu-id="ed017-3015">rootPath</span></span> | <span data-ttu-id="ed017-3016">contêiner de BLOBs do Azure Hello e pasta que contém o arquivo do Spark hello.</span><span class="sxs-lookup"><span data-stu-id="ed017-3016">hello Azure Blob container and folder that contains hello Spark file.</span></span> <span data-ttu-id="ed017-3017">nome do arquivo Hello diferencia maiusculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="ed017-3017">hello file name is case-sensitive.</span></span> | <span data-ttu-id="ed017-3018">Sim</span><span class="sxs-lookup"><span data-stu-id="ed017-3018">Yes</span></span> |
| <span data-ttu-id="ed017-3019">entryFilePath</span><span class="sxs-lookup"><span data-stu-id="ed017-3019">entryFilePath</span></span> | <span data-ttu-id="ed017-3020">Pasta de raiz de toohello de caminho relativo da saudação Spark/pacote de código.</span><span class="sxs-lookup"><span data-stu-id="ed017-3020">Relative path toohello root folder of hello Spark code/package.</span></span> | <span data-ttu-id="ed017-3021">Sim</span><span class="sxs-lookup"><span data-stu-id="ed017-3021">Yes</span></span> |
| <span data-ttu-id="ed017-3022">className</span><span class="sxs-lookup"><span data-stu-id="ed017-3022">className</span></span> | <span data-ttu-id="ed017-3023">Classe principal de Java/Spark do aplicativo</span><span class="sxs-lookup"><span data-stu-id="ed017-3023">Application's Java/Spark main class</span></span> | <span data-ttu-id="ed017-3024">Não</span><span class="sxs-lookup"><span data-stu-id="ed017-3024">No</span></span> | 
| <span data-ttu-id="ed017-3025">argumentos</span><span class="sxs-lookup"><span data-stu-id="ed017-3025">arguments</span></span> | <span data-ttu-id="ed017-3026">Uma lista de programas de Spark toohello argumentos de linha de comando.</span><span class="sxs-lookup"><span data-stu-id="ed017-3026">A list of command-line arguments toohello Spark program.</span></span> | <span data-ttu-id="ed017-3027">Não</span><span class="sxs-lookup"><span data-stu-id="ed017-3027">No</span></span> | 
| <span data-ttu-id="ed017-3028">proxyUser</span><span class="sxs-lookup"><span data-stu-id="ed017-3028">proxyUser</span></span> | <span data-ttu-id="ed017-3029">programa de saudação usuário conta tooimpersonate tooexecute Olá Spark</span><span class="sxs-lookup"><span data-stu-id="ed017-3029">hello user account tooimpersonate tooexecute hello Spark program</span></span> | <span data-ttu-id="ed017-3030">Não</span><span class="sxs-lookup"><span data-stu-id="ed017-3030">No</span></span> | 
| <span data-ttu-id="ed017-3031">sparkConfig</span><span class="sxs-lookup"><span data-stu-id="ed017-3031">sparkConfig</span></span> | <span data-ttu-id="ed017-3032">Propriedades de configuração do Spark.</span><span class="sxs-lookup"><span data-stu-id="ed017-3032">Spark configuration properties.</span></span> | <span data-ttu-id="ed017-3033">Não</span><span class="sxs-lookup"><span data-stu-id="ed017-3033">No</span></span> | 
| <span data-ttu-id="ed017-3034">getDebugInfo</span><span class="sxs-lookup"><span data-stu-id="ed017-3034">getDebugInfo</span></span> | <span data-ttu-id="ed017-3035">Especifica quando arquivos de log do Spark Olá são copiado toohello usado pelo cluster do HDInsight de armazenamento do Azure (ou) especificado por sparkJobLinkedService.</span><span class="sxs-lookup"><span data-stu-id="ed017-3035">Specifies when hello Spark log files are copied toohello Azure storage used by HDInsight cluster (or) specified by sparkJobLinkedService.</span></span> <span data-ttu-id="ed017-3036">Valores permitidos: Nenhum, Sempre ou Falha.</span><span class="sxs-lookup"><span data-stu-id="ed017-3036">Allowed values: None, Always, or Failure.</span></span> <span data-ttu-id="ed017-3037">Valor padrão: Nenhum.</span><span class="sxs-lookup"><span data-stu-id="ed017-3037">Default value: None.</span></span> | <span data-ttu-id="ed017-3038">Não</span><span class="sxs-lookup"><span data-stu-id="ed017-3038">No</span></span> | 
| <span data-ttu-id="ed017-3039">sparkJobLinkedService</span><span class="sxs-lookup"><span data-stu-id="ed017-3039">sparkJobLinkedService</span></span> | <span data-ttu-id="ed017-3040">Olá serviço vinculado do armazenamento do Azure que contém o arquivo de trabalho do Spark hello, dependências e logs.</span><span class="sxs-lookup"><span data-stu-id="ed017-3040">hello Azure Storage linked service that holds hello Spark job file, dependencies, and logs.</span></span>  <span data-ttu-id="ed017-3041">Se você não especificar um valor para essa propriedade, armazenamento de saudação associado com o cluster HDInsight é usado.</span><span class="sxs-lookup"><span data-stu-id="ed017-3041">If you do not specify a value for this property, hello storage associated with HDInsight cluster is used.</span></span> | <span data-ttu-id="ed017-3042">Não</span><span class="sxs-lookup"><span data-stu-id="ed017-3042">No</span></span> |

### <a name="json-example"></a><span data-ttu-id="ed017-3043">Exemplo de JSON</span><span class="sxs-lookup"><span data-stu-id="ed017-3043">JSON example</span></span>

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
<span data-ttu-id="ed017-3044">Observe Olá pontos a seguir:</span><span class="sxs-lookup"><span data-stu-id="ed017-3044">Note hello following points:</span></span> 

- <span data-ttu-id="ed017-3045">Olá **tipo** propriedade for definida muito**HDInsightSpark**.</span><span class="sxs-lookup"><span data-stu-id="ed017-3045">hello **type** property is set too**HDInsightSpark**.</span></span>
- <span data-ttu-id="ed017-3046">Olá **rootPath** está definido muito**adfspark\\pyFiles** onde adfspark é o contêiner de BLOBs do Azure hello e pyFiles é a pasta bem no contêiner.</span><span class="sxs-lookup"><span data-stu-id="ed017-3046">hello **rootPath** is set too**adfspark\\pyFiles** where adfspark is hello Azure Blob container and pyFiles is fine folder in that container.</span></span> <span data-ttu-id="ed017-3047">Neste exemplo, Olá armazenamento de BLOBs do Azure é hello que está associado ao cluster do Spark hello.</span><span class="sxs-lookup"><span data-stu-id="ed017-3047">In this example, hello Azure Blob Storage is hello one that is associated with hello Spark cluster.</span></span> <span data-ttu-id="ed017-3048">Você pode carregar Olá arquivo tooa armazenamento do Azure diferente.</span><span class="sxs-lookup"><span data-stu-id="ed017-3048">You can upload hello file tooa different Azure Storage.</span></span> <span data-ttu-id="ed017-3049">Se você fizer isso, crie um toolink de serviço vinculado do armazenamento do Azure essa fábrica de dados de toohello de conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="ed017-3049">If you do so, create an Azure Storage linked service toolink that storage account toohello data factory.</span></span> <span data-ttu-id="ed017-3050">Em seguida, especifique o nome de Olá de serviço de Olá vinculado como um valor para Olá **sparkJobLinkedService** propriedade.</span><span class="sxs-lookup"><span data-stu-id="ed017-3050">Then, specify hello name of hello linked service as a value for hello **sparkJobLinkedService** property.</span></span> <span data-ttu-id="ed017-3051">Consulte [propriedades da atividade Spark](#spark-activity-properties) para obter detalhes sobre essa propriedade e outras propriedades com suporte hello atividade Spark.</span><span class="sxs-lookup"><span data-stu-id="ed017-3051">See [Spark Activity properties](#spark-activity-properties) for details about this property and other properties supported by hello Spark Activity.</span></span>
- <span data-ttu-id="ed017-3052">Olá **entryFilePath** está definida toohello **test.py**, que é o arquivo de python hello.</span><span class="sxs-lookup"><span data-stu-id="ed017-3052">hello **entryFilePath** is set toohello **test.py**, which is hello python file.</span></span> 
- <span data-ttu-id="ed017-3053">Olá **getDebugInfo** propriedade for definida muito**sempre**, que significa que os arquivos de log Olá sempre são gerados (sucesso ou falha).</span><span class="sxs-lookup"><span data-stu-id="ed017-3053">hello **getDebugInfo** property is set too**Always**, which means hello log files are always generated (success or failure).</span></span>  

    > [!IMPORTANT]
    > <span data-ttu-id="ed017-3054">É recomendável que você não defina essa propriedade tooAlways em um ambiente de produção, a menos que você estiver solucionando um problema.</span><span class="sxs-lookup"><span data-stu-id="ed017-3054">We recommend that you do not set this property tooAlways in a production environment unless you are troubleshooting an issue.</span></span> 
- <span data-ttu-id="ed017-3055">Olá **gera** seção tem um conjunto de dados de saída.</span><span class="sxs-lookup"><span data-stu-id="ed017-3055">hello **outputs** section has one output dataset.</span></span> <span data-ttu-id="ed017-3056">Você deve especificar um conjunto de dados de saída, mesmo que o programa de spark Olá não produz nenhuma saída.</span><span class="sxs-lookup"><span data-stu-id="ed017-3056">You must specify an output dataset even if hello spark program does not produce any output.</span></span> <span data-ttu-id="ed017-3057">Olá dataset unidades Olá agenda para o pipeline de saudação (por hora, diariamente, etc.).</span><span class="sxs-lookup"><span data-stu-id="ed017-3057">hello output dataset drives hello schedule for hello pipeline (hourly, daily, etc.).</span></span>

<span data-ttu-id="ed017-3058">Para obter mais informações sobre a atividade de hello, consulte [Spark atividade](data-factory-spark.md) artigo.</span><span class="sxs-lookup"><span data-stu-id="ed017-3058">For more information about hello activity, see [Spark Activity](data-factory-spark.md) article.</span></span>  

## <a name="machine-learning-batch-execution-activity"></a><span data-ttu-id="ed017-3059">Atividade de Execução em Lote de Machine Learning</span><span class="sxs-lookup"><span data-stu-id="ed017-3059">Machine Learning Batch Execution Activity</span></span>
<span data-ttu-id="ed017-3060">Você pode especificar Olá seguintes propriedades em uma definição de JSON da atividade de execução em lote do Azure ML.</span><span class="sxs-lookup"><span data-stu-id="ed017-3060">You can specify hello following properties in a Azure ML Batch Execution Activity JSON definition.</span></span> <span data-ttu-id="ed017-3061">a propriedade de tipo Hello atividade Olá deve ser: **AzureMLBatchExecution**.</span><span class="sxs-lookup"><span data-stu-id="ed017-3061">hello type property for hello activity must be: **AzureMLBatchExecution**.</span></span> <span data-ttu-id="ed017-3062">Você deve criar uma primeiro o serviço vinculado de aprendizado de máquina do Azure e especificar o nome de Olá-lo como um valor para Olá **linkedServiceName** propriedade.</span><span class="sxs-lookup"><span data-stu-id="ed017-3062">You must create a Azure Machine Learning linked service first and specify hello name of it as a value for hello **linkedServiceName** property.</span></span> <span data-ttu-id="ed017-3063">Olá propriedades a seguir têm suporte no hello **typeProperties** seção quando você define o tipo de saudação do tooAzureMLBatchExecution de atividade:</span><span class="sxs-lookup"><span data-stu-id="ed017-3063">hello following properties are supported in hello **typeProperties** section when you set hello type of activity tooAzureMLBatchExecution:</span></span>

<span data-ttu-id="ed017-3064">Propriedade</span><span class="sxs-lookup"><span data-stu-id="ed017-3064">Property</span></span> | <span data-ttu-id="ed017-3065">Descrição</span><span class="sxs-lookup"><span data-stu-id="ed017-3065">Description</span></span> | <span data-ttu-id="ed017-3066">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="ed017-3066">Required</span></span> 
-------- | ----------- | --------
<span data-ttu-id="ed017-3067">webServiceInput</span><span class="sxs-lookup"><span data-stu-id="ed017-3067">webServiceInput</span></span> | <span data-ttu-id="ed017-3068">Olá dataset toobe passado como entrada para Olá serviço de web do ML do Azure.</span><span class="sxs-lookup"><span data-stu-id="ed017-3068">hello dataset toobe passed as an input for hello Azure ML web service.</span></span> <span data-ttu-id="ed017-3069">Este conjunto de dados também deve ser incluído em entradas de saudação para atividade de saudação.</span><span class="sxs-lookup"><span data-stu-id="ed017-3069">This dataset must also be included in hello inputs for hello activity.</span></span> |<span data-ttu-id="ed017-3070">Use webServiceInput ou webServiceInputs.</span><span class="sxs-lookup"><span data-stu-id="ed017-3070">Use either webServiceInput or webServiceInputs.</span></span> | 
<span data-ttu-id="ed017-3071">webServiceInputs</span><span class="sxs-lookup"><span data-stu-id="ed017-3071">webServiceInputs</span></span> | <span data-ttu-id="ed017-3072">Especifique toobe de conjuntos de dados passadas como entradas para Olá serviço de web do ML do Azure.</span><span class="sxs-lookup"><span data-stu-id="ed017-3072">Specify datasets toobe passed as inputs for hello Azure ML web service.</span></span> <span data-ttu-id="ed017-3073">Se o serviço web de saudação pega várias entradas, use a propriedade de webServiceInputs de saudação em vez de usar a propriedade de webServiceInput hello.</span><span class="sxs-lookup"><span data-stu-id="ed017-3073">If hello web service takes multiple inputs, use hello webServiceInputs property instead of using hello webServiceInput property.</span></span> <span data-ttu-id="ed017-3074">Conjuntos de dados que são referenciados por Olá **webServiceInputs** também deve ser incluído no hello atividade **entradas**.</span><span class="sxs-lookup"><span data-stu-id="ed017-3074">Datasets that are referenced by hello **webServiceInputs** must also be included in hello Activity **inputs**.</span></span> | <span data-ttu-id="ed017-3075">Use webServiceInput ou webServiceInputs.</span><span class="sxs-lookup"><span data-stu-id="ed017-3075">Use either webServiceInput or webServiceInputs.</span></span> | 
<span data-ttu-id="ed017-3076">webServiceOutputs</span><span class="sxs-lookup"><span data-stu-id="ed017-3076">webServiceOutputs</span></span> | <span data-ttu-id="ed017-3077">Olá conjuntos de dados que são atribuídos como saídas para serviço de web hello ML do Azure.</span><span class="sxs-lookup"><span data-stu-id="ed017-3077">hello datasets that are assigned as outputs for hello Azure ML web service.</span></span> <span data-ttu-id="ed017-3078">Olá web service retorna dados de saída neste conjunto de dados.</span><span class="sxs-lookup"><span data-stu-id="ed017-3078">hello web service returns output data in this dataset.</span></span> | <span data-ttu-id="ed017-3079">Sim</span><span class="sxs-lookup"><span data-stu-id="ed017-3079">Yes</span></span> | 
<span data-ttu-id="ed017-3080">globalParameters</span><span class="sxs-lookup"><span data-stu-id="ed017-3080">globalParameters</span></span> | <span data-ttu-id="ed017-3081">Especifica valores para parâmetros de serviço da web hello nesta seção.</span><span class="sxs-lookup"><span data-stu-id="ed017-3081">Specify values for hello web service parameters in this section.</span></span> | <span data-ttu-id="ed017-3082">Não</span><span class="sxs-lookup"><span data-stu-id="ed017-3082">No</span></span> | 

### <a name="json-example"></a><span data-ttu-id="ed017-3083">Exemplo de JSON</span><span class="sxs-lookup"><span data-stu-id="ed017-3083">JSON example</span></span>
<span data-ttu-id="ed017-3084">Neste exemplo, a atividade de saudação tem Olá dataset **MLSqlInput** como entrada e **MLSqlOutput** como saída de hello.</span><span class="sxs-lookup"><span data-stu-id="ed017-3084">In this example, hello activity has hello dataset **MLSqlInput** as input and **MLSqlOutput** as hello output.</span></span> <span data-ttu-id="ed017-3085">Olá **MLSqlInput** é passado como um serviço web de entrada toohello por usando Olá **webServiceInput** propriedade JSON.</span><span class="sxs-lookup"><span data-stu-id="ed017-3085">hello **MLSqlInput** is passed as an input toohello web service by using hello **webServiceInput** JSON property.</span></span> <span data-ttu-id="ed017-3086">Olá **MLSqlOutput** é passado como um serviço de Web saída toohello por usando Olá **webserviceoutputs na** propriedade JSON.</span><span class="sxs-lookup"><span data-stu-id="ed017-3086">hello **MLSqlOutput** is passed as an output toohello Web service by using hello **webServiceOutputs** JSON property.</span></span> 

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

<span data-ttu-id="ed017-3087">No exemplo JSON hello, Olá implantado aprendizado de máquina do Azure Web serviço usa um leitor e um gravador módulo tooread/gravação de dados de / tooan banco de dados do SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="ed017-3087">In hello JSON example, hello deployed Azure Machine Learning Web service uses a reader and a writer module tooread/write data from/tooan Azure SQL Database.</span></span> <span data-ttu-id="ed017-3088">Esse serviço da Web expõe Olá quatro parâmetros a seguir: nome do servidor, nome do banco de dados, nome de conta de usuário do servidor e senha de conta de usuário do servidor de banco de dados.</span><span class="sxs-lookup"><span data-stu-id="ed017-3088">This Web service exposes hello following four parameters:  Database server name, Database name, Server user account name, and Server user account password.</span></span>

> [!NOTE]
> <span data-ttu-id="ed017-3089">Somente entradas e saídas da atividade de AzureMLBatchExecution Olá podem ser passadas como parâmetros toohello serviço da Web.</span><span class="sxs-lookup"><span data-stu-id="ed017-3089">Only inputs and outputs of hello AzureMLBatchExecution activity can be passed as parameters toohello Web service.</span></span> <span data-ttu-id="ed017-3090">Por exemplo, Olá acima trecho JSON, MLSqlInput é uma entrada toohello AzureMLBatchExecution atividade, que é passada como um serviço Web de entrada toohello por meio do parâmetro webServiceInput.</span><span class="sxs-lookup"><span data-stu-id="ed017-3090">For example, in hello above JSON snippet, MLSqlInput is an input toohello AzureMLBatchExecution activity, which is passed as an input toohello Web service via webServiceInput parameter.</span></span>

## <a name="machine-learning-update-resource-activity"></a><span data-ttu-id="ed017-3091">Atividade de Atualização de Recursos do Machine Learning</span><span class="sxs-lookup"><span data-stu-id="ed017-3091">Machine Learning Update Resource Activity</span></span>
<span data-ttu-id="ed017-3092">Você pode especificar Olá propriedades em uma definição de JSON da atividade do Azure ML atualização recursos a seguir.</span><span class="sxs-lookup"><span data-stu-id="ed017-3092">You can specify hello following properties in a Azure ML Update Resource Activity JSON definition.</span></span> <span data-ttu-id="ed017-3093">a propriedade de tipo Hello atividade Olá deve ser: **AzureMLUpdateResource**.</span><span class="sxs-lookup"><span data-stu-id="ed017-3093">hello type property for hello activity must be: **AzureMLUpdateResource**.</span></span> <span data-ttu-id="ed017-3094">Você deve criar uma primeiro o serviço vinculado de aprendizado de máquina do Azure e especificar o nome de Olá-lo como um valor para Olá **linkedServiceName** propriedade.</span><span class="sxs-lookup"><span data-stu-id="ed017-3094">You must create a Azure Machine Learning linked service first and specify hello name of it as a value for hello **linkedServiceName** property.</span></span> <span data-ttu-id="ed017-3095">Olá propriedades a seguir têm suporte no hello **typeProperties** seção quando você define o tipo de saudação do tooAzureMLUpdateResource de atividade:</span><span class="sxs-lookup"><span data-stu-id="ed017-3095">hello following properties are supported in hello **typeProperties** section when you set hello type of activity tooAzureMLUpdateResource:</span></span>

<span data-ttu-id="ed017-3096">Propriedade</span><span class="sxs-lookup"><span data-stu-id="ed017-3096">Property</span></span> | <span data-ttu-id="ed017-3097">Descrição</span><span class="sxs-lookup"><span data-stu-id="ed017-3097">Description</span></span> | <span data-ttu-id="ed017-3098">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="ed017-3098">Required</span></span> 
-------- | ----------- | --------
<span data-ttu-id="ed017-3099">trainedModelName</span><span class="sxs-lookup"><span data-stu-id="ed017-3099">trainedModelName</span></span> | <span data-ttu-id="ed017-3100">Nome da saudação treinados novamente o modelo.</span><span class="sxs-lookup"><span data-stu-id="ed017-3100">Name of hello retrained model.</span></span> | <span data-ttu-id="ed017-3101">Sim</span><span class="sxs-lookup"><span data-stu-id="ed017-3101">Yes</span></span> |  
<span data-ttu-id="ed017-3102">trainedModelDatasetName</span><span class="sxs-lookup"><span data-stu-id="ed017-3102">trainedModelDatasetName</span></span> | <span data-ttu-id="ed017-3103">Conjunto de dados apontando toohello arquivo iLearner retornado por Olá treinar novamente a operação.</span><span class="sxs-lookup"><span data-stu-id="ed017-3103">Dataset pointing toohello iLearner file returned by hello retraining operation.</span></span> | <span data-ttu-id="ed017-3104">Sim</span><span class="sxs-lookup"><span data-stu-id="ed017-3104">Yes</span></span> | 

### <a name="json-example"></a><span data-ttu-id="ed017-3105">Exemplo de JSON</span><span class="sxs-lookup"><span data-stu-id="ed017-3105">JSON example</span></span>
<span data-ttu-id="ed017-3106">pipeline de saudação tem duas atividades: **AzureMLBatchExecution** e **AzureMLUpdateResource**.</span><span class="sxs-lookup"><span data-stu-id="ed017-3106">hello pipeline has two activities: **AzureMLBatchExecution** and **AzureMLUpdateResource**.</span></span> <span data-ttu-id="ed017-3107">Hello atividade de execução de lote do ML do Azure usa dados de treinamento hello como entrada e produz um arquivo iLearner como saída.</span><span class="sxs-lookup"><span data-stu-id="ed017-3107">hello Azure ML Batch Execution activity takes hello training data as input and produces an iLearner file as an output.</span></span> <span data-ttu-id="ed017-3108">atividade de Olá chama o serviço web de treinamento hello (experiência de treinamento exposto como um serviço da web) com dados de treinamento de entrada hello e recebe o arquivo ilearner de saudação do hello webservice.</span><span class="sxs-lookup"><span data-stu-id="ed017-3108">hello activity invokes hello training web service (training experiment exposed as a web service) with hello input training data and receives hello ilearner file from hello webservice.</span></span> <span data-ttu-id="ed017-3109">Olá placeholderBlob é apenas um saída fictício conjunto de dados que é exigido pelo pipeline de saudação do hello Azure Data Factory serviço toorun.</span><span class="sxs-lookup"><span data-stu-id="ed017-3109">hello placeholderBlob is just a dummy output dataset that is required by hello Azure Data Factory service toorun hello pipeline.</span></span>


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

## <a name="data-lake-analytics-u-sql-activity"></a><span data-ttu-id="ed017-3110">Atividade do U-SQL da Análise Data Lake</span><span class="sxs-lookup"><span data-stu-id="ed017-3110">Data Lake Analytics U-SQL Activity</span></span>
<span data-ttu-id="ed017-3111">Você pode especificar Olá propriedades em uma definição de JSON da atividade U-SQL a seguir.</span><span class="sxs-lookup"><span data-stu-id="ed017-3111">You can specify hello following properties in a U-SQL Activity JSON definition.</span></span> <span data-ttu-id="ed017-3112">a propriedade de tipo Hello atividade Olá deve ser: **DataLakeAnalyticsU SQL**.</span><span class="sxs-lookup"><span data-stu-id="ed017-3112">hello type property for hello activity must be: **DataLakeAnalyticsU-SQL**.</span></span> <span data-ttu-id="ed017-3113">Você deve criar um serviço vinculado de análise do Azure Data Lake e especificar o nome de Olá-lo como um valor para Olá **linkedServiceName** propriedade.</span><span class="sxs-lookup"><span data-stu-id="ed017-3113">You must create an Azure Data Lake Analytics linked service and specify hello name of it as a value for hello **linkedServiceName** property.</span></span> <span data-ttu-id="ed017-3114">Olá propriedades a seguir têm suporte no hello **typeProperties** seção quando você definir o tipo de saudação da atividade tooDataLakeAnalyticsU-SQL:</span><span class="sxs-lookup"><span data-stu-id="ed017-3114">hello following properties are supported in hello **typeProperties** section when you set hello type of activity tooDataLakeAnalyticsU-SQL:</span></span> 

| <span data-ttu-id="ed017-3115">Propriedade</span><span class="sxs-lookup"><span data-stu-id="ed017-3115">Property</span></span> | <span data-ttu-id="ed017-3116">Descrição</span><span class="sxs-lookup"><span data-stu-id="ed017-3116">Description</span></span> | <span data-ttu-id="ed017-3117">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="ed017-3117">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="ed017-3118">scriptPath</span><span class="sxs-lookup"><span data-stu-id="ed017-3118">scriptPath</span></span> |<span data-ttu-id="ed017-3119">Toofolder de caminho que contém o script hello U-SQL.</span><span class="sxs-lookup"><span data-stu-id="ed017-3119">Path toofolder that contains hello U-SQL script.</span></span> <span data-ttu-id="ed017-3120">Nome do arquivo hello diferencia maiusculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="ed017-3120">Name of hello file is case-sensitive.</span></span> |<span data-ttu-id="ed017-3121">Não (se você usar o script)</span><span class="sxs-lookup"><span data-stu-id="ed017-3121">No (if you use script)</span></span> |
| <span data-ttu-id="ed017-3122">scriptLinkedService</span><span class="sxs-lookup"><span data-stu-id="ed017-3122">scriptLinkedService</span></span> |<span data-ttu-id="ed017-3123">Serviço vinculado que vincula o armazenamento de saudação que contém a fábrica de dados Olá script toohello</span><span class="sxs-lookup"><span data-stu-id="ed017-3123">Linked service that links hello storage that contains hello script toohello data factory</span></span> |<span data-ttu-id="ed017-3124">Não (se você usar o script)</span><span class="sxs-lookup"><span data-stu-id="ed017-3124">No (if you use script)</span></span> |
| <span data-ttu-id="ed017-3125">script</span><span class="sxs-lookup"><span data-stu-id="ed017-3125">script</span></span> |<span data-ttu-id="ed017-3126">Especificar script embutido em vez de especificar scriptPath e scriptLinkedService.</span><span class="sxs-lookup"><span data-stu-id="ed017-3126">Specify inline script instead of specifying scriptPath and scriptLinkedService.</span></span> <span data-ttu-id="ed017-3127">Por exemplo: "script": "CREATE DATABASE test".</span><span class="sxs-lookup"><span data-stu-id="ed017-3127">For example: "script": "CREATE DATABASE test".</span></span> |<span data-ttu-id="ed017-3128">Não (se você usar scriptPath e scriptLinkedService)</span><span class="sxs-lookup"><span data-stu-id="ed017-3128">No (if you use scriptPath and scriptLinkedService)</span></span> |
| <span data-ttu-id="ed017-3129">degreeOfParallelism</span><span class="sxs-lookup"><span data-stu-id="ed017-3129">degreeOfParallelism</span></span> |<span data-ttu-id="ed017-3130">número máximo de saudação de nós usados simultaneamente toorun trabalho de saudação.</span><span class="sxs-lookup"><span data-stu-id="ed017-3130">hello maximum number of nodes simultaneously used toorun hello job.</span></span> |<span data-ttu-id="ed017-3131">Não</span><span class="sxs-lookup"><span data-stu-id="ed017-3131">No</span></span> |
| <span data-ttu-id="ed017-3132">prioridade</span><span class="sxs-lookup"><span data-stu-id="ed017-3132">priority</span></span> |<span data-ttu-id="ed017-3133">Determina quais trabalhos entre todos os que estão na fila devem ser selecionada toorun primeiro.</span><span class="sxs-lookup"><span data-stu-id="ed017-3133">Determines which jobs out of all that are queued should be selected toorun first.</span></span> <span data-ttu-id="ed017-3134">Olá Olá número menor, Olá Olá prioridade.</span><span class="sxs-lookup"><span data-stu-id="ed017-3134">hello lower hello number, hello higher hello priority.</span></span> |<span data-ttu-id="ed017-3135">Não</span><span class="sxs-lookup"><span data-stu-id="ed017-3135">No</span></span> |
| <span data-ttu-id="ed017-3136">parâmetros</span><span class="sxs-lookup"><span data-stu-id="ed017-3136">parameters</span></span> |<span data-ttu-id="ed017-3137">Parâmetros de script hello U-SQL</span><span class="sxs-lookup"><span data-stu-id="ed017-3137">Parameters for hello U-SQL script</span></span> |<span data-ttu-id="ed017-3138">Não</span><span class="sxs-lookup"><span data-stu-id="ed017-3138">No</span></span> |

### <a name="json-example"></a><span data-ttu-id="ed017-3139">Exemplo de JSON</span><span class="sxs-lookup"><span data-stu-id="ed017-3139">JSON example</span></span>

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

<span data-ttu-id="ed017-3140">Para saber mais, consulte [Atividade de U-SQL no Data Lake Analytics](data-factory-usql-activity.md).</span><span class="sxs-lookup"><span data-stu-id="ed017-3140">For more information, see [Data Lake Analytics U-SQL Activity](data-factory-usql-activity.md).</span></span> 

## <a name="stored-procedure-activity"></a><span data-ttu-id="ed017-3141">Atividade de Procedimento Armazenado</span><span class="sxs-lookup"><span data-stu-id="ed017-3141">Stored Procedure Activity</span></span>
<span data-ttu-id="ed017-3142">Você pode especificar Olá seguintes propriedades em uma definição de JSON de atividade de procedimento armazenado.</span><span class="sxs-lookup"><span data-stu-id="ed017-3142">You can specify hello following properties in a Stored Procedure Activity JSON definition.</span></span> <span data-ttu-id="ed017-3143">a propriedade de tipo Hello atividade Olá deve ser: **SqlServerStoredProcedure**.</span><span class="sxs-lookup"><span data-stu-id="ed017-3143">hello type property for hello activity must be: **SqlServerStoredProcedure**.</span></span> <span data-ttu-id="ed017-3144">Você deve criar uma saudação serviços vinculados a seguir e especificar o nome de saudação do serviço Olá vinculado como um valor para hello **linkedServiceName** propriedade:</span><span class="sxs-lookup"><span data-stu-id="ed017-3144">You must create an one of hello following linked services and specify hello name of hello linked service as a value for hello **linkedServiceName** property:</span></span>

- <span data-ttu-id="ed017-3145">SQL Server</span><span class="sxs-lookup"><span data-stu-id="ed017-3145">SQL Server</span></span> 
- <span data-ttu-id="ed017-3146">Banco de Dados SQL do Azure</span><span class="sxs-lookup"><span data-stu-id="ed017-3146">Azure SQL Database</span></span>
- <span data-ttu-id="ed017-3147">SQL Data Warehouse do Azure</span><span class="sxs-lookup"><span data-stu-id="ed017-3147">Azure SQL Data Warehouse</span></span>

<span data-ttu-id="ed017-3148">Olá propriedades a seguir têm suporte no hello **typeProperties** seção quando você define o tipo de saudação do tooSqlServerStoredProcedure de atividade:</span><span class="sxs-lookup"><span data-stu-id="ed017-3148">hello following properties are supported in hello **typeProperties** section when you set hello type of activity tooSqlServerStoredProcedure:</span></span>

| <span data-ttu-id="ed017-3149">Propriedade</span><span class="sxs-lookup"><span data-stu-id="ed017-3149">Property</span></span> | <span data-ttu-id="ed017-3150">Descrição</span><span class="sxs-lookup"><span data-stu-id="ed017-3150">Description</span></span> | <span data-ttu-id="ed017-3151">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="ed017-3151">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ed017-3152">storedProcedureName</span><span class="sxs-lookup"><span data-stu-id="ed017-3152">storedProcedureName</span></span> |<span data-ttu-id="ed017-3153">Especifique o nome de saudação do procedimento de Olá armazenado no banco de dados do SQL Azure hello ou Azure SQL Data Warehouse que é representado pelo serviço Olá vinculado que Olá usos da tabela de saída.</span><span class="sxs-lookup"><span data-stu-id="ed017-3153">Specify hello name of hello stored procedure in hello Azure SQL database or Azure SQL Data Warehouse that is represented by hello linked service that hello output table uses.</span></span> |<span data-ttu-id="ed017-3154">Sim</span><span class="sxs-lookup"><span data-stu-id="ed017-3154">Yes</span></span> |
| <span data-ttu-id="ed017-3155">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="ed017-3155">storedProcedureParameters</span></span> |<span data-ttu-id="ed017-3156">Especifique valores para parâmetros de procedimento armazenado.</span><span class="sxs-lookup"><span data-stu-id="ed017-3156">Specify values for stored procedure parameters.</span></span> <span data-ttu-id="ed017-3157">Se você precisar toopass nulo para um parâmetro, use a sintaxe de saudação: "param1": null (todas as letras minúsculas).</span><span class="sxs-lookup"><span data-stu-id="ed017-3157">If you need toopass null for a parameter, use hello syntax: "param1": null (all lower case).</span></span> <span data-ttu-id="ed017-3158">Consulte Olá toolearn de exemplo sobre como usar essa propriedade a seguir.</span><span class="sxs-lookup"><span data-stu-id="ed017-3158">See hello following sample toolearn about using this property.</span></span> |<span data-ttu-id="ed017-3159">Não</span><span class="sxs-lookup"><span data-stu-id="ed017-3159">No</span></span> |

<span data-ttu-id="ed017-3160">Se você especificar um conjunto de dados de entrada, ele deve estar disponível (em status 'Pronto') para Olá armazenados toorun de atividade de procedimento.</span><span class="sxs-lookup"><span data-stu-id="ed017-3160">If you do specify an input dataset, it must be available (in ‘Ready’ status) for hello stored procedure activity toorun.</span></span> <span data-ttu-id="ed017-3161">Olá conjunto de dados de entrada não pode ser consumido no procedimento Olá armazenado como um parâmetro.</span><span class="sxs-lookup"><span data-stu-id="ed017-3161">hello input dataset cannot be consumed in hello stored procedure as a parameter.</span></span> <span data-ttu-id="ed017-3162">É apenas dependência de saudação toocheck usado antes de atividade de procedimento armazenado de saudação inicial.</span><span class="sxs-lookup"><span data-stu-id="ed017-3162">It is only used toocheck hello dependency before starting hello stored procedure activity.</span></span> <span data-ttu-id="ed017-3163">Você deve especificar um conjunto de dados de saída para uma atividade de procedimento armazenado.</span><span class="sxs-lookup"><span data-stu-id="ed017-3163">You must specify an output dataset for a stored procedure activity.</span></span> 

<span data-ttu-id="ed017-3164">Conjunto de dados de saída especifica Olá **agenda** para Olá armazenados atividade de procedimento (por hora, semanalmente, mensalmente, etc.).</span><span class="sxs-lookup"><span data-stu-id="ed017-3164">Output dataset specifies hello **schedule** for hello stored procedure activity (hourly, weekly, monthly, etc.).</span></span> <span data-ttu-id="ed017-3165">Olá conjunto de dados de saída deve usar um **serviço vinculado** que se refere a tooan banco de dados do SQL Azure ou um Azure SQL Data Warehouse ou um banco de dados do SQL Server no qual você deseja Olá toorun do procedimento armazenado.</span><span class="sxs-lookup"><span data-stu-id="ed017-3165">hello output dataset must use a **linked service** that refers tooan Azure SQL Database or an Azure SQL Data Warehouse or a SQL Server Database in which you want hello stored procedure toorun.</span></span> <span data-ttu-id="ed017-3166">Olá conjunto de dados de saída pode servir como um resultado do modo toopass Olá do procedimento armazenado de saudação para processamento subsequente por outra atividade ([encadeamento atividades](data-factory-scheduling-and-execution.md##multiple-activities-in-a-pipeline)) no pipeline de saudação.</span><span class="sxs-lookup"><span data-stu-id="ed017-3166">hello output dataset can serve as a way toopass hello result of hello stored procedure for subsequent processing by another activity ([chaining activities](data-factory-scheduling-and-execution.md##multiple-activities-in-a-pipeline)) in hello pipeline.</span></span> <span data-ttu-id="ed017-3167">No entanto, fábrica de dados não gravará automaticamente saída Olá de um conjunto de dados do procedimento armazenado toothis.</span><span class="sxs-lookup"><span data-stu-id="ed017-3167">However, Data Factory does not automatically write hello output of a stored procedure toothis dataset.</span></span> <span data-ttu-id="ed017-3168">É Olá tabela gravações tooa SQL que Olá pontos do conjunto de dados de saída de procedimento armazenado.</span><span class="sxs-lookup"><span data-stu-id="ed017-3168">It is hello stored procedure that writes tooa SQL table that hello output dataset points to.</span></span> <span data-ttu-id="ed017-3169">Em alguns casos, o conjunto de dados de saída de hello pode ser um **conjunto de dados fictício**, que é usado somente para atividade de procedimento armazenado de agendamento de saudação toospecify para executar a saudação.</span><span class="sxs-lookup"><span data-stu-id="ed017-3169">In some cases, hello output dataset can be a **dummy dataset**, which is used only toospecify hello schedule for running hello stored procedure activity.</span></span>  

### <a name="json-example"></a><span data-ttu-id="ed017-3170">Exemplo de JSON</span><span class="sxs-lookup"><span data-stu-id="ed017-3170">JSON example</span></span>

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

<span data-ttu-id="ed017-3171">Para saber mais, consulte o artigo [Atividade de Procedimento Armazenado](data-factory-stored-proc-activity.md).</span><span class="sxs-lookup"><span data-stu-id="ed017-3171">For more information, see [Stored Procedure Activity](data-factory-stored-proc-activity.md) article.</span></span> 

## <a name="net-custom-activity"></a><span data-ttu-id="ed017-3172">Atividade personalizada do .NET</span><span class="sxs-lookup"><span data-stu-id="ed017-3172">.NET custom activity</span></span>
<span data-ttu-id="ed017-3173">Você pode especificar Olá seguintes propriedades em uma atividade personalizada do .NET definição JSON.</span><span class="sxs-lookup"><span data-stu-id="ed017-3173">You can specify hello following properties in a .NET custom activity JSON definition.</span></span> <span data-ttu-id="ed017-3174">a propriedade de tipo Hello atividade Olá deve ser: **DotNetActivity**.</span><span class="sxs-lookup"><span data-stu-id="ed017-3174">hello type property for hello activity must be: **DotNetActivity**.</span></span> <span data-ttu-id="ed017-3175">Você deve criar um serviço vinculado do HDInsight do Azure ou um lote do Azure vinculado de serviço e especifique o nome de saudação do serviço vinculado de saudação como um valor para Olá **linkedServiceName** propriedade.</span><span class="sxs-lookup"><span data-stu-id="ed017-3175">You must create an Azure HDInsight linked service or an Azure Batch linked service, and specify hello name of hello linked service as a value for hello **linkedServiceName** property.</span></span> <span data-ttu-id="ed017-3176">Olá propriedades a seguir têm suporte no hello **typeProperties** seção quando você define o tipo de saudação do tooDotNetActivity de atividade:</span><span class="sxs-lookup"><span data-stu-id="ed017-3176">hello following properties are supported in hello **typeProperties** section when you set hello type of activity tooDotNetActivity:</span></span>
 
| <span data-ttu-id="ed017-3177">Propriedade</span><span class="sxs-lookup"><span data-stu-id="ed017-3177">Property</span></span> | <span data-ttu-id="ed017-3178">Descrição</span><span class="sxs-lookup"><span data-stu-id="ed017-3178">Description</span></span> | <span data-ttu-id="ed017-3179">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="ed017-3179">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="ed017-3180">AssemblyName</span><span class="sxs-lookup"><span data-stu-id="ed017-3180">AssemblyName</span></span> | <span data-ttu-id="ed017-3181">Nome do assembly hello.</span><span class="sxs-lookup"><span data-stu-id="ed017-3181">Name of hello assembly.</span></span> <span data-ttu-id="ed017-3182">Exemplo hello, ele é: **MyDotnetActivity.dll**.</span><span class="sxs-lookup"><span data-stu-id="ed017-3182">In hello example, it is: **MyDotnetActivity.dll**.</span></span> | <span data-ttu-id="ed017-3183">Sim</span><span class="sxs-lookup"><span data-stu-id="ed017-3183">Yes</span></span> |
| <span data-ttu-id="ed017-3184">EntryPoint</span><span class="sxs-lookup"><span data-stu-id="ed017-3184">EntryPoint</span></span> |<span data-ttu-id="ed017-3185">Nome da classe de saudação que implementa a interface de IDotNetActivity hello.</span><span class="sxs-lookup"><span data-stu-id="ed017-3185">Name of hello class that implements hello IDotNetActivity interface.</span></span> <span data-ttu-id="ed017-3186">Exemplo hello, ele é: **MyDotNetActivityNS.MyDotNetActivity** onde MyDotNetActivityNS é o namespace de saudação e MyDotNetActivity é a classe de saudação.</span><span class="sxs-lookup"><span data-stu-id="ed017-3186">In hello example, it is: **MyDotNetActivityNS.MyDotNetActivity** where MyDotNetActivityNS is hello namespace and MyDotNetActivity is hello class.</span></span>  | <span data-ttu-id="ed017-3187">Sim</span><span class="sxs-lookup"><span data-stu-id="ed017-3187">Yes</span></span> | 
| <span data-ttu-id="ed017-3188">PackageLinkedService</span><span class="sxs-lookup"><span data-stu-id="ed017-3188">PackageLinkedService</span></span> | <span data-ttu-id="ed017-3189">Nome da saudação serviço vinculado do armazenamento do Azure que aponta toohello armazenamento de blob que contém o arquivo de zip hello atividade personalizado.</span><span class="sxs-lookup"><span data-stu-id="ed017-3189">Name of hello Azure Storage linked service that points toohello blob storage that contains hello custom activity zip file.</span></span> <span data-ttu-id="ed017-3190">Exemplo hello, ele é: **AzureStorageLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="ed017-3190">In hello example, it is: **AzureStorageLinkedService**.</span></span>| <span data-ttu-id="ed017-3191">Sim</span><span class="sxs-lookup"><span data-stu-id="ed017-3191">Yes</span></span> |
| <span data-ttu-id="ed017-3192">PackageFile</span><span class="sxs-lookup"><span data-stu-id="ed017-3192">PackageFile</span></span> | <span data-ttu-id="ed017-3193">Nome do arquivo zip de saudação.</span><span class="sxs-lookup"><span data-stu-id="ed017-3193">Name of hello zip file.</span></span> <span data-ttu-id="ed017-3194">Exemplo hello, ele é: **customactivitycontainer/MyDotNetActivity.zip**.</span><span class="sxs-lookup"><span data-stu-id="ed017-3194">In hello example, it is: **customactivitycontainer/MyDotNetActivity.zip**.</span></span> | <span data-ttu-id="ed017-3195">Sim</span><span class="sxs-lookup"><span data-stu-id="ed017-3195">Yes</span></span> |
| <span data-ttu-id="ed017-3196">extendedProperties</span><span class="sxs-lookup"><span data-stu-id="ed017-3196">extendedProperties</span></span> | <span data-ttu-id="ed017-3197">Propriedades estendidas que você pode definir e passar em código .NET de toohello.</span><span class="sxs-lookup"><span data-stu-id="ed017-3197">Extended properties that you can define and pass on toohello .NET code.</span></span> <span data-ttu-id="ed017-3198">Neste exemplo, Olá **SliceStart** variável estiver definida como valor tooa com base na variável de sistema SliceStart hello.</span><span class="sxs-lookup"><span data-stu-id="ed017-3198">In this example, hello **SliceStart** variable is set tooa value based on hello SliceStart system variable.</span></span> | <span data-ttu-id="ed017-3199">Não</span><span class="sxs-lookup"><span data-stu-id="ed017-3199">No</span></span> | 

### <a name="json-example"></a><span data-ttu-id="ed017-3200">Exemplo de JSON</span><span class="sxs-lookup"><span data-stu-id="ed017-3200">JSON example</span></span>

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

<span data-ttu-id="ed017-3201">Para saber informações detalhadas, consulte o artigo [Usar atividades personalizadas no Data Factory](data-factory-use-custom-activities.md).</span><span class="sxs-lookup"><span data-stu-id="ed017-3201">For detailed information, see [Use custom activities in Data Factory](data-factory-use-custom-activities.md) article.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="ed017-3202">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="ed017-3202">Next Steps</span></span>
<span data-ttu-id="ed017-3203">Consulte Olá tutoriais a seguir:</span><span class="sxs-lookup"><span data-stu-id="ed017-3203">See hello following tutorials:</span></span> 

- [<span data-ttu-id="ed017-3204">Tutorial: Criar um pipeline com uma atividade de cópia</span><span class="sxs-lookup"><span data-stu-id="ed017-3204">Tutorial: create a pipeline with a copy activity</span></span>](data-factory-copy-activity-tutorial-using-azure-portal.md)
- [<span data-ttu-id="ed017-3205">Tutorial: Criar um pipeline com uma atividade de hive</span><span class="sxs-lookup"><span data-stu-id="ed017-3205">Tutorial: create a pipeline with a hive activity</span></span>](data-factory-build-your-first-pipeline-using-editor.md)