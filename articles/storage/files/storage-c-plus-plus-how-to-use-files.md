---
title: aaaDevelop para armazenamento de arquivo do Azure com C++ | Microsoft Docs
description: "Saiba como toodevelop C++ de aplicativos e serviços que usam toostore de armazenamento do Azure arquivo dados de arquivos."
services: storage
documentationcenter: .net
author: renashahmsft
manager: aungoo
editor: tysonn
ms.assetid: a1e8c99e-47a6-43a9-9541-c9262eb00b38
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/27/2017
ms.author: renashahmsft
ms.openlocfilehash: 48f668cf9359f88baeaaa08ee0d44e70bd0f5f1a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="develop-for-azure-file-storage-with-c"></a>Desenvolvimento para o Armazenamento de Arquivos do Azure com o C++
[!INCLUDE [storage-selector-file-include](../../../includes/storage-selector-file-include.md)]

[!INCLUDE [storage-try-azure-tools-files](../../../includes/storage-try-azure-tools-files.md)]

## <a name="about-this-tutorial"></a>Sobre este tutorial

Neste tutorial, você aprenderá como operações básicas de tooperform no armazenamento de arquivo do Azure. Por meio de exemplos escritos em C++, você aprenderá como toocreate compartilhamentos e diretórios, carregar, listar e excluir arquivos. Se você for novo armazenamento de arquivo tooAzure, passando por conceitos Olá Olá próximas seções será útil na compreensão exemplos hello.


* Criar e excluir Compartilhamentos de Arquivos do Azure
* Criar e excluir diretórios
* Enumerar arquivos e diretórios em um Compartilhamento de Arquivos do Azure
* Carregar, baixar e excluir um arquivo
* Definir uma cota de saudação (tamanho máximo) para um compartilhamento de arquivos do Azure
* Crie uma assinatura de acesso compartilhado (chave SAS) para um arquivo que usa uma política de acesso compartilhado definida no compartilhamento de saudação.

