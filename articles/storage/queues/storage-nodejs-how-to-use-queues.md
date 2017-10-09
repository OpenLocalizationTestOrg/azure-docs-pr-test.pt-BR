---
title: aaaHow toouse armazenamento de fila do Node. js | Microsoft Docs
description: "Saiba como toocreate de serviço de fila do Azure toouse hello e filas delete e insert, obtenham e excluir mensagens. Amostras escritas em Node.js."
services: storage
documentationcenter: nodejs
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: a8a92db0-4333-43dd-a116-28b3147ea401
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 12/08/2016
ms.author: robinsh
ms.openlocfilehash: 7e9778da4efa69f2e9d8fd480b9b6f5ace85951e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-queue-storage-from-nodejs"></a>Como toouse armazenamento de fila do Node. js
[!INCLUDE [storage-selector-queue-include](../../../includes/storage-selector-queue-include.md)]

[!INCLUDE [storage-check-out-samples-all](../../../includes/storage-check-out-samples-all.md)]

## <a name="overview"></a>Visão geral
Este guia mostra como os cenários comuns de tooperform usando Olá serviço de fila do Microsoft Azure. exemplos de saudação são gravados usando Olá API Node. js. Olá cenários abordados incluem **inserindo**, **inspecionar**, **obtendo**, e **excluindo** Enfileirar mensagens, bem como  **criar e excluir filas**.

