---
title: aplicativo de aaaWeb com armazenamento de tabela (Node. js) | Microsoft Docs
description: "Um tutorial que amplia Olá aplicativo Web com o tutorial Express adicionando Olá módulo do Azure e serviços de armazenamento do Azure."
services: cosmos-db
documentationcenter: nodejs
author: mimig1
manager: jhubbard
editor: tysonn
ms.assetid: e90959a2-4cb2-4b19-9bfb-aede15b18b1c
ms.service: cosmos-db
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 12/08/2016
ms.author: mimig
ms.openlocfilehash: 7eefc09baab61cf44c98183135abe572b11812e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="nodejs-web-application-using-storage"></a><span data-ttu-id="7785b-103">Aplicativo Web do Node.js usando Armazenamento</span><span class="sxs-lookup"><span data-stu-id="7785b-103">Node.js Web Application using Storage</span></span>
## <a name="overview"></a><span data-ttu-id="7785b-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="7785b-104">Overview</span></span>
<span data-ttu-id="7785b-105">Neste tutorial, Olá aplicativo criado no [aplicativo de Web Node.js usando Express] tutorial é estendido usando Olá bibliotecas de cliente do Microsoft Azure para Node.js toowork com serviços de gerenciamento de dados.</span><span class="sxs-lookup"><span data-stu-id="7785b-105">In this tutorial, hello application you created in the [Node.js Web Application using Express] tutorial is extended using hello Microsoft Azure Client Libraries for Node.js toowork with data management services.</span></span> <span data-ttu-id="7785b-106">Você pode estender o aplicativo, criando um aplicativo baseado na web-lista de tarefas que você pode implantar tooAzure.</span><span class="sxs-lookup"><span data-stu-id="7785b-106">You extend your application by creating a web-based task-list application that you can deploy tooAzure.</span></span> <span data-ttu-id="7785b-107">lista de tarefas Olá permite que um usuário recuperar tarefas, adicionar novas tarefas e marcar tarefas como concluídas.</span><span class="sxs-lookup"><span data-stu-id="7785b-107">hello task list allows a user to retrieve tasks, add new tasks, and mark tasks as completed.</span></span>

<span data-ttu-id="7785b-108">itens de tarefa Olá são armazenados no armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="7785b-108">hello task items are stored in Azure Storage.</span></span> <span data-ttu-id="7785b-109">O Armazenamento do Azure fornece um armazenamento de dados não estruturado altamente disponível e tolerante a falhas.</span><span class="sxs-lookup"><span data-stu-id="7785b-109">Azure Storage provides unstructured data storage that is fault-tolerant and highly available.</span></span> <span data-ttu-id="7785b-110">O Armazenamento do Azure inclui várias estruturas de dados nas quais você pode armazenar e acessar dados.</span><span class="sxs-lookup"><span data-stu-id="7785b-110">Azure Storage includes several data structures where you can store and access data.</span></span> <span data-ttu-id="7785b-111">Você pode usar os serviços de armazenamento de saudação do hello APIs incluídas hello Azure SDK para Node.js ou por meio de APIs REST.</span><span class="sxs-lookup"><span data-stu-id="7785b-111">You can use hello storage services from hello APIs included in hello Azure SDK for Node.js or via REST APIs.</span></span> <span data-ttu-id="7785b-112">Para saber mais, veja [Armazenando e acessando dados no Azure].</span><span class="sxs-lookup"><span data-stu-id="7785b-112">For more information, see [Storing and Accessing Data in Azure].</span></span>

<span data-ttu-id="7785b-113">Este tutorial presume que você tenha concluído Olá [aplicativo Web Node.js] e [Node. js Express][aplicativo de Web Node.js usando Express] tutoriais.</span><span class="sxs-lookup"><span data-stu-id="7785b-113">This tutorial assumes that you have completed hello [Node.js Web Application] and [Node.js with Express][Node.js Web Application using Express] tutorials.</span></span>

<span data-ttu-id="7785b-114">Ele contém Olá informações a seguir:</span><span class="sxs-lookup"><span data-stu-id="7785b-114">It contains hello following information:</span></span>

* <span data-ttu-id="7785b-115">Como toowork com hello mecanismo de modelo Jade</span><span class="sxs-lookup"><span data-stu-id="7785b-115">How toowork with hello Jade template engine</span></span>
* <span data-ttu-id="7785b-116">Como toowork com serviços de gerenciamento de dados do Azure</span><span class="sxs-lookup"><span data-stu-id="7785b-116">How toowork with Azure Data Management services</span></span>

<span data-ttu-id="7785b-117">Olá captura de tela a seguir mostra um aplicativo hello concluída:</span><span class="sxs-lookup"><span data-stu-id="7785b-117">hello following screenshot shows hello completed application:</span></span>

