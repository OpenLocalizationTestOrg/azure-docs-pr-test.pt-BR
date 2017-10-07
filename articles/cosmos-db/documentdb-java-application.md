---
title: tutorial de desenvolvimento de aplicativo aaaJava usando o banco de dados do Azure Cosmos | Microsoft Docs
description: "Este tutorial de aplicativo web Java mostra como toouse hello Azure Cosmos DB Olá toostore API DocumentDB e acessar dados de um aplicativo Java hospedado em sites do Azure."
keywords: Desenvolvimento de aplicativos, tutorial de banco de dados, aplicativo java, tutorial do aplicativo web java, banco de dados de documentos, azure, Microsoft azure
services: cosmos-db
documentationcenter: java
author: dennyglee
manager: jhubbard
editor: mimig
ms.assetid: 0867a4a2-4bf5-4898-a1f4-44e3868f8725
ms.service: cosmos-db
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.date: 08/22/2017
ms.author: denlee
ms.openlocfilehash: e073de23beb0037ee1e37b48a69e8fe7cdc3fc1d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="build-a-java-web-application-using-azure-cosmos-db-and-hello-documentdb-api"></a>Criar um aplicativo da web de Java usando o banco de dados do Azure Cosmos e hello API DocumentDB
> [!div class="op_single_selector"]
> * [.NET](documentdb-dotnet-application.md)
> * [Node.js](documentdb-nodejs-application.md)
> * [Java](documentdb-java-application.md)
> * [Python](documentdb-python-application.md)
> 
> 

