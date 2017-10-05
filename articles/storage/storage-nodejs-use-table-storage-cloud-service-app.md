---
title: Aplicativo Web com armazenamento de tabelas (Node.js) | Microsoft Docs
description: "Um tutorial que tem como base o tutorial Aplicativo Web com o Express adicionando os serviços de Armazenamento do Azure e o módulo Azure."
services: cloud-services, storage
documentationcenter: nodejs
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: e90959a2-4cb2-4b19-9bfb-aede15b18b1c
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 12/08/2016
ms.author: marsma
ms.openlocfilehash: 5d7ee2f529b5127ee60ec8b4f5acaa49e75ddf39
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="nodejs-web-application-using-storage"></a><span data-ttu-id="9d519-103">Aplicativo Web do Node.js usando Armazenamento</span><span class="sxs-lookup"><span data-stu-id="9d519-103">Node.js Web Application using Storage</span></span>
## <a name="overview"></a><span data-ttu-id="9d519-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="9d519-104">Overview</span></span>
<span data-ttu-id="9d519-105">Neste tutorial, você ampliará o aplicativo criado no tutorial [Aplicativo Web do Node.js usando o Express] usando as bibliotecas de clientes do Microsoft Azure para o Node.js para trabalhar com serviços de gerenciamento de dados.</span><span class="sxs-lookup"><span data-stu-id="9d519-105">In this tutorial, you will extend the application created in the [Node.js Web Application using Express] tutorial by using the Microsoft Azure Client Libraries for Node.js to work with data management services.</span></span> <span data-ttu-id="9d519-106">Você ampliará seu aplicativo para criar um aplicativo de lista de tarefas com base na Web que pode ser implantado no Azure.</span><span class="sxs-lookup"><span data-stu-id="9d519-106">You will extend your application to create a web-based task-list application that you can deploy to Azure.</span></span> <span data-ttu-id="9d519-107">A lista de tarefas permite que um usuário recupere tarefas, adicione novas tarefas e marque tarefas como concluídas.</span><span class="sxs-lookup"><span data-stu-id="9d519-107">The task list allows a user to retrieve tasks, add new tasks, and mark tasks as completed.</span></span>

<span data-ttu-id="9d519-108">Os itens da tarefa são armazenados no Armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="9d519-108">The task items are stored in Azure Storage.</span></span> <span data-ttu-id="9d519-109">O Armazenamento do Azure fornece um armazenamento de dados não estruturado altamente disponível e tolerante a falhas.</span><span class="sxs-lookup"><span data-stu-id="9d519-109">Azure Storage provides unstructured data storage that is fault-tolerant and highly available.</span></span> <span data-ttu-id="9d519-110">O Armazenamento do Azure inclui diversas estruturas de dados, em que você pode armazenar e acessar dados, além de poder utilizar os serviços de armazenamento das APIs incluídos no SDK do Azure para Node.js ou por meio de APIs REST.</span><span class="sxs-lookup"><span data-stu-id="9d519-110">Azure Storage includes several data structures where you can store and access data, and you can leverage the storage services from the APIs included in the Azure SDK for Node.js or via REST APIs.</span></span> <span data-ttu-id="9d519-111">Para saber mais, veja [Armazenando e acessando dados no Azure].</span><span class="sxs-lookup"><span data-stu-id="9d519-111">For more information, see [Storing and Accessing Data in Azure].</span></span>

<span data-ttu-id="9d519-112">Este tutorial presume que você tenha concluído os tutoriais [Aplicativo Web do Node.js] e [Node.js com Express][Aplicativo Web do Node.js usando o Express].</span><span class="sxs-lookup"><span data-stu-id="9d519-112">This tutorial assumes that you have completed the [Node.js Web Application] and [Node.js with Express][Node.js Web Application using Express] tutorials.</span></span>

<span data-ttu-id="9d519-113">Você aprenderá:</span><span class="sxs-lookup"><span data-stu-id="9d519-113">You will learn:</span></span>

