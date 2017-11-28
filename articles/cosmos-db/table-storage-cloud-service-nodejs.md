---
title: Aplicativo Web com armazenamento de tabelas (Node.js) | Microsoft Docs
description: "Um tutorial que tem como base o tutorial Aplicativo Web com o Express adicionando os serviços de Armazenamento do Azure e o módulo Azure."
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
ms.openlocfilehash: b802f880c1131abb7eb9ba00dd8f2e65017bc802
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="nodejs-web-application-using-storage"></a><span data-ttu-id="f71a8-103">Aplicativo Web do Node.js usando Armazenamento</span><span class="sxs-lookup"><span data-stu-id="f71a8-103">Node.js Web Application using Storage</span></span>
## <a name="overview"></a><span data-ttu-id="f71a8-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="f71a8-104">Overview</span></span>
<span data-ttu-id="f71a8-105">Neste tutorial, o aplicativo criado no tutorial [Aplicativo Web do Node.js usando o Expresso] é ampliado usando as Bibliotecas de cliente do Microsoft Azure para o Node.js para trabalhar com serviços de gerenciamento de dados.</span><span class="sxs-lookup"><span data-stu-id="f71a8-105">In this tutorial, the application you created in the [Node.js Web Application using Express] tutorial is extended using the Microsoft Azure Client Libraries for Node.js to work with data management services.</span></span> <span data-ttu-id="f71a8-106">Você amplia seu aplicativo ao criar um aplicativo de lista de tarefas com base na Web que pode ser implantado no Azure.</span><span class="sxs-lookup"><span data-stu-id="f71a8-106">You extend your application by creating a web-based task-list application that you can deploy to Azure.</span></span> <span data-ttu-id="f71a8-107">A lista de tarefas permite que um usuário recupere tarefas, adicione novas tarefas e marque tarefas como concluídas.</span><span class="sxs-lookup"><span data-stu-id="f71a8-107">The task list allows a user to retrieve tasks, add new tasks, and mark tasks as completed.</span></span>

<span data-ttu-id="f71a8-108">Os itens da tarefa são armazenados no Armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="f71a8-108">The task items are stored in Azure Storage.</span></span> <span data-ttu-id="f71a8-109">O Armazenamento do Azure fornece um armazenamento de dados não estruturado altamente disponível e tolerante a falhas.</span><span class="sxs-lookup"><span data-stu-id="f71a8-109">Azure Storage provides unstructured data storage that is fault-tolerant and highly available.</span></span> <span data-ttu-id="f71a8-110">O Armazenamento do Azure inclui várias estruturas de dados nas quais você pode armazenar e acessar dados.</span><span class="sxs-lookup"><span data-stu-id="f71a8-110">Azure Storage includes several data structures where you can store and access data.</span></span> <span data-ttu-id="f71a8-111">Você pode usar os serviços de armazenamento das APIs incluídas no SDK do Azure para Node.js ou por meio de APIs REST.</span><span class="sxs-lookup"><span data-stu-id="f71a8-111">You can use the storage services from the APIs included in the Azure SDK for Node.js or via REST APIs.</span></span> <span data-ttu-id="f71a8-112">Para saber mais, veja [Armazenando e acessando dados no Azure].</span><span class="sxs-lookup"><span data-stu-id="f71a8-112">For more information, see [Storing and Accessing Data in Azure].</span></span>

<span data-ttu-id="f71a8-113">Este tutorial presume que você tenha concluído os tutoriais [Aplicativo Web do Node.js] e [Node.js com Express][Aplicativo Web do Node.js usando o Expresso].</span><span class="sxs-lookup"><span data-stu-id="f71a8-113">This tutorial assumes that you have completed the [Node.js Web Application] and [Node.js with Express][Node.js Web Application using Express] tutorials.</span></span>

<span data-ttu-id="f71a8-114">Ele contém as seguintes informações:</span><span class="sxs-lookup"><span data-stu-id="f71a8-114">It contains the following information:</span></span>

