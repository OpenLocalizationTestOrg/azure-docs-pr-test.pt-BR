---
title: 'Tutorial: Criptografar e descriptografar blobs no Armazenamento do Azure usando o Azure Key Vault | Microsoft Docs'
description: Como criptografar e descriptografar um blob usando a criptografia do lado do cliente para o Armazenamento do Microsoft Azure com o Azure Key Vault.
services: storage
documentationcenter: 
author: adhurwit
manager: jasonsav
editor: tysonn
ms.assetid: 027e8631-c1bf-48c1-9d9b-f6843e88b583
ms.service: storage
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: required
ms.date: 01/23/2017
ms.author: adhurwit
ms.openlocfilehash: 0c33742a0212e670072a947a2d2ab8304c77b973
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-encrypt-and-decrypt-blobs-in-microsoft-azure-storage-using-azure-key-vault"></a><span data-ttu-id="a8ec6-103">Tutorial: criptografar e descriptografar blobs no Armazenamento do Microsoft Azure usando o Cofre da Chave do Azure</span><span class="sxs-lookup"><span data-stu-id="a8ec6-103">Tutorial: Encrypt and decrypt blobs in Microsoft Azure Storage using Azure Key Vault</span></span>
## <a name="introduction"></a><span data-ttu-id="a8ec6-104">Introdução</span><span class="sxs-lookup"><span data-stu-id="a8ec6-104">Introduction</span></span>
<span data-ttu-id="a8ec6-105">Este tutorial aborda como aproveitar a criptografia de armazenamento do cliente com o Cofre da Chave do Azure.</span><span class="sxs-lookup"><span data-stu-id="a8ec6-105">This tutorial covers how to make use of client-side storage encryption with Azure Key Vault.</span></span> <span data-ttu-id="a8ec6-106">Ele explica como criptografar e descriptografar um blob em um aplicativo de console usando essas tecnologias.</span><span class="sxs-lookup"><span data-stu-id="a8ec6-106">It walks you through how to encrypt and decrypt a blob in a console application using these technologies.</span></span>

<span data-ttu-id="a8ec6-107">**Tempo estimado para conclusão:** 20 minutos</span><span class="sxs-lookup"><span data-stu-id="a8ec6-107">**Estimated time to complete:** 20 minutes</span></span>