* <span data-ttu-id="9d519-114">Trabalhar com o mecanismo de modelo Jade</span><span class="sxs-lookup"><span data-stu-id="9d519-114">How to work with the Jade template engine</span></span>
* <span data-ttu-id="9d519-115">Trabalhar com os serviços de gerenciamento de dados do Azure</span><span class="sxs-lookup"><span data-stu-id="9d519-115">How to work with Azure Data Management services</span></span>

<span data-ttu-id="9d519-116">Abaixo, uma captura de tela do aplicativo concluído:</span><span class="sxs-lookup"><span data-stu-id="9d519-116">A screenshot of the completed application is below:</span></span>

![A página da Web completa no Internet Explorer](./media/storage-nodejs-use-table-storage-cloud-service-app/getting-started-1.png)

## <a name="setting-storage-credentials-in-webconfig"></a><span data-ttu-id="9d519-118">Definindo credenciais de armazenamento em Web.Config</span><span class="sxs-lookup"><span data-stu-id="9d519-118">Setting Storage Credentials in Web.Config</span></span>
<span data-ttu-id="9d519-119">Para acessar o Armazenamento do Azure, você precisa transmitir as credenciais de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="9d519-119">To access Azure Storage, you need to pass in storage credentials.</span></span> <span data-ttu-id="9d519-120">Para isso, você deve utilizar as configurações do aplicativo web.config.</span><span class="sxs-lookup"><span data-stu-id="9d519-120">To do this, you utilize web.config application settings.</span></span>
<span data-ttu-id="9d519-121">Essas configurações serão transmitidas como variáveis de ambiente para Node que, em seguida, serão lidas pelo SDK do Azure.</span><span class="sxs-lookup"><span data-stu-id="9d519-121">Those settings will be passed as environment variables to Node, which are then read by the Azure SDK.</span></span>

> [!NOTE]
> <span data-ttu-id="9d519-122">As credenciais de armazenamento são usadas somente quando o aplicativo é implantado no Azure.</span><span class="sxs-lookup"><span data-stu-id="9d519-122">Storage credentials are only used when the application is deployed to Azure.</span></span> <span data-ttu-id="9d519-123">Quando executado no emulador, o aplicativo usará o emulador de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="9d519-123">When running in the emulator, the application will use the storage emulator.</span></span>
>
>

<span data-ttu-id="9d519-124">Execute as etapas a seguir para recuperar as credenciais da conta de armazenamento e adicioná-las às configurações de web.config:</span><span class="sxs-lookup"><span data-stu-id="9d519-124">Perform the following steps to retrieve the storage account credentials and add them to the web.config settings:</span></span>

1. <span data-ttu-id="9d519-125">Se ainda não estiver aberto, inicie o PowerShell do Azure no menu **Iniciar** expandindo **Todos os Programas, Azure** e clicando com o botão direito do mouse em **Azure PowerShell** e selecione **Executar como Administrador**.</span><span class="sxs-lookup"><span data-stu-id="9d519-125">If it is not already open, start the Azure PowerShell from the **Start** menu by expanding **All Programs, Azure**, right-click **Azure PowerShell**, and then select **Run As Administrator**.</span></span>
2. <span data-ttu-id="9d519-126">Altere os diretórios para a pasta que contém o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="9d519-126">Change directories to the folder containing your application.</span></span> <span data-ttu-id="9d519-127">Por exemplo, C:\\node\\tasklist\\WebRole1.</span><span class="sxs-lookup"><span data-stu-id="9d519-127">For example, C:\\node\\tasklist\\WebRole1.</span></span>
3. <span data-ttu-id="9d519-128">Na janela do PowerShell do Azure, insira o seguinte cmdlet para recuperar as informações da conta de armazenamento:</span><span class="sxs-lookup"><span data-stu-id="9d519-128">From the Azure Powershell window enter the following cmdlet to retrieve the storage account information:</span></span>

    ```powershell
    PS C:\node\tasklist\WebRole1> Get-AzureStorageAccounts
    ```

   <span data-ttu-id="9d519-129">Isso recupera a lista de contas de armazenamento e as chaves da conta associada ao seu serviço hospedado.</span><span class="sxs-lookup"><span data-stu-id="9d519-129">This retrieves the list of storage accounts and account keys associated with your hosted service.</span></span>

   > [!NOTE]
   > <span data-ttu-id="9d519-130">Como o SDK do Azure cria uma conta de armazenamento quando você implanta um serviço, uma conta de armazenamento já deve existir da implantação de seu aplicativo nos guias anteriores.</span><span class="sxs-lookup"><span data-stu-id="9d519-130">Since the Azure SDK creates a storage account when you deploy a service, a storage account should already exist from deploying your application in the previous guides.</span></span>
   >
   >