* <span data-ttu-id="f71a8-115">Trabalhar com o mecanismo de modelo Jade</span><span class="sxs-lookup"><span data-stu-id="f71a8-115">How to work with the Jade template engine</span></span>
* <span data-ttu-id="f71a8-116">Trabalhar com os serviços de gerenciamento de dados do Azure</span><span class="sxs-lookup"><span data-stu-id="f71a8-116">How to work with Azure Data Management services</span></span>

<span data-ttu-id="f71a8-117">A captura de tela a seguir mostra o aplicativo concluído:</span><span class="sxs-lookup"><span data-stu-id="f71a8-117">The following screenshot shows the completed application:</span></span>

![A página da Web completa no Internet Explorer](./media/table-storage-cloud-service-nodejs/getting-started-1.png)

## <a name="setting-storage-credentials-in-webconfig"></a><span data-ttu-id="f71a8-119">Definindo credenciais de armazenamento em Web.Config</span><span class="sxs-lookup"><span data-stu-id="f71a8-119">Setting Storage Credentials in Web.Config</span></span>
<span data-ttu-id="f71a8-120">Você deve transmitir as credenciais de armazenamento para acessar o Armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="f71a8-120">You must pass in storage credentials to access Azure Storage.</span></span> <span data-ttu-id="f71a8-121">Isso é feito usando as configurações de aplicativo web.config.</span><span class="sxs-lookup"><span data-stu-id="f71a8-121">This is done by utilizing the web.config application settings.</span></span>
<span data-ttu-id="f71a8-122">As configurações web.config são transmitidas como variáveis de ambiente para o Nó as quais, em seguida, são lidas pelo SDK do Azure.</span><span class="sxs-lookup"><span data-stu-id="f71a8-122">The web.config settings are passed as environment variables to Node, which are then read by the Azure SDK.</span></span>

> [!NOTE]
> <span data-ttu-id="f71a8-123">As credenciais de armazenamento são usadas somente quando o aplicativo é implantado no Azure.</span><span class="sxs-lookup"><span data-stu-id="f71a8-123">Storage credentials are only used when the application is deployed to Azure.</span></span> <span data-ttu-id="f71a8-124">Quando executado no emulador, o aplicativo usa o emulador de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="f71a8-124">When running in the emulator, the application uses the storage emulator.</span></span>
>
>

<span data-ttu-id="f71a8-125">Execute as etapas a seguir para recuperar as credenciais da conta de armazenamento e adicioná-las às configurações de web.config:</span><span class="sxs-lookup"><span data-stu-id="f71a8-125">Perform the following steps to retrieve the storage account credentials and add them to the web.config settings:</span></span>

1. <span data-ttu-id="f71a8-126">Se ainda não estiver aberto, inicie o PowerShell do Azure no menu **Iniciar** expandindo **Todos os Programas, Azure** e clicando com o botão direito do mouse em **Azure PowerShell** e selecione **Executar como Administrador**.</span><span class="sxs-lookup"><span data-stu-id="f71a8-126">If it is not already open, start the Azure PowerShell from the **Start** menu by expanding **All Programs, Azure**, right-click **Azure PowerShell**, and then select **Run As Administrator**.</span></span>
2. <span data-ttu-id="f71a8-127">Altere os diretórios para a pasta que contém o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="f71a8-127">Change directories to the folder containing your application.</span></span> <span data-ttu-id="f71a8-128">Por exemplo, C:\\node\\tasklist\\WebRole1.</span><span class="sxs-lookup"><span data-stu-id="f71a8-128">For example, C:\\node\\tasklist\\WebRole1.</span></span>
3. <span data-ttu-id="f71a8-129">Na janela do Azure PowerShell, insira o seguinte cmdlet para recuperar as informações da conta de armazenamento:</span><span class="sxs-lookup"><span data-stu-id="f71a8-129">From the Azure Powershell window, enter the following cmdlet to retrieve the storage account information:</span></span>

    ```powershell
    PS C:\node\tasklist\WebRole1> Get-AzureStorageAccounts
    ```

   <span data-ttu-id="f71a8-130">O cmdlet anterior recupera a lista de contas de armazenamento e as chaves de conta associada ao seu serviço hospedado.</span><span class="sxs-lookup"><span data-stu-id="f71a8-130">The preceding cmdlet retrieves the list of storage accounts and account keys associated with your hosted service.</span></span>

   > [!NOTE]
   > <span data-ttu-id="f71a8-131">Como o SDK do Azure cria uma conta de armazenamento quando você implanta um serviço, uma conta de armazenamento já deve existir da implantação de seu aplicativo nos guias anteriores.</span><span class="sxs-lookup"><span data-stu-id="f71a8-131">Since the Azure SDK creates a storage account when you deploy a service, a storage account should already exist from deploying your application in the previous guides.</span></span>
   >
   >
