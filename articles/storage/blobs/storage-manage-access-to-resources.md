---
title: "acesso de leitura público aaaEnable para contêineres e blobs no armazenamento de BLOBs do Azure | Microsoft Docs"
description: "Saiba como toomake contêineres e blobs disponíveis para acesso anônimo e como tooaccess-los por meio de programação."
services: storage
documentationcenter: 
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: a2cffee6-3224-4f2a-8183-66ca23b2d2d7
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: marsma
ms.openlocfilehash: dd8ffdb39a66aa06f65ad3cdd4315d47c117f059
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-anonymous-read-access-toocontainers-and-blobs"></a>Gerenciar blobs e acesso de leitura anônimo toocontainers
Você pode habilitar o acesso de leitura anônimo, public tooa contêiner e seus blobs no armazenamento de BLOBs do Azure. Fazendo isso, você pode conceder recursos do acesso somente leitura toothese sem compartilhar sua chave de conta e sem a necessidade de uma assinatura de acesso compartilhado (SAS).

Acesso de leitura público é melhor para cenários onde você deseja que determinados blobs tooalways esteja disponível para acesso de leitura anônimo. Para ter um controle mais refinado, você pode criar uma assinatura de acesso compartilhado. Assinaturas de acesso compartilhado permitem acesso de tooprovide restringido usando permissões diferentes, por um período de tempo específico. Para saber mais sobre como criar assinaturas de acesso compartilhado, veja [Usando SAS (Assinaturas de Acesso Compartilhado) no Armazenamento do Azure](../common/storage-dotnet-shared-access-signature-part-1.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json).

## <a name="grant-anonymous-users-permissions-toocontainers-and-blobs"></a>Conceder a usuários anônimos permissões toocontainers e blobs
Por padrão, um contêiner e todos os blobs dentro dele podem ser acessados somente pelo proprietário Olá Olá da conta de armazenamento. contêiner de tooa toogive usuários anônimos permissões de leitura e seus blobs, você pode definir o acesso público do hello contêiner permissões tooallow. Usuários anônimos podem ler blobs dentro de um contêiner publicamente acessível sem autenticar a solicitação de saudação.

Você pode configurar um contêiner com hello as seguintes permissões:

* **Acesso de leitura não público:** Olá contêiner e seus blobs podem ser acessados somente pelo proprietário da conta de armazenamento hello. Esse é o padrão de Olá para todos os novos contêineres.
* **Acesso para blobs somente de leitura público:** Blobs no contêiner Olá podem ser lidos por solicitação anônima, mas os dados do contêiner não estão disponíveis. Clientes anônimos não é possível enumerar blobs hello dentro do contêiner de saudação.
* **Acesso de leitura público completo:** todos os dados de contêiner e blob podem ser lidos por solicitação anônima. Os clientes podem enumerar blobs no contêiner de saudação por solicitação anônima, mas não é possível enumerar os contêineres na conta de armazenamento hello.

Você pode usar as seguintes permissões de contêiner de tooset de saudação:

