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
# <a name="get-started-with-batch-sdk-for-nodejs"></a>Introdução ao SDK do lote para o Node.js

> [!div class="op_single_selector"]
> * [.NET](batch-dotnet-get-started.md)
> * [Python](batch-python-tutorial.md)
> * [Node.js](batch-nodejs-get-started.md)
>
>

Conheça os fundamentos de saudação da criação de um cliente em lotes usando Node. js [SDK de Node.js do Azure em lotes](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/). Podemos adotar uma abordagem passo a passo de compressão de um cenário para um aplicativo de lote e, em seguida, configurá-lo usando um cliente do Node.js.  

## <a name="prerequisites"></a>Pré-requisitos
Este artigo pressupõe que você tem um conhecimento prático do Node.js e que esteja familiarizado com o Linux. Ele também pressupõe que você tenha uma configuração de conta do Azure com serviços de armazenamento e de lote de toocreate de direitos do acesso.

Recomendamos a leitura [visão geral técnica do Azure Batch](batch-technical-overview.md) antes de passar por etapas Olá descritos neste artigo.

## <a name="hello-tutorial-scenario"></a>cenário do tutorial Olá
Vamos entenda o cenário de fluxo de trabalho em lotes hello. Temos um script simples escrito em Python downloads csv todos os arquivos a partir de um contêiner de armazenamento de BLOBs do Azure e converte-os tooJSON. tooprocess conta de armazenamento vários contêineres em paralelo, é possível implantar o script hello como um trabalho de lote do Azure.

## <a name="azure-batch-architecture"></a>Arquitetura de lote do Azure
Olá diagrama a seguir mostra como é possível dimensionar script de Python hello usando o lote do Azure e um cliente Node. js.

![Cenário de lote do Azure](./media/batch-nodejs-get-started/BatchScenario.png)

cliente de Node. js Olá implanta um trabalho em lotes com uma tarefa de preparação (explicado em detalhes mais tarde) e um conjunto de tarefas, dependendo do número de saudação de contêineres na conta de armazenamento hello. Você pode baixar os scripts de saudação do repositório do github hello.

