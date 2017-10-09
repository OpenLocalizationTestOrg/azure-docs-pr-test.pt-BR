---
title: aaaHow toouse armazenamento de tabela do Azure do Ruby | Microsoft Docs
description: "Armazene dados estruturados em nuvem hello usando o armazenamento de tabela do Azure, um repositório de dados NoSQL."
services: cosmos-db
documentationcenter: ruby
author: mimig1
manager: jhubbard
editor: 
ms.assetid: 047cd9ff-17d3-4c15-9284-1b5cc61a3224
ms.service: cosmos-db
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: ruby
ms.topic: article
ms.date: 12/08/2016
ms.author: mimig
ms.openlocfilehash: 2f9eb5a9160b551d6d1d198869787070c402b1d4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-table-storage-from-ruby"></a>Como toouse armazenamento de tabela do Azure do Ruby
[!INCLUDE [storage-selector-table-include](../../includes/storage-selector-table-include.md)]
[!INCLUDE [storage-table-cosmos-db-langsoon-tip-include](../../includes/storage-table-cosmos-db-langsoon-tip-include.md)]

## <a name="overview"></a>Visão geral
Este guia mostra como os cenários comuns de tooperform usando Olá serviço tabela do Azure. exemplos de saudação são gravados usando Olá Ruby API. Olá cenários abordados incluem **criação e exclusão de uma tabela, inserir e consultar entidades em uma tabela**.

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-ruby-application"></a>Criar um aplicativo Ruby
Para obter instruções como toocreate um aplicativo Ruby, consulte [Ruby no aplicativo Web de trilhos em uma VM do Azure](../virtual-machines/linux/classic/virtual-machines-linux-classic-ruby-rails-web-app.md).

## <a name="configure-your-application-tooaccess-storage"></a>Configurar o armazenamento de tooaccess do aplicativo
toouse armazenamento do Azure, você precisa toodownload e use Olá Ruby pacote do azure que inclui um conjunto de bibliotecas de conveniência que se comunicam com serviços da REST do armazenamento hello.

### <a name="use-rubygems-tooobtain-hello-package"></a>Use o pacote de saudação do RubyGems tooobtain
1. Use uma interface de linha de comando como **PowerShell** (Windows), **Terminal** (Mac) ou **Bash** (Unix).
2. Tipo **azure de instalação de gem** gem de Olá Olá comando janela tooinstall e dependências.

### <a name="import-hello-package"></a>Importar o pacote de saudação
Use o editor de texto favorito, adicione Olá toohello superior de saudação arquivo Ruby onde você pretende toouse armazenamento a seguir:

```ruby
require "azure"
```

## <a name="set-up-an-azure-storage-connection"></a>Configurar uma conexão do Armazenamento do Azure
Olá módulo do azure lerá variáveis de ambiente Olá **AZURE\_armazenamento\_conta** e **AZURE\_armazenamento\_acesso\_chave**para obter informações necessárias a conta de armazenamento do Azure tooyour tooconnect. Se essas variáveis de ambiente não forem definidas, você deve especificar informações de conta de saudação antes de usar **Azure::TableService** com hello código a seguir:

```ruby
Azure.config.storage_account_name = "<your azure storage account>"
Azure.config.storage_access_key = "<your azure storage access key>"
```

tooobtain esses valores de um clássico ou Gerenciador de recursos de armazenamento de conta no hello portal do Azure:

1. Faça logon no toohello [portal do Azure](https://portal.azure.com).
2. Navegue toohello conta de armazenamento que você deseja toouse.
3. Na folha de configurações de saudação em saudação à direita, clique em **chaves de acesso**.
4. Olá acesso folha de chaves que aparece, você verá a chave de acesso de saudação 1 e 2 de chave de acesso. Você pode usar qualquer uma das duas.
5. Clique em Olá copiar ícone toocopy Olá chave toohello área de transferência.

## <a name="create-a-table"></a>Criar uma tabela
Olá **Azure::TableService** objeto permite que você trabalhe com tabelas e entidades. toocreate uma tabela, use Olá **criar\_table()** método. Olá, exemplo a seguir cria uma tabela ou imprime Olá erro, se houver algum.

```ruby
azure_table_service = Azure::TableService.new
begin
    azure_table_service.create_table("testtable")
rescue
    puts $!
end
```

## <a name="add-an-entity-tooa-table"></a>Adicionar uma tabela de entidade tooa
tooadd uma entidade, primeiro crie um objeto de hash que define as propriedades de entidade. É importante lembrar que, para cada entidade, você deve especificar um **PartitionKey** e um **RowKey**. Esses são Olá identificadores exclusivos de suas entidades e os valores que podem ser consultados muito mais rápido do que as outras propriedades. Armazenamento do Azure usa **PartitionKey** tooautomatically distribuir entidades da tabela Olá em vários nós de armazenamento. Entidades com hello mesmo **PartitionKey** são armazenados em Olá mesmo nó. Olá **RowKey** é Olá a ID exclusiva da entidade de saudação na partição Olá pertence a.

```ruby
entity = { "content" => "test entity",
    :PartitionKey => "test-partition-key", :RowKey => "1" }
azure_table_service.insert_entity("testtable", entity)
```

## <a name="update-an-entity"></a>Atualizar uma entidade
Há vários métodos e disponível tooupdate uma entidade existente:

* **update\_entity():** atualiza uma entidade existente substituindo-a.
* **mesclagem\_entity():** atualiza uma entidade existente, mesclando novos valores de propriedade para a entidade existente hello.
* **insert\_or\_merge\_entity():** atualiza uma entidade existente substituindo-a. Se não existir nenhuma entidade, uma nova será inserida:
* **Inserir\_ou\_substituir\_entity():** atualiza uma entidade existente, mesclando novos valores de propriedade para a entidade existente hello. Se nenhuma entidade existir, uma nova será inserida.

Olá exemplo a seguir demonstra a atualização de uma entidade usando **atualizar\_entity()**:

```ruby
entity = { "content" => "test entity with updated content",
    :PartitionKey => "test-partition-key", :RowKey => "1" }
azure_table_service.update_entity("testtable", entity)
```

Com **atualizar\_entity()** e **mesclagem\_entity()**, se a entidade Olá que você está atualizando não existir, haverá falha na operação de atualização de saudação. Portanto, se você quiser toostore uma entidade, independentemente se ela já existir, você deve usar **inserir\_ou\_substituir\_entity()** ou **inserir\_ou \_mesclagem\_entity()**.

## <a name="work-with-groups-of-entities"></a>Trabalhar com grupos de entidades
Às vezes, faz sentido toosubmit várias operações juntos em um lote tooensure atômico processamento pelo servidor de saudação. tooaccomplish, criar um **lote** de objeto e, em seguida, usar Olá **executar\_batch()** método **TableService**. Olá exemplo a seguir demonstra enviando duas entidades com RowKey 2 e 3 em um lote. Observe que ele somente funciona para entidades com hello mesmo PartitionKey.

```ruby
azure_table_service = Azure::TableService.new
batch = Azure::Storage::Table::Batch.new("testtable",
    "test-partition-key") do
    insert "2", { "content" => "new content 2" }
    insert "3", { "content" => "new content 3" }
end
results = azure_table_service.execute_batch(batch)
```

## <a name="query-for-an-entity"></a>Consultar uma entidade
tooquery uma entidade em uma tabela, use Olá **obter\_entity()** método, passando o nome da tabela hello, **PartitionKey** e **RowKey**.

```ruby
result = azure_table_service.get_entity("testtable", "test-partition-key",
    "1")
```

## <a name="query-a-set-of-entities"></a>Consultar um conjunto de entidades
tooquery um conjunto de entidades em uma tabela, crie um objeto de hash de consulta e use Olá **consulta\_entities()** método. Olá exemplo a seguir demonstra obtendo todas as entidades de saudação com hello mesmo **PartitionKey**:

```ruby
query = { :filter => "PartitionKey eq 'test-partition-key'" }
result, token = azure_table_service.query_entities("testtable", query)
```

> [!NOTE]
> Se o conjunto de resultados de saudação é muito grande para uma única consulta tooreturn, um token de continuação será retornado que você pode usar as páginas subsequentes tooretrieve.
>
>

## <a name="query-a-subset-of-entity-properties"></a>consultar um subconjunto de propriedades da entidade
Uma tabela de consulta tooa pode recuperar apenas algumas propriedades de uma entidade. Essa técnica, chamada "projeção", reduz a largura de banda e pode melhorar o desempenho da consulta, principalmente em grandes entidades. Cláusula select de saudação de uso e os nomes de saudação de passagem de Olá propriedades que você gostaria que toobring sobre toohello cliente.

```ruby
query = { :filter => "PartitionKey eq 'test-partition-key'",
    :select => ["content"] }
result, token = azure_table_service.query_entities("testtable", query)
```

## <a name="delete-an-entity"></a>Excluir uma entidade
toodelete uma entidade, use Olá **excluir\_entity()** método. É necessário toopass no nome de saudação da tabela de saudação que contém a entidade hello, Olá PartitionKey e RowKey da entidade de saudação.

```ruby
azure_table_service.delete_entity("testtable", "test-partition-key", "1")
```

## <a name="delete-a-table"></a>Excluir uma tabela
toodelete uma tabela, use Olá **excluir\_table()** método e passar no nome de saudação do hello tabela que você deseja toodelete.

```ruby
azure_table_service.delete_table("testtable")
```

## <a name="next-steps"></a>Próximas etapas

* [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) é um aplicativo autônomo gratuito da Microsoft que permite que você toowork visualmente com dados de armazenamento do Azure no Linux, Windows e macOS.
* [SDK do Azure para repositório Ruby](http://github.com/WindowsAzure/azure-sdk-for-ruby) no GitHub

