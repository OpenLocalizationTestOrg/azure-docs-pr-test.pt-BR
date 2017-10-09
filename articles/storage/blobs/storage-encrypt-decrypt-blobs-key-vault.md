---
title: 'Tutorial: Criptografar e descriptografar blobs no Armazenamento do Azure usando o Azure Key Vault | Microsoft Docs'
description: Como tooencrypt e descriptografar um blob usando a criptografia do lado do cliente de armazenamento do Microsoft Azure com o Cofre de chaves do Azure.
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
ms.openlocfilehash: e387dd419a51b5b1df62d10ead97268e8295ff56
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-encrypt-and-decrypt-blobs-in-microsoft-azure-storage-using-azure-key-vault"></a><span data-ttu-id="a1729-103">Tutorial: criptografar e descriptografar blobs no Armazenamento do Microsoft Azure usando o Cofre da Chave do Azure</span><span class="sxs-lookup"><span data-stu-id="a1729-103">Tutorial: Encrypt and decrypt blobs in Microsoft Azure Storage using Azure Key Vault</span></span>
## <a name="introduction"></a><span data-ttu-id="a1729-104">Introdução</span><span class="sxs-lookup"><span data-stu-id="a1729-104">Introduction</span></span>
<span data-ttu-id="a1729-105">Este tutorial aborda como toomake o uso de criptografia de armazenamento do cliente com o Cofre de chaves do Azure.</span><span class="sxs-lookup"><span data-stu-id="a1729-105">This tutorial covers how toomake use of client-side storage encryption with Azure Key Vault.</span></span> <span data-ttu-id="a1729-106">Ele orienta como tooencrypt e descriptografar um blob em um aplicativo de console usando essas tecnologias.</span><span class="sxs-lookup"><span data-stu-id="a1729-106">It walks you through how tooencrypt and decrypt a blob in a console application using these technologies.</span></span>

<span data-ttu-id="a1729-107">**Estimado tempo toocomplete:** 20 minutos</span><span class="sxs-lookup"><span data-stu-id="a1729-107">**Estimated time toocomplete:** 20 minutes</span></span>

