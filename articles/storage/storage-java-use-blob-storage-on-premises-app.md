---
title: aplicativo de aaaOn local com armazenamento de blob (Java) | Microsoft Docs
description: "Saiba como toocreate um aplicativo de console que carrega uma imagem tooAzure e, em seguida, exibe Olá imagem em seu navegador. Amostras de código em Java."
services: storage
documentationcenter: java
author: mmacy
manager: carmonm
editor: tysonn
ms.assetid: ccc9a7d7-6fe4-467b-b7fd-a73f17539e3f
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 11/17/2016
ms.author: marsma
ms.openlocfilehash: ed8eb4c1045691c25abe94bf6c1b18b797adc3e3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="on-premises-application-with-blob-storage"></a>Aplicativo local com armazenamento de blob
## <a name="overview"></a>Visão geral
Olá exemplo a seguir mostra como você pode usar o armazenamento do Azure para armazenar imagens no Azure. código de saudação neste artigo é para um aplicativo de console que carrega uma imagem tooAzure e, em seguida, cria um arquivo HTML que exibe a imagem de saudação em seu navegador.

## <a name="prerequisites"></a>Pré-requisitos
* Um JDK (Java Developer Kit) versão 1.6 ou posterior deve estar instalado.
* Olá SDK do Azure está instalado.
* Olá JAR para bibliotecas do hello Azure para Java e JARs qualquer dependência aplicável, são instalados e estão no caminho de compilação de saudação usado pelo seu compilador Java. Para obter informações sobre como instalar Olá bibliotecas do Azure para Java, consulte [Download Olá SDK do Azure para Java](../java-download-azure-sdk.md).
* Uma conta de armazenamento do Azure deve ter sido configurada. Olá nome da conta e chave de conta para conta de armazenamento Olá serão usados pelo código Olá neste artigo. Consulte [como tooCreate uma conta de armazenamento](storage-create-storage-account.md#create-a-storage-account) para obter informações sobre como criar uma conta de armazenamento e [exibir e copiar chaves de acesso de armazenamento](storage-create-storage-account.md#view-and-copy-storage-access-keys) para obter informações sobre a recuperação de chave da conta hello.
* Você criou um arquivo de imagem local chamado armazenados no hello path c:\\myimages\\image1.jpg. Como alternativa, modifique o **FileInputStream** construtor no exemplo de hello toouse um nome de arquivo e caminho de imagem diferente.

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

## <a name="toouse-azure-blob-storage-tooupload-a-file"></a>tooupload de armazenamento de BLOBs do Azure toouse um arquivo
Um procedimento passo a passo é apresentado aqui. Se você quiser tooskip em frente, todo código de saudação será apresentado mais adiante neste artigo.

Iniciar código hello, incluindo imports para classes de armazenamento do Azure core hello, classes de cliente de BLOBs do Azure hello, classes de e/s de Java hello e Olá **URISyntaxException** classe.

```java
import com.microsoft.azure.storage.*;
import com.microsoft.azure.storage.blob.*;
import java.io.*;
import java.net.URISyntaxException;
```

Declare uma classe denominada **StorageSample**e incluir o colchete hello, **{**.

```java
public class StorageSample {
```

Dentro de saudação **StorageSample** classe, declare uma variável de cadeia de caracteres que irá conter o protocolo de ponto de extremidade saudação padrão, o nome da sua conta de armazenamento e sua chave de acesso de armazenamento, conforme especificado na conta de armazenamento do Azure. Substituir valores de espaço reservado de saudação **sua\_conta\_nome** e **sua\_conta\_chave** com seu próprio nome de conta e chave de conta respectivamente.

```java
public static final String storageConnectionString =
    "DefaultEndpointsProtocol=http;" +
    "AccountName=your_account_name;" +
    "AccountKey=your_account_name";
```

Adicionar na sua declaração de **principal**, incluem uma **tente** bloquear e incluem hello necessário abrir colchetes **{**.

```java
    public static void main(String[] args)
    {
        try
        {
```

Declare variáveis de hello (Olá são descrições de como eles são usados neste exemplo) de tipo a seguir:

* **CloudStorageAccount**: tooinitialize usado Olá conta objeto com o nome da conta de armazenamento do Azure e a chave e o toocreate o objeto de cliente do blob.
* **CloudBlobClient**: usado tooaccess Olá blob serviço.
* **CloudBlobContainer**: toocreate usado um contêiner de blob, listar os blobs em Olá contêineres e delete hello.
* **CloudBlockBlob**: tooupload usado um contêiner de toothe do arquivo de imagem local.

<!-- -->

```java
    CloudStorageAccount account;
    CloudBlobClient serviceClient;
    CloudBlobContainer container;
    CloudBlockBlob blob;
```

Atribuir um valor toohello **conta** variável.

```java
account = CloudStorageAccount.parse(storageConnectionString);
```

Atribuir um valor toohello **serviceClient** variável.

```java
serviceClient = account.createCloudBlobClient();
```

Atribuir um valor toohello **contêiner** variável. Teremos um contêiner de tooa de referência chamado **gettingstarted**.

```java
// Container name must be lower case.
container = serviceClient.getContainerReference("gettingstarted");
```

Crie contêiner de saudação. Esse método criará o contêiner de saudação se ele não existir (e retornar **true**). Se o contêiner de saudação existir, ele retornará **false**. Uma alternativa muito**createIfNotExists** é hello **criar** método (que será retornado um erro se já existir um contêiner de saudação).

```java
container.createIfNotExists();
```

Defina o acesso anônimo para o contêiner de saudação.

```java
// Set anonymous access on hello container.
BlobContainerPermissions containerPermissions;
containerPermissions = new BlobContainerPermissions();
containerPermissions.setPublicAccess(BlobContainerPublicAccessType.CONTAINER);
container.uploadPermissions(containerPermissions);
```

Obter um blob de bloco de toohello de referência, que representará o blob Olá no armazenamento do Azure.

```java
blob = container.getBlockBlobReference("image1.jpg");
```

Saudação de uso **arquivo** construtor tooget um arquivo de toohello criado localmente de referência que você fará o upload. Certifique-se de que você criou esse arquivo antes de executar código hello.

```java
File fileReference = new File ("c:\\myimages\\image1.jpg");
```

Carregar arquivo de saudação local por meio de uma chamada toohello **CloudBlockBlob.upload** método. Olá toohello do primeiro parâmetro **CloudBlockBlob.upload** método é um **FileInputStream** representa Olá local arquivo que será carregado tooAzure armazenamento do objeto. Olá segundo parâmetro é o tamanho de hello, em bytes, do arquivo hello.

```java
blob.upload(new FileInputStream(fileReference), fileReference.length());
```

Chamar uma função auxiliar chamada **MakeHTMLPage**, página toomake básica de HTML que contém um  **&lt;imagem&gt;**  elemento com o blob toohello de conjunto de origem de saudação que agora está no seu Azure conta de armazenamento. Olá código para **MakeHTMLPage** será discutido neste artigo.

```java
MakeHTMLPage(container);
```

Imprima uma mensagem de status e informações sobre Olá criado página HTML.

```java
System.out.println("Processing complete.");
System.out.println("Open index.html toosee hello images stored in your storage account.");
```

Olá fechar **tente** bloco inserindo um colchete de fechamento: **}**

Saudação de identificador exceções a seguir:

* **FileNotFoundException**: pode ser gerada pelo Olá **FileInputStream** ou **FileOutputStream** construtores.
* **StorageException**: pode ser gerada pela biblioteca de armazenamento do Azure cliente hello.
* **URISyntaxException**: pode ser gerada pelo Olá **ListBlobItem.getUri** método.
* **Exception**: manipulação de exceção genérica.

<!-- -->

```java
catch (FileNotFoundException fileNotFoundException)
{
    System.out.print("FileNotFoundException encountered: ");
    System.out.println(fileNotFoundException.getMessage());
    System.exit(-1);
}
catch (StorageException storageException)
{
    System.out.print("StorageException encountered: ");
    System.out.println(storageException.getMessage());
    System.exit(-1);
}
catch (URISyntaxException uriSyntaxException)
{
    System.out.print("URISyntaxException encountered: ");
    System.out.println(uriSyntaxException.getMessage());
    System.exit(-1);
}
catch (Exception e)
{
    System.out.print("Exception encountered: ");
    System.out.println(e.getMessage());
    System.exit(-1);
}
```

Feche **main** inserindo um colchete de fechamento: **}**

Crie um método chamado **MakeHTMLPage** toocreate uma HTML básico de página. Esse método tem um parâmetro de tipo **CloudBlobContainer**, que será usado tooiterate lista Olá de blobs carregados. Esse método lançará exceções do tipo **FileNotFoundException**, que pode ser gerado pelo Olá **FileOutputStream** construtor, e **URISyntaxException**, que pode lançada pelo Olá **ListBlobItem.getUri** método. Inclua o colchete de abertura, **{**.

```java
public static void MakeHTMLPage(CloudBlobContainer container) throws FileNotFoundException, URISyntaxException
{
```

Crie um arquivo local chamado **index.html**.

```java
PrintStream stream;
stream = new PrintStream(new FileOutputStream("index.html"));
```

Gravar o arquivo local toohello, adicionando no hello  **&lt;html&gt;**,  **&lt;cabeçalho&gt;**, e  **&lt;corpo&gt;**  elementos.

```java
stream.println("<html>");
stream.println("<header/>");
stream.println("<body>");
```

Itere a lista de saudação de blobs carregados. Para cada blob no hello HTML da página, crie um  **&lt;img&gt;**  elemento que tem seu **src** atributo enviado à saudação do URI do blob hello, conforme exibido na sua conta de armazenamento do Azure.
Embora tenha adicionado apenas uma imagem neste exemplo, se você adicionar mais imagens, este código iteraria todos eles.

Para simplificar, este exemplo assume que cada blob carregado é uma imagem. Se você atualizou blobs diferentes imagens ou blobs de página em vez de blobs de bloco, ajuste o código de saudação conforme necessário.

```java
// Enumerate hello uploaded blobs.
for (ListBlobItem blobItem : container.listBlobs()) {
// List each blob as an <img> element in hello HTML body.
stream.println("<img src='" + blobItem.getUri() + "'/><br/>");
}
```

Olá fechar  **&lt;corpo&gt;**  elemento e hello  **&lt;html&gt;**  elemento.

```java
stream.println("</body>");
stream.println("</html>");
```

Arquivo de local de saudação fechar.

```java
stream.close();
```

Feche **MakeHTMLPage** inserindo um colchete de fechamento: **}**

Feche **StorageSample** inserindo um colchete de fechamento: **}**

