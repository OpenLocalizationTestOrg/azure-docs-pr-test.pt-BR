---
title: "programação JavaScript aaaServer para o banco de dados do Azure Cosmos | Microsoft Docs"
description: "Saiba como toowrite de banco de dados do Azure Cosmos toouse procedimentos armazenados, gatilhos de banco de dados e funções definidas pelo usuário (UDFs) em JavaScript. Obtenha dicas de programação de banco de dados e muito mais."
keywords: Gatilhos de banco de dados, procedimento armazenado, programa de banco de dados, sproc, banco de dados de documentos, azure, Microsoft azure
services: cosmos-db
documentationcenter: 
author: aliuy
manager: jhubbard
editor: mimig
ms.assetid: 0fba7ebd-a4fc-4253-a786-97f1354fbf17
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2016
ms.author: andrl
ms.openlocfilehash: 5a011d1c4b0b5908d5de73607a1bc328ed1711d0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-server-side-programming-stored-procedures-database-triggers-and-udfs"></a>Programação do lado do servidor do Azure Cosmos DB: procedimentos armazenados, gatilhos de banco de dados e UDFs
Saiba como a execução transacional e integrada de linguagem do JavaScript pelo Azure Cosmos DB permite que desenvolvedores escrevam **procedimentos armazenados**, **gatilhos** e **UDFs (funções definidas pelo usuário)** nativamente em um JavaScript [ECMAScript 2015](http://www.ecma-international.org/ecma-262/6.0/). Isso permite que você toowrite banco de dados programa lógica do aplicativo que pode ser enviada e executada diretamente em partições de armazenamento do banco de dados de saudação. 

É recomendável obter iniciado por Olá assistindo a seguir vídeo, onde Andrew Liu fornece tooCosmos uma breve introdução do banco de dados modelo de programação de banco de dados do servidor. 

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Azure-Demo-A-Quick-Intro-to-Azure-DocumentDBs-Server-Side-Javascript/player]
> 
> 

Em seguida, retorne toothis artigo, onde você aprenderá Olá respostas toohello perguntas a seguir:  

* Como eu escrevo um procedimento armazenado, gatilho ou UDF usando JavaScript?
* Como o Cosmos DB garante o ACID?
* Como funcionam as transações no Cosmos DB?
* O que são pré-gatilhos e pós-gatilhos e como eu escrevo um?
* Como eu registro e executo um procedimento armazenado, gatilho ou UDF de modo RESTful usando HTTP?
* Quais Cosmos DB SDKs são toocreate disponível e execute procedimentos armazenados, gatilhos e UDFs?

## <a name="introduction-toostored-procedure-and-udf-programming"></a>Introdução tooStored procedimento e programação de UDF
Essa abordagem de *"JavaScript como dia moderno T-SQL"* libera os desenvolvedores de aplicativos das complexidades Olá de incompatibilidade do tipo de sistema e as tecnologias de mapeamento relacional de objeto. Ele também tem uma série de vantagens intrínsecas que podem ser utilizadas toobuild excelentes aplicativos:  

* **Lógica de procedimento:** JavaScript como uma linguagem de programação de alto nível, fornece uma interface familiar e avançado tooexpress lógica de negócios. Você pode executar sequências complexas dos dados toohello mais próximos de operações.
* **Transações atômicas:** o Cosmos DB garante que as operações de banco de dados realizadas em um único procedimento armazenado ou gatilho são atômicas. Isso permite que um aplicativo combine operações relacionadas em um único lote para que todas ou nenhuma delas seja bem-sucedida. 
* **Desempenho:** documentos de fato Olá JSON é o sistema de tipo de linguagem de Javascript toohello intrinsecamente mapeadas e também é a unidade básica Olá de armazenamento no banco de dados do Cosmos permite um número de otimizações como lenta materialização de JSON no buffer de saudação pool e tornando-os disponível toohello sob demanda executando o código. Há mais benefícios de desempenho associados com o banco de dados toohello lógica de envio comercial:
  
  * Envio em lote – Os desenvolvedores podem agrupar operações como inserções e enviá-las em massa. custo de latência de tráfego de rede Hello e transações separadas do hello repositório toocreate sobrecarga são reduzidas significativamente. 
  * Pré-compilação – Cosmos DB pré-compila procedimentos armazenados, disparadores e definidos pelo usuário UDFs (funções) tooavoid custo de compilação de JavaScript para cada invocação. Olá, sobrecarga de compilação de código de bytes de saudação para lógica de procedimento Olá é amortizado tooa o valor mínimo.
  * Sequenciamento – Várias operações precisam de um efeito colateral (“gatilho”) que possivelmente envolve realizar uma ou mais operações de armazenamento secundárias. Além de atomicidade, isso é mais eficaz quando movidos toohello server. 
* **Encapsulamento:** procedimentos armazenados podem ser usados toogroup lógica de negócios em um local. Isso apresenta duas vantagens:
  * Ele adiciona uma camada de abstração sobre dados brutos hello, que permite que dados arquitetos tooevolve seus aplicativos independentemente do dados saudação. Isso é particularmente vantajoso quando Olá dados sem esquema, devido a toohello suposições frágil que talvez seja necessário toobe implantada na aplicativo hello se eles tiverem toodeal com dados diretamente.  
  * Essa abstração permite que as empresas proteger seus dados simplificando o acesso de saudação de scripts de saudação.  

