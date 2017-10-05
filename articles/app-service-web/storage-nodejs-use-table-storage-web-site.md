---
title: "Aplicativo Web Node.js com o Serviço Tabela do Azure"
description: "Esse tutorial ensina a usar o serviço Tabela do Azure para armazenar dados de um aplicativo Node.js hospedado em Aplicativos Web do Serviço de Aplicativo do Azure."
tags: azure-portal
services: app-service\web, storage
documentationcenter: nodejs
author: TomArcher
manager: routlaw
editor: 
ms.assetid: 029e6f46-f586-4309-adbf-71c7b8d537d4
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 08/17/2016
ms.author: tarcher
ms.openlocfilehash: 3252914934c1084a165fa39ee983d3039e04d567
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="nodejs-web-app-using-the-azure-table-service"></a><span data-ttu-id="74665-103">Aplicativo Web Node.js com o Serviço Tabela do Azure</span><span class="sxs-lookup"><span data-stu-id="74665-103">Node.js web app using the Azure Table Service</span></span>
## <a name="overview"></a><span data-ttu-id="74665-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="74665-104">Overview</span></span>
<span data-ttu-id="74665-105">Este tutorial mostra como usar o serviço Tabela fornecido pelo Gerenciamento de Dados do Azure para armazenar e acessar dados em um aplicativo de [node] hospedado nos Aplicativos Web do [Serviço de Aplicativo do Azure](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="74665-105">This tutorial shows you how to use Table service provided by Azure Data Management to store and access data from a [node] application hosted in [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) Web Apps.</span></span> <span data-ttu-id="74665-106">Este tutorial pressupõe que você tenha alguma experiência anterior usando nó e [Git].</span><span class="sxs-lookup"><span data-stu-id="74665-106">This tutorial assumes that you have some prior experience using node and [Git].</span></span>

<span data-ttu-id="74665-107">Você aprenderá:</span><span class="sxs-lookup"><span data-stu-id="74665-107">You will learn:</span></span>

* <span data-ttu-id="74665-108">Como usar npm (gerenciador de pacote de nós) para instalar os módulos do nó</span><span class="sxs-lookup"><span data-stu-id="74665-108">How to use npm (node package manager) to install the node modules</span></span>
* <span data-ttu-id="74665-109">Como trabalhar com o serviço de Tabela do Azure</span><span class="sxs-lookup"><span data-stu-id="74665-109">How to work with the Azure Table service</span></span>
* <span data-ttu-id="74665-110">Como usar a CLI do Azure para criar um aplicativo da web.</span><span class="sxs-lookup"><span data-stu-id="74665-110">How to use the Azure CLI to create a web app.</span></span>

<span data-ttu-id="74665-111">Seguindo este tutorial, você criará um aplicativo simples de “lista de tarefas” baseado na web, que permite criar, recuperar e concluir tarefas.</span><span class="sxs-lookup"><span data-stu-id="74665-111">By following this tutorial, you will build a simple web-based "to-do list" application that allows creating, retrieving and completing tasks.</span></span> <span data-ttu-id="74665-112">As tarefas são armazenadas no serviço Tabela.</span><span class="sxs-lookup"><span data-stu-id="74665-112">The tasks are stored in the Table service.</span></span>

<span data-ttu-id="74665-113">Aqui está o aplicativo concluído:</span><span class="sxs-lookup"><span data-stu-id="74665-113">Here is the completed application:</span></span>

![Uma página da Web que exibe uma lista de tarefas vazia][node-table-finished]

> [!NOTE]
> <span data-ttu-id="74665-115">Se você deseja começar com o Serviço de Aplicativo do Azure antes de se inscrever em uma conta do Azure, acesse [Experimentar o Serviço de Aplicativo](https://azure.microsoft.com/try/app-service/), em que você pode criar imediatamente um aplicativo Web inicial de curta duração no Serviço de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="74665-115">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="74665-116">Nenhum cartão de crédito é exigido, sem compromissos.</span><span class="sxs-lookup"><span data-stu-id="74665-116">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="74665-117">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="74665-117">Prerequisites</span></span>
<span data-ttu-id="74665-118">Antes de seguir as instruções deste artigo, verifique se você tem os seguintes itens instalados:</span><span class="sxs-lookup"><span data-stu-id="74665-118">Before following the instructions in this article, ensure that you have the following installed:</span></span>

* <span data-ttu-id="74665-119">[node] versão 0.10.24 ou superior</span><span class="sxs-lookup"><span data-stu-id="74665-119">[node] version 0.10.24 or higher</span></span>
* <span data-ttu-id="74665-120">[Git]</span><span class="sxs-lookup"><span data-stu-id="74665-120">[Git]</span></span>

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

## <a name="create-a-storage-account"></a><span data-ttu-id="74665-121">Criar uma conta de armazenamento</span><span class="sxs-lookup"><span data-stu-id="74665-121">Create a storage account</span></span>
<span data-ttu-id="74665-122">Crie uma conta de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="74665-122">Create an Azure storage account.</span></span> <span data-ttu-id="74665-123">O aplicativo usará essa conta para armazenar os itens pendentes.</span><span class="sxs-lookup"><span data-stu-id="74665-123">The app will use this account to store the to-do items.</span></span>

1. <span data-ttu-id="74665-124">Faça logon no [Portal do Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="74665-124">Log into the [Azure Portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="74665-125">Clique no ícone **Novo** na parte inferior esquerda do portal e clique em **Dados + Armazenamento** > **Armazenamento**.</span><span class="sxs-lookup"><span data-stu-id="74665-125">Click the **New** icon on the bottom left of the portal, then click **Data + Storage** > **Storage**.</span></span> <span data-ttu-id="74665-126">Dê um nome exclusivo à conta de armazenamento e crie um novo [grupo de recursos](../azure-resource-manager/resource-group-overview.md) para ela.</span><span class="sxs-lookup"><span data-stu-id="74665-126">Give the storage account a unique name and create a new [resource group](../azure-resource-manager/resource-group-overview.md) for it.</span></span>
   
      ![Botão Novo](./media/storage-nodejs-use-table-storage-web-site/configure-storage.png)
   
    <span data-ttu-id="74665-128">Quando a conta de armazenamento for criada, o botão **Notificações** piscará **ÊXITO** em verde e a folha da conta de armazenamento será aberta para mostrar que pertence ao novo grupo de recursos criado.</span><span class="sxs-lookup"><span data-stu-id="74665-128">When the storage account has been created, the **Notifications** button will flash a green **SUCCESS** and the storage account's blade is open to show that it belongs to the new resource group you created.</span></span>
3. <span data-ttu-id="74665-129">Na folha da conta de armazenamento, clique em **Configurações** > **Chaves**.</span><span class="sxs-lookup"><span data-stu-id="74665-129">In the storage account's blade, click **Settings** > **Keys**.</span></span> <span data-ttu-id="74665-130">Copie a chave de acesso primário para a área de transferência.</span><span class="sxs-lookup"><span data-stu-id="74665-130">Copy the primary access key to the clipboard.</span></span>
   
    ![Chave de acesso][portal-storage-access-keys]

## <a name="install-modules-and-generate-scaffolding"></a><span data-ttu-id="74665-132">Instalar módulos e gerar scaffolding</span><span class="sxs-lookup"><span data-stu-id="74665-132">Install modules and generate scaffolding</span></span>
<span data-ttu-id="74665-133">Nesta seção você criará um novo aplicativo de nó e usará o npm para adicionar pacotes de módulo.</span><span class="sxs-lookup"><span data-stu-id="74665-133">In this section you will create a new Node application and use npm to add module packages.</span></span> <span data-ttu-id="74665-134">Para este aplicativo, você usará os módulos [Express] e [Azure].</span><span class="sxs-lookup"><span data-stu-id="74665-134">For this application you will use the [Express] and [Azure] modules.</span></span> <span data-ttu-id="74665-135">O módulo Express fornece uma estrutura de Controlador da Exibição do Modelo para o nó, enquanto que os módulos do Azure fornecem a conectividade ao serviço de Tabela.</span><span class="sxs-lookup"><span data-stu-id="74665-135">The Express module provides a Model View Controller framework for node, while the Azure modules provides connectivity to the Table service.</span></span>

### <a name="install-express-and-generate-scaffolding"></a><span data-ttu-id="74665-136">Instalar o express e gerar scaffolding</span><span class="sxs-lookup"><span data-stu-id="74665-136">Install express and generate scaffolding</span></span>
1. <span data-ttu-id="74665-137">Na linha de comando, crie um novo diretório chamado **tasklist** e alterne para esse diretório.</span><span class="sxs-lookup"><span data-stu-id="74665-137">From the command line, create a new directory named **tasklist** and switch to that directory.</span></span>  
2. <span data-ttu-id="74665-138">Digite o comando a seguir para instalar o módulo Express.</span><span class="sxs-lookup"><span data-stu-id="74665-138">Enter the following command to install the Express module.</span></span>
   
        npm install express-generator@4.2.0 -g
   
    <span data-ttu-id="74665-139">Dependendo do sistema operacional, talvez seja necessário colocar ‘sudo’ antes do comando:</span><span class="sxs-lookup"><span data-stu-id="74665-139">Depending on the operating system, you may need to put 'sudo' before the command:</span></span>
   
        sudo npm install express-generator@4.2.0 -g
   
    <span data-ttu-id="74665-140">A saída é semelhante a este exemplo:</span><span class="sxs-lookup"><span data-stu-id="74665-140">The output appears similar to the following example:</span></span>
   
        express-generator@4.2.0 /usr/local/lib/node_modules/express-generator
        ├── mkdirp@0.3.5
        └── commander@1.3.2 (keypress@0.1.0)
   
   > [!NOTE]
   > <span data-ttu-id="74665-141">O parâmetro '-g' instala o módulo de forma global.</span><span class="sxs-lookup"><span data-stu-id="74665-141">The '-g' parameter installs the module globally.</span></span> <span data-ttu-id="74665-142">Desse modo, podemos usar **express** para gerar o scaffolding do aplicativo Web sem precisar digitar informações adicionais de caminho.</span><span class="sxs-lookup"><span data-stu-id="74665-142">That way, we can use **express** to generate web app scaffolding without having to type in additional path information.</span></span>
   > 
   > 
3. <span data-ttu-id="74665-143">Para criar o scaffolding do aplicativo, digite o comando **express** :</span><span class="sxs-lookup"><span data-stu-id="74665-143">To create the scaffolding for the application, enter the **express** command:</span></span>
   
        express
   
    <span data-ttu-id="74665-144">A saída deste comando é semelhante a este exemplo:</span><span class="sxs-lookup"><span data-stu-id="74665-144">The output of this command appears similar to the following example:</span></span>
   
           create : .
           create : ./package.json
           create : ./app.js
           create : ./public
           create : ./public/images
           create : ./routes
           create : ./routes/index.js
           create : ./routes/users.js
           create : ./public/stylesheets
           create : ./public/stylesheets/style.css
           create : ./views
           create : ./views/index.jade
           create : ./views/layout.jade
           create : ./views/error.jade
           create : ./public/javascripts
           create : ./bin
           create : ./bin/www
   
           install dependencies:
             $ cd . && npm install
   
           run the app:
             $ DEBUG=my-application ./bin/www
   
    <span data-ttu-id="74665-145">Agora, você terá vários novos diretórios e arquivos no diretório **tasklist** .</span><span class="sxs-lookup"><span data-stu-id="74665-145">You now have several new directories and files in the **tasklist** directory.</span></span>

### <a name="install-additional-modules"></a><span data-ttu-id="74665-146">Instalar módulos adicionais</span><span class="sxs-lookup"><span data-stu-id="74665-146">Install additional modules</span></span>
<span data-ttu-id="74665-147">Um dos arquivos criados por **express** é **package.json**.</span><span class="sxs-lookup"><span data-stu-id="74665-147">One of the files that **express** creates is **package.json**.</span></span> <span data-ttu-id="74665-148">Esse arquivo contém uma lista das dependências do módulo.</span><span class="sxs-lookup"><span data-stu-id="74665-148">This file contains a list of module dependencies.</span></span> <span data-ttu-id="74665-149">Posteriormente, quando você implantar esse aplicativo nos Aplicativos Web do Serviço de Aplicativo, esse arquivo será usado para determinar quais módulos precisam ser instalados no Azure.</span><span class="sxs-lookup"><span data-stu-id="74665-149">Later, when you deploy the application to App Service Web Apps, this file determines which modules need to be installed on Azure.</span></span>

<span data-ttu-id="74665-150">Na linha de comando, digite o comando a seguir para instalar os módulos descritos no arquivo **package.json** .</span><span class="sxs-lookup"><span data-stu-id="74665-150">From the command-line, enter the following command to install the modules described in the **package.json** file.</span></span> <span data-ttu-id="74665-151">Talvez seja necessário usar 'sudo'.</span><span class="sxs-lookup"><span data-stu-id="74665-151">You may need to use 'sudo'.</span></span>

    npm install

<span data-ttu-id="74665-152">A saída deste comando é semelhante a este exemplo:</span><span class="sxs-lookup"><span data-stu-id="74665-152">The output of this command appears similar to the following example:</span></span>

    debug@0.7.4 node_modules\debug

    cookie-parser@1.0.1 node_modules\cookie-parser
    ├── cookie-signature@1.0.3
    └── cookie@0.1.0

    [...]


<span data-ttu-id="74665-153">Em seguida, insira o seguinte comando para instalar os módulos [azure], [node-uuid], [nconf] e [async]:</span><span class="sxs-lookup"><span data-stu-id="74665-153">Next, enter the following command to install the [azure], [node-uuid], [nconf] and [async] modules:</span></span>

    npm install azure-storage node-uuid async nconf --save

<span data-ttu-id="74665-154">O sinalizador **--save** adiciona entradas para esses módulos ao arquivo **package.json**.</span><span class="sxs-lookup"><span data-stu-id="74665-154">The **--save** flag adds entries for these modules to the **package.json** file.</span></span>

<span data-ttu-id="74665-155">A saída deste comando é semelhante a este exemplo:</span><span class="sxs-lookup"><span data-stu-id="74665-155">The output of this command appears similar to the following example:</span></span>

    async@0.9.0 node_modules\async

    node-uuid@1.4.1 node_modules\node-uuid

    nconf@0.6.9 node_modules\nconf
    ├── ini@1.2.1
    ├── async@0.2.9
    └── optimist@0.6.0 (wordwrap@0.0.2, minimist@0.0.10)

    [...]


## <a name="create-the-application"></a><span data-ttu-id="74665-156">Criar o aplicativo</span><span class="sxs-lookup"><span data-stu-id="74665-156">Create the application</span></span>
<span data-ttu-id="74665-157">Agora estamos prontos para criar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="74665-157">Now we're ready to build the application.</span></span>

### <a name="create-a-model"></a><span data-ttu-id="74665-158">Criar um modelo</span><span class="sxs-lookup"><span data-stu-id="74665-158">Create a model</span></span>
<span data-ttu-id="74665-159">Um *modelo* é um objeto que representa os dados no seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="74665-159">A *model* is an object that represents the data in your application.</span></span> <span data-ttu-id="74665-160">Para o aplicativo, o único modelo é um objeto de tarefa, que representa um item da lista de tarefas pendentes.</span><span class="sxs-lookup"><span data-stu-id="74665-160">For the application, the only model is a task object, which represents an item in the to-do list.</span></span> <span data-ttu-id="74665-161">As tarefas terão os seguintes campos:</span><span class="sxs-lookup"><span data-stu-id="74665-161">Tasks will have the following fields:</span></span>

* <span data-ttu-id="74665-162">PartitionKey</span><span class="sxs-lookup"><span data-stu-id="74665-162">PartitionKey</span></span>
* <span data-ttu-id="74665-163">RowKey</span><span class="sxs-lookup"><span data-stu-id="74665-163">RowKey</span></span>
* <span data-ttu-id="74665-164">nome (cadeia de caracteres)</span><span class="sxs-lookup"><span data-stu-id="74665-164">name (string)</span></span>
* <span data-ttu-id="74665-165">categoria (cadeia de caracteres)</span><span class="sxs-lookup"><span data-stu-id="74665-165">category (string)</span></span>
* <span data-ttu-id="74665-166">concluído (booleano)</span><span class="sxs-lookup"><span data-stu-id="74665-166">completed (Boolean)</span></span>

<span data-ttu-id="74665-167">**PartitionKey** e **RowKey** são usados pelo serviço Tabela como chaves de tabela.</span><span class="sxs-lookup"><span data-stu-id="74665-167">**PartitionKey** and **RowKey** are used by the Table Service as table keys.</span></span> <span data-ttu-id="74665-168">Para obter informações, consulte [Noções básicas sobre o modelo de dados do serviço Tabela](https://msdn.microsoft.com/library/azure/dd179338.aspx).</span><span class="sxs-lookup"><span data-stu-id="74665-168">For more information, see [Understanding the Table Service data model](https://msdn.microsoft.com/library/azure/dd179338.aspx).</span></span>

1. <span data-ttu-id="74665-169">No diretório **tasklist**, crie um novo diretório com nome **models**.</span><span class="sxs-lookup"><span data-stu-id="74665-169">In the **tasklist** directory, create a new directory named **models**.</span></span>
2. <span data-ttu-id="74665-170">No diretório **models**, crie um novo arquivo chamado **task.js**.</span><span class="sxs-lookup"><span data-stu-id="74665-170">In the **models** directory, create a new file named **task.js**.</span></span> <span data-ttu-id="74665-171">Esse arquivo vai conter o modelo para as tarefas criadas pelo seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="74665-171">This file will contain the model for the tasks created by your application.</span></span>
3. <span data-ttu-id="74665-172">No início do arquivo **task.js** , adicione o seguinte código para fazer a referência às bibliotecas necessárias:</span><span class="sxs-lookup"><span data-stu-id="74665-172">At the beginning of the **task.js** file, add the following code to reference required libraries:</span></span>
   
        var azure = require('azure-storage');
          var uuid = require('node-uuid');
        var entityGen = azure.TableUtilities.entityGenerator;
4. <span data-ttu-id="74665-173">Adicione o código a seguir para definir e exportar o objeto de tarefa.</span><span class="sxs-lookup"><span data-stu-id="74665-173">Add the following code to define and export the Task object.</span></span> <span data-ttu-id="74665-174">Este objeto é responsável por se conectar à tabela.</span><span class="sxs-lookup"><span data-stu-id="74665-174">This object is responsible for connecting to the table.</span></span>
   
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
5. <span data-ttu-id="74665-175">Adicione o seguinte código para definir métodos adicionais no objeto de tarefa, os quais permitem interações com os dados armazenados na tabela:</span><span class="sxs-lookup"><span data-stu-id="74665-175">Add the following code to define additional methods on the Task object, which allow interactions with data stored in the table:</span></span>
   
        Task.prototype = {
          find: function(query, callback) {
            self = this;
            self.storageClient.queryEntities(this.tableName, query, null, function entitiesQueried(error, result) {
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
6. <span data-ttu-id="74665-176">Salve e feche o arquivo **task.js** .</span><span class="sxs-lookup"><span data-stu-id="74665-176">Save and close the **task.js** file.</span></span>

### <a name="create-a-controller"></a><span data-ttu-id="74665-177">Criar um controlador</span><span class="sxs-lookup"><span data-stu-id="74665-177">Create a controller</span></span>
<span data-ttu-id="74665-178">O *controlador* trata as solicitações HTTP e renderiza a resposta HTML.</span><span class="sxs-lookup"><span data-stu-id="74665-178">A *controller* handles HTTP requests and renders the HTML response.</span></span>

1. <span data-ttu-id="74665-179">No diretório **tasklist/routes**, crie um novo arquivo chamado **tasklist.js** e abra-o em um editor de texto.</span><span class="sxs-lookup"><span data-stu-id="74665-179">In the **tasklist/routes** directory, create a new file named **tasklist.js** and open it in a text editor.</span></span>
2. <span data-ttu-id="74665-180">Adicione os seguintes códigos ao **tasklist.js**.</span><span class="sxs-lookup"><span data-stu-id="74665-180">Add the following code to **tasklist.js**.</span></span> <span data-ttu-id="74665-181">Isso carrega os módulos azure e async, que são usados por **tasklist.js**.</span><span class="sxs-lookup"><span data-stu-id="74665-181">This loads the azure and async modules, which are used by **tasklist.js**.</span></span> <span data-ttu-id="74665-182">Isso também define a função de **TaskList**, que é transmitida a uma instância do objeto da **Task** definido anteriormente:</span><span class="sxs-lookup"><span data-stu-id="74665-182">This also defines the **TaskList** function, which is passed an instance of the **Task** object we defined earlier:</span></span>
   
        var azure = require('azure-storage');
        var async = require('async');
   
        module.exports = TaskList;
3. <span data-ttu-id="74665-183">Defina um objeto **TaskList** .</span><span class="sxs-lookup"><span data-stu-id="74665-183">Define a **TaskList** object.</span></span>
   
        function TaskList(task) {
          this.task = task;
        }
4. <span data-ttu-id="74665-184">Adicione os seguintes métodos à **TaskList**:</span><span class="sxs-lookup"><span data-stu-id="74665-184">Add the following methods to **TaskList**:</span></span>
   
        TaskList.prototype = {
          showTasks: function(req, res) {
            self = this;
            var query = new azure.TableQuery()
              .where('completed eq ?', false);
            self.task.find(query, function itemsFound(error, items) {
              res.render('index',{title: 'My ToDo List ', tasks: items});
            });
          },
   
          addTask: function(req,res) {
            var self = this;
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

### <a name="modify-appjs"></a><span data-ttu-id="74665-185">Modificar app.js</span><span class="sxs-lookup"><span data-stu-id="74665-185">Modify app.js</span></span>
1. <span data-ttu-id="74665-186">No diretório **tasklist**, abra o arquivo **app.js**.</span><span class="sxs-lookup"><span data-stu-id="74665-186">From the **tasklist** directory, open the **app.js** file.</span></span> <span data-ttu-id="74665-187">Este arquivo foi criado anteriormente usando o comando **express** .</span><span class="sxs-lookup"><span data-stu-id="74665-187">This file was created earlier by running the **express** command.</span></span>
2. <span data-ttu-id="74665-188">No início do arquivo, adicione o seguinte para carregar o módulo azure, definir o nome da tabela, a chave de partição e definir as credenciais de armazenamento usadas neste exemplo:</span><span class="sxs-lookup"><span data-stu-id="74665-188">At the beginning of the file, add the following to load the azure module, set the table name, partition key, and set the storage credentials used by this example:</span></span>
   
        var azure = require('azure-storage');
        var nconf = require('nconf');
        nconf.env()
             .file({ file: 'config.json', search: true });
        var tableName = nconf.get("TABLE_NAME");
        var partitionKey = nconf.get("PARTITION_KEY");
        var accountName = nconf.get("STORAGE_NAME");
        var accountKey = nconf.get("STORAGE_KEY");
   
   > [!NOTE]
   > <span data-ttu-id="74665-189">nconf carregará os valores de configuração de uma das variáveis de ambiente ou o arquivo **config.json** , que será criado posteriormente.</span><span class="sxs-lookup"><span data-stu-id="74665-189">nconf will load the configuration values from either environment variables or the **config.json** file, which we will create later.</span></span>
   > 
   > 
3. <span data-ttu-id="74665-190">No arquivo app.js, role para baixo até onde for capaz de visualizar a seguinte linha:</span><span class="sxs-lookup"><span data-stu-id="74665-190">In the app.js file, scroll down to where you see the following line:</span></span>
   
        app.use('/', routes);
        app.use('/users', users);
   
    <span data-ttu-id="74665-191">Substitua as linhas acima pelo código mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="74665-191">Replace the above lines with the code shown below.</span></span> <span data-ttu-id="74665-192">Será inicializada uma instância de <strong>Tarefa</strong> com uma conexão à sua conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="74665-192">This will initialize an instance of <strong>Task</strong> with a connection to your storage account.</span></span> <span data-ttu-id="74665-193">Ela será transmitida à <strong>TaskList</strong>, que a usará para se comunicar com o serviço Tabela:</span><span class="sxs-lookup"><span data-stu-id="74665-193">This is passed to the <strong>TaskList</strong>, which will use it to communicate with the Table service:</span></span>
   
        var TaskList = require('./routes/tasklist');
        var Task = require('./models/task');
        var task = new Task(azure.createTableService(accountName, accountKey), tableName, partitionKey);
        var taskList = new TaskList(task);
   
        app.get('/', taskList.showTasks.bind(taskList));
        app.post('/addtask', taskList.addTask.bind(taskList));
        app.post('/completetask', taskList.completeTask.bind(taskList));
4. <span data-ttu-id="74665-194">Salve o arquivo **app.js** .</span><span class="sxs-lookup"><span data-stu-id="74665-194">Save the **app.js** file.</span></span>

### <a name="modify-the-index-view"></a><span data-ttu-id="74665-195">Modificar a exibição de índice</span><span class="sxs-lookup"><span data-stu-id="74665-195">Modify the index view</span></span>
1. <span data-ttu-id="74665-196">Abra o arquivo **tasklist/views/index.jade** em um editor de texto.</span><span class="sxs-lookup"><span data-stu-id="74665-196">Open the **tasklist/views/index.jade** file in a text editor.</span></span>
2. <span data-ttu-id="74665-197">Substitua todo o conteúdo do arquivo pelo código a seguir.</span><span class="sxs-lookup"><span data-stu-id="74665-197">Replace the entire contents of the file with the following code.</span></span> <span data-ttu-id="74665-198">Isso define o modo de exibição das tarefas existentes, bem como um formulário para adicionar novas tarefas e marcar as tarefas existentes como concluídas.</span><span class="sxs-lookup"><span data-stu-id="74665-198">This defines a view that displays existing tasks and includes a form for adding new tasks and marking existing ones as completed.</span></span>
   
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
              if (typeof tasks === "undefined")
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
3. <span data-ttu-id="74665-199">Salve e feche o arquivo **index.jade** .</span><span class="sxs-lookup"><span data-stu-id="74665-199">Save and close **index.jade** file.</span></span>

### <a name="modify-the-global-layout"></a><span data-ttu-id="74665-200">Modificar o layout global</span><span class="sxs-lookup"><span data-stu-id="74665-200">Modify the global layout</span></span>
<span data-ttu-id="74665-201">O arquivo **layout.jade** no diretório **views** é usado como um modelo global para outros arquivos **.jade**.</span><span class="sxs-lookup"><span data-stu-id="74665-201">The **layout.jade** file in the **views** directory is a global template for other **.jade** files.</span></span> <span data-ttu-id="74665-202">Nesta etapa, você o modificará para usar a [Twitter Bootstrap](https://github.com/twbs/bootstrap), que é um kit de ferramentas que facilita a criação de um aplicativo Web com uma aparência interessante.</span><span class="sxs-lookup"><span data-stu-id="74665-202">In this step you will modify it to use [Twitter Bootstrap](https://github.com/twbs/bootstrap), which is a toolkit that makes it easy to design a nice looking web app.</span></span>

<span data-ttu-id="74665-203">Baixe e extraia os arquivos para a [Twitter Bootstrap](http://getbootstrap.com/).</span><span class="sxs-lookup"><span data-stu-id="74665-203">Download and extract the files for [Twitter Bootstrap](http://getbootstrap.com/).</span></span> <span data-ttu-id="74665-204">Copie o arquivo **bootstrap.min.css** da pasta **css** do Bootstrap para o diretório **public/stylesheets** do seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="74665-204">Copy the **bootstrap.min.css** file from the Bootstrap **css** folder into the **public/stylesheets** directory of your application.</span></span>

<span data-ttu-id="74665-205">Na pasta **views**, abra o **layout.jade** e substitua todo o seu conteúdo pelo seguinte:</span><span class="sxs-lookup"><span data-stu-id="74665-205">From the **views** folder, open **layout.jade** and replace the entire contents with the following:</span></span>

    doctype html
    html
      head
        title= title
        link(rel='stylesheet', href='/stylesheets/bootstrap.min.css')
        link(rel='stylesheet', href='/stylesheets/style.css')
      body.app
        nav.navbar.navbar-default
          div.navbar-header
          a.navbar-brand(href='/') My Tasks
        block content

### <a name="create-a-config-file"></a><span data-ttu-id="74665-206">Criar um arquivo de configuração</span><span class="sxs-lookup"><span data-stu-id="74665-206">Create a config file</span></span>
<span data-ttu-id="74665-207">Para executar o aplicativo localmente, colocaremos as credenciais de Armazenamento do Azure em um arquivo de configuração.</span><span class="sxs-lookup"><span data-stu-id="74665-207">To run the app locally, we'll put Azure Storage credentials into a config file.</span></span> <span data-ttu-id="74665-208">Crie um arquivo chamado **config.json** com o JSON a seguir:</span><span class="sxs-lookup"><span data-stu-id="74665-208">Create a file named **config.json* *with the following JSON:</span></span>

    {
        "STORAGE_NAME": "<storage account name>",
        "STORAGE_KEY": "<storage access key>",
        "PARTITION_KEY": "mytasks",
        "TABLE_NAME": "tasks"
    }

<span data-ttu-id="74665-209">Substitua **nome da conta de armazenamento** pelo nome da conta de armazenamento criada anteriormente e substitua **chave de acesso de armazenamento** pela chave de acesso primário da sua conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="74665-209">Replace **storage account name** with the name of the storage account you created earlier, and replace **storage access key** with the primary access key for your storage account.</span></span> <span data-ttu-id="74665-210">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="74665-210">For example:</span></span>

    {
        "STORAGE_NAME": "nodejsappstorage",
        "STORAGE_KEY": "KG0oDd..."
        "PARTITION_KEY": "mytasks",
        "TABLE_NAME": "tasks"
    }

<span data-ttu-id="74665-211">Salve esse arquivo em *um nível de diretório superior* ao do diretório **tasklist** , como este:</span><span class="sxs-lookup"><span data-stu-id="74665-211">Save this file *one directory level higher* than the **tasklist** directory, like this:</span></span>

    parent/
      |-- config.json
      |-- tasklist/

<span data-ttu-id="74665-212">A razão para isso é evitar a verificação do arquivo de configuração no controle de origem, onde ele pode se tornar público.</span><span class="sxs-lookup"><span data-stu-id="74665-212">The reason for doing this is to avoid checking the config file into source control, where it might become public.</span></span> <span data-ttu-id="74665-213">Ao implantar o aplicativo no Azure, usaremos as variáveis de ambiente em vez de um arquivo de configuração.</span><span class="sxs-lookup"><span data-stu-id="74665-213">When we deploy the app to Azure, we will use environment variables instead of a config file.</span></span>

## <a name="run-the-application-locally"></a><span data-ttu-id="74665-214">Executar o aplicativo localmente</span><span class="sxs-lookup"><span data-stu-id="74665-214">Run the application locally</span></span>
<span data-ttu-id="74665-215">Execute as etapas a seguir para testar o aplicativo em seu computador local:</span><span class="sxs-lookup"><span data-stu-id="74665-215">To test the application on your local machine, perform the following steps:</span></span>

1. <span data-ttu-id="74665-216">Da linha de comando, mude os diretórios para o diretório **tasklist** .</span><span class="sxs-lookup"><span data-stu-id="74665-216">From the command-line, change directories to the **tasklist** directory.</span></span>
2. <span data-ttu-id="74665-217">Use o seguinte comando para iniciar o aplicativo localmente:</span><span class="sxs-lookup"><span data-stu-id="74665-217">Use the following command to launch the application locally:</span></span>
   
        npm start
3. <span data-ttu-id="74665-218">Abra um navegador da Web e navegue até http://127.0.0.1:3000.</span><span class="sxs-lookup"><span data-stu-id="74665-218">Open a web browser and navigate to http://127.0.0.1:3000.</span></span>
   
    <span data-ttu-id="74665-219">A saída da página Web semelhante ao exemplo a seguir aparece.</span><span class="sxs-lookup"><span data-stu-id="74665-219">A web page similar to the following example appears.</span></span>
   
    ![Uma página da Web que exibe uma lista de tarefas vazia][node-table-finished]
4. <span data-ttu-id="74665-221">Para criar um novo item pendente, insira um nome e uma categoria e clique em **Adicionar item**.</span><span class="sxs-lookup"><span data-stu-id="74665-221">To create a new to-do item, enter a name and category and click **Add Item**.</span></span> 
5. <span data-ttu-id="74665-222">Para marcar uma tarefa como concluída, marque **Concluir** e clique em **Atualizar Tarefas**.</span><span class="sxs-lookup"><span data-stu-id="74665-222">To mark a task as complete, check **Complete** and click **Update Tasks**.</span></span>
   
    ![Uma imagem do novo item na lista de tarefas][node-table-list-items]

<span data-ttu-id="74665-224">Mesmo que o aplicativo seja executado localmente, ele armazena os dados no serviço Tabela do Azure.</span><span class="sxs-lookup"><span data-stu-id="74665-224">Even though the application is running locally, it is storing the data in the Azure Table service.</span></span>

## <a name="deploy-your-application-to-azure"></a><span data-ttu-id="74665-225">Implantar seu aplicativo no Azure</span><span class="sxs-lookup"><span data-stu-id="74665-225">Deploy your application to Azure</span></span>
<span data-ttu-id="74665-226">As etapas desta seção usam as ferramentas de linha de comando do Azure para criar um novo aplicativo Web no Serviço de Aplicativo do Azure e, em seguida, usam o Git para implantar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="74665-226">The steps in this section use the Azure command-line tools to create a new web app in App Service, and then use Git to deploy your application.</span></span> <span data-ttu-id="74665-227">Para realizar essas etapas, você deve ter uma assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="74665-227">To perform these steps you must have an Azure subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="74665-228">Essas etapas também podem ser executadas usando o [Portal do Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="74665-228">These steps can also be performed by using the [Azure Portal](https://portal.azure.com/).</span></span> <span data-ttu-id="74665-229">Confira [Criar e implantar um aplicativo Web do Node.js no Serviço de Aplicativo do Azure].</span><span class="sxs-lookup"><span data-stu-id="74665-229">See [Build and deploy a Node.js web app in Azure App Service].</span></span>
> 
> <span data-ttu-id="74665-230">Se esse for o primeiro aplicativo web que você criou, use o Portal do Azure para implantar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="74665-230">If this is the first web app you have created, you must use the Azure Portal to deploy this application.</span></span>
> 
> 

<span data-ttu-id="74665-231">Para começar, instale a [CLI do Azure] inserindo o seguinte comando na linha de comando:</span><span class="sxs-lookup"><span data-stu-id="74665-231">To get started, install the [Azure CLI] by entering the following command from the command line:</span></span>

    npm install azure-cli -g

### <a name="import-publishing-settings"></a><span data-ttu-id="74665-232">Importar configurações de publicação</span><span class="sxs-lookup"><span data-stu-id="74665-232">Import publishing settings</span></span>
<span data-ttu-id="74665-233">Nesta etapa, você baixará um arquivo que contém informações sobre sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="74665-233">In this step, you will download a file containing information about your subscription.</span></span>

1. <span data-ttu-id="74665-234">Digite o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="74665-234">Enter the following command:</span></span>
   
        azure login
   
    <span data-ttu-id="74665-235">Esse comando inicia um navegador e acessa a página de download.</span><span class="sxs-lookup"><span data-stu-id="74665-235">This command launches a browser and navigates to the download page.</span></span> <span data-ttu-id="74665-236">Se solicitado, faça o logon usando a conta associada à sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="74665-236">If prompted, log in with the account associated with your Azure subscription.</span></span>
   
    <!-- ![The download page][download-publishing-settings] -->
   
    <span data-ttu-id="74665-237">O download do arquivo começa automaticamente. Se não, você pode clicar no link no início da página para baixar manualmente o arquivo.</span><span class="sxs-lookup"><span data-stu-id="74665-237">The file download begins automatically; if it does not, you can click the link at the beginning of the page to manually download the file.</span></span> <span data-ttu-id="74665-238">Salve o arquivo e anote o caminho do arquivo.</span><span class="sxs-lookup"><span data-stu-id="74665-238">Save the file and note the file path.</span></span>
2. <span data-ttu-id="74665-239">Digite o seguinte comando para importar as configurações:</span><span class="sxs-lookup"><span data-stu-id="74665-239">Enter the following command to import the settings:</span></span>
   
        azure account import <path-to-file>
   
    <span data-ttu-id="74665-240">Especifique o caminho e o nome do arquivo de configurações de publicação que você baixou na etapa anterior.</span><span class="sxs-lookup"><span data-stu-id="74665-240">Specify the path and file name of the publishing settings file you downloaded in the previous step.</span></span>
3. <span data-ttu-id="74665-241">Depois que as configurações forem importadas, exclua o arquivo de configurações de publicação.</span><span class="sxs-lookup"><span data-stu-id="74665-241">After the settings are imported, delete the publish settings file.</span></span> <span data-ttu-id="74665-242">Ele não é mais necessário e contém informações confidenciais sobre sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="74665-242">It is no longer needed, and contains sensitive information regarding your Azure subscription.</span></span>

### <a name="create-an-app-service-web-app"></a><span data-ttu-id="74665-243">Criar um aplicativo Web do Serviço de Aplicativo</span><span class="sxs-lookup"><span data-stu-id="74665-243">Create an App Service web app</span></span>
1. <span data-ttu-id="74665-244">Da linha de comando, mude os diretórios para o diretório **tasklist** .</span><span class="sxs-lookup"><span data-stu-id="74665-244">From the command-line, change directories to the **tasklist** directory.</span></span>
2. <span data-ttu-id="74665-245">Use o comando a seguir para criar um novo aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="74665-245">Use the following command to create a new web app.</span></span>
   
        azure site create --git
   
    <span data-ttu-id="74665-246">Será solicitada a informação do nome e do local do aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="74665-246">You will be prompted for the web app name and location.</span></span> <span data-ttu-id="74665-247">Forneça um nome exclusivo e selecione a mesma localização geográfica da sua conta de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="74665-247">Provide a unique name and select the same geographical location as your Azure Storage account.</span></span>
   
    <span data-ttu-id="74665-248">O parâmetro `--git` cria um repositório Git no Azure para esse aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="74665-248">The `--git` parameter creates a Git repository on Azure for this web app.</span></span> <span data-ttu-id="74665-249">Também inicializa um repositório Git no diretório atual (caso não exista) e adiciona um [Git remoto] chamado 'azure', que é usado para publicar o aplicativo no Azure.</span><span class="sxs-lookup"><span data-stu-id="74665-249">It also initializes a Git repository in the current directory if none exists, and adds a [Git remote] named 'azure', which is used to publish the application to Azure.</span></span> <span data-ttu-id="74665-250">Por fim, será criado um arquivo **web.config** , que contém as configurações usadas pelo Azure para hospedar aplicativos de nó.</span><span class="sxs-lookup"><span data-stu-id="74665-250">Finally, it creates a **web.config** file, which contains settings used by Azure to host node applications.</span></span> <span data-ttu-id="74665-251">Se você omitir o parâmetro `--git` mas se o diretório tiver um repositório Git, o comando ainda criará o 'azure' remoto.</span><span class="sxs-lookup"><span data-stu-id="74665-251">If you omit the `--git` parameter but the directory contains a Git repository, the command will still create the 'azure' remote.</span></span>
   
    <span data-ttu-id="74665-252">Quando este comando for concluído, você verá uma saída semelhante à seguinte.</span><span class="sxs-lookup"><span data-stu-id="74665-252">Once this command has completed, you will see output similar to the following.</span></span> <span data-ttu-id="74665-253">Observe que a linha que começa com **Site criado em** contém a URL do aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="74665-253">Note that the line beginning with **Website created at** contains the URL for the web app.</span></span>
   
        info:   Executing command site create
        help:   Need a site name
        Name: TableTasklist
        info:   Using location southcentraluswebspace
        info:   Executing `git init`
        info:   Creating default .gitignore file
        info:   Creating a new web site
        info:   Created web site at  tabletasklist.azurewebsites.net
        info:   Initializing repository
        info:   Repository initialized
        info:   Executing `git remote add azure https://username@tabletasklist.azurewebsites.net/TableTasklist.git`
        info:   site create command OK
   
   > [!NOTE]
   > <span data-ttu-id="74665-254">Se esse for o primeiro aplicativo Web do Serviço de Aplicativo da sua assinatura, você será instruído a usar o Portal do Azure para criar o aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="74665-254">If this is the first App Service web app for your subscription, you will be instructed to use the Azure Portal to create the web app.</span></span> <span data-ttu-id="74665-255">Para obter mais informações, consulte [Criar e implantar um aplicativo Web do Node.js no Serviço de Aplicativo do Azure].</span><span class="sxs-lookup"><span data-stu-id="74665-255">For more information, see [Build and deploy a Node.js web app in Azure App Service].</span></span>
   > 
   > 

### <a name="set-environment-variables"></a><span data-ttu-id="74665-256">Configurar variáveis de ambiente</span><span class="sxs-lookup"><span data-stu-id="74665-256">Set environment variables</span></span>
<span data-ttu-id="74665-257">Nesta etapa, você irá adicionar variáveis de ambiente à configuração do aplicativo Web no Azure.</span><span class="sxs-lookup"><span data-stu-id="74665-257">In this step, you will add environment variables to your web app configuration on Azure.</span></span>
<span data-ttu-id="74665-258">Na linha de comando, insira o seguinte:</span><span class="sxs-lookup"><span data-stu-id="74665-258">From the command line, enter the following:</span></span>

    azure site appsetting add
        STORAGE_NAME=<storage account name>;STORAGE_KEY=<storage access key>;PARTITION_KEY=mytasks;TABLE_NAME=tasks


<span data-ttu-id="74665-259">Substitua **<storage account name>** pelo nome da conta de armazenamento criada anteriormente e substitua **<storage access key>** pela chave de acesso primário da sua conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="74665-259">Replace **<storage account name>** with the name of the storage account you created earlier, and replace **<storage access key>** with the primary access key for your storage account.</span></span> <span data-ttu-id="74665-260">(Use os mesmos valores do arquivo config.json que você criou anteriormente.)</span><span class="sxs-lookup"><span data-stu-id="74665-260">(Use the same values as the config.json file that you created earlier.)</span></span>

<span data-ttu-id="74665-261">Como alternativa, você pode definir as variáveis de ambiente no [Portal do Azure](https://portal.azure.com/):</span><span class="sxs-lookup"><span data-stu-id="74665-261">Alternatively, you can set environment variables in the [Azure Portal](https://portal.azure.com/):</span></span>

1. <span data-ttu-id="74665-262">Abra a folha do aplicativo Web clicando em **Procurar** > **Aplicativos Web** > nome do aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="74665-262">Open the web app's blade by clicking **Browse** > **Web Apps** > your web app name.</span></span>
2. <span data-ttu-id="74665-263">Na folha do seu aplicativo Web, clique em **Todas as configurações** > **Configurações do Aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="74665-263">In your web app's blade, click **All Settings** > **Application Settings**.</span></span>
   
     <!-- ![Top Menu](./media/storage-nodejs-use-table-storage-web-site/PollsCommonWebSiteTopMenu.png) -->
3. <span data-ttu-id="74665-264">Role para baixo até a seção de **Configurações do aplicativo** seção e adicione os pares chave/valor.</span><span class="sxs-lookup"><span data-stu-id="74665-264">Scroll down to the **App settings** section and add the key/value pairs.</span></span>
   
     ![Configurações do aplicativo](./media/storage-nodejs-use-table-storage-web-site/storage-tasks-appsettings.png)
4. <span data-ttu-id="74665-266">Clique em **SALVAR**.</span><span class="sxs-lookup"><span data-stu-id="74665-266">Click **SAVE**.</span></span>

### <a name="publish-the-application"></a><span data-ttu-id="74665-267">Publicar o aplicativo</span><span class="sxs-lookup"><span data-stu-id="74665-267">Publish the application</span></span>
<span data-ttu-id="74665-268">Para publicar o aplicativo, confirme os arquivos de código no Git e envie por push ao azure/mestre.</span><span class="sxs-lookup"><span data-stu-id="74665-268">To publish the app, commit the code files to Git and then push to azure/master.</span></span>

1. <span data-ttu-id="74665-269">Configure suas credenciais de implantação.</span><span class="sxs-lookup"><span data-stu-id="74665-269">Set your deployment credentials.</span></span>
   
        azure site deployment user set <name> <password>
2. <span data-ttu-id="74665-270">Adicione e confirme os arquivos do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="74665-270">Add and commit your application files.</span></span>
   
        git add .
        git commit -m "adding files"
3. <span data-ttu-id="74665-271">Envie a confirmação para o aplicativo Web do Serviço de Aplicativo:</span><span class="sxs-lookup"><span data-stu-id="74665-271">Push the commit to the App Service web app:</span></span>
   
        git push azure master
   
    <span data-ttu-id="74665-272">Use **mestre** como a ramificação de destino.</span><span class="sxs-lookup"><span data-stu-id="74665-272">Use **master** as the target branch.</span></span> <span data-ttu-id="74665-273">No final da implantação, você verá uma instrução semelhante a este exemplo:</span><span class="sxs-lookup"><span data-stu-id="74665-273">At the end of the deployment, you see a statement similar to the following example:</span></span>
   
        To https://username@tabletasklist.azurewebsites.net/TableTasklist.git
          * [new branch]      master -> master
4. <span data-ttu-id="74665-274">Quando a operação de envio for concluída, vá até a URL do aplicativo Web retornada anteriormente pelo comando `azure create site` para exibir o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="74665-274">Once the push operation has completed, browse to the web app URL returned previously by the `azure create site` command to view your application.</span></span>

## <a name="next-steps"></a><span data-ttu-id="74665-275">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="74665-275">Next steps</span></span>
<span data-ttu-id="74665-276">Embora as etapas neste artigo descrevam como usar o Serviço Tabela para armazenar informações, você também pode usar o [MongoDB](https://mlab.com/azure/).</span><span class="sxs-lookup"><span data-stu-id="74665-276">While the steps in this article describe using the Table Service to store information, you can also use [MongoDB](https://mlab.com/azure/).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="74665-277">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="74665-277">Additional resources</span></span>
<span data-ttu-id="74665-278">[CLI do Azure]</span><span class="sxs-lookup"><span data-stu-id="74665-278">[Azure CLI]</span></span>

## <a name="whats-changed"></a><span data-ttu-id="74665-279">O que mudou</span><span class="sxs-lookup"><span data-stu-id="74665-279">What's changed</span></span>
* <span data-ttu-id="74665-280">Para obter um guia sobre a alteração de Sites para o Serviço de Aplicativo, consulte: [Serviço de Aplicativo do Azure e seu impacto sobre os serviços do Azure existentes](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="74665-280">For a guide to the change from Websites to App Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

<!-- URLs -->

<span data-ttu-id="74665-281">[Criar e implantar um aplicativo Web do Node.js no Serviço de Aplicativo do Azure]: app-service-web-get-started-nodejs.md</span><span class="sxs-lookup"><span data-stu-id="74665-281">[Build and deploy a Node.js web app in Azure App Service]: app-service-web-get-started-nodejs.md</span></span>
[Azure Developer Center]: /develop/nodejs/

<span data-ttu-id="74665-282">[node]: http://nodejs.org</span><span class="sxs-lookup"><span data-stu-id="74665-282">[node]: http://nodejs.org</span></span>
<span data-ttu-id="74665-283">[Git]: http://git-scm.com</span><span class="sxs-lookup"><span data-stu-id="74665-283">[Git]: http://git-scm.com</span></span>
<span data-ttu-id="74665-284">[Express]: http://expressjs.com</span><span class="sxs-lookup"><span data-stu-id="74665-284">[Express]: http://expressjs.com</span></span>
[for free]: http://windowsazure.com
<span data-ttu-id="74665-285">[Git remoto]: http://git-scm.com/docs/git-remote</span><span class="sxs-lookup"><span data-stu-id="74665-285">[Git remote]: http://git-scm.com/docs/git-remote</span></span>

<span data-ttu-id="74665-286">[CLI do Azure]:../cli-install-nodejs.md</span><span class="sxs-lookup"><span data-stu-id="74665-286">[Azure CLI]:../cli-install-nodejs.md</span></span>

<span data-ttu-id="74665-287">[azure]: https://github.com/Azure/azure-sdk-for-node</span><span class="sxs-lookup"><span data-stu-id="74665-287">[azure]: https://github.com/Azure/azure-sdk-for-node</span></span>
<span data-ttu-id="74665-288">[node-uuid]: https://www.npmjs.com/package/node-uuid</span><span class="sxs-lookup"><span data-stu-id="74665-288">[node-uuid]: https://www.npmjs.com/package/node-uuid</span></span>
<span data-ttu-id="74665-289">[nconf]: https://www.npmjs.com/package/nconf</span><span class="sxs-lookup"><span data-stu-id="74665-289">[nconf]: https://www.npmjs.com/package/nconf</span></span>
<span data-ttu-id="74665-290">[async]: https://www.npmjs.com/package/async</span><span class="sxs-lookup"><span data-stu-id="74665-290">[async]: https://www.npmjs.com/package/async</span></span>

[Azure Portal]: https://portal.azure.com

[Create and deploy a Node.js application to an Azure Web Site]: app-service-web-get-started-nodejs.md

<!-- Image References -->

[node-table-finished]: ./media/storage-nodejs-use-table-storage-web-site/table_todo_empty.png
[node-table-list-items]: ./media/storage-nodejs-use-table-storage-web-site/table_todo_list.png
[download-publishing-settings]: ./media/storage-nodejs-use-table-storage-web-site/azure-account-download-cli.png
[portal-storage-access-keys]: ./media/storage-nodejs-use-table-storage-web-site/manage-access-keys.png
[app-settings]: ./media/storage-nodejs-use-table-storage-web-site/storage-tasks-appsettings.png
