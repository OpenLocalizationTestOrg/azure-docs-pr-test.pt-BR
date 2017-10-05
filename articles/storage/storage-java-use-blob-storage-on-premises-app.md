---
title: Aplicativo local com armazenamento de blobs (Java) | Microsoft Docs
description: "Saiba como criar um aplicativo de console que carrega uma imagem para o Azure e a exibe no navegador. Amostras de código em Java."
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
ms.openlocfilehash: a172b881fa38a69f4510df94f5797b7a56940c52
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="on-premises-application-with-blob-storage"></a><span data-ttu-id="93d9a-104">Aplicativo local com armazenamento de blob</span><span class="sxs-lookup"><span data-stu-id="93d9a-104">On-premises application with blob storage</span></span>
## <a name="overview"></a><span data-ttu-id="93d9a-105">Visão geral</span><span class="sxs-lookup"><span data-stu-id="93d9a-105">Overview</span></span>
<span data-ttu-id="93d9a-106">O exemplo a seguir mostra como você pode usar o armazenamento do Azure paraarmazenar imagens no Azure.</span><span class="sxs-lookup"><span data-stu-id="93d9a-106">The following example shows you how you can use Azure storage to store images in Azure.</span></span> <span data-ttu-id="93d9a-107">O código deste arquivo é de um aplicativo de console que carrega uma imagem para o Azure e cria um arquivo HTML que exibe a imagem no seu navegador.</span><span class="sxs-lookup"><span data-stu-id="93d9a-107">The code in this article is for a console application that uploads an image to Azure, and then creates an HTML file that displays the image in your browser.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="93d9a-108">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="93d9a-108">Prerequisites</span></span>
* <span data-ttu-id="93d9a-109">Um JDK (Java Developer Kit) versão 1.6 ou posterior deve estar instalado.</span><span class="sxs-lookup"><span data-stu-id="93d9a-109">A Java Developer Kit (JDK), version 1.6 or later, is installed.</span></span>
* <span data-ttu-id="93d9a-110">O SDK do Azure deve estar instalado.</span><span class="sxs-lookup"><span data-stu-id="93d9a-110">The Azure SDK is installed.</span></span>
* <span data-ttu-id="93d9a-111">O JAR das bibliotecas do Azure para Java e todos os JARs de dependência aplicáveis devem estar instalados e no caminho de compilação usado por seu compilador Java.</span><span class="sxs-lookup"><span data-stu-id="93d9a-111">The JAR for the Azure Libraries for Java, and any applicable dependency JARs, are installed and are in the build path used by your Java compiler.</span></span> <span data-ttu-id="93d9a-112">Para saber mais sobre como instalar as bibliotecas do Azure para Java, consulte [Baixar o SDK do Azure para Java](../java-download-azure-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="93d9a-112">For information about installing the Azure Libraries for Java, see [Download the Azure SDK for Java](../java-download-azure-sdk.md).</span></span>
* <span data-ttu-id="93d9a-113">Uma conta de armazenamento do Azure deve ter sido configurada.</span><span class="sxs-lookup"><span data-stu-id="93d9a-113">An Azure storage account has been set up.</span></span> <span data-ttu-id="93d9a-114">O nome e a chave da conta de armazenamento serão usados pelo código deste artigo.</span><span class="sxs-lookup"><span data-stu-id="93d9a-114">The account name and account key for the storage account will be used by the code in this article.</span></span> <span data-ttu-id="93d9a-115">Consulte [Como criar uma Conta de Armazenamento](storage-create-storage-account.md#create-a-storage-account) para obter informações sobre como criar uma conta de armazenamento e [Exibir e copiar chaves de acesso de armazenamento](storage-create-storage-account.md#view-and-copy-storage-access-keys) para obter informações sobre como recuperar a chave de conta.</span><span class="sxs-lookup"><span data-stu-id="93d9a-115">See [How to Create a Storage Account](storage-create-storage-account.md#create-a-storage-account) for information about creating a storage account, and [View and copy storage access keys](storage-create-storage-account.md#view-and-copy-storage-access-keys) for information about retrieving the account key.</span></span>
* <span data-ttu-id="93d9a-116">Você criou um arquivo de imagem local armazenado no caminho c:\\myimages\\image1.jpg.</span><span class="sxs-lookup"><span data-stu-id="93d9a-116">You have created a local image file named stored at the path c:\\myimages\\image1.jpg.</span></span> <span data-ttu-id="93d9a-117">Como alternativa, modifique o construtor **FileInputStream** no exemplo para usar um caminho de imagem e um nome de arquivo diferentes.</span><span class="sxs-lookup"><span data-stu-id="93d9a-117">Alternatively, modify the **FileInputStream** constructor in the example to use a different image path and file name.</span></span>

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

## <a name="to-use-azure-blob-storage-to-upload-a-file"></a><span data-ttu-id="93d9a-118">Para usar o armazenamento de blobs do Azure para carregar um arquivo</span><span class="sxs-lookup"><span data-stu-id="93d9a-118">To use Azure blob storage to upload a file</span></span>
<span data-ttu-id="93d9a-119">Um procedimento passo a passo é apresentado aqui.</span><span class="sxs-lookup"><span data-stu-id="93d9a-119">A step-by-step procedure is presented here.</span></span> <span data-ttu-id="93d9a-120">Se você quiser pular, todo o código será apresentado mais tarde neste artigo.</span><span class="sxs-lookup"><span data-stu-id="93d9a-120">If you'd like to skip ahead, the entire code is presented later in this article.</span></span>

<span data-ttu-id="93d9a-121">Inicie o código incluindo as importações das principais classes de armazenamento do Azure, as classes de cliente do blob do Azure, as classes de E/S de Java e a classe **URISyntaxException** .</span><span class="sxs-lookup"><span data-stu-id="93d9a-121">Begin the code by including imports for the Azure core storage classes, the Azure blob client classes, the Java IO classes, and the **URISyntaxException** class.</span></span>

```java
import com.microsoft.azure.storage.*;
import com.microsoft.azure.storage.blob.*;
import java.io.*;
import java.net.URISyntaxException;
```

<span data-ttu-id="93d9a-122">Declare uma classe chamada **StorageSample** e inclua o colchete de abertura, **{**.</span><span class="sxs-lookup"><span data-stu-id="93d9a-122">Declare a class named **StorageSample**, and include the open bracket, **{**.</span></span>

```java
public class StorageSample {
```

<span data-ttu-id="93d9a-123">Na classe **StorageSample** , declare uma variável de cadeia de caracteres que conterá o protocolo de ponto de extremidade padrão, o nome da sua conta de armazenamento e a sua chave de acesso de armazenamento, conforme especificado na conta de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="93d9a-123">Within the **StorageSample** class, declare a string variable that will contain the default endpoint protocol, your storage account name, and your storage access key, as specified in your Azure storage account.</span></span> <span data-ttu-id="93d9a-124">Substitua os valores dos espaços reservados **nome\_da\_conta** e **chave\_da\_conta** pelo nome da sua conta e por sua chave de conta, respectivamente.</span><span class="sxs-lookup"><span data-stu-id="93d9a-124">Replace the placeholder values **your\_account\_name** and **your\_account\_key** with your own account name and account key, respectively.</span></span>

```java
public static final String storageConnectionString =
    "DefaultEndpointsProtocol=http;" +
    "AccountName=your_account_name;" +
    "AccountKey=your_account_name";
```

<span data-ttu-id="93d9a-125">Adicione sua declaração para **main**, inclua um bloco **try** e inclua os colchetes de abertura necessários, **{**.</span><span class="sxs-lookup"><span data-stu-id="93d9a-125">Add in your declaration for **main**, include a **try** block, and include the necessary open brackets, **{**.</span></span>

```java
    public static void main(String[] args)
    {
        try
        {
```

<span data-ttu-id="93d9a-126">Declare as variáveis do tipo a seguir (as descrições são sobre como elas são usadas neste exemplo):</span><span class="sxs-lookup"><span data-stu-id="93d9a-126">Declare variables of the following type (the descriptions are for how they are used in this example):</span></span>

* <span data-ttu-id="93d9a-127">**CloudStorageAccount**: usada para inicializar o objeto de conta com o nome e a chave da sua conta de armazenamento do Azure e para criar o objeto de cliente do blob.</span><span class="sxs-lookup"><span data-stu-id="93d9a-127">**CloudStorageAccount**: Used to initialize the account object with your Azure storage account name and key, and to create the blob client object.</span></span>
* <span data-ttu-id="93d9a-128">**CloudBlobClient**: usada para acessar o serviço Blob.</span><span class="sxs-lookup"><span data-stu-id="93d9a-128">**CloudBlobClient**: Used to access the blob service.</span></span>
* <span data-ttu-id="93d9a-129">**CloudBlobContainer**: usada para criar um contêiner de blobs, listar os blobs no contêiner e excluir o contêiner.</span><span class="sxs-lookup"><span data-stu-id="93d9a-129">**CloudBlobContainer**: Used to create a blob container, list the blobs in the container, and delete the container.</span></span>
* <span data-ttu-id="93d9a-130">**CloudBlockBlob**: usada para carregar um arquivo de imagem local para o contêiner.</span><span class="sxs-lookup"><span data-stu-id="93d9a-130">**CloudBlockBlob**: Used to upload a local image file to the container.</span></span>

<!-- -->

```java
    CloudStorageAccount account;
    CloudBlobClient serviceClient;
    CloudBlobContainer container;
    CloudBlockBlob blob;
```

<span data-ttu-id="93d9a-131">Atribua um valor à variável **account** .</span><span class="sxs-lookup"><span data-stu-id="93d9a-131">Assign a value to the **account** variable.</span></span>

```java
account = CloudStorageAccount.parse(storageConnectionString);
```

<span data-ttu-id="93d9a-132">Atribua um valor à variável **serviceClient** .</span><span class="sxs-lookup"><span data-stu-id="93d9a-132">Assign a value to the **serviceClient** variable.</span></span>

```java
serviceClient = account.createCloudBlobClient();
```

<span data-ttu-id="93d9a-133">Atribua um valor à variável **container** .</span><span class="sxs-lookup"><span data-stu-id="93d9a-133">Assign a value to the **container** variable.</span></span> <span data-ttu-id="93d9a-134">Obteremos uma referência para um contêiner chamado **gettingstarted**.</span><span class="sxs-lookup"><span data-stu-id="93d9a-134">We'll get a reference to a container named **gettingstarted**.</span></span>

```java
// Container name must be lower case.
container = serviceClient.getContainerReference("gettingstarted");
```

<span data-ttu-id="93d9a-135">Crie o contêiner.</span><span class="sxs-lookup"><span data-stu-id="93d9a-135">Create the container.</span></span> <span data-ttu-id="93d9a-136">Esse método criará o contêiner se ele ainda não existir (e retornará **true**).</span><span class="sxs-lookup"><span data-stu-id="93d9a-136">This method will create the container if it doesn't exist (and return **true**).</span></span> <span data-ttu-id="93d9a-137">Se o contêiner existir, retornará **false**.</span><span class="sxs-lookup"><span data-stu-id="93d9a-137">If the container does exist, it will return **false**.</span></span> <span data-ttu-id="93d9a-138">Uma alternativa para **createIfNotExists** é o método **create** (que retornará um erro se o contêiner já existir).</span><span class="sxs-lookup"><span data-stu-id="93d9a-138">An alternative to **createIfNotExists** is the **create** method (which will return an error if the container already exists).</span></span>

```java
container.createIfNotExists();
```

<span data-ttu-id="93d9a-139">Definir acesso anônimo para o contêiner.</span><span class="sxs-lookup"><span data-stu-id="93d9a-139">Set anonymous access for the container.</span></span>

```java
// Set anonymous access on the container.
BlobContainerPermissions containerPermissions;
containerPermissions = new BlobContainerPermissions();
containerPermissions.setPublicAccess(BlobContainerPublicAccessType.CONTAINER);
container.uploadPermissions(containerPermissions);
```

<span data-ttu-id="93d9a-140">Obtenha uma referência para o blob de blocos, que representará o blob no armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="93d9a-140">Get a reference to the block blob, which will represent the blob in Azure storage.</span></span>

```java
blob = container.getBlockBlobReference("image1.jpg");
```

<span data-ttu-id="93d9a-141">Use o construtor **File** para obter uma referência para o arquivo criado localmente que será carregado.</span><span class="sxs-lookup"><span data-stu-id="93d9a-141">Use the **File** constructor to get a reference to the locally created file that you will upload.</span></span> <span data-ttu-id="93d9a-142">Certifique-se de criar esse arquivo antes de executar o código.</span><span class="sxs-lookup"><span data-stu-id="93d9a-142">Ensure you have created this file before running the code.</span></span>

```java
File fileReference = new File ("c:\\myimages\\image1.jpg");
```

<span data-ttu-id="93d9a-143">Carregue o arquivo local por meio de uma chamada para o método **CloudBlockBlob.upload** .</span><span class="sxs-lookup"><span data-stu-id="93d9a-143">Upload the local file through a call to the **CloudBlockBlob.upload** method.</span></span> <span data-ttu-id="93d9a-144">O primeiro parâmetro do método **CloudBlockBlob.upload** é um objeto **FileInputStream** que representa o arquivo local que será carregado para o armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="93d9a-144">The first parameter to the **CloudBlockBlob.upload** method is a **FileInputStream** object that represents the local file that will be uploaded to Azure storage.</span></span> <span data-ttu-id="93d9a-145">O segundo parâmetro é o tamanho, em bytes, do arquivo.</span><span class="sxs-lookup"><span data-stu-id="93d9a-145">The second parameter is the size, in bytes, of the file.</span></span>

```java
blob.upload(new FileInputStream(fileReference), fileReference.length());
```

<span data-ttu-id="93d9a-146">Chame uma função auxiliar denominada **MakeHTMLPage** para fazer uma página HTML básica que contém um elemento **&lt;image&gt;** com a origem definida para o blob que agora está em sua conta de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="93d9a-146">Call a helper function named **MakeHTMLPage**, to make a basic HTML page that contains an **&lt;image&gt;** element with the source set to the blob that is now in your Azure storage account.</span></span> <span data-ttu-id="93d9a-147">O código de **MakeHTMLPage** será discutido posteriormente neste artigo.</span><span class="sxs-lookup"><span data-stu-id="93d9a-147">The code for **MakeHTMLPage** will be discussed later in this article.</span></span>

```java
MakeHTMLPage(container);
```

<span data-ttu-id="93d9a-148">Imprima uma mensagem de status e informações sobre a página HTML criada.</span><span class="sxs-lookup"><span data-stu-id="93d9a-148">Print out a status message and information about the created HTML page.</span></span>

```java
System.out.println("Processing complete.");
System.out.println("Open index.html to see the images stored in your storage account.");
```

<span data-ttu-id="93d9a-149">Feche o bloco **try** inserindo um colchete de fechamento: **}**</span><span class="sxs-lookup"><span data-stu-id="93d9a-149">Close the **try** block by inserting a close bracket: **}**</span></span>

<span data-ttu-id="93d9a-150">Utilize as seguintes exceções:</span><span class="sxs-lookup"><span data-stu-id="93d9a-150">Handle the following exceptions:</span></span>

* <span data-ttu-id="93d9a-151">**FileNotFoundException**: pode ser gerada pelos construtores **FileInputStream** ou **FileOutputStream**.</span><span class="sxs-lookup"><span data-stu-id="93d9a-151">**FileNotFoundException**: Can be thrown by the **FileInputStream** or **FileOutputStream** constructors.</span></span>
* <span data-ttu-id="93d9a-152">**StorageException**: pode ser gerada pela biblioteca de armazenamento de cliente do Azure.</span><span class="sxs-lookup"><span data-stu-id="93d9a-152">**StorageException**: Can be thrown by the Azure client storage library.</span></span>
* <span data-ttu-id="93d9a-153">**URISyntaxException**: pode ser gerada pelo método **ListBlobItem.getUri**.</span><span class="sxs-lookup"><span data-stu-id="93d9a-153">**URISyntaxException**: Can be thrown by the **ListBlobItem.getUri** method.</span></span>
* <span data-ttu-id="93d9a-154">**Exception**: manipulação de exceção genérica.</span><span class="sxs-lookup"><span data-stu-id="93d9a-154">**Exception**: Generic exception handling.</span></span>

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

<span data-ttu-id="93d9a-155">Feche **main** inserindo um colchete de fechamento: **}**</span><span class="sxs-lookup"><span data-stu-id="93d9a-155">Close **main** by inserting a close bracket: **}**</span></span>

<span data-ttu-id="93d9a-156">Crie um método chamado **MakeHTMLPage** para criar uma página HTML básica.</span><span class="sxs-lookup"><span data-stu-id="93d9a-156">Create a method named **MakeHTMLPage** to create a basic HTML page.</span></span> <span data-ttu-id="93d9a-157">Esse método tem um parâmetro do tipo **CloudBlobContainer**, que será usado para iterar pela lista de blobs carregados.</span><span class="sxs-lookup"><span data-stu-id="93d9a-157">This method has a parameter of type **CloudBlobContainer**, which will be used to iterate through the list of uploaded blobs.</span></span> <span data-ttu-id="93d9a-158">Esse método gerará exceções do tipo **FileNotFoundException**, que podem ser geradas pelo construtor **FileOutputStream** e **URISyntaxException**, que podem ser geradas pelo método **ListBlobItem.getUri**.</span><span class="sxs-lookup"><span data-stu-id="93d9a-158">This method will throw exceptions of type **FileNotFoundException**, which can be thrown by the **FileOutputStream** constructor, and **URISyntaxException**, which can be thrown by the **ListBlobItem.getUri** method.</span></span> <span data-ttu-id="93d9a-159">Inclua o colchete de abertura, **{**.</span><span class="sxs-lookup"><span data-stu-id="93d9a-159">Include the opening bracket, **{**.</span></span>

```java
public static void MakeHTMLPage(CloudBlobContainer container) throws FileNotFoundException, URISyntaxException
{
```

<span data-ttu-id="93d9a-160">Crie um arquivo local chamado **index.html**.</span><span class="sxs-lookup"><span data-stu-id="93d9a-160">Create a local file named **index.html**.</span></span>

```java
PrintStream stream;
stream = new PrintStream(new FileOutputStream("index.html"));
```

<span data-ttu-id="93d9a-161">Escreva no arquivo local, adicionando os elementos **&lt;html&gt;**, **&lt;header&gt;** e **&lt;body&gt;**.</span><span class="sxs-lookup"><span data-stu-id="93d9a-161">Write to the local file, adding in the **&lt;html&gt;**, **&lt;header&gt;**, and **&lt;body&gt;** elements.</span></span>

```java
stream.println("<html>");
stream.println("<header/>");
stream.println("<body>");
```

<span data-ttu-id="93d9a-162">Itere pela lista de blobs carregados.</span><span class="sxs-lookup"><span data-stu-id="93d9a-162">Iterate through the list of uploaded blobs.</span></span> <span data-ttu-id="93d9a-163">Para cada blob, na página HTML crie um elemento **&lt;img&gt;** que tenha seu atributo **src** enviado para o URI do blob, conforme ele existe em sua conta de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="93d9a-163">For each blob, in the HTML page create an **&lt;img&gt;** element that has its **src** attribute sent to the URI of the blob as it exists in your Azure storage account.</span></span>
<span data-ttu-id="93d9a-164">Embora tenha adicionado apenas uma imagem neste exemplo, se você adicionar mais imagens, este código iteraria todos eles.</span><span class="sxs-lookup"><span data-stu-id="93d9a-164">Although you added only one image in this sample, if you added more, this code would iterate all of them.</span></span>

<span data-ttu-id="93d9a-165">Para simplificar, este exemplo assume que cada blob carregado é uma imagem.</span><span class="sxs-lookup"><span data-stu-id="93d9a-165">For simplicity, this example assumes each uploaded blob is an image.</span></span> <span data-ttu-id="93d9a-166">Se você tiver atualizado blobs que não sejam imagens, ou blobs de páginas, em vez de blobs de blocos, ajuste o código conforme o necessário.</span><span class="sxs-lookup"><span data-stu-id="93d9a-166">If you've updated blobs other than images, or page blobs instead of block blobs, adjust the code as needed.</span></span>

```java
// Enumerate the uploaded blobs.
for (ListBlobItem blobItem : container.listBlobs()) {
// List each blob as an <img> element in the HTML body.
stream.println("<img src='" + blobItem.getUri() + "'/><br/>");
}
```

<span data-ttu-id="93d9a-167">Feche os elementos **&lt;body&gt;** e **&lt;html&gt;**.</span><span class="sxs-lookup"><span data-stu-id="93d9a-167">Close the **&lt;body&gt;** element and the **&lt;html&gt;** element.</span></span>

```java
stream.println("</body>");
stream.println("</html>");
```

<span data-ttu-id="93d9a-168">Feche o arquivo local.</span><span class="sxs-lookup"><span data-stu-id="93d9a-168">Close the local file.</span></span>

```java
stream.close();
```

<span data-ttu-id="93d9a-169">Feche **MakeHTMLPage** inserindo um colchete de fechamento: **}**</span><span class="sxs-lookup"><span data-stu-id="93d9a-169">Close **MakeHTMLPage** by inserting a close bracket: **}**</span></span>

<span data-ttu-id="93d9a-170">Feche **StorageSample** inserindo um colchete de fechamento: **}**</span><span class="sxs-lookup"><span data-stu-id="93d9a-170">Close **StorageSample** by inserting a close bracket: **}**</span></span>