<span data-ttu-id="a8ec6-108">Para obter informações gerais sobre o Cofre de Chaves do Azure, consulte [O que é o Cofre de Chaves do Azure?](../key-vault/key-vault-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="a8ec6-108">For overview information about Azure Key Vault, see [What is Azure Key Vault?](../key-vault/key-vault-whatis.md).</span></span>

<span data-ttu-id="a8ec6-109">Para obter informações gerais sobre a criptografia de cliente do armazenamento do Azure, consulte [Criptografia do lado do cliente e Cofre de Chaves do Azure para o Armazenamento do Microsoft Azure](storage-client-side-encryption.md).</span><span class="sxs-lookup"><span data-stu-id="a8ec6-109">For overview information about client-side encryption for Azure Storage, see [Client-Side Encryption and Azure Key Vault for Microsoft Azure Storage](storage-client-side-encryption.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a8ec6-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="a8ec6-110">Prerequisites</span></span>
<span data-ttu-id="a8ec6-111">Para concluir este tutorial, você precisará do seguinte:</span><span class="sxs-lookup"><span data-stu-id="a8ec6-111">To complete this tutorial, you must have the following:</span></span>

* <span data-ttu-id="a8ec6-112">Uma conta de armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="a8ec6-112">An Azure Storage account</span></span>
* <span data-ttu-id="a8ec6-113">Visual Studio 2013 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="a8ec6-113">Visual Studio 2013 or later</span></span>
* <span data-ttu-id="a8ec6-114">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="a8ec6-114">Azure PowerShell</span></span>

## <a name="overview-of-client-side-encryption"></a><span data-ttu-id="a8ec6-115">Visão geral da criptografia do lado do cliente</span><span class="sxs-lookup"><span data-stu-id="a8ec6-115">Overview of client-side encryption</span></span>
<span data-ttu-id="a8ec6-116">Para obter uma visão geral da criptografia do lado do cliente do Armazenamento do Azure, consulte [Criptografia do lado do cliente e o Cofre de Chaves do Azure para o Armazenamento do Microsoft Azure](storage-client-side-encryption.md)</span><span class="sxs-lookup"><span data-stu-id="a8ec6-116">For an overview of client-side encryption for Azure Storage, see [Client-Side Encryption and Azure Key Vault for Microsoft Azure Storage](storage-client-side-encryption.md)</span></span>

<span data-ttu-id="a8ec6-117">Aqui está uma breve descrição de como funciona a criptografia do lado do cliente:</span><span class="sxs-lookup"><span data-stu-id="a8ec6-117">Here is a brief description of how client side encryption works:</span></span>

1. <span data-ttu-id="a8ec6-118">O SDK do cliente do Armazenamento do Azure gera uma CEK (chave de criptografia de conteúdo) que é uma chave simétrica de uso único.</span><span class="sxs-lookup"><span data-stu-id="a8ec6-118">The Azure Storage client SDK generates a content encryption key (CEK), which is a one-time-use symmetric key.</span></span>
2. <span data-ttu-id="a8ec6-119">Os dados do cliente são criptografados usando essa CEK.</span><span class="sxs-lookup"><span data-stu-id="a8ec6-119">Customer data is encrypted using this CEK.</span></span>
3. <span data-ttu-id="a8ec6-120">O CEK é empacotada (criptografada) usando o KEK (Chave de Criptografia de Chave).</span><span class="sxs-lookup"><span data-stu-id="a8ec6-120">The CEK is then wrapped (encrypted) using the key encryption key (KEK).</span></span> <span data-ttu-id="a8ec6-121">A KEK é identificada por um identificador de chave e pode ser um par de chaves assimétricas ou uma chave simétrica, podendo ser gerenciada localmente ou armazenada no Cofre da Chave do Azure.</span><span class="sxs-lookup"><span data-stu-id="a8ec6-121">The KEK is identified by a key identifier and can be an asymmetric key pair or a symmetric key and can be managed locally or stored in Azure Key Vault.</span></span> <span data-ttu-id="a8ec6-122">O cliente de Armazenamento, por si só, nunca tem acesso à KEK.</span><span class="sxs-lookup"><span data-stu-id="a8ec6-122">The Storage client itself never has access to the KEK.</span></span> <span data-ttu-id="a8ec6-123">Ele simplesmente chama o algoritmo de quebra de chave fornecido pelo Cofre da Chave.</span><span class="sxs-lookup"><span data-stu-id="a8ec6-123">It just invokes the key wrapping algorithm that is provided by Key Vault.</span></span> <span data-ttu-id="a8ec6-124">Os clientes podem escolher usar provedores personalizados para desempacotamento/quebra da chave, se desejado.</span><span class="sxs-lookup"><span data-stu-id="a8ec6-124">Customers can choose to use custom providers for key wrapping/unwrapping if they want.</span></span>
4. <span data-ttu-id="a8ec6-125">Os dados criptografados, em seguida, são carregados para o serviço de Armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="a8ec6-125">The encrypted data is then uploaded to the Azure Storage service.</span></span>

## <a name="set-up-your-azure-key-vault"></a><span data-ttu-id="a8ec6-126">Configure o seu Cofre da Chave do Azure</span><span class="sxs-lookup"><span data-stu-id="a8ec6-126">Set up your Azure Key Vault</span></span>
<span data-ttu-id="a8ec6-127">Para continuar com este tutorial, você precisa realizar as etapas a seguir, que são descritas no tutorial: [Introdução ao Cofre de Chaves do Azure](../key-vault/key-vault-get-started.md):</span><span class="sxs-lookup"><span data-stu-id="a8ec6-127">In order to proceed with this tutorial, you need to do the following steps, which are outlined in the tutorial  [Get started with Azure Key Vault](../key-vault/key-vault-get-started.md):</span></span>

* <span data-ttu-id="a8ec6-128">Crie um cofre da chave.</span><span class="sxs-lookup"><span data-stu-id="a8ec6-128">Create a key vault.</span></span>
* <span data-ttu-id="a8ec6-129">Adicionar uma chave ou segredo ao cofre da chave.</span><span class="sxs-lookup"><span data-stu-id="a8ec6-129">Add a key or secret to the key vault.</span></span>
* <span data-ttu-id="a8ec6-130">Registre um aplicativo com o Active Directory do Azure.</span><span class="sxs-lookup"><span data-stu-id="a8ec6-130">Register an application with Azure Active Directory.</span></span>
* <span data-ttu-id="a8ec6-131">Autorize o aplicativo a usar a chave ou segredo.</span><span class="sxs-lookup"><span data-stu-id="a8ec6-131">Authorize the application to use the key or secret.</span></span>

<span data-ttu-id="a8ec6-132">Anote o ClientID e ClientSecret que foram gerados ao registrar um aplicativo com o Active Directory do Azure.</span><span class="sxs-lookup"><span data-stu-id="a8ec6-132">Make note of the ClientID and ClientSecret that were generated when registering an application with Azure Active Directory.</span></span>

<span data-ttu-id="a8ec6-133">Crie ambas as chaves no cofre da chave.</span><span class="sxs-lookup"><span data-stu-id="a8ec6-133">Create both keys in the key vault.</span></span> <span data-ttu-id="a8ec6-134">Vamos supor pelo restante do tutorial que você tenha usado os seguintes nomes: ContosoKeyVault e TestRSAKey1.</span><span class="sxs-lookup"><span data-stu-id="a8ec6-134">We assume for the rest of the tutorial that you have used the following names: ContosoKeyVault and TestRSAKey1.</span></span>

## <a name="create-a-console-application-with-packages-and-appsettings"></a><span data-ttu-id="a8ec6-135">Criar um aplicativo de console com pacotes e AppSettings</span><span class="sxs-lookup"><span data-stu-id="a8ec6-135">Create a console application with packages and AppSettings</span></span>
<span data-ttu-id="a8ec6-136">No Visual Studio, crie um novo aplicativo de console.</span><span class="sxs-lookup"><span data-stu-id="a8ec6-136">In Visual Studio, create a new console application.</span></span>

<span data-ttu-id="a8ec6-137">Adicione pacotes nuget necessários no Console do Gerenciador de Pacotes.</span><span class="sxs-lookup"><span data-stu-id="a8ec6-137">Add necessary nuget packages in the Package Manager Console.</span></span>

```
Install-Package WindowsAzure.Storage

// This is the latest stable release for ADAL.
Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -Version 2.16.204221202

Install-Package Microsoft.Azure.KeyVault
Install-Package Microsoft.Azure.KeyVault.Extensions
```

<span data-ttu-id="a8ec6-138">Adicione AppSettings a App.Config.</span><span class="sxs-lookup"><span data-stu-id="a8ec6-138">Add AppSettings to the App.Config.</span></span>

```xml
<appSettings>
    <add key="accountName" value="myaccount"/>
    <add key="accountKey" value="theaccountkey"/>
    <add key="clientId" value="theclientid"/>
    <add key="clientSecret" value="theclientsecret"/>
    <add key="container" value="stuff"/>
</appSettings>
```

<span data-ttu-id="a8ec6-139">Adicione as seguintes instruções `using` e certifique-se de adicionar uma referência a System.Configuration ao projeto.</span><span class="sxs-lookup"><span data-stu-id="a8ec6-139">Add the following `using` statements and make sure to add a reference to System.Configuration to the project.</span></span>

```csharp
using Microsoft.IdentityModel.Clients.ActiveDirectory;
using System.Configuration;
using Microsoft.WindowsAzure.Storage.Auth;
using Microsoft.WindowsAzure.Storage;
using Microsoft.WindowsAzure.Storage.Blob;
using Microsoft.Azure.KeyVault;
using System.Threading;        
using System.IO;
```

## <a name="add-a-method-to-get-a-token-to-your-console-application"></a><span data-ttu-id="a8ec6-140">Adicione um método para obter um token para o aplicativo de console</span><span class="sxs-lookup"><span data-stu-id="a8ec6-140">Add a method to get a token to your console application</span></span>
<span data-ttu-id="a8ec6-141">O método a seguir é usado pelas classes do Cofre da Chave que precisam ser autenticadas para acessar seu cofre da chave.</span><span class="sxs-lookup"><span data-stu-id="a8ec6-141">The following method is used by Key Vault classes that need to authenticate for access to your key vault.</span></span>

```csharp
private async static Task<string> GetToken(string authority, string resource, string scope)
{
    var authContext = new AuthenticationContext(authority);
    ClientCredential clientCred = new ClientCredential(
        ConfigurationManager.AppSettings["clientId"],
        ConfigurationManager.AppSettings["clientSecret"]);
    AuthenticationResult result = await authContext.AcquireTokenAsync(resource, clientCred);

    if (result == null)
        throw new InvalidOperationException("Failed to obtain the JWT token");

    return result.AccessToken;
}
```

## <a name="access-storage-and-key-vault-in-your-program"></a><span data-ttu-id="a8ec6-142">Acessar o Armazenamento e o Cofre da Chave em seu programa</span><span class="sxs-lookup"><span data-stu-id="a8ec6-142">Access Storage and Key Vault in your program</span></span>
<span data-ttu-id="a8ec6-143">Na função Main, adicione o código a seguir.</span><span class="sxs-lookup"><span data-stu-id="a8ec6-143">In the Main function, add the following code.</span></span>

```csharp
// This is standard code to interact with Blob storage.
StorageCredentials creds = new StorageCredentials(
    ConfigurationManager.AppSettings["accountName"],
       ConfigurationManager.AppSettings["accountKey"]);
CloudStorageAccount account = new CloudStorageAccount(creds, useHttps: true);
CloudBlobClient client = account.CreateCloudBlobClient();
CloudBlobContainer contain = client.GetContainerReference(ConfigurationManager.AppSettings["container"]);
contain.CreateIfNotExists();

// The Resolver object is used to interact with Key Vault for Azure Storage.
// This is where the GetToken method from above is used.
KeyVaultKeyResolver cloudResolver = new KeyVaultKeyResolver(GetToken);
```

> [!NOTE]
> <span data-ttu-id="a8ec6-144">Modelos de Objetos de Chave de Cofre</span><span class="sxs-lookup"><span data-stu-id="a8ec6-144">Key Vault Object Models</span></span>
> 
> <span data-ttu-id="a8ec6-145">É importante entender que há realmente dois Chave de Cofre modelos de objeto estar atento: uma baseada na API REST (namespace KeyVault) e a outra é uma extensão para criptografia do lado do cliente.</span><span class="sxs-lookup"><span data-stu-id="a8ec6-145">It is important to understand that there are actually two Key Vault object models to be aware of: one is based on the REST API (KeyVault namespace) and the other is an extension for client-side encryption.</span></span>
> 
> <span data-ttu-id="a8ec6-146">O Cliente do Cofre da Chave interage com a API REST e compreende JSON Web chaves e segredos para os dois tipos de coisas que estão contidos no Cofre da Chave.</span><span class="sxs-lookup"><span data-stu-id="a8ec6-146">The Key Vault Client interacts with the REST API and understands JSON Web Keys and secrets for the two kinds of things that are contained in Key Vault.</span></span>
> 
> <span data-ttu-id="a8ec6-147">As Extensões de Chave de Cofre são classes que parecem criados especificamente para a criptografia de cliente no Armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="a8ec6-147">The Key Vault Extensions are classes that seem specifically created for client-side encryption in Azure Storage.</span></span> <span data-ttu-id="a8ec6-148">Eles contêm uma interface para chaves (IKey) e classes com base no conceito de um Resolvedor de Chave.</span><span class="sxs-lookup"><span data-stu-id="a8ec6-148">They contain an interface for keys (IKey) and classes based on the concept of a Key Resolver.</span></span> <span data-ttu-id="a8ec6-149">Há duas implementações de IKey que você precisa saber: RSAKey e SymmetricKey.</span><span class="sxs-lookup"><span data-stu-id="a8ec6-149">There are two implementations of IKey that you need to know: RSAKey and SymmetricKey.</span></span> <span data-ttu-id="a8ec6-150">Agora que eles aconteçam coincidir com as coisas que estão contidas em um Cofre da Chave, mas agora são classes independentes (para a chave e o segredo recuperada pelo cliente Cofre da Chave não implementam IKey).</span><span class="sxs-lookup"><span data-stu-id="a8ec6-150">Now they happen to coincide with the things that are contained in a Key Vault, but at this point they are independent classes (so the Key and Secret retrieved by the Key Vault Client do not implement IKey).</span></span>
> 
> 

## <a name="encrypt-blob-and-upload"></a><span data-ttu-id="a8ec6-151">Criptografar o blob e carregar</span><span class="sxs-lookup"><span data-stu-id="a8ec6-151">Encrypt blob and upload</span></span>
<span data-ttu-id="a8ec6-152">Adicione o seguinte código para criptografar um blob e carregá-lo à sua conta de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="a8ec6-152">Add the following code to encrypt a blob and upload it to your Azure storage account.</span></span> <span data-ttu-id="a8ec6-153">O método **ResolveKeyAsync** usado retorna uma IKey.</span><span class="sxs-lookup"><span data-stu-id="a8ec6-153">The **ResolveKeyAsync** method that is used returns an IKey.</span></span>

```csharp
// Retrieve the key that you created previously.
// The IKey that is returned here is an RsaKey.
// Remember that we used the names contosokeyvault and testrsakey1.
var rsa = cloudResolver.ResolveKeyAsync("https://contosokeyvault.vault.azure.net/keys/TestRSAKey1", CancellationToken.None).GetAwaiter().GetResult();

// Now you simply use the RSA key to encrypt by setting it in the BlobEncryptionPolicy.
BlobEncryptionPolicy policy = new BlobEncryptionPolicy(rsa, null);
BlobRequestOptions options = new BlobRequestOptions() { EncryptionPolicy = policy };

// Reference a block blob.
CloudBlockBlob blob = contain.GetBlockBlobReference("MyFile.txt");

// Upload using the UploadFromStream method.
using (var stream = System.IO.File.OpenRead(@"C:\data\MyFile.txt"))
    blob.UploadFromStream(stream, stream.Length, null, options, null);
```

<span data-ttu-id="a8ec6-154">A seguir está uma captura de tela do [Portal Clássico do Azure](https://manage.windowsazure.com) de um blob que foi criptografado usando a criptografia de cliente com uma chave armazenada no Cofre de Chaves.</span><span class="sxs-lookup"><span data-stu-id="a8ec6-154">Following is a screenshot from the [Azure Classic Portal](https://manage.windowsazure.com) for a blob that has been encrypted by using client-side encryption with a key stored in Key Vault.</span></span> <span data-ttu-id="a8ec6-155">A propriedade **KeyId** é a URI para a chave no Cofre de Chaves que atua como a KEK.</span><span class="sxs-lookup"><span data-stu-id="a8ec6-155">The **KeyId** property is the URI for the key in Key Vault that acts as the KEK.</span></span> <span data-ttu-id="a8ec6-156">A propriedade **EncryptedKey** contém a versão criptografada da CEK.</span><span class="sxs-lookup"><span data-stu-id="a8ec6-156">The **EncryptedKey** property contains the encrypted version of the CEK.</span></span>

![Captura de tela mostrando os metadados de Blob que inclui metadados de criptografia](./media/storage-encrypt-decrypt-blobs-key-vault/blobmetadata.png)

> [!NOTE]
> <span data-ttu-id="a8ec6-158">Se você examinar o construtor BlobEncryptionPolicy, você verá que ele pode aceitar uma chave e/ou um resolvedor.</span><span class="sxs-lookup"><span data-stu-id="a8ec6-158">If you look at the BlobEncryptionPolicy constructor, you will see that it can accept a key and/or a resolver.</span></span> <span data-ttu-id="a8ec6-159">Lembre-se de que agora, você não pode usar um resolvedor para criptografia porque atualmente não dá suporte a uma chave padrão.</span><span class="sxs-lookup"><span data-stu-id="a8ec6-159">Be aware that right now you cannot use a resolver for encryption because it does not currently support a default key.</span></span>
> 
> 

## <a name="decrypt-blob-and-download"></a><span data-ttu-id="a8ec6-160">Descriptografar o blob e baixar</span><span class="sxs-lookup"><span data-stu-id="a8ec6-160">Decrypt blob and download</span></span>
<span data-ttu-id="a8ec6-161">Descriptografia é quando o uso das classes de resolvedor realmente fazem sentido.</span><span class="sxs-lookup"><span data-stu-id="a8ec6-161">Decryption is really when using the Resolver classes make sense.</span></span> <span data-ttu-id="a8ec6-162">A ID da chave usada para criptografia é associada ao blob em seus metadados, portanto, não há motivo para recuperar a chave e lembre-se a associação entre a chave e o blob.</span><span class="sxs-lookup"><span data-stu-id="a8ec6-162">The ID of the key used for encryption is associated with the blob in its metadata, so there is no reason for you to retrieve the key and remember the association between key and blob.</span></span> <span data-ttu-id="a8ec6-163">Você precisa certificar-se de que a chave permanece no Cofre da Chave.</span><span class="sxs-lookup"><span data-stu-id="a8ec6-163">You just have to make sure that the key remains in Key Vault.</span></span>   

<span data-ttu-id="a8ec6-164">A chave privada de uma Chave RSA permanece no Cofre da Chave de modo que, para a descriptografia ocorrer, a Chave Criptografada dos metadados do blob que contêm a CEK é enviada ao Cofre da Chave para descriptografia.</span><span class="sxs-lookup"><span data-stu-id="a8ec6-164">The private key of an RSA Key remains in Key Vault, so for decryption to occur, the Encrypted Key from the blob metadata that contains the CEK is sent to Key Vault for decryption.</span></span>

<span data-ttu-id="a8ec6-165">Adicione o seguinte para descriptografar o blob que você acabou de carregar.</span><span class="sxs-lookup"><span data-stu-id="a8ec6-165">Add the following to decrypt the blob that you just uploaded.</span></span>

```csharp
// In this case, we will not pass a key and only pass the resolver because
// this policy will only be used for downloading / decrypting.
BlobEncryptionPolicy policy = new BlobEncryptionPolicy(null, cloudResolver);
BlobRequestOptions options = new BlobRequestOptions() { EncryptionPolicy = policy };

using (var np = File.Open(@"C:\data\MyFileDecrypted.txt", FileMode.Create))
    blob.DownloadToStream(np, null, options, null);
```

> [!NOTE]
> <span data-ttu-id="a8ec6-166">Existem alguns outros tipos de resolvedores para facilitar o gerenciamento de chaves, incluindo: AggregateKeyResolver e CachingKeyResolver.</span><span class="sxs-lookup"><span data-stu-id="a8ec6-166">There are a couple of other kinds of resolvers to make key management easier, including: AggregateKeyResolver and CachingKeyResolver.</span></span>
> 
> 

## <a name="use-key-vault-secrets"></a><span data-ttu-id="a8ec6-167">Usar os segredos do Cofre da Chave</span><span class="sxs-lookup"><span data-stu-id="a8ec6-167">Use Key Vault secrets</span></span>
<span data-ttu-id="a8ec6-168">A maneira de usar um segredo com criptografia do lado do cliente é por meio da classe SymmetricKey, dado que um segredo é essencialmente uma chave simétrica.</span><span class="sxs-lookup"><span data-stu-id="a8ec6-168">The way to use a secret with client-side encryption is via the SymmetricKey class because a secret is essentially a symmetric key.</span></span> <span data-ttu-id="a8ec6-169">Mas, conforme observado anteriormente, um segredo no Cofre da Chave não é mapeado com exatidão para uma SymmetricKey.</span><span class="sxs-lookup"><span data-stu-id="a8ec6-169">But, as noted above, a secret in Key Vault does not map exactly to a SymmetricKey.</span></span> <span data-ttu-id="a8ec6-170">Há algumas coisas que deve compreender:</span><span class="sxs-lookup"><span data-stu-id="a8ec6-170">There are a few things to understand:</span></span>

* <span data-ttu-id="a8ec6-171">A chave em uma SymmetricKey deve ter um comprimento fixo: 192, 128, 256, 384 ou 512 bits.</span><span class="sxs-lookup"><span data-stu-id="a8ec6-171">The key in a SymmetricKey has to be a fixed length: 128, 192, 256, 384, or 512 bits.</span></span>
* <span data-ttu-id="a8ec6-172">A chave em uma SymmetricKey deve ser codificado em Base64.</span><span class="sxs-lookup"><span data-stu-id="a8ec6-172">The key in a SymmetricKey should be Base64 encoded.</span></span>
* <span data-ttu-id="a8ec6-173">Um segredo do Cofre da Chave que será usado como uma SymmetricKey deve ter um tipo de conteúdo de "application/octet-stream" no Cofre da Chave.</span><span class="sxs-lookup"><span data-stu-id="a8ec6-173">A Key Vault secret that will be used as a SymmetricKey needs to have a Content Type of "application/octet-stream" in Key Vault.</span></span>

<span data-ttu-id="a8ec6-174">Aqui está um exemplo no PowerShell sobre a criação de um segredo no Cofre da Chave que pode ser usado como uma SymmetricKey.</span><span class="sxs-lookup"><span data-stu-id="a8ec6-174">Here is an example in PowerShell of creating a secret in Key Vault that can be used as a SymmetricKey.</span></span>
<span data-ttu-id="a8ec6-175">Observe que o valor codificado, $key, serve apenas para demonstração.</span><span class="sxs-lookup"><span data-stu-id="a8ec6-175">Please note that the hard coded value, $key, is for demonstration purpose only.</span></span> <span data-ttu-id="a8ec6-176">Em seu próprio código, você desejará gerar essa chave.</span><span class="sxs-lookup"><span data-stu-id="a8ec6-176">In your own code you'll want to generate this key.</span></span>

```csharp
// Here we are making a 128-bit key so we have 16 characters.
//     The characters are in the ASCII range of UTF8 so they are
//    each 1 byte. 16 x 8 = 128.
$key = "qwertyuiopasdfgh"
$b = [System.Text.Encoding]::UTF8.GetBytes($key)
$enc = [System.Convert]::ToBase64String($b)
$secretvalue = ConvertTo-SecureString $enc -AsPlainText -Force

// Substitute the VaultName and Name in this command.
$secret = Set-AzureKeyVaultSecret -VaultName 'ContoseKeyVault' -Name 'TestSecret2' -SecretValue $secretvalue -ContentType "application/octet-stream"
```

<span data-ttu-id="a8ec6-177">Em seu aplicativo de console, você pode usar a mesma chamada como antes, para recuperar esse segredo como uma SymmetricKey.</span><span class="sxs-lookup"><span data-stu-id="a8ec6-177">In your console application, you can use the same call as before to retrieve this secret as a SymmetricKey.</span></span>

```csharp
SymmetricKey sec = (SymmetricKey) cloudResolver.ResolveKeyAsync(
    "https://contosokeyvault.vault.azure.net/secrets/TestSecret2/",
    CancellationToken.None).GetAwaiter().GetResult();
```
<span data-ttu-id="a8ec6-178">É isso.</span><span class="sxs-lookup"><span data-stu-id="a8ec6-178">That's it.</span></span> <span data-ttu-id="a8ec6-179">Aproveite!</span><span class="sxs-lookup"><span data-stu-id="a8ec6-179">Enjoy!</span></span>

## <a name="next-steps"></a><span data-ttu-id="a8ec6-180">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="a8ec6-180">Next steps</span></span>
<span data-ttu-id="a8ec6-181">Para obter mais informações sobre como usar o Armazenamento do Microsoft Azure com C#, consulte [Biblioteca de cliente de Armazenamento do Microsoft Azure para .NET](https://msdn.microsoft.com/library/azure/dn261237.aspx).</span><span class="sxs-lookup"><span data-stu-id="a8ec6-181">For more information about using Microsoft Azure Storage with C#, see [Microsoft Azure Storage Client Library for .NET](https://msdn.microsoft.com/library/azure/dn261237.aspx).</span></span>

<span data-ttu-id="a8ec6-182">Para obter mais informações sobre a API REST do Blob, consulte [API REST do Serviço Blob](https://msdn.microsoft.com/library/azure/dd135733.aspx).</span><span class="sxs-lookup"><span data-stu-id="a8ec6-182">For more information about the Blob REST API, see [Blob Service REST API](https://msdn.microsoft.com/library/azure/dd135733.aspx).</span></span>

<span data-ttu-id="a8ec6-183">Para obter as informações mais recentes sobre o Armazenamento do Microsoft Azure, vá para o [Blog da equipe de Armazenamento do Microsoft Azure](http://blogs.msdn.com/b/windowsazurestorage/).</span><span class="sxs-lookup"><span data-stu-id="a8ec6-183">For the latest information on Microsoft Azure Storage, go to the [Microsoft Azure Storage Team Blog](http://blogs.msdn.com/b/windowsazurestorage/).</span></span>