![Olá concluída a página da web no internet explorer](./media/table-storage-cloud-service-nodejs/getting-started-1.png)

## <a name="setting-storage-credentials-in-webconfig"></a><span data-ttu-id="7785b-119">Definindo credenciais de armazenamento em Web.Config</span><span class="sxs-lookup"><span data-stu-id="7785b-119">Setting Storage Credentials in Web.Config</span></span>
<span data-ttu-id="7785b-120">Você deve passar credenciais de armazenamento tooaccess armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="7785b-120">You must pass in storage credentials tooaccess Azure Storage.</span></span> <span data-ttu-id="7785b-121">Isso é feito com o uso de configurações do aplicativo Web. config Olá.</span><span class="sxs-lookup"><span data-stu-id="7785b-121">This is done by utilizing hello web.config application settings.</span></span>
<span data-ttu-id="7785b-122">configurações de Web. config Olá são passadas como tooNode de variáveis de ambiente, que são então lidos pelo Olá SDK do Azure.</span><span class="sxs-lookup"><span data-stu-id="7785b-122">hello web.config settings are passed as environment variables tooNode, which are then read by hello Azure SDK.</span></span>

> [!NOTE]
> <span data-ttu-id="7785b-123">As credenciais de armazenamento são usadas somente quando o aplicativo hello é tooAzure implantado.</span><span class="sxs-lookup"><span data-stu-id="7785b-123">Storage credentials are only used when hello application is deployed tooAzure.</span></span> <span data-ttu-id="7785b-124">Quando em execução no emulador hello, aplicativo hello usa o emulador de armazenamento hello.</span><span class="sxs-lookup"><span data-stu-id="7785b-124">When running in hello emulator, hello application uses hello storage emulator.</span></span>
>
>

<span data-ttu-id="7785b-125">Executar Olá seguintes credenciais de conta de armazenamento etapas tooretrieve hello e adicioná-los toohello configurações de Web. config:</span><span class="sxs-lookup"><span data-stu-id="7785b-125">Perform hello following steps tooretrieve hello storage account credentials and add them toohello web.config settings:</span></span>

1. <span data-ttu-id="7785b-126">Se ainda não estiver aberto, inicie hello Azure PowerShell de saudação **iniciar** menu expandindo **todos os programas, o Azure**, clique com botão direito **Azure PowerShell**e, em seguida, selecione  **Executar como administrador**.</span><span class="sxs-lookup"><span data-stu-id="7785b-126">If it is not already open, start hello Azure PowerShell from hello **Start** menu by expanding **All Programs, Azure**, right-click **Azure PowerShell**, and then select **Run As Administrator**.</span></span>
2. <span data-ttu-id="7785b-127">Alterar diretórios toohello pasta que contém seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="7785b-127">Change directories toohello folder containing your application.</span></span> <span data-ttu-id="7785b-128">Por exemplo, C:\\node\\tasklist\\WebRole1.</span><span class="sxs-lookup"><span data-stu-id="7785b-128">For example, C:\\node\\tasklist\\WebRole1.</span></span>
3. <span data-ttu-id="7785b-129">Na janela do Powershell do Azure hello, digite Olá informações de conta de armazenamento do cmdlet tooretrieve Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="7785b-129">From hello Azure Powershell window, enter hello following cmdlet tooretrieve hello storage account information:</span></span>

    ```powershell
    PS C:\node\tasklist\WebRole1> Get-AzureStorageAccounts
    ```

   <span data-ttu-id="7785b-130">Olá, cmdlet anterior recupera Olá lista de contas de armazenamento e chaves de conta associadas ao seu serviço hospedado.</span><span class="sxs-lookup"><span data-stu-id="7785b-130">hello preceding cmdlet retrieves hello list of storage accounts and account keys associated with your hosted service.</span></span>

   > [!NOTE]
   > <span data-ttu-id="7785b-131">Como Olá SDK do Azure cria uma conta de armazenamento ao implantar um serviço, uma conta de armazenamento já deve existir de implantar seu aplicativo em guias de saudação anterior.</span><span class="sxs-lookup"><span data-stu-id="7785b-131">Since hello Azure SDK creates a storage account when you deploy a service, a storage account should already exist from deploying your application in hello previous guides.</span></span>
   >
   >
4. <span data-ttu-id="7785b-132">Olá abrir **servicedefinition. Csdef** arquivo que contém configurações de ambiente de hello são usadas quando o aplicativo hello é tooAzure implantado:</span><span class="sxs-lookup"><span data-stu-id="7785b-132">Open hello **ServiceDefinition.csdef** file containing hello environment settings that are used when hello application is deployed tooAzure:</span></span>

    ```powershell
    PS C:\node\tasklist> notepad ServiceDefinition.csdef
    ```

