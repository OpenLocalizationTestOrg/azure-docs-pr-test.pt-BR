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
# <a name="on-premises-application-with-blob-storage"></a><span data-ttu-id="92148-104">Aplicativo local com armazenamento de blob</span><span class="sxs-lookup"><span data-stu-id="92148-104">On-premises application with blob storage</span></span>
## <a name="overview"></a><span data-ttu-id="92148-105">Visão geral</span><span class="sxs-lookup"><span data-stu-id="92148-105">Overview</span></span>
<span data-ttu-id="92148-106">Olá exemplo a seguir mostra como você pode usar o armazenamento do Azure para armazenar imagens no Azure.</span><span class="sxs-lookup"><span data-stu-id="92148-106">hello following example shows you how you can use Azure storage to store images in Azure.</span></span> <span data-ttu-id="92148-107">código de saudação neste artigo é para um aplicativo de console que carrega uma imagem tooAzure e, em seguida, cria um arquivo HTML que exibe a imagem de saudação em seu navegador.</span><span class="sxs-lookup"><span data-stu-id="92148-107">hello code in this article is for a console application that uploads an image tooAzure, and then creates an HTML file that displays hello image in your browser.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="92148-108">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="92148-108">Prerequisites</span></span>
* <span data-ttu-id="92148-109">Um JDK (Java Developer Kit) versão 1.6 ou posterior deve estar instalado.</span><span class="sxs-lookup"><span data-stu-id="92148-109">A Java Developer Kit (JDK), version 1.6 or later, is installed.</span></span>
* <span data-ttu-id="92148-110">Olá SDK do Azure está instalado.</span><span class="sxs-lookup"><span data-stu-id="92148-110">hello Azure SDK is installed.</span></span>
* <span data-ttu-id="92148-111">Olá JAR para bibliotecas do hello Azure para Java e JARs qualquer dependência aplicável, são instalados e estão no caminho de compilação de saudação usado pelo seu compilador Java.</span><span class="sxs-lookup"><span data-stu-id="92148-111">hello JAR for hello Azure Libraries for Java, and any applicable dependency JARs, are installed and are in hello build path used by your Java compiler.</span></span> <span data-ttu-id="92148-112">Para obter informações sobre como instalar Olá bibliotecas do Azure para Java, consulte [Download Olá SDK do Azure para Java](../java-download-azure-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="92148-112">For information about installing hello Azure Libraries for Java, see [Download hello Azure SDK for Java](../java-download-azure-sdk.md).</span></span>
* <span data-ttu-id="92148-113">Uma conta de armazenamento do Azure deve ter sido configurada.</span><span class="sxs-lookup"><span data-stu-id="92148-113">An Azure storage account has been set up.</span></span> <span data-ttu-id="92148-114">Olá nome da conta e chave de conta para conta de armazenamento Olá serão usados pelo código Olá neste artigo.</span><span class="sxs-lookup"><span data-stu-id="92148-114">hello account name and account key for hello storage account will be used by hello code in this article.</span></span> <span data-ttu-id="92148-115">Consulte [como tooCreate uma conta de armazenamento](storage-create-storage-account.md#create-a-storage-account) para obter informações sobre como criar uma conta de armazenamento e [exibir e copiar chaves de acesso de armazenamento](storage-create-storage-account.md#view-and-copy-storage-access-keys) para obter informações sobre a recuperação de chave da conta hello.</span><span class="sxs-lookup"><span data-stu-id="92148-115">See [How tooCreate a Storage Account](storage-create-storage-account.md#create-a-storage-account) for information about creating a storage account, and [View and copy storage access keys](storage-create-storage-account.md#view-and-copy-storage-access-keys) for information about retrieving hello account key.</span></span>
* <span data-ttu-id="92148-116">Você criou um arquivo de imagem local chamado armazenados no hello path c:\\myimages\\image1.jpg.</span><span class="sxs-lookup"><span data-stu-id="92148-116">You have created a local image file named stored at hello path c:\\myimages\\image1.jpg.</span></span> <span data-ttu-id="92148-117">Como alternativa, modifique o **FileInputStream** construtor no exemplo de hello toouse um nome de arquivo e caminho de imagem diferente.</span><span class="sxs-lookup"><span data-stu-id="92148-117">Alternatively, modify the **FileInputStream** constructor in hello example toouse a different image path and file name.</span></span>

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

## <a name="toouse-azure-blob-storage-tooupload-a-file"></a><span data-ttu-id="92148-118">tooupload de armazenamento de BLOBs do Azure toouse um arquivo</span><span class="sxs-lookup"><span data-stu-id="92148-118">toouse Azure blob storage tooupload a file</span></span>
<span data-ttu-id="92148-119">Um procedimento passo a passo é apresentado aqui.</span><span class="sxs-lookup"><span data-stu-id="92148-119">A step-by-step procedure is presented here.</span></span> <span data-ttu-id="92148-120">Se você quiser tooskip em frente, todo código de saudação será apresentado mais adiante neste artigo.</span><span class="sxs-lookup"><span data-stu-id="92148-120">If you'd like tooskip ahead, hello entire code is presented later in this article.</span></span>

<span data-ttu-id="92148-121">Iniciar código hello, incluindo imports para classes de armazenamento do Azure core hello, classes de cliente de BLOBs do Azure hello, classes de e/s de Java hello e Olá **URISyntaxException** classe.</span><span class="sxs-lookup"><span data-stu-id="92148-121">Begin hello code by including imports for hello Azure core storage classes, hello Azure blob client classes, hello Java IO classes, and hello **URISyntaxException** class.</span></span>

```java
import com.microsoft.azure.storage.*;
import com.microsoft.azure.storage.blob.*;
import java.io.*;
import java.net.URISyntaxException;
```

<span data-ttu-id="92148-122">Declare uma classe denominada **StorageSample**e incluir o colchete hello, **{**.</span><span class="sxs-lookup"><span data-stu-id="92148-122">Declare a class named **StorageSample**, and include hello open bracket, **{**.</span></span>

```java
public class StorageSample {
```

<span data-ttu-id="92148-123">Dentro de saudação **StorageSample** classe, declare uma variável de cadeia de caracteres que irá conter o protocolo de ponto de extremidade saudação padrão, o nome da sua conta de armazenamento e sua chave de acesso de armazenamento, conforme especificado na conta de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="92148-123">Within hello **StorageSample** class, declare a string variable that will contain hello default endpoint protocol, your storage account name, and your storage access key, as specified in your Azure storage account.</span></span> <span data-ttu-id="92148-124">Substituir valores de espaço reservado de saudação **sua\_conta\_nome** e **sua\_conta\_chave** com seu próprio nome de conta e chave de conta respectivamente.</span><span class="sxs-lookup"><span data-stu-id="92148-124">Replace hello placeholder values **your\_account\_name** and **your\_account\_key** with your own account name and account key, respectively.</span></span>

```java
public static final String storageConnectionString =
    "DefaultEndpointsProtocol=http;" +
    "AccountName=your_account_name;" +
    "AccountKey=your_account_name";
```

<span data-ttu-id="92148-125">Adicionar na sua declaração de **principal**, incluem uma **tente** bloquear e incluem hello necessário abrir colchetes **{**.</span><span class="sxs-lookup"><span data-stu-id="92148-125">Add in your declaration for **main**, include a **try** block, and include hello necessary open brackets, **{**.</span></span>

```java
    public static void main(String[] args)
    {
        try
        {
```

<span data-ttu-id="92148-126">Declare variáveis de hello (Olá são descrições de como eles são usados neste exemplo) de tipo a seguir:</span><span class="sxs-lookup"><span data-stu-id="92148-126">Declare variables of hello following type (hello descriptions are for how they are used in this example):</span></span>

* <span data-ttu-id="92148-127">**CloudStorageAccount**: tooinitialize usado Olá conta objeto com o nome da conta de armazenamento do Azure e a chave e o toocreate o objeto de cliente do blob.</span><span class="sxs-lookup"><span data-stu-id="92148-127">**CloudStorageAccount**: Used tooinitialize hello account object with your Azure storage account name and key, and toocreate the blob client object.</span></span>
* <span data-ttu-id="92148-128">**CloudBlobClient**: usado tooaccess Olá blob serviço.</span><span class="sxs-lookup"><span data-stu-id="92148-128">**CloudBlobClient**: Used tooaccess hello blob service.</span></span>
* <span data-ttu-id="92148-129">**CloudBlobContainer**: toocreate usado um contêiner de blob, listar os blobs em Olá contêineres e delete hello.</span><span class="sxs-lookup"><span data-stu-id="92148-129">**CloudBlobContainer**: Used toocreate a blob container, list the blobs in hello container, and delete hello container.</span></span>
* <span data-ttu-id="92148-130">**CloudBlockBlob**: tooupload usado um contêiner de toothe do arquivo de imagem local.</span><span class="sxs-lookup"><span data-stu-id="92148-130">**CloudBlockBlob**: Used tooupload a local image file toothe container.</span></span>

<!-- -->

```java
    CloudStorageAccount account;
    CloudBlobClient serviceClient;
    CloudBlobContainer container;
    CloudBlockBlob blob;
```

<span data-ttu-id="92148-131">Atribuir um valor toohello **conta** variável.</span><span class="sxs-lookup"><span data-stu-id="92148-131">Assign a value toohello **account** variable.</span></span>

```java
account = CloudStorageAccount.parse(storageConnectionString);
```

<span data-ttu-id="92148-132">Atribuir um valor toohello **serviceClient** variável.</span><span class="sxs-lookup"><span data-stu-id="92148-132">Assign a value toohello **serviceClient** variable.</span></span>

```java
serviceClient = account.createCloudBlobClient();
```

<span data-ttu-id="92148-133">Atribuir um valor toohello **contêiner** variável.</span><span class="sxs-lookup"><span data-stu-id="92148-133">Assign a value toohello **container** variable.</span></span> <span data-ttu-id="92148-134">Teremos um contêiner de tooa de referência chamado **gettingstarted**.</span><span class="sxs-lookup"><span data-stu-id="92148-134">We'll get a reference tooa container named **gettingstarted**.</span></span>

```java
// Container name must be lower case.
container = serviceClient.getContainerReference("gettingstarted");
```

<span data-ttu-id="92148-135">Crie contêiner de saudação.</span><span class="sxs-lookup"><span data-stu-id="92148-135">Create hello container.</span></span> <span data-ttu-id="92148-136">Esse método criará o contêiner de saudação se ele não existir (e retornar **true**).</span><span class="sxs-lookup"><span data-stu-id="92148-136">This method will create hello container if it doesn't exist (and return **true**).</span></span> <span data-ttu-id="92148-137">Se o contêiner de saudação existir, ele retornará **false**.</span><span class="sxs-lookup"><span data-stu-id="92148-137">If hello container does exist, it will return **false**.</span></span> <span data-ttu-id="92148-138">Uma alternativa muito**createIfNotExists** é hello **criar** método (que será retornado um erro se já existir um contêiner de saudação).</span><span class="sxs-lookup"><span data-stu-id="92148-138">An alternative too**createIfNotExists** is hello **create** method (which will return an error if hello container already exists).</span></span>

```java
container.createIfNotExists();
```

<span data-ttu-id="92148-139">Defina o acesso anônimo para o contêiner de saudação.</span><span class="sxs-lookup"><span data-stu-id="92148-139">Set anonymous access for hello container.</span></span>

```java
// Set anonymous access on hello container.
BlobContainerPermissions containerPermissions;
containerPermissions = new BlobContainerPermissions();
containerPermissions.setPublicAccess(BlobContainerPublicAccessType.CONTAINER);
container.uploadPermissions(containerPermissions);
```

<span data-ttu-id="92148-140">Obter um blob de bloco de toohello de referência, que representará o blob Olá no armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="92148-140">Get a reference toohello block blob, which will represent hello blob in Azure storage.</span></span>

```java
blob = container.getBlockBlobReference("image1.jpg");
```

<span data-ttu-id="92148-141">Saudação de uso **arquivo** construtor tooget um arquivo de toohello criado localmente de referência que você fará o upload.</span><span class="sxs-lookup"><span data-stu-id="92148-141">Use hello **File** constructor tooget a reference toohello locally created file that you will upload.</span></span> <span data-ttu-id="92148-142">Certifique-se de que você criou esse arquivo antes de executar código hello.</span><span class="sxs-lookup"><span data-stu-id="92148-142">Ensure you have created this file before running hello code.</span></span>

```java
File fileReference = new File ("c:\\myimages\\image1.jpg");
```

<span data-ttu-id="92148-143">Carregar arquivo de saudação local por meio de uma chamada toohello **CloudBlockBlob.upload** método.</span><span class="sxs-lookup"><span data-stu-id="92148-143">Upload hello local file through a call toohello **CloudBlockBlob.upload** method.</span></span> <span data-ttu-id="92148-144">Olá toohello do primeiro parâmetro **CloudBlockBlob.upload** método é um **FileInputStream** representa Olá local arquivo que será carregado tooAzure armazenamento do objeto.</span><span class="sxs-lookup"><span data-stu-id="92148-144">hello first parameter toohello **CloudBlockBlob.upload** method is a **FileInputStream** object that represents hello local file that will be uploaded tooAzure storage.</span></span> <span data-ttu-id="92148-145">Olá segundo parâmetro é o tamanho de hello, em bytes, do arquivo hello.</span><span class="sxs-lookup"><span data-stu-id="92148-145">hello second parameter is hello size, in bytes, of hello file.</span></span>

```java
blob.upload(new FileInputStream(fileReference), fileReference.length());
```

<span data-ttu-id="92148-146">Chamar uma função auxiliar chamada **MakeHTMLPage**, página toomake básica de HTML que contém um  **&lt;imagem&gt;**  elemento com o blob toohello de conjunto de origem de saudação que agora está no seu Azure conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="92148-146">Call a helper function named **MakeHTMLPage**, toomake a basic HTML page that contains an **&lt;image&gt;** element with hello source set toohello blob that is now in your Azure storage account.</span></span> <span data-ttu-id="92148-147">Olá código para **MakeHTMLPage** será discutido neste artigo.</span><span class="sxs-lookup"><span data-stu-id="92148-147">hello code for **MakeHTMLPage** will be discussed later in this article.</span></span>

```java
MakeHTMLPage(container);
```

<span data-ttu-id="92148-148">Imprima uma mensagem de status e informações sobre Olá criado página HTML.</span><span class="sxs-lookup"><span data-stu-id="92148-148">Print out a status message and information about hello created HTML page.</span></span>

```java
System.out.println("Processing complete.");
System.out.println("Open index.html toosee hello images stored in your storage account.");
```

<span data-ttu-id="92148-149">Olá fechar **tente** bloco inserindo um colchete de fechamento: **}**</span><span class="sxs-lookup"><span data-stu-id="92148-149">Close hello **try** block by inserting a close bracket: **}**</span></span>

<span data-ttu-id="92148-150">Saudação de identificador exceções a seguir:</span><span class="sxs-lookup"><span data-stu-id="92148-150">Handle hello following exceptions:</span></span>

* <span data-ttu-id="92148-151">**FileNotFoundException**: pode ser gerada pelo Olá **FileInputStream** ou **FileOutputStream** construtores.</span><span class="sxs-lookup"><span data-stu-id="92148-151">**FileNotFoundException**: Can be thrown by hello **FileInputStream** or **FileOutputStream** constructors.</span></span>
* <span data-ttu-id="92148-152">**StorageException**: pode ser gerada pela biblioteca de armazenamento do Azure cliente hello.</span><span class="sxs-lookup"><span data-stu-id="92148-152">**StorageException**: Can be thrown by hello Azure client storage library.</span></span>
* <span data-ttu-id="92148-153">**URISyntaxException**: pode ser gerada pelo Olá **ListBlobItem.getUri** método.</span><span class="sxs-lookup"><span data-stu-id="92148-153">**URISyntaxException**: Can be thrown by hello **ListBlobItem.getUri** method.</span></span>
* <span data-ttu-id="92148-154">**Exception**: manipulação de exceção genérica.</span><span class="sxs-lookup"><span data-stu-id="92148-154">**Exception**: Generic exception handling.</span></span>

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

<span data-ttu-id="92148-155">Feche **main** inserindo um colchete de fechamento: **}**</span><span class="sxs-lookup"><span data-stu-id="92148-155">Close **main** by inserting a close bracket: **}**</span></span>

<span data-ttu-id="92148-156">Crie um método chamado **MakeHTMLPage** toocreate uma HTML básico de página.</span><span class="sxs-lookup"><span data-stu-id="92148-156">Create a method named **MakeHTMLPage** toocreate a basic HTML page.</span></span> <span data-ttu-id="92148-157">Esse método tem um parâmetro de tipo **CloudBlobContainer**, que será usado tooiterate lista Olá de blobs carregados.</span><span class="sxs-lookup"><span data-stu-id="92148-157">This method has a parameter of type **CloudBlobContainer**, which will be used tooiterate through hello list of uploaded blobs.</span></span> <span data-ttu-id="92148-158">Esse método lançará exceções do tipo **FileNotFoundException**, que pode ser gerado pelo Olá **FileOutputStream** construtor, e **URISyntaxException**, que pode lançada pelo Olá **ListBlobItem.getUri** método.</span><span class="sxs-lookup"><span data-stu-id="92148-158">This method will throw exceptions of type **FileNotFoundException**, which can be thrown by hello **FileOutputStream** constructor, and **URISyntaxException**, which can be thrown by hello **ListBlobItem.getUri** method.</span></span> <span data-ttu-id="92148-159">Inclua o colchete de abertura, **{**.</span><span class="sxs-lookup"><span data-stu-id="92148-159">Include the opening bracket, **{**.</span></span>

```java
public static void MakeHTMLPage(CloudBlobContainer container) throws FileNotFoundException, URISyntaxException
{
```

<span data-ttu-id="92148-160">Crie um arquivo local chamado **index.html**.</span><span class="sxs-lookup"><span data-stu-id="92148-160">Create a local file named **index.html**.</span></span>

```java
PrintStream stream;
stream = new PrintStream(new FileOutputStream("index.html"));
```

<span data-ttu-id="92148-161">Gravar o arquivo local toohello, adicionando no hello  **&lt;html&gt;**,  **&lt;cabeçalho&gt;**, e  **&lt;corpo&gt;**  elementos.</span><span class="sxs-lookup"><span data-stu-id="92148-161">Write toohello local file, adding in hello **&lt;html&gt;**, **&lt;header&gt;**, and **&lt;body&gt;** elements.</span></span>

```java
stream.println("<html>");
stream.println("<header/>");
stream.println("<body>");
```

<span data-ttu-id="92148-162">Itere a lista de saudação de blobs carregados.</span><span class="sxs-lookup"><span data-stu-id="92148-162">Iterate through hello list of uploaded blobs.</span></span> <span data-ttu-id="92148-163">Para cada blob no hello HTML da página, crie um  **&lt;img&gt;**  elemento que tem seu **src** atributo enviado à saudação do URI do blob hello, conforme exibido na sua conta de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="92148-163">For each blob, in hello HTML page create an **&lt;img&gt;** element that has its **src** attribute sent to hello URI of hello blob as it exists in your Azure storage account.</span></span>
<span data-ttu-id="92148-164">Embora tenha adicionado apenas uma imagem neste exemplo, se você adicionar mais imagens, este código iteraria todos eles.</span><span class="sxs-lookup"><span data-stu-id="92148-164">Although you added only one image in this sample, if you added more, this code would iterate all of them.</span></span>

<span data-ttu-id="92148-165">Para simplificar, este exemplo assume que cada blob carregado é uma imagem.</span><span class="sxs-lookup"><span data-stu-id="92148-165">For simplicity, this example assumes each uploaded blob is an image.</span></span> <span data-ttu-id="92148-166">Se você atualizou blobs diferentes imagens ou blobs de página em vez de blobs de bloco, ajuste o código de saudação conforme necessário.</span><span class="sxs-lookup"><span data-stu-id="92148-166">If you've updated blobs other than images, or page blobs instead of block blobs, adjust hello code as needed.</span></span>

```java
// Enumerate hello uploaded blobs.
for (ListBlobItem blobItem : container.listBlobs()) {
// List each blob as an <img> element in hello HTML body.
stream.println("<img src='" + blobItem.getUri() + "'/><br/>");
}
```

<span data-ttu-id="92148-167">Olá fechar  **&lt;corpo&gt;**  elemento e hello  **&lt;html&gt;**  elemento.</span><span class="sxs-lookup"><span data-stu-id="92148-167">Close hello **&lt;body&gt;** element and hello **&lt;html&gt;** element.</span></span>

```java
stream.println("</body>");
stream.println("</html>");
```

<span data-ttu-id="92148-168">Arquivo de local de saudação fechar.</span><span class="sxs-lookup"><span data-stu-id="92148-168">Close hello local file.</span></span>

```java
stream.close();
```

<span data-ttu-id="92148-169">Feche **MakeHTMLPage** inserindo um colchete de fechamento: **}**</span><span class="sxs-lookup"><span data-stu-id="92148-169">Close **MakeHTMLPage** by inserting a close bracket: **}**</span></span>

<span data-ttu-id="92148-170">Feche **StorageSample** inserindo um colchete de fechamento: **}**</span><span class="sxs-lookup"><span data-stu-id="92148-170">Close **StorageSample** by inserting a close bracket: **}**</span></span>

