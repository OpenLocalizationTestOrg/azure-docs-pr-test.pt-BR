---
title: "aplicativo de web aaaNode.js usando Olá serviço tabela do Azure"
description: "Este tutorial ensina como toouse hello Azure Table serviço toostore dados de um aplicativo Node. js que está hospedado em aplicativos de Web do serviço de aplicativo do Azure."
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
ms.openlocfilehash: f6e08335b4c7f62f7b3994287edd586860cb7135
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="nodejs-web-app-using-hello-azure-table-service"></a>Aplicativo de web Node. js usando Olá serviço tabela do Azure
## <a name="overview"></a>Visão geral
Este tutorial mostra como o serviço de tabela toouse fornecida pelo toostore e acessar dados de gerenciamento de dados do Azure uma [nó] aplicativo hospedado no [do serviço de aplicativo do Azure](http://go.microsoft.com/fwlink/?LinkId=529714) aplicativos Web. Este tutorial pressupõe que você tenha alguma experiência anterior usando nó e [Git].

Você aprenderá:

* Como toouse npm (Gerenciador de pacotes de nó) tooinstall Olá módulos de nó
* Como toowork com hello serviço tabela do Azure
* Como toouse Olá toocreate CLI do Azure com um aplicativo web.

Seguindo este tutorial, você criará um aplicativo simples de “lista de tarefas” baseado na web, que permite criar, recuperar e concluir tarefas. tarefas de saudação são armazenadas em Olá serviço tabela.

Aqui está o aplicativo hello concluída:

![Uma página da Web que exibe uma lista de tarefas vazia][node-table-finished]

> [!NOTE]
> Se você quiser tooget iniciado com o serviço de aplicativo do Azure antes de se inscrever para uma conta do Azure, vá muito[tente do serviço de aplicativo](https://azure.microsoft.com/try/app-service/), onde você pode criar imediatamente um aplicativo web de curta duração starter no serviço de aplicativo. Nenhum cartão de crédito é exigido, sem compromissos.
> 
> 

## <a name="prerequisites"></a>Pré-requisitos
Antes de seguir as instruções neste artigo hello, certifique-se de que você tenha a seguinte Olá instalado:

* [nó] versão 0.10.24 ou superior
* [Git]

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

## <a name="create-a-storage-account"></a>Criar uma conta de armazenamento
Crie uma conta de armazenamento do Azure. aplicativo Hello usará esse itens de tarefas pendentes conta toostore hello.

1. Faça logon no hello [Portal do Azure](https://portal.azure.com/).
2. Clique em Olá **novo** ícone na parte inferior de saudação à esquerda do portal hello, em seguida, clique em **dados + armazenamento** > **armazenamento**. Dê um nome exclusivo de conta de armazenamento hello e criar um novo [grupo de recursos](../azure-resource-manager/resource-group-overview.md) para ele.
   
      ![Botão Novo](./media/storage-nodejs-use-table-storage-web-site/configure-storage.png)
   
    Quando tiver sido criada a conta de armazenamento hello, Olá **notificações** botão pisca uma verde **êxito** e folha da conta de armazenamento hello está aberta tooshow que ele pertence toohello novo recurso de grupo criado.
3. Na folha da conta de armazenamento hello, clique em **configurações** > **chaves**. Copie a área de transferência de toohello chave de acesso primária hello.
   
    ![Chave de acesso][portal-storage-access-keys]

## <a name="install-modules-and-generate-scaffolding"></a>Instalar módulos e gerar scaffolding
Nesta seção, você cria um novo aplicativo de nó e usar pacotes de módulo tooadd npm. Para este aplicativo, você usará Olá [Express] e [Azure] módulos. módulo do Hello Express fornece uma estrutura de Model View Controller para o nó, durante a saudação módulos do Azure fornece o serviço de tabela de toohello de conectividade.

### <a name="install-express-and-generate-scaffolding"></a>Instalar o express e gerar scaffolding
1. Na linha de comando hello, criar um novo diretório chamado **tasklist** e comutador toothat directory.  
2. Digite hello seguindo o módulo do comando tooinstall Olá Express.
   
        npm install express-generator@4.2.0 -g
   
    Dependendo do sistema operacional de saudação, talvez seja necessário tooput 'sudo' antes do comando hello:
   
        sudo npm install express-generator@4.2.0 -g
   
    saída de Hello aparece semelhante toohello exemplo a seguir:
   
        express-generator@4.2.0 /usr/local/lib/node_modules/express-generator
        ├── mkdirp@0.3.5
        └── commander@1.3.2 (keypress@0.1.0)
   
   > [!NOTE]
   > Olá '-g' parâmetro instala o módulo de saudação globalmente. Dessa forma, podemos usar **express** toogenerate scaffolding de aplicativo da web sem ter que tootype nas informações de caminho adicionais.
   > 
   > 
3. scaffolding de saudação do toocreate para o aplicativo hello, digite Olá **express** comando:
   
        express
   
    saída de Hello deste comando será semelhante toohello exemplo a seguir:
   
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
   
           run hello app:
             $ DEBUG=my-application ./bin/www
   
    Agora você tem vários novos diretórios e arquivos no hello **tasklist** directory.

### <a name="install-additional-modules"></a>Instalar módulos adicionais
Uma saudação arquivos **express** cria é **Package. JSON**. Esse arquivo contém uma lista das dependências do módulo. Posteriormente, quando você implanta Olá aplicativo tooApp aplicativos Web do serviço, esse arquivo determina quais módulos toobe instalado no Azure.

Em Olá de linha de comando, digite Olá seguintes módulos de saudação do comando tooinstall descritos em hello **Package. JSON** arquivo. Talvez seja necessário toouse 'sudo'.

    npm install

saída de Hello deste comando será semelhante toohello exemplo a seguir:

    debug@0.7.4 node_modules\debug

    cookie-parser@1.0.1 node_modules\cookie-parser
    ├── cookie-signature@1.0.3
    └── cookie@0.1.0

    [...]


Em seguida, digite Olá Olá de tooinstall de comando a seguir [azure], [uuid nó], [nconf] e [async] módulos:

    npm install azure-storage node-uuid async nconf --save

Olá **– salvar** sinalizador adiciona entradas para esses módulos toohello **Package. JSON** arquivo.

saída de Hello deste comando será semelhante toohello exemplo a seguir:

    async@0.9.0 node_modules\async

    node-uuid@1.4.1 node_modules\node-uuid

    nconf@0.6.9 node_modules\nconf
    ├── ini@1.2.1
    ├── async@0.2.9
    └── optimist@0.6.0 (wordwrap@0.0.2, minimist@0.0.10)

    [...]


## <a name="create-hello-application"></a>Criar um aplicativo hello
Agora, estamos aplicativo hello de toobuild pronto.

### <a name="create-a-model"></a>Criar um modelo
Um *modelo* é um objeto que representa dados de saudação em seu aplicativo. Para o aplicativo hello, modelo somente Olá é um objeto de tarefa que representa um item na lista de tarefas pendentes de saudação. Tarefas terá Olá campos a seguir:

* PartitionKey
* RowKey
* nome (cadeia de caracteres)
* categoria (cadeia de caracteres)
* concluído (booleano)

**PartitionKey** e **RowKey** são usados por Olá serviço tabela como chaves de tabela. Para obter mais informações, consulte [modelo de dados de serviço tabela Noções básicas sobre Olá](https://msdn.microsoft.com/library/azure/dd179338.aspx).

1. Em Olá **tasklist** diretório, crie um novo diretório chamado **modelos**.
2. Em Olá **modelos** diretório, crie um novo arquivo chamado **task.js**. Esse arquivo irá conter modelo Olá Olá tarefas criados pelo seu aplicativo.
3. Início de saudação do hello **task.js** de arquivo, adicione Olá bibliotecas tooreference necessárias de código a seguir:
   
        var azure = require('azure-storage');
          var uuid = require('node-uuid');
        var entityGen = azure.TableUtilities.entityGenerator;
4. Adicione seguinte Olá código toodefine e exportar o objeto de tarefa hello. Esse objeto é responsável por conectar-se a tabela de toohello.
   
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
5. Adicione Olá métodos adicionais de toodefine de código a seguir em objeto de tarefa hello, que permitem que as interações com os dados armazenados na tabela de saudação:
   
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
6. Salve e feche o hello **task.js** arquivo.

### <a name="create-a-controller"></a>Criar um controlador
Um *controlador* lida com solicitações HTTP e processa a resposta Olá HTML.

1. Em Olá **tasklist/rotas** diretório, crie um novo arquivo chamado **tasklist.js** e abri-lo em um editor de texto.
2. Adicionar Olá código a seguir muito**tasklist.js**. Isso carrega hello azure e async módulos, que são usados por **tasklist.js**. Isso também define Olá **TaskList** função, que é passada a uma instância do hello **tarefa** objeto definimos anteriormente:
   
        var azure = require('azure-storage');
        var async = require('async');
   
        module.exports = TaskList;
3. Defina um objeto **TaskList** .
   
        function TaskList(task) {
          this.task = task;
        }
4. Adicionar Olá métodos a seguir muito**TaskList**:
   
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

### <a name="modify-appjs"></a>Modificar app.js
1. De saudação **tasklist** Olá diretório, abra **app.js** arquivo. Este arquivo foi criado anteriormente executando Olá **express** comando.
2. Início de saudação do arquivo hello, adicione Olá tooload hello azure módulo, nome de tabela do conjunto hello, chave de partição e conjunto de credenciais de armazenamento de saudação usadas por este exemplo a seguir:
   
        var azure = require('azure-storage');
        var nconf = require('nconf');
        nconf.env()
             .file({ file: 'config.json', search: true });
        var tableName = nconf.get("TABLE_NAME");
        var partitionKey = nconf.get("PARTITION_KEY");
        var accountName = nconf.get("STORAGE_NAME");
        var accountKey = nconf.get("STORAGE_KEY");
   
   > [!NOTE]
   > nconf carregará os valores de configuração de saudação de variáveis de ambiente ou hello **config. JSON** arquivo, que vamos criar mais tarde.
   > 
   > 
3. No arquivo de app.js hello, role para baixo toowhere você ver Olá linha a seguir:
   
        app.use('/', routes);
        app.use('/users', users);
   
    Substitua Olá acima linhas com o código de saudação mostrado abaixo. Inicializar uma instância de <strong>tarefa</strong> com uma conta de armazenamento de tooyour de conexão. Isso é passado toohello <strong>TaskList</strong>, que irá usá-la toocommunicate com hello serviço tabela:
   
        var TaskList = require('./routes/tasklist');
        var Task = require('./models/task');
        var task = new Task(azure.createTableService(accountName, accountKey), tableName, partitionKey);
        var taskList = new TaskList(task);
   
        app.get('/', taskList.showTasks.bind(taskList));
        app.post('/addtask', taskList.addTask.bind(taskList));
        app.post('/completetask', taskList.completeTask.bind(taskList));
4. Salvar Olá **app.js** arquivo.

### <a name="modify-hello-index-view"></a>Modificar a exibição do índice Olá
1. Olá abrir **tasklist/views/index.jade** em um editor de texto.
2. Substitua todo o conteúdo do arquivo de Olá Olá Olá código a seguir. Isso define o modo de exibição das tarefas existentes, bem como um formulário para adicionar novas tarefas e marcar as tarefas existentes como concluídas.
   
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
3. Salve e feche o arquivo **index.jade** .

### <a name="modify-hello-global-layout"></a>Modificar o layout global Olá
Olá **layout.jade** arquivo hello **exibições** diretório é um modelo global para outros **.jade** arquivos. Nesta etapa você modificá-la toouse [Twitter Bootstrap](https://github.com/twbs/bootstrap), que é um kit de ferramentas que torna mais fácil toodesign um aplicativo de web buscam adequado.

Baixe e extraia os arquivos de saudação para [Twitter Bootstrap](http://getbootstrap.com/). Saudação de cópia **bootstrap.min.css** arquivo hello Bootstrap **css** pasta em Olá **público/folhas de estilo** diretório de seu aplicativo.

De saudação **exibições** pastas **layout.jade** e substitua todo o conteúdo Olá seguinte hello:

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

### <a name="create-a-config-file"></a>Criar um arquivo de configuração
toorun aplicativo hello localmente, colocaremos credenciais de armazenamento do Azure em um arquivo de configuração. Crie um arquivo chamado **config. JSON* * com hello JSON a seguir:

    {
        "STORAGE_NAME": "<storage account name>",
        "STORAGE_KEY": "<storage access key>",
        "PARTITION_KEY": "mytasks",
        "TABLE_NAME": "tasks"
    }

Substituir **nome da conta de armazenamento** com nome de saudação do armazenamento Olá conta criada anteriormente e substitua **chave de acesso de armazenamento** com a chave de acesso primária Olá para sua conta de armazenamento. Por exemplo:

    {
        "STORAGE_NAME": "nodejsappstorage",
        "STORAGE_KEY": "KG0oDd..."
        "PARTITION_KEY": "mytasks",
        "TABLE_NAME": "tasks"
    }

Salve esse arquivo *um nível de diretório superior* que Olá **tasklist** diretório, como este:

    parent/
      |-- config.json
      |-- tasklist/

razão de saudação para fazer isso é tooavoid Verificando arquivo de configuração de saudação no controle de origem, onde ele pode se tornar público. Quando for implantada Olá aplicativo tooAzure, usaremos as variáveis de ambiente em vez de um arquivo de configuração.

## <a name="run-hello-application-locally"></a>Executar o aplicativo hello localmente
aplicativo de hello tootest em seu computador local, execute Olá etapas a seguir:

1. Saudação de linha de comando, alterar diretórios toohello **tasklist** directory.
2. Use Olá toolaunch Olá aplicativo de comandos do local a seguir:
   
        npm start
3. Abra um navegador da web e navegue toohttp://127.0.0.1:3000.
   
    Um toohello semelhante de página da web exemplo a seguir é exibida.
   
    ![Uma página da Web que exibe uma lista de tarefas vazia][node-table-finished]
4. toocreate um novo item de tarefas, insira um nome e uma categoria e clique em **Adicionar Item**. 
5. toomark uma tarefa como concluída, verifique **concluir** e clique em **tarefas de atualização**.
   
    ![Uma imagem de saudação novo item na lista de saudação de tarefas][node-table-list-items]

Mesmo que o aplicativo hello estiver sendo executado localmente, ele está armazenando dados de saudação em Olá serviço tabela do Azure.

## <a name="deploy-your-application-tooazure"></a>Implantar seu aplicativo tooAzure
Olá etapas nesta seção usam ferramentas de linha de comando do Azure de saudação toocreate um novo aplicativo web no serviço de aplicativo e, em seguida, usam o Git toodeploy seu aplicativo. tooperform essas etapas, você deve ter uma assinatura do Azure.

> [!NOTE]
> Essas etapas também podem ser executadas usando Olá [Portal do Azure](https://portal.azure.com/). Confira [Criar e implantar um aplicativo Web do Node.js no Serviço de Aplicativo do Azure].
> 
> Se esse for o aplicativo web primeiro Olá que você criou, você deve usar hello Azure Portal toodeploy este aplicativo.
> 
> 

tooget iniciado, instalar Olá [CLI do Azure] inserindo Olá comando a seguir na linha de comando hello:

    npm install azure-cli -g

### <a name="import-publishing-settings"></a>Importar configurações de publicação
Nesta etapa, você baixará um arquivo que contém informações sobre sua assinatura.

1. Digite hello comando a seguir:
   
        azure login
   
    Esse comando inicia um navegador e navega toohello página de download. Se solicitado, faça logon com conta Olá associada à sua assinatura do Azure.
   
    <!-- ![hello download page][download-publishing-settings] -->
   
    download do arquivo Hello começa automaticamente. Se não estiver, você pode clicar Olá link no início de Olá Olá toomanually download saudação do arquivo de página. Salve o caminho de arquivo de saudação de observação e de saudação.
2. Digite hello configurações do comando tooimport Olá a seguir:
   
        azure account import <path-to-file>
   
    Especifica nome de arquivo e caminho de Olá do Olá publicando o arquivo de configurações que você baixou na etapa anterior hello.
3. Depois que as configurações de saudação são importadas, excluir Olá publicar o arquivo de configurações. Ele não é mais necessário e contém informações confidenciais sobre sua assinatura do Azure.

### <a name="create-an-app-service-web-app"></a>Criar um aplicativo Web do Serviço de Aplicativo
1. Saudação de linha de comando, alterar diretórios toohello **tasklist** directory.
2. Use Olá comando toocreate um novo aplicativo web a seguir.
   
        azure site create --git
   
    Você será solicitado para o local e o nome do aplicativo web hello. Forneça um nome exclusivo e selecione Olá mesmo local geográfico da sua conta de armazenamento do Azure.
   
    Olá `--git` parâmetro cria um repositório Git no Azure para este aplicativo web. Inicializa um repositório Git no diretório atual Olá também se nenhum existir e adiciona um [Git remoto] denominado 'do azure', que é usado toopublish Olá aplicativo tooAzure. Por fim, ele cria um **Web. config** arquivo, que contém as configurações usadas por aplicativos de nó toohost do Azure. Se você omitir Olá `--git` parâmetro mas Olá diretório contém um repositório Git, comando Olá ainda criará remoto Olá 'do azure'.
   
    Quando esse comando for concluído, você verá a seguinte de toohello semelhante de saída. Observe que Olá linha a partir **site criado em** contém Olá URL do aplicativo web de saudação.
   
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
   > Se isso for Olá primeiro aplicativo do serviço de aplicativo web para sua assinatura, você será toouse instruções hello Azure Portal toocreate Olá web app. Para obter mais informações, consulte [Criar e implantar um aplicativo Web do Node.js no Serviço de Aplicativo do Azure].
   > 
   > 

### <a name="set-environment-variables"></a>Configurar variáveis de ambiente
Nesta etapa, você irá adicionar a configuração de aplicativo web do tooyour de variáveis de ambiente no Azure.
Na linha de comando hello, digite seguinte hello:

    azure site appsetting add
        STORAGE_NAME=<storage account name>;STORAGE_KEY=<storage access key>;PARTITION_KEY=mytasks;TABLE_NAME=tasks


Substituir  **<storage account name>**  com nome de saudação do armazenamento Olá conta criada anteriormente e substitua  **<storage access key>**  com a chave de acesso primária Olá para sua conta de armazenamento. (Use Olá mesmos valores como arquivo de config. JSON Olá que você criou anteriormente).

Como alternativa, você pode definir variáveis de ambiente no hello [Portal do Azure](https://portal.azure.com/):

1. Abra a folha de seu aplicativo da web hello clicando **procurar** > **aplicativos Web** > nome do aplicativo web.
2. Na folha do seu aplicativo Web, clique em **Todas as configurações** > **Configurações do Aplicativo**.
   
     <!-- ![Top Menu](./media/storage-nodejs-use-table-storage-web-site/PollsCommonWebSiteTopMenu.png) -->
3. Role para baixo toohello **configurações do aplicativo** seção e adicionar pares de chave/valor hello.
   
     ![Configurações do aplicativo](./media/storage-nodejs-use-table-storage-web-site/storage-tasks-appsettings.png)
4. Clique em **SALVAR**.

### <a name="publish-hello-application"></a>Publicar o aplicativo hello
toopublish Olá aplicativo, Olá tooGit de arquivos de código de confirmação e, em seguida, enviar por push tooazure/mestre.

1. Configure suas credenciais de implantação.
   
        azure site deployment user set <name> <password>
2. Adicione e confirme os arquivos do aplicativo.
   
        git add .
        git commit -m "adding files"
3. Enviar por push Olá confirmação toohello aplicativo do serviço de aplicativo web:
   
        git push azure master
   
    Use **mestre** como branch de destino hello. No final de saudação da implantação Olá, você verá um toohello semelhante instrução exemplo a seguir:
   
        toohttps://username@tabletasklist.azurewebsites.net/TableTasklist.git
          * [new branch]      master -> master
4. Após a conclusão da operação de envio hello, procurar toohello URL do aplicativo web retornado anteriormente pelo Olá `azure create site` comando tooview seu aplicativo.

## <a name="next-steps"></a>Próximas etapas
Olá etapas neste artigo descrevem usando informações de toostore Olá serviço tabela, você também pode usar [MongoDB](https://mlab.com/azure/). 

## <a name="additional-resources"></a>Recursos adicionais
[CLI do Azure]

## <a name="whats-changed"></a>O que mudou
* Para um guia toohello alteração de sites tooApp serviço consulte: [do serviço de aplicativo do Azure e seu impacto sobre os serviços do Azure existente](http://go.microsoft.com/fwlink/?LinkId=529714)

<!-- URLs -->

[Criar e implantar um aplicativo Web do Node.js no Serviço de Aplicativo do Azure]: app-service-web-get-started-nodejs.md
[Azure Developer Center]: /develop/nodejs/

[nó]: http://nodejs.org
[Git]: http://git-scm.com
[Express]: http://expressjs.com
[for free]: http://windowsazure.com
[Git remoto]: http://git-scm.com/docs/git-remote

[CLI do Azure]:../cli-install-nodejs.md

[azure]: https://github.com/Azure/azure-sdk-for-node
[uuid nó]: https://www.npmjs.com/package/node-uuid
[nconf]: https://www.npmjs.com/package/nconf
[async]: https://www.npmjs.com/package/async

[Azure Portal]: https://portal.azure.com

[Create and deploy a Node.js application tooan Azure Web Site]: app-service-web-get-started-nodejs.md

<!-- Image References -->

[node-table-finished]: ./media/storage-nodejs-use-table-storage-web-site/table_todo_empty.png
[node-table-list-items]: ./media/storage-nodejs-use-table-storage-web-site/table_todo_list.png
[download-publishing-settings]: ./media/storage-nodejs-use-table-storage-web-site/azure-account-download-cli.png
[portal-storage-access-keys]: ./media/storage-nodejs-use-table-storage-web-site/manage-access-keys.png
[app-settings]: ./media/storage-nodejs-use-table-storage-web-site/storage-tasks-appsettings.png
