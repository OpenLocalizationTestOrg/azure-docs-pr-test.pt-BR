---
title: "aaaCreate um instantâneo somente leitura de um blob no armazenamento do Azure | Microsoft Docs"
description: "Saiba como toocreate um instantâneo de um tooback blob os dados de blob em um determinado momento. Entender como os instantâneos são cobrados e toouse-los toominimize encargos de capacidade."
services: storage
documentationcenter: 
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: 3710705d-e127-4b01-8d0f-29853fb06d0d
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/11/2017
ms.author: marsma
ms.openlocfilehash: 9e7af611e885d83df69d3329217f261b3f3f333e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-blob-snapshot"></a>Criar um instantâneo de blob

Um instantâneo é uma versão somente leitura de um blob capturada em um momento no tempo. Os instantâneos são úteis para fazer backup de blobs. Depois de criar um instantâneo, você pode lê-lo, copiá-lo ou excluí-lo, mas não é possível modificá-lo.

Um instantâneo de um blob é blob de base tooits idênticos, exceto blob Olá URI tem um **DateTime** valor acrescentado hora toohello blob URI tooindicate Olá no qual Olá o instantâneo foi tirado. Por exemplo, se o URI de blob de uma página é `http://storagesample.core.blob.windows.net/mydrives/myvhd`, Olá instantâneo URI é muito semelhante`http://storagesample.core.blob.windows.net/mydrives/myvhd?snapshot=2011-03-09T01:42:34.9360000Z`.

> [!NOTE]
> Todos os instantâneos de compartilham o URI do blob base hello. Olá apenas distinção entre o blob de base hello e instantâneo Olá Olá acrescentado **DateTime** valor.
>

Um blob pode ter qualquer número de instantâneos. Os instantâneos persistem até que sejam explicitamente excluídos. Um instantâneo não pode durar mais que seu blob de base. Você pode enumerar instantâneos de saudação associados Olá blob de base tootrack seus instantâneos atuais.

Quando você cria um instantâneo de um blob, Olá propriedades do sistema do blob é copiados toohello instantâneo com hello mesmos valores. metadados do blob base Olá também são copiado toohello de instantâneo, a menos que você especificar metadados separados para Olá instantâneo ao criá-lo.

Quaisquer concessões associados com o blob de base Olá não afetam instantâneo hello. Não é possível adquirir uma concessão em um instantâneo.

Um arquivo VHD é usado toostore Olá as informações atuais e o status de um disco VM. Você pode desanexar um disco de dentro de saudação VM ou desligar Olá VM e, em seguida, tire um instantâneo do seu arquivo VHD. Você pode usar esse arquivo de instantâneo posterior tooretrieve Olá VHD do arquivo no momento e recrie Olá VM.

Se a criptografia de serviço de armazenamento (SSE) está habilitada para a conta de armazenamento Olá na qual Olá blob reside, todos os instantâneos de blob serão criptografados em repouso.

