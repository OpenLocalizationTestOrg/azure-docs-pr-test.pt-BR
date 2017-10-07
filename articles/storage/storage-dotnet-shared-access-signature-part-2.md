---
title: aaaCreate e usar uma assinatura de acesso compartilhado (SAS) com o armazenamento de BLOBs do Azure | Microsoft Docs
description: Este tutorial mostra como toocreate compartilhado assinaturas de acesso para uso com o armazenamento de Blob e tooconsume-los em seus aplicativos cliente.
services: storage
documentationcenter: 
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: 491e0b3c-76d4-4149-9a80-bbbd683b1f3e
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 05/15/2017
ms.author: marsma
ms.openlocfilehash: 629f5c0aee3f41115a0d514a2010d8cc0187126d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="shared-access-signatures-part-2-create-and-use-a-sas-with-blob-storage"></a>Assinaturas de Acesso Compartilhado, Parte 2: criar e usar uma SAS com o Armazenamento de Blobs

[Parte 1](storage-dotnet-shared-access-signature-part-1.md) deste tutorial explorou as assinaturas de acesso compartilhado (SAS) e explicou as práticas recomendadas para sua utilização. Parte 2 mostra como toogenerate e usar o acesso compartilhado assinaturas com armazenamento de Blob. exemplos de saudação são escritos em c# e usam Olá biblioteca de cliente de armazenamento do Azure para .NET. exemplos de saudação neste tutorial:

* Geram uma assinatura de acesso compartilhado em um contêiner
* Geram uma assinatura de acesso compartilhado em um blob
* Criar assinaturas de toomanage de política de um acesso armazenado nos recursos do contêiner
* Assinaturas de acesso compartilhada de saudação de teste em um aplicativo cliente

## <a name="about-this-tutorial"></a>Sobre este tutorial
Neste tutorial, criamos dois aplicativos de console que demonstram a criação e uso de assinaturas de acesso compartilhado para contêineres e blobs:

**Aplicativo 1**: Olá aplicativo de gerenciamento. Gera uma assinatura de acesso compartilhado para um contêiner e um blob. Inclui a chave de acesso da conta de armazenamento Olá no código-fonte.

**Aplicativo 2**: Olá aplicativo cliente. Acessa contêiner e blob recursos usando assinaturas de acesso Olá compartilhado criadas com o aplicativo primeiro hello. Usa apenas Olá acesso compartilhado assinaturas tooaccess contêiner e recursos de blob – ele faz *não* incluem a chave de acesso da conta de armazenamento hello.

