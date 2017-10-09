---
title: aaaHow toouse armazenamento de fila do Java | Microsoft Docs
description: "Saiba como toocreate de serviço de fila do Azure toouse hello e filas delete e insert, obtenham e excluir mensagens. Amostras escritas em Java."
services: storage
documentationcenter: java
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 68cecc8e-38c9-4a24-99e8-cb722bc63cf9
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 12/08/2016
ms.author: robinsh
ms.openlocfilehash: c2d5211ec5b6454f7dbc126aad4ba9950df13661
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-queue-storage-from-java"></a>Como toouse armazenamento de fila do Java
[!INCLUDE [storage-selector-queue-include](../../includes/storage-selector-queue-include.md)]

[!INCLUDE [storage-check-out-samples-java](../../includes/storage-check-out-samples-java.md)]

## <a name="overview"></a>Visão geral
Este guia mostrará como tooperform cenários comuns usando Olá serviço de armazenamento de fila do Azure. exemplos de saudação são escritos em Java e usam Olá [SDK de armazenamento do Azure para Java][Azure Storage SDK for Java]. Olá cenários abordados incluem **inserindo**, **inspecionar**, **obtendo**, e **excluindo** Enfileirar mensagens, bem como  **Criando** e **excluindo** filas. Para obter mais informações sobre filas, consulte Olá [próximas etapas](#Next-Steps) seção.

Observação: um SDK está disponível para os desenvolvedores que usam o Armazenamento do Azure em dispositivos Android. Para obter mais informações, consulte Olá [SDK de armazenamento do Azure para Android][Azure Storage SDK for Android].

[!INCLUDE [storage-queue-concepts-include](../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-java-application"></a>Criar um aplicativo Java
Neste guia, você usará os recursos de armazenamento que podem ser executados em um aplicativo Java localmente ou no código em execução em uma função web ou de trabalho do Azure.

toodo assim, você precisará tooinstall Olá Java Development Kit (JDK) e criar uma conta de armazenamento do Azure em sua assinatura do Azure. Depois de você ter feito isso, você precisará tooverify seu sistema de desenvolvimento atende aos requisitos mínimos de saudação e dependências que são listadas no hello [SDK de armazenamento do Azure para Java] [ Azure Storage SDK for Java] repositório no GitHub. Se seu sistema atende a esses requisitos, você pode seguir as instruções de saudação para baixar e instalar Olá bibliotecas de armazenamento do Azure para Java em seu sistema desse repositório. Depois de concluir essas tarefas, será possível toocreate um aplicativo Java que usa exemplos Olá neste artigo.

## <a name="configure-your-application-tooaccess-queue-storage"></a>Configurar o armazenamento de fila de tooaccess de aplicativo
Adicione Olá importação instruções toohello superior do arquivo de Java Olá onde você deseja que as filas de tooaccess APIs de armazenamento do Azure toouse a seguir:

```java
// Include hello following imports toouse queue APIs.
import com.microsoft.azure.storage.*;
import com.microsoft.azure.storage.queue.*;
```

## <a name="setup-an-azure-storage-connection-string"></a>Configurar uma cadeia de conexão de armazenamento do Azure
Um cliente de armazenamento do Azure usa um pontos de extremidade de toostore de cadeia de caracteres de conexão de armazenamento e as credenciais para acessar os serviços de gerenciamento de dados. Quando em execução em um aplicativo cliente, deve fornecer a cadeia de conexão de armazenamento Olá no formato a seguir, usando o nome de saudação da sua conta de armazenamento de saudação e Olá chave de acesso primária para conta de armazenamento Olá listada no hello [Portal do Azure](https://portal.azure.com)para Olá *AccountName* e *AccountKey* valores. Este exemplo mostra como você pode declarar uma cadeia de caracteres de conexão do campo estático toohold hello:

```java
// Define hello connection-string with your values.
public static final String storageConnectionString =
    "DefaultEndpointsProtocol=http;" +
    "AccountName=your_storage_account;" +
    "AccountKey=your_storage_account_key";
```

Em um aplicativo em execução dentro de uma função no Microsoft Azure, essa cadeia de caracteres pode ser armazenada no arquivo de configuração do serviço hello, *ServiceConfiguration*e pode ser acessado com uma chamada toohello  **RoleEnvironment.getConfigurationSettings** método. Aqui está um exemplo de obter a cadeia de caracteres de conexão de saudação de um **configuração** elemento chamado *StorageConnectionString* no arquivo de configuração de serviço hello:

```java
// Retrieve storage account from connection-string.
String storageConnectionString =
    RoleEnvironment.getConfigurationSettings().get("StorageConnectionString");
```

Olá exemplos a seguir pressupõem que você usou uma cadeia de conexão de armazenamento esses dois métodos tooget hello.

## <a name="how-to-create-a-queue"></a>Como criar uma fila
Um objeto **CloudQueueClient** permite que você obtenha objetos de referência para filas. Olá código a seguir cria um **CloudQueueClient** objeto. (Observação: existem outras maneiras toocreate **CloudStorageAccount** objetos; para obter mais informações, consulte **CloudStorageAccount** em Olá [referência de SDK de cliente de armazenamento de Azure].)

Saudação de uso **CloudQueueClient** tooget uma fila de toohello de referência que você deseja toouse do objeto. Você pode criar a fila de saudação se ele não existir.

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
       CloudStorageAccount.parse(storageConnectionString);

   // Create hello queue client.
   CloudQueueClient queueClient = storageAccount.createCloudQueueClient();

   // Retrieve a reference tooa queue.
   CloudQueue queue = queueClient.getQueueReference("myqueue");

   // Create hello queue if it doesn't already exist.
   queue.createIfNotExists();
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-add-a-message-tooa-queue"></a>Como: adicionar uma fila de mensagens tooa
tooinsert uma mensagem em uma fila existente, primeiro crie um novo **CloudQueueMessage**. Em seguida, chame Olá **addMessage** método. Um **CloudQueueMessage** pode ser criado por meio de uma cadeia de caracteres (em formato UTF-8) ou de uma matriz de bytes. Aqui está o código que cria uma fila (se não existir) e a mensagem de saudação inserções "Olá, mundo".

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
       CloudStorageAccount.parse(storageConnectionString);

    // Create hello queue client.
    CloudQueueClient queueClient = storageAccount.createCloudQueueClient();

    // Retrieve a reference tooa queue.
    CloudQueue queue = queueClient.getQueueReference("myqueue");

    // Create hello queue if it doesn't already exist.
    queue.createIfNotExists();

    // Create a message and add it toohello queue.
    CloudQueueMessage message = new CloudQueueMessage("Hello, World");
    queue.addMessage(message);
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-peek-at-hello-next-message"></a>Como: espiar a próxima mensagem de saudação
Você pode inspecionar mensagem de saudação na frente de saudação de uma fila sem removê-la da fila de saudação chamando **peekMessage**.

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
       CloudStorageAccount.parse(storageConnectionString);

    // Create hello queue client.
    CloudQueueClient queueClient = storageAccount.createCloudQueueClient();

    // Retrieve a reference tooa queue.
    CloudQueue queue = queueClient.getQueueReference("myqueue");

    // Peek at hello next message.
    CloudQueueMessage peekedMessage = queue.peekMessage();

    // Output hello message value.
    if (peekedMessage != null)
    {
      System.out.println(peekedMessage.getMessageContentAsString());
   }
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-change-hello-contents-of-a-queued-message"></a>Como: alterar o conteúdo de saudação de uma mensagem na fila
Você pode alterar o conteúdo de saudação de um mensagem no local na fila de saudação. Se a mensagem de saudação representa uma tarefa de trabalho, você pode usar esse status do recurso tooupdate Olá da tarefa de trabalho hello. saudação de código a seguir atualiza a mensagem da fila de saudação com novo conteúdo e conjuntos Olá tooextend de tempo limite de visibilidade outro 60 segundos. Isso salva o estado de saudação do trabalho associado à mensagem de saudação e fornece cliente Olá outro toocontinue minuto trabalhando na mensagem de saudação. Você pode usar esta técnica tootrack várias etapas os fluxos de trabalho na fila de mensagens, sem ter que toostart através do hello início se uma etapa de processamento falhar devido a falha de toohardware ou software. Normalmente, você mantém uma contagem de tentativa e se hello mensagem será repetida mais de  *n*  vezes, excluí-lo. Isso protege contra uma mensagem que dispara um erro do aplicativo sempre que for processada.

a seguir Olá pesquisas de exemplo por meio de fila de saudação de mensagens de código, localiza a primeira mensagem de saudação que corresponde a "Olá, mundo" para obter conteúdo hello, em seguida, modifica o conteúdo da mensagem de saudação e será encerrado.

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create hello queue client.
    CloudQueueClient queueClient = storageAccount.createCloudQueueClient();

    // Retrieve a reference tooa queue.
    CloudQueue queue = queueClient.getQueueReference("myqueue");

    // hello maximum number of messages that can be retrieved is 32.
    final int MAX_NUMBER_OF_MESSAGES_TO_PEEK = 32;

    // Loop through hello messages in hello queue.
    for (CloudQueueMessage message : queue.retrieveMessages(MAX_NUMBER_OF_MESSAGES_TO_PEEK,1,null,null))
    {
        // Check for a specific string.
        if (message.getMessageContentAsString().equals("Hello, World"))
        {
            // Modify hello content of hello first matching message.
            message.setMessageContent("Updated contents.");
            // Set it toobe visible in 30 seconds.
            EnumSet<MessageUpdateFields> updateFields =
                EnumSet.of(MessageUpdateFields.CONTENT,
                MessageUpdateFields.VISIBILITY);
            // Update hello message.
            queue.updateMessage(message, 30, updateFields, null, null);
            break;
        }
    }
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

Como alternativa, hello exemplo de código a seguir atualiza apenas Olá primeiro visível mensagem na fila de saudação.

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
       CloudStorageAccount.parse(storageConnectionString);

    // Create hello queue client.
    CloudQueueClient queueClient = storageAccount.createCloudQueueClient();

    // Retrieve a reference tooa queue.
    CloudQueue queue = queueClient.getQueueReference("myqueue");

    // Retrieve hello first visible message in hello queue.
    CloudQueueMessage message = queue.retrieveMessage();

    if (message != null)
    {
        // Modify hello message content.
        message.setMessageContent("Updated contents.");
        // Set it toobe visible in 60 seconds.
        EnumSet<MessageUpdateFields> updateFields =
            EnumSet.of(MessageUpdateFields.CONTENT,
            MessageUpdateFields.VISIBILITY);
        // Update hello message.
        queue.updateMessage(message, 60, updateFields, null, null);
    }
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-get-hello-queue-length"></a>Como: obter o comprimento da fila de saudação
Você pode obter uma estimativa do número de saudação de mensagens em uma fila. Olá **downloadAttributes** método solicita o serviço de fila Olá para vários valores atuais, incluindo uma contagem de quantas mensagens estão em uma fila. Contagem de saudação só é aproximada pois mensagens podem ser adicionadas ou removidas depois Olá serviço fila responde tooyour solicitação. Olá **getApproximateMessageCount** método retorna o último valor de saudação recuperado pela chamada de saudação muito**downloadAttributes**, sem chamar o serviço de fila de saudação.

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
       CloudStorageAccount.parse(storageConnectionString);

    // Create hello queue client.
    CloudQueueClient queueClient = storageAccount.createCloudQueueClient();

    // Retrieve a reference tooa queue.
    CloudQueue queue = queueClient.getQueueReference("myqueue");

   // Download hello approximate message count from hello server.
    queue.downloadAttributes();

    // Retrieve hello newly cached approximate message count.
    long cachedMessageCount = queue.getApproximateMessageCount();

    // Display hello queue length.
    System.out.println(String.format("Queue length: %d", cachedMessageCount));
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-dequeue-hello-next-message"></a>Como: remover da fila de mensagem de saudação do próxima
Seu código remove uma mensagem de um fila em duas etapas. Quando você chama **retrieveMessage**, obter próxima mensagem de saudação em uma fila. Uma mensagem retornada de **retrieveMessage** se torna invisível tooany outro código de leitura de mensagens dessa fila. Por padrão, essa mensagem permanece invisível por 30 segundos. toofinish mensagem de saudação remover da fila hello, você também deve chamar **deleteMessage**. Esse processo de duas etapas de remoção de uma mensagem garante que se seu código falha tooprocess que uma mensagem devido a falha de toohardware ou software, outra instância do seu código pode obter Olá a mesma mensagem e tente novamente. Seu código chama **deleteMessage** logo depois que a mensagem de saudação foi processada.

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create hello queue client.
    CloudQueueClient queueClient = storageAccount.createCloudQueueClient();

    // Retrieve a reference tooa queue.
    CloudQueue queue = queueClient.getQueueReference("myqueue");

    // Retrieve hello first visible message in hello queue.
    CloudQueueMessage retrievedMessage = queue.retrieveMessage();

    if (retrievedMessage != null)
    {
        // Process hello message in less than 30 seconds, and then delete hello message.
        queue.deleteMessage(retrievedMessage);
    }
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="additional-options-for-dequeuing-messages"></a>Opções adicionais para remover mensagens da fila
Há duas maneiras de personalizar a recuperação da mensagem de uma fila. Primeiro, você pode obter um lote de mensagens (até too32). Em seguida, você pode definir um tempo limite de invisibilidade maiores ou menores, permitindo que o código mais ou menos tempo toofully processam cada mensagem.

Olá, exemplo de código a seguir usa Olá **retrieveMessages** mensagens tooget 20 de método em uma chamada. Em seguida, ele processa cada mensagem usando um loop **for** . Ele também define Olá invisibilidade tempo limite toofive minutos (300 segundos para cada mensagem). Observe que Olá cinco minutos é iniciado para todas as mensagens em Olá mesmo tempo, portanto, quando cinco minutos se passaram desde chamada hello muito**retrieveMessages**, qualquer mensagem que não foram excluídas se tornará visível novamente.

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create hello queue client.
    CloudQueueClient queueClient = storageAccount.createCloudQueueClient();

    // Retrieve a reference tooa queue.
    CloudQueue queue = queueClient.getQueueReference("myqueue");

    // Retrieve 20 messages from hello queue with a visibility timeout of 300 seconds.
    for (CloudQueueMessage message : queue.retrieveMessages(20, 300, null, null)) {
        // Do processing for all messages in less than 5 minutes,
        // deleting each message after processing.
        queue.deleteMessage(message);
    }
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-list-hello-queues"></a>Como: listar Olá filas
tooobtain uma lista de filas de atual hello, chamada hello **CloudQueueClient.listQueues()** método, que retorna uma coleção de **CloudQueue** objetos.

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create hello queue client.
    CloudQueueClient queueClient =
        storageAccount.createCloudQueueClient();

    // Loop through hello collection of queues.
    for (CloudQueue queue : queueClient.listQueues())
    {
        // Output each queue name.
        System.out.println(queue.getName());
    }
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-delete-a-queue"></a>Como excluir uma fila
toodelete uma fila e todas as mensagens de saudação contidos nele, chamada hello **deleteIfExists** método hello **CloudQueue** objeto.

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create hello queue client.
    CloudQueueClient queueClient = storageAccount.createCloudQueueClient();

    // Retrieve a reference tooa queue.
    CloudQueue queue = queueClient.getQueueReference("myqueue");

    // Delete hello queue if it exists.
    queue.deleteIfExists();
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="next-steps"></a>Próximas etapas
Agora que você aprendeu as Noções básicas de saudação do armazenamento de fila, siga essas toolearn links sobre tarefas mais complexas de armazenamento.

* [Microsoft Azure Storage SDK for Java][Azure Storage SDK for Java] (SDK de Armazenamento do Microsoft Azure para Java)
* [referência de SDK de cliente de armazenamento de Azure][referência de SDK de cliente de armazenamento de Azure]
* [Azure Storage Services REST API Reference][Azure Storage Services REST API] (Referência de API REST dos Serviços de Armazenamento do Azure)
* [Microsoft Azure Storage Team Blog][Azure Storage Team Blog] (Blog da equipe de Armazenamento do Microsoft Azure)

[Azure SDK for Java]: http://go.microsoft.com/fwlink/?LinkID=525671
[Azure Storage SDK for Java]: https://github.com/azure/azure-storage-java
[Azure Storage SDK for Android]: https://github.com/azure/azure-storage-android
[referência de SDK de cliente de armazenamento de Azure]: http://dl.windowsazure.com/storage/javadoc/
[Azure Storage Services REST API]: https://msdn.microsoft.com/library/azure/dd179355.aspx
[Azure Storage Team Blog]: http://blogs.msdn.com/b/windowsazurestorage/
