---
title: aaaBuild um aplicativo da web Node. js para o banco de dados do Azure Cosmos | Microsoft Docs
description: Este tutorial Node. js explora como toouse banco de dados do Microsoft Azure Cosmos toostore e acessar dados de um aplicativo da web Express Node. js hospedado em sites do Azure.
keywords: Desenvolvimento de aplicativos, tutorial de banco de dados, aprender node.js, tutorial do node.js
services: cosmos-db
documentationcenter: nodejs
author: mimig1
manager: jhubbard
editor: cgronlun
ms.assetid: 9da9e63b-e76a-434e-96dd-195ce2699ef3
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 08/14/2017
ms.author: mimig
ms.openlocfilehash: 31194dccf37eef69d2219b0d8328a88d434f79b9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="_Toc395783175"></a>Compilar um aplicativo Web Node.js usando o Azure Cosmos DB
> [!div class="op_single_selector"]
> * [.NET](documentdb-dotnet-application.md)
> * [Node.js](documentdb-nodejs-application.md)
> * [Java](documentdb-java-application.md)
> * [Python](documentdb-python-application.md)
> 
> 

Este tutorial Node. js mostra como toouse o banco de dados do Azure Cosmos e hello toostore e acessar dados de um aplicativo Node. js Express API DocumentDB hospedados nos sites do Azure. Você cria um aplicativo simples de gerenciamento de tarefas baseado na Web, um aplicativo ToDo, que permite criar, recuperar e concluir tarefas. tarefas de saudação são armazenadas como documentos JSON no banco de dados do Azure Cosmos. Este tutorial orienta você durante a criação de saudação e implantação do aplicativo hello e explica o que está acontecendo em cada trecho de código.

![Captura de tela de saudação aplicativo minha lista de tarefas criada neste tutorial Node. js](./media/documentdb-nodejs-application/cosmos-db-node-js-mytodo.png)