Olá criação e execução de gatilhos de banco de dados, o procedimento armazenado e operadores de consulta personalizada é suportado por meio de saudação [API REST](/rest/api/documentdb/), [Studio do Azure DocumentDB](https://github.com/mingaliu/DocumentDBStudio/releases), e [cliente SDKs](documentdb-sdk-dotnet.md) em muitas plataformas, incluindo .NET, Node.js e JavaScript.

Este tutorial usa Olá [Node. js SDK com p promessas](http://azure.github.io/azure-documentdb-node-q/) tooillustrate sintaxe e uso de procedimentos armazenados, gatilhos e UDFs.   

## <a name="stored-procedures"></a>Procedimentos armazenados
### <a name="example-write-a-simple-stored-procedure"></a>Exemplo: escrever um procedimento armazenado simples
Vamos começar com um procedimento armazenado simples que retorna uma resposta “Hello World”.

    var helloWorldStoredProc = {
        id: "helloWorld",
        serverScript: function () {
            var context = getContext();
            var response = context.getResponse();

            response.setBody("Hello, World");
        }
    }


Os procedimentos armazenados são registrados por coleção e podem operar em qualquer documento e anexo presente na coleção. Olá trecho a seguir mostra como tooregister Olá helloWorld armazenado procedimento com uma coleção. 

    // register hello stored procedure
    var createdStoredProcedure;
    client.createStoredProcedureAsync('dbs/testdb/colls/testColl', helloWorldStoredProc)
        .then(function (response) {
            createdStoredProcedure = response.resource;
            console.log("Successfully created stored procedure");
        }, function (error) {
            console.log("Error", error);
        });


Depois que o procedimento armazenado de saudação for registrado, podemos executá-lo em coleção hello e ler Olá resultados no cliente de saudação. 

    // execute hello stored procedure
    client.executeStoredProcedureAsync('dbs/testdb/colls/testColl/sprocs/helloWorld')
        .then(function (response) {
            console.log(response.result); // "Hello, World"
        }, function (err) {
            console.log("Error", error);
        });


objeto de contexto Olá fornece acesso a operações de tooall que podem ser executadas no armazenamento de banco de dados do Cosmos, bem como acessarem objetos de solicitação e resposta toohello. Nesse caso, usamos o corpo da saudação Olá resposta objeto tooset de resposta de saudação enviada toohello back cliente. Para obter mais detalhes, consulte toohello [server Azure Cosmos DB JavaScript documentação do SDK](http://azure.github.io/azure-documentdb-js-server/).  

Vamos ampliar esse exemplo e adicionar mais funcionalidades relacionadas do banco de dados toohello procedimento de armazenado. Procedimentos armazenados podem criar, atualizar, ler, consultar e excluir documentos e anexos de coleção de saudação.    

### <a name="example-write-a-stored-procedure-toocreate-a-document"></a>Exemplo: Gravar um procedimento armazenado toocreate um documento
trecho Avançar Olá mostra como toouse Olá toointeract de objeto de contexto com recursos de banco de dados do Cosmos.

    var createDocumentStoredProc = {
        id: "createMyDocument",
        serverScript: function createMyDocument(documentToCreate) {
            var context = getContext();
            var collection = context.getCollection();

            var accepted = collection.createDocument(collection.getSelfLink(),
                  documentToCreate,
                  function (err, documentCreated) {
                      if (err) throw new Error('Error' + err.message);
                      context.getResponse().setBody(documentCreated.id)
                  });
            if (!accepted) return;
        }
    }


Esse procedimento armazenado usa como entrada documentToCreate, corpo de saudação de um toobe documento criado no conjunto atual de saudação. Todas essas operações são assíncronas e dependem de retornos de chamada de função do JavaScript. função de retorno de chamada Hello tem dois parâmetros, um objeto de erro Olá caso Olá operação falhar e outra para Olá criou o objeto. No retorno de chamada hello, os usuários podem lidar com exceção de saudação ou gerar um erro. No caso de um retorno de chamada não for fornecido e há um erro, o tempo de execução de banco de dados do Azure Cosmos hello gera um erro.   

No exemplo hello acima, o retorno de chamada hello gera um erro se a falha na operação de saudação. Caso contrário, ele define id de saudação do hello criada o documento como corpo de saudação do cliente de toohello de resposta de saudação. A seguir, mostramos como esse procedimento armazenado é executado com parâmetros de entrada.

    // register hello stored procedure
    client.createStoredProcedureAsync('dbs/testdb/colls/testColl', createDocumentStoredProc)
        .then(function (response) {
            var createdStoredProcedure = response.resource;

            // run stored procedure toocreate a document
            var docToCreate = {
                id: "DocFromSproc",
                book: "hello Hitchhiker’s Guide toohello Galaxy",
                author: "Douglas Adams"
            };

            return client.executeStoredProcedureAsync('dbs/testdb/colls/testColl/sprocs/createMyDocument',
                  docToCreate);
        }, function (error) {
            console.log("Error", error);
        })
    .then(function (response) {
        console.log(response); // "DocFromSproc"
    }, function (error) {
        console.log("Error", error);
    });


Observe que este procedimento armazenado pode ser modificado tootake uma matriz de corpos de documento como entrada e criá-los em Olá mesmo armazenado execução do procedimento em vez de rede de várias solicitações toocreate cada um deles individualmente. Isso pode ser usado tooimplement um importador em massa eficiente para o banco de dados do Cosmos (discutidas posteriormente neste tutorial).   

exemplo Hello descrito demonstrou como toouse de procedimentos armazenados. Abordaremos gatilhos e funções definidas pelo usuário (UDFs) mais tarde no tutorial de saudação.

## <a name="database-program-transactions"></a>Transações do programa de banco de dados
A transação em um banco de dados típico pode ser definida como uma sequência de operações realizadas como uma única unidade lógica de trabalho. Cada transação oferece **garantias ACID**. ACID é um acrônimo bastante conhecido que indica quatro propriedades: Atomicidade, Consistência, Isolamento e Durabilidade.  

Em resumo, a atomicidade garante que todo o trabalho Olá feito dentro de uma transação é tratado como uma única unidade onde o tudo é confirmada ou nenhum. Consistência assegura que Olá dados sempre estejam em bom estado interno em transações. Isolamento garante que nenhuma das duas transações interfere uns aos outros – em geral, os sistemas comerciais mais fornecem vários níveis de isolamento que podem ser usados com base nas necessidades do aplicativo hello. Durabilidade garante que qualquer alteração que está confirmada no banco de dados de saudação sempre estarão presente.   

No banco de dados do Cosmos, JavaScript é hospedado no hello mesmo espaço de memória como banco de dados de saudação. Portanto, solicitações feitas em procedimentos armazenados e gatilhos executar no hello mesmo escopo de uma sessão de banco de dados. Isso permite que tooguarantee Cosmos DB ACID para todas as operações que fazem parte de um único armazenado procedimento/disparador. Considere o seguinte Olá armazenados definição do procedimento:

    // JavaScript source code
    var exchangeItemsSproc = {
        id: "exchangeItems",
        serverScript: function (playerId1, playerId2) {
            var context = getContext();
            var collection = context.getCollection();
            var response = context.getResponse();

            var player1Document, player2Document;

            // query for players
            var filterQuery = 'SELECT * FROM Players p where p.id  = "' + playerId1 + '"';
            var accept = collection.queryDocuments(collection.getSelfLink(), filterQuery, {},
                function (err, documents, responseOptions) {
                    if (err) throw new Error("Error" + err.message);

                    if (documents.length != 1) throw "Unable toofind both names";
                    player1Document = documents[0];

                    var filterQuery2 = 'SELECT * FROM Players p where p.id = "' + playerId2 + '"';
                    var accept2 = collection.queryDocuments(collection.getSelfLink(), filterQuery2, {},
                        function (err2, documents2, responseOptions2) {
                            if (err2) throw new Error("Error" + err2.message);
                            if (documents2.length != 1) throw "Unable toofind both names";
                            player2Document = documents2[0];
                            swapItems(player1Document, player2Document);
                            return;
                        });
                    if (!accept2) throw "Unable tooread player details, abort ";
                });

            if (!accept) throw "Unable tooread player details, abort ";

            // swap hello two players’ items
            function swapItems(player1, player2) {
                var player1ItemSave = player1.item;
                player1.item = player2.item;
                player2.item = player1ItemSave;

                var accept = collection.replaceDocument(player1._self, player1,
                    function (err, docReplaced) {
                        if (err) throw "Unable tooupdate player 1, abort ";

                        var accept2 = collection.replaceDocument(player2._self, player2,
                            function (err2, docReplaced2) {
                                if (err) throw "Unable tooupdate player 2, abort"
                            });

                        if (!accept2) throw "Unable tooupdate player 2, abort";
                    });

                if (!accept) throw "Unable tooupdate player 1, abort";
            }
        }
    }

    // register hello stored procedure in Node.js client
    client.createStoredProcedureAsync(collection._self, exchangeItemsSproc)
        .then(function (response) {
            var createdStoredProcedure = response.resource;
        }
    );

Esse procedimento armazenado usa transações em itens jogos aplicativo tootrade entre os dois participantes em uma única operação. Olá armazenados procedimento tentativas tooread dois documentos que cada player de toohello IDs correspondentes passado como um argumento. Se ambos os documentos de player for encontrados, o procedimento de Olá armazenado atualiza documentos Olá trocando seus itens. Se houver erros ao longo de maneira hello, ele lança uma exceção de JavaScript que implicitamente anula a transação de saudação.

Se hello coleção Olá armazenado procedimento é registrado em relação é uma coleção de partição única, transação hello está no escopo tooall Olá documentos na coleção de saudação. Se a coleção Olá estiver particionada, procedimentos armazenados são executados no escopo de transação de saudação de uma chave de partição única. Cada armazenado execução do procedimento deve incluir um valor de chave de partição deve ser executados na transação de saudação do escopo toohello correspondente. Para obter mais detalhes, consulte [Particionamento do Azure Cosmos DB](partition-data.md).

### <a name="commit-and-rollback"></a>Confirmação e reversão
As transações são profunda e nativamente integradas ao modelo de programação do JavaScript do Cosmos DB. Dentro de uma função de JavaScript, todas as operações são automaticamente encapsuladas em uma única transação. Se hello JavaScript é concluído sem qualquer exceção, o banco de dados do toohello Olá operações serão confirmadas. Na verdade, instruções de "BEGIN TRANSACTION" e "COMMIT TRANSACTION" hello em bancos de dados relacionais são implícitas no banco de dados do Cosmos.  

Se houver qualquer exceção que é propagada de script hello, tempo de execução de JavaScript do Cosmos DB reverterá toda a transação hello. Conforme mostrado no hello anteriormente exemplo, gerar uma exceção é efetivamente equivalente tooa "ROLLBACK TRANSACTION" no banco de dados do Cosmos.

### <a name="data-consistency"></a>Consistência de dados
Procedimentos armazenados e gatilhos são sempre executados na réplica primária de saudação do contêiner de banco de dados do Azure Cosmos hello. Isso assegura que as leituras de dentro de procedimentos armazenados ofereçam uma forte consistência. Consultas que usam funções definidas pelo usuário podem ser executadas no hello primário ou de qualquer réplica secundária, mas podemos garantir toomeet Olá solicitado nível de consistência escolhendo réplica apropriado hello.

## <a name="bounded-execution"></a>Execução vinculada
Todas as operações de banco de dados do Cosmos devem ser concluído no servidor de saudação especificado duração de tempo limite da solicitação. Essa restrição também se aplica a funções tooJavaScript (procedimentos armazenados, gatilhos e funções definidas pelo usuário). Se uma operação não for concluída com limite de tempo, as transações de saudação é revertida. Funções JavaScript devem ser concluída dentro do limite de tempo de saudação ou implementar uma execução de toobatch/retomar continuação com base em modelo.  

No desenvolvimento de toosimplify ordem armazenado procedimentos e gatilhos toohandle limites de tempo, todas as funções no objeto de coleção de saudação (para criar, ler, substituir e exclusão de documentos e anexos) retornam um valor booleano que representa se que a operação será concluída. Se esse valor for false, é uma indicação de que limite de tempo de saudação é sobre tooexpire e procedimento Olá deve encapsular a execução.  Operações em fila toohello anterior primeira operação de repositório inaceitável têm a garantia toocomplete se o procedimento de Olá armazenado é concluída no tempo e não enfileirar mais solicitações.  

Funções de JavaScript também são vinculadas quanto ao consumo de recursos. Cosmos DB reserva a taxa de transferência por coleção com base no tamanho de saudação provisionado de uma conta de banco de dados. A produtividade é expressa em termos de uma unidade normalizada de consumo de CPU, memória e E/S chamada unidade de solicitação ou RU. Funções JavaScript podem potencialmente usar um número grande de RUs dentro de um curto período de tempo e podem obter a taxa limitada se limite da coleção Olá for atingido. Procedimentos armazenados uso intensivo de recursos também podem estar em quarentena tooensure disponibilidade das operações de banco de dados primitivo.  

### <a name="example-bulk-importing-data-into-a-database-program"></a>Exemplo: importação de dados em massa em um programa de banco de dados
Abaixo está um exemplo de um procedimento armazenado que é gravado toobulk importar documentos em uma coleção. Observe como Olá armazenadas a execução do procedimento identificadores limitados verificando Olá booliano retornar o valor de createDocument e, em seguida, usa Olá contagem de documentos inseridos em cada invocação Olá armazenado procedimento tootrack e retomar o progresso em lotes.

    function bulkImport(docs) {
        var collection = getContext().getCollection();
        var collectionLink = collection.getSelfLink();

        // hello count of imported docs, also used as current doc index.
        var count = 0;

        // Validate input.
        if (!docs) throw new Error("hello array is undefined or null.");

        var docsLength = docs.length;
        if (docsLength == 0) {
            getContext().getResponse().setBody(0);
        }

        // Call hello create API toocreate a document.
        tryCreate(docs[count], callback);

        // Note that there are 2 exit conditions:
        // 1) hello createDocument request was not accepted. 
        //    In this case hello callback will not be called, we just call setBody and we are done.
        // 2) hello callback was called docs.length times.
        //    In this case all documents were created and we don’t need toocall tryCreate anymore. Just call setBody and we are done.
        function tryCreate(doc, callback) {
            var isAccepted = collection.createDocument(collectionLink, doc, callback);

            // If hello request was accepted, callback will be called.
            // Otherwise report current count back toohello client, 
            // which will call hello script again with remaining set of docs.
            if (!isAccepted) getContext().getResponse().setBody(count);
        }

        // This is called when collection.createDocument is done in order tooprocess hello result.
        function callback(err, doc, options) {
            if (err) throw err;

            // One more document has been inserted, increment hello count.
            count++;

            if (count >= docsLength) {
                // If we created all documents, we are done. Just set hello response.
                getContext().getResponse().setBody(count);
            } else {
                // Create next document.
                tryCreate(docs[count], callback);
            }
        }
    }

## <a id="trigger"></a> Gatilhos de banco de dados
### <a name="database-pre-triggers"></a>Pré-gatilhos de banco de dados
O Cosmos DB oferece gatilhos que são executados ou disparados por uma operação em um documento. Por exemplo, você pode especificar um pré-gatilho de quando você estiver criando um documento – esse pré-gatilho será executado antes que o documento hello é criado. a seguir Olá é um exemplo de como pré-gatilhos podem ser usado toovalidate Olá propriedades de um documento que está sendo criado:

    var validateDocumentContentsTrigger = {
        id: "validateDocumentContents",
        serverScript: function validate() {
            var context = getContext();
            var request = context.getRequest();

            // document toobe created in hello current operation
            var documentToCreate = request.getBody();

            // validate properties
            if (!("timestamp" in documentToCreate)) {
                var ts = new Date();
                documentToCreate["my timestamp"] = ts.getTime();
            }

            // update hello document that will be created
            request.setBody(documentToCreate);
        },
        triggerType: TriggerType.Pre,
        triggerOperation: TriggerOperation.Create
    }


E Olá código de registro de cliente Node. js correspondente para o disparador hello:

    // register pre-trigger
    client.createTriggerAsync(collection.self, validateDocumentContentsTrigger)
        .then(function (response) {
            console.log("Created", response.resource);
            var docToCreate = {
                id: "DocWithTrigger",
                event: "Error",
                source: "Network outage"
            };

            // run trigger while creating above document 
            var options = { preTriggerInclude: "validateDocumentContents" };

            return client.createDocumentAsync(collection.self,
                  docToCreate, options);
        }, function (error) {
            console.log("Error", error);
        })
    .then(function (response) {
        console.log(response.resource); // document with timestamp property added
    }, function (error) {
        console.log("Error", error);
    });


Pré-gatilhos não podem ter parâmetros de entrada. o objeto de solicitação Olá pode ser usado toomanipulate mensagem de solicitação de Olá associada à operação de saudação. Aqui, pré-gatilho hello está sendo executado com a criação de um documento hello e corpo de mensagem de solicitação de saudação contém Olá documento toobe criado no formato JSON.   

Quando os gatilhos são registrados, os usuários podem especificar operações Olá que podem ser executados com. Esse gatilho foi criado com TriggerOperation.Create, o que significa o seguinte Olá não é permitido.

    var options = { preTriggerInclude: "validateDocumentContents" };

    client.replaceDocumentAsync(docToReplace.self,
                  newDocBody, options)
    .then(function (response) {
        console.log(response.resource);
    }, function (error) {
        console.log("Error", error);
    });

    // Fails, can’t use a create trigger in a replace operation

### <a name="database-post-triggers"></a>Pós-gatilhos de banco de dados
Pós-gatilhos, assim como pré-gatilhos, são associados a uma operação em um documento e não assumem parâmetros de entrada. Eles são executados **depois** Olá operação foi concluída e ter acesso toohello resposta mensagem enviada toohello cliente.   

saudação de exemplo a seguir mostra pós-gatilhos em ação:

    var updateMetadataTrigger = {
        id: "updateMetadata",
        serverScript: function updateMetadata() {
            var context = getContext();
            var collection = context.getCollection();
            var response = context.getResponse();

            // document that was created
            var createdDocument = response.getBody();

            // query for metadata document
            var filterQuery = 'SELECT * FROM root r WHERE r.id = "_metadata"';
            var accept = collection.queryDocuments(collection.getSelfLink(), filterQuery,
                updateMetadataCallback);
            if(!accept) throw "Unable tooupdate metadata, abort";

            function updateMetadataCallback(err, documents, responseOptions) {
                if(err) throw new Error("Error" + err.message);
                         if(documents.length != 1) throw 'Unable toofind metadata document';

                         var metadataDocument = documents[0];

                         // update metadata
                         metadataDocument.createdDocuments += 1;
                         metadataDocument.createdNames += " " + createdDocument.id;
                         var accept = collection.replaceDocument(metadataDocument._self,
                               metadataDocument, function(err, docReplaced) {
                                      if(err) throw "Unable tooupdate metadata, abort";
                               });
                         if(!accept) throw "Unable tooupdate metadata, abort";
                         return;                    
            }                                                                                            
        },
        triggerType: TriggerType.Post,
        triggerOperation: TriggerOperation.All
    }


gatilho Olá pode ser registrado como mostrado na saudação de exemplo a seguir.

    // register post-trigger
    client.createTriggerAsync('dbs/testdb/colls/testColl', updateMetadataTrigger)
        .then(function(createdTrigger) { 
            var docToCreate = { 
                name: "artist_profile_1023",
                artist: "hello Band",
                albums: ["Hellujah", "Rotators", "Spinning Top"]
            };

            // run trigger while creating above document 
            var options = { postTriggerInclude: "updateMetadata" };

            return client.createDocumentAsync(collection.self,
                  docToCreate, options);
        }, function(error) {
            console.log("Error" , error);
        })
    .then(function(response) {
        console.log(response.resource); 
    }, function(error) {
        console.log("Error" , error);
    });


Esse gatilho consultas para o documento de metadados hello e atualiza com detalhes sobre documento hello recém-criado.  

Uma coisa importante toonote é hello **transacional** execução de gatilhos no banco de dados do Cosmos. Esse pós-gatilho executado como parte da saudação mesma transação como a criação de saudação do documento original hello. Portanto, se podemos lançar uma exceção de pós-gatilho de Olá (digamos se estamos documento de metadados não é possível tooupdate Olá), toda a transação Olá falhará e ser revertida. Nenhum documento será criado e uma exceção será retornada.  

## <a id="udf"></a>Funções definidas pelo usuário
Funções definidas pelo usuário (UDFs) são gramática da linguagem de consulta SQL do DocumentDB API tooextend usado hello e implementam a lógica de negócios personalizada. Elas podem ser invocadas somente de dentro das consultas. Eles não possuem o objeto de contexto de toohello de acesso e destinam-se toobe usado como o JavaScript somente computação. Portanto, UDFs podem ser executadas em réplicas secundárias de saudação serviço de banco de dados do Cosmos.  

Hello exemplo a seguir cria um imposto de renda UDF toocalculate com base em taxas de vários colchetes de renda e, em seguida, usa-lo dentro de uma consulta toofind todas as pessoas que paga mais de US $20.000 impostos.

    var taxUdf = {
        id: "tax",
        serverScript: function tax(income) {

            if(income == undefined) 
                throw 'no input';

            if (income < 1000) 
                return income * 0.1;
            else if (income < 10000) 
                return income * 0.2;
            else
                return income * 0.4;
        }
    }


Olá UDF subsequentemente pode ser usado em consultas como Olá exemplo a seguir:

    // register UDF
    client.createUserDefinedFunctionAsync('dbs/testdb/colls/testColl', taxUdf)
        .then(function(response) { 
            console.log("Created", response.resource);

            var query = 'SELECT * FROM TaxPayers t WHERE udf.tax(t.income) > 20000'; 
            return client.queryDocuments('dbs/testdb/colls/testColl',
                   query).toArrayAsync();
        }, function(error) {
            console.log("Error" , error);
        })
    .then(function(response) {
        var documents = response.feed;
        console.log(response.resource); 
    }, function(error) {
        console.log("Error" , error);
    });

## <a name="javascript-language-integrated-query-api"></a>API de consulta integrada da linguagem JavaScript
Além disso tooissuing consultas usando a gramática SQL do DocumentDB, hello SDK do lado do servidor permitem que você tooperform otimizada de consultas usando uma interface JavaScript fluente sem qualquer conhecimento de SQL. consulta de JavaScript Olá que API permite consultas de compilação tooprogrammatically passando funções de predicado em função encadeável chama com do tooECMAScript5 familiar uma sintaxe internos de matriz e bibliotecas JavaScript populares como lodash. Consultas são analisadas pelo Olá toobe de tempo de execução de JavaScript executado com eficiência usando índices do Azure Cosmos DB.

> [!NOTE]
> `__`(sublinhado duplo) é um alias muito`getContext().getCollection()`.
> <br/>
> Em outras palavras, você pode usar `__` ou `getContext().getCollection()` tooaccess Olá API de consulta do JavaScript.
> 
> 

As funções permitidas incluem:

<ul>
<li>
<b>chain() ... .value([callback] [, opções])</b>
<ul>
<li>
Inicia uma chamada encadeada que deve ser terminada com value().
</li>
</ul>
</li>
<li>
<b>filter(predicateFunction [, opções] [, callback])</b>
<ul>
<li>
Filtra hello usando uma função de predicado que retorna true/false na ordem toofilter in/out de documentos de entrada no conjunto resultante da saudação de entrada. Isso se comporta semelhante tooa cláusula WHERE no SQL.
</li>
</ul>
</li>
<li>
<b>map(transformationFunction [, opções] [, callback])</b>
<ul>
<li>
Aplica uma projeção recebe uma função de transformação que mapeia cada valor ou objeto do item de entrada tooa JavaScript. Isso se comporta semelhante cláusula SELECT de tooa em SQL.
</li>
</ul>
</li>
<li>
<b>pluck([propertyName] [, opções] [, callback])</b>
<ul>
<li>
Esse é um atalho para um mapa que extrai o valor de saudação de uma única propriedade de cada item de entrada.
</li>
</ul>
</li>
<li>
<b>flatten([isShallow] [, opções] [, callback])</b>
<ul>
<li>
Combina e mescla as matrizes de cada item na matriz de tooa única de entrada. Isso se comporta semelhante tooSelectMany em LINQ.
</li>
</ul>
</li>
<li>
<b>sortBy([predicate] [, opções] [, callback])</b>
<ul>
<li>
Gerar um novo conjunto de documentos classificando documentos Olá no fluxo de documento de entrada hello em ordem crescente utilizando Olá fornecido predicado. Isso se comporta semelhante tooa cláusula ORDER BY em SQL.
</li>
</ul>
</li>
<li>
<b>sortByDescending([predicate] [, opções] [, callback])</b>
<ul>
<li>
Gerar um novo conjunto de documentos classificando documentos Olá no fluxo de documento de entrada hello em ordem decrescente usando Olá fornecido predicado. Isso se comporta semelhante cláusula de ORDER BY x DESC tooa no SQL.
</li>
</ul>
</li>
</ul>


Quando incluído dentro de funções de predicado e/ou seletor, hello seguintes construções de JavaScript obtém automaticamente otimizada toorun diretamente no banco de dados do Azure Cosmos índices:

* Operadores simples: = + - * / % | ^ &amp; == != === !=== &lt; &gt; &lt;= &gt;= || &amp;&amp; &lt;&lt; &gt;&gt; &gt;&gt;&gt;! ~
* Literais, incluindo o literal de objeto Olá: {}
* var, return

Olá JavaScript seguinte construções não obter otimizado para índices de banco de dados do Azure Cosmos:

* Fluxo de controle (por exemplo,. if, for, while)
* Chamadas de função

Para saber mais, consulte nossos [JSDocs no servidor](http://azure.github.io/azure-documentdb-js-server/).

### <a name="example-write-a-stored-procedure-using-hello-javascript-query-api"></a>Exemplo: Gravar um procedimento armazenado usando a API de consulta Olá JavaScript
saudação de exemplo de código a seguir é um exemplo de como Olá JavaScript consulta API pode ser usada no contexto de saudação de um procedimento armazenado. Olá procedimento armazenado insere um documento, fornecido por um parâmetro de entrada e atualiza um documento de metadados usando Olá `__.filter()` método com minSize, maxSize e totalSize com base na propriedade de tamanho do documento hello entrada.

    /**
     * Insert actual doc and update metadata doc: minSize, maxSize, totalSize based on doc.size.
     */
    function insertDocumentAndUpdateMetadata(doc) {
      // HTTP error codes sent tooour callback funciton by DocDB server.
      var ErrorCode = {
        RETRY_WITH: 449,
      }

      var isAccepted = __.createDocument(__.getSelfLink(), doc, {}, function(err, doc, options) {
        if (err) throw err;

        // Check hello doc (ignore docs with invalid/zero size and metaDoc itself) and call updateMetadata.
        if (!doc.isMetadata && doc.size > 0) {
          // Get hello meta document. We keep it in hello same collection. it's hello only doc that has .isMetadata = true.
          var result = __.filter(function(x) {
            return x.isMetadata === true
          }, function(err, feed, options) {
            if (err) throw err;

            // We assume that metadata doc was pre-created and must exist when this script is called.
            if (!feed || !feed.length) throw new Error("Failed toofind hello metadata document.");

            // hello metadata document.
            var metaDoc = feed[0];

            // Update metaDoc.minSize:
            // for 1st document use doc.Size, for all hello rest see if it's less than last min.
            if (metaDoc.minSize == 0) metaDoc.minSize = doc.size;
            else metaDoc.minSize = Math.min(metaDoc.minSize, doc.size);

            // Update metaDoc.maxSize.
            metaDoc.maxSize = Math.max(metaDoc.maxSize, doc.size);

            // Update metaDoc.totalSize.
            metaDoc.totalSize += doc.size;

            // Update/replace hello metadata document in hello store.
            var isAccepted = __.replaceDocument(metaDoc._self, metaDoc, function(err) {
              if (err) throw err;
              // Note: in case concurrent updates causes conflict with ErrorCode.RETRY_WITH, we can't read hello meta again 
              //       and update again because due tooSnapshot isolation we will read same exact version (we are in same transaction).
              //       We have tootake care of that on hello client side.
            });
            if (!isAccepted) throw new Error("replaceDocument(metaDoc) returned false.");
          });
          if (!result.isAccepted) throw new Error("filter for metaDoc returned false.");
        }
      });
      if (!isAccepted) throw new Error("createDocument(actual doc) returned false.");
    }

## <a name="sql-toojavascript-cheat-sheet"></a>Roteiro de tooJavascript SQL
Olá tabela a seguir apresenta várias consultas SQL e consultas de JavaScript correspondentes hello.

Assim como acontece com consultas SQL, as chaves de propriedade do documento (por exemplo, `doc.id`) diferenciam maiúsculas de minúsculas.

|SQL| API de consulta do JavaScript|Descrição abaixo|
|---|---|---|
|SELECIONAR *<br>FROM docs| __.map(function(doc) { <br>&nbsp;&nbsp;&nbsp;&nbsp;return doc;<br>});|1|
|SELECT docs.id, docs.message AS msg, docs.actions <br>FROM docs|__.map(function(doc) {<br>&nbsp;&nbsp;&nbsp;&nbsp;return {<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;id: doc.id,<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;msg: doc.message,<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;actions:doc.actions<br>&nbsp;&nbsp;&nbsp;&nbsp;};<br>});|2|
|SELECIONAR *<br>FROM docs<br>WHERE docs.id="X998_Y998"|__.filter(function(doc) {<br>&nbsp;&nbsp;&nbsp;&nbsp;return doc.id ==="X998_Y998";<br>});|3|
|SELECIONAR *<br>FROM docs<br>WHERE ARRAY_CONTAINS(docs.Tags, 123)|__.filter(function(x) {<br>&nbsp;&nbsp;&nbsp;&nbsp;return x.Tags && x.Tags.indexOf(123) > -1;<br>});|4|
|SELECT docs.id, docs.message AS msg<br>FROM docs<br>WHERE docs.id="X998_Y998"|__.chain()<br>&nbsp;&nbsp;&nbsp;&nbsp;.filter(function(doc) {<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;return doc.id ==="X998_Y998";<br>&nbsp;&nbsp;&nbsp;&nbsp;})<br>&nbsp;&nbsp;&nbsp;&nbsp;.map(function(doc) {<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;return {<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;id: doc.id,<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;msg: doc.message<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;};<br>&nbsp;&nbsp;&nbsp;&nbsp;})<br>.value();|5|
|SELECT VALUE tag<br>FROM docs<br>JOIN tag IN docs.Tags<br>ORDER BY docs._ts|__.chain()<br>&nbsp;&nbsp;&nbsp;&nbsp;.filter(function(doc) {<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;return doc.Tags && Array.isArray(doc.Tags);<br>&nbsp;&nbsp;&nbsp;&nbsp;})<br>&nbsp;&nbsp;&nbsp;&nbsp;.sortBy(function(doc) {<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;return doc._ts;<br>&nbsp;&nbsp;&nbsp;&nbsp;})<br>&nbsp;&nbsp;&nbsp;&nbsp;.pluck("Tags")<br>&nbsp;&nbsp;&nbsp;&nbsp;.flatten()<br>&nbsp;&nbsp;&nbsp;&nbsp;.value()|6|

Olá, descrições a seguir explicam cada consulta na tabela de saudação acima.
1. Resulta em todos os documentos (paginados com token de continuação) no estado em que se encontram.
2. Projetos Olá id, a mensagem (alias toomsg) e a ação de todos os documentos.
3. Consultas em documentos com predicado de saudação: id = "X998_Y998".
4. Consultas para documentos que têm uma propriedade de marcas e marcas é uma matriz que contém o valor de saudação 123.
5. Consultas em documentos com um predicado, id = "X998_Y998" e, em seguida, id de saudação de projetos e (alias toomsg) da mensagem.
6. Filtros para documentos que têm uma propriedade de matriz, marcas, e classifica documentos resultantes Olá pela propriedade de sistema de carimbo de hora de TS Olá e, em seguida, projetos + mescla a matriz de marcas de saudação.


## <a name="runtime-support"></a>Suporte de tempo de execução
[API de servidor JavaScript do DocumentDB](http://azure.github.io/azure-documentdb-js-server/) fornece suporte para Olá a maioria das Olá principais recursos de linguagem JavaScript como padronizado pelo [ECMA-262](http://www.ecma-international.org/publications/standards/Ecma-262.htm).

### <a name="security"></a>Segurança
JavaScript de procedimentos armazenados e gatilhos são em modo seguro para que os efeitos de saudação de um script não apresentam vazamento toohello outros sem passar pelo isolamento de transação de instantâneo Olá no nível de banco de dados de saudação. ambientes de tempo de execução de saudação são reunidos mas limpo do contexto de saudação após cada execução. Portanto, eles não têm garantia toobe seguro de efeitos colaterais não intencionais uns dos outros.

### <a name="pre-compilation"></a>Pré-compilação
Procedimentos armazenados, gatilhos e UDFs são implicitamente pré-compilado toohello formato de código de bytes no custo da compilação ordem tooavoid na hora Olá cada invocação do script. Isso assegura que as invocações dos procedimentos armazenados sejam rápidas e possuam baixa pegada.

## <a name="client-sdk-support"></a>Suporte de SDK de cliente
Em adição toohello API DocumentDB para [Node.js](documentdb-sdk-node.md) tem de cliente, o banco de dados do Azure Cosmos [.NET](documentdb-sdk-dotnet.md), [.NET Core](documentdb-sdk-dotnet-core.md), [Java](documentdb-sdk-java.md), [ JavaScript](http://azure.github.io/azure-documentdb-js/), e [Python SDKs](documentdb-sdk-python.md) para Olá API DocumentDB. Os procedimentos armazenados, gatilhos e UDFs também podem ser criados e executados usando qualquer um desses SDKs. Olá mostrado no exemplo a seguir como toocreate e executar um procedimento armazenado usando o cliente do .NET hello. Observe como tipos de .NET Olá são passados em Olá procedimento armazenado como JSON e leia novamente.

    var markAntiquesSproc = new StoredProcedure
    {
        Id = "ValidateDocumentAge",
        Body = @"
                function(docToCreate, antiqueYear) {
                    var collection = getContext().getCollection();    
                    var response = getContext().getResponse();    

                    if(docToCreate.Year != undefined && docToCreate.Year < antiqueYear){
                        docToCreate.antique = true;
                    }

                    collection.createDocument(collection.getSelfLink(), docToCreate, {}, 
                        function(err, docCreated, options) { 
                            if(err) throw new Error('Error while creating document: ' + err.message);                              
                            if(options.maxCollectionSizeInMb == 0) throw 'max collection size not found'; 
                            response.setBody(docCreated);
                    });
             }"
    };

    // register stored procedure
    StoredProcedure createdStoredProcedure = await client.CreateStoredProcedureAsync(UriFactory.CreateDocumentCollectionUri("db", "coll"), markAntiquesSproc);
    dynamic document = new Document() { Id = "Borges_112" };
    document.Title = "Aleph";
    document.Year = 1949;

    // execute stored procedure
    Document createdDocument = await client.ExecuteStoredProcedureAsync<Document>(UriFactory.CreateStoredProcedureUri("db", "coll", "sproc"), document, 1920);


Este exemplo mostra como Olá toouse [API .NET do DocumentDB](/dotnet/api/overview/azure/cosmosdb?view=azure-dotnet) toocreate um gatilho de pré-lançamento e criar um documento com hello gatilho habilitado. 

    Trigger preTrigger = new Trigger()
    {
        Id = "CapitalizeName",
        Body = @"function() {
            var item = getContext().getRequest().getBody();
            item.id = item.id.toUpperCase();
            getContext().getRequest().setBody(item);
        }",
        TriggerOperation = TriggerOperation.Create,
        TriggerType = TriggerType.Pre
    };

    Document createdItem = await client.CreateDocumentAsync(UriFactory.CreateDocumentCollectionUri("db", "coll"), new Document { Id = "documentdb" },
        new RequestOptions
        {
            PreTriggerInclude = new List<string> { "CapitalizeName" },
        });


E hello exemplo a seguir mostra como toocreate um usuário definido UDF (função) e usá-lo em uma [consulta SQL do DocumentDB API](documentdb-sql-query.md).

    UserDefinedFunction function = new UserDefinedFunction()
    {
        Id = "LOWER",
        Body = @"function(input) 
        {
            return input.toLowerCase();
        }"
    };

    foreach (Book book in client.CreateDocumentQuery(UriFactory.CreateDocumentCollectionUri("db", "coll"),
        "SELECT * FROM Books b WHERE udf.LOWER(b.Title) = 'war and peace'"))
    {
        Console.WriteLine("Read {0} from query", book);
    }

## <a name="rest-api"></a>API REST
Todas as operações do Azure Cosmos DB podem ser realizadas de maneira RESTful. Procedimentos armazenados, gatilhos e funções definidas pelo usuário podem ser registrados em uma coleção usando HTTP POST. Olá, a seguir está um exemplo de como tooregister um procedimento armazenado:

    POST https://<url>/sprocs/ HTTP/1.1
    authorization: <<auth>>
    x-ms-date: Thu, 07 Aug 2014 03:43:10 GMT


    var x = {
      "name": "createAndAddProperty",
      "body": function (docToCreate, addedPropertyName, addedPropertyValue) {
                var collectionManager = getContext().getCollection();
                collectionManager.createDocument(
                    collectionManager.getSelfLink(),
                    docToCreate,
                    function(err, docCreated) {
                      if(err) throw new Error('Error:  ' + err.message);
                      docCreated[addedPropertyName] = addedPropertyValue;
                      getContext().getResponse().setBody(docCreated);
                    });
            }
    }


Olá procedimento armazenado está registrado executando uma solicitação POST em relação a saudação URI bancos de dados/testdb/colls/testColl/sprocs Olá corpo contendo Olá toocreate do procedimento armazenado. Disparadores e UDFs podem ser registrados da mesma forma, emitindo um POST para /triggers e /udfs respectivamente.
Este procedimento armazenado pode, então, ser executado emitindo uma solicitação POST ao link de recursos:

    POST https://<url>/sprocs/<sproc> HTTP/1.1
    authorization: <<auth>>
    x-ms-date: Thu, 07 Aug 2014 03:43:20 GMT


    [ { "name": "TestDocument", "book": "Autumn of hello Patriarch"}, "Price", 200 ]


Aqui, o procedimento de entrada toohello armazenado Olá é passado no corpo de solicitação de hello. Observe que a entrada hello é passada como uma matriz JSON dos parâmetros de entrada. Olá armazenados procedimento leva Olá primeira entrada como um documento que é um corpo de resposta. resposta de saudação que recebemos é a seguinte:

    HTTP/1.1 200 OK

    { 
      name: 'TestDocument',
      book: ‘Autumn of hello Patriarch’,
      id: ‘V7tQANV3rAkDAAAAAAAAAA==‘,
      ts: 1407830727,
      self: ‘dbs/V7tQAA==/colls/V7tQANV3rAk=/docs/V7tQANV3rAkDAAAAAAAAAA==/’,
      etag: ‘6c006596-0000-0000-0000-53e9cac70000’,
      attachments: ‘attachments/’,
      Price: 200
    }


Gatilhos, diferentemente dos procedimentos armazenados, não podem ser executados diretamente. Ao invés disso, eles são executados como parte de uma operação em um documento. Podemos especificar Olá gatilhos toorun com uma solicitação usando cabeçalhos HTTP. a seguir Olá é solicitação toocreate um documento.

    POST https://<url>/docs/ HTTP/1.1
    authorization: <<auth>>
    x-ms-date: Thu, 07 Aug 2014 03:43:10 GMT
    x-ms-documentdb-pre-trigger-include: validateDocumentContents 
    x-ms-documentdb-post-trigger-include: bookCreationPostTrigger


    {
       "name": "newDocument",
       “title”: “hello Wizard of Oz”,
       “author”: “Frank Baum”,
       “pages”: 92
    }


Aqui Olá pré-gatilho toobe executar com a solicitação de saudação especificado no cabeçalho x-ms-documentdb-pre-trigger-include hello. De maneira correspondente, os pós-disparadores de recebem no cabeçalho x-ms-documentdb-post-trigger-include Olá. Observe que pré e pós-gatilhos podem ser especificados para uma determinada solicitação.

## <a name="sample-code"></a>Exemplo de código
Você pode encontrar mais exemplos de código do lado do servidor (incluindo [bulk-delete](https://github.com/Azure/azure-documentdb-js-server/tree/master/samples/stored-procedures/bulkDelete.js) e [update](https://github.com/Azure/azure-documentdb-js-server/tree/master/samples/stored-procedures/update.js)) em nosso [repositório GitHub](https://github.com/Azure/azure-documentdb-js-server/tree/master/samples).

Deseja tooshare o incrível procedimento armazenado? Por favor, envie uma solicitação pull! 

## <a name="next-steps"></a>Próximas etapas
Uma vez que um ou mais procedimentos armazenados, gatilhos e funções definidas pelo usuário criadas, você pode carregá-los e exibi-los no hello portal do Azure usando o Gerenciador de dados.

Você também pode encontrar o seguinte Olá referências e recursos úteis no seu toolearn de caminho mais sobre a programação do Azure Cosmos banco de dados do servidor:

* [SDKs do Azure Cosmos DB](documentdb-sdk-dotnet.md)
* [Estudo do DocumentDB](https://github.com/mingaliu/DocumentDBStudio/releases)
* [JSON](http://www.json.org/) 
* [JavaScript ECMA-262](http://www.ecma-international.org/publications/standards/Ecma-262.htm)
* [Extensibilidade de banco de dados seguro e portátil](http://dl.acm.org/citation.cfm?id=276339) 
* [Arquitetura de banco de dados orientada a serviços](http://dl.acm.org/citation.cfm?id=1066267&coll=Portal&dl=GUIDE) 
* [Olá hospedagem .NET Runtime no Microsoft SQL server](http://dl.acm.org/citation.cfm?id=1007669)