* [Portal do Azure](https://portal.azure.com)
* [Azure PowerShell](../common/storage-powershell-guide-full.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json#how-to-manage-azure-blobs)
* [CLI 2.0 do Azure](../common/storage-azure-cli.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json#create-and-manage-blobs)
* Programaticamente, usando uma das bibliotecas de cliente de armazenamento hello ou hello API REST

### <a name="set-container-permissions-in-hello-azure-portal"></a>Definir permissões de contêiner de saudação portal do Azure
permissões do contêiner tooset no hello [portal do Azure](https://portal.azure.com), siga estas etapas:

1. Abra o **conta de armazenamento** folha no portal de saudação. Você pode encontrar sua conta de armazenamento selecionando **contas de armazenamento** na folha do menu principal do portal de saudação.
1. Em **serviço BLOB** na folha de menu hello, selecione **contêineres**.
1. Clique na linha do contêiner de saudação ou do contêiner do hello selecione reticências tooopen Olá **menu de contexto**.
1. Selecione **política de acesso** no menu de contexto de saudação.
1. Selecione um **tipo de acesso** de saudação menu suspenso.

    ![Caixa de diálogo Editar Metadados do Contêiner](./media/storage-manage-access-to-resources/storage-manage-access-to-resources-0.png)

### <a name="set-container-permissions-with-net"></a>Definir permissões de contêiner com .NET
tooset permissões para um contêiner usando o c# e hello biblioteca de cliente de armazenamento para .NET, recuperar as permissões existentes do contêiner Olá por chamada hello **GetPermissions** método. Saudação de conjunto, em seguida, **PublicAccess** propriedade Olá **BlobContainerPermissions** objeto que é retornado pelo Olá **GetPermissions** método. Finalmente, chame Olá **SetPermissions** método com hello atualizado permissões.

saudação de exemplo a seguir define permissões do contêiner Olá toofull acesso de leitura público. tooset permissões toopublic acesso de leitura para blobs, defina Olá **PublicAccess** propriedade muito**BlobContainerPublicAccessType.Blob**. conjunto de todas as permissões para usuários anônimos, tooremove Olá propriedade muito**BlobContainerPublicAccessType.Off**.

```csharp
public static void SetPublicContainerPermissions(CloudBlobContainer container)
{
    BlobContainerPermissions permissions = container.GetPermissions();
    permissions.PublicAccess = BlobContainerPublicAccessType.Container;
    container.SetPermissions(permissions);
}
```

## <a name="access-containers-and-blobs-anonymously"></a>Acessar contêineres e blobs anonimamente
Um cliente que acessa contêineres e blobs anonimamente pode usar construtores que não necessitam de credenciais. Olá exemplos a seguir mostra algumas maneiras diferentes de recursos do serviço Blob tooreference anonimamente.

### <a name="create-an-anonymous-client-object"></a>Criar um objeto de cliente anônimo
Você pode criar um novo objeto de cliente de serviço para acesso anônimo, fornecendo o ponto de extremidade de serviço de Blob Olá para conta de saudação. No entanto, você também deve saber o nome de saudação de um contêiner nessa conta que está disponível para acesso anônimo.

```csharp
public static void CreateAnonymousBlobClient()
{
    // Create hello client object using hello Blob service endpoint.
    CloudBlobClient blobClient = new CloudBlobClient(new Uri(@"https://storagesample.blob.core.windows.net"));

    // Get a reference tooa container that's available for anonymous access.
    CloudBlobContainer container = blobClient.GetContainerReference("sample-container");

    // Read hello container's properties. Note this is only possible when hello container supports full public read access.
    container.FetchAttributes();
    Console.WriteLine(container.Properties.LastModified);
    Console.WriteLine(container.Properties.ETag);
}
```

### <a name="reference-a-container-anonymously"></a>Fazer referência a um contêiner anonimamente
Se você tiver Olá URL tooa contêiner anonimamente disponível, você pode usá-lo contêiner de saudação tooreference diretamente.

```csharp
public static void ListBlobsAnonymously()
{
    // Get a reference tooa container that's available for anonymous access.
    CloudBlobContainer container = new CloudBlobContainer(new Uri(@"https://storagesample.blob.core.windows.net/sample-container"));

    // List blobs in hello container.
    foreach (IListBlobItem blobItem in container.ListBlobs())
    {
        Console.WriteLine(blobItem.Uri);
    }
}
```

### <a name="reference-a-blob-anonymously"></a>Fazer referência a um blob anonimamente
Se você tiver um blob Olá de tooa de URL que está disponível para acesso anônimo, você pode referenciar blob Olá diretamente usando essa URL:

```csharp
public static void DownloadBlobAnonymously()
{
    CloudBlockBlob blob = new CloudBlockBlob(new Uri(@"https://storagesample.blob.core.windows.net/sample-container/logfile.txt"));
    blob.DownloadToFile(@"C:\Temp\logfile.txt", System.IO.FileMode.Create);
}
```

## <a name="features-available-tooanonymous-users"></a>Recursos que os usuários tooanonymous disponíveis
Olá, a tabela a seguir mostra quais operações podem ser chamadas por usuários anônimos quando a ACL do contêiner é definir o acesso público de tooallow.

| Operação REST | Permissão com acesso de leitura público completo | Permissão de acesso de leitura público apenas para blobs |
| --- | --- | --- |
| Listar contêineres |Somente proprietário |Somente proprietário |
| Create Container |Somente proprietário |Somente proprietário |
| Get Container Properties |Todos |Somente proprietário |
| Get Container Metadata |Todos |Somente proprietário |
| Set Container Metadata |Somente proprietário |Somente proprietário |
| Get Container ACL |Somente proprietário |Somente proprietário |
| Set Container ACL |Somente proprietário |Somente proprietário |
| Delete Container |Somente proprietário |Somente proprietário |
| Listar Blobs |Todos |Somente proprietário |
| Put Blob |Somente proprietário |Somente proprietário |
| Get Blob |Todos |Todos |
| Get Blob Properties |Todos |Todos |
| Set Blob Properties |Somente proprietário |Somente proprietário |
| Get Blob Metadata |Todos |Todos |
| Set Blob Metadata |Somente proprietário |Somente proprietário |
| Put Block |Somente proprietário |Somente proprietário |
| Obter lista de blocos (somente blocos confirmados) |Todos |Todos |
| Obter lista de blocos (somente blocos não confirmados ou todos os blocos) |Somente proprietário |Somente proprietário |
| Put Block List |Somente proprietário |Somente proprietário |
| Delete Blob |Somente proprietário |Somente proprietário |
| Copiar blob |Somente proprietário |Somente proprietário |
| Blob de instantâneo |Somente proprietário |Somente proprietário |
| Lease Blob |Somente proprietário |Somente proprietário |
| Put Page |Somente proprietário |Somente proprietário |
| Get Page Ranges |Todos |Todos |
| Acrescentar blob |Somente proprietário |Somente proprietário |

## <a name="next-steps"></a>Próximas etapas

* [Autenticação para Olá serviços de armazenamento do Azure](https://msdn.microsoft.com/library/azure/dd179428.aspx)
* [Uso de SAS (Assinaturas de Acesso Compartilhado)](../common/storage-dotnet-shared-access-signature-part-1.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json)
* [Delegando acesso com uma assinatura de acesso compartilhado](https://msdn.microsoft.com/library/azure/ee395415.aspx)