<span data-ttu-id="92148-171">a seguir Olá é código completo de saudação para este exemplo.</span><span class="sxs-lookup"><span data-stu-id="92148-171">hello following is hello complete code for this example.</span></span> <span data-ttu-id="92148-172">Lembre-se de valores de espaço reservado de saudação toomodify **sua\_conta\_nome** e **sua\_conta\_chave** toouse seu nome de conta e a conta chave, respectivamente.</span><span class="sxs-lookup"><span data-stu-id="92148-172">Remember toomodify hello placeholder values **your\_account\_name** and **your\_account\_key** toouse your account name and account key, respectively.</span></span>

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

<span data-ttu-id="92148-173">Adição toouploading seu armazenamento de tooAzure do arquivo de imagem local, o código de exemplo hello cria namedindex.html um arquivo local, que pode ser aberto no seu navegador toosee sua imagem carregada.</span><span class="sxs-lookup"><span data-stu-id="92148-173">In addition toouploading your local image file tooAzure storage, hello example code creates a local file namedindex.html, which you can open in your browser toosee your uploaded image.</span></span>

<span data-ttu-id="92148-174">Como código Olá contém o nome da conta e chave de conta, certifique-se de que seu código-fonte é seguro.</span><span class="sxs-lookup"><span data-stu-id="92148-174">Because hello code contains your account name and account key, ensure that your source code is secure.</span></span>