a seguir Olá é código completo de saudação para este exemplo. Lembre-se de valores de espaço reservado de saudação toomodify **sua\_conta\_nome** e **sua\_conta\_chave** toouse seu nome de conta e a conta chave, respectivamente.

```java
import com.microsoft.azure.storage.*;
import com.microsoft.azure.storage.blob.*;
import java.io.*;
import java.net.URISyntaxException;

// Create an image, c:\myimages\image1.jpg, prior toorunning this sample.
// Alternatively, change hello value used by hello FileInputStream constructor
// toouse a different image path and file that you have already created.
public class StorageSample {

    public static final String storageConnectionString =
            "DefaultEndpointsProtocol=http;" +
                    "AccountName=your_account_name;" +
                    "AccountKey=your_account_name";

    public static void main(String[] args) {
        try {
            CloudStorageAccount account;
            CloudBlobClient serviceClient;
            CloudBlobContainer container;
            CloudBlockBlob blob;

            account = CloudStorageAccount.parse(storageConnectionString);
            serviceClient = account.createCloudBlobClient();
            // Container name must be lower case.
            container = serviceClient.getContainerReference("gettingstarted");
            container.createIfNotExists();

            // Set anonymous access on hello container.
            BlobContainerPermissions containerPermissions;
            containerPermissions = new BlobContainerPermissions();
            containerPermissions.setPublicAccess(BlobContainerPublicAccessType.CONTAINER);
            container.uploadPermissions(containerPermissions);

            // Upload an image file.
            blob = container.getBlockBlobReference("image1.jpg");

            File fileReference = new File("c:\\myimages\\image1.jpg");
            blob.upload(new FileInputStream(fileReference), fileReference.length());

            // At this point hello image is uploaded.
            // Next, create an HTML page that lists all of hello uploaded images.
            MakeHTMLPage(container);

            System.out.println("Processing complete.");
            System.out.println("Open index.html toosee hello images stored in your storage account.");

        } catch (FileNotFoundException fileNotFoundException) {
            System.out.print("FileNotFoundException encountered: ");
            System.out.println(fileNotFoundException.getMessage());
            System.exit(-1);
        } catch (StorageException storageException) {
            System.out.print("StorageException encountered: ");
            System.out.println(storageException.getMessage());
            System.exit(-1);
        } catch (URISyntaxException uriSyntaxException) {
            System.out.print("URISyntaxException encountered: ");
            System.out.println(uriSyntaxException.getMessage());
            System.exit(-1);
        } catch (Exception e) {
            System.out.print("Exception encountered: ");
            System.out.println(e.getMessage());
            System.exit(-1);
        }
    }

    // Create an HTML page that can be used toodisplay hello uploaded images.
    // This example assumes all of hello blobs are for images.
    public static void MakeHTMLPage(CloudBlobContainer container) throws FileNotFoundException, URISyntaxException
    {
        PrintStream stream;
        stream = new PrintStream(new FileOutputStream("index.html"));

        // Create hello opening <html>, <header>, and <body> elements.
        stream.println("<html>");
        stream.println("<header/>");
        stream.println("<body>");

        // Enumerate hello uploaded blobs.
        for (ListBlobItem blobItem : container.listBlobs()) {
            // List each blob as an <img> element in hello HTML body.
            stream.println("<img src='" + blobItem.getUri() + "'/><br/>");
        }

        stream.println("</body>");

        // Complete hello <html> element and close hello file.
        stream.println("</html>");
        stream.close();
    }
}
```