4. <span data-ttu-id="9d519-131">Abra o arquivo **ServiceDefinition.csdef** que contém as configurações de ambiente usadas quando o aplicativo é implantado no Azure:</span><span class="sxs-lookup"><span data-stu-id="9d519-131">Open the **ServiceDefinition.csdef** file containing the environment settings that are used when the application is deployed to Azure:</span></span>

    ```powershell
    PS C:\node\tasklist> notepad ServiceDefinition.csdef
    ```

5. <span data-ttu-id="9d519-132">Insira o seguinte bloco sob o elemento **Environment**, substituindo {STORAGE ACCOUNT} e {STORAGE ACCESS KEY} pelo nome da conta e a chave primária da conta de armazenamento que deseja usar para a implantação:</span><span class="sxs-lookup"><span data-stu-id="9d519-132">Insert the following block under **Environment** element, substituting {STORAGE ACCOUNT} and {STORAGE ACCESS KEY} with the account name and the primary key for the storage account you want to use for deployment:</span></span>

  <Variable name="AZURE_STORAGE_ACCOUNT" value="{STORAGE ACCOUNT}" />
  <Variable name="AZURE_STORAGE_ACCESS_KEY" value="{STORAGE ACCESS KEY}" />

   ![O conteúdo do arquivo web.cloud.config](./media/storage-nodejs-use-table-storage-cloud-service-app/node37.png)

6. <span data-ttu-id="9d519-134">Salve o arquivo e feche o Bloco de Notas.</span><span class="sxs-lookup"><span data-stu-id="9d519-134">Save the file and close notepad.</span></span>

### <a name="install-additional-modules"></a><span data-ttu-id="9d519-135">Instalar módulos adicionais</span><span class="sxs-lookup"><span data-stu-id="9d519-135">Install additional modules</span></span>
1. <span data-ttu-id="9d519-136">Use o seguinte comando para instalar os módulos azure, [node-uuid], [nconf] e [async] localmente, bem como para salvar uma entrada para eles no arquivo **package.json**:</span><span class="sxs-lookup"><span data-stu-id="9d519-136">Use the following command to install the [azure], [node-uuid], [nconf] and [async] modules locally as well as to save an entry for them to the **package.json** file:</span></span>

  ```powershell
  PS C:\node\tasklist\WebRole1> npm install azure-storage node-uuid async nconf --save
  ```

  <span data-ttu-id="9d519-137">A saída desse comando deve ser semelhante ao seguinte:</span><span class="sxs-lookup"><span data-stu-id="9d519-137">The output of this command should appear similar to the following:</span></span>

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

