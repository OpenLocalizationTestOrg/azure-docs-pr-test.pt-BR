---
title: aaaHow toouse o armazenamento de BLOBs do Azure (armazenamento de objeto) do Java | Microsoft Docs
description: "Armazene dados não estruturados em nuvem Olá com armazenamento de BLOBs do Azure (armazenamento de objeto)."
services: storage
documentationcenter: java
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: 2e223b38-92de-4c2f-9254-346374545d32
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: java
ms.topic: article
ms.date: 12/08/2016
ms.author: marsma
ms.openlocfilehash: a905d318abdaa7538ec3f6b53b5186b965b8b86e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-blob-storage-from-java"></a>Como toouse armazenamento de Blob do Java
[!INCLUDE [storage-selector-blob-include](../../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-check-out-samples-java](../../../includes/storage-check-out-samples-java.md)]

## <a name="overview"></a>Visão geral
Armazenamento de BLOBs do Azure é um serviço que armazena dados não estruturados em nuvem hello como objetos/blobs. O Armazenamento de Blobs pode conter qualquer tipo de texto ou de dados binários, como um documento, um arquivo de mídia ou um instalador de aplicativo. Armazenamento de blob também é chamado tooas armazenamento de objeto.

Este artigo mostra como tooperform cenários comuns usando Olá armazenamento de BLOBs do Microsoft Azure. exemplos de saudação são escritos em Java e usam Olá [SDK de armazenamento do Azure para Java][Azure Storage SDK for Java]. Olá cenários abordados incluem **Carregando**, **listando**, **baixando**, e **excluindo** blobs. Para obter mais informações sobre blobs, consulte Olá [próximas etapas](#Next-Steps) seção.

> [!NOTE]
> Um SDK está disponível para os desenvolvedores que usam o Armazenamento do Azure em dispositivos Android. Para obter mais informações, consulte Olá [SDK de armazenamento do Azure para Android][Azure Storage SDK for Android].
>
>

[!INCLUDE [storage-blob-concepts-include](../../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

## <a name="create-a-java-application"></a>Criar um aplicativo Java
Neste artigo, você usará os recursos de armazenamento que podem ser executados em um aplicativo Java localmente ou no código em execução em uma função web ou de trabalho do Azure.

toodo assim, você precisará tooinstall Olá Java Development Kit (JDK) e criar uma conta de armazenamento do Azure em sua assinatura do Azure. Depois de você ter feito isso, você precisará tooverify seu sistema de desenvolvimento atende aos requisitos mínimos de saudação e dependências que são listadas no hello [SDK de armazenamento do Azure para Java] [ Azure Storage SDK for Java] repositório no GitHub. Se seu sistema atende a esses requisitos, você pode seguir as instruções de saudação para baixar e instalar Olá bibliotecas de armazenamento do Azure para Java em seu sistema desse repositório. Depois de concluir essas tarefas, será possível toocreate um aplicativo Java que usa exemplos Olá neste artigo.

## <a name="configure-your-application-tooaccess-blob-storage"></a>Configurar seu aplicativo tooaccess armazenamento de Blob
Adicione Olá após a importação instruções toohello superior do arquivo de Java Olá onde você deseja que os blobs de tooaccess toouse Olá APIs de armazenamento do Azure.

```java
// Include hello following imports toouse blob APIs.
import com.microsoft.azure.storage.*;
import com.microsoft.azure.storage.blob.*;
```

## <a name="set-up-an-azure-storage-connection-string"></a>Configurar uma cadeia de conexão de Armazenamento do Azure
Um cliente de armazenamento do Azure usa um pontos de extremidade de toostore de cadeia de caracteres de conexão de armazenamento e as credenciais para acessar os serviços de gerenciamento de dados. Quando em execução em um aplicativo cliente, deve fornecer a cadeia de conexão de armazenamento Olá no formato a seguir, usando o nome de saudação da sua conta de armazenamento de saudação e Olá chave de acesso primária para conta de armazenamento Olá listada no hello [portal do Azure](https://portal.azure.com)para Olá *AccountName* e *AccountKey* valores. Olá exemplo a seguir mostra como você pode declarar uma cadeia de caracteres de conexão do campo estático toohold hello.

```java
// Define hello connection-string with your values
public static final String storageConnectionString =
    "DefaultEndpointsProtocol=http;" +
    "AccountName=your_storage_account;" +
    "AccountKey=your_storage_account_key";
```

Em um aplicativo em execução dentro de uma função no Microsoft Azure, essa cadeia de caracteres pode ser armazenada no arquivo de configuração do serviço hello, *ServiceConfiguration*e pode ser acessado com uma chamada toohello  **RoleEnvironment.getConfigurationSettings** método. Olá, exemplo a seguir obtém Olá cadeia de caracteres de conexão de um **configuração** elemento chamado *StorageConnectionString* no arquivo de configuração do serviço de saudação.

```java
// Retrieve storage account from connection-string.
String storageConnectionString =
    RoleEnvironment.getConfigurationSettings().get("StorageConnectionString");
```

Olá exemplos a seguir pressupõem que você usou uma cadeia de conexão de armazenamento esses dois métodos tooget hello.

## <a name="create-a-container"></a>Criar um contêiner
Um objeto **CloudBlobClient** permite que você obtenha os objetos de referência para os contêineres e blobs. Olá código a seguir cria um **CloudBlobClient** objeto.

> [!NOTE]
> Existem outras maneiras toocreate **CloudStorageAccount** objetos; para obter mais informações, consulte **CloudStorageAccount** em Olá [referência de SDK do cliente de armazenamento do Azure].
>
>

[!INCLUDE [storage-container-naming-rules-include](../../../includes/storage-container-naming-rules-include.md)]

Saudação de uso **CloudBlobClient** tooget um contêiner de toohello de referência que você deseja toouse do objeto. Você pode criar o contêiner de saudação se ele não existir com hello **createIfNotExists** método, caso contrário, retornará o contêiner existente hello. Por padrão, novo contêiner de saudação é privado, portanto, você deve especificar sua chave de acesso de armazenamento (como feito anteriormente) blobs toodownload desse contêiner.

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount = CloudStorageAccount.parse(storageConnectionString);

    // Create hello blob client.
    CloudBlobClient blobClient = storageAccount.createCloudBlobClient();

    // Get a reference tooa container.
    // hello container name must be lower case
    CloudBlobContainer container = blobClient.getContainerReference("mycontainer");

    // Create hello container if it does not exist.
    container.createIfNotExists();
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

### <a name="optional-configure-a-container-for-public-access"></a>Opcional: configurar um contêiner para acesso público
Permissões do contêiner são configuradas para acesso privado por padrão, mas você pode facilmente configurar permissões tooallow pública, somente leitura acesso um contêiner para todos os usuários em Olá Internet:

```java
// Create a permissions object.
BlobContainerPermissions containerPermissions = new BlobContainerPermissions();

// Include public access in hello permissions object.
containerPermissions.setPublicAccess(BlobContainerPublicAccessType.CONTAINER);

// Set hello permissions on hello container.
container.uploadPermissions(containerPermissions);
```

## <a name="upload-a-blob-into-a-container"></a>Carregar um blob em um contêiner
tooupload um blob de tooa de arquivo, obtenha uma referência de contêiner e usá-lo tooget uma referência de blob. Quando você tem uma referência de blob, você pode carregar qualquer fluxo chamando o carregamento em referência de blob hello. Esta operação criará blob Olá se ele não existe ou substituí-lo se ele faz. saudação de exemplo de código a seguir mostra esse e supõe que esse contêiner Olá já foi criado.

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount = CloudStorageAccount.parse(storageConnectionString);

    // Create hello blob client.
    CloudBlobClient blobClient = storageAccount.createCloudBlobClient();

    // Retrieve reference tooa previously created container.
    CloudBlobContainer container = blobClient.getContainerReference("mycontainer");

    // Define hello path tooa local file.
    final String filePath = "C:\\myimages\\myimage.jpg";

    // Create or overwrite hello "myimage.jpg" blob with contents from a local file.
    CloudBlockBlob blob = container.getBlockBlobReference("myimage.jpg");
    File source = new File(filePath);
    blob.upload(new FileInputStream(source), source.length());
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="list-hello-blobs-in-a-container"></a>Saudação de listar blobs em um contêiner
blobs de saudação toolist em um contêiner, primeiro obtenha uma referência de contêiner como você fez tooupload um blob. Você pode usar o contêiner de saudação **listBlobs** método com um **para** loop. Olá código a seguir gera Olá Uri de cada blob em um console de toohello do contêiner.

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount = CloudStorageAccount.parse(storageConnectionString);

    // Create hello blob client.
    CloudBlobClient blobClient = storageAccount.createCloudBlobClient();

    // Retrieve reference tooa previously created container.
    CloudBlobContainer container = blobClient.getContainerReference("mycontainer");

    // Loop over blobs within hello container and output hello URI tooeach of them.
    for (ListBlobItem blobItem : container.listBlobs()) {
        System.out.println(blobItem.getUri());
    }
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

Lembre-se de que você pode nomear blobs com informações de caminho em seus nomes. Isso cria uma estrutura de diretório virtual que você pode organizar e percorrer como faria com um sistema de arquivos tradicional. Observe que a estrutura de diretórios Olá só é virtual - Olá somente os recursos disponíveis no armazenamento de Blob são contêineres e blobs. No entanto, a biblioteca de saudação do cliente oferece uma **CloudBlobDirectory** objeto de diretório virtual do toorefer tooa e simplificar o processo de saudação do trabalho com blobs são organizados dessa maneira.

Por exemplo, você pode ter um contêiner denominado “photos”, no qual poderia carregar os blobs “rootphoto1”, “2010/photo1”, “2010/photo2” e “2011/photo1”. Isso criaria Olá diretórios virtuais dentro do contêiner do "fotos" hello "2011" e "2010". Quando você chama **listBlobs** no contêiner do "fotos" Olá, coleção Olá retornada conterá **CloudBlobDirectory** e **CloudBlob** objetos que representam Olá diretórios e blobs presentes no nível superior de saudação. Nesse caso, os diretórios “2010” e “2011”, bem como “rootphoto1” de photo, seriam retornados. Você pode usar o hello **instanceof** toodistinguish operador esses objetos.

Opcionalmente, você pode passar parâmetros toohello **listBlobs** método com hello **useFlatBlobListing** parâmetro definido tootrue. Isso resultará no retorno de cada blob, independentemente do diretório. Para obter mais informações, consulte **Cloudblobcontainer** em Olá [referência de SDK do cliente de armazenamento do Azure].

## <a name="download-a-blob"></a>Baixar um blob
blobs toodownload, siga Olá mesmo as etapas de como você fez para carregar um blob em ordem tooget uma referência de blob. Em Olá carregamento de exemplo, você chamou o carregamento no objeto de blob hello. Olá exemplo a seguir, chamar download tootransfer Olá conteúdo tooa fluxo objeto blob como um **FileOutputStream** que você pode usar o arquivo do local de tooa toopersist Olá blob.

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount = CloudStorageAccount.parse(storageConnectionString);

    // Create hello blob client.
    CloudBlobClient blobClient = storageAccount.createCloudBlobClient();

    // Retrieve reference tooa previously created container.
    CloudBlobContainer container = blobClient.getContainerReference("mycontainer");

    // Loop through each blob item in hello container.
    for (ListBlobItem blobItem : container.listBlobs()) {
        // If hello item is a blob, not a virtual directory.
        if (blobItem instanceof CloudBlob) {
            // Download hello item and save it tooa file with hello same name.
            CloudBlob blob = (CloudBlob) blobItem;
            blob.download(new FileOutputStream("C:\\mydownloads\\" + blob.getName()));
        }
    }
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="delete-a-blob"></a>Excluir um blob
toodelete um blob, obter um blob de referência e, em seguida, chamar **deleteIfExists**.

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount = CloudStorageAccount.parse(storageConnectionString);

    // Create hello blob client.
    CloudBlobClient blobClient = storageAccount.createCloudBlobClient();

    // Retrieve reference tooa previously created container.
    CloudBlobContainer container = blobClient.getContainerReference("mycontainer");

    // Retrieve reference tooa blob named "myimage.jpg".
    CloudBlockBlob blob = container.getBlockBlobReference("myimage.jpg");

    // Delete hello blob.
    blob.deleteIfExists();
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="delete-a-blob-container"></a>Excluir um contêiner de blob
Por fim, toodelete um contêiner de blob, obter um blob de referência de contêiner e chame **deleteIfExists**.

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount = CloudStorageAccount.parse(storageConnectionString);

    // Create hello blob client.
    CloudBlobClient blobClient = storageAccount.createCloudBlobClient();

    // Retrieve reference tooa previously created container.
    CloudBlobContainer container = blobClient.getContainerReference("mycontainer");

    // Delete hello blob container.
    container.deleteIfExists();
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="next-steps"></a>Próximas etapas
Agora que você aprendeu as Noções básicas de saudação do armazenamento de Blob, siga essas toolearn links sobre tarefas mais complexas de armazenamento.

* [Microsoft Azure Storage SDK for Java][Azure Storage SDK for Java] (SDK de Armazenamento do Microsoft Azure para Java)
* [referência de SDK do cliente de armazenamento do Azure][referência de SDK do cliente de armazenamento do Azure]
* [Azure Storage REST API Reference][Azure Storage REST API] (Referência de API REST do Armazenamento do Azure)
* [Microsoft Azure Storage Team Blog][Azure Storage Team Blog] (Blog da equipe de Armazenamento do Microsoft Azure)

Para saber mais, consulte também [Azure para desenvolvedores Java](/java/azure).

[Azure SDK for Java]: http://go.microsoft.com/fwlink/?LinkID=525671
[Azure Storage SDK for Java]: https://github.com/azure/azure-storage-java
[Azure Storage SDK for Android]: https://github.com/azure/azure-storage-android
[referência de SDK do cliente de armazenamento do Azure]: http://dl.windowsazure.com/storage/javadoc/
[Azure Storage REST API]: https://msdn.microsoft.com/library/azure/dd179355.aspx
[Azure Storage Team Blog]: http://blogs.msdn.com/b/windowsazurestorage/