* [Cliente Node.js](https://github.com/Azure/azure-batch-samples/blob/master/Node.js/GettingStarted/nodejs_batch_client_sample.js)
* [Shell scripts de tarefa de preparação](https://github.com/Azure/azure-batch-samples/blob/master/Node.js/GettingStarted/startup_prereq.sh)
* [Processador do Python csv tooJSON](https://github.com/Azure/azure-batch-samples/blob/master/Node.js/GettingStarted/processcsv.py)

> [!TIP]
> cliente Node. js Olá Olá link especificado não contém código específico toobe implantado como um aplicativo de função do Azure. Você pode consultar toohello seguindo os links para toocreate instruções um.
> - [Como criar um aplicativo de função](../azure-functions/functions-create-first-azure-function.md)
> - [Como criar uma função de gatilho de temporizador](../azure-functions/functions-bindings-timer.md)
>
>

## <a name="build-hello-application"></a>Criar um aplicativo hello

Agora, vamos siga o processo de Olá passo a passo na criação de cliente do Node. js hello:

### <a name="step-1-install-azure-batch-sdk"></a>Etapa 1: instalação o SDK do lote do Azure

Você pode instalar o SDK do lote do Azure para Node.js usando o comando Olá npm install.

`npm install azure-batch`

Esse comando instala a versão mais recente de saudação do nó de lote do azure SDK.

>[!Tip]
> Em um aplicativo de função do Azure, você pode ir muito o "Console de Kudu" hello Azure função configurações guia toorun Olá npm comandos de instalação. Nesse caso tooinstall SDK de lote do Azure para Node.js.
>
>

### <a name="step-2-create-an-azure-batch-account"></a>Etapa 2: criação uma conta de lote do Azure

Você pode criá-la de saudação [portal do Azure](batch-account-create-portal.md) ou da linha de comando ([Powershell](batch-powershell-cmdlets-get-started.md) /[cli do Azure](https://docs.microsoft.com/cli/azure/overview)).

A seguir é Olá comandos toocreate um por meio de CLI do Azure.

Criar um grupo de recursos, ignore esta etapa se você já tiver um onde você deseja toocreate Olá conta do lote:

`az group create -n "<resource-group-name>" -l "<location>"`

Em seguida, crie uma conta de lote do Azure.

`az batch account create -l "<location>"  -g "<resource-group-name>" -n "<batch-account-name>"`

Cada conta de lote tem suas chaves de acesso correspondentes. Essas chaves são toocreate necessários mais recursos na conta do lote do Azure. Uma prática recomendada para o ambiente de produção é toouse Azure Key Vault toostore essas chaves. Em seguida, você pode criar um serviço principal para o aplicativo hello. Usar este aplicativo de serviço principal Olá pode criar um chaves de tooaccess token OAuth do Cofre de chave hello.

`az batch account keys list -g "<resource-group-name>" -n "<batch-account-name>"`

Copie e armazene Olá toobe chave usado nas etapas subsequentes hello.

### <a name="step-3-create-an-azure-batch-service-client"></a>Etapa 3: criação um cliente de serviço de lote do Azure
Trecho de código a seguir primeiro importa o módulo de Node.js do azure batch hello e, em seguida, cria um cliente de serviço de lote. Você precisa toofirst criar um objeto SharedKeyCredentials com chave de conta em lotes Olá copiado da etapa anterior hello.

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

Olá URI do lote do Azure pode ser encontrada no guia de visão geral de saudação do hello portal do Azure. Ela é do formato de saudação:

`https://accountname.location.batch.azure.com`

Consulte a captura de tela de toohello:

![URI de lote do Azure](./media/batch-nodejs-get-started/azurebatchuri.png)



### <a name="step-4-create-an-azure-batch-pool"></a>Etapa 4: criação de um pool de lote do Azure
Um pool de lote do Azure consiste em várias VMs (também conhecidos como nós de lote). Serviço de lote do Azure implanta tarefas Olá em nós e os gerencia. Você pode definir Olá seguindo os parâmetros de configuração para o pool.

* Tipo de imagem da máquina virtual
* Tamanho dos nós da máquina virtual
* Número de nós da máquina virtual

> [!Tip]
> tamanho de saudação e o número de nós de máquina Virtual dependem em número de saudação de tarefas que deseja toorun em paralelo e também própria tarefa hello. Recomendamos que você teste toodetermine Olá ideal número e tamanho.
>
>

Olá trecho de código a seguir cria Olá objetos de parâmetro de configuração.

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
> Para Olá lista de imagens de VM do Linux disponíveis para o lote do Azure e seus IDs de SKU, consulte [lista de imagens de máquinas virtuais](batch-linux-nodes.md#list-of-virtual-machine-images).
>
>

Após a definição de configuração do pool Olá, você pode criar pool de lote do Azure hello. Olá comando de pool de lote cria nós de máquina Virtual do Azure e prepara-los toobe tooreceive pronto tarefas tooexecute. Cada pool deve ter um ID exclusivo para referência em etapas subsequentes.

saudação de trecho de código a seguir cria um pool de lote do Azure.

```nodejs
// Create a unique Azure Batch pool ID
var poolid = "pool" + customerDetails.customerid;
var poolConfig = {id:poolid, displayName:poolid,vmSize:vmSize,virtualMachineConfiguration:vmconfig,targetDedicatedComputeNodes:numVms,enableAutoScale:false };
// Creating hello Pool for hello specific customer
var pool = batch_client.pool.add(poolConfig,function(error,result){
    if(error!=null){console.log(error.response)};
});
```

Você pode verificar o status Olá Olá pool criado e verifique se o estado de saudação está em "ativo" antes de prosseguir com o envio de um pool de toothat de trabalho.

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

A seguir é um objeto de resultado de exemplo retornado pela função de pool.get hello.

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


### <a name="step-4-submit-an-azure-batch-job"></a>Etapa 4: envio de um trabalho de lote do Azure
Um trabalho de lote do Azure é um grupo lógico de tarefas semelhantes. Em nosso cenário, é "Csv de processo tooJSON". Cada uma dessas tarefas poderia processar arquivos CSV presentes nos contêineres de armazenamento do Azure.

Essas tarefas seriam executado em paralelo e implantados em vários nós, orquestrados pelo serviço de lote do Azure hello.

> [!Tip]
> Você pode usar o hello [maxTasksPerNode](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/Pool.html#add) número máximo de tarefas que podem ser executados simultaneamente em um único nó toospecify propriedades.
>
>

#### <a name="preparation-task"></a>Tarefa de preparação

nós VM Olá criados são nós de Ubuntu em branco. Geralmente, você precisa tooinstall um conjunto de programas como pré-requisitos.
Normalmente, para nós do Linux, você pode ter um script de shell que instala pré-requisitos Olá antes das tarefas real Olá executar. No entanto, pode ser qualquer executável programável.
Olá [script de shell](https://github.com/shwetams/azure-batchclient-sample-nodejs/blob/master/startup_prereq.sh) neste exemplo instala pip Python e hello Azure Storage SDK para Python.

Você pode carregar o script hello em uma conta de armazenamento do Azure e gerar um script de saudação tooaccess URI SAS. Esse processo também pode ser automatizado usando hello Azure Storage Node. js SDK.

> [!Tip]
> Uma tarefa de preparação de um trabalho é executado apenas em nós VM Olá onde a tarefa específica Olá precisa toorun. Se você quiser toobe pré-requisitos instalado em todos os nós independentemente tarefas Olá executadas nele, você pode usar o hello [startTask](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/Pool.html#add) propriedade durante a adição de um pool. Você pode usar o hello após a definição de tarefa de preparação para referência.
>
>

Uma tarefa de preparação é especificada durante o envio de saudação do trabalho em lotes do Azure. A seguir são Olá parâmetros de configuração da tarefa de preparação:

* **ID**: um identificador exclusivo para a tarefa de preparação de saudação
* **linha de comando**: linha de comando tooexecute Olá executável da tarefa
* **resourceFiles**: matriz de objetos que fornecem detalhes dos arquivos necessários toobe baixado para toorun esta tarefa.  Seguem as suas opções
    - blobSource: Olá SAS URI do arquivo hello
    - filePath: toodownload caminho Local e salve o arquivo hello
    - fileMode: aplicável somente para nós de Linux, o fileMode está em formato octal com um valor padrão de 0770
* **waitForSuccess**: se o conjunto tootrue, tarefa Olá não é executado em falhas de tarefas de preparação
* **runElevated**: definir tootrue se privilégios elevados são tarefas de saudação toorun necessários.

Trecho de código a seguir mostra um exemplo de configuração do hello preparação tarefa script:

```nodejs
var job_prep_task_config = {id:"installprereq",commandLine:"sudo sh startup_prereq.sh > startup.log",resourceFiles:[{'blobSource':'Blob SAS URI','filePath':'startup_prereq.sh'}],waitForSuccess:true,runElevated:true}
```

Se não houver nenhum toobe pré-requisitos instalado para o toorun de tarefas, você poderá ignorar as tarefas de preparação de saudação. O código a seguir cria um trabalho cujo nome de exibição é "arquivos de CSV do processo."

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


### <a name="step-5-submit-azure-batch-tasks-for-a-job"></a>Etapa 5: enviar tarefas de lote do Azure para um trabalho

Depois de criar o trabalho de CSV do processo, vamos criar as tarefas para esse trabalho. Supondo que temos quatro contêineres, temos toocreate quatro tarefas, uma para cada contêiner.

Se observarmos Olá [script Python](https://github.com/shwetams/azure-batchclient-sample-nodejs/blob/master/processcsv.py), ele aceita dois parâmetros:

* nome do contêiner: Olá arquivos de toodownload de contêiner de armazenamento de
* padrão: um parâmetro opcional do padrão de nome do arquivo

Supondo que temos quatro contêineres "con1", "con2", "con3", "con4" código a seguir mostra enviando para tarefas toohello Azure batch trabalho "processo csv" criado anteriormente.

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

código de saudação adiciona o pool de toohello várias tarefas. E cada uma das tarefas de saudação é executada em um nó no pool de saudação de máquinas virtuais criadas. Se várias tarefas Olá excedem o número de saudação de VMs em uma propriedade de pool ou hello maxTasksPerNode, tarefas de saudação Aguarde até que um nó seja disponibilizado. O lote do Azure lida com a orquestração automaticamente.

portal de saudação tem detalhadas exibições em tarefas de saudação e status do trabalho. Você também pode usar lista hello e obter funções na Olá SDK de nó do Azure. Os detalhes são fornecidos na documentação de saudação [link](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/Job.html).

## <a name="next-steps"></a>Próximas etapas

- Saudação de revisão [recursos de visão geral do Azure Batch](batch-api-basics.md) artigo, que é recomendável que você confirme o novo serviço toohello.
- Consulte Olá [referência lote Node. js](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/) tooexplore Olá API de lote.

