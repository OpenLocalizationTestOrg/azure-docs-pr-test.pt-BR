---
title: aaaHow toouse armazenamento de tabela do Azure do Node. js | Microsoft Docs
description: "Armazene dados estruturados em nuvem hello usando o armazenamento de tabela do Azure, um repositório de dados NoSQL."
services: storage
documentationcenter: nodejs
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: fc2e33d2-c5da-4861-8503-53fdc25750de
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 12/08/2016
ms.author: marsma
ms.openlocfilehash: 990a71337b806d759d0277a7691712346db7b355
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-table-storage-from-nodejs"></a>Como toouse armazenamento de tabela do Azure do Node. js
[!INCLUDE [storage-selector-table-include](../../includes/storage-selector-table-include.md)]
[!INCLUDE [storage-table-cosmos-db-langsoon-tip-include](../../includes/storage-table-cosmos-db-langsoon-tip-include.md)]

## <a name="overview"></a>Visão geral
Este tópico mostra como tooperform cenários comuns usando Olá tabela do Azure do serviço em um aplicativo Node. js.

exemplos de código Olá neste tópico pressupõem que você já tiver um aplicativo Node. js. Para obter informações sobre como toocreate um aplicativo Node.js no Azure, consulte qualquer um dos seguintes tópicos:

* [Criar um aplicativo Web do Node.js no Serviço de Aplicativo do Azure](../app-service-web/app-service-web-get-started-nodejs.md)
* [Criar e implantar um tooAzure de aplicativo web Node.js usando o WebMatrix](../app-service-web/web-sites-nodejs-use-webmatrix.md)
* [Criar e implantar um aplicativo de Node. js tooan serviço de nuvem do Azure](../cloud-services/cloud-services-nodejs-develop-deploy-app.md) (usando o Windows PowerShell)

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="configure-your-application-tooaccess-azure-storage"></a>Configurar seu aplicativo tooaccess armazenamento do Azure
toouse armazenamento do Azure, é necessário hello Azure Storage SDK para Node.js, que inclui um conjunto de bibliotecas de conveniência que se comunicam com serviços da REST do armazenamento hello.

### <a name="use-node-package-manager-npm-tooinstall-hello-package"></a>Usar o pacote de saudação do Gerenciador de pacote de nó (NPM) tooinstall
1. Use uma interface de linha de comando como **PowerShell** (Windows), **Terminal** (Mac), ou **Bash** (Unix) e navegue toohello pasta em que você criou seu aplicativo.
2. Tipo **npm instalar o armazenamento do azure** na janela de comando hello. A saída do comando de saudação é semelhante toohello exemplo a seguir.

       azure-storage@0.5.0 node_modules\azure-storage
       +-- extend@1.2.1
       +-- xmlbuilder@0.4.3
       +-- mime@1.2.11
       +-- node-uuid@1.4.3
       +-- validator@3.22.2
       +-- underscore@1.4.4
       +-- readable-stream@1.0.33 (string_decoder@0.10.31, isarray@0.0.1, inherits@2.0.1, core-util-is@1.0.1)
       +-- xml2js@0.2.7 (sax@0.5.2)
       +-- request@2.57.0 (caseless@0.10.0, aws-sign2@0.5.0, forever-agent@0.6.1, stringstream@0.0.4, oauth-sign@0.8.0, tunnel-agent@0.4.1, isstream@0.1.2, json-stringify-safe@5.0.1, bl@0.9.4, combined-stream@1.0.5, qs@3.1.0, mime-types@2.0.14, form-data@0.2.0, http-signature@0.11.0, tough-cookie@2.0.0, hawk@2.3.1, har-validator@1.8.0)
3. Você pode executar manualmente Olá **ls** tooverify de comando que um **nó\_módulos** pasta foi criada. Dentro dessa pasta, você encontrará Olá **armazenamento do azure** pacote, que contém as bibliotecas de hello, você precisa de armazenamento tooaccess.

### <a name="import-hello-package"></a>Importar o pacote de saudação
Adicionar Olá após o início de toohello de código da saudação **server.js** arquivo em seu aplicativo:

