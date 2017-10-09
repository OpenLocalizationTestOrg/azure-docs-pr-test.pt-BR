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
# <a name="nodejs-web-application-using-storage"></a>Aplicativo Web do Node.js usando Armazenamento
## <a name="overview"></a>Visão geral
Neste tutorial, Olá aplicativo criado no [aplicativo de Web Node.js usando Express] tutorial é estendido usando Olá bibliotecas de cliente do Microsoft Azure para Node.js toowork com serviços de gerenciamento de dados. Você pode estender o aplicativo, criando um aplicativo baseado na web-lista de tarefas que você pode implantar tooAzure. lista de tarefas Olá permite que um usuário recuperar tarefas, adicionar novas tarefas e marcar tarefas como concluídas.

itens de tarefa Olá são armazenados no armazenamento do Azure. O Armazenamento do Azure fornece um armazenamento de dados não estruturado altamente disponível e tolerante a falhas. O Armazenamento do Azure inclui várias estruturas de dados nas quais você pode armazenar e acessar dados. Você pode usar os serviços de armazenamento de saudação do hello APIs incluídas hello Azure SDK para Node.js ou por meio de APIs REST. Para saber mais, veja [Armazenando e acessando dados no Azure].

Este tutorial presume que você tenha concluído Olá [aplicativo Web Node.js] e [Node. js Express][aplicativo de Web Node.js usando Express] tutoriais.

Ele contém Olá informações a seguir:

* Como toowork com hello mecanismo de modelo Jade
* Como toowork com serviços de gerenciamento de dados do Azure

Olá captura de tela a seguir mostra um aplicativo hello concluída:

![Olá concluída a página da web no internet explorer](./media/table-storage-cloud-service-nodejs/getting-started-1.png)

## <a name="setting-storage-credentials-in-webconfig"></a>Definindo credenciais de armazenamento em Web.Config
Você deve passar credenciais de armazenamento tooaccess armazenamento do Azure. Isso é feito com o uso de configurações do aplicativo Web. config Olá.
configurações de Web. config Olá são passadas como tooNode de variáveis de ambiente, que são então lidos pelo Olá SDK do Azure.

> [!NOTE]
> As credenciais de armazenamento são usadas somente quando o aplicativo hello é tooAzure implantado. Quando em execução no emulador hello, aplicativo hello usa o emulador de armazenamento hello.
>
>

Executar Olá seguintes credenciais de conta de armazenamento etapas tooretrieve hello e adicioná-los toohello configurações de Web. config:

1. Se ainda não estiver aberto, inicie hello Azure PowerShell de saudação **iniciar** menu expandindo **todos os programas, o Azure**, clique com botão direito **Azure PowerShell**e, em seguida, selecione  **Executar como administrador**.
2. Alterar diretórios toohello pasta que contém seu aplicativo. Por exemplo, C:\\node\\tasklist\\WebRole1.
3. Na janela do Powershell do Azure hello, digite Olá informações de conta de armazenamento do cmdlet tooretrieve Olá a seguir:

    ```powershell
    PS C:\node\tasklist\WebRole1> Get-AzureStorageAccounts
    ```

   Olá, cmdlet anterior recupera Olá lista de contas de armazenamento e chaves de conta associadas ao seu serviço hospedado.

   > [!NOTE]
   > Como Olá SDK do Azure cria uma conta de armazenamento ao implantar um serviço, uma conta de armazenamento já deve existir de implantar seu aplicativo em guias de saudação anterior.
   >
   >
4. Olá abrir **servicedefinition. Csdef** arquivo que contém configurações de ambiente de hello são usadas quando o aplicativo hello é tooAzure implantado:

    ```powershell
    PS C:\node\tasklist> notepad ServiceDefinition.csdef
    ```

5. Bloquear a seguir Olá INSERT em **ambiente** elemento, substituindo a {conta de armazenamento} e {chave de acesso de armazenamento} com o nome da conta de saudação e a chave primária Olá Olá conta de armazenamento você deseja toouse para implantação:

  <Variable name="AZURE_STORAGE_ACCOUNT" value="{STORAGE ACCOUNT}" />
  <Variable name="AZURE_STORAGE_ACCESS_KEY" value="{STORAGE ACCESS KEY}" />

   ![conteúdo do arquivo Hello web.cloud.config](./media/table-storage-cloud-service-nodejs/node37.png)

6. Salve o arquivo hello e feche o bloco de notas.