4. <span data-ttu-id="f71a8-132">Abra o arquivo **ServiceDefinition.csdef** que contém as configurações de ambiente usadas quando o aplicativo é implantado no Azure:</span><span class="sxs-lookup"><span data-stu-id="f71a8-132">Open the **ServiceDefinition.csdef** file containing the environment settings that are used when the application is deployed to Azure:</span></span>

    ```powershell
    PS C:\node\tasklist> notepad ServiceDefinition.csdef
    ```

5. <span data-ttu-id="f71a8-133">Insira o seguinte bloco sob o elemento **Environment**, substituindo {STORAGE ACCOUNT} e {STORAGE ACCESS KEY} pelo nome da conta e a chave primária da conta de armazenamento que deseja usar para a implantação:</span><span class="sxs-lookup"><span data-stu-id="f71a8-133">Insert the following block under **Environment** element, substituting {STORAGE ACCOUNT} and {STORAGE ACCESS KEY} with the account name and the primary key for the storage account you want to use for deployment:</span></span>

  <Variable name="AZURE_STORAGE_ACCOUNT" value="{STORAGE ACCOUNT}" />
  <Variable name="AZURE_STORAGE_ACCESS_KEY" value="{STORAGE ACCESS KEY}" />

   ![O conteúdo do arquivo web.cloud.config](./media/table-storage-cloud-service-nodejs/node37.png)

6. <span data-ttu-id="f71a8-135">Salve o arquivo e feche o Bloco de Notas.</span><span class="sxs-lookup"><span data-stu-id="f71a8-135">Save the file and close notepad.</span></span>

### <a name="install-additional-modules"></a><span data-ttu-id="f71a8-136">Instalar módulos adicionais</span><span class="sxs-lookup"><span data-stu-id="f71a8-136">Install additional modules</span></span>
1. <span data-ttu-id="f71a8-137">Use o seguinte comando para instalar os módulos azure, [node-uuid], [nconf] e [async] localmente, bem como para salvar uma entrada para eles no arquivo **package.json**:</span><span class="sxs-lookup"><span data-stu-id="f71a8-137">Use the following command to install the [azure], [node-uuid], [nconf] and [async] modules locally as well as to save an entry for them to the **package.json** file:</span></span>

  ```powershell
  PS C:\node\tasklist\WebRole1> npm install azure-storage node-uuid async nconf --save
  ```

  <span data-ttu-id="f71a8-138">A saída desse comando deve ser semelhante ao seguinte:</span><span class="sxs-lookup"><span data-stu-id="f71a8-138">The output of this command should appear similar to the following:</span></span>

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

## <a name="using-the-table-service-in-a-node-application"></a><span data-ttu-id="f71a8-139">Usando um serviço de Tabela em um aplicativo de nó</span><span class="sxs-lookup"><span data-stu-id="f71a8-139">Using the Table service in a node application</span></span>
<span data-ttu-id="f71a8-140">Nesta seção, o aplicativo básico criado pelo comando **express** é ampliado, adicionando um arquivo **task.js** que contém o modelo para suas tarefas.</span><span class="sxs-lookup"><span data-stu-id="f71a8-140">In this section, the basic application created by the **express** command is extended by adding a **task.js** file containing the model for your tasks.</span></span> <span data-ttu-id="f71a8-141">Modifique o arquivo **app.js** existente e crie um novo arquivo **tasklist.js** que use o modelo.</span><span class="sxs-lookup"><span data-stu-id="f71a8-141">Modify the existing **app.js** file and create a new **tasklist.js** file that uses the model.</span></span>