[!INCLUDE [storage-queue-concepts-include](../../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

## <a name="create-a-nodejs-application"></a>Criar um aplicativo Node.js
Criar um aplicativo Node.js em branco. Para obter instruções sobre como criar um aplicativo Node. js, consulte [criar um aplicativo da web Node. js no serviço de aplicativo do Azure](../../app-service-web/app-service-web-get-started-nodejs.md), [criar e implantar um aplicativo de Node. js tooan serviço de nuvem do Azure](../../cloud-services/cloud-services-nodejs-develop-deploy-app.md) usando o Windows PowerShell ou [ Criar e implantar um tooAzure de aplicativo web Node.js usando o Web Matrix](https://www.microsoft.com/web/webmatrix/).

## <a name="configure-your-application-tooaccess-storage"></a>Configurar seu aplicativo tooAccess armazenamento
toouse armazenamento do Azure, você precisa hello Azure Storage SDK para Node.js, que inclui um conjunto de bibliotecas de conveniência que se comunicam com serviços da REST do armazenamento Olá.

### <a name="use-node-package-manager-npm-tooobtain-hello-package"></a>Usar o pacote de saudação do Gerenciador de pacote de nó (NPM) tooobtain
1. Use uma interface de linha de comando como **PowerShell** (Windows), **Terminal** (Mac), ou **Bash** (Unix), navegue toohello pasta em que você criou o aplicativo de exemplo.
2. Tipo **npm instalar o armazenamento do azure** na janela de comando hello. A saída do comando de saudação é semelhante toohello exemplo a seguir.
 
    ```
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
    ```

3. Você pode executar manualmente Olá **ls** tooverify de comando que um **nó\_módulos** pasta foi criada. Dentro dessa pasta, você encontrará Olá **armazenamento do azure** pacote, que contém as bibliotecas de hello, você precisa acessar o armazenamento.

### <a name="import-hello-package"></a>Importar o pacote de saudação
Usando o bloco de notas ou outro editor de texto, adicione Olá toohello superior a seguir o **server.js** arquivo de aplicativo hello onde você pretende toouse armazenamento:

```
var azure = require('azure-storage');
```

## <a name="setup-an-azure-storage-connection"></a>Configurar uma conexão de armazenamento do Azure
módulo de saudação do azure lerá variáveis de ambiente hello AZURE\_armazenamento\_conta e o AZURE\_armazenamento\_acesso\_chave ou o AZURE\_armazenamento\_conexão \_Cadeia de caracteres de informações necessárias tooconnect tooyour conta de armazenamento do Azure. Se essas variáveis de ambiente não forem definidas, você deve especificar as informações de conta de saudação ao chamar **createQueueService**.

Para obter um exemplo de configuração de variáveis de ambiente Olá no hello [Portal do Azure](https://portal.azure.com) para um site do Azure, consulte [Node. js web app usando] Olá serviço tabela do Azure.

## <a name="how-to-create-a-queue"></a>Como criar uma fila
Olá código a seguir cria um **QueueService** objeto, que permite que você toowork com filas.

```
var queueSvc = azure.createQueueService();
```

Saudação de uso **createQueueIfNotExists** método, que retorna a fila especificada Olá se ela já existir, ou cria uma nova fila com o nome especificado da saudação se ele ainda não existir.

```
queueSvc.createQueueIfNotExists('myqueue', function(error, result, response){
  if(!error){
    // Queue created or exists
  }
});
```

Se a fila de saudação é criada, `result.created` é verdadeiro. Se a fila de saudação existir, `result.created` é false.

### <a name="filters"></a>Filtros
Operações de filtragem opcionais podem ser aplicadas toooperations realizada usando **QueueService**. As operações de filtragem podem incluir registro em log, repetição automática, etc. Os filtros são objetos que implementam um método com assinatura hello:

```
function handle (requestOptions, next)
```

Depois de fazer sua pré-processamento nas opções de solicitação hello, método hello precisa toocall "Avançar" passando um retorno de chamada com hello assinatura a seguir:

```
function (returnObject, finalCallback, next)
```

Esse retorno de chamada e após o processamento returnObject hello (resposta de saudação do servidor de toohello de solicitação de saudação), o retorno de chamada hello precisa tooeither invocar lado, se ele existe toocontinue outros filtros de processamento ou simplesmente chamar finalCallback tooend caso contrário, a saudação invocação de serviço.

Dois filtros que implementam a lógica de repetição são incluídos com hello Azure SDK para Node.js, **ExponentialRetryPolicyFilter** e **LinearRetryPolicyFilter**. Olá seguir cria um **QueueService** objeto que usa Olá **ExponentialRetryPolicyFilter**:

```
var retryOperations = new azure.ExponentialRetryPolicyFilter();
var queueSvc = azure.createQueueService().withFilter(retryOperations);
```

## <a name="how-to-insert-a-message-into-a-queue"></a>Como inserir uma mensagem em uma fila
tooinsert uma mensagem em uma fila, use Olá **createMessage** método para criar uma nova mensagem e adicioná-lo toohello fila.

```
queueSvc.createMessage('myqueue', "Hello world!", function(error, result, response){
  if(!error){
    // Message inserted
  }
});
```

## <a name="how-to-peek-at-hello-next-message"></a>Como: Espiar a próxima mensagem de saudação
Você pode inspecionar mensagem de saudação na frente de saudação de uma fila sem removê-la da fila de saudação por chamada hello **peekMessages** método. Por padrão, **peekMessages** inspeciona uma única mensagem.

```
queueSvc.peekMessages('myqueue', function(error, result, response){
  if(!error){
    // Message text is in messages[0].messageText
  }
});
```

Olá `result` contém a mensagem de saudação.

> [!NOTE]
> Usando **peekMessages** quando não existem mensagens na fila de saudação não retornará um erro, mas nenhuma mensagem será retornada.
> 
> 

## <a name="how-to-dequeue-hello-next-message"></a>Como: Remover da fila Olá próxima mensagem
O processamento de uma mensagem é um processo de duas fases:

1. Mensagem de saudação de remoção da fila.
2. Exclua mensagem de saudação.

toodequeue uma mensagem, use **getMessages**. Isso faz com que mensagens de saudação invisível na fila Olá, para que outros clientes não podem processá-los. Depois que seu aplicativo tiver processado uma mensagem, chame **deleteMessage** toodelete-la da fila de saudação. saudação de exemplo a seguir obtém uma mensagem e exclui-lo:

```
queueSvc.getMessages('myqueue', function(error, result, response){
  if(!error){
    // Message text is in messages[0].messageText
    var message = result[0];
    queueSvc.deleteMessage('myqueue', message.messageId, message.popReceipt, function(error, response){
      if(!error){
        //message deleted
      }
    });
  }
});
```

> [!NOTE]
> Por padrão, uma mensagem apenas ficará oculta para 30 segundos, após o qual é visível tooother clientes. Você pode especificar um valor diferente usando `options.visibilityTimeout` com **getMessages**.
> 
> [!NOTE]
> Usando **getMessages** quando não existem mensagens na fila de saudação não retornará um erro, mas nenhuma mensagem será retornada.
> 
> 

## <a name="how-to-change-hello-contents-of-a-queued-message"></a>Como: Alterar o conteúdo de saudação de uma mensagem na fila
Você pode alterar o conteúdo de saudação de um mensagem no local Olá fila usando **updateMessage**. saudação de exemplo a seguir atualiza o texto de saudação de uma mensagem:

```
queueSvc.getMessages('myqueue', function(error, result, response){
  if(!error){
    // Got hello message
    var message = result[0];
    queueSvc.updateMessage('myqueue', message.messageId, message.popReceipt, 10, {messageText: 'new text'}, function(error, result, response){
      if(!error){
        // Message updated successfully
      }
    });
  }
});
```

## <a name="how-to-additional-options-for-dequeuing-messages"></a>Como adicionar opções para remover mensagens da fila
Há duas maneiras de personalizar a recuperação da mensagem de uma fila:

* `options.numOfMessages`-Recuperar um lote de mensagens (até too32).
* `options.visibilityTimeout` - definir um tempo limite de invisibilidade mais longo ou mais curto.

Olá, exemplo a seguir usa Olá **getMessages** mensagens tooget 15 de método em uma chamada. Em seguida, ele processa cada mensagem usando um loop for. Ele também define minutos de toofive de tempo limite de invisibilidade de saudação para todas as mensagens retornadas por este método.

```
queueSvc.getMessages('myqueue', {numOfMessages: 15, visibilityTimeout: 5 * 60}, function(error, result, response){
  if(!error){
    // Messages retreived
    for(var index in result){
      // text is available in result[index].messageText
      var message = result[index];
      queueSvc.deleteMessage(queueName, message.messageId, message.popReceipt, function(error, response){
        if(!error){
          // Message deleted
        }
      });
    }
  }
});
```

## <a name="how-to-get-hello-queue-length"></a>Como Obter Olá comprimento da fila
Olá **getQueueMetadata** retorna metadados sobre a fila de hello, incluindo o número aproximado de mensagens aguardando na fila de saudação hello.

```
queueSvc.getQueueMetadata('myqueue', function(error, result, response){
  if(!error){
    // Queue length is available in result.approximateMessageCount
  }
});
```

## <a name="how-to-list-queues"></a>Como: Listar Filas
tooretrieve uma lista de filas, use **listQueuesSegmented**. tooretrieve uma lista filtrada por um prefixo específico, use **listQueuesSegmentedWithPrefix**.

```
queueSvc.listQueuesSegmented(null, function(error, result, response){
  if(!error){
    // result.entries contains hello list of queues
  }
});
```

Se todas as filas não podem ser retornadas, `result.continuationToken` pode ser usado como Olá primeiro parâmetro de **listQueuesSegmented** ou Olá segundo parâmetro de **listQueuesSegmentedWithPrefix** tooretrieve mais resultados.

## <a name="how-to-delete-a-queue"></a>Como excluir uma fila
toodelete uma fila e todas as mensagens de saudação contidos nela, chame o **deleteQueue** método no objeto de fila de saudação.

```
queueSvc.deleteQueue(queueName, function(error, response){
  if(!error){
    // Queue has been deleted
  }
});
```

tooclear todas as mensagens de uma fila sem excluí-la, use **clearMessages**.

## <a name="how-to-work-with-shared-access-signatures"></a>Como: Trabalhar com assinaturas de acesso compartilhado
Assinaturas de acesso compartilhado (SAS) são uma tooqueues de acesso granular de tooprovide de maneira segura sem fornecer o nome da conta de armazenamento ou chaves. SAS geralmente são as filas tooyour de acesso usados tooprovide limitado, como permitir que um aplicativo móvel toosubmit mensagens.

Um aplicativo confiável como um serviço baseado em nuvem gera uma SAS usando Olá **generateSharedAccessSignature** de saudação **QueueService**e fornece-tooan aplicativos de confiança parcial ou não confiável. Por exemplo, um aplicativo móvel. Olá SAS é gerado usando uma política, que descreve o início de saudação e datas finais durante o qual Olá SAS é válido, bem como Olá detentor SAS do nível toohello concedido acesso.

saudação de exemplo a seguir gera uma nova política de acesso compartilhado que permitirá Olá a fila SAS detentor tooadd mensagens toohello e expira 100 minutos após o tempo de saudação que é criado.

```
var startDate = new Date();
var expiryDate = new Date(startDate);
expiryDate.setMinutes(startDate.getMinutes() + 100);
startDate.setMinutes(startDate.getMinutes() - 100);

var sharedAccessPolicy = {
  AccessPolicy: {
    Permissions: azure.QueueUtilities.SharedAccessPermissions.ADD,
    Start: startDate,
    Expiry: expiryDate
  }
};

var queueSAS = queueSvc.generateSharedAccessSignature('myqueue', sharedAccessPolicy);
var host = queueSvc.host;
```

Observe que informações do host Olá devem ser fornecido, além disso, como é necessário quando detentor SAS Olá tentativas de fila de saudação tooaccess.

Olá aplicativo cliente, em seguida, usa Olá SAS com **QueueServiceWithSAS** tooperform operações em fila hello. saudação de exemplo a seguir conecta-se a fila de toohello e cria uma mensagem.

```
var sharedQueueService = azure.createQueueServiceWithSas(host, queueSAS);
sharedQueueService.createMessage('myqueue', 'Hello world from SAS!', function(error, result, response){
  if(!error){
    //message added
  }
});
```

Desde que hello SAS foi gerado com acesso de adicionar, se uma tentativa foi feita tooread, atualizar ou excluir mensagens, um erro será retornado.

### <a name="access-control-lists"></a>Listas de controle de acesso
Você também pode usar uma política de acesso de saudação de tooset de lista de controle de acesso (ACL) para uma SAS. Isso é útil se você quiser tooallow várias filas de saudação tooaccess de clientes, mas fornece as políticas de acesso diferentes para cada cliente.

Uma ACL é implementada através de um conjunto de políticas de acesso, com uma ID associada a cada política. saudação de exemplo a seguir define duas políticas; um para 'user1' e outro para o 'Usuário2':

```
var sharedAccessPolicy = {
  user1: {
    Permissions: azure.QueueUtilities.SharedAccessPermissions.PROCESS,
    Start: startDate,
    Expiry: expiryDate
  },
  user2: {
    Permissions: azure.QueueUtilities.SharedAccessPermissions.ADD,
    Start: startDate,
    Expiry: expiryDate
  }
};
```

Olá obtém de exemplo a seguir Olá ACL atual para **myqueue**, em seguida, adiciona novas políticas de saudação usando **setQueueAcl**. Essa abordagem permite:

```
var extend = require('extend');
queueSvc.getQueueAcl('myqueue', function(error, result, response) {
  if(!error){
    var newSignedIdentifiers = extend(true, result.signedIdentifiers, sharedAccessPolicy);
    queueSvc.setQueueAcl('myqueue', newSignedIdentifiers, function(error, result, response){
      if(!error){
        // ACL set
      }
    });
  }
});
```

Uma vez Olá que ACL tiver sido definido, você pode criar uma SAS com base na ID de saudação de uma política. saudação de exemplo a seguir cria uma nova SAS para 'Usuário2':

```
queueSAS = queueSvc.generateSharedAccessSignature('myqueue', { Id: 'user2' });
```

## <a name="next-steps"></a>Próximas etapas
Agora que você aprendeu as Noções básicas de saudação do armazenamento de fila, siga essas toolearn links sobre tarefas mais complexas de armazenamento.

* Visite Olá [Azure Storage Team Blog] [Blog da equipe do armazenamento do Azure].
* Visite Olá [SDK de armazenamento do Azure para o nó] [ Azure Storage SDK for Node] repositório no GitHub.

[Azure Storage SDK for Node]: https://github.com/Azure/azure-storage-node
[using hello REST API]: http://msdn.microsoft.com/library/azure/hh264518.aspx
[Azure Portal]: https://portal.azure.com
[Criar um aplicativo Web do Node.js no Serviço de Aplicativo do Azure](../../app-service-web/app-service-web-get-started-nodejs.md)   
[Aplicativo de web Node. js usando Olá serviço tabela do Azure](../../app-service-web/storage-nodejs-use-table-storage-web-site.md)
  


[Criar e implantar um aplicativo de Node. js tooan serviço de nuvem do Azure](../../cloud-services/cloud-services-nodejs-develop-deploy-app.md)   
[Blog da equipe do armazenamento do azure]: http://blogs.msdn.com/b/windowsazurestorage/ [compilar e implantar um tooAzure de aplicativo web Node.js usando o Web Matrix]: https://www.microsoft.com/web/webmatrix/   