## <a name="using-the-table-service-in-a-node-application"></a><span data-ttu-id="9d519-138">Usando um serviço de Tabela em um aplicativo de nó</span><span class="sxs-lookup"><span data-stu-id="9d519-138">Using the Table service in a node application</span></span>
<span data-ttu-id="9d519-139">Nesta seção, você ampliará o aplicativo básico criado pelo comando **express**, adicionando um arquivo **task.js** que contém o modelo para suas tarefas.</span><span class="sxs-lookup"><span data-stu-id="9d519-139">In this section you will extend the basic application created by the **express** command by adding a **task.js** file which contains the model for your tasks.</span></span> <span data-ttu-id="9d519-140">Você também modificará o **app.js** existente e criar um novo arquivo **tasklist.js** que usa o modelo.</span><span class="sxs-lookup"><span data-stu-id="9d519-140">You will also modify the existing **app.js** and create a new **tasklist.js** file that uses the model.</span></span>

### <a name="create-the-model"></a><span data-ttu-id="9d519-141">Criar o modelo</span><span class="sxs-lookup"><span data-stu-id="9d519-141">Create the model</span></span>
1. <span data-ttu-id="9d519-142">No diretório **WebRole1**, crie um novo diretório com nome **models**.</span><span class="sxs-lookup"><span data-stu-id="9d519-142">In the **WebRole1** directory, create a new directory named **models**.</span></span>
2. <span data-ttu-id="9d519-143">No diretório **models**, crie um novo arquivo chamado **task.js**.</span><span class="sxs-lookup"><span data-stu-id="9d519-143">In the **models** directory, create a new file named **task.js**.</span></span> <span data-ttu-id="9d519-144">Esse arquivo vai conter o modelo para as tarefas criadas pelo seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="9d519-144">This file will contain the model for the tasks created by your application.</span></span>
3. <span data-ttu-id="9d519-145">No início do arquivo **task.js** , adicione o seguinte código para fazer a referência às bibliotecas necessárias:</span><span class="sxs-lookup"><span data-stu-id="9d519-145">At the beginning of the **task.js** file, add the following code to reference required libraries:</span></span>

    ```nodejs
    var azure = require('azure-storage');
    var uuid = require('node-uuid');
    var entityGen = azure.TableUtilities.entityGenerator;
    ```

4. <span data-ttu-id="9d519-146">Em seguida, você adicionará o código para definir e exportar o objeto da tarefa.</span><span class="sxs-lookup"><span data-stu-id="9d519-146">Next, you will add code to define and export the Task object.</span></span> <span data-ttu-id="9d519-147">Este objeto é responsável por se conectar à tabela.</span><span class="sxs-lookup"><span data-stu-id="9d519-147">This object is responsible for connecting to the table.</span></span>

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

5. <span data-ttu-id="9d519-148">Em seguida, adicione o seguinte código para definir métodos adicionais no objeto da Tarefa, que permitem interações com os dados armazenados na tabela:</span><span class="sxs-lookup"><span data-stu-id="9d519-148">Next, add the following code to define additional methods on the Task object, which allow interactions with data stored in the table:</span></span>

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

6. <span data-ttu-id="9d519-149">Salve e feche o arquivo **task.js** .</span><span class="sxs-lookup"><span data-stu-id="9d519-149">Save and close the **task.js** file.</span></span>

### <a name="create-the-controller"></a><span data-ttu-id="9d519-150">Criar o controlador</span><span class="sxs-lookup"><span data-stu-id="9d519-150">Create the controller</span></span>
1. <span data-ttu-id="9d519-151">No diretório **WebRole1/routes**, crie um novo arquivo chamado **tasklist.js** e abra-o em um editor de texto.</span><span class="sxs-lookup"><span data-stu-id="9d519-151">In the **WebRole1/routes** directory, create a new file named **tasklist.js** and open it in a text editor.</span></span>
2. <span data-ttu-id="9d519-152">Adicione os seguintes códigos ao **tasklist.js**.</span><span class="sxs-lookup"><span data-stu-id="9d519-152">Add the following code to **tasklist.js**.</span></span> <span data-ttu-id="9d519-153">Isso carrega os módulos azure e async, que são usados por **tasklist.js**.</span><span class="sxs-lookup"><span data-stu-id="9d519-153">This loads the azure and async modules, which are used by **tasklist.js**.</span></span> <span data-ttu-id="9d519-154">Isso também define a função de **TaskList**, que é transmitida a uma instância do objeto da **Task** definido anteriormente:</span><span class="sxs-lookup"><span data-stu-id="9d519-154">This also defines the **TaskList** function, which is passed an instance of the **Task** object we defined earlier:</span></span>

    ```nodejs
    var azure = require('azure-storage');
    var async = require('async');

    module.exports = TaskList;

    function TaskList(task) {
      this.task = task;
    }
    ```

