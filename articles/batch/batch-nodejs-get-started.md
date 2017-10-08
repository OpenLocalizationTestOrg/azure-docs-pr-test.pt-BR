---
title: "aaaTutorial - biblioteca de cliente do uso Olá lote do Azure para Node.js | Microsoft Docs"
description: "Aprenda os conceitos básicos de saudação do lote do Azure e criar uma solução simple usando o Node. js."
services: batch
author: shwetams
manager: timlt
ms.assetid: 
ms.service: batch
ms.devlang: nodejs
ms.topic: hero-article
ms.workload: big-compute
ms.date: 05/22/2017
ms.author: shwetams
ms.openlocfilehash: d2b0ecbe764e7100affd7b02839aef3077b073cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-batch-sdk-for-nodejs"></a><span data-ttu-id="4b5bd-103">Introdução ao SDK do lote para o Node.js</span><span class="sxs-lookup"><span data-stu-id="4b5bd-103">Get started with Batch SDK for Node.js</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="4b5bd-104">.NET</span><span class="sxs-lookup"><span data-stu-id="4b5bd-104">.NET</span></span>](batch-dotnet-get-started.md)
> * [<span data-ttu-id="4b5bd-105">Python</span><span class="sxs-lookup"><span data-stu-id="4b5bd-105">Python</span></span>](batch-python-tutorial.md)
> * [<span data-ttu-id="4b5bd-106">Node.js</span><span class="sxs-lookup"><span data-stu-id="4b5bd-106">Node.js</span></span>](batch-nodejs-get-started.md)
>
>

<span data-ttu-id="4b5bd-107">Conheça os fundamentos de saudação da criação de um cliente em lotes usando Node. js [SDK de Node.js do Azure em lotes](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/).</span><span class="sxs-lookup"><span data-stu-id="4b5bd-107">Learn hello basics of building a Batch client in Node.js using [Azure Batch Node.js SDK](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/).</span></span> <span data-ttu-id="4b5bd-108">Podemos adotar uma abordagem passo a passo de compressão de um cenário para um aplicativo de lote e, em seguida, configurá-lo usando um cliente do Node.js.</span><span class="sxs-lookup"><span data-stu-id="4b5bd-108">We take a step by step approach of understanding a scenario for a batch application and then setting it up using a Node.js client.</span></span>  

## <a name="prerequisites"></a><span data-ttu-id="4b5bd-109">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="4b5bd-109">Prerequisites</span></span>
<span data-ttu-id="4b5bd-110">Este artigo pressupõe que você tem um conhecimento prático do Node.js e que esteja familiarizado com o Linux.</span><span class="sxs-lookup"><span data-stu-id="4b5bd-110">This article assumes that you have a working knowledge of Node.js and familiarity with Linux.</span></span> <span data-ttu-id="4b5bd-111">Ele também pressupõe que você tenha uma configuração de conta do Azure com serviços de armazenamento e de lote de toocreate de direitos do acesso.</span><span class="sxs-lookup"><span data-stu-id="4b5bd-111">It also assumes that you have an Azure account setup with access rights toocreate Batch and Storage services.</span></span>

<span data-ttu-id="4b5bd-112">Recomendamos a leitura [visão geral técnica do Azure Batch](batch-technical-overview.md) antes de passar por etapas Olá descritos neste artigo.</span><span class="sxs-lookup"><span data-stu-id="4b5bd-112">We recommend reading [Azure Batch Technical Overview](batch-technical-overview.md) before you go through hello steps outlined this article.</span></span>

## <a name="hello-tutorial-scenario"></a><span data-ttu-id="4b5bd-113">cenário do tutorial Olá</span><span class="sxs-lookup"><span data-stu-id="4b5bd-113">hello tutorial scenario</span></span>
<span data-ttu-id="4b5bd-114">Vamos entenda o cenário de fluxo de trabalho em lotes hello.</span><span class="sxs-lookup"><span data-stu-id="4b5bd-114">Let us understand hello batch workflow scenario.</span></span> <span data-ttu-id="4b5bd-115">Temos um script simples escrito em Python downloads csv todos os arquivos a partir de um contêiner de armazenamento de BLOBs do Azure e converte-os tooJSON.</span><span class="sxs-lookup"><span data-stu-id="4b5bd-115">We have a simple script written in Python that downloads all csv files from an Azure Blob storage container and converts them tooJSON.</span></span> <span data-ttu-id="4b5bd-116">tooprocess conta de armazenamento vários contêineres em paralelo, é possível implantar o script hello como um trabalho de lote do Azure.</span><span class="sxs-lookup"><span data-stu-id="4b5bd-116">tooprocess multiple storage account containers in parallel, we can deploy hello script as an Azure Batch job.</span></span>

## <a name="azure-batch-architecture"></a><span data-ttu-id="4b5bd-117">Arquitetura de lote do Azure</span><span class="sxs-lookup"><span data-stu-id="4b5bd-117">Azure Batch Architecture</span></span>
<span data-ttu-id="4b5bd-118">Olá diagrama a seguir mostra como é possível dimensionar script de Python hello usando o lote do Azure e um cliente Node. js.</span><span class="sxs-lookup"><span data-stu-id="4b5bd-118">hello following diagram depicts how we can scale hello Python script using Azure Batch and a Node.js client.</span></span>

