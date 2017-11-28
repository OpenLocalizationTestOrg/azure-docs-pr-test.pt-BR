---
title: "aaaRun do Azure Batch trabalhos de ponta a ponta sem escrever código (visualização) | Microsoft Docs"
description: "Crie arquivos de modelo para pools de lote de toocreate Olá CLI do Azure, trabalhos e tarefas."
services: batch
author: mscurrell
manager: timlt
ms.assetid: 
ms.service: batch
ms.devlang: na
ms.topic: article
ms.workload: big-compute
ms.date: 07/20/2017
ms.author: markscu
ms.openlocfilehash: c0434d09766451f6ba516efbad949834711ee819
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-batch-cli-templates-and-file-transfer-preview"></a><span data-ttu-id="400e2-103">Usar modelos CLI do Lote do Azure e o arquivo de transferência (Versão prévia)</span><span class="sxs-lookup"><span data-stu-id="400e2-103">Use Azure Batch CLI Templates and File Transfer (Preview)</span></span>

<span data-ttu-id="400e2-104">Usando Olá CLI do Azure é possível toorun trabalhos de lote sem escrever código.</span><span class="sxs-lookup"><span data-stu-id="400e2-104">Using hello Azure CLI it is possible toorun Batch jobs without writing code.</span></span>

<span data-ttu-id="400e2-105">Arquivos de modelo podem ser criados e usados com hello CLI do Azure que permitem que o lote pools, trabalhos e tarefas toobe criado.</span><span class="sxs-lookup"><span data-stu-id="400e2-105">Template files can be created and used with hello Azure CLI that allow Batch pools, jobs, and tasks toobe created.</span></span> <span data-ttu-id="400e2-106">Arquivos de entrada de trabalho podem ser carregados facilmente a conta de armazenamento Olá associada Olá lote conta e o trabalho de saída arquivos baixados.</span><span class="sxs-lookup"><span data-stu-id="400e2-106">Job input files can be easily uploaded to hello storage account associated with hello Batch account and job output files downloaded.</span></span>

## <a name="overview"></a><span data-ttu-id="400e2-107">Visão geral</span><span class="sxs-lookup"><span data-stu-id="400e2-107">Overview</span></span>

<span data-ttu-id="400e2-108">Toohello uma extensão CLI do Azure permite que o lote toobe usado-a ponta por usuários que não são desenvolvedores.</span><span class="sxs-lookup"><span data-stu-id="400e2-108">An extension toohello Azure CLI enables Batch toobe used end-to-end by users who are not developers.</span></span> <span data-ttu-id="400e2-109">Um pool pode ser criado, carregado de dados de entrada, trabalhos e tarefas associadas criadas, e Olá resultante saída dados baixados – nenhum código obrigatório, Olá CLI que está sendo usada diretamente ou que está sendo integrado em scripts.</span><span class="sxs-lookup"><span data-stu-id="400e2-109">A pool can be created, input data uploaded, jobs and associated tasks created, and hello resulting output data downloaded – no code required, hello CLI being used directly or being integrated into scripts.</span></span>