Este tutorial de aplicativo web Java mostra como Olá toouse [banco de dados do Microsoft Azure Cosmos](https://azure.microsoft.com/services/cosmos-db/) toostore e acessar dados de um aplicativo Java hospedado em aplicativos de Web do serviço de aplicativo do Azure service. Neste tópico, você aprenderá:

* Como toobuild um aplicativo básico do JavaServer Pages (JSP) no Eclipse.
* Como toowork com hello Azure Cosmos DB serviço usando Olá [SDK de Java do Azure Cosmos DB](https://github.com/Azure/azure-documentdb-java).

Este tutorial de aplicativo Java mostra como o aplicativo de gerenciamento de tarefas de toocreate baseado na web, que permite marcar, recuperar e você toocreate tarefas como concluída, conforme mostrado no Olá a imagem a seguir. Cada uma das tarefas de saudação na lista de tarefas de saudação são armazenadas como documentos JSON no banco de dados do Azure Cosmos.

![Aplicativo Java Minha lista de tarefas pendentes](./media/documentdb-java-application/image1.png)

> [!TIP]
> Este tutorial de desenvolvimento de aplicativo presume que você tenha experiência anterior com o Java. Se você for novo tooJava ou Olá [ferramentas pré-requisito](#Prerequisites), recomendamos o download Olá completa [todo](https://github.com/Azure-Samples/documentdb-java-todo-app) projeto do GitHub e compilá-lo usando [Olá instruções no final da saudação deste artigo](#GetProject). Depois de criado, você pode examinar informações de toogain artigo Olá no código Olá no contexto de saudação do projeto hello.  
> 
> 

## <a id="Prerequisites"></a>Pré-requisitos para este tutorial de aplicativo Web Java
Antes de começar este tutorial de desenvolvimento de aplicativo, você deve ter o seguinte hello:

* Uma conta ativa do Azure. Se você não tiver uma conta, poderá criar uma conta de avaliação gratuita em apenas alguns minutos. Para obter detalhes, consulte [Avaliação gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/)

    OU

    Uma instalação local do hello [emulador de banco de dados do Azure Cosmos](local-emulator.md).
* [Java Development Kit (JDK) 7 +](http://www.oracle.com/technetwork/java/javase/downloads/index.html).
* [Eclipse IDE para desenvolvedores de Java EE.](http://www.eclipse.org/downloads/packages/eclipse-ide-java-ee-developers/lunasr1)
* [Um site do Azure com um Java runtime environment (por exemplo, Tomcat ou Jetty) habilitado.](../app-service-web/web-sites-java-get-started.md)

Se você estiver instalando essas ferramentas para Olá a primeira vez, coreservlets.com fornece uma passo a passo do processo de instalação de saudação na seção de início rápido de saudação do seu [Tutorial: Instalando TomCat7 e usá-lo com o Eclipse](http://www.coreservlets.com/Apache-Tomcat-Tutorial/tomcat-7-with-eclipse.html) artigo.

## <a id="CreateDB"></a>Etapa 1: Criar uma conta de banco de dados do Azure Cosmos DB
Vamos começar criando uma conta do Azure Cosmos DB. Se você já tiver uma conta ou se você estiver usando hello Azure Cosmos DB emulador para este tutorial, você poderá ignorar muito[etapa 2: criar o aplicativo de Java JSP hello](#CreateJSP).

[!INCLUDE [create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

[!INCLUDE [keys](../../includes/cosmos-db-keys.md)]

## <a id="CreateJSP"></a>Etapa 2: Criar um aplicativo de Java JSP hello
Olá toocreate aplicativo JSP:

1. Primeiro, começaremos criando um projeto Java. Inicie o Eclipse, clique em **Arquivo**, **Novo** e clique em **Projeto Web dinâmico**. Se você não vir **projeto Web dinâmico** listado como um projeto disponível, Olá a seguir: clique em **arquivo**, clique em **novo**, clique em **projeto**..., expanda **Web**, clique em **projeto Web dinâmico**e clique em **próximo**.
   
    ![Desenvolvimento de aplicativo Java JSP](./media/documentdb-java-application/image10.png)
2. Insira um nome de projeto em Olá **nome do projeto** caixa e em Olá **tempo de execução de destino** menu suspenso, selecione, opcionalmente, um valor (por exemplo, Apache Tomcat v 7.0) e, em seguida, clique em **concluir**. Selecionar um destino de tempo de execução permite que você toorun seu projeto localmente por meio do Eclipse.
3. No Eclipse, na exibição do Explorador de projeto hello, expanda seu projeto. Clique com o botão direito do mouse em **WebContent**, clique em **Novo** e, em seguida, clique em **Arquivo JSP**.
4. Em Olá **novo arquivo JSP** caixa de diálogo, o arquivo de saudação do nome **index.jsp**. Mantenha a pasta pai Olá **WebContent**, conforme mostrado no Olá a ilustração a seguir e, em seguida, clique em **próximo**.
   
    ![Criar um novo arquivo JSP — tutorial de aplicativo Web Java](./media/documentdb-java-application/image11.png)
5. Em Olá **Selecionar modelo JSP** caixa de diálogo para finalidade de saudação deste tutorial, selecione **novo arquivo JSP (html)**e, em seguida, clique em **concluir**.
6. Quando o arquivo do hello index.jsp for aberto no Eclipse, adicionar texto toodisplay **Olá, mundo!** dentro de saudação existente <body> elemento. Seu atualizada <body> conteúdo deve ter aparência Olá código a seguir:
   
        <body>
            <% out.println("Hello World!"); %>
        </body>
7. Salve o arquivo index.jsp de saudação.
8. Se você definir um tempo de execução de destino na etapa 2, você pode clicar em **projeto** e **executar** toorun aplicativo JSP localmente:
   
    ![Hello World — tutorial de aplicativo Java](./media/documentdb-java-application/image12.png)

## <a id="InstallSDK"></a>Etapa 3: Instalar Olá SDK de Java do DocumentDB
Olá toopull de maneira mais fácil no hello SDK de Java do DocumentDB e suas dependências é por meio de [Apache Maven](http://maven.apache.org/).

toodo isso, você precisará tooconvert seu projeto do projeto tooa maven Concluindo Olá etapas a seguir:

1. Seu projeto no hello Explorador de projeto, clique **configurar**, clique em **converter tooMaven projeto**.
2. Em Olá **criar novo POM** janela, aceite os padrões de saudação e clique em **concluir**.
3. Em **Explorador de projeto**, abrir arquivo de pom.xml hello.
4. Em Olá **dependências** guia Olá **dependências** painel, clique em **adicionar**.
5. Em Olá **selecione dependência** janela, Olá a seguir:
   
   * Em Olá **Id do grupo** , digite com.microsoft.azure.
   * Em Olá **Id do artefato** , digite documentdb do azure.
   * Em Olá **versão** , digite 1.5.1.
     
   ![Instalar o SDK do aplicativo Java para DocumentDB](./media/documentdb-java-application/image13.png)
     
   * Ou Adicionar dependência Olá XML para o Id de grupo e a Id de artefato diretamente toohello pom.xml por meio de um editor de texto:
     
        <dependency> <groupId>com.microsoft.azure</groupId> <artifactId>azure-documentdb</artifactId> <version>1.9.1</version> </dependency>
6. Clique em **Okey** e Maven instalará Olá SDK de Java do DocumentDB.
7. Salve o arquivo de pom.xml hello.

## <a id="UseService"></a>Etapa 4: Usando o serviço de banco de dados do Azure Cosmos Olá em um aplicativo Java
1. Primeiro, vamos definir objeto de TodoItem Olá em TodoItem.java:
   
        @Data
        @Builder
        public class TodoItem {
            private String category;
            private boolean complete;
            private String id;
            private String name;
        }
   
    Este projeto, estamos usando [Lombok projeto](http://projectlombok.org/) toogenerate Olá construtor, getters, setters e um construtor. Como alternativa, você pode gravar este código manualmente ou ter Olá IDE gerá-lo.
2. serviço de banco de dados do Azure Cosmos de saudação tooinvoke, você deve criar um novo **DocumentClient**. Em geral, é melhor Olá de tooreuse **DocumentClient** - em vez de criar um novo cliente para cada solicitação subsequente. Cliente Olá pode ser reutilizado por quebra automática de cliente de saudação em uma **DocumentClientFactory**. Em DocumentClientFactory.java, você precisa toopaste Olá URI e chave primária valor salvo tooyour a área de transferência em [etapa 1](#CreateDB). Substitua [SEU\_PONTODEEXTREMIDADE\_AQUI] pelo seu URI e substitua [SUA\_CHAVE\_AQUI] pela sua chave primária.
   
        private static final String HOST = "[YOUR_ENDPOINT_HERE]";
        private static final String MASTER_KEY = "[YOUR_KEY_HERE]";
   
        private static DocumentClient documentClient = new DocumentClient(HOST, MASTER_KEY,
                        ConnectionPolicy.GetDefault(), ConsistencyLevel.Session);
   
        public static DocumentClient getDocumentClient() {
            return documentClient;
        }
3. Agora vamos criar um tooabstract Data Access Object (DAO) persistentes nosso tooAzure de itens de ToDo banco de dados do Cosmos.
   
    Em ordem de itens de tarefas toosave tooa coleção, Olá cliente precisa toopersist qual banco de dados e coleção de tooknow muito (como referenciada por links automáticos). Em geral, é o banco de dados do melhor toocache hello e coleção quando possível tooavoid banco de dados de toohello de ida e volta adicionais.
   
    Olá código a seguir ilustra como tooretrieve nosso banco de dados e a coleção, se ele existir, ou crie um novo se não existir:
   
        public class DocDbDao implements TodoDao {
            // hello name of our database.
            private static final String DATABASE_ID = "TodoDB";
   
            // hello name of our collection.
            private static final String COLLECTION_ID = "TodoCollection";
   
            // hello Azure Cosmos DB Client
            private static DocumentClient documentClient = DocumentClientFactory
                    .getDocumentClient();
   
            // Cache for hello database object, so we don't have tooquery for it to
            // retrieve self links.
            private static Database databaseCache;
   
            // Cache for hello collection object, so we don't have tooquery for it to
            // retrieve self links.
            private static DocumentCollection collectionCache;
   
            private Database getTodoDatabase() {
                if (databaseCache == null) {
                    // Get hello database if it exists
                    List<Database> databaseList = documentClient
                            .queryDatabases(
                                    "SELECT * FROM root r WHERE r.id='" + DATABASE_ID
                                            + "'", null).getQueryIterable().toList();
   
                    if (databaseList.size() > 0) {
                        // Cache hello database object so we won't have tooquery for it
                        // later tooretrieve hello selfLink.
                        databaseCache = databaseList.get(0);
                    } else {
                        // Create hello database if it doesn't exist.
                        try {
                            Database databaseDefinition = new Database();
                            databaseDefinition.setId(DATABASE_ID);
   
                            databaseCache = documentClient.createDatabase(
                                    databaseDefinition, null).getResource();
                        } catch (DocumentClientException e) {
                            // TODO: Something has gone terribly wrong - hello app wasn't
                            // able tooquery or create hello collection.
                            // Verify your connection, endpoint, and key.
                            e.printStackTrace();
                        }
                    }
                }
   
                return databaseCache;
            }
   
            private DocumentCollection getTodoCollection() {
                if (collectionCache == null) {
                    // Get hello collection if it exists.
                    List<DocumentCollection> collectionList = documentClient
                            .queryCollections(
                                    getTodoDatabase().getSelfLink(),
                                    "SELECT * FROM root r WHERE r.id='" + COLLECTION_ID
                                            + "'", null).getQueryIterable().toList();
   
                    if (collectionList.size() > 0) {
                        // Cache hello collection object so we won't have tooquery for it
                        // later tooretrieve hello selfLink.
                        collectionCache = collectionList.get(0);
                    } else {
                        // Create hello collection if it doesn't exist.
                        try {
                            DocumentCollection collectionDefinition = new DocumentCollection();
                            collectionDefinition.setId(COLLECTION_ID);
   
                            collectionCache = documentClient.createCollection(
                                    getTodoDatabase().getSelfLink(),
                                    collectionDefinition, null).getResource();
                        } catch (DocumentClientException e) {
                            // TODO: Something has gone terribly wrong - hello app wasn't
                            // able tooquery or create hello collection.
                            // Verify your connection, endpoint, and key.
                            e.printStackTrace();
                        }
                    }
                }
   
                return collectionCache;
            }
        }
4. próxima etapa do Hello é toowrite alguns hello de toopersist de código TodoItems na coleção toohello. Neste exemplo, usaremos [Gson](https://code.google.com/p/google-gson/) tooserialize e desserializar documentos de tooJSON TodoItem POJOs Plain Old Java Objects ().
   
        // We'll use Gson for POJO <=> JSON serialization for this example.
        private static Gson gson = new Gson();
   
        @Override
        public TodoItem createTodoItem(TodoItem todoItem) {
            // Serialize hello TodoItem as a JSON Document.
            Document todoItemDocument = new Document(gson.toJson(todoItem));
   
            // Annotate hello document as a TodoItem for retrieval (so that we can
            // store multiple entity types in hello collection).
            todoItemDocument.set("entityType", "todoItem");
   
            try {
                // Persist hello document using hello DocumentClient.
                todoItemDocument = documentClient.createDocument(
                        getTodoCollection().getSelfLink(), todoItemDocument, null,
                        false).getResource();
            } catch (DocumentClientException e) {
                e.printStackTrace();
                return null;
            }
   
            return gson.fromJson(todoItemDocument.toString(), TodoItem.class);
        }
5. Assim como os bancos de dados e coleções do Azure Cosmos DB, os documentos também são referenciados por self-links. Olá permite a função auxiliar a seguir nos recuperar documentos por outro atributo (por exemplo, "id") em vez de vínculo automático:
   
        private Document getDocumentById(String id) {
            // Retrieve hello document using hello DocumentClient.
            List<Document> documentList = documentClient
                    .queryDocuments(getTodoCollection().getSelfLink(),
                            "SELECT * FROM root r WHERE r.id='" + id + "'", null)
                    .getQueryIterable().toList();
   
            if (documentList.size() > 0) {
                return documentList.get(0);
            } else {
                return null;
            }
        }
6. Podemos usar o método auxiliar de saudação na etapa 5 tooretrieve um documento JSON TodoItem por id e desserializá-la tooa POJO:
   
        @Override
        public TodoItem readTodoItem(String id) {
            // Retrieve hello document by id using our helper method.
            Document todoItemDocument = getDocumentById(id);
   
            if (todoItemDocument != null) {
                // De-serialize hello document in tooa TodoItem.
                return gson.fromJson(todoItemDocument.toString(), TodoItem.class);
            } else {
                return null;
            }
        }
7. Também podemos usar Olá DocumentClient tooget uma coleção ou uma lista de TodoItems usando SQL do DocumentDB:
   
        @Override
        public List<TodoItem> readTodoItems() {
            List<TodoItem> todoItems = new ArrayList<TodoItem>();
   
            // Retrieve hello TodoItem documents
            List<Document> documentList = documentClient
                    .queryDocuments(getTodoCollection().getSelfLink(),
                            "SELECT * FROM root r WHERE r.entityType = 'todoItem'",
                            null).getQueryIterable().toList();
   
            // De-serialize hello documents in tooTodoItems.
            for (Document todoItemDocument : documentList) {
                todoItems.add(gson.fromJson(todoItemDocument.toString(),
                        TodoItem.class));
            }
   
            return todoItems;
        }
8. Há tooupdate de muitas maneiras de um documento com hello DocumentClient. Em nosso aplicativo de lista de tarefas, queremos tootoggle capaz de toobe se um TodoItem é concluído. Isso pode ser feito atualizando o atributo "concluído" no documento de saudação do hello:
   
        @Override
        public TodoItem updateTodoItem(String id, boolean isComplete) {
            // Retrieve hello document from hello database
            Document todoItemDocument = getDocumentById(id);
   
            // You can update hello document as a JSON document directly.
            // For more complex operations - you could de-serialize hello document in
            // tooa POJO, update hello POJO, and then re-serialize hello POJO back in to
            // a document.
            todoItemDocument.set("complete", isComplete);
   
            try {
                // Persist/replace hello updated document.
                todoItemDocument = documentClient.replaceDocument(todoItemDocument,
                        null).getResource();
            } catch (DocumentClientException e) {
                e.printStackTrace();
                return null;
            }
   
            return gson.fromJson(todoItemDocument.toString(), TodoItem.class);
        }
9. Por fim, queremos Olá capacidade toodelete um TodoItem de nossa lista. toodo isso, podemos usar o método auxiliar de saudação escrevemos anteriormente tooretrieve Olá vínculo automático e, em seguida, diga Olá cliente toodelete-lo:
   
        @Override
        public boolean deleteTodoItem(String id) {
            // Azure Cosmos DB refers toodocuments by self link rather than id.
   
            // Query for hello document tooretrieve hello self link.
            Document todoItemDocument = getDocumentById(id);
   
            try {
                // Delete hello document by self link.
                documentClient.deleteDocument(todoItemDocument.getSelfLink(), null);
            } catch (DocumentClientException e) {
                e.printStackTrace();
                return false;
            }
   
            return true;
        }

## <a id="Wire"></a>Etapa 5: Fiação restante Olá Olá do projeto de desenvolvimento de aplicativos Java em conjunto
Agora que concluímos fun Olá bits - resta é toobuild uma interface do usuário rápida e conectá-lo tooour DAO.

1. Primeiro, vamos começar com a criação de um controlador toocall nosso DAO:
   
        public class TodoItemController {
            public static TodoItemController getInstance() {
                if (todoItemController == null) {
                    todoItemController = new TodoItemController(TodoDaoFactory.getDao());
                }
                return todoItemController;
            }
   
            private static TodoItemController todoItemController;
   
            private final TodoDao todoDao;
   
            TodoItemController(TodoDao todoDao) {
                this.todoDao = todoDao;
            }
   
            public TodoItem createTodoItem(@NonNull String name,
                    @NonNull String category, boolean isComplete) {
                TodoItem todoItem = TodoItem.builder().name(name).category(category)
                        .complete(isComplete).build();
                return todoDao.createTodoItem(todoItem);
            }
   
            public boolean deleteTodoItem(@NonNull String id) {
                return todoDao.deleteTodoItem(id);
            }
   
            public TodoItem getTodoItemById(@NonNull String id) {
                return todoDao.readTodoItem(id);
            }
   
            public List<TodoItem> getTodoItems() {
                return todoDao.readTodoItems();
            }
   
            public TodoItem updateTodoItem(@NonNull String id, boolean isComplete) {
                return todoDao.updateTodoItem(id, isComplete);
            }
        }
   
    Em um aplicativo mais complexo, controlador Olá pode hospedar a lógica de negócios complicado sobre Olá DAO.
2. Em seguida, vamos criar um controlador de toohello solicitações HTTP do servlet tooroute:
   
        public class TodoServlet extends HttpServlet {
            // API Keys
            public static final String API_METHOD = "method";
   
            // API Methods
            public static final String CREATE_TODO_ITEM = "createTodoItem";
            public static final String GET_TODO_ITEMS = "getTodoItems";
            public static final String UPDATE_TODO_ITEM = "updateTodoItem";
   
            // API Parameters
            public static final String TODO_ITEM_ID = "todoItemId";
            public static final String TODO_ITEM_NAME = "todoItemName";
            public static final String TODO_ITEM_CATEGORY = "todoItemCategory";
            public static final String TODO_ITEM_COMPLETE = "todoItemComplete";
   
            public static final String MESSAGE_ERROR_INVALID_METHOD = "{'error': 'Invalid method'}";
   
            private static final long serialVersionUID = 1L;
            private static final Gson gson = new Gson();
   
            @Override
            protected void doGet(HttpServletRequest request,
                    HttpServletResponse response) throws ServletException, IOException {
   
                String apiResponse = MESSAGE_ERROR_INVALID_METHOD;
   
                TodoItemController todoItemController = TodoItemController
                        .getInstance();
   
                String id = request.getParameter(TODO_ITEM_ID);
                String name = request.getParameter(TODO_ITEM_NAME);
                String category = request.getParameter(TODO_ITEM_CATEGORY);
                boolean isComplete = StringUtils.equalsIgnoreCase("true",
                        request.getParameter(TODO_ITEM_COMPLETE)) ? true : false;
   
                switch (request.getParameter(API_METHOD)) {
                case CREATE_TODO_ITEM:
                    apiResponse = gson.toJson(todoItemController.createTodoItem(name,
                            category, isComplete));
                    break;
                case GET_TODO_ITEMS:
                    apiResponse = gson.toJson(todoItemController.getTodoItems());
                    break;
                case UPDATE_TODO_ITEM:
                    apiResponse = gson.toJson(todoItemController.updateTodoItem(id,
                            isComplete));
                    break;
                default:
                    break;
                }
   
                response.getWriter().println(apiResponse);
            }
   
            @Override
            protected void doPost(HttpServletRequest request,
                    HttpServletResponse response) throws ServletException, IOException {
                doGet(request, response);
            }
        }
3. Precisaremos de usuário da web usuário interface toodisplay toohello. Vamos reescrever Olá JSP criado anteriormente:
    ```html
        <html>
        <head>
          <meta http-equiv="Content-Type" content="text/html; charset=ISO-8859-1">
          <meta http-equiv="X-UA-Compatible" content="IE=edge;" />
          <title>Azure Cosmos DB Java Sample</title>
   
          <!-- Bootstrap -->
          <link href="//ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/css/bootstrap.min.css" rel="stylesheet">
   
          <style>
            /* Add padding toobody for fixed nav bar */
            body {
              padding-top: 50px;
            }
          </style>
        </head>
        <body>
          <!-- Nav Bar -->
          <div class="navbar navbar-inverse navbar-fixed-top" role="navigation">
            <div class="container">
              <div class="navbar-header">
                <a class="navbar-brand" href="#">My Tasks</a>
              </div>
            </div>
          </div>
   
          <!-- Body -->
          <div class="container">
            <h1>My ToDo List</h1>
   
            <hr/>
   
            <!-- hello ToDo List -->
            <div class = "todoList">
              <table class="table table-bordered table-striped" id="todoItems">
                <thead>
                  <tr>
                    <th>Name</th>
                    <th>Category</th>
                    <th>Complete</th>
                  </tr>
                </thead>
                <tbody>
                </tbody>
              </table>
   
              <!-- Update Button -->
              <div class="todoUpdatePanel">
                <form class="form-horizontal" role="form">
                  <button type="button" class="btn btn-primary">Update Tasks</button>
                </form>
              </div>
   
            </div>
   
            <hr/>
   
            <!-- Item Input Form -->
            <div class="todoForm">
              <form class="form-horizontal" role="form">
                <div class="form-group">
                  <label for="inputItemName" class="col-sm-2">Task Name</label>
                  <div class="col-sm-10">
                    <input type="text" class="form-control" id="inputItemName" placeholder="Enter name">
                  </div>
                </div>
   
                <div class="form-group">
                  <label for="inputItemCategory" class="col-sm-2">Task Category</label>
                  <div class="col-sm-10">
                    <input type="text" class="form-control" id="inputItemCategory" placeholder="Enter category">
                  </div>
                </div>
   
                <button type="button" class="btn btn-primary">Add Task</button>
              </form>
            </div>
   
          </div>
   
          <!-- Placed at hello end of hello document so hello pages load faster -->
          <script src="//ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.1.min.js"></script>
          <script src="//ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/bootstrap.min.js"></script>
          <script src="assets/todo.js"></script>
        </body>
        </html>
    ```
4. Por fim, gravar alguma interface de usuário do lado do cliente JavaScript tootie Olá web e Olá servlet juntos:
   
        var todoApp = {
          /*
           * API methods toocall Java backend.
           */
          apiEndpoint: "api",
   
          createTodoItem: function(name, category, isComplete) {
            $.post(todoApp.apiEndpoint, {
                "method": "createTodoItem",
                "todoItemName": name,
                "todoItemCategory": category,
                "todoItemComplete": isComplete
              },
              function(data) {
                var todoItem = data;
                todoApp.addTodoItemToTable(todoItem.id, todoItem.name, todoItem.category, todoItem.complete);
              },
              "json");
          },
   
          getTodoItems: function() {
            $.post(todoApp.apiEndpoint, {
                "method": "getTodoItems"
              },
              function(data) {
                var todoItemArr = data;
                $.each(todoItemArr, function(index, value) {
                  todoApp.addTodoItemToTable(value.id, value.name, value.category, value.complete);
                });
              },
              "json");
          },
   
          updateTodoItem: function(id, isComplete) {
            $.post(todoApp.apiEndpoint, {
                "method": "updateTodoItem",
                "todoItemId": id,
                "todoItemComplete": isComplete
              },
              function(data) {},
              "json");
          },
   
          /*
           * UI Methods
           */
          addTodoItemToTable: function(id, name, category, isComplete) {
            var rowColor = isComplete ? "active" : "warning";
   
            todoApp.ui_table().append($("<tr>")
              .append($("<td>").text(name))
              .append($("<td>").text(category))
              .append($("<td>")
                .append($("<input>")
                  .attr("type", "checkbox")
                  .attr("id", id)
                  .attr("checked", isComplete)
                  .attr("class", "isComplete")
                ))
              .addClass(rowColor)
            );
          },
   
          /*
           * UI Bindings
           */
          bindCreateButton: function() {
            todoApp.ui_createButton().click(function() {
              todoApp.createTodoItem(todoApp.ui_createNameInput().val(), todoApp.ui_createCategoryInput().val(), false);
              todoApp.ui_createNameInput().val("");
              todoApp.ui_createCategoryInput().val("");
            });
          },
   
          bindUpdateButton: function() {
            todoApp.ui_updateButton().click(function() {
              // Disable button temporarily.
              var myButton = $(this);
              var originalText = myButton.text();
              $(this).text("Updating...");
              $(this).prop("disabled", true);
   
              // Call api tooupdate todo items.
              $.each(todoApp.ui_updateId(), function(index, value) {
                todoApp.updateTodoItem(value.name, value.value);
                $(value).remove();
              });
   
              // Re-enable button.
              setTimeout(function() {
                myButton.prop("disabled", false);
                myButton.text(originalText);
              }, 500);
            });
          },
   
          bindUpdateCheckboxes: function() {
            todoApp.ui_table().on("click", ".isComplete", function(event) {
              var checkboxElement = $(event.currentTarget);
              var rowElement = $(event.currentTarget).parents('tr');
              var id = checkboxElement.attr('id');
              var isComplete = checkboxElement.is(':checked');
   
              // Toggle table row color
              if (isComplete) {
                rowElement.addClass("active");
                rowElement.removeClass("warning");
              } else {
                rowElement.removeClass("active");
                rowElement.addClass("warning");
              }
   
              // Update hidden inputs for update panel.
              todoApp.ui_updateForm().children("input[name='" + id + "']").remove();
   
              todoApp.ui_updateForm().append($("<input>")
                .attr("type", "hidden")
                .attr("class", "updateComplete")
                .attr("name", id)
                .attr("value", isComplete));
   
            });
          },
   
          /*
           * UI Elements
           */
          ui_createNameInput: function() {
            return $(".todoForm #inputItemName");
          },
   
          ui_createCategoryInput: function() {
            return $(".todoForm #inputItemCategory");
          },
   
          ui_createButton: function() {
            return $(".todoForm button");
          },
   
          ui_table: function() {
            return $(".todoList table tbody");
          },
   
          ui_updateButton: function() {
            return $(".todoUpdatePanel button");
          },
   
          ui_updateForm: function() {
            return $(".todoUpdatePanel form");
          },
   
          ui_updateId: function() {
            return $(".todoUpdatePanel .updateComplete");
          },
   
          /*
           * Install hello TodoApp
           */
          install: function() {
            todoApp.bindCreateButton();
            todoApp.bindUpdateButton();
            todoApp.bindUpdateCheckboxes();
   
            todoApp.getTodoItems();
          }
        };
   
        $(document).ready(function() {
          todoApp.install();
        });
5. Incrível! Agora tudo o que resta é aplicativo de hello tootest. Execute o aplicativo hello localmente e adicione alguns itens de tarefas, preenchendo a categoria e o nome do item hello e clicando em **adicionar tarefa**.
6. Depois que o item de saudação aparece, você pode atualizar seja concluída, alternando a caixa de seleção hello e clicando em **atualizar tarefas**.

## <a id="Deploy"></a>Etapa 6: Implantar seu aplicativo de Java tooAzure Sites da Web
Sites do Azure tornam a implantação de aplicativos Java tão simples quanto a exportação de seu aplicativo como um arquivo WAR e por carregamento ou por meio do controle de origem (por exemplo, Git) ou FTP.

1. tooexport seu aplicativo como um arquivo WAR, com o botão direito no seu projeto no **Explorador de projeto**, clique em **exportar**e, em seguida, clique em **arquivo WAR**.
2. Em Olá **WAR exportar** janela, Olá a seguir:
   
   * Na caixa do projeto Web hello, insira documentdb do azure-exemplo java.
   * Na caixa de destino hello, escolha um arquivo WAR do destino toosave hello.
   * Clique em **Concluir**.
3. Agora que você tem um arquivo WAR lado, você pode simplesmente carregá-lo tooyour Site do Azure **webapps** directory. Para obter instruções sobre como carregar o arquivo hello, consulte [adicionar um aplicativo de Java tooAzure aplicativos de Web do serviço de aplicativo](../app-service-web/web-sites-java-add-app.md).
   
    Depois de saudação WAR arquivo carregado toohello webapps diretório, o ambiente de tempo de execução de saudação detectará que você adicionou a ele e automaticamente carregará.
4. tooview seu produto final, navegar toohttp://YOUR\_SITE\_NAME.azurewebsites.net/azure-java-sample/ e começar a adicionar tarefas!

## <a id="GetProject"></a>Obter o projeto de saudação do GitHub
Todos os exemplos de saudação neste tutorial são incluídos no hello [todo](https://github.com/Azure-Samples/documentdb-java-todo-app) projeto no GitHub. projeto de todo tooimport Olá no Eclipse, certifique-se de ter software hello e recursos listados em Olá [pré-requisitos](#Prerequisites) seção e, em seguida, Olá a seguir:

1. Instalar [Project Lombok](http://projectlombok.org/). Lombok é toogenerate usados construtores, getters, setters no projeto de saudação. Depois que você baixou o arquivo de lombok.jar hello, clique duas vezes nele tooinstall-lo ou instalá-lo na linha de comando hello.
2. Se o Eclipse estiver aberto, fechá-la e reiniciá-lo tooload Lombok.
3. No Eclipse, no hello **arquivo** menu, clique em **importação**.
4. Em Olá **importação** janela, clique em **Git**, clique em **projetos do Git**e, em seguida, clique em **próximo**.
5. Em Olá **Selecionar origem de repositório** tela, clique em **Clone URI**.
6. Em Olá **repositório Git de origem** tela hello **URI** caixa, digite https://github.com/Azure-Samples/java-todo-app.git e, em seguida, clique em **próximo**.
7. Em Olá **seleção ramificação** tela, verifique se **mestre** está selecionado e, em seguida, clique em **próximo**.
8. Em Olá **destino Local** tela, clique em **procurar** tooselect uma pasta onde Olá repositório pode ser copiada e, em seguida, clique em **próximo**.
9. Em Olá **selecione toouse um Assistente para importar projetos** tela, verifique se **importar projetos existentes** está selecionado e, em seguida, clique em **próximo**.
10. Em Olá **importar projetos** tela, desmarque Olá **DocumentDB** do projeto e, em seguida, clique em **concluir**. projeto de documentos Olá contém hello Azure Cosmos DB Java SDK, vamos adicionar como uma dependência em vez disso.
11. Em **Explorador de projeto**, navegue tooazure-documentdb-java-sample\src\com.microsoft.azure.documentdb.sample.dao\DocumentClientFactory.java e substitua os valores HOST e MASTER_KEY Olá Olá URI e a chave primária para sua conta do banco de dados do Azure Cosmos e salvar Olá arquivo. Para obter mais informações, consulte a [Etapa 1. Crie uma conta do banco de dados BD Cosmos do Azure](#CreateDB).
12. Em **Explorador de projeto**, Olá clique com botão direito **documentdb do azure-exemplo java**, clique em **caminho de compilação de**e, em seguida, clique em **configurar o caminho de compilação**.
13. Em Olá **caminho de compilação de Java** tela, no painel direito da saudação, selecione Olá **bibliotecas** guia e, em seguida, clique em **adicionar JARs externo**. Navegue toohello local do arquivo de lombok.jar hello e, em seguida, clique em **abrir**e, em seguida, clique em **Okey**.
14. Saudação do uso etapa 12 tooopen **propriedades** janela novamente e, no painel esquerdo do hello, clique em **tempos de execução de destino**.
15. Em Olá **tempos de execução de destino** tela, clique em **novo**, selecione **versão 7.0 do Apache Tomcat**e, em seguida, clique em **Okey**.
16. Saudação do uso etapa 12 tooopen **propriedades** janela novamente e, no painel esquerdo do hello, clique em **facetas de projeto**.
17. Em Olá **projeto facetas** tela, selecione **módulo Web dinâmico** e **Java**e, em seguida, clique em **Okey**.
18. Em Olá **servidores** guia na parte inferior da saudação da tela hello, clique no **Tomcat versão 7.0 do servidor no localhost** e, em seguida, clique em **adicionar e remover**.
19. Em Olá **adicionar e remover** janela, mover **documentdb do azure-exemplo java** toohello **configurado** caixa e, em seguida, clique em **concluir**.
20. Em Olá **servidores** guia, clique no **Tomcat versão 7.0 do servidor no localhost**e, em seguida, clique em **reiniciar**.
21. Em um navegador, navegue toohttp://localhost:8080 / azure-documentdb-exemplo de java / e comece a adicionar tooyour lista de tarefas. Observe que se você tiver alterado os valores de porta padrão, alterar 8080 toohello valor selecionado.
22. toodeploy tooan seu projeto site do Azure, consulte [etapa 6. Implantar seu aplicativo tooAzure Sites da Web](#Deploy).

[1]: media/documentdb-java-application/keys.png
