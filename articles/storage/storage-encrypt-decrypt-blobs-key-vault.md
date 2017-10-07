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
ms.openlocfilehash: 3eb64f104f378dd09ef295c94e03167655883391
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-encrypt-and-decrypt-blobs-in-microsoft-azure-storage-using-azure-key-vault"></a>Tutorial: criptografar e descriptografar blobs no Armazenamento do Microsoft Azure usando o Cofre da Chave do Azure
## <a name="introduction"></a>Introdução
Este tutorial aborda como toomake o uso de criptografia de armazenamento do cliente com o Cofre de chaves do Azure. Ele orienta como tooencrypt e descriptografar um blob em um aplicativo de console usando essas tecnologias.

**Estimado tempo toocomplete:** 20 minutos

Para obter informações gerais sobre o Cofre de Chaves do Azure, consulte [O que é o Cofre de Chaves do Azure?](../key-vault/key-vault-whatis.md).

Para obter informações gerais sobre a criptografia de cliente do armazenamento do Azure, consulte [Criptografia do lado do cliente e Cofre de Chaves do Azure para o Armazenamento do Microsoft Azure](storage-client-side-encryption.md).

## <a name="prerequisites"></a>Pré-requisitos
toocomplete neste tutorial, você deve ter Olá a seguir:

* Uma conta de armazenamento do Azure
* Visual Studio 2013 ou posterior.
* Azure PowerShell

## <a name="overview-of-client-side-encryption"></a>Visão geral da criptografia do lado do cliente
Para obter uma visão geral da criptografia do lado do cliente do Armazenamento do Azure, consulte [Criptografia do lado do cliente e o Cofre de Chaves do Azure para o Armazenamento do Microsoft Azure](storage-client-side-encryption.md)

Aqui está uma breve descrição de como funciona a criptografia do lado do cliente:

1. SDK de cliente de armazenamento do Azure Hello gera uma chave de criptografia do conteúdo (CEK), que é uma chave simétrica do uso de uma vez.
2. Os dados do cliente são criptografados usando essa CEK.
3. Olá CEK é fornecida (criptografada) usando a chave de criptografia de chave da saudação (KEK). Olá KEK é identificada por um identificador de chave e pode ser um par de chaves assimétricas ou uma chave simétrica e podem ser gerenciado localmente ou armazenada no cofre de chaves do Azure. cliente de armazenamento Olá próprio nunca tem acesso toohello KEK. Ele apenas invoca o algoritmo de chave encapsulamento Olá fornecida pelo Cofre de chaves. Os clientes podem escolher provedores personalizados de toouse chave encapsulamento/desencapsulamento se desejarem.
4. Olá os dados criptografados são, em seguida, carregar toohello serviço de armazenamento do Azure.

## <a name="set-up-your-azure-key-vault"></a>Configure o seu Cofre da Chave do Azure
Na ordem tooproceed com este tutorial, você precisa Olá toodo etapas, que são descritas no tutorial Olá [Introdução ao Azure Key Vault](../key-vault/key-vault-get-started.md):

* Crie um cofre da chave.
* Adicione uma chave ou segredo toohello Cofre de chaves.
* Registre um aplicativo com o Active Directory do Azure.
* Autorize Olá aplicativo toouse Olá chave ou segredo.

Verifique a nota da saudação ClientID e ClientSecret que foram gerados ao registrar um aplicativo com o Active Directory do Azure.

Crie as chaves no cofre de chaves hello. Vamos supor restante de saudação do tutorial de saudação que você usou Olá nomes a seguir: ContosoKeyVault e TestRSAKey1.

## <a name="create-a-console-application-with-packages-and-appsettings"></a>Criar um aplicativo de console com pacotes e AppSettings
No Visual Studio, crie um novo aplicativo de console.

Adicione pacotes nuget necessárias no hello Package Manager Console.

```
Install-Package WindowsAzure.Storage

// This is hello latest stable release for ADAL.
Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -Version 2.16.204221202

Install-Package Microsoft.Azure.KeyVault
Install-Package Microsoft.Azure.KeyVault.Extensions
```

Adicione toohello AppSettings App. config.

```xml
<appSettings>
    <add key="accountName" value="myaccount"/>
    <add key="accountKey" value="theaccountkey"/>
    <add key="clientId" value="theclientid"/>
    <add key="clientSecret" value="theclientsecret"/>
    <add key="container" value="stuff"/>
</appSettings>
```

Adicione o seguinte Olá `using` instruções e certifique-se de que tooadd um projeto de toohello de tooSystem.Configuration de referência.

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

## <a name="add-a-method-tooget-a-token-tooyour-console-application"></a>Adicionar um método tooget um aplicativo de console tooyour token
Olá método a seguir é usado pelas classes de Cofre de chaves que precisam tooauthenticate para Cofre de chaves de tooyour de acesso.

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

