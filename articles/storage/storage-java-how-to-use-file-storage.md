---
title: aaaDevelop para armazenamento de arquivo do Azure com Java | Microsoft Docs
description: "Saiba como aplicativos do Java toodevelop e serviços que usam toostore de armazenamento do Azure arquivo dados de arquivos."
services: storage
documentationcenter: java
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 3bfbfa7f-d378-4fb4-8df3-e0b6fcea5b27
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 05/27/2017
ms.author: robinsh
ms.openlocfilehash: b50703815daf2c829e7e9a9a4196c31a2b8727e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="develop-for-azure-file-storage-with-java"></a>Desenvolvimento para o Armazenamento de Arquivos do Azure com Java
[!INCLUDE [storage-selector-file-include](../../includes/storage-selector-file-include.md)]

[!INCLUDE [storage-check-out-samples-java](../../includes/storage-check-out-samples-java.md)]

## <a name="about-this-tutorial"></a>Sobre este tutorial
Este tutorial demonstra Noções básicas de saudação do uso de aplicativos do Java toodevelop ou serviços que usam dados de arquivo de toostore de armazenamento de arquivo do Azure. Neste tutorial, vamos criar um aplicativo de console simples e mostram como ações básicas de tooperform com armazenamento de Java e o arquivo do Azure:

* Criar e excluir Compartilhamentos de Arquivos do Azure
* Criar e excluir diretórios
* Enumerar arquivos e diretórios em um Compartilhamento de Arquivos do Azure
* Carregar, baixar e excluir um arquivo