> [!Note]  
> Como armazenamento de arquivo do Azure pode ser acessado via SMB, é possível toowrite aplicativos simples que acessar o compartilhamento de arquivo do Azure hello usando funções e classes de e/s de C++ padrão hello. Este artigo descreve como toowrite os aplicativos que usam Olá SDK de C++ de armazenamento do Azure, que usa Olá [armazenamento de arquivo do Azure API REST](https://docs.microsoft.com/rest/api/storageservices/fileservices/file-service-rest-api) tootalk tooAzure o armazenamento de arquivos.

## <a name="create-a-c-application"></a>Criar um aplicativo em C++
exemplos de saudação toobuild, você precisará Olá tooinstall 2.4.0 de biblioteca de cliente de armazenamento do Azure para C++. Você também deverá ter criado uma conta de armazenamento do Azure.

Olá tooinstall 2.4.0 do cliente de armazenamento do Azure para C++, você pode usar um dos métodos a seguir de saudação:

* **Linux:** siga instruções Olá fornecidas em Olá [biblioteca de cliente de armazenamento do Azure para C++ Leiame](https://github.com/Azure/azure-storage-cpp/blob/master/README.md) página.
* **Windows:** no Visual Studio, clique em **Ferramentas &gt; Gerenciador de Pacotes do NuGet &gt; Console do Gerenciador de Pacotes**. Digite o seguinte Olá comando em Olá [NuGet Package Manager console](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) e pressione **ENTER**.
  
```
Install-Package wastorage
```

## <a name="set-up-your-application-toouse-azure-file-storage"></a>Configurar seu aplicativo toouse armazenamento de arquivo do Azure
Adicione a seguinte Olá incluem superior de toohello instruções Olá C++ do arquivo de origem em que você deseja que o armazenamento de arquivo do Azure toomanipulate:

```cpp
#include <was/storage_account.h>
#include <was/file.h>
```

## <a name="set-up-an-azure-storage-connection-string"></a>Configurar uma cadeia de conexão de armazenamento do Azure
toouse o armazenamento de arquivos, você precisa de conta de armazenamento do Azure de tooyour tooconnect. Olá primeira etapa seria tooconfigure uma cadeia de conexão, que vamos usar conta de armazenamento do tooconnect tooyour. Vamos definir uma toodo variável estática que.

```cpp
// Define hello connection-string with your values.
const utility::string_t 
storage_connection_string(U("DefaultEndpointsProtocol=https;AccountName=your_storage_account;AccountKey=your_storage_account_key"));
```

## <a name="connecting-tooan-azure-storage-account"></a>Conectar-se a conta de armazenamento do Azure tooan
Você pode usar o hello **cloud_storage_account** classe toorepresent suas informações de conta de armazenamento. tooretrieve informações de cadeia de caracteres de conexão de armazenamento Olá da conta de armazenamento, você pode usar o hello **analisar** método.

```cpp
// Retrieve storage account from connection string.    
azure::storage::cloud_storage_account storage_account = 
  azure::storage::cloud_storage_account::parse(storage_connection_string);
```

## <a name="create-an-azure-file-share"></a>Criar um Compartilhamento de Arquivos do Azure
Todos os arquivos e diretórios do Armazenamento de Arquivos do Azure residem em um contêiner chamado **Compartilhamento**. Sua conta de armazenamento pode a quantidade de compartilhamentos que a capacidade da conta permitir. compartilhamento de tooa tooobtain acesso e seu conteúdo, você precisa toouse um cliente de armazenamento do arquivo do Azure.

```cpp
// Create hello Azure File storage client.
azure::storage::cloud_file_client file_client = 
  storage_account.create_cloud_file_client();
```

Usando o cliente de armazenamento do Azure arquivo hello, em seguida, você pode obter um compartilhamento de tooa de referência.

```cpp
// Get a reference toohello file share
azure::storage::cloud_file_share share = 
  file_client.get_share_reference(_XPLATSTR("my-sample-share"));
```

compartilhamento de saudação toocreate, use Olá **create_if_not_exists** método hello **cloud_file_share** objeto.

```cpp
if (share.create_if_not_exists()) {    
    std::wcout << U("New share created") << std::endl;    
}
```

Neste ponto, **compartilhar** contém um compartilhamento de tooa de referência chamado **compartilhamento meu exemplo**.

## <a name="delete-an-azure-file-share"></a>Excluir um Compartilhamento de Arquivos do Azure
Excluir um compartilhamento é feito através da chamada hello **delete_if_exists** método em um objeto cloud_file_share. O código fornecido a seguir é um exemplo de como fazer isso.

```cpp
// Get a reference toohello share.
azure::storage::cloud_file_share share = 
  file_client.get_share_reference(_XPLATSTR("my-sample-share"));

// delete hello share if exists
share.delete_share_if_exists();
```

## <a name="create-a-directory"></a>Criar um diretório
Você pode organizar o armazenamento, colocando arquivos em subpastas em vez de ter todos eles no diretório raiz de saudação. Armazenamento de arquivo do Azure permite que você toocreate como permitir que vários diretórios como será sua conta. saudação de código abaixo cria um diretório chamado **meu diretório de exemplo** sob diretório raiz de hello, bem como uma subpasta chamada **meu subdiretório de exemplo**.

```cpp
// Retrieve a reference tooa directory
azure::storage::cloud_file_directory directory = share.get_directory_reference(_XPLATSTR("my-sample-directory"));

// Return value is true if hello share did not exist and was successfully created.
directory.create_if_not_exists();

// Create a subdirectory.
azure::storage::cloud_file_directory subdirectory = 
  directory.get_subdirectory_reference(_XPLATSTR("my-sample-subdirectory"));
subdirectory.create_if_not_exists();
```

## <a name="delete-a-directory"></a>Excluir um diretório
Excluir um diretório é uma tarefa simples, embora deva-se observar que não é possível excluir um diretório que ainda contenha arquivos ou outros diretórios.

```cpp
// Get a reference toohello share.
azure::storage::cloud_file_share share = 
  file_client.get_share_reference(_XPLATSTR("my-sample-share"));

// Get a reference toohello directory.
azure::storage::cloud_file_directory directory = 
  share.get_directory_reference(_XPLATSTR("my-sample-directory"));

// Get a reference toohello subdirectory you want toodelete.
azure::storage::cloud_file_directory sub_directory =
  directory.get_subdirectory_reference(_XPLATSTR("my-sample-subdirectory"));

// Delete hello subdirectory and hello sample directory.
sub_directory.delete_directory_if_exists();

directory.delete_directory_if_exists();
```

## <a name="enumerate-files-and-directories-in-an-azure-file-share"></a>Enumerar arquivos e diretórios em um Compartilhamento de Arquivos do Azure
A lista de arquivos e diretórios em um compartilhamento pode ser obtida facilmente chamando **list_files_and_directories** em uma referência **cloud_file_directory**. tooaccess Olá rico conjunto de propriedades e métodos para uma retornado **list_file_and_directory_item**, você deve chamar hello **list_file_and_directory_item.as_file** método tooget um **cloud_ arquivo** objeto ou hello **list_file_and_directory_item.as_directory** método tooget um **cloud_file_directory** objeto.

saudação de código a seguir demonstra como tooretrieve e saída Olá URI de cada item no diretório raiz de saudação do compartilhamento de saudação.

```cpp
//Get a reference toohello root directory for hello share.
azure::storage::cloud_file_directory root_dir = 
  share.get_root_directory_reference();

// Output URI of each item.
azure::storage::list_file_and_diretory_result_iterator end_of_results;

for (auto it = directory.list_files_and_directories(); it != end_of_results; ++it)
{
    if(it->is_directory())
    {
        ucout << "Directory: " << it->as_directory().uri().primary_uri().to_string() << std::endl;
    }
    else if (it->is_file())
    {
        ucout << "File: " << it->as_file().uri().primary_uri().to_string() << std::endl;
    }        
}
```

## <a name="upload-a-file"></a>Carregar um arquivo
No hello muito menos, um compartilhamento de arquivos do Azure contém um diretório raiz onde os arquivos podem residir. Nesta seção, você aprenderá como o diretório de um compartilhamento de raiz tooupload um arquivo do armazenamento local para hello.

a primeira etapa Olá no carregamento de um arquivo é tooobtain um diretório de toohello de referência em que ele deve residir. Para fazer isso, Olá chamada **get_root_directory_reference** método do objeto de compartilhamento de saudação.

```cpp
//Get a reference toohello root directory for hello share.
azure::storage::cloud_file_directory root_dir = share.get_root_directory_reference();
```

Agora que você tem um diretório de raiz de toohello de referência do compartilhamento hello, você pode carregar um arquivo para ele. Este exemplo carrega de um arquivo, de um texto e de um fluxo.

```cpp
// Upload a file from a stream.
concurrency::streams::istream input_stream = 
  concurrency::streams::file_stream<uint8_t>::open_istream(_XPLATSTR("DataFile.txt")).get();

azure::storage::cloud_file file1 = 
  root_dir.get_file_reference(_XPLATSTR("my-sample-file-1"));
file1.upload_from_stream(input_stream);

// Upload some files from text.
azure::storage::cloud_file file2 = 
  root_dir.get_file_reference(_XPLATSTR("my-sample-file-2"));
file2.upload_text(_XPLATSTR("more text"));

// Upload a file from a file.
azure::storage::cloud_file file4 = 
  root_dir.get_file_reference(_XPLATSTR("my-sample-file-3"));
file4.upload_from_file(_XPLATSTR("DataFile.txt"));    
```

## <a name="download-a-file"></a>Baixar um arquivo
arquivos toodownload, recuperar uma referência de arquivo e, em seguida, chamar hello **download_to_stream** método tootransfer Olá arquivo conteúdo tooa objeto de fluxo, que, em seguida, você pode manter arquivo local tooa. Como alternativa, você pode usar o hello **download_to_file** conteúdo de saudação do método toodownload um arquivo local tooa. Você pode usar o hello **download_text** conteúdo de saudação do método toodownload de um arquivo como uma cadeia de caracteres de texto.

Olá, exemplo a seguir usa Olá **download_to_stream** e **download_text** toodemonstrate métodos baixando arquivos hello, que foram criados nas seções anteriores.

```cpp
// Download as text
azure::storage::cloud_file text_file = 
  root_dir.get_file_reference(_XPLATSTR("my-sample-file-2"));
utility::string_t text = text_file.download_text();
ucout << "File Text: " << text << std::endl;

// Download as a stream.
azure::storage::cloud_file stream_file = 
  root_dir.get_file_reference(_XPLATSTR("my-sample-file-3"));

concurrency::streams::container_buffer<std::vector<uint8_t>> buffer;
concurrency::streams::ostream output_stream(buffer);
stream_file.download_to_stream(output_stream);
std::ofstream outfile("DownloadFile.txt", std::ofstream::binary);
std::vector<unsigned char>& data = buffer.collection();
outfile.write((char *)&data[0], buffer.size());
outfile.close();
```

## <a name="delete-a-file"></a>Excluir um arquivo
Outra operação comum do Armazenamento de Arquivos do Azure é a exclusão de arquivos. Olá código a seguir exclui um arquivo chamado Meu-exemplo-arquivo-3 armazenados no diretório raiz de saudação.

```cpp
// Get a reference toohello root directory for hello share.    
azure::storage::cloud_file_share share = 
  file_client.get_share_reference(_XPLATSTR("my-sample-share"));

azure::storage::cloud_file_directory root_dir = 
  share.get_root_directory_reference();

azure::storage::cloud_file file = 
  root_dir.get_file_reference(_XPLATSTR("my-sample-file-3"));

file.delete_file_if_exists();
```

## <a name="set-hello-quota-maximum-size-for-an-azure-file-share"></a>Definir uma cota de saudação (tamanho máximo) para um compartilhamento de arquivos do Azure
Você pode definir cotas de hello (ou o tamanho máximo) para um compartilhamento de arquivo, em gigabytes. Você também pode verificar toosee a quantidade de dados é atualmente armazenado no compartilhamento de saudação.

Pela configuração cota Olá para um compartilhamento, você pode limitar o tamanho total de Olá Olá arquivos armazenados no compartilhamento de saudação. Se excede o tamanho total de saudação de arquivos no compartilhamento de saudação cota Olá definidos no compartilhamento de saudação, os clientes serão tooincrease não é possível Olá tamanho dos arquivos existentes ou criar novos arquivos, a menos que esses arquivos estão vazios.

exemplo Hello abaixo mostra como toocheck Olá uso atual para um compartilhamento e como tooset Olá cota para compartilhamento de saudação.

```cpp
// Parse hello connection string for hello storage account.
azure::storage::cloud_storage_account storage_account = 
  azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello file client.
azure::storage::cloud_file_client file_client = 
  storage_account.create_cloud_file_client();

// Get a reference toohello share.
azure::storage::cloud_file_share share = 
  file_client.get_share_reference(_XPLATSTR("my-sample-share"));
if (share.exists())
{
    std::cout << "Current share usage: " << share.download_share_usage() << "/" << share.properties().quota();

    //This line sets hello quota too2560GB
    share.resize(2560);

    std::cout << "Quota increased: " << share.download_share_usage() << "/" << share.properties().quota();

}
```

## <a name="generate-a-shared-access-signature-for-a-file-or-file-share"></a>Gerar uma assinatura de acesso compartilhado para um arquivo ou compartilhamento de arquivos
Você pode gerar uma SAS (assinatura de acesso compartilhado) para um compartilhamento de arquivo ou para um arquivo individual. Você pode também criar uma política de acesso compartilhado um acesso de toomanage compartilhado de compartilhamento de arquivo assinaturas. Criar uma política de acesso compartilhado é recomendada, pois ele fornece um meio de revogar Olá SAS se ela deve ser comprometida.

saudação de exemplo a seguir cria uma política de acesso compartilhado em um compartilhamento e usa que compartilham tooprovide Olá restrições para uma SAS em um arquivo hello.

```cpp
// Parse hello connection string for hello storage account.
azure::storage::cloud_storage_account storage_account = 
  azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello file client and get a reference toohello share
azure::storage::cloud_file_client file_client = 
  storage_account.create_cloud_file_client();

azure::storage::cloud_file_share share = 
  file_client.get_share_reference(_XPLATSTR("my-sample-share"));

if (share.exists())
{
    // Create and assign a policy
    utility::string_t policy_name = _XPLATSTR("sampleSharePolicy");

    azure::storage::file_shared_access_policy sharedPolicy = 
      azure::storage::file_shared_access_policy();

    //set permissions tooexpire in 90 minutes
    sharedPolicy.set_expiry(utility::datetime::utc_now() + 
       utility::datetime::from_minutes(90));

    //give read and write permissions
    sharedPolicy.set_permissions(azure::storage::file_shared_access_policy::permissions::write | azure::storage::file_shared_access_policy::permissions::read);

    //set permissions for hello share
    azure::storage::file_share_permissions permissions;    

    //retrieve hello current list of shared access policies
    azure::storage::shared_access_policies<azure::storage::file_shared_access_policy> policies;

    //add hello new shared policy
    policies.insert(std::make_pair(policy_name, sharedPolicy));

    //save hello updated policy list
    permissions.set_policies(policies);
    share.upload_permissions(permissions);

    //Retrieve hello root directory and file references
    azure::storage::cloud_file_directory root_dir = 
        share.get_root_directory_reference();
    azure::storage::cloud_file file = 
      root_dir.get_file_reference(_XPLATSTR("my-sample-file-1"));

    // Generate a SAS for a file in hello share 
    //  and associate this access policy with it.        
    utility::string_t sas_token = file.get_shared_access_signature(sharedPolicy);

    // Create a new CloudFile object from hello SAS, and write some text toohello file.        
    azure::storage::cloud_file file_with_sas(azure::storage::storage_credentials(sas_token).transform_uri(file.uri().primary_uri()));
    utility::string_t text = _XPLATSTR("My sample content");        
    file_with_sas.upload_text(text);        

    //Download and print URL with SAS.
    utility::string_t downloaded_text = file_with_sas.download_text();        
    ucout << downloaded_text << std::endl;        
    ucout << azure::storage::storage_credentials(sas_token).transform_uri(file.uri().primary_uri()).to_string() << std::endl;

}
```
## <a name="next-steps"></a>Próximas etapas
toolearn mais sobre o armazenamento do Azure, explore esses recursos:

* [Biblioteca do Cliente de Armazenamento para C++](https://github.com/Azure/azure-storage-cpp)
* [Exemplos de Serviço de Arquivo do Armazenamento do Azure no C++] (https://github.com/Azure-Samples/storage-file-cpp-getting-started)
* [Gerenciador de Armazenamento do Azure](http://go.microsoft.com/fwlink/?LinkID=822673&clcid=0x409)
* [Documentação do Armazenamento do Azure](https://azure.microsoft.com/documentation/services/storage/)