5. <span data-ttu-id="7785b-133">Bloquear a seguir Olá INSERT em **ambiente** elemento, substituindo a {conta de armazenamento} e {chave de acesso de armazenamento} com o nome da conta de saudação e a chave primária Olá Olá conta de armazenamento você deseja toouse para implantação:</span><span class="sxs-lookup"><span data-stu-id="7785b-133">Insert hello following block under **Environment** element, substituting {STORAGE ACCOUNT} and {STORAGE ACCESS KEY} with hello account name and hello primary key for hello storage account you want toouse for deployment:</span></span>

  <Variable name="AZURE_STORAGE_ACCOUNT" value="{STORAGE ACCOUNT}" />
  <Variable name="AZURE_STORAGE_ACCESS_KEY" value="{STORAGE ACCESS KEY}" />

   ![conteúdo do arquivo Hello web.cloud.config](./media/table-storage-cloud-service-nodejs/node37.png)

6. <span data-ttu-id="7785b-135">Salve o arquivo hello e feche o bloco de notas.</span><span class="sxs-lookup"><span data-stu-id="7785b-135">Save hello file and close notepad.</span></span>

### <a name="install-additional-modules"></a><span data-ttu-id="7785b-136">Instalar módulos adicionais</span><span class="sxs-lookup"><span data-stu-id="7785b-136">Install additional modules</span></span>
1. <span data-ttu-id="7785b-137">Saudação de uso após a saudação de tooinstall de comando [azure], [nó uuid], [nconf] e [assíncrono] módulos localmente, bem como toosave uma entrada para eles toohello **Package. JSON** arquivo:</span><span class="sxs-lookup"><span data-stu-id="7785b-137">Use hello following command tooinstall hello [azure], [node-uuid], [nconf] and [async] modules locally as well as toosave an entry for them toohello **package.json** file:</span></span>

  ```powershell
  PS C:\node\tasklist\WebRole1> npm install azure-storage node-uuid async nconf --save
  ```

  <span data-ttu-id="7785b-138">saída de Hello desse comando deve aparecer a seguir toohello semelhante:</span><span class="sxs-lookup"><span data-stu-id="7785b-138">hello output of this command should appear similar toohello following:</span></span>

  ```
  node-uuid@1.4.1 node_modules\node-uuid

  nconf@0.6.9 node_modules\nconf
  ├── ini@1.1.0
  ├── async@0.2.9
  └── optimist@0.6.0 (wordwrap@0.0.2, minimist@0.0.8)

  azure-storage@0.1.0 node_modules\azure-storage
  ├── extend@1.2.1
  ├── xmlbuilder@0.4.3
  ├── mime@1.2.11
  ├── underscore@1.4.4
  ├── validator@3.1.0
  ├── node-uuid@1.4.1
  ├── xml2js@0.2.7 (sax@0.5.2)
  └── request@2.27.0 (json-stringify-safe@5.0.0, tunnel-agent@0.3.0, aws-sign@0.3.0, forever-agent@0.5.2, qs@0.6.6, oauth-sign@0.3.0, cookie-jar@0.3.0, hawk@1.0.0, form-data@0.1.3, http-signature@0.10.0)
  ```

## <a name="using-hello-table-service-in-a-node-application"></a><span data-ttu-id="7785b-139">Usando o serviço de tabela de saudação em um aplicativo de nó</span><span class="sxs-lookup"><span data-stu-id="7785b-139">Using hello Table service in a node application</span></span>
<span data-ttu-id="7785b-140">Nesta seção, Olá aplicativo básico criado pelo Olá **express** comando é estendido pela adição de um **task.js** arquivo que contém o modelo de saudação para suas tarefas.</span><span class="sxs-lookup"><span data-stu-id="7785b-140">In this section, hello basic application created by hello **express** command is extended by adding a **task.js** file containing hello model for your tasks.</span></span> <span data-ttu-id="7785b-141">Modificar Olá existente **app.js** de arquivo e criar um novo **tasklist.js** arquivo que usa o modelo de saudação.</span><span class="sxs-lookup"><span data-stu-id="7785b-141">Modify hello existing **app.js** file and create a new **tasklist.js** file that uses hello model.</span></span>