> [!Note]  
> Como armazenamento de arquivo do Azure pode ser acessado via SMB, é possível toowrite aplicativos simples que acessar o compartilhamento de arquivo do Azure hello usando classes de e/s de Java padrão hello. Este artigo descreve como aplicativos toowrite que usam Olá SDK de Java do armazenamento do Azure, que usa Olá [armazenamento de arquivo do Azure API REST](https://docs.microsoft.com/rest/api/storageservices/fileservices/file-service-rest-api) tootalk tooAzure o armazenamento de arquivos.

## <a name="create-a-java-application"></a>Criar um aplicativo Java
exemplos de saudação toobuild, será necessário hello Java Development Kit (JDK) e [Olá [SDK do armazenamento do Azure para Java]]. Você também deverá ter criado uma conta de armazenamento do Azure.

## <a name="setup-your-application-toouse-azure-file-storage"></a>Configurar seu aplicativo toouse armazenamento de arquivo do Azure
Olá toouse APIs, o armazenamento do Azure adicionar Olá superior de toohello instrução saudação do arquivo de Java em que você pretende tooaccess serviço de armazenamento de saudação da seguir.

```java
// Include hello following imports toouse blob APIs.
import com.microsoft.azure.storage.*;
import com.microsoft.azure.storage.file.*;
```

## <a name="setup-an-azure-storage-connection-string"></a>Configurar uma cadeia de conexão de armazenamento do Azure
toouse armazenamento de arquivo do Azure, você precisa de conta de armazenamento do Azure de tooyour tooconnect. Olá primeira etapa seria tooconfigure uma cadeia de caracteres de conexão que vamos usar conta de armazenamento do tooconnect tooyour. Vamos definir uma toodo variável estática que.

```java
// Configure hello connection-string with your values
public static final String storageConnectionString =
    "DefaultEndpointsProtocol=http;" +
    "AccountName=your_storage_account_name;" +
    "AccountKey=your_storage_account_key";
```

> [!NOTE]
> Substitua your_storage_account_name e your_storage_account_key por valores reais de saudação para sua conta de armazenamento.
> 
> 

## <a name="connecting-tooan-azure-storage-account"></a>Conectar-se a conta de armazenamento do Azure tooan
conta de armazenamento do tooconnect tooyour, você precisa Olá toouse **CloudStorageAccount** um tooits de cadeia de caracteres de conexão de passagem do objeto **analisar** método.

```java
// Use hello CloudStorageAccount object tooconnect tooyour storage account
try {
    CloudStorageAccount storageAccount = CloudStorageAccount.parse(storageConnectionString);
} catch (InvalidKeyException invalidKey) {
    // Handle hello exception
}
```

**CloudStorageAccount.parse** gera um InvalidKeyException, portanto, você precisará tooput dentro de um bloco try/catch bloquear.

## <a name="create-an-azure-file-share"></a>Criar um Compartilhamento de Arquivos do Azure
Todos os arquivos e diretórios do Armazenamento de Arquivos do Azure residem em um contêiner chamado **Compartilhamento**. Sua conta de armazenamento pode ter tantos compartilhamentos quantos a capacidade da conta permitir. compartilhamento de tooa tooobtain acesso e seu conteúdo, você precisa toouse um cliente de armazenamento do arquivo do Azure.

```java
// Create hello Azure File storage client.
CloudFileClient fileClient = storageAccount.createCloudFileClient();
```

Usando o cliente de armazenamento do Azure arquivo hello, em seguida, você pode obter um compartilhamento de tooa de referência.

```java
// Get a reference toohello file share
CloudFileShare share = fileClient.getShareReference("sampleshare");
```

tooactually criar compartilhamento de hello, use Olá **createIfNotExists** método do objeto de CloudFileShare hello.

```java
if (share.createIfNotExists()) {
    System.out.println("New share created");
}
```

Neste ponto, **compartilhar** contém um compartilhamento de tooa de referência chamado **sampleshare**.

## <a name="delete-an-azure-file-share"></a>Excluir um Compartilhamento de Arquivos do Azure
Excluir um compartilhamento é feito através da chamada hello **deleteIfExists** método em um objeto CloudFileShare. O código fornecido a seguir é um exemplo de como fazer isso.

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount = CloudStorageAccount.parse(storageConnectionString);

    // Create hello file client.
   CloudFileClient fileClient = storageAccount.createCloudFileClient();

   // Get a reference toohello file share
   CloudFileShare share = fileClient.getShareReference("sampleshare");

   if (share.deleteIfExists()) {
       System.out.println("sampleshare deleted");
   }
} catch (Exception e) {
    e.printStackTrace();
}
```

## <a name="create-a-directory"></a>Criar um diretório
Você também pode organizar o armazenamento, colocando arquivos nos subdiretórios em vez de ter todos eles no diretório raiz de saudação. Armazenamento de arquivo do Azure permite toocreate como permitem muito diretórios como será sua conta. saudação de código abaixo cria um subdiretório chamado **sampledir** no diretório raiz de saudação.

```java
//Get a reference toohello root directory for hello share.
CloudFileDirectory rootDir = share.getRootDirectoryReference();

//Get a reference toohello sampledir directory
CloudFileDirectory sampleDir = rootDir.getDirectoryReference("sampledir");

if (sampleDir.createIfNotExists()) {
    System.out.println("sampledir created");
} else {
    System.out.println("sampledir already exists");
}
```

## <a name="delete-a-directory"></a>Excluir um diretório
Excluir um diretório é uma tarefa bem simples, embora deva-se observar que não é possível excluir um diretório que ainda contenha arquivos ou outros diretórios.

```java
// Get a reference toohello root directory for hello share.
CloudFileDirectory rootDir = share.getRootDirectoryReference();

// Get a reference toohello directory you want toodelete
CloudFileDirectory containerDir = rootDir.getDirectoryReference("sampledir");

// Delete hello directory
if ( containerDir.deleteIfExists() ) {
    System.out.println("Directory deleted");
}
```

## <a name="enumerate-files-and-directories-in-an-azure-file-share"></a>Enumerar arquivos e diretórios em um Compartilhamento de Arquivos do Azure
A lista de arquivos e diretórios em um compartilhamento pode ser obtida facilmente chamando **listFilesAndDirectories** em uma referência CloudFileDirectory. método Hello retorna uma lista de objetos ListFileItem que você pode iterar em. Por exemplo, hello código a seguir lista arquivos e diretórios dentro do diretório raiz de saudação.

```java
//Get a reference toohello root directory for hello share.
CloudFileDirectory rootDir = share.getRootDirectoryReference();