<span data-ttu-id="a1729-108">Para obter informações gerais sobre o Cofre de Chaves do Azure, consulte [O que é o Cofre de Chaves do Azure?](../../key-vault/key-vault-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="a1729-108">For overview information about Azure Key Vault, see [What is Azure Key Vault?](../../key-vault/key-vault-whatis.md).</span></span>

<span data-ttu-id="a1729-109">Para obter informações gerais sobre a criptografia de cliente do armazenamento do Azure, consulte [Criptografia do lado do cliente e Cofre de Chaves do Azure para o Armazenamento do Microsoft Azure](../common/storage-client-side-encryption.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="a1729-109">For overview information about client-side encryption for Azure Storage, see [Client-Side Encryption and Azure Key Vault for Microsoft Azure Storage](../common/storage-client-side-encryption.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a1729-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="a1729-110">Prerequisites</span></span>
<span data-ttu-id="a1729-111">toocomplete neste tutorial, você deve ter Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="a1729-111">toocomplete this tutorial, you must have hello following:</span></span>

* <span data-ttu-id="a1729-112">Uma conta de armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="a1729-112">An Azure Storage account</span></span>
* <span data-ttu-id="a1729-113">Visual Studio 2013 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="a1729-113">Visual Studio 2013 or later</span></span>
* <span data-ttu-id="a1729-114">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="a1729-114">Azure PowerShell</span></span>

## <a name="overview-of-client-side-encryption"></a><span data-ttu-id="a1729-115">Visão geral da criptografia do lado do cliente</span><span class="sxs-lookup"><span data-stu-id="a1729-115">Overview of client-side encryption</span></span>
<span data-ttu-id="a1729-116">Para obter uma visão geral da criptografia do lado do cliente do Armazenamento do Azure, consulte [Criptografia do lado do cliente e o Cofre de Chaves do Azure para o Armazenamento do Microsoft Azure](../common/storage-client-side-encryption.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="a1729-116">For an overview of client-side encryption for Azure Storage, see [Client-Side Encryption and Azure Key Vault for Microsoft Azure Storage](../common/storage-client-side-encryption.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json)</span></span>

<span data-ttu-id="a1729-117">Aqui está uma breve descrição de como funciona a criptografia do lado do cliente:</span><span class="sxs-lookup"><span data-stu-id="a1729-117">Here is a brief description of how client side encryption works:</span></span>

1. <span data-ttu-id="a1729-118">SDK de cliente de armazenamento do Azure Hello gera uma chave de criptografia do conteúdo (CEK), que é uma chave simétrica do uso de uma vez.</span><span class="sxs-lookup"><span data-stu-id="a1729-118">hello Azure Storage client SDK generates a content encryption key (CEK), which is a one-time-use symmetric key.</span></span>
2. <span data-ttu-id="a1729-119">Os dados do cliente são criptografados usando essa CEK.</span><span class="sxs-lookup"><span data-stu-id="a1729-119">Customer data is encrypted using this CEK.</span></span>
3. <span data-ttu-id="a1729-120">Olá CEK é fornecida (criptografada) usando a chave de criptografia de chave da saudação (KEK).</span><span class="sxs-lookup"><span data-stu-id="a1729-120">hello CEK is then wrapped (encrypted) using hello key encryption key (KEK).</span></span> <span data-ttu-id="a1729-121">Olá KEK é identificada por um identificador de chave e pode ser um par de chaves assimétricas ou uma chave simétrica e podem ser gerenciado localmente ou armazenada no cofre de chaves do Azure.</span><span class="sxs-lookup"><span data-stu-id="a1729-121">hello KEK is identified by a key identifier and can be an asymmetric key pair or a symmetric key and can be managed locally or stored in Azure Key Vault.</span></span> <span data-ttu-id="a1729-122">cliente de armazenamento Olá próprio nunca tem acesso toohello KEK.</span><span class="sxs-lookup"><span data-stu-id="a1729-122">hello Storage client itself never has access toohello KEK.</span></span> <span data-ttu-id="a1729-123">Ele apenas invoca o algoritmo de chave encapsulamento Olá fornecida pelo Cofre de chaves.</span><span class="sxs-lookup"><span data-stu-id="a1729-123">It just invokes hello key wrapping algorithm that is provided by Key Vault.</span></span> <span data-ttu-id="a1729-124">Os clientes podem escolher provedores personalizados de toouse chave encapsulamento/desencapsulamento se desejarem.</span><span class="sxs-lookup"><span data-stu-id="a1729-124">Customers can choose toouse custom providers for key wrapping/unwrapping if they want.</span></span>
4. <span data-ttu-id="a1729-125">Olá os dados criptografados são, em seguida, carregar toohello serviço de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="a1729-125">hello encrypted data is then uploaded toohello Azure Storage service.</span></span>

## <a name="set-up-your-azure-key-vault"></a><span data-ttu-id="a1729-126">Configure o seu Cofre da Chave do Azure</span><span class="sxs-lookup"><span data-stu-id="a1729-126">Set up your Azure Key Vault</span></span>
<span data-ttu-id="a1729-127">Na ordem tooproceed com este tutorial, você precisa Olá toodo etapas, que são descritas no tutorial Olá [Introdução ao Azure Key Vault](../../key-vault/key-vault-get-started.md):</span><span class="sxs-lookup"><span data-stu-id="a1729-127">In order tooproceed with this tutorial, you need toodo hello following steps, which are outlined in hello tutorial  [Get started with Azure Key Vault](../../key-vault/key-vault-get-started.md):</span></span>

* <span data-ttu-id="a1729-128">Crie um cofre da chave.</span><span class="sxs-lookup"><span data-stu-id="a1729-128">Create a key vault.</span></span>
* <span data-ttu-id="a1729-129">Adicione uma chave ou segredo toohello Cofre de chaves.</span><span class="sxs-lookup"><span data-stu-id="a1729-129">Add a key or secret toohello key vault.</span></span>
* <span data-ttu-id="a1729-130">Registre um aplicativo com o Active Directory do Azure.</span><span class="sxs-lookup"><span data-stu-id="a1729-130">Register an application with Azure Active Directory.</span></span>
* <span data-ttu-id="a1729-131">Autorize Olá aplicativo toouse Olá chave ou segredo.</span><span class="sxs-lookup"><span data-stu-id="a1729-131">Authorize hello application toouse hello key or secret.</span></span>

<span data-ttu-id="a1729-132">Verifique a nota da saudação ClientID e ClientSecret que foram gerados ao registrar um aplicativo com o Active Directory do Azure.</span><span class="sxs-lookup"><span data-stu-id="a1729-132">Make note of hello ClientID and ClientSecret that were generated when registering an application with Azure Active Directory.</span></span>

<span data-ttu-id="a1729-133">Crie as chaves no cofre de chaves hello.</span><span class="sxs-lookup"><span data-stu-id="a1729-133">Create both keys in hello key vault.</span></span> <span data-ttu-id="a1729-134">Vamos supor restante de saudação do tutorial de saudação que você usou Olá nomes a seguir: ContosoKeyVault e TestRSAKey1.</span><span class="sxs-lookup"><span data-stu-id="a1729-134">We assume for hello rest of hello tutorial that you have used hello following names: ContosoKeyVault and TestRSAKey1.</span></span>

## <a name="create-a-console-application-with-packages-and-appsettings"></a><span data-ttu-id="a1729-135">Criar um aplicativo de console com pacotes e AppSettings</span><span class="sxs-lookup"><span data-stu-id="a1729-135">Create a console application with packages and AppSettings</span></span>
<span data-ttu-id="a1729-136">No Visual Studio, crie um novo aplicativo de console.</span><span class="sxs-lookup"><span data-stu-id="a1729-136">In Visual Studio, create a new console application.</span></span>

<span data-ttu-id="a1729-137">Adicione pacotes nuget necessárias no hello Package Manager Console.</span><span class="sxs-lookup"><span data-stu-id="a1729-137">Add necessary nuget packages in hello Package Manager Console.</span></span>

```
Install-Package WindowsAzure.Storage

// This is hello latest stable release for ADAL.
Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -Version 2.16.204221202

Install-Package Microsoft.Azure.KeyVault
Install-Package Microsoft.Azure.KeyVault.Extensions
```

<span data-ttu-id="a1729-138">Adicione toohello AppSettings App. config.</span><span class="sxs-lookup"><span data-stu-id="a1729-138">Add AppSettings toohello App.Config.</span></span>

```xml
<appSettings>
    <add key="accountName" value="myaccount"/>
    <add key="accountKey" value="theaccountkey"/>
    <add key="clientId" value="theclientid"/>
    <add key="clientSecret" value="theclientsecret"/>
    <add key="container" value="stuff"/>
</appSettings>
```

<span data-ttu-id="a1729-139">Adicione o seguinte Olá `using` instruções e certifique-se de que tooadd um projeto de toohello de tooSystem.Configuration de referência.</span><span class="sxs-lookup"><span data-stu-id="a1729-139">Add hello following `using` statements and make sure tooadd a reference tooSystem.Configuration toohello project.</span></span>

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

## <a name="add-a-method-tooget-a-token-tooyour-console-application"></a><span data-ttu-id="a1729-140">Adicionar um método tooget um aplicativo de console tooyour token</span><span class="sxs-lookup"><span data-stu-id="a1729-140">Add a method tooget a token tooyour console application</span></span>
<span data-ttu-id="a1729-141">Olá método a seguir é usado pelas classes de Cofre de chaves que precisam tooauthenticate para Cofre de chaves de tooyour de acesso.</span><span class="sxs-lookup"><span data-stu-id="a1729-141">hello following method is used by Key Vault classes that need tooauthenticate for access tooyour key vault.</span></span>

```csharp
private async static Task<string> GetToken(string authority, string resource, string scope)
{
    var authContext = new AuthenticationContext(authority);
    ClientCredential clientCred = new ClientCredential(
        ConfigurationManager.AppSettings["clientId"],
        ConfigurationManager.AppSettings["clientSecret"]);
    AuthenticationResult result = await authContext.AcquireTokenAsync(resource, clientCred);

    if (result == null)
        throw new InvalidOperationException("Failed tooobtain hello JWT token");

    return result.AccessToken;
}
```

## <a name="access-storage-and-key-vault-in-your-program"></a><span data-ttu-id="a1729-142">Acessar o Armazenamento e o Cofre da Chave em seu programa</span><span class="sxs-lookup"><span data-stu-id="a1729-142">Access Storage and Key Vault in your program</span></span>
<span data-ttu-id="a1729-143">Olá função Main, adiciona Olá código a seguir.</span><span class="sxs-lookup"><span data-stu-id="a1729-143">In hello Main function, add hello following code.</span></span>

```csharp
// This is standard code toointeract with Blob storage.
StorageCredentials creds = new StorageCredentials(
    ConfigurationManager.AppSettings["accountName"],
       ConfigurationManager.AppSettings["accountKey"]);
CloudStorageAccount account = new CloudStorageAccount(creds, useHttps: true);
CloudBlobClient client = account.CreateCloudBlobClient();
CloudBlobContainer contain = client.GetContainerReference(ConfigurationManager.AppSettings["container"]);
contain.CreateIfNotExists();

// hello Resolver object is used toointeract with Key Vault for Azure Storage.
// This is where hello GetToken method from above is used.
KeyVaultKeyResolver cloudResolver = new KeyVaultKeyResolver(GetToken);
```

> [!NOTE]
> <span data-ttu-id="a1729-144">Modelos de Objetos de Chave de Cofre</span><span class="sxs-lookup"><span data-stu-id="a1729-144">Key Vault Object Models</span></span>
> 
> <span data-ttu-id="a1729-145">É importante toounderstand que há, na verdade, os dois objetos de Cofre de chaves modelos toobe atento: um é baseado em Olá API REST (namespace KeyVault) e outros Olá é uma extensão para a criptografia do lado do cliente.</span><span class="sxs-lookup"><span data-stu-id="a1729-145">It is important toounderstand that there are actually two Key Vault object models toobe aware of: one is based on hello REST API (KeyVault namespace) and hello other is an extension for client-side encryption.</span></span>
> 
> <span data-ttu-id="a1729-146">Olá chave cofre cliente interage com hello API REST e entenda JSON Web chaves e segredos para dois tipos de saudação de coisas que estão contidos no cofre de chaves.</span><span class="sxs-lookup"><span data-stu-id="a1729-146">hello Key Vault Client interacts with hello REST API and understands JSON Web Keys and secrets for hello two kinds of things that are contained in Key Vault.</span></span>
> 
> <span data-ttu-id="a1729-147">Extensões de Cofre de chave Olá são classes que parecem especificamente criadas para a criptografia do lado do cliente no armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="a1729-147">hello Key Vault Extensions are classes that seem specifically created for client-side encryption in Azure Storage.</span></span> <span data-ttu-id="a1729-148">Elas contêm uma interface para chaves (IKey) e classes com base no conceito de saudação de um resolvedor de chave.</span><span class="sxs-lookup"><span data-stu-id="a1729-148">They contain an interface for keys (IKey) and classes based on hello concept of a Key Resolver.</span></span> <span data-ttu-id="a1729-149">Há duas implementações do IKey que você precisa tooknow: RSAKey e SymmetricKey.</span><span class="sxs-lookup"><span data-stu-id="a1729-149">There are two implementations of IKey that you need tooknow: RSAKey and SymmetricKey.</span></span> <span data-ttu-id="a1729-150">Agora que ocorram toocoincide itens Olá que estão contidos em um cofre de chaves, mas agora são independentes classes (forma Olá chave e o segredo recuperada por Olá cliente de Cofre de chave não implementam IKey).</span><span class="sxs-lookup"><span data-stu-id="a1729-150">Now they happen toocoincide with hello things that are contained in a Key Vault, but at this point they are independent classes (so hello Key and Secret retrieved by hello Key Vault Client do not implement IKey).</span></span>
> 
> 

## <a name="encrypt-blob-and-upload"></a><span data-ttu-id="a1729-151">Criptografar o blob e carregar</span><span class="sxs-lookup"><span data-stu-id="a1729-151">Encrypt blob and upload</span></span>
<span data-ttu-id="a1729-152">Adicione a seguinte Olá tooencrypt um blob de código e carregá-lo tooyour conta de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="a1729-152">Add hello following code tooencrypt a blob and upload it tooyour Azure storage account.</span></span> <span data-ttu-id="a1729-153">Olá **ResolveKeyAsync** método retorna um IKey.</span><span class="sxs-lookup"><span data-stu-id="a1729-153">hello **ResolveKeyAsync** method that is used returns an IKey.</span></span>

```csharp
// Retrieve hello key that you created previously.
// hello IKey that is returned here is an RsaKey.
// Remember that we used hello names contosokeyvault and testrsakey1.
var rsa = cloudResolver.ResolveKeyAsync("https://contosokeyvault.vault.azure.net/keys/TestRSAKey1", CancellationToken.None).GetAwaiter().GetResult();

// Now you simply use hello RSA key tooencrypt by setting it in hello BlobEncryptionPolicy.
BlobEncryptionPolicy policy = new BlobEncryptionPolicy(rsa, null);
BlobRequestOptions options = new BlobRequestOptions() { EncryptionPolicy = policy };

// Reference a block blob.
CloudBlockBlob blob = contain.GetBlockBlobReference("MyFile.txt");

// Upload using hello UploadFromStream method.
using (var stream = System.IO.File.OpenRead(@"C:\data\MyFile.txt"))
    blob.UploadFromStream(stream, stream.Length, null, options, null);
```

<span data-ttu-id="a1729-154">A seguir está uma captura de tela de saudação [Portal clássico do Azure](https://manage.windowsazure.com) para um blob que foi criptografado usando a criptografia do lado do cliente com uma chave armazenada no cofre de chaves.</span><span class="sxs-lookup"><span data-stu-id="a1729-154">Following is a screenshot from hello [Azure Classic Portal](https://manage.windowsazure.com) for a blob that has been encrypted by using client-side encryption with a key stored in Key Vault.</span></span> <span data-ttu-id="a1729-155">Olá **KeyId** propriedade é hello URI para a chave de saudação no cofre de chaves que atua como Olá KEK.</span><span class="sxs-lookup"><span data-stu-id="a1729-155">hello **KeyId** property is hello URI for hello key in Key Vault that acts as hello KEK.</span></span> <span data-ttu-id="a1729-156">Olá **EncryptedKey** propriedade contém a versão criptografada Olá Olá CEK.</span><span class="sxs-lookup"><span data-stu-id="a1729-156">hello **EncryptedKey** property contains hello encrypted version of hello CEK.</span></span>

![Captura de tela mostrando os metadados de Blob que inclui metadados de criptografia](./media/storage-encrypt-decrypt-blobs-key-vault/blobmetadata.png)

> [!NOTE]
> <span data-ttu-id="a1729-158">Se você observar o construtor de BlobEncryptionPolicy hello, você verá que ele pode aceitar uma chave e/ou um resolvedor.</span><span class="sxs-lookup"><span data-stu-id="a1729-158">If you look at hello BlobEncryptionPolicy constructor, you will see that it can accept a key and/or a resolver.</span></span> <span data-ttu-id="a1729-159">Lembre-se de que agora, você não pode usar um resolvedor para criptografia porque atualmente não dá suporte a uma chave padrão.</span><span class="sxs-lookup"><span data-stu-id="a1729-159">Be aware that right now you cannot use a resolver for encryption because it does not currently support a default key.</span></span>
> 
> 

## <a name="decrypt-blob-and-download"></a><span data-ttu-id="a1729-160">Descriptografar o blob e baixar</span><span class="sxs-lookup"><span data-stu-id="a1729-160">Decrypt blob and download</span></span>
<span data-ttu-id="a1729-161">Descriptografia é realmente quando usando Olá resolvedor classes fazem sentido.</span><span class="sxs-lookup"><span data-stu-id="a1729-161">Decryption is really when using hello Resolver classes make sense.</span></span> <span data-ttu-id="a1729-162">ID de saudação do hello chave usada para criptografia está associado ao blob Olá em seus metadados, portanto não há nenhum motivo para a chave Olá tooretrieve e lembre-se de associação de saudação entre chave e o blob.</span><span class="sxs-lookup"><span data-stu-id="a1729-162">hello ID of hello key used for encryption is associated with hello blob in its metadata, so there is no reason for you tooretrieve hello key and remember hello association between key and blob.</span></span> <span data-ttu-id="a1729-163">Você tem apenas toomake se que essa chave Olá permanece no cofre de chaves.</span><span class="sxs-lookup"><span data-stu-id="a1729-163">You just have toomake sure that hello key remains in Key Vault.</span></span>   

<span data-ttu-id="a1729-164">chave privada de saudação do permanece chave RSA no cofre de chaves, então para descriptografia toooccur, Olá a chave criptografada da saudação metadados de blob que contém Olá CEK é enviada tooKey cofre para descriptografia.</span><span class="sxs-lookup"><span data-stu-id="a1729-164">hello private key of an RSA Key remains in Key Vault, so for decryption toooccur, hello Encrypted Key from hello blob metadata that contains hello CEK is sent tooKey Vault for decryption.</span></span>

<span data-ttu-id="a1729-165">Adicione Olá seguindo o blob de saudação toodecrypt que você acabou de ser carregado.</span><span class="sxs-lookup"><span data-stu-id="a1729-165">Add hello following toodecrypt hello blob that you just uploaded.</span></span>

```csharp
// In this case, we will not pass a key and only pass hello resolver because
// this policy will only be used for downloading / decrypting.
BlobEncryptionPolicy policy = new BlobEncryptionPolicy(null, cloudResolver);
BlobRequestOptions options = new BlobRequestOptions() { EncryptionPolicy = policy };

using (var np = File.Open(@"C:\data\MyFileDecrypted.txt", FileMode.Create))
    blob.DownloadToStream(np, null, options, null);
```

> [!NOTE]
> <span data-ttu-id="a1729-166">Há alguns outros tipos de gerenciamento de chaves resolvedores toomake mais fácil, incluindo: AggregateKeyResolver e CachingKeyResolver.</span><span class="sxs-lookup"><span data-stu-id="a1729-166">There are a couple of other kinds of resolvers toomake key management easier, including: AggregateKeyResolver and CachingKeyResolver.</span></span>
> 
> 

## <a name="use-key-vault-secrets"></a><span data-ttu-id="a1729-167">Usar os segredos do Cofre da Chave</span><span class="sxs-lookup"><span data-stu-id="a1729-167">Use Key Vault secrets</span></span>
<span data-ttu-id="a1729-168">Olá maneira toouse um segredo com criptografia do lado do cliente é por meio de saudação SymmetricKey classe como um segredo é essencialmente uma chave simétrica.</span><span class="sxs-lookup"><span data-stu-id="a1729-168">hello way toouse a secret with client-side encryption is via hello SymmetricKey class because a secret is essentially a symmetric key.</span></span> <span data-ttu-id="a1729-169">Mas, conforme observado acima, um segredo no cofre de chaves não mapeia exatamente tooa SymmetricKey.</span><span class="sxs-lookup"><span data-stu-id="a1729-169">But, as noted above, a secret in Key Vault does not map exactly tooa SymmetricKey.</span></span> <span data-ttu-id="a1729-170">Há alguns toounderstand de coisas:</span><span class="sxs-lookup"><span data-stu-id="a1729-170">There are a few things toounderstand:</span></span>

* <span data-ttu-id="a1729-171">chave de saudação em um SymmetricKey tem toobe um comprimento fixo: 128, 192, 256, 384 ou 512 bits.</span><span class="sxs-lookup"><span data-stu-id="a1729-171">hello key in a SymmetricKey has toobe a fixed length: 128, 192, 256, 384, or 512 bits.</span></span>
* <span data-ttu-id="a1729-172">chave de saudação em um SymmetricKey deve ser codificada em Base64.</span><span class="sxs-lookup"><span data-stu-id="a1729-172">hello key in a SymmetricKey should be Base64 encoded.</span></span>
* <span data-ttu-id="a1729-173">Precisa de um segredo do Cofre de chaves que será usado como um SymmetricKey toohave um tipo de conteúdo de "application/octet-stream" no cofre de chaves.</span><span class="sxs-lookup"><span data-stu-id="a1729-173">A Key Vault secret that will be used as a SymmetricKey needs toohave a Content Type of "application/octet-stream" in Key Vault.</span></span>

<span data-ttu-id="a1729-174">Aqui está um exemplo no PowerShell sobre a criação de um segredo no Cofre da Chave que pode ser usado como uma SymmetricKey.</span><span class="sxs-lookup"><span data-stu-id="a1729-174">Here is an example in PowerShell of creating a secret in Key Vault that can be used as a SymmetricKey.</span></span>
<span data-ttu-id="a1729-175">Observe que o valor de saudação rígido codificada, $key, é apenas a fins de demonstração.</span><span class="sxs-lookup"><span data-stu-id="a1729-175">Please note that hello hard coded value, $key, is for demonstration purpose only.</span></span> <span data-ttu-id="a1729-176">Em seu próprio código convém toogenerate essa chave.</span><span class="sxs-lookup"><span data-stu-id="a1729-176">In your own code you'll want toogenerate this key.</span></span>

```csharp
// Here we are making a 128-bit key so we have 16 characters.
//     hello characters are in hello ASCII range of UTF8 so they are
//    each 1 byte. 16 x 8 = 128.
$key = "qwertyuiopasdfgh"
$b = [System.Text.Encoding]::UTF8.GetBytes($key)
$enc = [System.Convert]::ToBase64String($b)
$secretvalue = ConvertTo-SecureString $enc -AsPlainText -Force

// Substitute hello VaultName and Name in this command.
$secret = Set-AzureKeyVaultSecret -VaultName 'ContoseKeyVault' -Name 'TestSecret2' -SecretValue $secretvalue -ContentType "application/octet-stream"
```

<span data-ttu-id="a1729-177">Em seu aplicativo de console, você pode usar o hello mesma chamada anterior tooretrieve nesse secreta como um SymmetricKey.</span><span class="sxs-lookup"><span data-stu-id="a1729-177">In your console application, you can use hello same call as before tooretrieve this secret as a SymmetricKey.</span></span>

```csharp
SymmetricKey sec = (SymmetricKey) cloudResolver.ResolveKeyAsync(
    "https://contosokeyvault.vault.azure.net/secrets/TestSecret2/",
    CancellationToken.None).GetAwaiter().GetResult();
```
<span data-ttu-id="a1729-178">É isso.</span><span class="sxs-lookup"><span data-stu-id="a1729-178">That's it.</span></span> <span data-ttu-id="a1729-179">Aproveite!</span><span class="sxs-lookup"><span data-stu-id="a1729-179">Enjoy!</span></span>

## <a name="next-steps"></a><span data-ttu-id="a1729-180">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="a1729-180">Next steps</span></span>
<span data-ttu-id="a1729-181">Para obter mais informações sobre como usar o Armazenamento do Microsoft Azure com C#, consulte [Biblioteca de cliente de Armazenamento do Microsoft Azure para .NET](https://msdn.microsoft.com/library/azure/dn261237.aspx).</span><span class="sxs-lookup"><span data-stu-id="a1729-181">For more information about using Microsoft Azure Storage with C#, see [Microsoft Azure Storage Client Library for .NET](https://msdn.microsoft.com/library/azure/dn261237.aspx).</span></span>

<span data-ttu-id="a1729-182">Para obter mais informações sobre Olá API REST do Blob, consulte [API REST do serviço Blob](https://msdn.microsoft.com/library/azure/dd135733.aspx).</span><span class="sxs-lookup"><span data-stu-id="a1729-182">For more information about hello Blob REST API, see [Blob Service REST API](https://msdn.microsoft.com/library/azure/dd135733.aspx).</span></span>

<span data-ttu-id="a1729-183">Para obter informações mais recentes do hello no armazenamento do Microsoft Azure, vá toohello [Blog da equipe de armazenamento do Microsoft Azure](http://blogs.msdn.com/b/windowsazurestorage/).</span><span class="sxs-lookup"><span data-stu-id="a1729-183">For hello latest information on Microsoft Azure Storage, go toohello [Microsoft Azure Storage Team Blog](http://blogs.msdn.com/b/windowsazurestorage/).</span></span>