### <a name="create-hello-model"></a><span data-ttu-id="7785b-142">Criar modelo Olá</span><span class="sxs-lookup"><span data-stu-id="7785b-142">Create hello model</span></span>
1. <span data-ttu-id="7785b-143">Em Olá **WebRole1** diretório, crie um novo diretório chamado **modelos**.</span><span class="sxs-lookup"><span data-stu-id="7785b-143">In hello **WebRole1** directory, create a new directory named **models**.</span></span>
2. <span data-ttu-id="7785b-144">Em Olá **modelos** diretório, crie um novo arquivo chamado **task.js**.</span><span class="sxs-lookup"><span data-stu-id="7785b-144">In hello **models** directory, create a new file named **task.js**.</span></span> <span data-ttu-id="7785b-145">Este arquivo contém o modelo Olá Olá tarefas criados pelo seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="7785b-145">This file contains hello model for hello tasks created by your application.</span></span>
3. <span data-ttu-id="7785b-146">Início de saudação do hello **task.js** de arquivo, adicione Olá bibliotecas tooreference necessárias de código a seguir:</span><span class="sxs-lookup"><span data-stu-id="7785b-146">At hello beginning of hello **task.js** file, add hello following code tooreference required libraries:</span></span>

    ```nodejs
    var azure = require('azure-storage');
    var uuid = require('node-uuid');
    var entityGen = azure.TableUtilities.entityGenerator;
    ```

4. <span data-ttu-id="7785b-147">Em seguida, adicione código toodefine e exportar o objeto de tarefa hello.</span><span class="sxs-lookup"><span data-stu-id="7785b-147">Next, add code toodefine and export hello Task object.</span></span> <span data-ttu-id="7785b-148">objeto de tarefa Olá é responsável por conectar-se a tabela de toohello.</span><span class="sxs-lookup"><span data-stu-id="7785b-148">hello Task object is responsible for connecting toohello table.</span></span>

    ```nodejs
    module.exports = Task;

    function Task(storageClient, tableName, partitionKey) {
      this.storageClient = storageClient;
      this.tableName = tableName;
      this.partitionKey = partitionKey;
      this.storageClient.createTableIfNotExists(tableName, function tableCreated(error) {
        if(error) {
          throw error;
        }
      });
    };
    ```

5. <span data-ttu-id="7785b-149">Em seguida, adicione Olá métodos adicionais de toodefine de código a seguir em objeto de tarefa hello, que permitem que as interações com os dados armazenados na tabela de saudação:</span><span class="sxs-lookup"><span data-stu-id="7785b-149">Next, add hello following code toodefine additional methods on hello Task object, which allow interactions with data stored in hello table:</span></span>

    ```nodejs
    Task.prototype = {
      find: function(query, callback) {
        self = this;
        self.storageClient.queryEntities(query, function entitiesQueried(error, result) {
          if(error) {
            callback(error);
          } else {
            callback(null, result.entries);
          }
        });
      },

      addItem: function(item, callback) {
        self = this;
        // use entityGenerator tooset types
        // NOTE: RowKey must be a string type, even though
        // it contains a GUID in this example.
        var itemDescriptor = {
          PartitionKey: entityGen.String(self.partitionKey),
          RowKey: entityGen.String(uuid()),
          name: entityGen.String(item.name),
          category: entityGen.String(item.category),
          completed: entityGen.Boolean(false)
        };

        self.storageClient.insertEntity(self.tableName, itemDescriptor, function entityInserted(error) {
          if(error){
            callback(error);
          }
          callback(null);
        });
      },

      updateItem: function(rKey, callback) {
        self = this;
        self.storageClient.retrieveEntity(self.tableName, self.partitionKey, rKey, function entityQueried(error, entity) {
          if(error) {
            callback(error);
          }
          entity.completed._ = true;
          self.storageClient.updateEntity(self.tableName, entity, function entityUpdated(error) {
            if(error) {
              callback(error);
            }
            callback(null);
          });
        });
      }
    }
    ```

6. <span data-ttu-id="7785b-150">Salve e feche o hello **task.js** arquivo.</span><span class="sxs-lookup"><span data-stu-id="7785b-150">Save and close hello **task.js** file.</span></span>

### <a name="create-hello-controller"></a><span data-ttu-id="7785b-151">Criar hello controlador</span><span class="sxs-lookup"><span data-stu-id="7785b-151">Create hello controller</span></span>
1. <span data-ttu-id="7785b-152">Em Olá **WebRole1/rotas** diretório, crie um novo arquivo chamado **tasklist.js** e abri-lo em um editor de texto.</span><span class="sxs-lookup"><span data-stu-id="7785b-152">In hello **WebRole1/routes** directory, create a new file named **tasklist.js** and open it in a text editor.</span></span>
2. <span data-ttu-id="7785b-153">Adicionar Olá código a seguir muito**tasklist.js**.</span><span class="sxs-lookup"><span data-stu-id="7785b-153">Add hello following code too**tasklist.js**.</span></span> <span data-ttu-id="7785b-154">Esse código carrega hello azure e módulos assíncrono, que são usados pelo **tasklist.js** e define Olá **TaskList** função, que é passada a uma instância de saudação **tarefa** nós de objeto definido anteriormente:</span><span class="sxs-lookup"><span data-stu-id="7785b-154">This code loads hello azure and async modules, which are used by **tasklist.js** and defines hello **TaskList** function, which is passed an instance of hello **Task** object we defined earlier:</span></span>

    ```nodejs
    var azure = require('azure-storage');
    var async = require('async');

    module.exports = TaskList;

    function TaskList(task) {
      this.task = task;
    }
    ```

