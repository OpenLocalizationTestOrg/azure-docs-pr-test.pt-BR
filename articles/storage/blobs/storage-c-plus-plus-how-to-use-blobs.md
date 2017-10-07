---
title: armazenamento de blob aaaHow toouse (armazenamento de objeto) de C++ | Microsoft Docs
description: "Armazene dados não estruturados em nuvem Olá com armazenamento de BLOBs do Azure (armazenamento de objeto)."
services: storage
documentationcenter: .net
author: michaelhauss
manager: vamshik
editor: tysonn
ms.assetid: 53844120-1c48-4e2f-8f77-5359ed0147a4
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/11/2017
ms.author: michaelhauss
ms.openlocfilehash: e63df4683e5c10c9f8fbe4106c655df61be0e1a6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-blob-storage-from-c"></a>Como toouse armazenamento de Blob de C++
[!INCLUDE [storage-selector-blob-include](../../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-try-azure-tools-blobs](../../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a>Visão geral
Armazenamento de BLOBs do Azure é um serviço que armazena dados não estruturados em nuvem hello como objetos/blobs. O Armazenamento de Blobs pode conter qualquer tipo de texto ou de dados binários, como um documento, um arquivo de mídia ou um instalador de aplicativo. Armazenamento de blob também é chamado tooas armazenamento de objeto.

Este guia demonstra como os cenários comuns de tooperform usando Olá serviço de armazenamento de BLOBs do Azure. exemplos de saudação são escritos em C++ e usam Olá [biblioteca de cliente de armazenamento do Azure para C++](http://github.com/Azure/azure-storage-cpp/blob/master/README.md). Olá cenários abordados incluem **Carregando**, **listando**, **baixando**, e **excluindo** blobs.  

> [!NOTE]
> Destino dessa guia Olá biblioteca de cliente de armazenamento do Azure para a versão 1.0.0 de C++ e acima. Olá recomendado versão é a biblioteca de cliente de armazenamento 2.2.0, que está disponível por meio de [NuGet](http://www.nuget.org/packages/wastorage) ou [GitHub](https://github.com/Azure/azure-storage-cpp).
> 
> 

[!INCLUDE [storage-blob-concepts-include](../../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

## <a name="create-a-c-application"></a>Criar um aplicativo em C++
Neste guia, você usará os recursos de armazenamento que podem ser executados em um aplicativo C++.  

toodo assim, você precisará tooinstall hello biblioteca de cliente de armazenamento do Azure para C++ e criar uma conta de armazenamento do Azure em sua assinatura do Azure.   

Olá tooinstall biblioteca de cliente de armazenamento do Azure para C++, você pode usar o hello métodos a seguir:

* **Linux:** siga instruções Olá fornecidas em Olá [biblioteca de cliente de armazenamento do Azure para C++ Leiame](https://github.com/Azure/azure-storage-cpp/blob/master/README.md) página.  
* **Windows:** no Visual Studio, clique em **Ferramentas > Gerenciador de Pacotes do NuGet > Console do Gerenciador de Pacotes**. Digite o seguinte Olá comando em Olá [NuGet Package Manager console](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) e pressione **ENTER**.  
  
     Install-Package wastorage

## <a name="configure-your-application-tooaccess-blob-storage"></a>Configurar seu aplicativo tooaccess armazenamento de Blob
Adicione a seguinte Olá incluem superior de toohello de instruções do arquivo de C++ de saudação onde você deseja toouse Olá armazenamento do Azure APIs tooaccess blobs:  

```cpp
#include <was/storage_account.h>
#include <was/blob.h>
```

## <a name="setup-an-azure-storage-connection-string"></a>Configurar uma cadeia de conexão de armazenamento do Azure
Um cliente de armazenamento do Azure usa um pontos de extremidade de toostore de cadeia de caracteres de conexão de armazenamento e as credenciais para acessar os serviços de gerenciamento de dados. Quando em execução em um aplicativo cliente, você deve fornecer a cadeia de conexão de armazenamento Olá no hello formato a seguir, usando o nome de saudação da chave de acesso do armazenamento seu armazenamento conta e Olá Olá conta de armazenamento listada no hello [Portal do Azure](https://portal.azure.com)para Olá *AccountName* e *AccountKey* valores. Para obter informações sobre as contas de armazenamento e as chaves de acesso, consulte [Sobre as Contas de Armazenamento do Azure](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json). Este exemplo mostra como você pode declarar uma cadeia de caracteres de conexão do campo estático toohold hello:  

```cpp
// Define hello connection-string with your values.
const utility::string_t storage_connection_string(U("DefaultEndpointsProtocol=https;AccountName=your_storage_account;AccountKey=your_storage_account_key"));
```

tootest seu aplicativo no seu computador local do Windows, você pode usar o hello Microsoft Azure [emulador de armazenamento](../storage-use-emulator.md) que é instalada com hello [SDK do Azure](https://azure.microsoft.com/downloads/). emulador de armazenamento Olá é um utilitário que simula os serviços de Blob, fila e tabela de saudação disponíveis no Azure em sua máquina de desenvolvimento local. Olá exemplo a seguir mostra como você pode declarar um emulador de armazenamento local do campo estático toohold Olá cadeia de caracteres conexão tooyour:

```cpp
// Define hello connection-string with Azure Storage Emulator.
const utility::string_t storage_connection_string(U("UseDevelopmentStorage=true;"));  
```

emulador de armazenamento do Azure toostart hello, selecione Olá **iniciar** Olá botão ou pressione **Windows** chave. Comece digitando **emulador de armazenamento do Azure**e selecione **emulador de armazenamento do Microsoft Azure** da lista de saudação de aplicativos.  

Olá exemplos a seguir pressupõem que você usou uma cadeia de conexão de armazenamento esses dois métodos tooget hello.  

## <a name="retrieve-your-connection-string"></a>Recuperar sua cadeia de conexão
Você pode usar o hello **cloud_storage_account** classe toorepresent suas informações de conta de armazenamento. tooretrieve informações de cadeia de caracteres de conexão de armazenamento Olá da conta de armazenamento, você pode usar o hello **analisar** método.  

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);
```

Em seguida, obtenha uma referência tooa **cloud_blob_client** classe que permite a você tooretrieve objetos que representam os contêineres e blobs armazenados em Olá serviço de armazenamento de Blob. Olá código a seguir cria um **cloud_blob_client** objeto usando o objeto de conta de armazenamento Olá recuperamos acima:  

```cpp
// Create hello blob client.
azure::storage::cloud_blob_client blob_client = storage_account.create_cloud_blob_client();  
```

## <a name="how-to-create-a-container"></a>Como criar um contêiner
[!INCLUDE [storage-container-naming-rules-include](../../../includes/storage-container-naming-rules-include.md)]

Este exemplo mostra como toocreate um contêiner se ele ainda não existir:  

```cpp
try
{
    // Retrieve storage account from connection string.
    azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

    // Create hello blob client.
    azure::storage::cloud_blob_client blob_client = storage_account.create_cloud_blob_client();

    // Retrieve a reference tooa container.
    azure::storage::cloud_blob_container container = blob_client.get_container_reference(U("my-sample-container"));

    // Create hello container if it doesn't already exist.
    container.create_if_not_exists();
}
catch (const std::exception& e)
{
    std::wcout << U("Error: ") << e.what() << std::endl;
}  
```

Por padrão, novo contêiner de saudação é privado e você deve especificar seus blobs de toodownload chave de acesso de armazenamento desse contêiner. Toomake Olá arquivos se (blobs) em Olá contêiner disponível tooeveryone, você pode definir Olá contêiner toobe pública usando Olá código a seguir:  

```cpp
// Make hello blob container publicly accessible.
azure::storage::blob_container_permissions permissions;
permissions.set_public_access(azure::storage::blob_container_public_access_type::blob);
container.upload_permissions(permissions);  
```

Qualquer pessoa na Internet de saudação pode ver os blobs em um contêiner público, mas você pode modificar ou excluí-los somente se você tiver a chave de acesso apropriadas de saudação.  

## <a name="how-to-upload-a-blob-into-a-container"></a>Como: carregar um blob em um contêiner
O Armazenamento de Blob do Azure oferece suporte a blobs de blocos e a blobs de páginas. Na maioria Olá dos casos, blob de blocos é hello recomendado toouse de tipo.  

tooupload um blob de blocos de tooa de arquivo, obtenha uma referência de contêiner e usá-lo tooget uma referência de blob de bloco. Quando você tem uma referência de blob, você pode carregar qualquer fluxo de dados tooit Olá chamada **upload_from_stream** método. Esta operação criará blob Olá se ele anteriormente não existe ou substituí-lo se ele existir. Olá mostrado no exemplo a seguir como tooupload um blob em um contêiner e supõe que esse contêiner Olá já foi criado.  

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello blob client.
azure::storage::cloud_blob_client blob_client = storage_account.create_cloud_blob_client();

// Retrieve a reference tooa previously created container.
azure::storage::cloud_blob_container container = blob_client.get_container_reference(U("my-sample-container"));

// Retrieve reference tooa blob named "my-blob-1".
azure::storage::cloud_block_blob blockBlob = container.get_block_blob_reference(U("my-blob-1"));

// Create or overwrite hello "my-blob-1" blob with contents from a local file.
concurrency::streams::istream input_stream = concurrency::streams::file_stream<uint8_t>::open_istream(U("DataFile.txt")).get();
blockBlob.upload_from_stream(input_stream);
input_stream.close().wait();

// Create or overwrite hello "my-blob-2" and "my-blob-3" blobs with contents from text.
// Retrieve a reference tooa blob named "my-blob-2".
azure::storage::cloud_block_blob blob2 = container.get_block_blob_reference(U("my-blob-2"));
blob2.upload_text(U("more text"));

// Retrieve a reference tooa blob named "my-blob-3".
azure::storage::cloud_block_blob blob3 = container.get_block_blob_reference(U("my-directory/my-sub-directory/my-blob-3"));
blob3.upload_text(U("other text"));  
```

Como alternativa, você pode usar o hello **upload_from_file** tooupload método um blob de blocos de tooa do arquivo.

## <a name="how-to-list-hello-blobs-in-a-container"></a>Como: lista Olá blobs em um contêiner
blobs de saudação toolist em um contêiner, primeiro obtenha uma referência de contêiner. Você pode usar do contêiner Olá **list_blobs** blobs de saudação do método tooretrieve e/ou diretórios dentro dele. tooaccess Olá rico conjunto de propriedades e métodos para uma retornado **list_blob_item**, você deve chamar hello **list_blob_item.as_blob** método tooget um **cloud_blob** objeto, ou hello **list_blob.as_directory** método tooget um objeto cloud_blob_directory. Olá código a seguir demonstra como tooretrieve e saída Olá URI de cada item em Olá **meu contêiner de exemplo** contêiner:

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello blob client.
azure::storage::cloud_blob_client blob_client = storage_account.create_cloud_blob_client();

// Retrieve a reference tooa previously created container.
azure::storage::cloud_blob_container container = blob_client.get_container_reference(U("my-sample-container"));

// Output URI of each item.
azure::storage::list_blob_item_iterator end_of_results;
for (auto it = container.list_blobs(); it != end_of_results; ++it)
{
    if (it->is_blob())
    {
        std::wcout << U("Blob: ") << it->as_blob().uri().primary_uri().to_string() << std::endl;
    }
    else
    {
        std::wcout << U("Directory: ") << it->as_directory().uri().primary_uri().to_string() << std::endl;
    }
}
```

Para obter mais detalhes sobre a lista de operações, consulte [Listar recursos de Armazenamento do Azure em C++](../storage-c-plus-plus-enumeration.md).

## <a name="how-to-download-blobs"></a>Como: baixar blobs
blobs toodownload, recuperar uma referência de blob e, em seguida, chamar hello **download_to_stream** método. Olá, exemplo a seguir usa Olá **download_to_stream** método tootransfer Olá conteúdo tooa fluxo objeto blob que, em seguida, você pode persistir o arquivo local tooa.  

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello blob client.
azure::storage::cloud_blob_client blob_client = storage_account.create_cloud_blob_client();

// Retrieve a reference tooa previously created container.
azure::storage::cloud_blob_container container = blob_client.get_container_reference(U("my-sample-container"));

// Retrieve reference tooa blob named "my-blob-1".
azure::storage::cloud_block_blob blockBlob = container.get_block_blob_reference(U("my-blob-1"));

// Save blob contents tooa file.
concurrency::streams::container_buffer<std::vector<uint8_t>> buffer;
concurrency::streams::ostream output_stream(buffer);
blockBlob.download_to_stream(output_stream);

std::ofstream outfile("DownloadBlobFile.txt", std::ofstream::binary);
std::vector<unsigned char>& data = buffer.collection();

outfile.write((char *)&data[0], buffer.size());
outfile.close();  
```

Como alternativa, você pode usar o hello **download_to_file** conteúdo de saudação do método toodownload um tooa do arquivo de blob.
Além disso, você também pode usar Olá **download_text** conteúdo de saudação do método toodownload de um blob como uma cadeia de caracteres de texto.  

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello blob client.
azure::storage::cloud_blob_client blob_client = storage_account.create_cloud_blob_client();

// Retrieve a reference tooa previously created container.
azure::storage::cloud_blob_container container = blob_client.get_container_reference(U("my-sample-container"));

// Retrieve reference tooa blob named "my-blob-2".
azure::storage::cloud_block_blob text_blob = container.get_block_blob_reference(U("my-blob-2"));

// Download hello contents of a blog as a text string.
utility::string_t text = text_blob.download_text();
```

## <a name="how-to-delete-blobs"></a>Como: excluir blobs
toodelete um blob, primeiro obter uma referência de blob e, em seguida, chamar hello **delete_blob** método nele.  

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello blob client.
azure::storage::cloud_blob_client blob_client = storage_account.create_cloud_blob_client();

// Retrieve a reference tooa previously created container.
azure::storage::cloud_blob_container container = blob_client.get_container_reference(U("my-sample-container"));

// Retrieve reference tooa blob named "my-blob-1".
azure::storage::cloud_block_blob blockBlob = container.get_block_blob_reference(U("my-blob-1"));

// Delete hello blob.
blockBlob.delete_blob();
```

## <a name="next-steps"></a>Próximas etapas
Agora que você aprendeu as Noções básicas de saudação do armazenamento de blob, siga essas toolearn links mais sobre o armazenamento do Azure.  

* [Como toouse armazenamento de fila de C++](../storage-c-plus-plus-how-to-use-queues.md)
* [Como toouse o armazenamento de tabela do C++](../../cosmos-db/table-storage-how-to-use-c-plus.md)
* [Listar recursos de Armazenamento do Azure em C++](../storage-c-plus-plus-enumeration.md)
* [Referência da Biblioteca de Cliente de Armazenamento para C++](http://azure.github.io/azure-storage-cpp)
* [Documentação do Armazenamento do Azure](https://azure.microsoft.com/documentation/services/storage/)
* [Transferência de dados com hello AzCopy utilitário de linha de comando](../storage-use-azcopy.md)