<span data-ttu-id="93d9a-171">A seguir está o código completo deste exemplo.</span><span class="sxs-lookup"><span data-stu-id="93d9a-171">The following is the complete code for this example.</span></span> <span data-ttu-id="93d9a-172">Modifique os valores dos espaços reservados **nome\_da\_conta** e **chave\_da\_conta** para usar o nome da sua conta e a sua chave de conta, respectivamente.</span><span class="sxs-lookup"><span data-stu-id="93d9a-172">Remember to modify the placeholder values **your\_account\_name** and **your\_account\_key** to use your account name and account key, respectively.</span></span>

```java
import com.microsoft.azure.storage.*;
import com.microsoft.azure.storage.blob.*;
import java.io.*;
import java.net.URISyntaxException;

// Create an image, c:\myimages\image1.jpg, prior to running this sample.
// Alternatively, change the value used by the FileInputStream constructor
// to use a different image path and file that you have already created.
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

            // Set anonymous access on the container.
            BlobContainerPermissions containerPermissions;
            containerPermissions = new BlobContainerPermissions();
            containerPermissions.setPublicAccess(BlobContainerPublicAccessType.CONTAINER);
            container.uploadPermissions(containerPermissions);

            // Upload an image file.
            blob = container.getBlockBlobReference("image1.jpg");

            File fileReference = new File("c:\\myimages\\image1.jpg");
            blob.upload(new FileInputStream(fileReference), fileReference.length());

            // At this point the image is uploaded.
            // Next, create an HTML page that lists all of the uploaded images.
            MakeHTMLPage(container);

            System.out.println("Processing complete.");
            System.out.println("Open index.html to see the images stored in your storage account.");

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

    // Create an HTML page that can be used to display the uploaded images.
    // This example assumes all of the blobs are for images.
    public static void MakeHTMLPage(CloudBlobContainer container) throws FileNotFoundException, URISyntaxException
    {
        PrintStream stream;
        stream = new PrintStream(new FileOutputStream("index.html"));

        // Create the opening <html>, <header>, and <body> elements.
        stream.println("<html>");
        stream.println("<header/>");
        stream.println("<body>");

        // Enumerate the uploaded blobs.
        for (ListBlobItem blobItem : container.listBlobs()) {
            // List each blob as an <img> element in the HTML body.
            stream.println("<img src='" + blobItem.getUri() + "'/><br/>");
        }

        stream.println("</body>");

        // Complete the <html> element and close the file.
        stream.println("</html>");
        stream.close();
    }
}
```