3. <span data-ttu-id="9d519-155">Continue adicionando ao arquivo **tasklist.js**, adicionando os métodos usados para **showTasks**, **addTask** e **completeTasks**:</span><span class="sxs-lookup"><span data-stu-id="9d519-155">Continue adding to the **tasklist.js** file by adding the methods used to **showTasks**, **addTask**, and **completeTasks**:</span></span>

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

4. <span data-ttu-id="9d519-156">Salve o arquivo **tasklist.js**.</span><span class="sxs-lookup"><span data-stu-id="9d519-156">Save the **tasklist.js** file.</span></span>

### <a name="modify-appjs"></a><span data-ttu-id="9d519-157">Modificar app.js</span><span class="sxs-lookup"><span data-stu-id="9d519-157">Modify app.js</span></span>
1. <span data-ttu-id="9d519-158">No diretório **WebRole1**, abra o arquivo **app.js** em um editor de texto.</span><span class="sxs-lookup"><span data-stu-id="9d519-158">In the **WebRole1** directory, open the **app.js** file in a text editor.</span></span>
2. <span data-ttu-id="9d519-159">No início do arquivo, adicione o seguinte para carregar o módulo azure e definir o nome da tabela e a chave de partição:</span><span class="sxs-lookup"><span data-stu-id="9d519-159">At the beginning of the file, add the following to load the azure module and set the table name and partition key:</span></span>

    ```nodejs
    var azure = require('azure-storage');
    var tableName = 'tasks';
    var partitionKey = 'hometasks';
    ```

3. <span data-ttu-id="9d519-160">No arquivo app.js, role para baixo até onde for capaz de visualizar a seguinte linha:</span><span class="sxs-lookup"><span data-stu-id="9d519-160">In the app.js file, scroll down to where you see the following line:</span></span>

    ```nodejs
    app.use('/', routes);
    app.use('/users', users);
    ```

    <span data-ttu-id="9d519-161">Substitua as linhas acima pelo código mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="9d519-161">Replace the above lines with the code shown below.</span></span> <span data-ttu-id="9d519-162">Será inicializada uma instância de <strong>Tarefa</strong> com uma conexão à sua conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="9d519-162">This will initialize an instance of <strong>Task</strong> with a connection to your storage account.</span></span> <span data-ttu-id="9d519-163">Ela será transmitida à <strong>TaskList</strong>, que a usará para se comunicar com o serviço Tabela:</span><span class="sxs-lookup"><span data-stu-id="9d519-163">This is passed to the <strong>TaskList</strong>, which will use it to communicate with the Table service:</span></span>

    ```nodejs
    var TaskList = require('./routes/tasklist');
    var Task = require('./models/task');
    var task = new Task(azure.createTableService(), tableName, partitionKey);
    var taskList = new TaskList(task);

    app.get('/', taskList.showTasks.bind(taskList));
    app.post('/addtask', taskList.addTask.bind(taskList));
    app.post('/completetask', taskList.completeTask.bind(taskList));
    ```

4. <span data-ttu-id="9d519-164">Salve o arquivo **app.js** .</span><span class="sxs-lookup"><span data-stu-id="9d519-164">Save the **app.js** file.</span></span>