<span data-ttu-id="400e2-110">Criar modelos de lote no hello [suporte de lote existente no hello CLI do Azure](https://docs.microsoft.com/azure/batch/batch-cli-get-started#json-files-for-resource-creation) que permite que os arquivos JSON toospecify valores de propriedade para a criação de saudação de pools, trabalhos, tarefas e outros itens.</span><span class="sxs-lookup"><span data-stu-id="400e2-110">Batch templates build on hello [existing Batch support in hello Azure CLI](https://docs.microsoft.com/azure/batch/batch-cli-get-started#json-files-for-resource-creation) that allows JSON files toospecify property values for hello creation of pools, jobs, tasks, and other items.</span></span> <span data-ttu-id="400e2-111">Com modelos de lote, hello seguintes recursos são adicionados em que é possível com os arquivos JSON hello:</span><span class="sxs-lookup"><span data-stu-id="400e2-111">With Batch templates, hello following capabilities are added over what is possible with hello JSON files:</span></span>

-   <span data-ttu-id="400e2-112">Parâmetros podem ser definidos.</span><span class="sxs-lookup"><span data-stu-id="400e2-112">Parameters can be defined.</span></span> <span data-ttu-id="400e2-113">Quando Olá modelo é usado, somente os valores de parâmetro hello são item Olá toocreate especificado com outros valores de propriedade do item que está sendo especificada no corpo do modelo de saudação.</span><span class="sxs-lookup"><span data-stu-id="400e2-113">When hello template is used, only hello parameter values are specified toocreate hello item, with other item property values being specified in hello template body.</span></span> <span data-ttu-id="400e2-114">Um usuário que entende o que lote e toobe a aplicativos executados em lote pode criar modelos, a especificação de pool de trabalho e valores de propriedade da tarefa.</span><span class="sxs-lookup"><span data-stu-id="400e2-114">A user who understands Batch and the applications toobe run by Batch can create templates, specifying pool, job, and task property values.</span></span> <span data-ttu-id="400e2-115">Um usuário menos familiarizados com o lote e/ou os aplicativos só precisa os valores hello toospecify para parâmetros de saudação definido.</span><span class="sxs-lookup"><span data-stu-id="400e2-115">A user less familiar with Batch and/or the applications only needs toospecify hello values for hello defined parameters.</span></span>

-   <span data-ttu-id="400e2-116">Fábricas de tarefa de trabalho criar uma ou mais tarefas associadas a um trabalho, evitando Olá necessário para muitas tarefas definições toobe criado e simplificar significativamente o envio de trabalho.</span><span class="sxs-lookup"><span data-stu-id="400e2-116">Job task factories create one or more tasks associated with a job, avoiding hello need for many task definitions toobe created and significantly simplifying job submission.</span></span>


<span data-ttu-id="400e2-117">Arquivos de dados de entrada necessário toobe fornecido para trabalhos e geralmente são produzidos, arquivos de dados de saída.</span><span class="sxs-lookup"><span data-stu-id="400e2-117">Input data files need toobe supplied for jobs and output data files are often produced.</span></span> <span data-ttu-id="400e2-118">Uma conta de armazenamento está associada, por padrão, com cada lote de conta e arquivos podem ser facilmente transferido tooand desta conta de armazenamento usando a CLI, sem codificação e nenhuma credencial de armazenamento necessária.</span><span class="sxs-lookup"><span data-stu-id="400e2-118">A storage account is associated, by default, with each Batch account and files can be easily transferred tooand from this storage account using the CLI, with no coding and no storage credentials required.</span></span>

<span data-ttu-id="400e2-119">Por exemplo, [ffmpeg](http://ffmpeg.org/) é um aplicativo popular que processa arquivos de áudio e vídeo.</span><span class="sxs-lookup"><span data-stu-id="400e2-119">For example, [ffmpeg](http://ffmpeg.org/) is a popular application that processes audio and video files.</span></span> <span data-ttu-id="400e2-120">Olá CLI de lote do Azure pode ser usado tooinvoke ffmpeg tootranscode fonte arquivos de vídeo toodifferent resoluções.</span><span class="sxs-lookup"><span data-stu-id="400e2-120">hello Azure Batch CLI can be used tooinvoke ffmpeg tootranscode source video files toodifferent resolutions.</span></span>

-   <span data-ttu-id="400e2-121">Um modelo de pool é criado.</span><span class="sxs-lookup"><span data-stu-id="400e2-121">A pool template is created.</span></span> <span data-ttu-id="400e2-122">usuário de Olá criar modelo Olá sabe como toocall Olá ffmpeg aplicativo e seus requisitos. Olá, elas especificam OS apropriado, VM de tamanho, como ffmpeg está instalado (de um pacote de aplicativo ou usando um Gerenciador de pacotes, por exemplo) e outros valores de propriedade do pool.</span><span class="sxs-lookup"><span data-stu-id="400e2-122">hello user creating hello template knows how toocall hello ffmpeg application and its requirements; they specify hello appropriate OS, VM size, how ffmpeg is installed (from an application package or using a package manager, for example), and other pool property values.</span></span> <span data-ttu-id="400e2-123">Parâmetros são criados quando o modelo de saudação é usado, somente id do pool hello e número de VMs necessário toobe especificado.</span><span class="sxs-lookup"><span data-stu-id="400e2-123">Parameters are created so when hello template is used, only hello pool id and number of VMs need toobe specified.</span></span>

-   <span data-ttu-id="400e2-124">Um modelo de trabalho é criado.</span><span class="sxs-lookup"><span data-stu-id="400e2-124">A job template is created.</span></span> <span data-ttu-id="400e2-125">modelo de criação Olá Olá usuário sabe como ffmpeg necessidades toobe chamado resolução de vídeo tooa diferente da origem de tootranscode e especifica a linha de comando da tarefa de saudação; Eles também sabem que é uma pasta que contém arquivos de vídeo de origem hello, com uma tarefa obrigatória por arquivo de entrada.</span><span class="sxs-lookup"><span data-stu-id="400e2-125">hello user creating hello template knows how ffmpeg needs toobe invoked tootranscode source video tooa different resolution and specifies hello task command line; they also know that there is a folder containing hello source video files, with a task required per input file.</span></span>

-   <span data-ttu-id="400e2-126">Um usuário final com um conjunto de arquivos de vídeo tootranscode primeiro cria um pool usando o modelo de pool hello, especificando somente id do pool hello e número de VMs necessárias.</span><span class="sxs-lookup"><span data-stu-id="400e2-126">An end user with a set of video files tootranscode first creates a pool using hello pool template, specifying only hello pool id and number of VMs required.</span></span> <span data-ttu-id="400e2-127">Eles podem, em seguida, carregue Olá tootranscode de arquivos de origem.</span><span class="sxs-lookup"><span data-stu-id="400e2-127">They can then upload hello source files tootranscode.</span></span> <span data-ttu-id="400e2-128">Um trabalho pode ser enviado usando o modelo de trabalho hello, especificando somente a id do pool de hello e local dos arquivos de origem Olá carregado.</span><span class="sxs-lookup"><span data-stu-id="400e2-128">A job can then be submitted using hello job template, specifying only hello pool id and location of hello source files uploaded.</span></span> <span data-ttu-id="400e2-129">trabalho em lotes de saudação é criado com uma tarefa por arquivo de entrada que está sendo gerado.</span><span class="sxs-lookup"><span data-stu-id="400e2-129">hello Batch job is created, with one task per input file being generated.</span></span> <span data-ttu-id="400e2-130">Por fim, Olá transcodificado nos arquivos de saída podem ser o download.</span><span class="sxs-lookup"><span data-stu-id="400e2-130">Finally, hello transcoded output files can be download.</span></span>

## <a name="installation"></a><span data-ttu-id="400e2-131">Instalação</span><span class="sxs-lookup"><span data-stu-id="400e2-131">Installation</span></span>

<span data-ttu-id="400e2-132">capacidade de transferência de arquivo e o modelo de saudação exige um toobe extensão instalada.</span><span class="sxs-lookup"><span data-stu-id="400e2-132">hello template and file transfer capabilities require an extension toobe installed.</span></span>

<span data-ttu-id="400e2-133">Para obter instruções sobre como ver tooinstall Olá CLI do Azure [instalar o Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="400e2-133">For instructions on how tooinstall hello Azure CLI see [Install Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli).</span></span>

<span data-ttu-id="400e2-134">Uma vez Olá que CLI do Azure foi instalado, Olá extensão pode ser instalada usando o seguinte comando CLI do lote:</span><span class="sxs-lookup"><span data-stu-id="400e2-134">Once hello Azure CLI has been installed, hello Batch extension can be installed using the following CLI command:</span></span>

```azurecli
az component update --add batch-extensions --allow-third-party
```

<span data-ttu-id="400e2-135">Para obter mais informações sobre Olá extensão em lotes, consulte [do Microsoft Azure lote CLI extensões do Windows, Mac e Linux](https://github.com/Azure/azure-batch-cli-extensions#microsoft-azure-batch-cli-extensions-for-windows-mac-and-linux).</span><span class="sxs-lookup"><span data-stu-id="400e2-135">For more information about hello Batch extension, see [Microsoft Azure Batch CLI Extensions for Windows, Mac and Linux](https://github.com/Azure/azure-batch-cli-extensions#microsoft-azure-batch-cli-extensions-for-windows-mac-and-linux).</span></span>

## <a name="templates"></a><span data-ttu-id="400e2-136">Modelos</span><span class="sxs-lookup"><span data-stu-id="400e2-136">Templates</span></span>

<span data-ttu-id="400e2-137">Olá CLI de lote do Azure permite que os itens como grupos, trabalhos e tarefas toobe criados, especificando um arquivo JSON que contém os valores e nomes de propriedade.</span><span class="sxs-lookup"><span data-stu-id="400e2-137">hello Azure Batch CLI allows items such as pools, jobs, and tasks toobe created by specifying a JSON file containing property names and values.</span></span> <span data-ttu-id="400e2-138">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="400e2-138">For example:</span></span>

```azurecli
az batch pool create –-json-file AppPool.json
```

<span data-ttu-id="400e2-139">Modelos de lote do Azure são semelhantes tooAzure Gerenciador de recursos modelos, na funcionalidade e a sintaxe.</span><span class="sxs-lookup"><span data-stu-id="400e2-139">Azure Batch templates are similar tooAzure Resource Manager templates, in functionality and syntax.</span></span> <span data-ttu-id="400e2-140">Elas são arquivos JSON que contêm valores e nomes de propriedade do item, mas adicionar Olá principais conceitos a seguir:</span><span class="sxs-lookup"><span data-stu-id="400e2-140">They are JSON files that contain item property names and values, but add hello following main concepts:</span></span>

-   <span data-ttu-id="400e2-141">**Parâmetros**</span><span class="sxs-lookup"><span data-stu-id="400e2-141">**Parameters**</span></span>

    -   <span data-ttu-id="400e2-142">Permitir toobe de valores de propriedade especificado em uma seção de corpo, com apenas os valores de parâmetro necessidade toobe fornecido ao modelo de saudação é usado.</span><span class="sxs-lookup"><span data-stu-id="400e2-142">Allow property values toobe specified in a body section, with only parameter values needing toobe supplied when hello template is used.</span></span> <span data-ttu-id="400e2-143">Por exemplo, a definição completa Olá para um pool pôde ser colocada no corpo de saudação e apenas um parâmetro definido para a id do pool; apenas uma cadeia de id do pool, portanto, precisa toocreate toobe fornecido um pool.</span><span class="sxs-lookup"><span data-stu-id="400e2-143">For example, hello complete definition for a pool could be placed in hello body and only one parameter defined for pool id; only a pool id string therefore needs toobe supplied toocreate a pool.</span></span>
        
    -   <span data-ttu-id="400e2-144">corpo do modelo de saudação pode ser criado por uma pessoa com conhecimento do lote e Olá aplicativos toobe execute o lote; somente os valores para parâmetros definidos pelo autor do hello devem ser fornecidos quando Olá modelo é usado.</span><span class="sxs-lookup"><span data-stu-id="400e2-144">hello template body can be authored by someone with knowledge of Batch and hello applications toobe run by Batch; only values for hello author-defined parameters must be supplied when hello template is used.</span></span> <span data-ttu-id="400e2-145">Um usuário sem Olá lote detalhada e/ou dados de conhecimento do aplicativo, portanto, podem usar os modelos.</span><span class="sxs-lookup"><span data-stu-id="400e2-145">A user without hello in-depth Batch and/or application knowledge can therefore use the templates.</span></span>

-   <span data-ttu-id="400e2-146">**Variáveis**</span><span class="sxs-lookup"><span data-stu-id="400e2-146">**Variables**</span></span>

    -   <span data-ttu-id="400e2-147">Permitir toobe de valores simples ou complexos de parâmetro especificado em um local e usado em um ou mais locais do corpo do modelo de saudação.</span><span class="sxs-lookup"><span data-stu-id="400e2-147">Allow simple or complex parameter values toobe specified in one place and used in one or more places in hello template body.</span></span> <span data-ttu-id="400e2-148">Variáveis podem simplificar e reduzir o tamanho de saudação do modelo hello, bem como tornar mais fácil manutenção tendo um propriedades de toochange local cujo valor pode ser alterado.</span><span class="sxs-lookup"><span data-stu-id="400e2-148">Variables can simplify and reduce hello size of hello template, as well as make it more maintainable by having one location toochange properties whose value may change.</span></span>

-   <span data-ttu-id="400e2-149">**Construções de nível superior**</span><span class="sxs-lookup"><span data-stu-id="400e2-149">**Higher-level constructs**</span></span>

    -   <span data-ttu-id="400e2-150">Algumas construções de nível superior estão disponíveis no modelo de saudação que ainda não estão disponíveis no hello APIs de lote.</span><span class="sxs-lookup"><span data-stu-id="400e2-150">Some higher-level constructs are available in hello template that are not yet available in hello Batch APIs.</span></span> <span data-ttu-id="400e2-151">Por exemplo, uma fábrica de tarefas pode ser definida em um modelo de trabalho que cria várias tarefas de trabalho hello usando uma definição de tarefa comum.</span><span class="sxs-lookup"><span data-stu-id="400e2-151">For example, a task factory can be defined in a job template that creates multiple tasks for hello job using a common task definition.</span></span> <span data-ttu-id="400e2-152">Essas construções evitar Olá necessidade toocode para dinamicamente crie vários arquivos JSON, como um arquivo por tarefa, bem como criar script arquivos tooinstall aplicativos por meio de um Gerenciador de pacotes, por exemplo.</span><span class="sxs-lookup"><span data-stu-id="400e2-152">These constructs avoid hello need toocode to dynamically create multiple JSON files, such as one file per task, as well as create script files tooinstall applications via a package manager, for example.</span></span>

    -   <span data-ttu-id="400e2-153">Em algum ponto, onde aplicável, que essas construções podem ser adicionados toothe lote serviço e está disponível em Olá APIs de lote, interfaces do usuário, etc.</span><span class="sxs-lookup"><span data-stu-id="400e2-153">At some point, where applicable, these constructs may be added toothe Batch service and available in hello Batch APIs, UIs, etc.</span></span>

### <a name="pool-templates"></a><span data-ttu-id="400e2-154">Modelos de pool</span><span class="sxs-lookup"><span data-stu-id="400e2-154">Pool templates</span></span>

<span data-ttu-id="400e2-155">Além disso, toohello recursos de modelo padrão de parâmetros e variáveis, Olá construções de nível superior a seguir são suportados pelo modelo de pool de saudação:</span><span class="sxs-lookup"><span data-stu-id="400e2-155">In addition toohello standard template capabilities of parameters and variables, hello following higher-level constructs are supported by hello pool template:</span></span>

-   <span data-ttu-id="400e2-156">**Referências do pacote**</span><span class="sxs-lookup"><span data-stu-id="400e2-156">**Package references**</span></span>

    -   <span data-ttu-id="400e2-157">Opcionalmente, permite que software toobe copiado toopool nós usando o pacote gerentes.</span><span class="sxs-lookup"><span data-stu-id="400e2-157">Optionally allows software toobe copied toopool nodes by using package managers.</span></span> <span data-ttu-id="400e2-158">Gerenciador de pacotes de saudação e a id do pacote são especificados.</span><span class="sxs-lookup"><span data-stu-id="400e2-158">hello package manager and package id are specified.</span></span> <span data-ttu-id="400e2-159">Sendo toodeclare capaz de um ou mais pacotes evita Olá necessidade toocreate um script que obtém os pacotes de saudação necessários, Olá script de instalação e execute o script hello em cada nó de pool.</span><span class="sxs-lookup"><span data-stu-id="400e2-159">Being able toodeclare one or more packages avoids hello need toocreate a script that gets hello required packages, install hello script, and run hello script on each pool node.</span></span>

<span data-ttu-id="400e2-160">a seguir Olá é um exemplo de um modelo que cria um pool de VMs do Linux com ffmpeg instalado e apenas requer um número de cadeia de caracteres e hello da id de pool de máquinas virtuais toobe fornecido toouse:</span><span class="sxs-lookup"><span data-stu-id="400e2-160">hello following is an example of a template that creates a pool of Linux VMs with ffmpeg installed and only requires a pool id string and hello number of VMs toobe supplied toouse:</span></span>

```json
{
    "parameters": {
        "nodeCount": {
            "type": "int",
            "metadata": {
                "description": "hello number of pool nodes"
            }
        },
        "poolId": {
            "type": "string",
            "metadata": {
                "description": "hello pool id "
            }
        }
    },
    "pool": {
        "type": "Microsoft.Batch/batchAccounts/pools",
        "apiVersion": "2016-12-01",
        "properties": {
            "id": "[parameters('poolId')]",
            "virtualMachineConfiguration": {
                "imageReference": {
                    "publisher": "Canonical",
                    "offer": "UbuntuServer",
                    "sku": "16.04.0-LTS",
                    "version": "latest"
                },
                "nodeAgentSKUId": "batch.node.ubuntu 16.04"
            },
            "vmSize": "STANDARD_D3_V2",
            "targetDedicatedNodes": "[parameters('nodeCount')]",
            "enableAutoScale": false,
            "maxTasksPerNode": 1,
            "packageReferences": [
                {
                    "type": "aptPackage",
                    "id": "ffmpeg"
                }
            ]
        }
    }
}
```

<span data-ttu-id="400e2-161">Se o arquivo de modelo de saudação foi nomeado _ffmpeg.json do pool de_, em seguida, o modelo Olá seria invocado da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="400e2-161">If hello template file was named _pool-ffmpeg.json_, then hello template would be invoked as follows:</span></span>

```azurecli
az batch pool create --template pool-ffmpeg.json
```

### <a name="job-templates"></a><span data-ttu-id="400e2-162">Modelos de trabalho</span><span class="sxs-lookup"><span data-stu-id="400e2-162">Job templates</span></span>

<span data-ttu-id="400e2-163">Além disso, toohello recursos de modelo padrão de parâmetros e variáveis, Olá construções de nível superior a seguir são suportados pelo modelo de trabalho hello:</span><span class="sxs-lookup"><span data-stu-id="400e2-163">In addition toohello standard template capabilities of parameters and variables, hello following higher-level constructs are supported by hello job template:</span></span>

-   <span data-ttu-id="400e2-164">**Fábrica de tarefas**</span><span class="sxs-lookup"><span data-stu-id="400e2-164">**Task factory**</span></span>

    -   <span data-ttu-id="400e2-165">Com base em uma definição de tarefa, cria várias tarefas para um trabalho.</span><span class="sxs-lookup"><span data-stu-id="400e2-165">Creates multiple tasks for a job from one task definition.</span></span> <span data-ttu-id="400e2-166">Três tipos de fábrica de tarefas têm suporte – limpeza paramétrica, tarefa por arquivo e coleção de tarefas.</span><span class="sxs-lookup"><span data-stu-id="400e2-166">Three types of task factory are supported – parametric sweep, task per file, and task collection.</span></span>

<span data-ttu-id="400e2-167">Olá seguinte é um exemplo de um modelo que cria um trabalho que usa ffmpeg para transcodificar tooone de arquivos de vídeo MP4 de duas resoluções mais baixas, com uma tarefa criada por um arquivo de vídeo de origem:</span><span class="sxs-lookup"><span data-stu-id="400e2-167">hello following is an example of a template that creates a job that uses ffmpeg to transcode MP4 video files tooone of two lower resolutions, with one task created per source video file:</span></span>

```json
{
    "parameters": {
        "poolId": {
            "type": "string",
            "metadata": {
                "description": "hello name of Azure Batch pool which runs hello job"
            }
        },
        "jobId": {
            "type": "string",
            "metadata": {
                "description": "hello name of Azure Batch job"
            }
        },
        "resolution": {
            "type": "string",
            "defaultValue": "428x240",
            "allowedValues": [
                "428x240",
                "854x480"
            ],
            "metadata": {
                "description": "Target video resolution"
            }
        }
    },
    "job": {
        "type": "Microsoft.Batch/batchAccounts/jobs",
        "apiVersion": "2016-12-01",
        "properties": {
            "id": "[parameters('jobId')]",
            "constraints": {
                "maxWallClockTime": "PT5H",
                "maxTaskRetryCount": 1
            },
            "poolInfo": {
                "poolId": "[parameters('poolId')]"
            },
            "taskFactory": {
                "type": "taskPerFile",
                "source": { 
                    "fileGroup": "ffmpeg-input"
                },
                "repeatTask": {
                    "commandLine": "ffmpeg -i {fileName} -y -s [parameters('resolution')] -strict -2 {fileNameWithoutExtension}_[parameters('resolution')].mp4",
                    "resourceFiles": [
                        {
                            "blobSource": "{url}",
                            "filePath": "{fileName}"
                        }
                    ],
                    "outputFiles": [
                        {
                            "filePattern": "{fileNameWithoutExtension}_[parameters('resolution')].mp4",
                            "destination": {
                                "autoStorage": {
                                    "path": "{fileNameWithoutExtension}_[parameters('resolution')].mp4",
                                    "fileGroup": "ffmpeg-output"
                                }
                            },
                            "uploadOptions": {
                                "uploadCondition": "TaskSuccess"
                            }
                        }
                    ]
                }
            },
            "onAllTasksComplete": "terminatejob"
        }
    }
}
```

<span data-ttu-id="400e2-168">Se o arquivo de modelo de saudação foi nomeado _ffmpeg.json trabalho_, em seguida, o modelo Olá seria invocado da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="400e2-168">If hello template file was named _job-ffmpeg.json_, then hello template would be invoked as follows:</span></span>

```azurecli
az batch job create --template job-ffmpeg.json
```

## <a name="file-groups-and-file-transfer"></a><span data-ttu-id="400e2-169">Transferência de arquivos e grupos de arquivo</span><span class="sxs-lookup"><span data-stu-id="400e2-169">File groups and file transfer</span></span>

<span data-ttu-id="400e2-170">A maioria dos trabalhos e tarefas exigem arquivos de entrada e produzem arquivos de saída.</span><span class="sxs-lookup"><span data-stu-id="400e2-170">Most jobs and tasks require input files and produce output files.</span></span> <span data-ttu-id="400e2-171">Os dois arquivos de entrada e arquivos de saída necessário normalmente toobe transferido, do nó de toohello Olá cliente ou do cliente do hello nó toohello.</span><span class="sxs-lookup"><span data-stu-id="400e2-171">Both input files and output files typically need toobe transferred, either from hello client toohello node, or from hello node toohello client.</span></span> <span data-ttu-id="400e2-172">Olá extensão CLI de lote do Azure abstrai a transferência de arquivo ausente e utiliza a conta de armazenamento de saudação que é criada por padrão para cada conta do lote.</span><span class="sxs-lookup"><span data-stu-id="400e2-172">hello Azure Batch CLI extension abstracts away file transfer and utilizes hello storage account that is created by default for each Batch account.</span></span>

<span data-ttu-id="400e2-173">Um grupo de arquivos é igual a tooa contêiner que é criado no hello conta de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="400e2-173">A file group equates tooa container that is created in hello Azure storage account.</span></span> <span data-ttu-id="400e2-174">grupo de arquivos Olá pode ter subpastas.</span><span class="sxs-lookup"><span data-stu-id="400e2-174">hello file group may have subfolders.</span></span>

<span data-ttu-id="400e2-175">Olá extensão CLI de lote fornece comandos para carregar arquivos do grupo de arquivos especificado tooa cliente e baixar arquivos de cliente de tooa de grupo Olá arquivo especificado.</span><span class="sxs-lookup"><span data-stu-id="400e2-175">hello Batch CLI extension provides commands for uploading files from client tooa specified file group and downloading files from hello specified file group tooa client.</span></span>

```azurecli
az batch file upload --local-path c:\source_videos\*.mp4 
    --file-group ffmpeg-input

az batch file download --file-group ffmpeg-output --local-path
    c:\output_lowres_videos
```

<span data-ttu-id="400e2-176">Modelos de pool e trabalho permitem que os arquivos armazenados em toobe de grupos de arquivo especificado para a cópia em nós de pool ou desativar o pool de nós novamente tooa o grupo de arquivos.</span><span class="sxs-lookup"><span data-stu-id="400e2-176">Pool and job templates allow files stored in file groups toobe specified for copy onto pool nodes or off pool nodes back tooa file group.</span></span> <span data-ttu-id="400e2-177">Por exemplo, no modelo de trabalho especificado anteriormente, Olá grupo "ffmpeg-entrada de arquivo" for especificado para a fábrica de tarefas Olá como local de Olá Olá vídeo de arquivos de origem copiado para baixo para o nó Olá para transcodificação; Olá grupo "ffmpeg-saída de arquivo" é usado como o local onde os arquivos de saída transcodificado Olá são hello copiados nó de saudação toofrom executar cada tarefa.</span><span class="sxs-lookup"><span data-stu-id="400e2-177">For example, in the job template specified previously, hello file group “ffmpeg-input” is specified for hello task factory as hello location of hello source video files copied down onto hello node for transcoding; hello file group “ffmpeg-output” is used as hello location where hello transcoded output files are copied toofrom hello node running each task.</span></span>

## <a name="summary"></a><span data-ttu-id="400e2-178">Resumo</span><span class="sxs-lookup"><span data-stu-id="400e2-178">Summary</span></span>

<span data-ttu-id="400e2-179">Suporte de transferência de arquivo e o modelo atualmente foram adicionados apenas toohello CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="400e2-179">Template and file transfer support have currently been added only toohello Azure CLI.</span></span> <span data-ttu-id="400e2-180">meta de saudação é tooexpand Olá público-alvo que pode usar toousers de lote que não é necessário o código de toodevelop usando Olá APIs de lote, como os pesquisadores, usuários e assim por diante.</span><span class="sxs-lookup"><span data-stu-id="400e2-180">hello goal is tooexpand hello audience that can use Batch toousers who do not need toodevelop code using hello Batch APIs, such as researchers, IT users, and so on.</span></span> <span data-ttu-id="400e2-181">Sem codificação, usuários com conhecimento do Azure, lote e Olá aplicativos toobe executado por lote podem criar modelos para criação de pool e de trabalho.</span><span class="sxs-lookup"><span data-stu-id="400e2-181">Without coding, users with knowledge of Azure, Batch, and hello applications toobe run by Batch can create templates for pool and job creation.</span></span> <span data-ttu-id="400e2-182">Com os parâmetros de modelo, os usuários sem conhecimento detalhado dos aplicativos de lote e hello podem usar modelos de saudação.</span><span class="sxs-lookup"><span data-stu-id="400e2-182">With template parameters, users without detailed knowledge of Batch and hello applications can use hello templates.</span></span>

<span data-ttu-id="400e2-183">Experimente Olá extensão de lote para Olá CLI do Azure e fornecer comentários ou sugestões, a saudação em comentários para este artigo ou por meio de saudação [Fórum do Azure Batch](https://social.msdn.microsoft.com/forums/azure/home?forum=azurebatch).</span><span class="sxs-lookup"><span data-stu-id="400e2-183">Try out hello Batch extension for hello Azure CLI and provide us with any feedback or suggestions, either in hello comments for this article or via hello [Azure Batch forum](https://social.msdn.microsoft.com/forums/azure/home?forum=azurebatch).</span></span>

## <a name="next-steps"></a><span data-ttu-id="400e2-184">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="400e2-184">Next steps</span></span>

- <span data-ttu-id="400e2-185">Consulte a postagem de blog de modelos de lote Olá: [trabalhos em execução em lote do Azure usando Olá CLI do Azure – nenhum código necessário](https://azure.microsoft.com/en-us/blog/running-azure-batch-jobs-using-the-azure-cli-no-code-required/).</span><span class="sxs-lookup"><span data-stu-id="400e2-185">See hello Batch templates blog post: [Running Azure Batch jobs using hello Azure CLI – no code required](https://azure.microsoft.com/en-us/blog/running-azure-batch-jobs-using-the-azure-cli-no-code-required/).</span></span>
- <span data-ttu-id="400e2-186">Documentação detalhada de instalação e uso, exemplos e código-fonte estão disponíveis no hello [repositório GitHub Azure](https://github.com/Azure/azure-batch-cli-extensions).</span><span class="sxs-lookup"><span data-stu-id="400e2-186">Detailed installation and usage documentation, samples, and source code are available in hello [Azure GitHub repository](https://github.com/Azure/azure-batch-cli-extensions).</span></span>