3. <span data-ttu-id="7785b-155">Continue adicionando toohello **tasklist.js** arquivo adicionando métodos de saudação usados muito**showTasks**, **addTask**, e **completeTasks**:</span><span class="sxs-lookup"><span data-stu-id="7785b-155">Continue adding toohello **tasklist.js** file by adding hello methods used too**showTasks**, **addTask**, and **completeTasks**:</span></span>

    ```nodejs
    TaskList.prototype = {
      showTasks: function(req, res) {
        self = this;
        var query = azure.TableQuery()
          .where('completed eq ?', false);
        self.task.find(query, function itemsFound(error, items) {
          res.render('index',{title: 'My ToDo List ', tasks: items});
        });
      },

      addTask: function(req,res) {
        var self = this
        var item = req.body.item;
        self.task.addItem(item, function itemAdded(error) {
          if(error) {
            throw error;
          }
          res.redirect('/');
        });
      },

      completeTask: function(req,res) {
        var self = this;
        var completedTasks = Object.keys(req.body);
        async.forEach(completedTasks, function taskIterator(completedTask, callback) {
          self.task.updateItem(completedTask, function itemsUpdated(error) {
            if(error){
              callback(error);
            } else {
              callback(null);
            }
          });
        }, function goHome(error){
          if(error) {
            throw error;
          } else {
            res.redirect('/');
          }
        });
      }
    }
    ```

4. <span data-ttu-id="7785b-156">Salvar Olá **tasklist.js** arquivo.</span><span class="sxs-lookup"><span data-stu-id="7785b-156">Save hello **tasklist.js** file.</span></span>

### <a name="modify-appjs"></a><span data-ttu-id="7785b-157">Modificar app.js</span><span class="sxs-lookup"><span data-stu-id="7785b-157">Modify app.js</span></span>
1. <span data-ttu-id="7785b-158">Em Olá **WebRole1** Olá diretório, abra **app.js** em um editor de texto.</span><span class="sxs-lookup"><span data-stu-id="7785b-158">In hello **WebRole1** directory, open hello **app.js** file in a text editor.</span></span>
2. <span data-ttu-id="7785b-159">No início de saudação do arquivo hello, adicione Olá módulo de saudação do azure tooload a seguir e defina a chave de nome e a partição da tabela de saudação:</span><span class="sxs-lookup"><span data-stu-id="7785b-159">At hello beginning of hello file, add hello following tooload hello azure module and set hello table name and partition key:</span></span>

    ```nodejs
    var azure = require('azure-storage');
    var tableName = 'tasks';
    var partitionKey = 'hometasks';
    ```

3. <span data-ttu-id="7785b-160">No arquivo de app.js hello, role para baixo toowhere você ver Olá linha a seguir:</span><span class="sxs-lookup"><span data-stu-id="7785b-160">In hello app.js file, scroll down toowhere you see hello following line:</span></span>

    ```nodejs
    app.use('/', routes);
    app.use('/users', users);
    ```

    <span data-ttu-id="7785b-161">Substitua saudação precedendo linhas com hello código a seguir.</span><span class="sxs-lookup"><span data-stu-id="7785b-161">Replace hello preceding lines with hello following code.</span></span> <span data-ttu-id="7785b-162">Esse código inicializa uma instância de <strong>tarefa</strong> com uma conta de armazenamento de tooyour de conexão.</span><span class="sxs-lookup"><span data-stu-id="7785b-162">This code initializes an instance of <strong>Task</strong> with a connection tooyour storage account.</span></span> <span data-ttu-id="7785b-163">Olá <strong>tarefa</strong> é passado toohello <strong>TaskList</strong>, que usa toocommunicate com o serviço de tabela hello:</span><span class="sxs-lookup"><span data-stu-id="7785b-163">hello <strong>Task</strong> is passed toohello <strong>TaskList</strong>, which uses it toocommunicate with hello Table service:</span></span>

    ```nodejs
    var TaskList = require('./routes/tasklist');
    var Task = require('./models/task');
    var task = new Task(azure.createTableService(), tableName, partitionKey);
    var taskList = new TaskList(task);

    app.get('/', taskList.showTasks.bind(taskList));
    app.post('/addtask', taskList.addTask.bind(taskList));
    app.post('/completetask', taskList.completeTask.bind(taskList));
    ```