### <a name="create-the-model"></a><span data-ttu-id="f71a8-142">Criar o modelo</span><span class="sxs-lookup"><span data-stu-id="f71a8-142">Create the model</span></span>
1. <span data-ttu-id="f71a8-143">No diretório **WebRole1**, crie um novo diretório com nome **models**.</span><span class="sxs-lookup"><span data-stu-id="f71a8-143">In the **WebRole1** directory, create a new directory named **models**.</span></span>
2. <span data-ttu-id="f71a8-144">No diretório **models**, crie um novo arquivo chamado **task.js**.</span><span class="sxs-lookup"><span data-stu-id="f71a8-144">In the **models** directory, create a new file named **task.js**.</span></span> <span data-ttu-id="f71a8-145">Esse arquivo contém o modelo para as tarefas criadas pelo seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="f71a8-145">This file contains the model for the tasks created by your application.</span></span>
3. <span data-ttu-id="f71a8-146">No início do arquivo **task.js** , adicione o seguinte código para fazer a referência às bibliotecas necessárias:</span><span class="sxs-lookup"><span data-stu-id="f71a8-146">At the beginning of the **task.js** file, add the following code to reference required libraries:</span></span>

    ```nodejs
    var azure = require('azure-storage');
    var uuid = require('node-uuid');
    var entityGen = azure.TableUtilities.entityGenerator;
    ```

4. <span data-ttu-id="f71a8-147">Em seguida, adicione o código para definir e exportar o objeto Tarefa.</span><span class="sxs-lookup"><span data-stu-id="f71a8-147">Next, add code to define and export the Task object.</span></span> <span data-ttu-id="f71a8-148">O objeto Tarefa é responsável por se conectar à tabela.</span><span class="sxs-lookup"><span data-stu-id="f71a8-148">The Task object is responsible for connecting to the table.</span></span>

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

5. <span data-ttu-id="f71a8-149">Em seguida, adicione o seguinte código para definir métodos adicionais no objeto da Tarefa, que permitem interações com os dados armazenados na tabela:</span><span class="sxs-lookup"><span data-stu-id="f71a8-149">Next, add the following code to define additional methods on the Task object, which allow interactions with data stored in the table:</span></span>

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
        // use entityGenerator to set types
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

6. <span data-ttu-id="f71a8-150">Salve e feche o arquivo **task.js** .</span><span class="sxs-lookup"><span data-stu-id="f71a8-150">Save and close the **task.js** file.</span></span>

### <a name="create-the-controller"></a><span data-ttu-id="f71a8-151">Criar o controlador</span><span class="sxs-lookup"><span data-stu-id="f71a8-151">Create the controller</span></span>
1. <span data-ttu-id="f71a8-152">No diretório **WebRole1/routes**, crie um novo arquivo chamado **tasklist.js** e abra-o em um editor de texto.</span><span class="sxs-lookup"><span data-stu-id="f71a8-152">In the **WebRole1/routes** directory, create a new file named **tasklist.js** and open it in a text editor.</span></span>
2. <span data-ttu-id="f71a8-153">Adicione os seguintes códigos ao **tasklist.js**.</span><span class="sxs-lookup"><span data-stu-id="f71a8-153">Add the following code to **tasklist.js**.</span></span> <span data-ttu-id="f71a8-154">Esse código carrega os módulos do azure e assíncronos, que são usados pelo **tasklist.js** e define a função **TaskList**, que é passada a uma instância do objeto **Tarefa** que definimos anteriormente:</span><span class="sxs-lookup"><span data-stu-id="f71a8-154">This code loads the azure and async modules, which are used by **tasklist.js** and defines the **TaskList** function, which is passed an instance of the **Task** object we defined earlier:</span></span>

    ```nodejs
    var azure = require('azure-storage');
    var async = require('async');

    module.exports = TaskList;

    function TaskList(task) {
      this.task = task;
    }
    ```

