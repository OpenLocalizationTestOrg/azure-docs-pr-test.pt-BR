---
title: "Executar trabalhos do Lote do Azure de ponta a ponta sem escrever código (Versão Prévia) | Microsoft Docs"
description: Crie arquivos de modelo para a CLI do Azure criar pools de Lote, trabalhos e tarefas.
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
ms.openlocfilehash: 6b91466da46d1f4ca9f25bf1718be783603efc58
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/29/2017
---
# <a name="use-azure-batch-cli-templates-and-file-transfer-preview"></a><span data-ttu-id="537bb-103">Usar modelos CLI do Lote do Azure e o arquivo de transferência (Versão prévia)</span><span class="sxs-lookup"><span data-stu-id="537bb-103">Use Azure Batch CLI Templates and File Transfer (Preview)</span></span>

<span data-ttu-id="537bb-104">Ao usar a CLI do Azure é possível executar trabalhos do Lote sem escrever código.</span><span class="sxs-lookup"><span data-stu-id="537bb-104">Using the Azure CLI it is possible to run Batch jobs without writing code.</span></span>

<span data-ttu-id="537bb-105">É possível criar arquivos de modelo que podem ser usados com a CLI do Azure e permitem a criação de trabalhos, tarefas pools de Lote.</span><span class="sxs-lookup"><span data-stu-id="537bb-105">Template files can be created and used with the Azure CLI that allow Batch pools, jobs, and tasks to be created.</span></span> <span data-ttu-id="537bb-106">Arquivos de entrada de trabalho podem ser facilmente carregados para a conta de armazenamento associada com a conta do Lote e os arquivos de saída de trabalho baixados.</span><span class="sxs-lookup"><span data-stu-id="537bb-106">Job input files can be easily uploaded to the storage account associated with the Batch account and job output files downloaded.</span></span>

## <a name="overview"></a><span data-ttu-id="537bb-107">Visão geral</span><span class="sxs-lookup"><span data-stu-id="537bb-107">Overview</span></span>

<span data-ttu-id="537bb-108">Uma extensão da CLI do Azure permite que o Lote seja usado de ponta a ponta por usuários que não são desenvolvedores.</span><span class="sxs-lookup"><span data-stu-id="537bb-108">An extension to the Azure CLI enables Batch to be used end-to-end by users who are not developers.</span></span> <span data-ttu-id="537bb-109">É possível criar um pool, carregar os dados de entrada, criar trabalhos e tarefas associadas e baixar os dados de saída resultantes – sem necessidade de nenhum código, com a CLI sendo usada diretamente ou integrada em scripts.</span><span class="sxs-lookup"><span data-stu-id="537bb-109">A pool can be created, input data uploaded, jobs and associated tasks created, and the resulting output data downloaded – no code required, the CLI being used directly or being integrated into scripts.</span></span>