4. <span data-ttu-id="7785b-164">Salvar Olá **app.js** arquivo.</span><span class="sxs-lookup"><span data-stu-id="7785b-164">Save hello **app.js** file.</span></span>

### <a name="modify-hello-index-view"></a><span data-ttu-id="7785b-165">Modificar a exibição do índice Olá</span><span class="sxs-lookup"><span data-stu-id="7785b-165">Modify hello index view</span></span>
1. <span data-ttu-id="7785b-166">Altere os diretórios toohello **exibições** Olá diretório e abra **Jade** em um editor de texto.</span><span class="sxs-lookup"><span data-stu-id="7785b-166">Change directories toohello **views** directory and open hello **index.jade** file in a text editor.</span></span>
2. <span data-ttu-id="7785b-167">Substitua o conteúdo de saudação do hello **Jade** arquivo com hello código a seguir.</span><span class="sxs-lookup"><span data-stu-id="7785b-167">Replace hello contents of hello **index.jade** file with hello following code.</span></span> <span data-ttu-id="7785b-168">Esse código define a exibição Olá para exibir tarefas existentes e define um formulário para adicionar novas tarefas e marcar os existentes, como concluída.</span><span class="sxs-lookup"><span data-stu-id="7785b-168">This code defines hello view for displaying existing tasks, and defines a form for adding new tasks and marking existing ones as completed.</span></span>

    ```
    extends layout

    block content
      h1= title
      br

      form(action="/completetask", method="post")
        table.table.table-striped.table-bordered
          tr
            td Name
            td Category
            td Date
            td Complete
          if tasks != []
            tr
              td
          else
            each task in tasks
              tr
                td #{task.name._}
                td #{task.category._}
                - var day   = task.Timestamp._.getDate();
                - var month = task.Timestamp._.getMonth() + 1;
                - var year  = task.Timestamp._.getFullYear();
                td #{month + "/" + day + "/" + year}
                td
                  input(type="checkbox", name="#{task.RowKey._}", value="#{!task.completed._}", checked=task.completed._)
        button.btn(type="submit") Update tasks
      hr
      form.well(action="/addtask", method="post")
        label Item Name:
        input(name="item[name]", type="textbox")
        label Item Category:
        input(name="item[category]", type="textbox")
        br
        button.btn(type="submit") Add item
    ```

3. <span data-ttu-id="7785b-169">Salve e feche o arquivo **index.jade** .</span><span class="sxs-lookup"><span data-stu-id="7785b-169">Save and close **index.jade** file.</span></span>