## <a name="toodelete-a-container"></a><span data-ttu-id="92148-175">toodelete um contêiner</span><span class="sxs-lookup"><span data-stu-id="92148-175">toodelete a container</span></span>
<span data-ttu-id="92148-176">Como você é cobrado para armazenamento, você pode querer toodelete o **gettingstarted** contêiner depois que você experimentar este exemplo.</span><span class="sxs-lookup"><span data-stu-id="92148-176">Because you are charged for storage, you may want toodelete the **gettingstarted** container after you are done experimenting with this example.</span></span> <span data-ttu-id="92148-177">toodelete um contêiner, use Olá **CloudBlobContainer.delete** método.</span><span class="sxs-lookup"><span data-stu-id="92148-177">toodelete a container, use hello **CloudBlobContainer.delete** method.</span></span>

```java
container = serviceClient.getContainerReference("gettingstarted");
container.delete();
```

<span data-ttu-id="92148-178">Olá toocall **CloudBlobContainer.delete** método, o processo de saudação de inicialização **CloudStorageAccount**, **ClodBlobClient**, e  **CloudBlobContainer** objetos é Olá mesmo mostrado para o **createIfNotExist** método.</span><span class="sxs-lookup"><span data-stu-id="92148-178">toocall hello **CloudBlobContainer.delete** method, hello process of initializing **CloudStorageAccount**, **ClodBlobClient**, and **CloudBlobContainer** objects is hello same as shown for the **createIfNotExist** method.</span></span> <span data-ttu-id="92148-179">Olá, a seguir é um exemplo completo que exclusões Olá contêiner nomeado **gettingstarted**.</span><span class="sxs-lookup"><span data-stu-id="92148-179">hello following is a complete example that deletes hello container named **gettingstarted**.</span></span>

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