### <a name="modify-the-index-view"></a><span data-ttu-id="9d519-165">Modificar a exibição de índice</span><span class="sxs-lookup"><span data-stu-id="9d519-165">Modify the index view</span></span>
1. <span data-ttu-id="9d519-166">Altere os diretórios para o diretório **views** e abra o arquivo **index.jade** em um editor de texto.</span><span class="sxs-lookup"><span data-stu-id="9d519-166">Change directories to the **views** directory and open the **index.jade** file in a text editor.</span></span>
2. <span data-ttu-id="9d519-167">Substitua o conteúdo do arquivo **index.jade** pelo código abaixo.</span><span class="sxs-lookup"><span data-stu-id="9d519-167">Replace the contents of the **index.jade** file with the code below.</span></span> <span data-ttu-id="9d519-168">Isso define o modo de exibição das tarefas existentes, bem como um formulário para adicionar novas tarefas e marcar as tarefas existentes como concluídas.</span><span class="sxs-lookup"><span data-stu-id="9d519-168">This defines the view for displaying existing tasks, as well as a form for adding new tasks and marking existing ones as completed.</span></span>

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

3. <span data-ttu-id="9d519-169">Salve e feche o arquivo **index.jade** .</span><span class="sxs-lookup"><span data-stu-id="9d519-169">Save and close **index.jade** file.</span></span>