## <a name="create-a-snapshot"></a>Criar um instantâneo
Olá exemplo de código a seguir mostra como um instantâneo por meio de toocreate Olá [biblioteca de cliente de armazenamento do Azure para .NET](https://www.nuget.org/packages/WindowsAzure.Storage/). Este exemplo especifica os metadados adicionais para instantâneo de saudação quando ele é criado.

```csharp
private static async Task CreateBlockBlobSnapshot(CloudBlobContainer container)
{
    // Create a new block blob in hello container.
    CloudBlockBlob baseBlob = container.GetBlockBlobReference("sample-base-blob.txt");

    // Add blob metadata.
    baseBlob.Metadata.Add("ApproxBlobCreatedDate", DateTime.UtcNow.ToString());

    try
    {
        // Upload hello blob toocreate it, with its metadata.
        await baseBlob.UploadTextAsync(string.Format("Base blob: {0}", baseBlob.Uri.ToString()));

        // Sleep 5 seconds.
        System.Threading.Thread.Sleep(5000);

        // Create a snapshot of hello base blob.
        // Specify metadata at hello time that hello snapshot is created toospecify unique metadata for hello snapshot.
        // If no metadata is specified when hello snapshot is created, hello base blob's metadata is copied toohello snapshot.
        Dictionary<string, string> metadata = new Dictionary<string, string>();
        metadata.Add("ApproxSnapshotCreatedDate", DateTime.UtcNow.ToString());
        await baseBlob.CreateSnapshotAsync(metadata, null, null, null);
    }
    catch (StorageException e)
    {
        Console.WriteLine(e.Message);
        Console.ReadLine();
        throw;
    }
}
```

## <a name="copy-snapshots"></a>Copiar instantâneos
As operações de cópia que envolvem blobs e instantâneos seguem estas regras:

* Você pode copiar um instantâneo sobre seu blob de base. Promovendo uma posição de toohello de instantâneo de blob de base hello, você pode restaurar uma versão anterior de um blob. Olá instantâneo permanece, mas o blob de base de saudação é substituído por uma cópia gravável do instantâneo de saudação.
* Você pode copiar um blob de destino do instantâneo tooa com um nome diferente. blob de destino Olá resultante é um blob gravável e não um instantâneo.
* Quando um blob de origem é copiado, todos os instantâneos de blob de origem Olá não são copiados toohello destino. Quando um blob de destino é substituído por uma cópia, todos os instantâneos associados com o blob de destino original Olá permanecem intactos.
* Quando você cria um instantâneo de um blob de bloco, lista de blocos confirmados do blob Olá também é copiado toohello instantâneo. Todos os blocos não confirmados não são copiados.

## <a name="specify-an-access-condition"></a>Especificar uma condição de acesso
Quando você chama [CreateSnapshotAsync][dotnet_CreateSnapshotAsync], você pode especificar uma condição de acesso para que hello instantâneo é criado somente se uma condição for atendida. toospecify uma condição de acesso, use Olá [AccessCondition] [ dotnet_AccessCondition] parâmetro. Se Olá especificado condição não for atendida, Olá instantâneo não será criado e Olá serviço Blob retornará o código de status [HTTPStatusCode][dotnet_HTTPStatusCode]. PreconditionFailed.

## <a name="delete-snapshots"></a>Excluir instantâneos
Você não pode excluir um blob com instantâneos, a menos que os instantâneos de saudação também são excluídos. Você pode excluir um instantâneo individualmente ou especificar que todos os instantâneos de ser excluída quando o blob de origem Olá é excluído. Se você tentar toodelete um blob que ainda possui instantâneos, ocorrerá um erro.

Olá mostra exemplo de código a seguir como toodelete um blob e seus instantâneos no .NET, onde `blockBlob` é um objeto do tipo [CloudBlockBlob][dotnet_CloudBlockBlob]:

```csharp
await blockBlob.DeleteIfExistsAsync(DeleteSnapshotsOption.IncludeSnapshots, null, null, null);
```

## <a name="snapshots-with-azure-premium-storage"></a>Instantâneos com Armazenamento Premium do Azure
Ao usar instantâneos com o armazenamento Premium, Olá regras a seguir se aplicam:

* Olá o número máximo de instantâneos por blob de página em uma conta de armazenamento premium é 100. Se esse limite for excedido, Olá operação de instantâneo de Blob retornará o código de erro 409 (`SnapshotCountExceeded`).
* Você pode criar um instantâneo de um blob de páginas em uma conta de armazenamento premium uma vez a cada 10 minutos. Se essa taxa for excedida, Olá operação de Blob de instantâneo retornará o código de erro 409 (`SnapshotOperationRateExceeded`).
* tooread um instantâneo, você pode usar o hello copiar Blob operação toocopy um blob de páginas do instantâneo tooanother na conta de saudação. blob de destino Olá Olá operação de cópia não deve ter nenhum instantâneo existente. Se o blob de destino Olá tiver instantâneos, Olá operação Copiar Blob retornará o código de erro 409 (`SnapshotsPresent`).

## <a name="return-hello-absolute-uri-tooa-snapshot"></a>Instantâneo de tooa URI absoluto Olá retorno
Este exemplo de código c# cria um instantâneo e grava Olá URI absoluto para o local primário hello.

```csharp
//Create hello blob service client object.
const string ConnectionString = "DefaultEndpointsProtocol=https;AccountName=account-name;AccountKey=account-key";

CloudStorageAccount storageAccount = CloudStorageAccount.Parse(ConnectionString);
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

//Get a reference tooa container.
CloudBlobContainer container = blobClient.GetContainerReference("sample-container");
container.CreateIfNotExists();

//Get a reference tooa blob.
CloudBlockBlob blob = container.GetBlockBlobReference("sampleblob.txt");
blob.UploadText("This is a blob.");

//Create a snapshot of hello blob and write out its primary URI.
CloudBlockBlob blobSnapshot = blob.CreateSnapshot();
Console.WriteLine(blobSnapshot.SnapshotQualifiedStorageUri.PrimaryUri);
```

## <a name="understand-how-snapshots-accrue-charges"></a>Entender como instantâneos acumulam cobranças
Criando um instantâneo, que é uma cópia somente leitura de um blob, pode resultar na conta de tooyour de encargos de armazenamento de dados adicionais. Ao projetar seu aplicativo, é importante toobe ciente de como essas cobranças podem se acumulam para que você pode minimizar os custos.

### <a name="important-billing-considerations"></a>Considerações importantes sobre cobrança
Olá lista a seguir inclui tooconsider pontos importantes ao criar um instantâneo.

* Sua conta de armazenamento incorre em encargos para blocos exclusivos ou páginas, independentemente de estarem no blob hello ou no instantâneo de saudação. Sua conta não incorrerá em cobranças adicionais para instantâneos associados a um blob até que você atualize o blob Olá no qual eles se baseiam. Depois de atualizar o blob de base hello, ele divergirá dos instantâneos. Quando isso acontece, você é cobrado para blocos exclusivos hello ou páginas em cada blob ou instantâneo.
* Quando você substituir um bloco em um blob de blocos, esse bloco será cobrado subsequentemente como um único bloco. Isso é verdadeiro mesmo se o bloco de saudação tem Olá a mesma ID do bloco e Olá mesmo dados porque ela tem no instantâneo de saudação. Depois de saudação bloco for confirmado novamente, ele divergirá de sua contraparte em qualquer instantâneo e você será cobrado por seus dados. Olá que mesmo é válido para uma página em um blob de página é atualizado com dados idênticos.
* Substituindo um blob de bloco por chamada hello [UploadFromFile][dotnet_UploadFromFile], [UploadText][dotnet_UploadText], [UploadFromStream] [ dotnet_UploadFromStream], ou [UploadFromByteArray] [ dotnet_UploadFromByteArray] método substitui todos os blocos no blob de saudação. Se você tiver um instantâneo associado a esse blob, todos os blocos no blob base hello e instantâneo agora divergem e você será cobrado por todos os blocos de saudação em ambos os blobs. Isso é verdadeiro mesmo se os dados de saudação no blob base hello e instantâneo Olá permanecem idênticos.
* Olá serviço Blob do Azure não tem um toodetermine significa que se dois blocos contêm dados idênticos. Cada bloco que é carregado e confirmado é tratado como exclusivo, mesmo se ele tem Olá mesmo dados e hello mesmo bloco ID. Como cobranças se acumulam para blocos exclusivos, é importante tooconsider que atualizar um blob que tem um instantâneo resulta em blocos exclusivos adicionais e cobranças adicionais.

### <a name="minimize-cost-with-snapshot-management"></a>Minimizar o custo com gerenciamento de instantâneos

É recomendável gerenciar seus instantâneos com cuidado tooavoid encargos adicionais. Você pode seguir estas práticas recomendadas toohelp minimizar Olá custos de armazenamento de saudação de seus instantâneos:

* Exclua e recrie instantâneos associados a um blob sempre que você atualizar o blob hello, mesmo se você estiver atualizando com dados idênticos, a menos que o projeto do seu aplicativo requer que você mantenha instantâneos. Excluindo e recriando em instantâneos do blob Olá, você pode garantir instantâneos e blob Olá não divergem.
* Se você estiver mantendo instantâneos para um blob, evite chamar [UploadFromFile][dotnet_UploadFromFile], [UploadText][dotnet_UploadText], [ UploadFromStream][dotnet_UploadFromStream], ou [UploadFromByteArray] [ dotnet_UploadFromByteArray] tooupdate blob de saudação. Esses métodos substituem todos os blocos de saudação no blob hello, fazendo com que o blob de base e seu instantâneos toodiverge significativamente. Em vez disso, a atualização Olá menor número possível de blocos usando Olá [PutBlock] [ dotnet_PutBlock] e [PutBlockList] [ dotnet_PutBlockList] métodos.

### <a name="snapshot-billing-scenarios"></a>Cenários de cobrança de instantâneo
Olá cenários a seguir demonstram como cobranças se acumulam para um blob de bloco e seus instantâneos.

**Cenário 1**

No cenário 1, blob base Olá não foi atualizada depois Olá instantâneo foi tirado, para que as cobranças incorrem apenas para blocos exclusivos 1, 2 e 3.

![Recursos de Armazenamento do Azure](./media/storage-blob-snapshots/storage-blob-snapshots-billing-scenario-1.png)

**Cenário 2**

No cenário 2, Olá blob de base tiver sido atualizado, mas instantâneo Olá não tem. O bloco 3 foi atualizado e mesmo que ele contém Olá os mesmos dados e Olá a mesma ID, é não Olá igual ao bloco 3 no instantâneo de saudação. Como resultado, a conta de saudação é cobrada por quatro blocos.

![Recursos de Armazenamento do Azure](./media/storage-blob-snapshots/storage-blob-snapshots-billing-scenario-2.png)

**Cenário 3**

No cenário 3, Olá blob de base tiver sido atualizado, mas instantâneo Olá não tem. O bloco 3 foi substituído pelo bloco 4 no blob base hello, mas Olá instantâneo ainda reflete o bloco 3. Como resultado, a conta de saudação é cobrada por quatro blocos.

![Recursos de Armazenamento do Azure](./media/storage-blob-snapshots/storage-blob-snapshots-billing-scenario-3.png)

**Cenário 4**

Cenário 4, blob base Olá foi completamente atualizado e não contém nenhum dos seus blocos originais. Como resultado, a conta de saudação é cobrada por todos os oito blocos exclusivos. Esse cenário pode ocorrer se você estiver usando um método de atualização, como [UploadFromFile][dotnet_UploadFromFile], [UploadText][dotnet_UploadText], [ UploadFromStream][dotnet_UploadFromStream], ou [UploadFromByteArray][dotnet_UploadFromByteArray], pois esses métodos substituem todo o conteúdo de saudação de um blob.

![Recursos de Armazenamento do Azure](./media/storage-blob-snapshots/storage-blob-snapshots-billing-scenario-4.png)

## <a name="next-steps"></a>Próximas etapas

* Você pode encontrar mais informações sobre como trabalhar com instantâneos de disco de VM (máquina virtual) em [Fazer backup dos discos não gerenciados de VM do Azure com instantâneos incrementais](storage-incremental-snapshots.md)

* Para obter exemplos de código adicionais usando o Armazenamento de Blobs, confira [Exemplos de código do Azure](https://azure.microsoft.com/documentation/samples/?service=storage&term=blob). Você pode baixar um aplicativo de exemplo e executá-lo ou procurar Olá código no GitHub.

[dotnet_AccessCondition]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.accesscondition.aspx
[dotnet_CloudBlockBlob]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.cloudblockblob.aspx
[dotnet_CreateSnapshotAsync]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.cloudblockblob.createsnapshotasync.aspx
[dotnet_HTTPStatusCode]: https://msdn.microsoft.com/library/system.net.httpstatuscode(v=vs.110).aspx
[dotnet_PutBlockList]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.cloudblockblob.putblocklist.aspx
[dotnet_PutBlock]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.cloudblockblob.putblock.aspx
[dotnet_UploadFromByteArray]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.cloudblockblob.uploadfrombytearray.aspx
[dotnet_UploadFromFile]: https://msdn.microsoft.com/library/azure/mt705654.aspx
[dotnet_UploadFromStream]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.cloudblockblob.uploadfromstream.aspx
[dotnet_UploadText]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.cloudblockblob.uploadtext.aspx