3. <span data-ttu-id="f71a8-155">Continue adicionando ao arquivo **tasklist.js**, adicionando os métodos usados para **showTasks**, **addTask** e **completeTasks**:</span><span class="sxs-lookup"><span data-stu-id="f71a8-155">Continue adding to the **tasklist.js** file by adding the methods used to **showTasks**, **addTask**, and **completeTasks**:</span></span>

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

4. <span data-ttu-id="f71a8-156">Salve o arquivo **tasklist.js**.</span><span class="sxs-lookup"><span data-stu-id="f71a8-156">Save the **tasklist.js** file.</span></span>

### <a name="modify-appjs"></a><span data-ttu-id="f71a8-157">Modificar app.js</span><span class="sxs-lookup"><span data-stu-id="f71a8-157">Modify app.js</span></span>
1. <span data-ttu-id="f71a8-158">No diretório **WebRole1**, abra o arquivo **app.js** em um editor de texto.</span><span class="sxs-lookup"><span data-stu-id="f71a8-158">In the **WebRole1** directory, open the **app.js** file in a text editor.</span></span>
2. <span data-ttu-id="f71a8-159">No início do arquivo, adicione o seguinte para carregar o módulo azure e definir o nome da tabela e a chave de partição:</span><span class="sxs-lookup"><span data-stu-id="f71a8-159">At the beginning of the file, add the following to load the azure module and set the table name and partition key:</span></span>

    ```nodejs
    var azure = require('azure-storage');
    var tableName = 'tasks';
    var partitionKey = 'hometasks';
    ```

3. <span data-ttu-id="f71a8-160">No arquivo app.js, role para baixo até onde for capaz de visualizar a seguinte linha:</span><span class="sxs-lookup"><span data-stu-id="f71a8-160">In the app.js file, scroll down to where you see the following line:</span></span>

    ```nodejs
    app.use('/', routes);
    app.use('/users', users);
    ```

    <span data-ttu-id="f71a8-161">Substitua as linhas anteriores pelo seguinte código.</span><span class="sxs-lookup"><span data-stu-id="f71a8-161">Replace the preceding lines with the following code.</span></span> <span data-ttu-id="f71a8-162">Esse código inicializa uma instância de <strong>Tarefa</strong> com uma conexão com sua conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="f71a8-162">This code initializes an instance of <strong>Task</strong> with a connection to your storage account.</span></span> <span data-ttu-id="f71a8-163">A <strong>Tarefa</strong> é transmitida à <strong>TaskList</strong>, que a usa para se comunicar com o serviço Tabela:</span><span class="sxs-lookup"><span data-stu-id="f71a8-163">The <strong>Task</strong> is passed to the <strong>TaskList</strong>, which uses it to communicate with the Table service:</span></span>

    ```nodejs
    var TaskList = require('./routes/tasklist');
    var Task = require('./models/task');
    var task = new Task(azure.createTableService(), tableName, partitionKey);
    var taskList = new TaskList(task);

    app.get('/', taskList.showTasks.bind(taskList));
    app.post('/addtask', taskList.addTask.bind(taskList));
    app.post('/completetask', taskList.completeTask.bind(taskList));
    ```

4. <span data-ttu-id="f71a8-164">Salve o arquivo **app.js** .</span><span class="sxs-lookup"><span data-stu-id="f71a8-164">Save the **app.js** file.</span></span>