### <a name="modify-hello-global-layout"></a><span data-ttu-id="7785b-170">Modificar o layout global Olá</span><span class="sxs-lookup"><span data-stu-id="7785b-170">Modify hello global layout</span></span>
<span data-ttu-id="7785b-171">Olá **layout.jade** arquivo hello **exibições** diretório é usado como um modelo global para outros **.jade** arquivos.</span><span class="sxs-lookup"><span data-stu-id="7785b-171">hello **layout.jade** file in hello **views** directory is used as a global template for other **.jade** files.</span></span> <span data-ttu-id="7785b-172">Nesta etapa, modifique Olá **layout.jade** arquivo toouse [Twitter Bootstrap](https://github.com/twbs/bootstrap), que é um kit de ferramentas que torna mais fácil toodesign um site de aparência adequado.</span><span class="sxs-lookup"><span data-stu-id="7785b-172">In this step, modify hello **layout.jade** file toouse [Twitter Bootstrap](https://github.com/twbs/bootstrap), which is a toolkit that makes it easy toodesign a nice looking website.</span></span>

1. <span data-ttu-id="7785b-173">Baixe e extraia os arquivos de saudação para [Twitter Bootstrap](http://getbootstrap.com/).</span><span class="sxs-lookup"><span data-stu-id="7785b-173">Download and extract hello files for [Twitter Bootstrap](http://getbootstrap.com/).</span></span> <span data-ttu-id="7785b-174">Saudação de cópia **bootstrap.min.css** arquivo hello **bootstrap\\dist\\css** pasta toohello **pública\\folhas de estilo** diretório do seu aplicativo de lista de tarefas.</span><span class="sxs-lookup"><span data-stu-id="7785b-174">Copy hello **bootstrap.min.css** file from hello **bootstrap\\dist\\css** folder toohello **public\\stylesheets** directory of your tasklist application.</span></span>
2. <span data-ttu-id="7785b-175">De saudação **exibições** pasta, abra Olá **layout.jade** do arquivo em seu editor de texto e substitua o conteúdo de saudação pelo seguinte hello:</span><span class="sxs-lookup"><span data-stu-id="7785b-175">From hello **views** folder, open hello **layout.jade** file in your text editor and replace hello contents with hello following:</span></span>

    <span data-ttu-id="7785b-176">doctype html  html    head      title= title      link(rel='stylesheet', href='/stylesheets/bootstrap.min.css')      link(rel='stylesheet', href='/stylesheets/style.css')    body.app      nav.navbar.navbar-default        div.navbar-header          a.navbar-brand(href='/') My Tasks      block content</span><span class="sxs-lookup"><span data-stu-id="7785b-176">doctype html  html    head      title= title      link(rel='stylesheet', href='/stylesheets/bootstrap.min.css')      link(rel='stylesheet', href='/stylesheets/style.css')    body.app      nav.navbar.navbar-default        div.navbar-header          a.navbar-brand(href='/') My Tasks      block content</span></span>

3. <span data-ttu-id="7785b-177">Salvar Olá **layout.jade** arquivo.</span><span class="sxs-lookup"><span data-stu-id="7785b-177">Save hello **layout.jade** file.</span></span>

### <a name="running-hello-application-in-hello-emulator"></a><span data-ttu-id="7785b-178">Aplicativo de saudação em execução no emulador de saudação</span><span class="sxs-lookup"><span data-stu-id="7785b-178">Running hello Application in hello Emulator</span></span>
<span data-ttu-id="7785b-179">Use Olá aplicativo do comando toostart hello no emulador Olá a seguir.</span><span class="sxs-lookup"><span data-stu-id="7785b-179">Use hello following command toostart hello application in hello emulator.</span></span>

```powershell
PS C:\node\tasklist\WebRole1> start-azureemulator -launch
```

<span data-ttu-id="7785b-180">navegador de saudação abre e exibe o saudação página a seguir:</span><span class="sxs-lookup"><span data-stu-id="7785b-180">hello browser opens and displays hello following page:</span></span>

![Uma web paginada intitulada minha lista de tarefas com uma tabela que contém tarefas e campos tooadd uma nova tarefa.](./media/table-storage-cloud-service-nodejs/node44.png)

<span data-ttu-id="7785b-182">Usar Olá formulário tooadd itens ou remover itens existentes marcando-as como concluída.</span><span class="sxs-lookup"><span data-stu-id="7785b-182">Use hello form tooadd items, or remove existing items by marking them as completed.</span></span>

## <a name="publishing-hello-application-tooazure"></a><span data-ttu-id="7785b-183">Publicação tooAzure de aplicativo hello</span><span class="sxs-lookup"><span data-stu-id="7785b-183">Publishing hello Application tooAzure</span></span>
<span data-ttu-id="7785b-184">Na janela do Windows PowerShell hello, chame hello tooredeploy cmdlet a seguir tooAzure seu serviço hospedado.</span><span class="sxs-lookup"><span data-stu-id="7785b-184">In hello Windows PowerShell window, call hello following cmdlet tooredeploy your hosted service tooAzure.</span></span>

```powershell
PS C:\node\tasklist\WebRole1> Publish-AzureServiceProject -name myuniquename -location datacentername -launch
```

<span data-ttu-id="7785b-185">Substitua **myuniquename** por um nome exclusivo para o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="7785b-185">Replace **myuniquename** with a unique name for this application.</span></span> <span data-ttu-id="7785b-186">Substituir **datacentername** com o nome de saudação de um data center do Azure, como **Oeste dos EUA**.</span><span class="sxs-lookup"><span data-stu-id="7785b-186">Replace **datacentername** with hello name of an Azure data center, such as **West US**.</span></span>

<span data-ttu-id="7785b-187">Após a conclusão da implantação hello, você deve ver uma resposta semelhante toohello a seguir:</span><span class="sxs-lookup"><span data-stu-id="7785b-187">After hello deployment is complete, you should see a response similar toohello following:</span></span>

```
  PS C:\node\tasklist> publish-azureserviceproject -servicename tasklist -location "West US"
  WARNING: Publishing tasklist tooMicrosoft Azure. This may take several minutes...
  WARNING: 2:18:42 PM - Preparing runtime deployment for service 'tasklist'
  WARNING: 2:18:42 PM - Verifying storage account 'tasklist'...
  WARNING: 2:18:43 PM - Preparing deployment for tasklist with Subscription ID: 65a1016d-0f67-45d2-b838-b8f373d6d52e...
  WARNING: 2:19:01 PM - Connecting...
  WARNING: 2:19:02 PM - Uploading Package toostorage service larrystore...
  WARNING: 2:19:40 PM - Upgrading...
  WARNING: 2:22:48 PM - Created Deployment ID: b7134ab29b1249ff84ada2bd157f296a.
  WARNING: 2:22:48 PM - Initializing...
  WARNING: 2:22:49 PM - Instance WebRole1_IN_0 of role WebRole1 is ready.
  WARNING: 2:22:50 PM - Created Website URL: http://tasklist.cloudapp.net/.
```

<span data-ttu-id="7785b-188">Especificando Olá **-iniciar** opção no cmdlet anterior hello, navegador Olá abre e exibe seu aplicativo em execução no Azure, quando a publicação é concluída.</span><span class="sxs-lookup"><span data-stu-id="7785b-188">By specifying hello **-launch** option in hello previous cmdlet, hello browser opens and displays your application running in Azure when publishing is completed.</span></span>

![Uma janela do navegador exibindo a página do hello minha lista de tarefas.](./media/table-storage-cloud-service-nodejs/getting-started-1.png)

## <a name="stopping-and-deleting-your-application"></a><span data-ttu-id="7785b-191">Parando e excluindo o aplicativo</span><span class="sxs-lookup"><span data-stu-id="7785b-191">Stopping and Deleting Your Application</span></span>
<span data-ttu-id="7785b-192">Depois de implantar seu aplicativo, talvez você queira toodisable para evitar custos ou criar e implantar outros aplicativos Olá gratuitamente período de avaliação.</span><span class="sxs-lookup"><span data-stu-id="7785b-192">After deploying your application, you may want toodisable it so you can avoid costs or build and deploy other applications within hello free trial time period.</span></span>

<span data-ttu-id="7785b-193">O Azure cobra as instâncias de função web por hora de acordo com o tempo consumido do servidor.</span><span class="sxs-lookup"><span data-stu-id="7785b-193">Azure bills web role instances per hour of server time consumed.</span></span>
<span data-ttu-id="7785b-194">Hora do servidor é consumida quando o aplicativo for implantado, mesmo se as instâncias não estão em execução e estão em estado de saudação interrompido.</span><span class="sxs-lookup"><span data-stu-id="7785b-194">Server time is consumed once your application is deployed, even if the instances are not running and are in hello stopped state.</span></span>

<span data-ttu-id="7785b-195">Olá etapas a seguir mostram como toostop e excluir seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="7785b-195">hello following steps show you how toostop and delete your application.</span></span>

1. <span data-ttu-id="7785b-196">Na janela do Windows PowerShell hello, interrompa a implantação do serviço Olá criada na seção anterior Olá com hello cmdlet a seguir:</span><span class="sxs-lookup"><span data-stu-id="7785b-196">In hello Windows PowerShell window, stop hello service deployment created in hello previous section with hello following cmdlet:</span></span>

    ```powershell
    PS C:\node\tasklist\WebRole1> Stop-AzureService
    ```

   <span data-ttu-id="7785b-197">Parar serviço Olá pode levar vários minutos.</span><span class="sxs-lookup"><span data-stu-id="7785b-197">Stopping hello service may take several minutes.</span></span> <span data-ttu-id="7785b-198">Quando a saudação serviço for interrompido, você recebe uma mensagem indicando que ele foi interrompido.</span><span class="sxs-lookup"><span data-stu-id="7785b-198">When hello service is stopped, you receive a message indicating that it has stopped.</span></span>

2. <span data-ttu-id="7785b-199">serviço de saudação toodelete, chamada hello cmdlet a seguir:</span><span class="sxs-lookup"><span data-stu-id="7785b-199">toodelete hello service, call hello following cmdlet:</span></span>

    ```powershell
    PS C:\node\tasklist\WebRole1> Remove-AzureService contosotasklist
    ```

   <span data-ttu-id="7785b-200">Quando solicitado, insira **Y** toodelete serviço de saudação.</span><span class="sxs-lookup"><span data-stu-id="7785b-200">When prompted, enter **Y** toodelete hello service.</span></span>

   <span data-ttu-id="7785b-201">Excluindo serviço Olá pode levar vários minutos.</span><span class="sxs-lookup"><span data-stu-id="7785b-201">Deleting hello service may take several minutes.</span></span> <span data-ttu-id="7785b-202">Depois que serviço Olá for excluído, você receberá uma mensagem indicando que o serviço de saudação foi excluído.</span><span class="sxs-lookup"><span data-stu-id="7785b-202">After hello service is deleted, you will receive a message indicating that hello service was deleted.</span></span>

[aplicativo de Web Node.js usando Express]: http://azure.microsoft.com/develop/nodejs/tutorials/web-app-with-express/
[Armazenando e acessando dados no Azure]: http://msdn.microsoft.com/library/azure/gg433040.aspx
[aplicativo Web Node.js]: http://azure.microsoft.com/develop/nodejs/tutorials/getting-started/