### <a name="install-additional-modules"></a>Instalar módulos adicionais
1. Saudação de uso após a saudação de tooinstall de comando [azure], [nó uuid], [nconf] e [assíncrono] módulos localmente, bem como toosave uma entrada para eles toohello **Package. JSON** arquivo:

  ```powershell
  PS C:\node\tasklist\WebRole1> npm install azure-storage node-uuid async nconf --save
  ```

  saída de Hello desse comando deve aparecer a seguir toohello semelhante:

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

## <a name="using-hello-table-service-in-a-node-application"></a>Usando o serviço de tabela de saudação em um aplicativo de nó
Nesta seção, Olá aplicativo básico criado pelo Olá **express** comando é estendido pela adição de um **task.js** arquivo que contém o modelo de saudação para suas tarefas. Modificar Olá existente **app.js** de arquivo e criar um novo **tasklist.js** arquivo que usa o modelo de saudação.

### <a name="create-hello-model"></a>Criar modelo Olá
1. Em Olá **WebRole1** diretório, crie um novo diretório chamado **modelos**.
2. Em Olá **modelos** diretório, crie um novo arquivo chamado **task.js**. Este arquivo contém o modelo Olá Olá tarefas criados pelo seu aplicativo.
3. Início de saudação do hello **task.js** de arquivo, adicione Olá bibliotecas tooreference necessárias de código a seguir:

    ```nodejs
    var azure = require('azure-storage');
    var uuid = require('node-uuid');
    var entityGen = azure.TableUtilities.entityGenerator;
    ```

4. Em seguida, adicione código toodefine e exportar o objeto de tarefa hello. objeto de tarefa Olá é responsável por conectar-se a tabela de toohello.

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

5. Em seguida, adicione Olá métodos adicionais de toodefine de código a seguir em objeto de tarefa hello, que permitem que as interações com os dados armazenados na tabela de saudação:

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

6. Salve e feche o hello **task.js** arquivo.

### <a name="create-hello-controller"></a>Criar hello controlador
1. Em Olá **WebRole1/rotas** diretório, crie um novo arquivo chamado **tasklist.js** e abri-lo em um editor de texto.
2. Adicionar Olá código a seguir muito**tasklist.js**. Esse código carrega hello azure e módulos assíncrono, que são usados pelo **tasklist.js** e define Olá **TaskList** função, que é passada a uma instância de saudação **tarefa** nós de objeto definido anteriormente:

    ```nodejs
    var azure = require('azure-storage');
    var async = require('async');

    module.exports = TaskList;

    function TaskList(task) {
      this.task = task;
    }
    ```

3. Continue adicionando toohello **tasklist.js** arquivo adicionando métodos de saudação usados muito**showTasks**, **addTask**, e **completeTasks**:

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

4. Salvar Olá **tasklist.js** arquivo.

### <a name="modify-appjs"></a>Modificar app.js
1. Em Olá **WebRole1** Olá diretório, abra **app.js** em um editor de texto.
2. No início de saudação do arquivo hello, adicione Olá módulo de saudação do azure tooload a seguir e defina a chave de nome e a partição da tabela de saudação:

    ```nodejs
    var azure = require('azure-storage');
    var tableName = 'tasks';
    var partitionKey = 'hometasks';
    ```

3. No arquivo de app.js hello, role para baixo toowhere você ver Olá linha a seguir:

    ```nodejs
    app.use('/', routes);
    app.use('/users', users);
    ```

    Substitua saudação precedendo linhas com hello código a seguir. Esse código inicializa uma instância de <strong>tarefa</strong> com uma conta de armazenamento de tooyour de conexão. Olá <strong>tarefa</strong> é passado toohello <strong>TaskList</strong>, que usa toocommunicate com o serviço de tabela hello:

    ```nodejs
    var TaskList = require('./routes/tasklist');
    var Task = require('./models/task');
    var task = new Task(azure.createTableService(), tableName, partitionKey);
    var taskList = new TaskList(task);

    app.get('/', taskList.showTasks.bind(taskList));
    app.post('/addtask', taskList.addTask.bind(taskList));
    app.post('/completetask', taskList.completeTask.bind(taskList));
    ```

4. Salvar Olá **app.js** arquivo.

### <a name="modify-hello-index-view"></a>Modificar a exibição do índice Olá
1. Altere os diretórios toohello **exibições** Olá diretório e abra **Jade** em um editor de texto.
2. Substitua o conteúdo de saudação do hello **Jade** arquivo com hello código a seguir. Esse código define a exibição Olá para exibir tarefas existentes e define um formulário para adicionar novas tarefas e marcar os existentes, como concluída.

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

3. Salve e feche o arquivo **index.jade** .