<span data-ttu-id="93d9a-173">Além de carregar o arquivo de imagem local para o armazenamento do Azure, esse código de exemplo cria um arquivo local chamado namedindex.html, que você pode abrir no navegador para ver a sua imagem carregada.</span><span class="sxs-lookup"><span data-stu-id="93d9a-173">In addition to uploading your local image file to Azure storage, the example code creates a local file namedindex.html, which you can open in your browser to see your uploaded image.</span></span>

<span data-ttu-id="93d9a-174">Como o código contém o nome e a chave da sua conta, certifique-se de que seu código-fonte seja seguro.</span><span class="sxs-lookup"><span data-stu-id="93d9a-174">Because the code contains your account name and account key, ensure that your source code is secure.</span></span>

## <a name="to-delete-a-container"></a><span data-ttu-id="93d9a-175">Para excluir um contêiner</span><span class="sxs-lookup"><span data-stu-id="93d9a-175">To delete a container</span></span>
<span data-ttu-id="93d9a-176">Como você é cobrado pelo armazenamento, talvez queira excluir o contêiner **gettingstarted** após concluir os testes com este exemplo.</span><span class="sxs-lookup"><span data-stu-id="93d9a-176">Because you are charged for storage, you may want to delete the **gettingstarted** container after you are done experimenting with this example.</span></span> <span data-ttu-id="93d9a-177">Para excluir um contêiner, use o método **CloudBlobContainer.delete** .</span><span class="sxs-lookup"><span data-stu-id="93d9a-177">To delete a container, use the **CloudBlobContainer.delete** method.</span></span>