### <a name="modify-the-index-view"></a><span data-ttu-id="f71a8-165">Modificar a exibição de índice</span><span class="sxs-lookup"><span data-stu-id="f71a8-165">Modify the index view</span></span>
1. <span data-ttu-id="f71a8-166">Altere os diretórios para o diretório **views** e abra o arquivo **index.jade** em um editor de texto.</span><span class="sxs-lookup"><span data-stu-id="f71a8-166">Change directories to the **views** directory and open the **index.jade** file in a text editor.</span></span>
2. <span data-ttu-id="f71a8-167">Substitua o conteúdo do arquivo **index.jade** pelo seguinte código.</span><span class="sxs-lookup"><span data-stu-id="f71a8-167">Replace the contents of the **index.jade** file with the following code.</span></span> <span data-ttu-id="f71a8-168">Esse código define a exibição das tarefas existentes, bem como define um formulário para adicionar novas tarefas e marcar as tarefas existentes como concluídas.</span><span class="sxs-lookup"><span data-stu-id="f71a8-168">This code defines the view for displaying existing tasks, and defines a form for adding new tasks and marking existing ones as completed.</span></span>

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

3. <span data-ttu-id="f71a8-169">Salve e feche o arquivo **index.jade** .</span><span class="sxs-lookup"><span data-stu-id="f71a8-169">Save and close **index.jade** file.</span></span>