<span data-ttu-id="537bb-110">Os modelos do Lote usam o [suporte do Lote existente na CLI do Azure](https://docs.microsoft.com/azure/batch/batch-cli-get-started#json-files-for-resource-creation), que permite que os arquivos JSON especifiquem valores de propriedade para a criação de pools, trabalhos, tarefas e outros itens.</span><span class="sxs-lookup"><span data-stu-id="537bb-110">Batch templates build on the [existing Batch support in the Azure CLI](https://docs.microsoft.com/azure/batch/batch-cli-get-started#json-files-for-resource-creation) that allows JSON files to specify property values for the creation of pools, jobs, tasks, and other items.</span></span> <span data-ttu-id="537bb-111">Com modelos de Lote, os seguintes recursos são adicionados além do que é possível com os arquivos JSON:</span><span class="sxs-lookup"><span data-stu-id="537bb-111">With Batch templates, the following capabilities are added over what is possible with the JSON files:</span></span>

-   <span data-ttu-id="537bb-112">Parâmetros podem ser definidos.</span><span class="sxs-lookup"><span data-stu-id="537bb-112">Parameters can be defined.</span></span> <span data-ttu-id="537bb-113">Quando o modelo é usado, somente os valores de parâmetro são especificados para criar o item, com outros valores de propriedade de item sendo especificados no corpo do modelo.</span><span class="sxs-lookup"><span data-stu-id="537bb-113">When the template is used, only the parameter values are specified to create the item, with other item property values being specified in the template body.</span></span> <span data-ttu-id="537bb-114">Um usuário que entende o Lote e os aplicativos a serem executados pelo Lote pode criar modelos especificando os valores de propriedade de pool, de trabalho e de tarefa.</span><span class="sxs-lookup"><span data-stu-id="537bb-114">A user who understands Batch and the applications to be run by Batch can create templates, specifying pool, job, and task property values.</span></span> <span data-ttu-id="537bb-115">Um usuário menos familiarizado com o Lote e/ou os aplicativos só precisa especificar os valores para os parâmetros definidos.</span><span class="sxs-lookup"><span data-stu-id="537bb-115">A user less familiar with Batch and/or the applications only needs to specify the values for the defined parameters.</span></span>

-   <span data-ttu-id="537bb-116">As fábricas de tarefa de trabalho criam uma ou mais tarefas associadas a um trabalho, evitando a necessidade de criar muitas definições de tarefa e simplificando significativamente o envio do trabalho.</span><span class="sxs-lookup"><span data-stu-id="537bb-116">Job task factories create one or more tasks associated with a job, avoiding the need for many task definitions to be created and significantly simplifying job submission.</span></span>


<span data-ttu-id="537bb-117">Arquivos de dados de entrada devem ser fornecidos para trabalhos, sendo que arquivos de dados de saída são produzidos com frequência.</span><span class="sxs-lookup"><span data-stu-id="537bb-117">Input data files need to be supplied for jobs and output data files are often produced.</span></span> <span data-ttu-id="537bb-118">Uma conta de armazenamento é associada por padrão com cada conta do Lote e os arquivos podem ser transferidos facilmente para e desta conta de armazenamento usando a CLI, sem necessidade de codificação nem de credenciais de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="537bb-118">A storage account is associated, by default, with each Batch account and files can be easily transferred to and from this storage account using the CLI, with no coding and no storage credentials required.</span></span>

<span data-ttu-id="537bb-119">Por exemplo, [ffmpeg](http://ffmpeg.org/) é um aplicativo popular que processa arquivos de áudio e vídeo.</span><span class="sxs-lookup"><span data-stu-id="537bb-119">For example, [ffmpeg](http://ffmpeg.org/) is a popular application that processes audio and video files.</span></span> <span data-ttu-id="537bb-120">A CLI do Lote do Azure pode ser usada para invocar ffmpeg para transcodificar arquivos de vídeo de origem para resoluções diferentes.</span><span class="sxs-lookup"><span data-stu-id="537bb-120">The Azure Batch CLI can be used to invoke ffmpeg to transcode source video files to different resolutions.</span></span>

-   <span data-ttu-id="537bb-121">Um modelo de pool é criado.</span><span class="sxs-lookup"><span data-stu-id="537bb-121">A pool template is created.</span></span> <span data-ttu-id="537bb-122">O usuário criando o modelo sabe como chamar o aplicativo ffmpeg e os respectivos requisitos; ele especifica o sistema operacional apropriado, o tamanho da VM, como o ffmpeg é instalado (de um pacote de aplicativos ou usando um gerenciador de pacotes, por exemplo) e outros valores de propriedade do pool.</span><span class="sxs-lookup"><span data-stu-id="537bb-122">The user creating the template knows how to call the ffmpeg application and its requirements; they specify the appropriate OS, VM size, how ffmpeg is installed (from an application package or using a package manager, for example), and other pool property values.</span></span> <span data-ttu-id="537bb-123">Parâmetros são criados para que, quando o modelo for usado, somente a ID do pool e o número de VMs precisem ser especificados.</span><span class="sxs-lookup"><span data-stu-id="537bb-123">Parameters are created so when the template is used, only the pool id and number of VMs need to be specified.</span></span>

-   <span data-ttu-id="537bb-124">Um modelo de trabalho é criado.</span><span class="sxs-lookup"><span data-stu-id="537bb-124">A job template is created.</span></span> <span data-ttu-id="537bb-125">O usuário criando o modelo sabe como o ffmpeg precisa ser invocado para transcodificar o vídeo de origem para uma resolução diferente e especifica a linha de comando da tarefa; ele também sabe que há uma pasta contendo os arquivos de vídeo de origem, com uma tarefa necessária por arquivo de entrada.</span><span class="sxs-lookup"><span data-stu-id="537bb-125">The user creating the template knows how ffmpeg needs to be invoked to transcode source video to a different resolution and specifies the task command line; they also know that there is a folder containing the source video files, with a task required per input file.</span></span>

-   <span data-ttu-id="537bb-126">Um usuário final com um conjunto de arquivos de vídeo para transcodificar cria primeiro um pool usando o modelo de pool, especificando somente a ID do pool e o número de VMs necessário.</span><span class="sxs-lookup"><span data-stu-id="537bb-126">An end user with a set of video files to transcode first creates a pool using the pool template, specifying only the pool id and number of VMs required.</span></span> <span data-ttu-id="537bb-127">Em seguida, ele pode carregar os arquivos de origem para transcodificar.</span><span class="sxs-lookup"><span data-stu-id="537bb-127">They can then upload the source files to transcode.</span></span> <span data-ttu-id="537bb-128">Um trabalho pode ser enviado usando o modelo de trabalho, especificando somente a ID do pool e o local dos arquivos de origem carregados.</span><span class="sxs-lookup"><span data-stu-id="537bb-128">A job can then be submitted using the job template, specifying only the pool id and location of the source files uploaded.</span></span> <span data-ttu-id="537bb-129">O trabalho do Lote é criado, com uma tarefa por arquivo de entrada sendo gerada.</span><span class="sxs-lookup"><span data-stu-id="537bb-129">The Batch job is created, with one task per input file being generated.</span></span> <span data-ttu-id="537bb-130">Por fim, os arquivos de saída transcodificados podem ser baixados.</span><span class="sxs-lookup"><span data-stu-id="537bb-130">Finally, the transcoded output files can be download.</span></span>

## <a name="installation"></a><span data-ttu-id="537bb-131">Instalação</span><span class="sxs-lookup"><span data-stu-id="537bb-131">Installation</span></span>

<span data-ttu-id="537bb-132">Os recursos de transferência de arquivo e de modelo requerem a instalação de uma extensão.</span><span class="sxs-lookup"><span data-stu-id="537bb-132">The template and file transfer capabilities require an extension to be installed.</span></span>

<span data-ttu-id="537bb-133">Para obter instruções sobre como instalar a CLI do Azure, consulte [Instalar a CLI do Azure 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="537bb-133">For instructions on how to install the Azure CLI see [Install Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli).</span></span>

<span data-ttu-id="537bb-134">Depois que a CLI do Azure foi instalada, a extensão do Lote pode ser instalada usando o seguinte comando de CLI:</span><span class="sxs-lookup"><span data-stu-id="537bb-134">Once the Azure CLI has been installed, the Batch extension can be installed using the following CLI command:</span></span>

```azurecli
az component update --add batch-extensions --allow-third-party
```

<span data-ttu-id="537bb-135">Para obter mais informações sobre a extensão do Lote, consulte [Extensões de CLI do Lote do Microsoft Azure para Windows, Mac e Linux](https://github.com/Azure/azure-batch-cli-extensions#microsoft-azure-batch-cli-extensions-for-windows-mac-and-linux).</span><span class="sxs-lookup"><span data-stu-id="537bb-135">For more information about the Batch extension, see [Microsoft Azure Batch CLI Extensions for Windows, Mac and Linux](https://github.com/Azure/azure-batch-cli-extensions#microsoft-azure-batch-cli-extensions-for-windows-mac-and-linux).</span></span>

## <a name="templates"></a><span data-ttu-id="537bb-136">Modelos</span><span class="sxs-lookup"><span data-stu-id="537bb-136">Templates</span></span>

<span data-ttu-id="537bb-137">A CLI do Lote do Azure permite que os itens como pools, trabalhos e tarefas sejam criados, especificando um arquivo JSON contendo os valores e nomes de propriedades.</span><span class="sxs-lookup"><span data-stu-id="537bb-137">The Azure Batch CLI allows items such as pools, jobs, and tasks to be created by specifying a JSON file containing property names and values.</span></span> <span data-ttu-id="537bb-138">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="537bb-138">For example:</span></span>

```azurecli
az batch pool create –-json-file AppPool.json
```

<span data-ttu-id="537bb-139">Os modelos do Lote do Azure são semelhantes aos modelos do Azure Resource Manager, na funcionalidade e na sintaxe.</span><span class="sxs-lookup"><span data-stu-id="537bb-139">Azure Batch templates are similar to Azure Resource Manager templates, in functionality and syntax.</span></span> <span data-ttu-id="537bb-140">Eles são arquivos JSON que contêm valores e nomes de propriedade do item, mas adicionam os conceitos principais a seguir:</span><span class="sxs-lookup"><span data-stu-id="537bb-140">They are JSON files that contain item property names and values, but add the following main concepts:</span></span>

-   <span data-ttu-id="537bb-141">**Parâmetros**</span><span class="sxs-lookup"><span data-stu-id="537bb-141">**Parameters**</span></span>

    -   <span data-ttu-id="537bb-142">Permitem que os valores de propriedade sejam especificados em uma seção de corpo, com necessidade de fornecer apenas os valores de parâmetro quando o modelo é usado.</span><span class="sxs-lookup"><span data-stu-id="537bb-142">Allow property values to be specified in a body section, with only parameter values needing to be supplied when the template is used.</span></span> <span data-ttu-id="537bb-143">Por exemplo, a definição completa para um pool pode ser colocada no corpo e apenas um parâmetro definido para a ID do pool; assim, para criar um pool, é necessário fornecer apenas uma cadeia de caracteres de ID do pool.</span><span class="sxs-lookup"><span data-stu-id="537bb-143">For example, the complete definition for a pool could be placed in the body and only one parameter defined for pool id; only a pool id string therefore needs to be supplied to create a pool.</span></span>
        
    -   <span data-ttu-id="537bb-144">O corpo do modelo pode ser criado por uma pessoa com conhecimento do Lote e dos aplicativos a serem executados pelo Lote; somente os valores dos parâmetros definidos pelo autor devem ser fornecidos quando o modelo é usado.</span><span class="sxs-lookup"><span data-stu-id="537bb-144">The template body can be authored by someone with knowledge of Batch and the applications to be run by Batch; only values for the author-defined parameters must be supplied when the template is used.</span></span> <span data-ttu-id="537bb-145">Portanto, um usuário sem o conhecimento detalhado do Lote e/ou do aplicativo pode usar os modelos.</span><span class="sxs-lookup"><span data-stu-id="537bb-145">A user without the in-depth Batch and/or application knowledge can therefore use the templates.</span></span>

-   <span data-ttu-id="537bb-146">**Variáveis**</span><span class="sxs-lookup"><span data-stu-id="537bb-146">**Variables**</span></span>

    -   <span data-ttu-id="537bb-147">Permitem que valores de parâmetro simples ou complexos sejam especificados em um local e usado em um ou mais locais no corpo do modelo.</span><span class="sxs-lookup"><span data-stu-id="537bb-147">Allow simple or complex parameter values to be specified in one place and used in one or more places in the template body.</span></span> <span data-ttu-id="537bb-148">Variáveis podem simplificar e reduzir o tamanho do modelo, bem como facilitar a manutenção dele por ter um local para alterar as propriedades cujo valor pode ser alterado.</span><span class="sxs-lookup"><span data-stu-id="537bb-148">Variables can simplify and reduce the size of the template, as well as make it more maintainable by having one location to change properties whose value may change.</span></span>

-   <span data-ttu-id="537bb-149">**Construções de nível superior**</span><span class="sxs-lookup"><span data-stu-id="537bb-149">**Higher-level constructs**</span></span>

    -   <span data-ttu-id="537bb-150">Há algumas construções de nível superior disponíveis no modelo que ainda não estão disponíveis nas APIs do Lote.</span><span class="sxs-lookup"><span data-stu-id="537bb-150">Some higher-level constructs are available in the template that are not yet available in the Batch APIs.</span></span> <span data-ttu-id="537bb-151">Por exemplo, uma fábrica de tarefas pode ser definida em um modelo de trabalho que cria várias tarefas para o trabalho usando uma definição de tarefa comum.</span><span class="sxs-lookup"><span data-stu-id="537bb-151">For example, a task factory can be defined in a job template that creates multiple tasks for the job using a common task definition.</span></span> <span data-ttu-id="537bb-152">Essas construções evitam a necessidade de codificar para criar dinamicamente vários arquivos JSON (assim como um arquivo por tarefa), bem como para criar arquivos de script para instalar aplicativos por meio de um gerenciador de pacotes, por exemplo.</span><span class="sxs-lookup"><span data-stu-id="537bb-152">These constructs avoid the need to code to dynamically create multiple JSON files, such as one file per task, as well as create script files to install applications via a package manager, for example.</span></span>

    -   <span data-ttu-id="537bb-153">Em algum momento, quando aplicável, essas construções podem ser adicionadas ao serviço de Lote e disponível nas APIs de Lote, interfaces do usuário, etc.</span><span class="sxs-lookup"><span data-stu-id="537bb-153">At some point, where applicable, these constructs may be added to the Batch service and available in the Batch APIs, UIs, etc.</span></span>

### <a name="pool-templates"></a><span data-ttu-id="537bb-154">Modelos de pool</span><span class="sxs-lookup"><span data-stu-id="537bb-154">Pool templates</span></span>

<span data-ttu-id="537bb-155">Além dos recursos de modelo padrão de variáveis e parâmetros, as seguintes construções de nível superior têm suporte pelo modelo de pool:</span><span class="sxs-lookup"><span data-stu-id="537bb-155">In addition to the standard template capabilities of parameters and variables, the following higher-level constructs are supported by the pool template:</span></span>

-   <span data-ttu-id="537bb-156">**Referências do pacote**</span><span class="sxs-lookup"><span data-stu-id="537bb-156">**Package references**</span></span>

    -   <span data-ttu-id="537bb-157">Opcionalmente, permite que o software seja copiado para nós de pool usando gerenciadores de pacotes.</span><span class="sxs-lookup"><span data-stu-id="537bb-157">Optionally allows software to be copied to pool nodes by using package managers.</span></span> <span data-ttu-id="537bb-158">O gerenciador de pacotes e a ID do pacote são especificados.</span><span class="sxs-lookup"><span data-stu-id="537bb-158">The package manager and package id are specified.</span></span> <span data-ttu-id="537bb-159">Ser capaz de declarar um ou mais pacotes evita a necessidade de criar um script que obtém os pacotes necessários, instalá-lo e executá-lo em cada nó de pool.</span><span class="sxs-lookup"><span data-stu-id="537bb-159">Being able to declare one or more packages avoids the need to create a script that gets the required packages, install the script, and run the script on each pool node.</span></span>

<span data-ttu-id="537bb-160">A seguir está um exemplo de um modelo que cria um pool de VMs do Linux com ffmpeg instalado, cujo uso requer apenas o fornecimento do número de VMs e de uma cadeia de caracteres de ID do pool:</span><span class="sxs-lookup"><span data-stu-id="537bb-160">The following is an example of a template that creates a pool of Linux VMs with ffmpeg installed and only requires a pool id string and the number of VMs to be supplied to use:</span></span>

```json
{
    "parameters": {
        "nodeCount": {
            "type": "int",
            "metadata": {
                "description": "The number of pool nodes"
            }
        },
        "poolId": {
            "type": "string",
            "metadata": {
                "description": "The pool id "
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

<span data-ttu-id="537bb-161">Se o arquivo de modelo fosse nomeado _pool-ffmpeg.json_, o modelo seria invocado da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="537bb-161">If the template file was named _pool-ffmpeg.json_, then the template would be invoked as follows:</span></span>

```azurecli
az batch pool create --template pool-ffmpeg.json
```

### <a name="job-templates"></a><span data-ttu-id="537bb-162">Modelos de trabalho</span><span class="sxs-lookup"><span data-stu-id="537bb-162">Job templates</span></span>

<span data-ttu-id="537bb-163">Além dos recursos de modelo padrão de variáveis e parâmetros, as seguintes construções de nível superior têm suporte pelo modelo de trabalho:</span><span class="sxs-lookup"><span data-stu-id="537bb-163">In addition to the standard template capabilities of parameters and variables, the following higher-level constructs are supported by the job template:</span></span>

-   <span data-ttu-id="537bb-164">**Fábrica de tarefas**</span><span class="sxs-lookup"><span data-stu-id="537bb-164">**Task factory**</span></span>

    -   <span data-ttu-id="537bb-165">Com base em uma definição de tarefa, cria várias tarefas para um trabalho.</span><span class="sxs-lookup"><span data-stu-id="537bb-165">Creates multiple tasks for a job from one task definition.</span></span> <span data-ttu-id="537bb-166">Três tipos de fábrica de tarefas têm suporte – limpeza paramétrica, tarefa por arquivo e coleção de tarefas.</span><span class="sxs-lookup"><span data-stu-id="537bb-166">Three types of task factory are supported – parametric sweep, task per file, and task collection.</span></span>

<span data-ttu-id="537bb-167">Este é um exemplo de um modelo que cria um trabalho que, por sua vez, usa ffmpeg para transcodificar arquivos de vídeo MP4 para uma de duas resoluções mais baixas, com uma tarefa criada por arquivo de vídeo de origem:</span><span class="sxs-lookup"><span data-stu-id="537bb-167">The following is an example of a template that creates a job that uses ffmpeg to transcode MP4 video files to one of two lower resolutions, with one task created per source video file:</span></span>

```json
{
    "parameters": {
        "poolId": {
            "type": "string",
            "metadata": {
                "description": "The name of Azure Batch pool which runs the job"
            }
        },
        "jobId": {
            "type": "string",
            "metadata": {
                "description": "The name of Azure Batch job"
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

<span data-ttu-id="537bb-168">Se o arquivo de modelo fosse nomeado _job-ffmpeg.json_, o modelo seria invocado da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="537bb-168">If the template file was named _job-ffmpeg.json_, then the template would be invoked as follows:</span></span>

```azurecli
az batch job create --template job-ffmpeg.json
```

## <a name="file-groups-and-file-transfer"></a><span data-ttu-id="537bb-169">Transferência de arquivos e grupos de arquivo</span><span class="sxs-lookup"><span data-stu-id="537bb-169">File groups and file transfer</span></span>

<span data-ttu-id="537bb-170">A maioria dos trabalhos e tarefas exigem arquivos de entrada e produzem arquivos de saída.</span><span class="sxs-lookup"><span data-stu-id="537bb-170">Most jobs and tasks require input files and produce output files.</span></span> <span data-ttu-id="537bb-171">Os arquivos de entrada e de saída normalmente precisam ser transferidos do cliente para o nó ou do nó para o cliente.</span><span class="sxs-lookup"><span data-stu-id="537bb-171">Both input files and output files typically need to be transferred, either from the client to the node, or from the node to the client.</span></span> <span data-ttu-id="537bb-172">A extensão de CLI do Lote do Azure abstrai a transferência de arquivo e utiliza a conta de armazenamento que é criada por padrão para cada conta do Lote.</span><span class="sxs-lookup"><span data-stu-id="537bb-172">The Azure Batch CLI extension abstracts away file transfer and utilizes the storage account that is created by default for each Batch account.</span></span>

<span data-ttu-id="537bb-173">Um grupo de arquivo é igual a um contêiner que é criado na conta de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="537bb-173">A file group equates to a container that is created in the Azure storage account.</span></span> <span data-ttu-id="537bb-174">O grupo de arquivo pode ter subpastas.</span><span class="sxs-lookup"><span data-stu-id="537bb-174">The file group may have subfolders.</span></span>

<span data-ttu-id="537bb-175">A extensão de CLI do Lote fornece comandos para carregar arquivos do cliente para um grupo de arquivo especificado e baixar arquivos do grupo de arquivo especificado para um cliente.</span><span class="sxs-lookup"><span data-stu-id="537bb-175">The Batch CLI extension provides commands for uploading files from client to a specified file group and downloading files from the specified file group to a client.</span></span>

```azurecli
az batch file upload --local-path c:\source_videos\*.mp4 
    --file-group ffmpeg-input

az batch file download --file-group ffmpeg-output --local-path
    c:\output_lowres_videos
```

<span data-ttu-id="537bb-176">Modelos de pool e de trabalho permitem que os arquivos armazenados em grupos de arquivo sejam especificados para cópia em nós de pool ou transferidos de nós de pool para um grupo de arquivo.</span><span class="sxs-lookup"><span data-stu-id="537bb-176">Pool and job templates allow files stored in file groups to be specified for copy onto pool nodes or off pool nodes back to a file group.</span></span> <span data-ttu-id="537bb-177">Por exemplo, o modelo de trabalho especificado anteriormente, o grupo de arquivo "ffmpeg-input" é especificado para a fábrica de tarefas como o local dos arquivos de vídeo de origem copiados para o nó para transcodificação; o grupo de arquivo "ffmpeg-output" é usado como o local para o qual os arquivos de saída transcodificados são copiados do nó que executa cada tarefa.</span><span class="sxs-lookup"><span data-stu-id="537bb-177">For example, in the job template specified previously, the file group “ffmpeg-input” is specified for the task factory as the location of the source video files copied down onto the node for transcoding; the file group “ffmpeg-output” is used as the location where the transcoded output files are copied to from the node running each task.</span></span>

## <a name="summary"></a><span data-ttu-id="537bb-178">Resumo</span><span class="sxs-lookup"><span data-stu-id="537bb-178">Summary</span></span>

<span data-ttu-id="537bb-179">Atualmente, o suporte à transferência de arquivo e de modelo foi adicionado somente à CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="537bb-179">Template and file transfer support have currently been added only to the Azure CLI.</span></span> <span data-ttu-id="537bb-180">A meta é expandir o público que pode usar o Lote para usuários que não precisam desenvolver código usando as APIs de Lote, tais como pesquisadores, usuários de TI e assim por diante.</span><span class="sxs-lookup"><span data-stu-id="537bb-180">The goal is to expand the audience that can use Batch to users who do not need to develop code using the Batch APIs, such as researchers, IT users, and so on.</span></span> <span data-ttu-id="537bb-181">Sem codificação, os usuários com conhecimento do Azure, do Lote e dos aplicativos a serem executados pelo Lote podem criar modelos para criação de pools e trabalhos.</span><span class="sxs-lookup"><span data-stu-id="537bb-181">Without coding, users with knowledge of Azure, Batch, and the applications to be run by Batch can create templates for pool and job creation.</span></span> <span data-ttu-id="537bb-182">Com os parâmetros de modelo, os usuários sem conhecimento detalhado do Lote e dos aplicativos podem usar esses modelos.</span><span class="sxs-lookup"><span data-stu-id="537bb-182">With template parameters, users without detailed knowledge of Batch and the applications can use the templates.</span></span>

<span data-ttu-id="537bb-183">Experimente a extensão do Lote para a CLI do Azure e forneça comentários ou sugestões, seja nos comentários deste artigo ou no [fórum do Lote do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=azurebatch).</span><span class="sxs-lookup"><span data-stu-id="537bb-183">Try out the Batch extension for the Azure CLI and provide us with any feedback or suggestions, either in the comments for this article or via the [Azure Batch forum](https://social.msdn.microsoft.com/forums/azure/home?forum=azurebatch).</span></span>

## <a name="next-steps"></a><span data-ttu-id="537bb-184">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="537bb-184">Next steps</span></span>

- <span data-ttu-id="537bb-185">Veja a postagem de blog de modelos do Lote: [Executando trabalhos do Lote do Azure usando a CLI do Azure – não há necessidade de código](https://azure.microsoft.com/en-us/blog/running-azure-batch-jobs-using-the-azure-cli-no-code-required/).</span><span class="sxs-lookup"><span data-stu-id="537bb-185">See the Batch templates blog post: [Running Azure Batch jobs using the Azure CLI – no code required](https://azure.microsoft.com/en-us/blog/running-azure-batch-jobs-using-the-azure-cli-no-code-required/).</span></span>
- <span data-ttu-id="537bb-186">Documentação detalhada de instalação e uso, amostras e código-fonte estão disponíveis no [repositório GitHub do Azure](https://github.com/Azure/azure-batch-cli-extensions).</span><span class="sxs-lookup"><span data-stu-id="537bb-186">Detailed installation and usage documentation, samples, and source code are available in the [Azure GitHub repository](https://github.com/Azure/azure-batch-cli-extensions).</span></span>