for ( ListFileItem fileItem : rootDir.listFilesAndDirectories() ) {
    System.out.println(fileItem.getUri());
}
```

## <a name="upload-a-file"></a>Carregar um arquivo
Um arquivo Azure compartilhamento contém em Olá muito menos, um diretório raiz onde os arquivos podem residir. Nesta seção, você aprenderá como o diretório de um compartilhamento de raiz tooupload um arquivo do armazenamento local para hello.

a primeira etapa Olá no carregamento de um arquivo é tooobtain um diretório de toohello de referência em que ele deve residir. Para fazer isso, Olá chamada **getRootDirectoryReference** método do objeto de compartilhamento de saudação.

```java
//Get a reference toohello root directory for hello share.
CloudFileDirectory rootDir = share.getRootDirectoryReference();
```

Agora que você tem um diretório de raiz de toohello de referência do compartilhamento hello, você pode carregar um arquivo nele usando Olá código a seguir.

```java
        // Define hello path tooa local file.
        final String filePath = "C:\\temp\\Readme.txt";
    
        CloudFile cloudFile = rootDir.getFileReference("Readme.txt");
        cloudFile.uploadFromFile(filePath);
```

## <a name="download-a-file"></a>Baixar um arquivo
Uma saudação mais frequentam operações que serão executadas em relação ao armazenamento de arquivo do Azure é arquivos toodownload. No hello exemplo a seguir, o código de saudação downloads SampleFile.txt e exibe seu conteúdo.

```java
//Get a reference toohello root directory for hello share.
CloudFileDirectory rootDir = share.getRootDirectoryReference();

//Get a reference toohello directory that contains hello file
CloudFileDirectory sampleDir = rootDir.getDirectoryReference("sampledir");

//Get a reference toohello file you want toodownload
CloudFile file = sampleDir.getFileReference("SampleFile.txt");

//Write hello contents of hello file toohello console.
System.out.println(file.downloadText());
```

## <a name="delete-a-file"></a>Excluir um arquivo
Outra operação comum do Armazenamento de Arquivos do Azure é a exclusão de arquivos. Olá, código a seguir exclui um arquivo chamado SampleFile.txt armazenados dentro de um diretório chamado **sampledir**.

```java
// Get a reference toohello root directory for hello share.
CloudFileDirectory rootDir = share.getRootDirectoryReference();

// Get a reference toohello directory where hello file toobe deleted is in
CloudFileDirectory containerDir = rootDir.getDirectoryReference("sampledir");

String filename = "SampleFile.txt"
CloudFile file;

file = containerDir.getFileReference(filename)
if ( file.deleteIfExists() ) {
    System.out.println(filename + " was deleted");
}
```

## <a name="next-steps"></a>Próximas etapas
Se você quiser toolearn mais sobre outros APIs de armazenamento do Azure, siga estes links.

* [Central de Desenvolvedores do Java](http://azure.microsoft.com/develop/java/)
* [SDK de Armazenamento do Azure para Java](https://github.com/azure/azure-storage-java)
* [SDK de Armazenamento do Azure para Android](https://github.com/azure/azure-storage-android)
* [Referência de SDK do Cliente de Armazenamento do Azure](http://dl.windowsazure.com/storage/javadoc/)
* [API REST de serviços de armazenamento do Azure](https://msdn.microsoft.com/library/azure/dd179355.aspx)
* [Blog da equipe de Armazenamento do Azure](http://blogs.msdn.com/b/windowsazurestorage/)
* [Transferência de dados com hello AzCopy utilitário de linha de comando](storage-use-azcopy.md)