## <a name="part-1-create-a-console-application-toogenerate-shared-access-signatures"></a>Parte 1: Criar assinaturas de um acesso de toogenerate compartilhado do aplicativo de console
Primeiro, certifique-se de que você tenha Olá biblioteca de cliente de armazenamento do Azure para .NET instalado. Você pode instalar Olá [pacote NuGet](http://nuget.org/packages/WindowsAzure.Storage/ "pacote NuGet") que contêm assemblies de hello mais atualizados para a biblioteca de saudação do cliente. Isso é hello recomendado método para garantir que você tenha as correções mais recentes hello. Você também pode baixar a biblioteca de saudação do cliente como parte da versão mais recente de saudação do hello [SDK do Azure para .NET](https://azure.microsoft.com/downloads/).

No Visual Studio, crie um novo aplicativo de console do Windows e dê a ele o nome **GenerateSharedAccessSignatures**. Adicione referências muito[Microsoft.WindowsAzure.ConfigurationManager](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager) e [windowsazure](https://www.nuget.org/packages/WindowsAzure.Storage/) usando uma saudação abordagens a seguir:

* Saudação de uso [Gerenciador de pacotes do NuGet](https://docs.nuget.org/consume/installing-nuget) no Visual Studio. Selecione **Projeto** > **Gerenciar Pacotes do NuGet**, pesquise online por cada pacote (Microsoft.WindowsAzure.ConfigurationManager e WindowsAzure.Storage) e instale-os.
* Como alternativa, localize esses assemblies em sua instalação de saudação do SDK do Azure e adicionar referências toothem:
  * Microsoft.WindowsAzure.Configuration.dll
  * Microsoft.WindowsAzure.Storage.dll

Na parte superior de saudação do arquivo do hello Program.cs, adicione o seguinte de Olá **usando** diretivas:

```csharp
using System.IO;
using Microsoft.Azure;
using Microsoft.WindowsAzure.Storage;
using Microsoft.WindowsAzure.Storage.Blob;
```

Edite o arquivo App. config de saudação para que ele contém uma definição de configuração com uma cadeia de caracteres de conexão que aponta tooyour conta de armazenamento. O arquivo App. config deve ser semelhante toothis um:

```xml
<configuration>
  <startup>
    <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.5.2" />
  </startup>
  <appSettings>
    <add key="StorageConnectionString" value="DefaultEndpointsProtocol=https;AccountName=myaccount;AccountKey=mykey"/>
  </appSettings>
</configuration>
```

### <a name="generate-a-shared-access-signature-uri-for-a-container"></a>Gerar um URI de assinatura de acesso compartilhado para um contêiner
toobegin com, podemos adicionar um método toogenerate uma assinatura de acesso compartilhado em um novo contêiner. Nesse caso, assinatura de saudação não está associada uma política de acesso armazenada, portanto ele realiza a saudação informações de saudação do URI indicando suas permissões de saudação e de tempo de expiração, ele concede.

Primeiro, adicione o código toohello **Main** método tooauthenticate acessar tooyour conta de armazenamento e criar um novo contêiner:

```csharp
static void Main(string[] args)
{
    //Parse hello connection string and return a reference toohello storage account.
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(CloudConfigurationManager.GetSetting("StorageConnectionString"));

    //Create hello blob client object.
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

    //Get a reference tooa container toouse for hello sample code, and create it if it does not exist.
    CloudBlobContainer container = blobClient.GetContainerReference("sascontainer");
    container.CreateIfNotExists();

    //Insert calls toohello methods created below here...

    //Require user input before closing hello console window.
    Console.ReadLine();
}
```

Em seguida, adicione um método que gera a assinatura de acesso compartilhado de saudação do contêiner hello e retorna o URI de assinatura de saudação:

```csharp
static string GetContainerSasUri(CloudBlobContainer container)
{
    //Set hello expiry time and permissions for hello container.
    //In this case no start time is specified, so hello shared access signature becomes valid immediately.
    SharedAccessBlobPolicy sasConstraints = new SharedAccessBlobPolicy();
    sasConstraints.SharedAccessExpiryTime = DateTimeOffset.UtcNow.AddHours(24);
    sasConstraints.Permissions = SharedAccessBlobPermissions.List | SharedAccessBlobPermissions.Write;

    //Generate hello shared access signature on hello container, setting hello constraints directly on hello signature.
    string sasContainerToken = container.GetSharedAccessSignature(sasConstraints);

    //Return hello URI string for hello container, including hello SAS token.
    return container.Uri + sasContainerToken;
}
```

Adicionar Olá linhas na parte inferior de saudação do hello seguintes **Main ()** método, antes de chamar de saudação muito**Console.ReadLine()**, toocall **GetContainerSasUri()** e escrever "hello" janela do console de toohello URI de assinatura:

```csharp
//Generate a SAS URI for hello container, without a stored access policy.
Console.WriteLine("Container SAS URI: " + GetContainerSasUri(container));
Console.WriteLine();
```

Compile e execute a assinatura de acesso compartilhado toooutput Olá URI para o novo contêiner de saudação. Olá URI será a seguir toohello semelhante:

```
https://storageaccount.blob.core.windows.net/sascontainer?sv=2012-02-12&se=2013-04-13T00%3A12%3A08Z&sr=c&sp=wl&sig=t%2BbzU9%2B7ry4okULN9S0wst%2F8MCUhTjrHyV9rDNLSe8g%3D
```

Depois de executar o código de saudação, você criou para o contêiner de saudação de assinatura de acesso compartilhado Olá será válida para Olá próximas 24 horas. assinatura de saudação concede a um cliente blobs toolist permissão Olá contêineres e toowrite novos blobs toohello.

### <a name="generate-a-shared-access-signature-uri-for-a-blob"></a>Gerar um URI de assinatura de acesso compartilhado para um blob
Em seguida, podemos gravar toocreate de código semelhante um novo blob no contêiner de saudação e gerar uma assinatura de acesso compartilhado para ele. Essa assinatura de acesso compartilhado não está associada uma política de acesso armazenada, para que ela inclua a hora de início hello, tempo de expiração e informações de permissão em Olá URI.

Adicione um novo método que cria um novo blob e grava alguns tooit de texto, em seguida, gera uma assinatura de acesso compartilhado e retorna o URI de assinatura de saudação:

```csharp
static string GetBlobSasUri(CloudBlobContainer container)
{
    //Get a reference tooa blob within hello container.
    CloudBlockBlob blob = container.GetBlockBlobReference("sasblob.txt");

    //Upload text toohello blob. If hello blob does not yet exist, it will be created.
    //If hello blob does exist, its existing content will be overwritten.
    string blobContent = "This blob will be accessible tooclients via a shared access signature (SAS).";
    blob.UploadText(blobContent);

    //Set hello expiry time and permissions for hello blob.
    //In this case, hello start time is specified as a few minutes in hello past, toomitigate clock skew.
    //hello shared access signature will be valid immediately.
    SharedAccessBlobPolicy sasConstraints = new SharedAccessBlobPolicy();
    sasConstraints.SharedAccessStartTime = DateTimeOffset.UtcNow.AddMinutes(-5);
    sasConstraints.SharedAccessExpiryTime = DateTimeOffset.UtcNow.AddHours(24);
    sasConstraints.Permissions = SharedAccessBlobPermissions.Read | SharedAccessBlobPermissions.Write;

    //Generate hello shared access signature on hello blob, setting hello constraints directly on hello signature.
    string sasBlobToken = blob.GetSharedAccessSignature(sasConstraints);

    //Return hello URI string for hello container, including hello SAS token.
    return blob.Uri + sasBlobToken;
}
```

Na parte inferior de saudação do hello **Main ()** método, adicione Olá toocall linhas a seguir **GetBlobSasUri()**, antes de chamar de saudação muito**Console.ReadLine()**e gravar Olá compartilhado janela de console toohello do URI de assinatura de acesso:

```csharp
//Generate a SAS URI for a blob within hello container, without a stored access policy.
Console.WriteLine("Blob SAS URI: " + GetBlobSasUri(container));
Console.WriteLine();
```

Compile e execute a assinatura de acesso compartilhado toooutput Olá URI para o novo blob de saudação. Olá URI será a seguir toohello semelhante:

```
https://storageaccount.blob.core.windows.net/sascontainer/sasblob.txt?sv=2012-02-12&st=2013-04-12T23%3A37%3A08Z&se=2013-04-13T00%3A12%3A08Z&sr=b&sp=rw&sig=dF2064yHtc8RusQLvkQFPItYdeOz3zR8zHsDMBi4S30%3D
```

### <a name="create-a-stored-access-policy-on-hello-container"></a>Criar uma política de acesso armazenado no contêiner de saudação
Agora vamos criar uma política de acesso armazenado no contêiner de saudação, que definirá as restrições de saudação para nenhuma assinatura de acesso compartilhado que estão associada ele.

Nos exemplos anteriores do hello, especificamos hora de início da saudação (implícita ou explicitamente), tempo de expiração de saudação e permissões Olá Olá compartilhado assinatura de acesso URI em si. Olá exemplos a seguir, podemos especificar esses na política de acesso de saudação armazenada, não na assinatura de acesso compartilhado hello. Isso permite que nós toochange essas restrições sem emitir novamente Olá compartilhadas acessar a assinatura.

É possível toohave uma ou mais das restrições de saudação na assinatura de acesso compartilhado Olá e restante Olá na política de acesso de saudação armazenada. No entanto, você só pode especificar a hora de início hello, tempo de expiração e permissões em um local ou Olá outros. Por exemplo, você não pode especificar permissões na assinatura de acesso compartilhado hello e também especificá-los na política de acesso de saudação armazenada.

Quando você adicionar um contêiner de tooa de política de acesso armazenada, obter as permissões existentes do contêiner hello, adicionar nova política de acesso hello e, em seguida, definir permissões do contêiner de saudação.

Adicione um novo método que cria uma nova política de acesso armazenada em um contêiner e retorna o nome de saudação da política de saudação:

```csharp
static void CreateSharedAccessPolicy(CloudBlobClient blobClient, CloudBlobContainer container,
    string policyName)
{
    //Get hello container's existing permissions.
    BlobContainerPermissions permissions = container.GetPermissions();

    //Create a new shared access policy and define its constraints.
    SharedAccessBlobPolicy sharedPolicy = new SharedAccessBlobPolicy()
    {
        SharedAccessExpiryTime = DateTimeOffset.UtcNow.AddHours(24),
        Permissions = SharedAccessBlobPermissions.Write | SharedAccessBlobPermissions.List | SharedAccessBlobPermissions.Read
    };

    //Add hello new policy toohello container's permissions, and set hello container's permissions.
    permissions.SharedAccessPolicies.Add(policyName, sharedPolicy);
    container.SetPermissions(permissions);
}
```

Na parte inferior de saudação do hello **Main ()** método, antes de chamar de saudação muito**Console.ReadLine()**, adicione Olá seguir linhas toofirst desmarque quaisquer políticas de acesso existentes e, em seguida, chamar hello  **CreateSharedAccessPolicy()** método:

```csharp
//Clear any existing access policies on container.
BlobContainerPermissions perms = container.GetPermissions();
perms.SharedAccessPolicies.Clear();
container.SetPermissions(perms);

//Create a new access policy on hello container, which may be optionally used tooprovide constraints for
//shared access signatures on hello container and hello blob.
string sharedAccessPolicyName = "tutorialpolicy";
CreateSharedAccessPolicy(blobClient, container, sharedAccessPolicyName);
```

Quando você limpa as políticas de acesso de saudação em um contêiner, primeiro deve obter permissões existentes do contêiner Olá e permissões Olá limpar e definir permissões de saudação novamente.

### <a name="generate-a-shared-access-signature-uri-on-hello-container-that-uses-an-access-policy"></a>Gerar um URI no contêiner de saudação que usa uma política de acesso de assinatura de acesso compartilhado
Em seguida, podemos criar outra assinatura de acesso compartilhado para o contêiner de saudação que criamos anteriormente, mas desta vez associamos assinatura Olá com a política de acesso Olá armazenado criada no exemplo anterior de saudação.

Adicione um novo toogenerate de método outra assinatura de acesso compartilhado para o contêiner de saudação:

```csharp
static string GetContainerSasUriWithPolicy(CloudBlobContainer container, string policyName)
{
    //Generate hello shared access signature on hello container. In this case, all of hello constraints for the
    //shared access signature are specified on hello stored access policy.
    string sasContainerToken = container.GetSharedAccessSignature(null, policyName);

    //Return hello URI string for hello container, including hello SAS token.
    return container.Uri + sasContainerToken;
}
```

Na parte inferior de saudação do hello **Main ()** método, antes de chamar de saudação muito**Console.ReadLine()**, adicionar Olá Olá de toocall linhas a seguir **GetContainerSasUriWithPolicy** método :

```csharp
//Generate a SAS URI for hello container, using a stored access policy tooset constraints on hello SAS.
Console.WriteLine("Container SAS URI using stored access policy: " + GetContainerSasUriWithPolicy(container, sharedAccessPolicyName));
Console.WriteLine();
```

### <a name="generate-a-shared-access-signature-uri-on-hello-blob-that-uses-an-access-policy"></a>Gerar um URI de assinatura de acesso compartilhado no hello Blob que usa uma política de acesso
Finalmente, adicione um toocreate método semelhante outro blob e gerar uma assinatura de acesso compartilhado que está associado a uma política de acesso armazenada.

Adicionar um novo toocreate de método um blob e gerar uma assinatura de acesso compartilhado:

```csharp
static string GetBlobSasUriWithPolicy(CloudBlobContainer container, string policyName)
{
    //Get a reference tooa blob within hello container.
    CloudBlockBlob blob = container.GetBlockBlobReference("sasblobpolicy.txt");

    //Upload text toohello blob. If hello blob does not yet exist, it will be created.
    //If hello blob does exist, its existing content will be overwritten.
    string blobContent = "This blob will be accessible tooclients via a shared access signature. " +
    "A stored access policy defines hello constraints for hello signature.";
    MemoryStream ms = new MemoryStream(Encoding.UTF8.GetBytes(blobContent));
    ms.Position = 0;
    using (ms)
    {
        blob.UploadFromStream(ms);
    }

    //Generate hello shared access signature on hello blob.
    string sasBlobToken = blob.GetSharedAccessSignature(null, policyName);

    //Return hello URI string for hello container, including hello SAS token.
    return blob.Uri + sasBlobToken;
}
```

Na parte inferior de saudação do hello **Main ()** método, antes de chamar de saudação muito**Console.ReadLine()**, adicionar Olá Olá de toocall linhas a seguir **GetBlobSasUriWithPolicy** método:

```csharp
//Generate a SAS URI for a blob within hello container, using a stored access policy tooset constraints on hello SAS.
Console.WriteLine("Blob SAS URI using stored access policy: " + GetBlobSasUriWithPolicy(container, sharedAccessPolicyName));
Console.WriteLine();
```

Olá **Main** método agora deve parecer com isso em sua totalidade. Execute-a assinatura de acesso compartilhado toowrite Olá janela de console toohello URIs, copiar e colá-los em um arquivo de texto para uso na segunda parte Olá deste tutorial.

```csharp
static void Main(string[] args)
{
    //Parse hello connection string and return a reference toohello storage account.
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(CloudConfigurationManager.GetSetting("StorageConnectionString"));

    //Create hello blob client object.
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

    //Get a reference tooa container toouse for hello sample code, and create it if it does not exist.
    CloudBlobContainer container = blobClient.GetContainerReference("sascontainer");
    container.CreateIfNotExists();

    //Generate a SAS URI for hello container, without a stored access policy.
    Console.WriteLine("Container SAS URI: " + GetContainerSasUri(container));
    Console.WriteLine();

    //Generate a SAS URI for a blob within hello container, without a stored access policy.
    Console.WriteLine("Blob SAS URI: " + GetBlobSasUri(container));
    Console.WriteLine();

    //Clear any existing access policies on container.
    BlobContainerPermissions perms = container.GetPermissions();
    perms.SharedAccessPolicies.Clear();
    container.SetPermissions(perms);

    //Create a new access policy on hello container, which may be optionally used tooprovide constraints for
    //shared access signatures on hello container and hello blob.
    string sharedAccessPolicyName = "tutorialpolicy";
    CreateSharedAccessPolicy(blobClient, container, sharedAccessPolicyName);

    //Generate a SAS URI for hello container, using a stored access policy tooset constraints on hello SAS.
    Console.WriteLine("Container SAS URI using stored access policy: " + GetContainerSasUriWithPolicy(container, sharedAccessPolicyName));
    Console.WriteLine();

    //Generate a SAS URI for a blob within hello container, using a stored access policy tooset constraints on hello SAS.
    Console.WriteLine("Blob SAS URI using stored access policy: " + GetBlobSasUriWithPolicy(container, sharedAccessPolicyName));
    Console.WriteLine();

    Console.ReadLine();
}
```

Quando você executa o aplicativo de console GenerateSharedAccessSignatures hello, você verá a seguinte de toohello semelhante de saída. São assinaturas de acesso Olá compartilhado que usar na parte 2 do tutorial de saudação.

```
Container SAS URI: https://storagesample.blob.core.windows.net/sascontainer?sv=2016-05-31&sr=c&sig=pFlEZD%2F6sJTNLxD%2FQ26Hh85j%2FzYPxZav6mP1KJwnvJE%3D&se=2017-05-16T16%3A16%3A47Z&sp=wl

Blob SAS URI: https://storagesample.blob.core.windows.net/sascontainer/sasblob.txt?sv=2016-05-31&sr=b&sig=%2FiBWAZbXESzCMvRcm7JwJBK0gT0BtPSWEq4pRwmlBRI%3D&st=2017-05-15T16%3A11%3A48Z&se=2017-05-16T16%3A16%3A48Z&sp=rw

Container SAS URI using stored access policy: https://storagesample.blob.core.windows.net/sascontainer?sv=2016-05-31&sr=c&si=tutorialpolicy&sig=aMb6rKDvvpfiGVsZI2rCmyUra6ZPpq%2BZ%2FLyTgAeec%2Bk%3D

Blob SAS URI using stored access policy: https://storagesample.blob.core.windows.net/sascontainer/sasblobpolicy.txt?sv=2016-05-31&sr=b&si=tutorialpolicy&sig=%2FkTWkT23SS45%2FoF4bK2mqXkN%2BPKs%2FyHuzkfQ4GFoZVU%3D
```

## <a name="part-2-create-a-console-application-tootest-hello-shared-access-signatures"></a>Parte 2: Criar um acesso ao console aplicativo tootest Olá compartilhado assinaturas
Olá tootest compartilhados assinaturas de acesso criadas nos exemplos anteriores hello, podemos criar um segundo aplicativo de console que usa as operações do hello assinaturas tooperform no contêiner hello e em um blob.

> [!NOTE]
> Se mais de 24 horas passaram desde que você concluiu a primeira parte Olá tutorial hello, assinaturas de saudação gerado não serão válidas. Nesse caso, você deve executar código Olá no primeiro toogenerate de aplicativo de console Olá assinaturas de acesso compartilhado nova para uso na segunda parte Olá tutorial hello.
>

No Visual Studio, crie um novo aplicativo de console do Windows e dê a ele o nome **ConsumeSharedAccessSignatures**. Adicione referências muito[Microsoft.WindowsAzure.ConfigurationManager](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager) e [windowsazure](https://www.nuget.org/packages/WindowsAzure.Storage/), como você fez anteriormente.

Na parte superior de saudação do arquivo do hello Program.cs, adicione o seguinte de Olá **usando** diretivas:

```csharp
using System.IO;
using Microsoft.WindowsAzure.Storage;
using Microsoft.WindowsAzure.Storage.Blob;
```

No corpo de saudação do hello **Main** método, adicione Olá constantes de cadeia de caracteres a seguir, a alteração de suas assinaturas de acesso de toohello compartilhado valores gerados na parte 1 do tutorial de saudação.

```csharp
static void Main(string[] args)
{
    const string containerSAS = "<your container SAS>";
    const string blobSAS = "<your blob SAS>";
    const string containerSASWithAccessPolicy = "<your container SAS with access policy>";
    const string blobSASWithAccessPolicy = "<your blob SAS with access policy>";
}
```

### <a name="add-a-method-tootry-container-operations-using-a-shared-access-signature"></a>Adicionar um método tootry contêiner as operações usando uma assinatura de acesso compartilhado
Em seguida, adicionamos um método que testa a algumas operações de contêiner usando uma assinatura de acesso compartilhado para o contêiner de saudação. assinatura de acesso compartilhado Olá é tooreturn usado um contêiner de toohello de referência, autenticar o contêiner de toohello de acesso com base na assinatura de saudação sozinha.

Adicione Olá tooProgram.cs do método a seguir:

```csharp
static void UseContainerSAS(string sas)
{
    //Try performing container operations with hello SAS provided.

    //Return a reference toohello container using hello SAS URI.
    CloudBlobContainer container = new CloudBlobContainer(new Uri(sas));

    //Create a list toostore blob URIs returned by a listing operation on hello container.
    List<ICloudBlob> blobList = new List<ICloudBlob>();

    //Write operation: write a new blob toohello container.
    try
    {
        CloudBlockBlob blob = container.GetBlockBlobReference("blobCreatedViaSAS.txt");
        string blobContent = "This blob was created with a shared access signature granting write permissions toohello container. ";
        blob.UploadText(blobContent);

        Console.WriteLine("Write operation succeeded for SAS " + sas);
        Console.WriteLine();
    }
    catch (StorageException e)
    {
        Console.WriteLine("Write operation failed for SAS " + sas);
        Console.WriteLine("Additional error information: " + e.Message);
        Console.WriteLine();
    }

    //List operation: List hello blobs in hello container.
    try
    {
        foreach (ICloudBlob blob in container.ListBlobs())
        {
            blobList.Add(blob);
        }
        Console.WriteLine("List operation succeeded for SAS " + sas);
        Console.WriteLine();
    }
    catch (StorageException e)
    {
        Console.WriteLine("List operation failed for SAS " + sas);
        Console.WriteLine("Additional error information: " + e.Message);
        Console.WriteLine();
    }

    //Read operation: Get a reference tooone of hello blobs in hello container and read it.
    try
    {
        CloudBlockBlob blob = container.GetBlockBlobReference(blobList[0].Name);
        MemoryStream msRead = new MemoryStream();
        msRead.Position = 0;
        using (msRead)
        {
            blob.DownloadToStream(msRead);
            Console.WriteLine(msRead.Length);
        }
        Console.WriteLine("Read operation succeeded for SAS " + sas);
        Console.WriteLine();
    }
    catch (StorageException e)
    {
        Console.WriteLine("Read operation failed for SAS " + sas);
        Console.WriteLine("Additional error information: " + e.Message);
        Console.WriteLine();
    }
    Console.WriteLine();

    //Delete operation: Delete a blob in hello container.
    try
    {
        CloudBlockBlob blob = container.GetBlockBlobReference(blobList[0].Name);
        blob.Delete();
        Console.WriteLine("Delete operation succeeded for SAS " + sas);
        Console.WriteLine();
    }
    catch (StorageException e)
    {
        Console.WriteLine("Delete operation failed for SAS " + sas);
        Console.WriteLine("Additional error information: " + e.Message);
        Console.WriteLine();
    }
}
```

Saudação de atualização **Main ()** método toocall **UseContainerSAS()** com ambos Olá compartilhados criados no contêiner de saudação de assinaturas de acesso:

```csharp
static void Main(string[] args)
{
    string containerSAS = "<your container SAS>";
    string blobSAS = "<your blob SAS>";
    string containerSASWithAccessPolicy = "<your container SAS with access policy>";
    string blobSASWithAccessPolicy = "<your blob SAS with access policy>";

    //Call hello test methods with hello shared access signatures created on hello container, with and without hello access policy.
    UseContainerSAS(containerSAS);
    UseContainerSAS(containerSASWithAccessPolicy);

    Console.ReadLine();
}
```

### <a name="add-a-method-tootry-blob-operations-using-a-shared-access-signature"></a>Adicionar um método tootry blob as operações usando uma assinatura de acesso compartilhado
Por fim, adicionamos um método que testa a algumas operações de blob usando uma assinatura de acesso compartilhado no blob de saudação. Nesse caso, usamos o construtor Olá **CloudBlockBlob(String)**, passando na assinatura de acesso compartilhado hello, tooreturn um blob de toohello de referência. Nenhuma outra autenticação é necessária; baseia-se a assinatura de saudação sozinha.

Adicione Olá tooProgram.cs do método a seguir:

```csharp
static void UseBlobSAS(string sas)
{
    //Try performing blob operations using hello SAS provided.

    //Return a reference toohello blob using hello SAS URI.
    CloudBlockBlob blob = new CloudBlockBlob(new Uri(sas));

    //Write operation: Write a new blob toohello container.
    try
    {
        string blobContent = "This blob was created with a shared access signature granting write permissions toohello blob. ";
        MemoryStream msWrite = new MemoryStream(Encoding.UTF8.GetBytes(blobContent));
        msWrite.Position = 0;
        using (msWrite)
        {
            blob.UploadFromStream(msWrite);
        }
        Console.WriteLine("Write operation succeeded for SAS " + sas);
        Console.WriteLine();
    }
    catch (StorageException e)
    {
        Console.WriteLine("Write operation failed for SAS " + sas);
        Console.WriteLine("Additional error information: " + e.Message);
        Console.WriteLine();
    }

    //Read operation: Read hello contents of hello blob.
    try
    {
        MemoryStream msRead = new MemoryStream();
        using (msRead)
        {
            blob.DownloadToStream(msRead);
            msRead.Position = 0;
            using (StreamReader reader = new StreamReader(msRead, true))
            {
                string line;
                while ((line = reader.ReadLine()) != null)
                {
                    Console.WriteLine(line);
                }
            }
        }
        Console.WriteLine("Read operation succeeded for SAS " + sas);
        Console.WriteLine();
    }
    catch (StorageException e)
    {
        Console.WriteLine("Read operation failed for SAS " + sas);
        Console.WriteLine("Additional error information: " + e.Message);
        Console.WriteLine();
    }

    //Delete operation: Delete hello blob.
    try
    {
        blob.Delete();
        Console.WriteLine("Delete operation succeeded for SAS " + sas);
        Console.WriteLine();
    }
    catch (StorageException e)
    {
        Console.WriteLine("Delete operation failed for SAS " + sas);
        Console.WriteLine("Additional error information: " + e.Message);
        Console.WriteLine();
    }
}
```

Saudação de atualização **Main ()** método toocall **UseBlobSAS()** com ambos Olá compartilhado assinaturas de acesso que você criou no blob hello:

```csharp
static void Main(string[] args)
{
    string containerSAS = "<your container SAS>";
    string blobSAS = "<your blob SAS>";
    string containerSASWithAccessPolicy = "<your container SAS with access policy>";
    string blobSASWithAccessPolicy = "<your blob SAS with access policy>";

    //Call hello test methods with hello shared access signatures created on hello container, with and without hello access policy.
    UseContainerSAS(containerSAS);
    UseContainerSAS(containerSASWithAccessPolicy);

    //Call hello test methods with hello shared access signatures created on hello blob, with and without hello access policy.
    UseBlobSAS(blobSAS);
    UseBlobSAS(blobSASWithAccessPolicy);

    Console.ReadLine();
}
```

Execute o aplicativo de console hello e observe Olá saída toosee quais operações são permitidas para as assinaturas. saída de Hello na janela de console Olá procurará a seguir toohello semelhante:

```
Write operation succeeded for SAS https://storagesample.blob.core.windows.net/sascontainer?sv=2016-05-31&sr=c&sig=32EaQGuFyDMb3yOAey3wq%2B%2FLwgPQxAgSo7UhzLdyIDU%3D&se=2017-05-16T15%3A41%3A20Z&sp=wl

List operation succeeded for SAS https://storagesample.blob.core.windows.net/sascontainer?sv=2016-05-31&sr=c&sig=32EaQGuFyDMb3yOAey3wq%2B%2FLwgPQxAgSo7UhzLdyIDU%3D&se=2017-05-16T15%3A41%3A20Z&sp=wl

Read operation failed for SAS https://storagesample.blob.core.windows.net/sascontainer?sv=2016-05-31&sr=c&sig=32EaQGuFyDMb3yOAey3wq%2B%2FLwgPQxAgSo7UhzLdyIDU%3D&se=2017-05-16T15%3A41%3A20Z&sp=wl
Additional error information: hello remote server returned an error: (403) Forbidden.

Delete operation failed for SAS https://storagesample.blob.core.windows.net/sascontainer?sv=2016-05-31&sr=c&sig=32EaQGuFyDMb3yOAey3wq%2B%2FLwgPQxAgSo7UhzLdyIDU%3D&se=2017-05-16T15%3A41%3A20Z&sp=wl
Additional error information: hello remote server returned an error: (403) Forbidden.

...
```

## <a name="next-steps"></a>Próximas etapas

* [Assinaturas de acesso compartilhado, parte 1: Saudação de Noções básicas sobre modelo SAS](storage-dotnet-shared-access-signature-part-1.md)
* [Gerenciar blobs e acesso de leitura anônimo toocontainers](storage-manage-access-to-resources.md)
* [Delegar o acesso com uma assinatura de acesso compartilhado (API REST)](http://msdn.microsoft.com/library/azure/ee395415.aspx)
* [Introdução à Tabela e à Fila SAS](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-table-sas-shared-access-signature-queue-sas-and-update-to-blob-sas.aspx)