<span data-ttu-id="92148-180">Para obter uma visão geral de outros métodos e classes de armazenamento de blob, consulte [como toouse armazenamento de Blob do Java](storage-java-how-to-use-blob-storage.md).</span><span class="sxs-lookup"><span data-stu-id="92148-180">For an overview of other blob storage classes and methods, see [How toouse Blob storage from Java](storage-java-how-to-use-blob-storage.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="92148-181">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="92148-181">Next steps</span></span>
<span data-ttu-id="92148-182">Siga essas toolearn links mais informações sobre tarefas mais complexas de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="92148-182">Follow these links toolearn more about more complex storage tasks.</span></span>

* [<span data-ttu-id="92148-183">SDK de Armazenamento do Azure para Java</span><span class="sxs-lookup"><span data-stu-id="92148-183">Azure Storage SDK for Java</span></span>](https://github.com/azure/azure-storage-java)
* [<span data-ttu-id="92148-184">Referência de SDK do Cliente de Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="92148-184">Azure Storage Client SDK Reference</span></span>](http://dl.windowsazure.com/storage/javadoc/)
* [<span data-ttu-id="92148-185">API REST de serviços de armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="92148-185">Azure Storage Services REST API</span></span>](https://msdn.microsoft.com/library/azure/dd179355.aspx)
* [<span data-ttu-id="92148-186">Blog da equipe de Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="92148-186">Azure Storage Team Blog</span></span>](http://blogs.msdn.com/b/windowsazurestorage/)