### <a name="modify-hello-global-layout"></a>Modificar o layout global Olá
Olá **layout.jade** arquivo hello **exibições** diretório é usado como um modelo global para outros **.jade** arquivos. Nesta etapa, modifique Olá **layout.jade** arquivo toouse [Twitter Bootstrap](https://github.com/twbs/bootstrap), que é um kit de ferramentas que torna mais fácil toodesign um site de aparência adequado.

1. Baixe e extraia os arquivos de saudação para [Twitter Bootstrap](http://getbootstrap.com/). Saudação de cópia **bootstrap.min.css** arquivo hello **bootstrap\\dist\\css** pasta toohello **pública\\folhas de estilo** diretório do seu aplicativo de lista de tarefas.
2. De saudação **exibições** pasta, abra Olá **layout.jade** do arquivo em seu editor de texto e substitua o conteúdo de saudação pelo seguinte hello:

    doctype html  html    head      title= title      link(rel='stylesheet', href='/stylesheets/bootstrap.min.css')      link(rel='stylesheet', href='/stylesheets/style.css')    body.app      nav.navbar.navbar-default        div.navbar-header          a.navbar-brand(href='/') My Tasks      block content

3. Salvar Olá **layout.jade** arquivo.

### <a name="running-hello-application-in-hello-emulator"></a>Aplicativo de saudação em execução no emulador de saudação
Use Olá aplicativo do comando toostart hello no emulador Olá a seguir.

```powershell
PS C:\node\tasklist\WebRole1> start-azureemulator -launch
```

navegador de saudação abre e exibe o saudação página a seguir:

![Uma web paginada intitulada minha lista de tarefas com uma tabela que contém tarefas e campos tooadd uma nova tarefa.](./media/table-storage-cloud-service-nodejs/node44.png)

Usar Olá formulário tooadd itens ou remover itens existentes marcando-as como concluída.

## <a name="publishing-hello-application-tooazure"></a>Publicação tooAzure de aplicativo hello
Na janela do Windows PowerShell hello, chame hello tooredeploy cmdlet a seguir tooAzure seu serviço hospedado.

```powershell
PS C:\node\tasklist\WebRole1> Publish-AzureServiceProject -name myuniquename -location datacentername -launch
```

Substitua **myuniquename** por um nome exclusivo para o aplicativo. Substituir **datacentername** com o nome de saudação de um data center do Azure, como **Oeste dos EUA**.

Após a conclusão da implantação hello, você deve ver uma resposta semelhante toohello a seguir:

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

Especificando Olá **-iniciar** opção no cmdlet anterior hello, navegador Olá abre e exibe seu aplicativo em execução no Azure, quando a publicação é concluída.

![Uma janela do navegador exibindo a página do hello minha lista de tarefas. URL de saudação indica a página Olá agora está sendo hospedada no Azure.](./media/table-storage-cloud-service-nodejs/getting-started-1.png)

## <a name="stopping-and-deleting-your-application"></a>Parando e excluindo o aplicativo
Depois de implantar seu aplicativo, talvez você queira toodisable para evitar custos ou criar e implantar outros aplicativos Olá gratuitamente período de avaliação.

O Azure cobra as instâncias de função web por hora de acordo com o tempo consumido do servidor.
Hora do servidor é consumida quando o aplicativo for implantado, mesmo se as instâncias não estão em execução e estão em estado de saudação interrompido.

Olá etapas a seguir mostram como toostop e excluir seu aplicativo.

1. Na janela do Windows PowerShell hello, interrompa a implantação do serviço Olá criada na seção anterior Olá com hello cmdlet a seguir:

    ```powershell
    PS C:\node\tasklist\WebRole1> Stop-AzureService
    ```

   Parar serviço Olá pode levar vários minutos. Quando a saudação serviço for interrompido, você recebe uma mensagem indicando que ele foi interrompido.

2. serviço de saudação toodelete, chamada hello cmdlet a seguir:

    ```powershell
    PS C:\node\tasklist\WebRole1> Remove-AzureService contosotasklist
    ```

   Quando solicitado, insira **Y** toodelete serviço de saudação.

   Excluindo serviço Olá pode levar vários minutos. Depois que serviço Olá for excluído, você receberá uma mensagem indicando que o serviço de saudação foi excluído.

[aplicativo de Web Node.js usando Express]: http://azure.microsoft.com/develop/nodejs/tutorials/web-app-with-express/
[Armazenando e acessando dados no Azure]: http://msdn.microsoft.com/library/azure/gg433040.aspx
[aplicativo Web Node.js]: http://azure.microsoft.com/develop/nodejs/tutorials/getting-started/