```nodejs
var azure = require('azure-storage');
```

## <a name="set-up-an-azure-storage-connection"></a>Configurar uma conexão do Armazenamento do Azure
módulo de saudação do azure lerá variáveis de ambiente hello AZURE\_armazenamento\_conta e o AZURE\_armazenamento\_acesso\_chave ou o AZURE\_armazenamento\_conexão \_Cadeia de caracteres de informações necessárias tooconnect tooyour conta de armazenamento do Azure. Se essas variáveis de ambiente não forem definidas, você deve especificar as informações de conta de saudação ao chamar **TableService**.

Para obter um exemplo de configuração de variáveis de ambiente Olá no hello [portal do Azure](https://portal.azure.com) para um site do Azure, consulte [usando o aplicativo web Node.js hello Azure serviço de tabela](../app-service-web/storage-nodejs-use-table-storage-web-site.md).

## <a name="create-a-table"></a>Criar uma tabela
Olá código a seguir cria um **TableService** do objeto e o utiliza toocreate uma nova tabela. Adicione a seguinte Olá superior de saudação do **server.js**.

```nodejs
var tableSvc = azure.createTableService();
```

Olá chamada muito**createTableIfNotExists** criará uma nova tabela com o nome especificado da saudação se ele ainda não existir. Olá, exemplo a seguir cria uma nova tabela chamada 'mytable' se ele ainda não existir:

```nodejs
tableSvc.createTableIfNotExists('mytable', function(error, result, response){
  if(!error){
    // Table exists or created
  }
});
```

Olá `result.created` será `true` se uma nova tabela é criada, e `false` se Olá tabela já existir. Olá `response` conterá informações sobre a solicitação de saudação.

### <a name="filters"></a>Filtros
Operações de filtragem opcionais podem ser aplicadas toooperations realizada usando **TableService**. As operações de filtragem podem incluir registro em log, repetição automática, etc. Os filtros são objetos que implementam um método com assinatura hello:

```nodejs
function handle (requestOptions, next)
```

Depois de fazer sua pré-processamento nas opções de solicitação hello, método hello precisa toocall "Avançar", passando um retorno de chamada com hello assinatura a seguir:

```nodejs
function (returnObject, finalCallback, next)
```

Esse retorno de chamada e após o processamento returnObject hello (resposta de saudação do servidor de toohello de solicitação de saudação), o retorno de chamada hello precisa tooeither invocar lado, se ele existe toocontinue outros filtros de processamento ou simplesmente chamar finalCallback caso contrário Olá de tooend invocação de serviço.

Dois filtros que implementam a lógica de repetição são incluídos com hello Azure SDK para Node.js, **ExponentialRetryPolicyFilter** e **LinearRetryPolicyFilter**. Olá seguir cria um **TableService** objeto que usa Olá **ExponentialRetryPolicyFilter**:

```nodejs
var retryOperations = new azure.ExponentialRetryPolicyFilter();
var tableSvc = azure.createTableService().withFilter(retryOperations);
```

## <a name="add-an-entity-tooa-table"></a>Adicionar uma tabela de entidade tooa
tooadd uma entidade, primeiro crie um objeto que define as propriedades de entidade. Todas as entidades devem conter um **PartitionKey** e **RowKey**, que são identificadores exclusivos para a entidade de saudação.

* **PartitionKey** -determina partição Olá Olá entidade será armazenada no
* **RowKey** - exclusivamente identifica a entidade Olá na partição Olá

Ambas, **PartitionKey** e **RowKey**, devem ser valores de cadeia de caracteres. Para obter mais informações, consulte [Olá Noções básicas sobre modelo de dados do serviço de tabela](http://msdn.microsoft.com/library/azure/dd179338.aspx).

a seguir Olá é um exemplo de definição de uma entidade. Observe que **dueDate** é definido com um tipo de **Edm.DateTime**. Especificar tipo de saudação é opcional, e tipos serão ser inferidos se não for especificados.

```nodejs
var task = {
  PartitionKey: {'_':'hometasks'},
  RowKey: {'_': '1'},
  description: {'_':'take out hello trash'},
  dueDate: {'_':new Date(2015, 6, 20), '$':'Edm.DateTime'}
};
```

> [!NOTE]
> Existe também um campo **Carimbo de Data/Hora** para cada registro, que é definido pelo Azure quando uma entidade é inserida ou atualizada.
>
>

Você também pode usar o hello **entityGenerator** toocreate entidades. Olá, exemplo a seguir cria Olá mesma entidade de tarefa usando Olá **entityGenerator**.

```nodejs
var entGen = azure.TableUtilities.entityGenerator;
var task = {
  PartitionKey: entGen.String('hometasks'),
  RowKey: entGen.String('1'),
  description: entGen.String('take out hello trash'),
  dueDate: entGen.DateTime(new Date(Date.UTC(2015, 6, 20))),
};
```

tooadd uma tabela de tooyour de entidade, passar toohello de objeto de entidade Olá **insertEntity** método.

```nodejs
tableSvc.insertEntity('mytable',task, function (error, result, response) {
  if(!error){
    // Entity inserted
  }
});
```

Se Olá operação for bem-sucedida, `result` conterá Olá [ETag](http://en.wikipedia.org/wiki/HTTP_ETag) de saudação inserida no registro e `response` contêm informações sobre a operação de saudação.

Resposta de exemplo:

```nodejs
{ '.metadata': { etag: 'W/"datetime\'2015-02-25T01%3A22%3A22.5Z\'"' } }
```

> [!NOTE]
> Por padrão, **insertEntity** não retornar a entidade Olá inserido como parte da saudação `response` informações. Se você planeja realizar outras operações nesta entidade ou deseja informações de saudação toocache, pode ser útil toohave retornou como parte da saudação `result`. Você pode fazer isso habilitando **echoContent** da seguinte maneira:
>
> `tableSvc.insertEntity('mytable', task, {echoContent: true}, function (error, result, response) {...}`
>
>

## <a name="update-an-entity"></a>Atualizar uma entidade
Há vários métodos e disponível tooupdate uma entidade existente:

* **replaceEntity** – atualiza uma entidade existente ao substituí-la
* **mergeEntity** -atualiza uma entidade existente, mesclando novos valores de propriedade para a entidade existente Olá
* **insertOrReplaceEntity** – atualiza uma entidade existente substituindo-a. Se não existir nenhuma entidade, uma nova será inserida
* **insertOrMergeEntity** -atualiza uma entidade existente, mesclando novos valores de propriedade em Olá existente. Se não existir nenhuma entidade, uma nova será inserida

Olá exemplo a seguir demonstra a atualização de uma entidade usando **replaceEntity**:

```nodejs
tableSvc.replaceEntity('mytable', updatedTask, function(error, result, response){
  if(!error) {
    // Entity updated
  }
});
```

> [!NOTE]
> Por padrão, a atualização de uma entidade não verifica toosee se dados hello está sendo atualizados anteriormente tem sido modificados por outro processo. atualizações simultâneas de toosupport:
>
> 1. Obter Olá ETag do objeto de hello está sendo atualizado. Isto é retornado como parte da saudação `response` para qualquer operação de entidade e podem ser recuperados por meio de `response['.metadata'].etag`.
> 2. Ao executar uma operação de atualização em uma entidade, adicione informações de ETag Olá recuperados anteriormente toohello nova entidade. Por exemplo:
>
>       entity2['.metadata'].etag = currentEtag;
> 3. Execute a operação de atualização de saudação. Se a entidade Olá foi modificada desde que você recuperou o valor de ETag hello, como outra instância do seu aplicativo, um `error` será retornado indicando que a condição de atualização de saudação especificada na solicitação de saudação não foi atendida.
>
>

Com **replaceEntity** e **mergeEntity**, se a entidade de saudação que está sendo atualizada não existir, e em seguida, haverá falha na operação de atualização de saudação. Portanto, se desejar toostore uma entidade, independentemente se ela já existir, usar **insertOrReplaceEntity** ou **insertOrMergeEntity**.

Olá `result` para atualização bem sucedida operações conterá Olá **Etag** Olá atualizadas entidade.

## <a name="work-with-groups-of-entities"></a>Trabalhar com grupos de entidades
Às vezes, faz sentido toosubmit várias operações juntos em um lote tooensure atômico processamento pelo servidor de saudação. tooaccomplish que use Olá **TableBatch** toocreate um lote de classe e, em seguida, usar o hello **executeBatch** método de **TableService** tooperform Olá de operações em lote.

 saudação de exemplo a seguir demonstra duas entidades em um lote de envio:

```nodejs
var task1 = {
  PartitionKey: {'_':'hometasks'},
  RowKey: {'_': '1'},
  description: {'_':'Take out hello trash'},
  dueDate: {'_':new Date(2015, 6, 20)}
};
var task2 = {
  PartitionKey: {'_':'hometasks'},
  RowKey: {'_': '2'},
  description: {'_':'Wash hello dishes'},
  dueDate: {'_':new Date(2015, 6, 20)}
};

var batch = new azure.TableBatch();

batch.insertEntity(task1, {echoContent: true});
batch.insertEntity(task2, {echoContent: true});

tableSvc.executeBatch('mytable', batch, function (error, result, response) {
  if(!error) {
    // Batch completed
  }
});
```

Para operações de lote bem-sucedido, `result` conterá informações para cada operação em lote hello.

### <a name="work-with-batched-operations"></a>Trabalhando com operações em lote
Operações adicionadas tooa lote pode ser inspecionado exibindo Olá `operations` propriedade. Você também pode usar o hello toowork métodos com as operações a seguir:

* **clear** – limpa todas as operações de um lote.
* **getOperations** -obtém uma operação de lote Olá
* **hasOperations** -retorna true se o lote Olá contém operações
* **removeOperations** – remove uma operação
* **tamanho** -retorna Olá número de operações em lote Olá

## <a name="retrieve-an-entity-by-key"></a>Recuperar uma entidade por chave
tooreturn uma entidade específica com base em Olá **PartitionKey** e **RowKey**, use Olá **retrieveEntity** método.

```nodejs
tableSvc.retrieveEntity('mytable', 'hometasks', '1', function(error, result, response){
  if(!error){
    // result contains hello entity
  }
});
```

Quando essa operação é concluída, `result` conterá entidade hello.

## <a name="query-a-set-of-entities"></a>Consultar um conjunto de entidades
tooquery uma tabela, use Olá **TableQuery** objeto toobuild uma expressão de consulta usando Olá cláusulas a seguir:

* **Selecione** -Olá campos toobe retornado da consulta de saudação
* **onde** - Olá onde cláusula

  * **and** – uma condição where `and`
  * **or** – uma condição where `or`
* **superior** -Olá o número de itens toofetch

Olá, exemplo a seguir cria uma consulta que retornará Olá primeiros cinco itens com um PartitionKey de 'hometasks'.

```nodejs
var query = new azure.TableQuery()
  .top(5)
  .where('PartitionKey eq ?', 'hometasks');
```

Como **select** não é usado, todos os campos serão retornados. consulta de saudação de tooperform em uma tabela, use **queryEntities**. Olá, exemplo a seguir usa entidades de tooreturn esta consulta de 'mytable'.

```nodejs
tableSvc.queryEntities('mytable',query, null, function(error, result, response) {
  if(!error) {
    // query was successful
  }
});
```

Se for bem-sucedido, `result.entries` conterá uma matriz de entidades que correspondem à consulta de saudação. Se a consulta Olá foi tooreturn não é possível todas as entidades, `result.continuationToken` serão não -*nulo* e pode ser usado como Olá terceiro parâmetro de **queryEntities** tooretrieve mais resultados. Para consulta inicial de hello, use *nulo* para o terceiro parâmetro de saudação.

### <a name="query-a-subset-of-entity-properties"></a>consultar um subconjunto de propriedades da entidade
Uma tabela de consulta tooa pode recuperar apenas alguns campos de uma entidade.
Isso reduz a largura de banda e pode melhorar o desempenho da consulta, principalmente em grandes entidades. Saudação de uso **selecione** cláusula e passar nomes de saudação do hello campos toobe retornados. Por exemplo, hello consulta a seguir retornará apenas Olá **descrição** e **dueDate** campos.

```nodejs
var query = new azure.TableQuery()
  .select(['description', 'dueDate'])
  .top(5)
  .where('PartitionKey eq ?', 'hometasks');
```

## <a name="delete-an-entity"></a>Excluir uma entidade
Você pode excluir uma entidade usando suas chaves de partição e de linha. Neste exemplo, Olá **task1** objeto contém Olá **RowKey** e **PartitionKey** valores hello entidade toobe excluído. E o objeto de saudação é passado toohello **deleteEntity** método.

```nodejs
var task = {
  PartitionKey: {'_':'hometasks'},
  RowKey: {'_': '1'}
};

tableSvc.deleteEntity('mytable', task, function(error, response){
  if(!error) {
    // Entity deleted
  }
});
```

> [!NOTE]
> Considere usar ETags quando a exclusão de itens, tooensure Olá item não foi modificada por outro processo. Veja [Atualizar uma entidade](#update-an-entity) para obter informações sobre o uso de ETags.
>
>

## <a name="delete-a-table"></a>Excluir uma tabela
saudação de código a seguir exclui uma tabela de uma conta de armazenamento.

```nodejs
tableSvc.deleteTable('mytable', function(error, response){
    if(!error){
        // Table deleted
    }
});
```

Se você não tiver certeza se a tabela de saudação existe, use **deleteTableIfExists**.

## <a name="use-continuation-tokens"></a>Usar tokens de continuação
Quando você estiver consultando tabelas com grandes quantidades de resultados, deverá procurar tokens de continuação. Pode haver grandes quantidades de dados disponíveis para a consulta que você talvez não percebam se você não criar toorecognize quando um token de continuação estiver presente.

resultados de saudação do objeto retornado durante consultar conjuntos de entidades um `continuationToken` propriedade quando esse token está presente. Você pode usar isso ao executar uma toomove toocontinue de consulta em entidades de partição e a tabela de saudação.

Ao consultar, um parâmetro de continuationToken pode ser fornecido entre a instância do objeto de consulta hello e função de retorno de chamada hello:

```nodejs
var nextContinuationToken = null;
dc.table.queryEntities(tableName,
    query,
    nextContinuationToken,
    function (error, results) {
        if (error) throw error;

        // iterate through results.entries with results

        if (results.continuationToken) {
            nextContinuationToken = results.continuationToken;
        }

    });
```

Se você inspecionar Olá `continuationToken` objeto, você encontrará propriedades como `nextPartitionKey`, `nextRowKey` e `targetLocation`, que pode ser usado tooiterate por meio de todos os resultados de saudação.

Também é um exemplo de continuação no repositório de Node.js do armazenamento do Azure Olá no GitHub. Procure `examples/samples/continuationsample.js`.

## <a name="work-with-shared-access-signatures"></a>Trabalhar com assinaturas de acesso compartilhado
Assinaturas de acesso compartilhado (SAS) são uma tootables de acesso granular de tooprovide de maneira segura sem fornecer o nome da conta de armazenamento ou chaves. SAS geralmente são usadas tooprovide limitado acessar tooyour os dados, como permitir que um aplicativo móvel tooquery registros.

Um aplicativo confiável como um serviço baseado em nuvem gera uma SAS usando Olá **generateSharedAccessSignature** de saudação **TableService**e fornece-tooan aplicativos de confiança parcial ou não confiáveis como um aplicativo móvel. Olá SAS é gerado usando uma política, que descreve o início de saudação e datas finais durante o qual Olá SAS é válido, bem como Olá detentor SAS do nível toohello concedido acesso.

Olá exemplo a seguir gera uma nova política de acesso compartilhado que permitirá a saudação da tabela SAS detentor tooquery ('r') hello e expira 100 minutos após o tempo de saudação que é criado.

```nodejs
var startDate = new Date();
var expiryDate = new Date(startDate);
expiryDate.setMinutes(startDate.getMinutes() + 100);
startDate.setMinutes(startDate.getMinutes() - 100);

var sharedAccessPolicy = {
  AccessPolicy: {
    Permissions: azure.TableUtilities.SharedAccessPermissions.QUERY,
    Start: startDate,
    Expiry: expiryDate
  },
};

var tableSAS = tableSvc.generateSharedAccessSignature('mytable', sharedAccessPolicy);
var host = tableSvc.host;
```

Observe que informações do host Olá devem ser fornecido, além disso, como é necessário quando detentor SAS Olá tentativas de tabela de saudação tooaccess.

Olá aplicativo cliente, em seguida, usa Olá SAS com **TableServiceWithSAS** tooperform operações em relação à tabela hello. saudação de exemplo a seguir conecta-se a tabela de toohello e executa uma consulta.

```nodejs
var sharedTableService = azure.createTableServiceWithSas(host, tableSAS);
var query = azure.TableQuery()
  .where('PartitionKey eq ?', 'hometasks');

sharedTableService.queryEntities(query, null, function(error, result, response) {
  if(!error) {
    // result contains hello entities
  }
});
```

Desde que hello SAS foi gerado com acesso somente de consulta, se uma tentativa foi feita tooinsert, atualizar ou excluir entidades, um erro será retornado.

### <a name="access-control-lists"></a>Listas de Controle de Acesso
Você também pode usar uma política de acesso de saudação de tooset de lista de controle de acesso (ACL) para uma SAS. Isso é útil se você quiser tooallow várias tabelas de saudação tooaccess de clientes, mas fornece as políticas de acesso diferentes para cada cliente.

Uma ACL é implementada através de um conjunto de políticas de acesso, com uma ID associada a cada política. saudação de exemplo a seguir define duas políticas, uma para 'user1' e outra para o 'Usuário2':

```nodejs
var sharedAccessPolicy = {
  user1: {
    Permissions: azure.TableUtilities.SharedAccessPermissions.QUERY,
    Start: startDate,
    Expiry: expiryDate
  },
  user2: {
    Permissions: azure.TableUtilities.SharedAccessPermissions.ADD,
    Start: startDate,
    Expiry: expiryDate
  }
};
```

Olá obtém de exemplo a seguir Olá ACL atual para Olá **hometasks** da tabela e, em seguida, adiciona novas políticas de saudação usando **setTableAcl**. Essa abordagem permite:

```nodejs
var extend = require('extend');
tableSvc.getTableAcl('hometasks', function(error, result, response) {
if(!error){
    var newSignedIdentifiers = extend(true, result.signedIdentifiers, sharedAccessPolicy);
    tableSvc.setTableAcl('hometasks', newSignedIdentifiers, function(error, result, response){
      if(!error){
        // ACL set
      }
    });
  }
});
```

Uma vez Olá que ACL tiver sido definido, você pode criar uma SAS com base na ID de saudação de uma política. saudação de exemplo a seguir cria uma nova SAS para 'Usuário2':

```nodejs
tableSAS = tableSvc.generateSharedAccessSignature('hometasks', { Id: 'user2' });
```

## <a name="next-steps"></a>Próximas etapas
Para obter mais informações, consulte Olá recursos a seguir.

* [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) é um aplicativo autônomo gratuito da Microsoft que permite que você toowork visualmente com dados de armazenamento do Azure no Linux, Windows e macOS.
* [SDK do Armazenamento do Azure para Node](https://github.com/Azure/azure-storage-node) no GitHub.
* [Centro de Desenvolvedores do Node.js](/develop/nodejs/)
* [Criar e implantar um aplicativo de Node. js tooan site do Azure](../app-service-web/app-service-web-get-started-nodejs.md)