### <a name="modify-the-global-layout"></a><span data-ttu-id="9d519-170">Modificar o layout global</span><span class="sxs-lookup"><span data-stu-id="9d519-170">Modify the global layout</span></span>
<span data-ttu-id="9d519-171">O arquivo **layout.jade** no diretório **views** é usado como um modelo global para outros arquivos **.jade**.</span><span class="sxs-lookup"><span data-stu-id="9d519-171">The **layout.jade** file in the **views** directory is used as a global template for other **.jade** files.</span></span> <span data-ttu-id="9d519-172">Nesta etapa, você o modificará para usar a [Twitter Bootstrap](https://github.com/twbs/bootstrap), que é um kit de ferramentas que facilita a criação de um site com uma aparência interessante.</span><span class="sxs-lookup"><span data-stu-id="9d519-172">In this step you will modify it to use [Twitter Bootstrap](https://github.com/twbs/bootstrap), which is a toolkit that makes it easy to design a nice looking website.</span></span>

1. <span data-ttu-id="9d519-173">Baixe e extraia os arquivos para a [Twitter Bootstrap](http://getbootstrap.com/).</span><span class="sxs-lookup"><span data-stu-id="9d519-173">Download and extract the files for [Twitter Bootstrap](http://getbootstrap.com/).</span></span> <span data-ttu-id="9d519-174">Copie o arquivo **bootstrap.min.css** da pasta **bootstrap\\dist\\css** para o diretório **public\\stylesheets** de seu aplicativo de lista de tarefas.</span><span class="sxs-lookup"><span data-stu-id="9d519-174">Copy the **bootstrap.min.css** file from the **bootstrap\\dist\\css** folder to the **public\\stylesheets** directory of your tasklist application.</span></span>
2. <span data-ttu-id="9d519-175">Na pasta **views**, abra o **layout.jade** em seu editor de texto e substitua o conteúdo pelo seguinte:</span><span class="sxs-lookup"><span data-stu-id="9d519-175">From the **views** folder, open the **layout.jade** in your text editor and replace the contents with the following:</span></span>

    <span data-ttu-id="9d519-176">doctype html  html    head      title= title      link(rel='stylesheet', href='/stylesheets/bootstrap.min.css')      link(rel='stylesheet', href='/stylesheets/style.css')    body.app      nav.navbar.navbar-default        div.navbar-header          a.navbar-brand(href='/') My Tasks      block content</span><span class="sxs-lookup"><span data-stu-id="9d519-176">doctype html  html    head      title= title      link(rel='stylesheet', href='/stylesheets/bootstrap.min.css')      link(rel='stylesheet', href='/stylesheets/style.css')    body.app      nav.navbar.navbar-default        div.navbar-header          a.navbar-brand(href='/') My Tasks      block content</span></span>

3. <span data-ttu-id="9d519-177">Salve o arquivo **layout.jade**.</span><span class="sxs-lookup"><span data-stu-id="9d519-177">Save the **layout.jade** file.</span></span>

### <a name="running-the-application-in-the-emulator"></a><span data-ttu-id="9d519-178">Executando o aplicativo no emulador</span><span class="sxs-lookup"><span data-stu-id="9d519-178">Running the Application in the Emulator</span></span>
<span data-ttu-id="9d519-179">Use o seguinte comando para iniciar o aplicativo no emulador.</span><span class="sxs-lookup"><span data-stu-id="9d519-179">Use the following command to start the application in the emulator.</span></span>

```powershell
PS C:\node\tasklist\WebRole1> start-azureemulator -launch
```

<span data-ttu-id="9d519-180">O navegador abrirá e exibirá a página a seguir:</span><span class="sxs-lookup"><span data-stu-id="9d519-180">The browser will open and displays the following page:</span></span>

![Uma página da Web chamada My Task List com uma tabela que contém tarefas e campos para adicionar uma nova tarefa.](./media/storage-nodejs-use-table-storage-cloud-service-app/node44.png)

<span data-ttu-id="9d519-182">Use o formulário para adicionar itens ou remover itens existentes marcando-os como completos.</span><span class="sxs-lookup"><span data-stu-id="9d519-182">Use the form to add items, or remove existing items by marking them as completed.</span></span>

## <a name="publishing-the-application-to-azure"></a><span data-ttu-id="9d519-183">Publicando o aplicativo no Azure</span><span class="sxs-lookup"><span data-stu-id="9d519-183">Publishing the Application to Azure</span></span>
<span data-ttu-id="9d519-184">Na janela do Windows PowerShell, chame o seguinte cmdlet para reimplantar o serviço hospedado no Azure.</span><span class="sxs-lookup"><span data-stu-id="9d519-184">In the Windows PowerShell window, call the following cmdlet to redeploy your hosted service to Azure.</span></span>

```powershell
PS C:\node\tasklist\WebRole1> Publish-AzureServiceProject -name myuniquename -location datacentername -launch
```

<span data-ttu-id="9d519-185">Substitua **myuniquename** por um nome exclusivo para o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="9d519-185">Replace **myuniquename** with a unique name for this application.</span></span> <span data-ttu-id="9d519-186">Substitua **datacentername** pelo nome de um data center do Azure, como **Oeste dos EUA**.</span><span class="sxs-lookup"><span data-stu-id="9d519-186">Replace **datacentername** with the name of an Azure data center, such as **West US**.</span></span>

<span data-ttu-id="9d519-187">Após a conclusão da implantação, você deverá ver uma resposta semelhante ao seguinte:</span><span class="sxs-lookup"><span data-stu-id="9d519-187">After the deployment is complete, you should see a response similar to the following:</span></span>

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

<span data-ttu-id="9d519-188">Da mesma maneira que antes, como você especificou a opção **-launch**, o navegador será aberto e exibirá o aplicativo em execução no Azure quando a publicação for concluída.</span><span class="sxs-lookup"><span data-stu-id="9d519-188">As before, because you specified the **-launch** option, the browser opens and displays your application running in Azure when publishing is completed.</span></span>

![Uma janela do navegador exibindo a página My Task List.](./media/storage-nodejs-use-table-storage-cloud-service-app/getting-started-1.png)

## <a name="stopping-and-deleting-your-application"></a><span data-ttu-id="9d519-191">Parando e excluindo o aplicativo</span><span class="sxs-lookup"><span data-stu-id="9d519-191">Stopping and Deleting Your Application</span></span>
<span data-ttu-id="9d519-192">Depois de implantar o aplicativo, você talvez queira desabilitá-lo, de forma que seja possível evitar os custos ou compilar e implantar outros aplicativos no período de avaliação gratuita.</span><span class="sxs-lookup"><span data-stu-id="9d519-192">After deploying your application, you may want to disable it so you can avoid costs or build and deploy other applications within the free trial time period.</span></span>

<span data-ttu-id="9d519-193">O Azure cobra as instâncias de função web por hora de acordo com o tempo consumido do servidor.</span><span class="sxs-lookup"><span data-stu-id="9d519-193">Azure bills web role instances per hour of server time consumed.</span></span>
<span data-ttu-id="9d519-194">O tempo do servidor é consumido quando seu aplicativo é implantado, mesmo se as instâncias não estiverem sendo executadas e estiverem no estado parado.</span><span class="sxs-lookup"><span data-stu-id="9d519-194">Server time is consumed once your application is deployed, even if the instances are not running and are in the stopped state.</span></span>

<span data-ttu-id="9d519-195">As etapas a seguir mostram como parar e excluir o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="9d519-195">The following steps show you how to stop and delete your application.</span></span>

1. <span data-ttu-id="9d519-196">Na janela do Windows PowerShell, interrompa a implantação do serviço criada na seção anterior com o seguinte cmdlet:</span><span class="sxs-lookup"><span data-stu-id="9d519-196">In the Windows PowerShell window, stop the service deployment created in the previous section with the following cmdlet:</span></span>

    ```powershell
    PS C:\node\tasklist\WebRole1> Stop-AzureService
    ```

   <span data-ttu-id="9d519-197">Interromper o serviço pode levar alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="9d519-197">Stopping the service may take several minutes.</span></span> <span data-ttu-id="9d519-198">Quando o serviço for interrompido, você recebe uma mensagem indicando que foi interrompido.</span><span class="sxs-lookup"><span data-stu-id="9d519-198">When the service is stopped, you receive a message indicating that it has stopped.</span></span>

2. <span data-ttu-id="9d519-199">Para excluir o serviço, chame o seguinte cmdlet:</span><span class="sxs-lookup"><span data-stu-id="9d519-199">To delete the service, call the following cmdlet:</span></span>

    ```powershell
    PS C:\node\tasklist\WebRole1> Remove-AzureService contosotasklist
    ```

   <span data-ttu-id="9d519-200">Quando solicitado, insira **Y** para excluir o serviço.</span><span class="sxs-lookup"><span data-stu-id="9d519-200">When prompted, enter **Y** to delete the service.</span></span>

   <span data-ttu-id="9d519-201">Excluir o serviço pode levar alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="9d519-201">Deleting the service may take several minutes.</span></span> <span data-ttu-id="9d519-202">Após o serviço ter sido excluído, você recebe uma mensagem indicando que o serviço foi excluído.</span><span class="sxs-lookup"><span data-stu-id="9d519-202">After the service has been deleted you receive a message indicating that the service was deleted.</span></span>

<span data-ttu-id="9d519-203">[Aplicativo Web do Node.js usando o Express]: http://azure.microsoft.com/develop/nodejs/tutorials/web-app-with-express/</span><span class="sxs-lookup"><span data-stu-id="9d519-203">[Node.js Web Application using Express]: http://azure.microsoft.com/develop/nodejs/tutorials/web-app-with-express/</span></span>
<span data-ttu-id="9d519-204">[Armazenando e acessando dados no Azure]: http://msdn.microsoft.com/library/azure/gg433040.aspx</span><span class="sxs-lookup"><span data-stu-id="9d519-204">[Storing and Accessing Data in Azure]: http://msdn.microsoft.com/library/azure/gg433040.aspx</span></span>
<span data-ttu-id="9d519-205">[Aplicativo Web do Node.js]: http://azure.microsoft.com/develop/nodejs/tutorials/getting-started/</span><span class="sxs-lookup"><span data-stu-id="9d519-205">[Node.js Web Application]: http://azure.microsoft.com/develop/nodejs/tutorials/getting-started/</span></span>