![Cenário de lote do Azure](./media/batch-nodejs-get-started/BatchScenario.png)

<span data-ttu-id="4b5bd-120">cliente de Node. js Olá implanta um trabalho em lotes com uma tarefa de preparação (explicado em detalhes mais tarde) e um conjunto de tarefas, dependendo do número de saudação de contêineres na conta de armazenamento hello.</span><span class="sxs-lookup"><span data-stu-id="4b5bd-120">hello node.js client deploys a batch job with a preparation task (explained in detail later) and a set of tasks depending on hello number of containers in hello storage account.</span></span> <span data-ttu-id="4b5bd-121">Você pode baixar os scripts de saudação do repositório do github hello.</span><span class="sxs-lookup"><span data-stu-id="4b5bd-121">You can download hello scripts from hello github repository.</span></span>

* [<span data-ttu-id="4b5bd-122">Cliente Node.js</span><span class="sxs-lookup"><span data-stu-id="4b5bd-122">Node.js client</span></span>](https://github.com/Azure/azure-batch-samples/blob/master/Node.js/GettingStarted/nodejs_batch_client_sample.js)
* [<span data-ttu-id="4b5bd-123">Shell scripts de tarefa de preparação</span><span class="sxs-lookup"><span data-stu-id="4b5bd-123">Preparation task shell scripts</span></span>](https://github.com/Azure/azure-batch-samples/blob/master/Node.js/GettingStarted/startup_prereq.sh)
* [<span data-ttu-id="4b5bd-124">Processador do Python csv tooJSON</span><span class="sxs-lookup"><span data-stu-id="4b5bd-124">Python csv tooJSON processor</span></span>](https://github.com/Azure/azure-batch-samples/blob/master/Node.js/GettingStarted/processcsv.py)

> [!TIP]
> <span data-ttu-id="4b5bd-125">cliente Node. js Olá Olá link especificado não contém código específico toobe implantado como um aplicativo de função do Azure.</span><span class="sxs-lookup"><span data-stu-id="4b5bd-125">hello Node.js client in hello link specified does not contain specific code toobe deployed as an Azure function app.</span></span> <span data-ttu-id="4b5bd-126">Você pode consultar toohello seguindo os links para toocreate instruções um.</span><span class="sxs-lookup"><span data-stu-id="4b5bd-126">You can refer toohello following links for instructions toocreate one.</span></span>
> - [<span data-ttu-id="4b5bd-127">Como criar um aplicativo de função</span><span class="sxs-lookup"><span data-stu-id="4b5bd-127">Create function app</span></span>](../azure-functions/functions-create-first-azure-function.md)
> - [<span data-ttu-id="4b5bd-128">Como criar uma função de gatilho de temporizador</span><span class="sxs-lookup"><span data-stu-id="4b5bd-128">Create timer trigger function</span></span>](../azure-functions/functions-bindings-timer.md)
>
>

## <a name="build-hello-application"></a><span data-ttu-id="4b5bd-129">Criar um aplicativo hello</span><span class="sxs-lookup"><span data-stu-id="4b5bd-129">Build hello application</span></span>

<span data-ttu-id="4b5bd-130">Agora, vamos siga o processo de Olá passo a passo na criação de cliente do Node. js hello:</span><span class="sxs-lookup"><span data-stu-id="4b5bd-130">Now, let us follow hello process step by step into building hello Node.js client:</span></span>

### <a name="step-1-install-azure-batch-sdk"></a><span data-ttu-id="4b5bd-131">Etapa 1: instalação o SDK do lote do Azure</span><span class="sxs-lookup"><span data-stu-id="4b5bd-131">Step 1: Install Azure Batch SDK</span></span>

<span data-ttu-id="4b5bd-132">Você pode instalar o SDK do lote do Azure para Node.js usando o comando Olá npm install.</span><span class="sxs-lookup"><span data-stu-id="4b5bd-132">You can install Azure Batch SDK for Node.js using hello npm install command.</span></span>

`npm install azure-batch`

<span data-ttu-id="4b5bd-133">Esse comando instala a versão mais recente de saudação do nó de lote do azure SDK.</span><span class="sxs-lookup"><span data-stu-id="4b5bd-133">This command installs hello latest version of azure-batch node SDK.</span></span>

>[!Tip]
> <span data-ttu-id="4b5bd-134">Em um aplicativo de função do Azure, você pode ir muito o "Console de Kudu" hello Azure função configurações guia toorun Olá npm comandos de instalação.</span><span class="sxs-lookup"><span data-stu-id="4b5bd-134">In an Azure Function app, you can go too"Kudu Console" in hello Azure function's Settings tab toorun hello npm install commands.</span></span> <span data-ttu-id="4b5bd-135">Nesse caso tooinstall SDK de lote do Azure para Node.js.</span><span class="sxs-lookup"><span data-stu-id="4b5bd-135">In this case tooinstall Azure Batch SDK for Node.js.</span></span>
>
>

### <a name="step-2-create-an-azure-batch-account"></a><span data-ttu-id="4b5bd-136">Etapa 2: criação uma conta de lote do Azure</span><span class="sxs-lookup"><span data-stu-id="4b5bd-136">Step 2: Create an Azure Batch account</span></span>

<span data-ttu-id="4b5bd-137">Você pode criá-la de saudação [portal do Azure](batch-account-create-portal.md) ou da linha de comando ([Powershell](batch-powershell-cmdlets-get-started.md) /[cli do Azure](https://docs.microsoft.com/cli/azure/overview)).</span><span class="sxs-lookup"><span data-stu-id="4b5bd-137">You can create it from hello [Azure portal](batch-account-create-portal.md) or from command line ([Powershell](batch-powershell-cmdlets-get-started.md) /[Azure cli](https://docs.microsoft.com/cli/azure/overview)).</span></span>

<span data-ttu-id="4b5bd-138">A seguir é Olá comandos toocreate um por meio de CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="4b5bd-138">Following are hello commands toocreate one through Azure CLI.</span></span>

<span data-ttu-id="4b5bd-139">Criar um grupo de recursos, ignore esta etapa se você já tiver um onde você deseja toocreate Olá conta do lote:</span><span class="sxs-lookup"><span data-stu-id="4b5bd-139">Create a Resource Group, skip this step if you already have one where you want toocreate hello Batch Account:</span></span>

`az group create -n "<resource-group-name>" -l "<location>"`

<span data-ttu-id="4b5bd-140">Em seguida, crie uma conta de lote do Azure.</span><span class="sxs-lookup"><span data-stu-id="4b5bd-140">Next, create an Azure Batch account.</span></span>

`az batch account create -l "<location>"  -g "<resource-group-name>" -n "<batch-account-name>"`

<span data-ttu-id="4b5bd-141">Cada conta de lote tem suas chaves de acesso correspondentes.</span><span class="sxs-lookup"><span data-stu-id="4b5bd-141">Each Batch account has its corresponding access keys.</span></span> <span data-ttu-id="4b5bd-142">Essas chaves são toocreate necessários mais recursos na conta do lote do Azure.</span><span class="sxs-lookup"><span data-stu-id="4b5bd-142">These keys are needed toocreate further resources in Azure batch account.</span></span> <span data-ttu-id="4b5bd-143">Uma prática recomendada para o ambiente de produção é toouse Azure Key Vault toostore essas chaves.</span><span class="sxs-lookup"><span data-stu-id="4b5bd-143">A good practice for production environment is toouse Azure Key Vault toostore these keys.</span></span> <span data-ttu-id="4b5bd-144">Em seguida, você pode criar um serviço principal para o aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="4b5bd-144">You can then create a Service principal for hello application.</span></span> <span data-ttu-id="4b5bd-145">Usar este aplicativo de serviço principal Olá pode criar um chaves de tooaccess token OAuth do Cofre de chave hello.</span><span class="sxs-lookup"><span data-stu-id="4b5bd-145">Using this service principal hello application can create an OAuth token tooaccess keys from hello key vault.</span></span>

`az batch account keys list -g "<resource-group-name>" -n "<batch-account-name>"`

<span data-ttu-id="4b5bd-146">Copie e armazene Olá toobe chave usado nas etapas subsequentes hello.</span><span class="sxs-lookup"><span data-stu-id="4b5bd-146">Copy and store hello key toobe used in hello subsequent steps.</span></span>

### <a name="step-3-create-an-azure-batch-service-client"></a><span data-ttu-id="4b5bd-147">Etapa 3: criação um cliente de serviço de lote do Azure</span><span class="sxs-lookup"><span data-stu-id="4b5bd-147">Step 3: Create an Azure Batch service client</span></span>
<span data-ttu-id="4b5bd-148">Trecho de código a seguir primeiro importa o módulo de Node.js do azure batch hello e, em seguida, cria um cliente de serviço de lote.</span><span class="sxs-lookup"><span data-stu-id="4b5bd-148">Following code snippet first imports hello azure-batch Node.js module and then creates a Batch Service client.</span></span> <span data-ttu-id="4b5bd-149">Você precisa toofirst criar um objeto SharedKeyCredentials com chave de conta em lotes Olá copiado da etapa anterior hello.</span><span class="sxs-lookup"><span data-stu-id="4b5bd-149">You need toofirst create a SharedKeyCredentials object with hello Batch account key copied from hello previous step.</span></span>

```nodejs
// Initializing Azure Batch variables

var batch = require('azure-batch');

var accountName = '<azure-batch-account-name>';

var accountKey = '<account-key-downloaded>';

var accountUrl = '<account-url>'

// Create Batch credentials object using account name and account key

var credentials = new batch.SharedKeyCredentials(accountName,accountKey);

// Create Batch service client

var batch_client = new batch.ServiceClient(credentials,accountUrl);

```

<span data-ttu-id="4b5bd-150">Olá URI do lote do Azure pode ser encontrada no guia de visão geral de saudação do hello portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="4b5bd-150">hello Azure Batch URI can be found in hello Overview tab of hello Azure portal.</span></span> <span data-ttu-id="4b5bd-151">Ela é do formato de saudação:</span><span class="sxs-lookup"><span data-stu-id="4b5bd-151">It is of hello format:</span></span>

`https://accountname.location.batch.azure.com`

<span data-ttu-id="4b5bd-152">Consulte a captura de tela de toohello:</span><span class="sxs-lookup"><span data-stu-id="4b5bd-152">Refer toohello screenshot:</span></span>

![URI de lote do Azure](./media/batch-nodejs-get-started/azurebatchuri.png)



### <a name="step-4-create-an-azure-batch-pool"></a><span data-ttu-id="4b5bd-154">Etapa 4: criação de um pool de lote do Azure</span><span class="sxs-lookup"><span data-stu-id="4b5bd-154">Step 4: Create an Azure Batch pool</span></span>
<span data-ttu-id="4b5bd-155">Um pool de lote do Azure consiste em várias VMs (também conhecidos como nós de lote).</span><span class="sxs-lookup"><span data-stu-id="4b5bd-155">An Azure Batch pool consists of multiple VMs (also known as Batch Nodes).</span></span> <span data-ttu-id="4b5bd-156">Serviço de lote do Azure implanta tarefas Olá em nós e os gerencia.</span><span class="sxs-lookup"><span data-stu-id="4b5bd-156">Azure Batch service deploys hello tasks on these nodes and manages them.</span></span> <span data-ttu-id="4b5bd-157">Você pode definir Olá seguindo os parâmetros de configuração para o pool.</span><span class="sxs-lookup"><span data-stu-id="4b5bd-157">You can define hello following configuration parameters for your pool.</span></span>

* <span data-ttu-id="4b5bd-158">Tipo de imagem da máquina virtual</span><span class="sxs-lookup"><span data-stu-id="4b5bd-158">Type of Virtual Machine image</span></span>
* <span data-ttu-id="4b5bd-159">Tamanho dos nós da máquina virtual</span><span class="sxs-lookup"><span data-stu-id="4b5bd-159">Size of Virtual Machine nodes</span></span>
* <span data-ttu-id="4b5bd-160">Número de nós da máquina virtual</span><span class="sxs-lookup"><span data-stu-id="4b5bd-160">Number of Virtual Machine nodes</span></span>

> [!Tip]
> <span data-ttu-id="4b5bd-161">tamanho de saudação e o número de nós de máquina Virtual dependem em número de saudação de tarefas que deseja toorun em paralelo e também própria tarefa hello.</span><span class="sxs-lookup"><span data-stu-id="4b5bd-161">hello size and number of Virtual Machine nodes largely depend on hello number of tasks you want toorun in parallel and also hello task itself.</span></span> <span data-ttu-id="4b5bd-162">Recomendamos que você teste toodetermine Olá ideal número e tamanho.</span><span class="sxs-lookup"><span data-stu-id="4b5bd-162">We recommend testing toodetermine hello ideal number and size.</span></span>
>
>

<span data-ttu-id="4b5bd-163">Olá trecho de código a seguir cria Olá objetos de parâmetro de configuração.</span><span class="sxs-lookup"><span data-stu-id="4b5bd-163">hello following code snippet creates hello configuration parameter objects.</span></span>

```nodejs
// Creating Image reference configuration for Ubuntu Linux VM
var imgRef = {publisher:"Canonical",offer:"UbuntuServer",sku:"14.04.2-LTS",version:"latest"}

// Creating hello VM configuration object with hello SKUID
var vmconfig = {imageReference:imgRef,nodeAgentSKUId:"batch.node.ubuntu 14.04"}

// Setting hello VM size tooStandard F4
var vmSize = "STANDARD_F4"

//Setting number of VMs in hello pool too4
var numVMs = 4
```

> [!Tip]
> <span data-ttu-id="4b5bd-164">Para Olá lista de imagens de VM do Linux disponíveis para o lote do Azure e seus IDs de SKU, consulte [lista de imagens de máquinas virtuais](batch-linux-nodes.md#list-of-virtual-machine-images).</span><span class="sxs-lookup"><span data-stu-id="4b5bd-164">For hello list of Linux VM images available for Azure Batch and their SKU IDs, see [List of virtual machine images](batch-linux-nodes.md#list-of-virtual-machine-images).</span></span>
>
>

<span data-ttu-id="4b5bd-165">Após a definição de configuração do pool Olá, você pode criar pool de lote do Azure hello.</span><span class="sxs-lookup"><span data-stu-id="4b5bd-165">Once hello pool configuration is defined, you can create hello Azure Batch pool.</span></span> <span data-ttu-id="4b5bd-166">Olá comando de pool de lote cria nós de máquina Virtual do Azure e prepara-los toobe tooreceive pronto tarefas tooexecute.</span><span class="sxs-lookup"><span data-stu-id="4b5bd-166">hello Batch pool command creates Azure Virtual Machine nodes and prepares them toobe ready tooreceive tasks tooexecute.</span></span> <span data-ttu-id="4b5bd-167">Cada pool deve ter um ID exclusivo para referência em etapas subsequentes.</span><span class="sxs-lookup"><span data-stu-id="4b5bd-167">Each pool should have a unique ID for reference in subsequent steps.</span></span>

<span data-ttu-id="4b5bd-168">saudação de trecho de código a seguir cria um pool de lote do Azure.</span><span class="sxs-lookup"><span data-stu-id="4b5bd-168">hello following code snippet creates an Azure Batch pool.</span></span>

```nodejs
// Create a unique Azure Batch pool ID
var poolid = "pool" + customerDetails.customerid;
var poolConfig = {id:poolid, displayName:poolid,vmSize:vmSize,virtualMachineConfiguration:vmconfig,targetDedicatedComputeNodes:numVms,enableAutoScale:false };
// Creating hello Pool for hello specific customer
var pool = batch_client.pool.add(poolConfig,function(error,result){
    if(error!=null){console.log(error.response)};
});
```

<span data-ttu-id="4b5bd-169">Você pode verificar o status Olá Olá pool criado e verifique se o estado de saudação está em "ativo" antes de prosseguir com o envio de um pool de toothat de trabalho.</span><span class="sxs-lookup"><span data-stu-id="4b5bd-169">You can check hello status of hello pool created and ensure that hello state is in "active" before going ahead with submission of a Job toothat pool.</span></span>

```nodejs
var cloudPool = batch_client.pool.get(poolid,function(error,result,request,response){
        if(error == null)
        {

            if(result.state == "active")
            {
                console.log("Pool is active");
            }
        }
        else
        {
            if(error.statusCode==404)
            {
                console.log("Pool not found yet returned 404...");    

            }
            else
            {
                console.log("Error occurred while retrieving pool data");
            }
        }
        });
```

<span data-ttu-id="4b5bd-170">A seguir é um objeto de resultado de exemplo retornado pela função de pool.get hello.</span><span class="sxs-lookup"><span data-stu-id="4b5bd-170">Following is a sample result object returned by hello pool.get function.</span></span>

```
{ id: 'processcsv_201721152',
  displayName: 'processcsv_201721152',
  url: 'https://<batch-account-name>.centralus.batch.azure.com/pools/processcsv_201721152',
  eTag: '<eTag>',
  lastModified: 2017-03-27T10:28:02.398Z,
  creationTime: 2017-03-27T10:28:02.398Z,
  state: 'active',
  stateTransitionTime: 2017-03-27T10:28:02.398Z,
  allocationState: 'resizing',
  allocationStateTransitionTime: 2017-03-27T10:28:02.398Z,
  vmSize: 'standard_a1',
  virtualMachineConfiguration:
   { imageReference:
      { publisher: 'Canonical',
        offer: 'UbuntuServer',
        sku: '14.04.2-LTS',
        version: 'latest' },
     nodeAgentSKUId: 'batch.node.ubuntu 14.04' },
  resizeTimeout:
   { [Number: 900000]
     _milliseconds: 900000,
     _days: 0,
     _months: 0,
     _data:
      { milliseconds: 0,
        seconds: 0,
        minutes: 15,
        hours: 0,
        days: 0,
        months: 0,
        years: 0 },
     _locale:
      Locale {
        _calendar: [Object],
        _longDateFormat: [Object],
        _invalidDate: 'Invalid date',
        ordinal: [Function: ordinal],
        _ordinalParse: /\d{1,2}(th|st|nd|rd)/,
        _relativeTime: [Object],
        _months: [Object],
        _monthsShort: [Object],
        _week: [Object],
        _weekdays: [Object],
        _weekdaysMin: [Object],
        _weekdaysShort: [Object],
        _meridiemParse: /[ap]\.?m?\.?/i,
        _abbr: 'en',
        _config: [Object],
        _ordinalParseLenient: /\d{1,2}(th|st|nd|rd)|\d{1,2}/ } },
  currentDedicated: 0,
  targetDedicated: 4,
  enableAutoScale: false,
  enableInterNodeCommunication: false,
  maxTasksPerNode: 1,
  taskSchedulingPolicy: { nodeFillType: 'Spread' } }
```


### <a name="step-4-submit-an-azure-batch-job"></a><span data-ttu-id="4b5bd-171">Etapa 4: envio de um trabalho de lote do Azure</span><span class="sxs-lookup"><span data-stu-id="4b5bd-171">Step 4: Submit an Azure Batch job</span></span>
<span data-ttu-id="4b5bd-172">Um trabalho de lote do Azure é um grupo lógico de tarefas semelhantes.</span><span class="sxs-lookup"><span data-stu-id="4b5bd-172">An Azure Batch job is a logical group of similar tasks.</span></span> <span data-ttu-id="4b5bd-173">Em nosso cenário, é "Csv de processo tooJSON".</span><span class="sxs-lookup"><span data-stu-id="4b5bd-173">In our scenario, it is "Process csv tooJSON."</span></span> <span data-ttu-id="4b5bd-174">Cada uma dessas tarefas poderia processar arquivos CSV presentes nos contêineres de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="4b5bd-174">Each task here could be processing csv files present in each Azure Storage container.</span></span>

<span data-ttu-id="4b5bd-175">Essas tarefas seriam executado em paralelo e implantados em vários nós, orquestrados pelo serviço de lote do Azure hello.</span><span class="sxs-lookup"><span data-stu-id="4b5bd-175">These tasks would run in parallel and deployed across multiple nodes, orchestrated by hello Azure Batch service.</span></span>

> [!Tip]
> <span data-ttu-id="4b5bd-176">Você pode usar o hello [maxTasksPerNode](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/Pool.html#add) número máximo de tarefas que podem ser executados simultaneamente em um único nó toospecify propriedades.</span><span class="sxs-lookup"><span data-stu-id="4b5bd-176">You can use hello [maxTasksPerNode](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/Pool.html#add) property toospecify maximum number of tasks that can run concurrently on a single node.</span></span>
>
>

#### <a name="preparation-task"></a><span data-ttu-id="4b5bd-177">Tarefa de preparação</span><span class="sxs-lookup"><span data-stu-id="4b5bd-177">Preparation task</span></span>

<span data-ttu-id="4b5bd-178">nós VM Olá criados são nós de Ubuntu em branco.</span><span class="sxs-lookup"><span data-stu-id="4b5bd-178">hello VM nodes created are blank Ubuntu nodes.</span></span> <span data-ttu-id="4b5bd-179">Geralmente, você precisa tooinstall um conjunto de programas como pré-requisitos.</span><span class="sxs-lookup"><span data-stu-id="4b5bd-179">Often, you need tooinstall a set of programs as prerequisites.</span></span>
<span data-ttu-id="4b5bd-180">Normalmente, para nós do Linux, você pode ter um script de shell que instala pré-requisitos Olá antes das tarefas real Olá executar.</span><span class="sxs-lookup"><span data-stu-id="4b5bd-180">Typically, for Linux nodes you can have a shell script that installs hello prerequisites before hello actual tasks run.</span></span> <span data-ttu-id="4b5bd-181">No entanto, pode ser qualquer executável programável.</span><span class="sxs-lookup"><span data-stu-id="4b5bd-181">However it could be any programmable executable.</span></span>
<span data-ttu-id="4b5bd-182">Olá [script de shell](https://github.com/shwetams/azure-batchclient-sample-nodejs/blob/master/startup_prereq.sh) neste exemplo instala pip Python e hello Azure Storage SDK para Python.</span><span class="sxs-lookup"><span data-stu-id="4b5bd-182">hello [shell script](https://github.com/shwetams/azure-batchclient-sample-nodejs/blob/master/startup_prereq.sh) in this example installs Python-pip and hello Azure Storage SDK for Python.</span></span>

<span data-ttu-id="4b5bd-183">Você pode carregar o script hello em uma conta de armazenamento do Azure e gerar um script de saudação tooaccess URI SAS.</span><span class="sxs-lookup"><span data-stu-id="4b5bd-183">You can upload hello script on an Azure Storage Account and generate a SAS URI tooaccess hello script.</span></span> <span data-ttu-id="4b5bd-184">Esse processo também pode ser automatizado usando hello Azure Storage Node. js SDK.</span><span class="sxs-lookup"><span data-stu-id="4b5bd-184">This process can also be automated using hello Azure Storage Node.js SDK.</span></span>

> [!Tip]
> <span data-ttu-id="4b5bd-185">Uma tarefa de preparação de um trabalho é executado apenas em nós VM Olá onde a tarefa específica Olá precisa toorun.</span><span class="sxs-lookup"><span data-stu-id="4b5bd-185">A preparation task for a job runs only on hello VM nodes where hello specific task needs toorun.</span></span> <span data-ttu-id="4b5bd-186">Se você quiser toobe pré-requisitos instalado em todos os nós independentemente tarefas Olá executadas nele, você pode usar o hello [startTask](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/Pool.html#add) propriedade durante a adição de um pool.</span><span class="sxs-lookup"><span data-stu-id="4b5bd-186">If you want prerequisites toobe installed on all nodes irrespective of hello tasks that run on it, you can use hello [startTask](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/Pool.html#add) property while adding a pool.</span></span> <span data-ttu-id="4b5bd-187">Você pode usar o hello após a definição de tarefa de preparação para referência.</span><span class="sxs-lookup"><span data-stu-id="4b5bd-187">You can use hello following preparation task definition for reference.</span></span>
>
>

<span data-ttu-id="4b5bd-188">Uma tarefa de preparação é especificada durante o envio de saudação do trabalho em lotes do Azure.</span><span class="sxs-lookup"><span data-stu-id="4b5bd-188">A preparation task is specified during hello submission of Azure Batch job.</span></span> <span data-ttu-id="4b5bd-189">A seguir são Olá parâmetros de configuração da tarefa de preparação:</span><span class="sxs-lookup"><span data-stu-id="4b5bd-189">Following are hello preparation task configuration parameters:</span></span>

* <span data-ttu-id="4b5bd-190">**ID**: um identificador exclusivo para a tarefa de preparação de saudação</span><span class="sxs-lookup"><span data-stu-id="4b5bd-190">**ID**: A unique identifier for hello preparation task</span></span>
* <span data-ttu-id="4b5bd-191">**linha de comando**: linha de comando tooexecute Olá executável da tarefa</span><span class="sxs-lookup"><span data-stu-id="4b5bd-191">**commandLine**: Command line tooexecute hello task executable</span></span>
* <span data-ttu-id="4b5bd-192">**resourceFiles**: matriz de objetos que fornecem detalhes dos arquivos necessários toobe baixado para toorun esta tarefa.</span><span class="sxs-lookup"><span data-stu-id="4b5bd-192">**resourceFiles**: Array of objects that provide details of files needed toobe downloaded for this task toorun.</span></span>  <span data-ttu-id="4b5bd-193">Seguem as suas opções</span><span class="sxs-lookup"><span data-stu-id="4b5bd-193">Following are its options</span></span>
    - <span data-ttu-id="4b5bd-194">blobSource: Olá SAS URI do arquivo hello</span><span class="sxs-lookup"><span data-stu-id="4b5bd-194">blobSource: hello SAS URI of hello file</span></span>
    - <span data-ttu-id="4b5bd-195">filePath: toodownload caminho Local e salve o arquivo hello</span><span class="sxs-lookup"><span data-stu-id="4b5bd-195">filePath: Local path toodownload and save hello file</span></span>
    - <span data-ttu-id="4b5bd-196">fileMode: aplicável somente para nós de Linux, o fileMode está em formato octal com um valor padrão de 0770</span><span class="sxs-lookup"><span data-stu-id="4b5bd-196">fileMode: Only applicable for Linux nodes, fileMode is in octal format with a default value of 0770</span></span>
* <span data-ttu-id="4b5bd-197">**waitForSuccess**: se o conjunto tootrue, tarefa Olá não é executado em falhas de tarefas de preparação</span><span class="sxs-lookup"><span data-stu-id="4b5bd-197">**waitForSuccess**: If set tootrue, hello task does not run on preparation task failures</span></span>
* <span data-ttu-id="4b5bd-198">**runElevated**: definir tootrue se privilégios elevados são tarefas de saudação toorun necessários.</span><span class="sxs-lookup"><span data-stu-id="4b5bd-198">**runElevated**: Set it tootrue if elevated privileges are needed toorun hello task.</span></span>

<span data-ttu-id="4b5bd-199">Trecho de código a seguir mostra um exemplo de configuração do hello preparação tarefa script:</span><span class="sxs-lookup"><span data-stu-id="4b5bd-199">Following code snippet shows hello preparation task script configuration sample:</span></span>

```nodejs
var job_prep_task_config = {id:"installprereq",commandLine:"sudo sh startup_prereq.sh > startup.log",resourceFiles:[{'blobSource':'Blob SAS URI','filePath':'startup_prereq.sh'}],waitForSuccess:true,runElevated:true}
```

<span data-ttu-id="4b5bd-200">Se não houver nenhum toobe pré-requisitos instalado para o toorun de tarefas, você poderá ignorar as tarefas de preparação de saudação.</span><span class="sxs-lookup"><span data-stu-id="4b5bd-200">If there are no prerequisites toobe installed for your tasks toorun, you can skip hello preparation tasks.</span></span> <span data-ttu-id="4b5bd-201">O código a seguir cria um trabalho cujo nome de exibição é "arquivos de CSV do processo."</span><span class="sxs-lookup"><span data-stu-id="4b5bd-201">Following code creates a job with display name "process csv files."</span></span>

 ```nodejs
 // Setting up Batch pool configuration
 var pool_config = {poolId:poolid}
 // Setting up Job configuration along with preparation task
 var jobId = "processcsvjob"
 var job_config = {id:jobId,displayName:"process csv files",jobPreparationTask:job_prep_task_config,poolInfo:pool_config}
 // Adding Azure batch job toohello pool
 var job = batch_client.job.add(job_config,function(error,result){
     if(error != null)
     {
         console.log("Error submitting job : " + error.response);
     }});
```


### <a name="step-5-submit-azure-batch-tasks-for-a-job"></a><span data-ttu-id="4b5bd-202">Etapa 5: enviar tarefas de lote do Azure para um trabalho</span><span class="sxs-lookup"><span data-stu-id="4b5bd-202">Step 5: Submit Azure Batch tasks for a job</span></span>

<span data-ttu-id="4b5bd-203">Depois de criar o trabalho de CSV do processo, vamos criar as tarefas para esse trabalho.</span><span class="sxs-lookup"><span data-stu-id="4b5bd-203">Now that our process csv job is created, let us create tasks for that job.</span></span> <span data-ttu-id="4b5bd-204">Supondo que temos quatro contêineres, temos toocreate quatro tarefas, uma para cada contêiner.</span><span class="sxs-lookup"><span data-stu-id="4b5bd-204">Assuming we have four containers, we have toocreate four tasks, one for each container.</span></span>

<span data-ttu-id="4b5bd-205">Se observarmos Olá [script Python](https://github.com/shwetams/azure-batchclient-sample-nodejs/blob/master/processcsv.py), ele aceita dois parâmetros:</span><span class="sxs-lookup"><span data-stu-id="4b5bd-205">If we look at hello [Python script](https://github.com/shwetams/azure-batchclient-sample-nodejs/blob/master/processcsv.py), it accepts two parameters:</span></span>

* <span data-ttu-id="4b5bd-206">nome do contêiner: Olá arquivos de toodownload de contêiner de armazenamento de</span><span class="sxs-lookup"><span data-stu-id="4b5bd-206">container name: hello Storage container toodownload files from</span></span>
* <span data-ttu-id="4b5bd-207">padrão: um parâmetro opcional do padrão de nome do arquivo</span><span class="sxs-lookup"><span data-stu-id="4b5bd-207">pattern: An optional parameter of file name pattern</span></span>

<span data-ttu-id="4b5bd-208">Supondo que temos quatro contêineres "con1", "con2", "con3", "con4" código a seguir mostra enviando para tarefas toohello Azure batch trabalho "processo csv" criado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="4b5bd-208">Assuming we have four containers "con1", "con2", "con3","con4" following code shows submitting for tasks toohello Azure batch job "process csv" we created earlier.</span></span>

```nodejs
// storing container names in an array
var container_list = ["con1","con2","con3","con4"]
    container_list.forEach(function(val,index){           

           var container_name = val;
           var taskID = container_name + "_process";
           var task_config = {id:taskID,displayName:'process csv in ' + container_name,commandLine:'python processcsv.py --container ' + container_name,resourceFiles:[{'blobSource':'<blob SAS URI>','filePath':'processcsv.py'}]}
           var task = batch_client.task.add(poolid,task_config,function(error,result){
                if(error != null)
                {
                    console.log(error.response);     
                }
                else
                {
                    console.log("Task for container : " + container_name + "submitted successfully");
                }



           });

    });
```

<span data-ttu-id="4b5bd-209">código de saudação adiciona o pool de toohello várias tarefas.</span><span class="sxs-lookup"><span data-stu-id="4b5bd-209">hello code adds multiple tasks toohello pool.</span></span> <span data-ttu-id="4b5bd-210">E cada uma das tarefas de saudação é executada em um nó no pool de saudação de máquinas virtuais criadas.</span><span class="sxs-lookup"><span data-stu-id="4b5bd-210">And each of hello tasks is executed on a node in hello pool of VMs created.</span></span> <span data-ttu-id="4b5bd-211">Se várias tarefas Olá excedem o número de saudação de VMs em uma propriedade de pool ou hello maxTasksPerNode, tarefas de saudação Aguarde até que um nó seja disponibilizado.</span><span class="sxs-lookup"><span data-stu-id="4b5bd-211">If hello number of tasks exceeds hello number of VMs in a pool or hello maxTasksPerNode property, hello tasks wait until a node is made available.</span></span> <span data-ttu-id="4b5bd-212">O lote do Azure lida com a orquestração automaticamente.</span><span class="sxs-lookup"><span data-stu-id="4b5bd-212">This orchestration is handled by Azure Batch automatically.</span></span>

<span data-ttu-id="4b5bd-213">portal de saudação tem detalhadas exibições em tarefas de saudação e status do trabalho.</span><span class="sxs-lookup"><span data-stu-id="4b5bd-213">hello portal has detailed views on hello tasks and job statuses.</span></span> <span data-ttu-id="4b5bd-214">Você também pode usar lista hello e obter funções na Olá SDK de nó do Azure.</span><span class="sxs-lookup"><span data-stu-id="4b5bd-214">You can also use hello list and get functions in hello Azure Node SDK.</span></span> <span data-ttu-id="4b5bd-215">Os detalhes são fornecidos na documentação de saudação [link](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/Job.html).</span><span class="sxs-lookup"><span data-stu-id="4b5bd-215">Details are provided in hello documentation [link](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/Job.html).</span></span>

## <a name="next-steps"></a><span data-ttu-id="4b5bd-216">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="4b5bd-216">Next steps</span></span>

- <span data-ttu-id="4b5bd-217">Saudação de revisão [recursos de visão geral do Azure Batch](batch-api-basics.md) artigo, que é recomendável que você confirme o novo serviço toohello.</span><span class="sxs-lookup"><span data-stu-id="4b5bd-217">Review hello [Overview of Azure Batch features](batch-api-basics.md) article, which we recommend if you're new toohello service.</span></span>
- <span data-ttu-id="4b5bd-218">Consulte Olá [referência lote Node. js](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/) tooexplore Olá API de lote.</span><span class="sxs-lookup"><span data-stu-id="4b5bd-218">See hello [Batch Node.js reference](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/) tooexplore hello Batch API.</span></span>