```java
container = serviceClient.getContainerReference("gettingstarted");
container.delete();
```

<span data-ttu-id="93d9a-178">Para chamar o método**CloudBlobContainer.delete**, o processo de inicializar objetos **CloudStorageAccount**, **ClodBlobClient** e **CloudBlobContainer** é o mesmo mostrado para o método **createIfNotExist**.</span><span class="sxs-lookup"><span data-stu-id="93d9a-178">To call the **CloudBlobContainer.delete** method, the process of initializing **CloudStorageAccount**, **ClodBlobClient**, and **CloudBlobContainer** objects is the same as shown for the **createIfNotExist** method.</span></span> <span data-ttu-id="93d9a-179">A seguir é fornecido um exemplo completo que exclui o contêiner chamado **gettingstarted**.</span><span class="sxs-lookup"><span data-stu-id="93d9a-179">The following is a complete example that deletes the container named **gettingstarted**.</span></span>

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

<span data-ttu-id="93d9a-180">Para obter uma visão geral de outras classes e outros métodos de armazenamento de blobs, consulte [Como usar o Armazenamento de Blobs do Java](storage-java-how-to-use-blob-storage.md).</span><span class="sxs-lookup"><span data-stu-id="93d9a-180">For an overview of other blob storage classes and methods, see [How to use Blob storage from Java](storage-java-how-to-use-blob-storage.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="93d9a-181">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="93d9a-181">Next steps</span></span>
<span data-ttu-id="93d9a-182">Siga estes links para saber mais sobre as tarefas mais complexas de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="93d9a-182">Follow these links to learn more about more complex storage tasks.</span></span>

* [<span data-ttu-id="93d9a-183">SDK de Armazenamento do Azure para Java</span><span class="sxs-lookup"><span data-stu-id="93d9a-183">Azure Storage SDK for Java</span></span>](https://github.com/azure/azure-storage-java)
* [<span data-ttu-id="93d9a-184">Referência de SDK do Cliente de Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="93d9a-184">Azure Storage Client SDK Reference</span></span>](http://dl.windowsazure.com/storage/javadoc/)
* [<span data-ttu-id="93d9a-185">API REST de serviços de armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="93d9a-185">Azure Storage Services REST API</span></span>](https://msdn.microsoft.com/library/azure/dd179355.aspx)
* [<span data-ttu-id="93d9a-186">Blog da equipe de Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="93d9a-186">Azure Storage Team Blog</span></span>](http://blogs.msdn.com/b/windowsazurestorage/)