## <a name="access-storage-and-key-vault-in-your-program"></a>Acessar o Armazenamento e o Cofre da Chave em seu programa
Olá função Main, adiciona Olá código a seguir.

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
> Modelos de Objetos de Chave de Cofre
> 
> É importante toounderstand que há, na verdade, os dois objetos de Cofre de chaves modelos toobe atento: um é baseado em Olá API REST (namespace KeyVault) e outros Olá é uma extensão para a criptografia do lado do cliente.
> 
> Olá chave cofre cliente interage com hello API REST e entenda JSON Web chaves e segredos para dois tipos de saudação de coisas que estão contidos no cofre de chaves.
> 
> Extensões de Cofre de chave Olá são classes que parecem especificamente criadas para a criptografia do lado do cliente no armazenamento do Azure. Elas contêm uma interface para chaves (IKey) e classes com base no conceito de saudação de um resolvedor de chave. Há duas implementações do IKey que você precisa tooknow: RSAKey e SymmetricKey. Agora que ocorram toocoincide itens Olá que estão contidos em um cofre de chaves, mas agora são independentes classes (forma Olá chave e o segredo recuperada por Olá cliente de Cofre de chave não implementam IKey).
> 
> 

## <a name="encrypt-blob-and-upload"></a>Criptografar o blob e carregar
Adicione a seguinte Olá tooencrypt um blob de código e carregá-lo tooyour conta de armazenamento do Azure. Olá **ResolveKeyAsync** método retorna um IKey.

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

A seguir está uma captura de tela de saudação [Portal clássico do Azure](https://manage.windowsazure.com) para um blob que foi criptografado usando a criptografia do lado do cliente com uma chave armazenada no cofre de chaves. Olá **KeyId** propriedade é hello URI para a chave de saudação no cofre de chaves que atua como Olá KEK. Olá **EncryptedKey** propriedade contém a versão criptografada Olá Olá CEK.

![Captura de tela mostrando os metadados de Blob que inclui metadados de criptografia](./media/storage-encrypt-decrypt-blobs-key-vault/blobmetadata.png)

> [!NOTE]
> Se você observar o construtor de BlobEncryptionPolicy hello, você verá que ele pode aceitar uma chave e/ou um resolvedor. Lembre-se de que agora, você não pode usar um resolvedor para criptografia porque atualmente não dá suporte a uma chave padrão.
> 
> 

## <a name="decrypt-blob-and-download"></a>Descriptografar o blob e baixar
Descriptografia é realmente quando usando Olá resolvedor classes fazem sentido. ID de saudação do hello chave usada para criptografia está associado ao blob Olá em seus metadados, portanto não há nenhum motivo para a chave Olá tooretrieve e lembre-se de associação de saudação entre chave e o blob. Você tem apenas toomake se que essa chave Olá permanece no cofre de chaves.   

chave privada de saudação do permanece chave RSA no cofre de chaves, então para descriptografia toooccur, Olá a chave criptografada da saudação metadados de blob que contém Olá CEK é enviada tooKey cofre para descriptografia.

Adicione Olá seguindo o blob de saudação toodecrypt que você acabou de ser carregado.

```csharp
// In this case, we will not pass a key and only pass hello resolver because
// this policy will only be used for downloading / decrypting.
BlobEncryptionPolicy policy = new BlobEncryptionPolicy(null, cloudResolver);
BlobRequestOptions options = new BlobRequestOptions() { EncryptionPolicy = policy };

using (var np = File.Open(@"C:\data\MyFileDecrypted.txt", FileMode.Create))
    blob.DownloadToStream(np, null, options, null);
```

> [!NOTE]
> Há alguns outros tipos de gerenciamento de chaves resolvedores toomake mais fácil, incluindo: AggregateKeyResolver e CachingKeyResolver.
> 
> 

## <a name="use-key-vault-secrets"></a>Usar os segredos do Cofre da Chave
Olá maneira toouse um segredo com criptografia do lado do cliente é por meio de saudação SymmetricKey classe como um segredo é essencialmente uma chave simétrica. Mas, conforme observado acima, um segredo no cofre de chaves não mapeia exatamente tooa SymmetricKey. Há alguns toounderstand de coisas:

* chave de saudação em um SymmetricKey tem toobe um comprimento fixo: 128, 192, 256, 384 ou 512 bits.
* chave de saudação em um SymmetricKey deve ser codificada em Base64.
* Precisa de um segredo do Cofre de chaves que será usado como um SymmetricKey toohave um tipo de conteúdo de "application/octet-stream" no cofre de chaves.

Aqui está um exemplo no PowerShell sobre a criação de um segredo no Cofre da Chave que pode ser usado como uma SymmetricKey.
Observe que o valor de saudação rígido codificada, $key, é apenas a fins de demonstração. Em seu próprio código convém toogenerate essa chave.

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

Em seu aplicativo de console, você pode usar o hello mesma chamada anterior tooretrieve nesse secreta como um SymmetricKey.

```csharp
SymmetricKey sec = (SymmetricKey) cloudResolver.ResolveKeyAsync(
    "https://contosokeyvault.vault.azure.net/secrets/TestSecret2/",
    CancellationToken.None).GetAwaiter().GetResult();
```
É isso. Aproveite!

## <a name="next-steps"></a>Próximas etapas
Para obter mais informações sobre como usar o Armazenamento do Microsoft Azure com C#, consulte [Biblioteca de cliente de Armazenamento do Microsoft Azure para .NET](https://msdn.microsoft.com/library/azure/dn261237.aspx).

Para obter mais informações sobre Olá API REST do Blob, consulte [API REST do serviço Blob](https://msdn.microsoft.com/library/azure/dd135733.aspx).

Para obter informações mais recentes do hello no armazenamento do Microsoft Azure, vá toohello [Blog da equipe de armazenamento do Microsoft Azure](http://blogs.msdn.com/b/windowsazurestorage/).