### <a name="modify-the-global-layout"></a><span data-ttu-id="f71a8-170">Modificar o layout global</span><span class="sxs-lookup"><span data-stu-id="f71a8-170">Modify the global layout</span></span>
<span data-ttu-id="f71a8-171">O arquivo **layout.jade** no diretório **views** é usado como um modelo global para outros arquivos **.jade**.</span><span class="sxs-lookup"><span data-stu-id="f71a8-171">The **layout.jade** file in the **views** directory is used as a global template for other **.jade** files.</span></span> <span data-ttu-id="f71a8-172">Nesta etapa, modifique o arquivo **layout.jade** para usar a [Inicialização do Twitter](https://github.com/twbs/bootstrap), que é um kit de ferramentas que facilita a criação de um site com uma aparência interessante.</span><span class="sxs-lookup"><span data-stu-id="f71a8-172">In this step, modify the **layout.jade** file to use [Twitter Bootstrap](https://github.com/twbs/bootstrap), which is a toolkit that makes it easy to design a nice looking website.</span></span>

1. <span data-ttu-id="f71a8-173">Baixe e extraia os arquivos para a [Twitter Bootstrap](http://getbootstrap.com/).</span><span class="sxs-lookup"><span data-stu-id="f71a8-173">Download and extract the files for [Twitter Bootstrap](http://getbootstrap.com/).</span></span> <span data-ttu-id="f71a8-174">Copie o arquivo **bootstrap.min.css** da pasta **bootstrap\\dist\\css** para o diretório **public\\stylesheets** de seu aplicativo de lista de tarefas.</span><span class="sxs-lookup"><span data-stu-id="f71a8-174">Copy the **bootstrap.min.css** file from the **bootstrap\\dist\\css** folder to the **public\\stylesheets** directory of your tasklist application.</span></span>
2. <span data-ttu-id="f71a8-175">Na pasta **views**, abra o arquivo **layout.jade** em seu editor de texto e substitua o conteúdo pelo seguinte:</span><span class="sxs-lookup"><span data-stu-id="f71a8-175">From the **views** folder, open the **layout.jade** file in your text editor and replace the contents with the following:</span></span>

    <span data-ttu-id="f71a8-176">doctype html  html    head      title= title      link(rel='stylesheet', href='/stylesheets/bootstrap.min.css')      link(rel='stylesheet', href='/stylesheets/style.css')    body.app      nav.navbar.navbar-default        div.navbar-header          a.navbar-brand(href='/') My Tasks      block content</span><span class="sxs-lookup"><span data-stu-id="f71a8-176">doctype html  html    head      title= title      link(rel='stylesheet', href='/stylesheets/bootstrap.min.css')      link(rel='stylesheet', href='/stylesheets/style.css')    body.app      nav.navbar.navbar-default        div.navbar-header          a.navbar-brand(href='/') My Tasks      block content</span></span>

3. <span data-ttu-id="f71a8-177">Salve o arquivo **layout.jade**.</span><span class="sxs-lookup"><span data-stu-id="f71a8-177">Save the **layout.jade** file.</span></span>

### <a name="running-the-application-in-the-emulator"></a><span data-ttu-id="f71a8-178">Executando o aplicativo no emulador</span><span class="sxs-lookup"><span data-stu-id="f71a8-178">Running the Application in the Emulator</span></span>
<span data-ttu-id="f71a8-179">Use o seguinte comando para iniciar o aplicativo no emulador.</span><span class="sxs-lookup"><span data-stu-id="f71a8-179">Use the following command to start the application in the emulator.</span></span>

```powershell
PS C:\node\tasklist\WebRole1> start-azureemulator -launch
```

<span data-ttu-id="f71a8-180">O navegador é aberto e exibe a página a seguir:</span><span class="sxs-lookup"><span data-stu-id="f71a8-180">The browser opens and displays the following page:</span></span>

![Uma página da Web chamada My Task List com uma tabela que contém tarefas e campos para adicionar uma nova tarefa.](./media/table-storage-cloud-service-nodejs/node44.png)

<span data-ttu-id="f71a8-182">Use o formulário para adicionar itens ou remover itens existentes marcando-os como completos.</span><span class="sxs-lookup"><span data-stu-id="f71a8-182">Use the form to add items, or remove existing items by marking them as completed.</span></span>

## <a name="publishing-the-application-to-azure"></a><span data-ttu-id="f71a8-183">Publicando o aplicativo no Azure</span><span class="sxs-lookup"><span data-stu-id="f71a8-183">Publishing the Application to Azure</span></span>
<span data-ttu-id="f71a8-184">Na janela do Windows PowerShell, chame o seguinte cmdlet para reimplantar o serviço hospedado no Azure.</span><span class="sxs-lookup"><span data-stu-id="f71a8-184">In the Windows PowerShell window, call the following cmdlet to redeploy your hosted service to Azure.</span></span>

```powershell
PS C:\node\tasklist\WebRole1> Publish-AzureServiceProject -name myuniquename -location datacentername -launch
```

<span data-ttu-id="f71a8-185">Substitua **myuniquename** por um nome exclusivo para o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="f71a8-185">Replace **myuniquename** with a unique name for this application.</span></span> <span data-ttu-id="f71a8-186">Substitua **datacentername** pelo nome de um data center do Azure, como **Oeste dos EUA**.</span><span class="sxs-lookup"><span data-stu-id="f71a8-186">Replace **datacentername** with the name of an Azure data center, such as **West US**.</span></span>

<span data-ttu-id="f71a8-187">Após a conclusão da implantação, você deverá ver uma resposta semelhante ao seguinte:</span><span class="sxs-lookup"><span data-stu-id="f71a8-187">After the deployment is complete, you should see a response similar to the following:</span></span>

```
  PS C:\node\tasklist> publish-azureserviceproject -servicename tasklist -location "West US"
  WARNING: Publishing tasklist to Microsoft Azure. This may take several minutes...
  WARNING: 2:18:42 PM - Preparing runtime deployment for service 'tasklist'
  WARNING: 2:18:42 PM - Verifying storage account 'tasklist'...
  WARNING: 2:18:43 PM - Preparing deployment for tasklist with Subscription ID: 65a1016d-0f67-45d2-b838-b8f373d6d52e...
  WARNING: 2:19:01 PM - Connecting...
  WARNING: 2:19:02 PM - Uploading Package to storage service larrystore...
  WARNING: 2:19:40 PM - Upgrading...
  WARNING: 2:22:48 PM - Created Deployment ID: b7134ab29b1249ff84ada2bd157f296a.
  WARNING: 2:22:48 PM - Initializing...
  WARNING: 2:22:49 PM - Instance WebRole1_IN_0 of role WebRole1 is ready.
  WARNING: 2:22:50 PM - Created Website URL: http://tasklist.cloudapp.net/.
```

<span data-ttu-id="f71a8-188">Ao especificar a opção **-launch** no cmdlet anterior, o navegador será aberto e exibirá o aplicativo em execução no Azure quando a publicação for concluída.</span><span class="sxs-lookup"><span data-stu-id="f71a8-188">By specifying the **-launch** option in the previous cmdlet, the browser opens and displays your application running in Azure when publishing is completed.</span></span>

![Uma janela do navegador exibindo a página My Task List.](./media/table-storage-cloud-service-nodejs/getting-started-1.png)

## <a name="stopping-and-deleting-your-application"></a><span data-ttu-id="f71a8-191">Parando e excluindo o aplicativo</span><span class="sxs-lookup"><span data-stu-id="f71a8-191">Stopping and Deleting Your Application</span></span>
<span data-ttu-id="f71a8-192">Depois de implantar o aplicativo, você talvez queira desabilitá-lo, de forma que seja possível evitar os custos ou compilar e implantar outros aplicativos no período de avaliação gratuita.</span><span class="sxs-lookup"><span data-stu-id="f71a8-192">After deploying your application, you may want to disable it so you can avoid costs or build and deploy other applications within the free trial time period.</span></span>

<span data-ttu-id="f71a8-193">O Azure cobra as instâncias de função web por hora de acordo com o tempo consumido do servidor.</span><span class="sxs-lookup"><span data-stu-id="f71a8-193">Azure bills web role instances per hour of server time consumed.</span></span>
<span data-ttu-id="f71a8-194">O tempo do servidor é consumido quando seu aplicativo é implantado, mesmo se as instâncias não estiverem sendo executadas e estiverem no estado parado.</span><span class="sxs-lookup"><span data-stu-id="f71a8-194">Server time is consumed once your application is deployed, even if the instances are not running and are in the stopped state.</span></span>

<span data-ttu-id="f71a8-195">As etapas a seguir mostram como parar e excluir o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="f71a8-195">The following steps show you how to stop and delete your application.</span></span>

1. <span data-ttu-id="f71a8-196">Na janela do Windows PowerShell, interrompa a implantação do serviço criada na seção anterior com o seguinte cmdlet:</span><span class="sxs-lookup"><span data-stu-id="f71a8-196">In the Windows PowerShell window, stop the service deployment created in the previous section with the following cmdlet:</span></span>

    ```powershell
    PS C:\node\tasklist\WebRole1> Stop-AzureService
    ```

   <span data-ttu-id="f71a8-197">Interromper o serviço pode levar alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="f71a8-197">Stopping the service may take several minutes.</span></span> <span data-ttu-id="f71a8-198">Quando o serviço for interrompido, você recebe uma mensagem indicando que foi interrompido.</span><span class="sxs-lookup"><span data-stu-id="f71a8-198">When the service is stopped, you receive a message indicating that it has stopped.</span></span>

2. <span data-ttu-id="f71a8-199">Para excluir o serviço, chame o seguinte cmdlet:</span><span class="sxs-lookup"><span data-stu-id="f71a8-199">To delete the service, call the following cmdlet:</span></span>

    ```powershell
    PS C:\node\tasklist\WebRole1> Remove-AzureService contosotasklist
    ```

   <span data-ttu-id="f71a8-200">Quando solicitado, insira **Y** para excluir o serviço.</span><span class="sxs-lookup"><span data-stu-id="f71a8-200">When prompted, enter **Y** to delete the service.</span></span>

   <span data-ttu-id="f71a8-201">Excluir o serviço pode levar alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="f71a8-201">Deleting the service may take several minutes.</span></span> <span data-ttu-id="f71a8-202">Depois que o serviço for excluído, você receberá uma mensagem indicando que o serviço foi excluído.</span><span class="sxs-lookup"><span data-stu-id="f71a8-202">After the service is deleted, you will receive a message indicating that the service was deleted.</span></span>

[Aplicativo Web do Node.js usando o Expresso]: http://azure.microsoft.com/develop/nodejs/tutorials/web-app-with-express/
[Armazenando e acessando dados no Azure]: http://msdn.microsoft.com/library/azure/gg433040.aspx
[Aplicativo Web do Node.js]: http://azure.microsoft.com/develop/nodejs/tutorials/getting-started/