Não ter tempo toocomplete Olá tutorial e deseja apenas solução completa de saudação tooget? Não é um problema, você pode obter a solução de exemplo completo de saudação do [GitHub][GitHub]. Apenas ler Olá [Leiame](https://github.com/Azure-Samples/documentdb-node-todo-app/blob/master/README.md) arquivo para obter instruções sobre como toorun Olá aplicativo.

## <a name="_Toc395783176"></a>Pré-requisitos
> [!TIP]
> Este tutorial do Node.js presume que você tenha alguma experiência anterior com o Node.js e sites do Azure.
> 
> 

Antes de seguir as instruções neste artigo hello, você deve garantir que você tenha a seguinte hello:

* Uma conta ativa do Azure. Se você não tiver uma conta, poderá criar uma conta de avaliação gratuita em apenas alguns minutos. Para obter detalhes, consulte [Avaliação gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/).

   OU

   Uma instalação local do hello [emulador de banco de dados do Azure Cosmos](local-emulator.md) (somente Windows).
* [Node.js][Node.js] versão v0.10.29 ou superior.
* [Gerador expresso](http://www.expressjs.com/starter/generator.html) (você pode instalá-lo por meio de `npm install express-generator -g`)
* [Git][Git].

## <a name="_Toc395637761"></a>Etapa 1: Criar uma conta de banco de dados do Azure Cosmos DB
Vamos começar criando uma conta do Azure Cosmos DB. Se você já tiver uma conta ou se você estiver usando hello Azure Cosmos DB emulador para este tutorial, você poderá ignorar muito[etapa 2: criar um novo aplicativo Node. js](#_Toc395783178).

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

[!INCLUDE [cosmos-db-keys](../../includes/cosmos-db-keys.md)]

## <a name="_Toc395783178"></a>Etapa 2: criar um novo aplicativo do Node.js
Agora vamos aprender toocreate um projeto de Hello World Node básico usando Olá [Express](http://expressjs.com/) framework.

1. Abra seu terminal favorito, como o prompt de comando do hello Node. js.
2. Navegue toohello diretório em que você gostaria que o novo aplicativo de saudação toostore.
3. Use Olá gerador express toogenerate um novo aplicativo chamado **todo**.
   
        express todo
4. Abra o novo diretório **tarefas** e instale as dependências.
   
        cd todo
        npm install
5. Execute seu novo aplicativo.
   
        npm start
6. Você pode exibir o novo aplicativo navegando seu navegador muito[http://localhost:3000](http://localhost:3000).
   
    ![Saiba Node. js - captura de tela da saudação aplicativo Hello World em uma janela do navegador](./media/documentdb-nodejs-application/cosmos-db-node-js-express.png)

    Em seguida, toostop Olá aplicativo, pressione CTRL + C na janela do terminal hello e, em seguida, clique em **y** tooterminate trabalho de lote de saudação.

## <a name="_Toc395783179"></a>Etapa 3: Instalar módulos adicionais
Olá **Package. JSON** arquivo é um dos arquivos de saudação criados na raiz de saudação do projeto de saudação. Esse arquivo contém uma lista dos módulos adicionais que são necessários para seu aplicativo do Node.js. Posteriormente, quando você implanta esse tooAzure aplicativo sites, esse arquivo é usado toodetermine quais toobe da necessidade de módulos instalados no Azure toosupport seu aplicativo. Ainda precisamos tooinstall dois pacotes de mais para este tutorial.

1. Em Olá terminal, instale Olá **async** módulo por meio do npm.
   
        npm install async --save
2. Instalar Olá **documentdb** módulo por meio do npm. Este é o módulo de saudação onde acontece toda mágica do Azure Cosmos DB hello.
   
        npm install documentdb --save
3. Uma verificação rápida da saudação **Package. JSON** arquivo de aplicativo hello deve mostrar Olá módulos adicionais. Esse arquivo será informar o Azure toodownload quais pacotes e instalar quando executar o aplicativo. Ele deve se parecer com o exemplo hello abaixo.
   
        {
          "name": "todo",
          "version": "0.0.0",
          "private": true,
          "scripts": {
            "start": "node ./bin/www"
          },
          "dependencies": {
            "async": "^2.1.4",
            "body-parser": "~1.15.2",
            "cookie-parser": "~1.4.3",
            "debug": "~2.2.0",
            "documentdb": "^1.10.0",
            "express": "~4.14.0",
            "jade": "~1.11.0",
            "morgan": "~1.7.0",
            "serve-favicon": "~2.3.0"
          }
        }
   
    Isso informa ao Nó (e ao Azure mais tarde) que seu aplicativo depende desses módulos adicionais.

## <a name="_Toc395783180"></a>Etapa 4: Usando o serviço de banco de dados do Azure Cosmos Olá em um aplicativo de nó
Que cuida de todos os a configuração inicial hello e configuração, agora vamos get para baixo toowhy estamos aqui e que é parte de código usando o banco de dados do Azure Cosmos de toowrite.

### <a name="create-hello-model"></a>Criar modelo Olá
1. No diretório do projeto hello, criar um novo diretório chamado **modelos** em Olá mesmo diretório que o arquivo Package. JSON de saudação.
2. Em Olá **modelos** diretório, crie um novo arquivo chamado **taskDao.js**. Esse arquivo irá conter modelo Olá Olá tarefas criados pelo nosso aplicativo.
3. Em Olá mesmo **modelos** diretório, crie um novo arquivo denominado **docdbUtils.js**. Esse arquivo conterá algum código útil e reutilizável, que será usado em todo o nosso aplicativo. 
4. Código a seguir de saudação de cópia em muito**docdbUtils.js**
   
        var DocumentDBClient = require('documentdb').DocumentClient;
   
        var DocDBUtils = {
            getOrCreateDatabase: function (client, databaseId, callback) {
                var querySpec = {
                    query: 'SELECT * FROM root r WHERE r.id= @id',
                    parameters: [{
                        name: '@id',
                        value: databaseId
                    }]
                };
   
                client.queryDatabases(querySpec).toArray(function (err, results) {
                    if (err) {
                        callback(err);
   
                    } else {
                        if (results.length === 0) {
                            var databaseSpec = {
                                id: databaseId
                            };
   
                            client.createDatabase(databaseSpec, function (err, created) {
                                callback(null, created);
                            });
   
                        } else {
                            callback(null, results[0]);
                        }
                    }
                });
            },
   
            getOrCreateCollection: function (client, databaseLink, collectionId, callback) {
                var querySpec = {
                    query: 'SELECT * FROM root r WHERE r.id=@id',
                    parameters: [{
                        name: '@id',
                        value: collectionId
                    }]
                };               
   
                client.queryCollections(databaseLink, querySpec).toArray(function (err, results) {
                    if (err) {
                        callback(err);
   
                    } else {        
                        if (results.length === 0) {
                            var collectionSpec = {
                                id: collectionId
                            };
   
                            client.createCollection(databaseLink, collectionSpec, function (err, created) {
                                callback(null, created);
                            });
   
                        } else {
                            callback(null, results[0]);
                        }
                    }
                });
            }
        };
   
        module.exports = DocDBUtils;
   
5. Salve e feche o hello **docdbUtils.js** arquivo.
6. Início de saudação do hello **taskDao.js** de arquivo, adicione Olá Olá de tooreference de código a seguir **DocumentDBClient** e hello **docdbUtils.js** criado anteriormente:
   
        var DocumentDBClient = require('documentdb').DocumentClient;
        var docdbUtils = require('./docdbUtils');
7. Em seguida, você adicionará código toodefine e exportar o objeto de tarefa hello. Isso é responsável por inicializar nosso objeto de tarefa e a configuração Olá banco de dados e o conjunto de documentos, vamos usar.
   
        function TaskDao(documentDBClient, databaseId, collectionId) {
          this.client = documentDBClient;
          this.databaseId = databaseId;
          this.collectionId = collectionId;
   
          this.database = null;
          this.collection = null;
        }
   
        module.exports = TaskDao;
8. Em seguida, adicione Olá métodos adicionais de toodefine de código a seguir em objeto de tarefa hello, que permitem que as interações com os dados armazenados no banco de dados do Azure Cosmos.
   
        TaskDao.prototype = {
            init: function (callback) {
                var self = this;
   
                docdbUtils.getOrCreateDatabase(self.client, self.databaseId, function (err, db) {
                    if (err) {
                        callback(err);
                    } else {
                        self.database = db;
                        docdbUtils.getOrCreateCollection(self.client, self.database._self, self.collectionId, function (err, coll) {
                            if (err) {
                                callback(err);
   
                            } else {
                                self.collection = coll;
                            }
                        });
                    }
                });
            },
   
            find: function (querySpec, callback) {
                var self = this;
   
                self.client.queryDocuments(self.collection._self, querySpec).toArray(function (err, results) {
                    if (err) {
                        callback(err);
   
                    } else {
                        callback(null, results);
                    }
                });
            },
   
            addItem: function (item, callback) {
                var self = this;
   
                item.date = Date.now();
                item.completed = false;
   
                self.client.createDocument(self.collection._self, item, function (err, doc) {
                    if (err) {
                        callback(err);
   
                    } else {
                        callback(null, doc);
                    }
                });
            },
   
            updateItem: function (itemId, callback) {
                var self = this;
   
                self.getItem(itemId, function (err, doc) {
                    if (err) {
                        callback(err);
   
                    } else {
                        doc.completed = true;
   
                        self.client.replaceDocument(doc._self, doc, function (err, replaced) {
                            if (err) {
                                callback(err);
   
                            } else {
                                callback(null, replaced);
                            }
                        });
                    }
                });
            },
   
            getItem: function (itemId, callback) {
                var self = this;
   
                var querySpec = {
                    query: 'SELECT * FROM root r WHERE r.id = @id',
                    parameters: [{
                        name: '@id',
                        value: itemId
                    }]
                };
   
                self.client.queryDocuments(self.collection._self, querySpec).toArray(function (err, results) {
                    if (err) {
                        callback(err);
   
                    } else {
                        callback(null, results[0]);
                    }
                });
            }
        };
9. Salve e feche o hello **taskDao.js** arquivo. 

### <a name="create-hello-controller"></a>Criar hello controlador
1. Em Olá **rotas** diretório do projeto, criar um novo arquivo denominado **tasklist.js**. 
2. Adicionar Olá código a seguir muito**tasklist.js**. Isso carrega Olá DocumentDBClient e async módulos, que são usados por **tasklist.js**. Isso também definido Olá **TaskList** função, que é passada a uma instância do hello **tarefa** objeto definimos anteriormente:
   
        var DocumentDBClient = require('documentdb').DocumentClient;
        var async = require('async');
   
        function TaskList(taskDao) {
          this.taskDao = taskDao;
        }
   
        module.exports = TaskList;
3. Continue adicionando toohello **tasklist.js** arquivo adicionando métodos de saudação usados muito**showTasks, addTask**, e **completeTasks**:
   
        TaskList.prototype = {
            showTasks: function (req, res) {
                var self = this;
   
                var querySpec = {
                    query: 'SELECT * FROM root r WHERE r.completed=@completed',
                    parameters: [{
                        name: '@completed',
                        value: false
                    }]
                };
   
                self.taskDao.find(querySpec, function (err, items) {
                    if (err) {
                        throw (err);
                    }
   
                    res.render('index', {
                        title: 'My ToDo List ',
                        tasks: items
                    });
                });
            },
   
            addTask: function (req, res) {
                var self = this;
                var item = req.body;
   
                self.taskDao.addItem(item, function (err) {
                    if (err) {
                        throw (err);
                    }
   
                    res.redirect('/');
                });
            },
   
            completeTask: function (req, res) {
                var self = this;
                var completedTasks = Object.keys(req.body);
   
                async.forEach(completedTasks, function taskIterator(completedTask, callback) {
                    self.taskDao.updateItem(completedTask, function (err) {
                        if (err) {
                            callback(err);
                        } else {
                            callback(null);
                        }
                    });
                }, function goHome(err) {
                    if (err) {
                        throw err;
                    } else {
                        res.redirect('/');
                    }
                });
            }
        };
4. Salve e feche o hello **tasklist.js** arquivo.

### <a name="add-configjs"></a>Adicionar config.js
1. No diretório do projeto, crie um novo arquivo chamado **config.js**.
2. Adicionar Olá seguir muito**config.js**. Isso define as configurações e valores necessários para nosso aplicativo.
   
        var config = {}
   
        config.host = process.env.HOST || "[hello URI value from hello Azure Cosmos DB Keys blade on http://portal.azure.com]";
        config.authKey = process.env.AUTH_KEY || "[hello PRIMARY KEY value from hello Azure Cosmos DB Keys blade on http://portal.azure.com]";
        config.databaseId = "ToDoList";
        config.collectionId = "Items";
   
        module.exports = config;
3. Em Olá **config.js** arquivo atualizar valores de saudação do HOST e AUTH_KEY usando valores hello encontrados na folha de chaves de saudação da sua conta de banco de dados do Azure Cosmos Olá [portal do Microsoft Azure](https://portal.azure.com).
4. Salve e feche o hello **config.js** arquivo.

### <a name="modify-appjs"></a>Modificar app.js
1. No diretório do projeto hello, abra Olá **app.js** arquivo. Este arquivo foi criado anteriormente ao aplicativo de web Express hello foi criado.
2. Adicionar Olá seguir superior de toohello código de **app.js**
   
        var DocumentDBClient = require('documentdb').DocumentClient;
        var config = require('./config');
        var TaskList = require('./routes/tasklist');
        var TaskDao = require('./models/taskDao');
3. Esse código define Olá toobe de arquivo de configuração usado e continua tooread valores desse arquivo para algumas variáveis que usaremos em breve.
4. Substituir saudação duas linhas a seguir **app.js** arquivo:
   
        app.use('/', index);
        app.use('/users', users); 
   
      com hello trecho de código a seguir:
   
        var docDbClient = new DocumentDBClient(config.host, {
            masterKey: config.authKey
        });
        var taskDao = new TaskDao(docDbClient, config.databaseId, config.collectionId);
        var taskList = new TaskList(taskDao);
        taskDao.init();
   
        app.get('/', taskList.showTasks.bind(taskList));
        app.post('/addtask', taskList.addTask.bind(taskList));
        app.post('/completetask', taskList.completeTask.bind(taskList));
        app.set('view engine', 'jade');
5. Essas linhas definem uma nova instância da nossa **TaskDao** objeto, com um novo tooAzure de conexão Cosmos DB (usando valores hello leia Olá **config.js**), inicializar o objeto de tarefa hello e, em seguida, associar ações do formulário toomethods em nosso **TaskList** controlador. 
6. Por fim, salve e feche o hello **app.js** arquivo, quase pronto.

## <a name="_Toc395783181"></a>Etapa 5: Criar uma interface do usuário
Agora vamos examinar nossa interface do usuário atenção toobuilding Olá para um usuário, na verdade, pode interagir com o nosso aplicativo. Olá aplicativo Express criamos usa **Jade** como mecanismo de exibição de saudação. Para obter mais informações sobre Jade consulte muito[http://jade-lang.com/](http://jade-lang.com/).

1. Olá **layout.jade** arquivo hello **exibições** diretório é usado como um modelo global para outros **.jade** arquivos. Nesta etapa você modificá-la toouse [Twitter Bootstrap](https://github.com/twbs/bootstrap), que é um kit de ferramentas que torna mais fácil toodesign um site de aparência adequado. 
2. Olá abrir **layout.jade** arquivo encontrado em Olá **exibições** pasta e substitua conteúdo Olá com os seguintes hello:

    ```
    doctype html
    html
      head
        title= title
        link(rel='stylesheet', href='//ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/css/bootstrap.min.css')
        link(rel='stylesheet', href='/stylesheets/style.css')
      body
        nav.navbar.navbar-inverse.navbar-fixed-top
          div.navbar-header
            a.navbar-brand(href='#') My Tasks
        block content
        script(src='//ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.2.min.js')
        script(src='//ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/bootstrap.min.js')
    ```

    Isso indica efetivamente Olá **Jade** mecanismo toorender alguns HTML para nosso aplicativo e cria um **bloco** chamado **conteúdo** onde é possível fornecer o layout de saudação para nosso conteúdo páginas.

    Salve e feche o arquivo **layout.jade** .

3. Agora, abra Olá **Jade** arquivo, a exibição Olá que será usada pelo nosso aplicativo e substitua o conteúdo de saudação do arquivo hello pela seguinte hello:
   
        extends layout
        block content
           h1 #{title}
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
                     td #{task.name}
                     td #{task.category}
                     - var date  = new Date(task.date);
                     - var day   = date.getDate();
                     - var month = date.getMonth() + 1;
                     - var year  = date.getFullYear();
                     td #{month + "/" + day + "/" + year}
                     td
                       input(type="checkbox", name="#{task.id}", value="#{!task.completed}", checked=task.completed)
             button.btn.btn-primary(type="submit") Update tasks
           hr
           form.well(action="/addtask", method="post")
             .form-group
               label(for="name") Item Name:
               input.form-control(name="name", type="textbox")
             .form-group
               label(for="category") Item Category:
               input.form-control(name="category", type="textbox")
             br
             button.btn(type="submit") Add item
   

Isso estende o layout e fornece o conteúdo Olá **conteúdo** espaço reservado que vimos em Olá **layout.jade** arquivo anteriormente.
   
Nesse layout criamos dois formulários HTML.

formulário primeiro Olá contém uma tabela para nossos dados e um botão que nos permite tooupdate itens postando muito**/completetask** método do nosso controlador.
    
segunda forma de saudação contém dois campos de entrada e um botão que nos permite toocreate um novo item postando muito**/addtask** método do nosso controlador.

Isso deve ser tudo o que precisamos para nossa toowork de aplicativo.

## <a name="_Toc395783181"></a>Etapa 6: Execute o seu aplicativo localmente
1. aplicativo de hello tootest em seu computador local, execute `npm start` em Olá terminal toostart seu aplicativo e atualize seu [http://localhost:3000](http://localhost:3000) página do navegador. página Olá deve agora ser semelhante Olá imagem abaixo:
   
    ![Captura de tela da saudação aplicativo MyTodo lista em uma janela do navegador](./media/documentdb-nodejs-application/cosmos-db-node-js-localhost.png)

    > [!TIP]
    > Se você receber um erro sobre Olá recuo no arquivo de layout.jade hello ou Olá Jade, certifique-se de que duas primeiras linhas Olá em ambos os arquivos é justificado à esquerda, sem espaços. Se houver espaços antes duas primeiras linhas de saudação, removê-los, salve os dois arquivos e atualizar a janela do navegador. 

2. Use Olá campos de Item, o nome do Item e categoria tooenter uma nova tarefa e, em seguida, clique em **Adicionar Item**. Isso cria um documento no Azure Cosmos DB com essas propriedades. 
3. página Olá deve atualizar Olá toodisplay recém-criado item na lista de tarefas de saudação.
   
    ![Captura de tela do aplicativo hello com um novo item na lista de tarefas de saudação](./media/documentdb-nodejs-application/cosmos-db-node-js-added-task.png)
4. toocomplete uma tarefa, basta marcar Olá a caixa de seleção na coluna completa hello e, em seguida, clique em **atualizar tarefas**. Isso atualiza o documento de saudação já criado.

5. aplicativo de hello toostop, pressione CTRL + C na janela do terminal hello e, em seguida, clique em **Y** tooterminate trabalho de lote de saudação.

## <a name="_Toc395783182"></a>Etapa 7: Implantar o tooAzure de projeto de desenvolvimento de aplicativo sites
1. Se ainda não o fez, habilite um repositório git do seu site do Azure. Você pode encontrar instruções sobre como toodo isso em Olá [tooAzure de implantação Local do Git do serviço de aplicativo](../app-service-web/app-service-deploy-local-git.md) tópico.
2. Adicione seu site do Azure como um git remoto.
   
        git remote add azure https://username@your-azure-website.scm.azurewebsites.net:443/your-azure-website.git
3. Implante por push toohello remoto.
   
        git push azure master
4. Em poucos segundos, o git terminará de publicar seu aplicativo Web e iniciará um navegador onde você poderá ver seu trabalho sendo executado no Azure!

    Parabéns! Você acabou de criado seu primeiro Node. js Express aplicativo Web usando o banco de dados do Azure Cosmos e publicá-la tooAzure sites.

    Se você quiser toodownload ou consulte aplicativos de referência completa de toohello para este tutorial, ele pode ser baixado de [GitHub][GitHub].

## <a name="_Toc395637775"></a>Próximas etapas

* Deseja tooperform escala e testes de desempenho com o banco de dados do Azure Cosmos? Confira [teste de desempenho e escalabilidade com o Azure Cosmos DB](performance-testing.md)
* Saiba como muito[monitorar uma conta de banco de dados do Azure Cosmos](monitor-accounts.md).
* Executar consultas em nosso conjunto de dados de exemplo hello [parque de consulta](https://www.documentdb.com/sql/demo).
* Explorar Olá [documentação de banco de dados do Azure Cosmos](https://docs.microsoft.com/azure/documentdb/).

[Node.js]: http://nodejs.org/
[Git]: http://git-scm.com/
[GitHub]: https://github.com/Azure-Samples/documentdb-node-todo-app

