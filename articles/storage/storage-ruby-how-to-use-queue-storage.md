---
title: aaaHow toouse armazenamento de fila do Ruby | Microsoft Docs
description: "Saiba como toocreate de serviço de fila do Azure toouse hello e filas delete e insert, obtenham e excluir mensagens. Exemplos gravados no Ruby."
services: storage
documentationcenter: ruby
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 59c2d81b-db9c-46ee-ade2-2f0caae6b1e6
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: ruby
ms.topic: article
ms.date: 12/08/2016
ms.author: robinsh
ms.openlocfilehash: 726c7d2f08b2d5938ee5f9dcdc2735e447388856
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-queue-storage-from-ruby"></a>Como toouse armazenamento de fila do Ruby
[!INCLUDE [storage-selector-queue-include](../../includes/storage-selector-queue-include.md)]

[!INCLUDE [storage-try-azure-tools-queues](../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a>Visão geral
Este guia mostra como os cenários comuns de tooperform usando Olá serviço de armazenamento de fila do Microsoft Azure. exemplos de saudação são gravados usando Olá Ruby a API do Azure.
Olá cenários abordados incluem **inserindo**, **inspecionar**, **obtendo**, e **excluindo** Enfileirar mensagens, bem como  **criar e excluir filas**.

[!INCLUDE [storage-queue-concepts-include](../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-ruby-application"></a>Criar um aplicativo Ruby
Crie um aplicativo Ruby. Para ver as instruções, confira [Aplicativo Web Ruby on Rails em uma VM do Azure](../virtual-machines/linux/classic/virtual-machines-linux-classic-ruby-rails-web-app.md).

## <a name="configure-your-application-tooaccess-storage"></a>Configurar seu aplicativo tooAccess armazenamento
toouse armazenamento do Azure, você precisa toodownload e use Olá Ruby pacote do azure, que inclui um conjunto de bibliotecas de conveniência que se comunicam com serviços da REST do armazenamento hello.

### <a name="use-rubygems-tooobtain-hello-package"></a>Use o pacote de saudação do RubyGems tooobtain
1. Use uma interface de linha de comando como **PowerShell** (Windows), **Terminal** (Mac) ou **Bash** (Unix).
2. Digite "gem instalar o azure" em gem de Olá Olá comando janela tooinstall e dependências.

### <a name="import-hello-package"></a>Importar o pacote de saudação
Use o editor de texto favorito, adicione Olá toohello superior de saudação arquivo Ruby onde você pretende toouse armazenamento a seguir:

```ruby
require "azure"
```

## <a name="setup-an-azure-storage-connection"></a>Configurar uma conexão de armazenamento do Azure
módulo de saudação do azure lerá variáveis de ambiente Olá **AZURE\_armazenamento\_conta** e **AZURE\_armazenamento\_ACCESS_KEY** para as informações necessárias a conta de armazenamento do Azure tooyour tooconnect. Se essas variáveis de ambiente não forem definidas, você deve especificar informações de conta de saudação antes de usar **Azure::QueueService** com hello código a seguir:

```ruby
Azure.config.storage_account_name = "<your azure storage account>"
Azure.config.storage_access_key = "<your Azure storage access key>"
```

tooobtain esses valores de um clássico ou Gerenciador de recursos de armazenamento de conta no hello portal do Azure:

1. Faça logon no toohello [portal do Azure](https://portal.azure.com).
2. Navegue toohello conta de armazenamento que você deseja toouse.
3. Na folha de configurações de saudação em saudação à direita, clique em **chaves de acesso**.
4. Olá acesso folha de chaves que aparece, você verá a chave de acesso de saudação 1 e 2 de chave de acesso. Você pode usar qualquer uma das duas. 
5. Clique em Olá copiar ícone toocopy Olá chave toohello área de transferência. 

tooobtain esses valores de um armazenamento clássico contam no portal do Azure clássico de saudação:

1. Faça logon no toohello [portal clássico do Azure](https://manage.windowsazure.com).
2. Navegue toohello conta de armazenamento que você deseja toouse.
3. Clique em **gerenciar chaves de acesso** na parte inferior de Olá Olá do painel de navegação.
4. Olá pop-up da caixa de diálogo, você verá o nome de conta de armazenamento hello, chave de acesso primária e chave de acesso secundária. Para a chave de acesso, você pode usar Olá principal ou Olá um secundário. 
5. Clique em Olá copiar ícone toocopy Olá chave toohello área de transferência.

## <a name="how-to-create-a-queue"></a>Como criar uma fila
Olá código a seguir cria um **Azure::QueueService** objeto, que permite que você toowork com filas.

```ruby
azure_queue_service = Azure::QueueService.new
```

Saudação de uso **create_queue()** nome do método toocreate uma fila com hello especificado.

```ruby
begin
  azure_queue_service.create_queue("test-queue")
rescue
  puts $!
end
```

## <a name="how-to-insert-a-message-into-a-queue"></a>Como inserir uma mensagem em uma fila
tooinsert uma mensagem em uma fila, use Olá **create_message()** método toocreate uma nova mensagem e adicioná-lo toohello fila.

```ruby
azure_queue_service.create_message("test-queue", "test message")
```

## <a name="how-to-peek-at-hello-next-message"></a>Como: Espiar a próxima mensagem de saudação
Você pode inspecionar mensagem de saudação na frente de saudação de uma fila sem removê-la da fila de saudação por chamada hello **inspeção\_messages()** método. Por padrão, o **peek\_messages()** inspeciona uma única mensagem. Você também pode especificar quantas mensagens você deseja toopeek.

```ruby
result = azure_queue_service.peek_messages("test-queue",
  {:number_of_messages => 10})
```

## <a name="how-to-dequeue-hello-next-message"></a>Como: Remover da fila Olá próxima mensagem
É possível remover uma mensagem da fila em duas etapas.

1. Quando você chama **lista\_messages()**, obter próxima mensagem de saudação em uma fila por padrão. Você também pode especificar quantas mensagens você deseja tooget. Olá mensagens retornadas do **lista\_messages()** se torna invisível tooany outro código de leitura de mensagens dessa fila. Você passa no tempo limite de visibilidade de saudação em segundos como um parâmetro.
2. toofinish mensagem de saudação remover da fila hello, você também deve chamar **delete_message()**.

Esse processo de duas etapas de remoção de uma mensagem garante que, quando seu tooprocess de falha de código pode obter uma mensagem devido a falha de toohardware ou software, outra instância do seu código Olá mesma mensagem e tente novamente. Seu código chama **excluir\_message()** logo depois que a mensagem de saudação foi processada.

```ruby
messages = azure_queue_service.list_messages("test-queue", 30)
azure_queue_service.delete_message("test-queue", 
  messages[0].id, messages[0].pop_receipt)
```

## <a name="how-to-change-hello-contents-of-a-queued-message"></a>Como: Alterar o conteúdo de saudação de uma mensagem na fila
Você pode alterar o conteúdo de saudação de um mensagem no local na fila de saudação. código de saudação abaixo usa Olá **update_message()** método tooupdate uma mensagem. método Hello retornará uma tupla que contém a confirmação pop Olá de mensagem da fila de saudação e um valor de tempo de data UTC que representa quando a mensagem de saudação ficará visível na fila de saudação.

```ruby
message = azure_queue_service.list_messages("test-queue", 30)
pop_receipt, time_next_visible = azure_queue_service.update_message(
  "test-queue", message.id, message.pop_receipt, "updated test message", 
  30)
```

## <a name="how-to-additional-options-for-dequeuing-messages"></a>Como adicionar opções para remover mensagens da fila
Há duas maneiras de personalizar a recuperação da mensagem de uma fila.

1. Você pode obter um lote de mensagens.
2. Você pode definir um tempo limite de invisibilidade maiores ou menores, permitindo que o código mais ou menos tempo toofully processam cada mensagem.

Olá, exemplo de código a seguir usa Olá **lista\_messages()** mensagens tooget 15 de método em uma chamada. Em seguida, ele lê e exclui cada mensagem. Ele também define minutos de toofive de tempo limite de invisibilidade de saudação para cada mensagem.

```ruby
azure_queue_service.list_messages("test-queue", 300
  {:number_of_messages => 15}).each do |m|
  puts m.message_text
  azure_queue_service.delete_message("test-queue", m.id, m.pop_receipt)
end
```

## <a name="how-to-get-hello-queue-length"></a>Como Obter Olá comprimento da fila
Você pode obter uma estimativa do número de saudação de mensagens na fila de saudação. Olá **obter\_fila\_metadata()** método faz a contagem de aproximada das mensagens de saudação Olá fila serviço tooreturn e metadados sobre fila hello.

```ruby
message_count, metadata = azure_queue_service.get_queue_metadata(
  "test-queue")
```

## <a name="how-to-delete-a-queue"></a>Como excluir uma fila
toodelete uma fila e todas as mensagens de saudação contidos nele, chamada hello **excluir\_Queue ()** método no objeto de fila de saudação.

```ruby
azure_queue_service.delete_queue("test-queue")
```

## <a name="next-steps"></a>Próximas etapas
Agora que você aprendeu as Noções básicas de saudação do armazenamento de fila, siga essas toolearn links sobre tarefas mais complexas de armazenamento.

* Visite Olá [Blog da equipe do armazenamento do Azure](http://blogs.msdn.com/b/windowsazurestorage/)
* Visite Olá [SDK do Azure para Ruby](https://github.com/WindowsAzure/azure-sdk-for-ruby) repositório no GitHub

Para obter uma comparação entre Olá serviço de fila do Azure discutidos neste artigo e filas do barramento de serviço do Azure discutidos Olá [como toouse filas do barramento de serviço](/develop/ruby/how-to-guides/service-bus-queues/) do artigo, consulte [filas do Azure e filas do Service Bus - comparadas e Contrastados](../service-bus-messaging/service-bus-azure-and-service-bus-queues-compared-contrasted.md)