Adição toouploading seu armazenamento de tooAzure do arquivo de imagem local, o código de exemplo hello cria namedindex.html um arquivo local, que pode ser aberto no seu navegador toosee sua imagem carregada.

Como código Olá contém o nome da conta e chave de conta, certifique-se de que seu código-fonte é seguro.

## <a name="toodelete-a-container"></a>toodelete um contêiner
Como você é cobrado para armazenamento, você pode querer toodelete o **gettingstarted** contêiner depois que você experimentar este exemplo. toodelete um contêiner, use Olá **CloudBlobContainer.delete** método.

```java
container = serviceClient.getContainerReference("gettingstarted");
container.delete();
```

Olá toocall **CloudBlobContainer.delete** método, o processo de saudação de inicialização **CloudStorageAccount**, **ClodBlobClient**, e  **CloudBlobContainer** objetos é Olá mesmo mostrado para o **createIfNotExist** método. Olá, a seguir é um exemplo completo que exclusões Olá contêiner nomeado **gettingstarted**.

```java
import com.microsoft.azure.storage.*;
import com.microsoft.azure.storage.blob.*;

public class DeleteContainer {

    public static final String storageConnectionString =
            "DefaultEndpointsProtocol=http;" +
                "AccountName=your_account_name;" +
                "AccountKey=your_account_key";

    public static void main(String[] args)
    {
        try
        {
            CloudStorageAccount account;
            CloudBlobClient serviceClient;
            CloudBlobContainer container;

            account = CloudStorageAccount.parse(storageConnectionString);
            serviceClient = account.createCloudBlobClient();
            // Container name must be lower case.
            container = serviceClient.getContainerReference("gettingstarted");
            container.delete();

            System.out.println("Container deleted.");

        }
        catch (StorageException storageException)
        {
            System.out.print("StorageException encountered: ");
            System.out.println(storageException.getMessage());
            System.exit(-1);
        }
        catch (Exception e)
        {
            System.out.print("Exception encountered: ");
            System.out.println(e.getMessage());
            System.exit(-1);
        }
    }
}
```

Para obter uma visão geral de outros métodos e classes de armazenamento de blob, consulte [como toouse armazenamento de Blob do Java](storage-java-how-to-use-blob-storage.md).

## <a name="next-steps"></a>Próximas etapas
Siga essas toolearn links mais informações sobre tarefas mais complexas de armazenamento.

* [SDK de Armazenamento do Azure para Java](https://github.com/azure/azure-storage-java)
* [Referência de SDK do Cliente de Armazenamento do Azure](http://dl.windowsazure.com/storage/javadoc/)
* [API REST de serviços de armazenamento do Azure](https://msdn.microsoft.com/library/azure/dd179355.aspx)
* [Blog da equipe de Armazenamento do Azure](http://blogs.msdn.com/b/windowsazurestorage/)

