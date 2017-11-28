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
# <a name="create-a-blob-snapshot"></a><span data-ttu-id="09e53-104">Criar um instantâneo de blob</span><span class="sxs-lookup"><span data-stu-id="09e53-104">Create a blob snapshot</span></span>

<span data-ttu-id="09e53-105">Um instantâneo é uma versão somente leitura de um blob capturada em um momento no tempo.</span><span class="sxs-lookup"><span data-stu-id="09e53-105">A snapshot is a read-only version of a blob that's taken at a point in time.</span></span> <span data-ttu-id="09e53-106">Os instantâneos são úteis para fazer backup de blobs.</span><span class="sxs-lookup"><span data-stu-id="09e53-106">Snapshots are useful for backing up blobs.</span></span> <span data-ttu-id="09e53-107">Depois de criar um instantâneo, você pode lê-lo, copiá-lo ou excluí-lo, mas não é possível modificá-lo.</span><span class="sxs-lookup"><span data-stu-id="09e53-107">After you create a snapshot, you can read, copy, or delete it, but you cannot modify it.</span></span>

<span data-ttu-id="09e53-108">Um instantâneo de um blob é blob de base tooits idênticos, exceto blob Olá URI tem um **DateTime** valor acrescentado hora toohello blob URI tooindicate Olá no qual Olá o instantâneo foi tirado.</span><span class="sxs-lookup"><span data-stu-id="09e53-108">A snapshot of a blob is identical tooits base blob, except that hello blob URI has a **DateTime** value appended toohello blob URI tooindicate hello time at which hello snapshot was taken.</span></span> <span data-ttu-id="09e53-109">Por exemplo, se o URI de blob de uma página é `http://storagesample.core.blob.windows.net/mydrives/myvhd`, Olá instantâneo URI é muito semelhante`http://storagesample.core.blob.windows.net/mydrives/myvhd?snapshot=2011-03-09T01:42:34.9360000Z`.</span><span class="sxs-lookup"><span data-stu-id="09e53-109">For example, if a page blob URI is `http://storagesample.core.blob.windows.net/mydrives/myvhd`, hello snapshot URI is similar too`http://storagesample.core.blob.windows.net/mydrives/myvhd?snapshot=2011-03-09T01:42:34.9360000Z`.</span></span>

> [!NOTE]
> <span data-ttu-id="09e53-110">Todos os instantâneos de compartilham o URI do blob base hello.</span><span class="sxs-lookup"><span data-stu-id="09e53-110">All snapshots share hello base blob's URI.</span></span> <span data-ttu-id="09e53-111">Olá apenas distinção entre o blob de base hello e instantâneo Olá Olá acrescentado **DateTime** valor.</span><span class="sxs-lookup"><span data-stu-id="09e53-111">hello only distinction between hello base blob and hello snapshot is hello appended **DateTime** value.</span></span>
>

<span data-ttu-id="09e53-112">Um blob pode ter qualquer número de instantâneos.</span><span class="sxs-lookup"><span data-stu-id="09e53-112">A blob can have any number of snapshots.</span></span> <span data-ttu-id="09e53-113">Os instantâneos persistem até que sejam explicitamente excluídos.</span><span class="sxs-lookup"><span data-stu-id="09e53-113">Snapshots persist until they are explicitly deleted.</span></span> <span data-ttu-id="09e53-114">Um instantâneo não pode durar mais que seu blob de base.</span><span class="sxs-lookup"><span data-stu-id="09e53-114">A snapshot cannot outlive its base blob.</span></span> <span data-ttu-id="09e53-115">Você pode enumerar instantâneos de saudação associados Olá blob de base tootrack seus instantâneos atuais.</span><span class="sxs-lookup"><span data-stu-id="09e53-115">You can enumerate hello snapshots associated with hello base blob tootrack your current snapshots.</span></span>

<span data-ttu-id="09e53-116">Quando você cria um instantâneo de um blob, Olá propriedades do sistema do blob é copiados toohello instantâneo com hello mesmos valores.</span><span class="sxs-lookup"><span data-stu-id="09e53-116">When you create a snapshot of a blob, hello blob's system properties are copied toohello snapshot with hello same values.</span></span> <span data-ttu-id="09e53-117">metadados do blob base Olá também são copiado toohello de instantâneo, a menos que você especificar metadados separados para Olá instantâneo ao criá-lo.</span><span class="sxs-lookup"><span data-stu-id="09e53-117">hello base blob's metadata is also copied toohello snapshot, unless you specify separate metadata for hello snapshot when you create it.</span></span>

<span data-ttu-id="09e53-118">Quaisquer concessões associados com o blob de base Olá não afetam instantâneo hello.</span><span class="sxs-lookup"><span data-stu-id="09e53-118">Any leases associated with hello base blob do not affect hello snapshot.</span></span> <span data-ttu-id="09e53-119">Não é possível adquirir uma concessão em um instantâneo.</span><span class="sxs-lookup"><span data-stu-id="09e53-119">You cannot acquire a lease on a snapshot.</span></span>

<span data-ttu-id="09e53-120">Um arquivo VHD é usado toostore Olá as informações atuais e o status de um disco VM.</span><span class="sxs-lookup"><span data-stu-id="09e53-120">A VHD file is used toostore hello current information and status for a VM disk.</span></span> <span data-ttu-id="09e53-121">Você pode desanexar um disco de dentro de saudação VM ou desligar Olá VM e, em seguida, tire um instantâneo do seu arquivo VHD.</span><span class="sxs-lookup"><span data-stu-id="09e53-121">You can detach a disk from within hello VM or shut down hello VM, and then take a snapshot of its VHD file.</span></span> <span data-ttu-id="09e53-122">Você pode usar esse arquivo de instantâneo posterior tooretrieve Olá VHD do arquivo no momento e recrie Olá VM.</span><span class="sxs-lookup"><span data-stu-id="09e53-122">You can use that snapshot file later tooretrieve hello VHD file at that point in time and recreate hello VM.</span></span>

<span data-ttu-id="09e53-123">Se a criptografia de serviço de armazenamento (SSE) está habilitada para a conta de armazenamento Olá na qual Olá blob reside, todos os instantâneos de blob serão criptografados em repouso.</span><span class="sxs-lookup"><span data-stu-id="09e53-123">If Storage Service Encryption (SSE) is enabled for hello storage account in which hello blob resides, then any snapshots taken of that blob will be encrypted at rest.</span></span>

## <a name="create-a-snapshot"></a><span data-ttu-id="09e53-124">Criar um instantâneo</span><span class="sxs-lookup"><span data-stu-id="09e53-124">Create a snapshot</span></span>
<span data-ttu-id="09e53-125">Olá exemplo de código a seguir mostra como um instantâneo por meio de toocreate Olá [biblioteca de cliente de armazenamento do Azure para .NET](https://www.nuget.org/packages/WindowsAzure.Storage/).</span><span class="sxs-lookup"><span data-stu-id="09e53-125">hello following code example shows how toocreate a snapshot by using hello [Azure Storage Client Library for .NET](https://www.nuget.org/packages/WindowsAzure.Storage/).</span></span> <span data-ttu-id="09e53-126">Este exemplo especifica os metadados adicionais para instantâneo de saudação quando ele é criado.</span><span class="sxs-lookup"><span data-stu-id="09e53-126">This example specifies additional metadata for hello snapshot when it is created.</span></span>

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

## <a name="copy-snapshots"></a><span data-ttu-id="09e53-127">Copiar instantâneos</span><span class="sxs-lookup"><span data-stu-id="09e53-127">Copy snapshots</span></span>
<span data-ttu-id="09e53-128">As operações de cópia que envolvem blobs e instantâneos seguem estas regras:</span><span class="sxs-lookup"><span data-stu-id="09e53-128">Copy operations involving blobs and snapshots follow these rules:</span></span>

* <span data-ttu-id="09e53-129">Você pode copiar um instantâneo sobre seu blob de base.</span><span class="sxs-lookup"><span data-stu-id="09e53-129">You can copy a snapshot over its base blob.</span></span> <span data-ttu-id="09e53-130">Promovendo uma posição de toohello de instantâneo de blob de base hello, você pode restaurar uma versão anterior de um blob.</span><span class="sxs-lookup"><span data-stu-id="09e53-130">By promoting a snapshot toohello position of hello base blob, you can restore an earlier version of a blob.</span></span> <span data-ttu-id="09e53-131">Olá instantâneo permanece, mas o blob de base de saudação é substituído por uma cópia gravável do instantâneo de saudação.</span><span class="sxs-lookup"><span data-stu-id="09e53-131">hello snapshot remains, but hello base blob is overwritten with a writable copy of hello snapshot.</span></span>
* <span data-ttu-id="09e53-132">Você pode copiar um blob de destino do instantâneo tooa com um nome diferente.</span><span class="sxs-lookup"><span data-stu-id="09e53-132">You can copy a snapshot tooa destination blob with a different name.</span></span> <span data-ttu-id="09e53-133">blob de destino Olá resultante é um blob gravável e não um instantâneo.</span><span class="sxs-lookup"><span data-stu-id="09e53-133">hello resulting destination blob is a writable blob and not a snapshot.</span></span>
* <span data-ttu-id="09e53-134">Quando um blob de origem é copiado, todos os instantâneos de blob de origem Olá não são copiados toohello destino.</span><span class="sxs-lookup"><span data-stu-id="09e53-134">When a source blob is copied, any snapshots of hello source blob are not copied toohello destination.</span></span> <span data-ttu-id="09e53-135">Quando um blob de destino é substituído por uma cópia, todos os instantâneos associados com o blob de destino original Olá permanecem intactos.</span><span class="sxs-lookup"><span data-stu-id="09e53-135">When a destination blob is overwritten with a copy, any snapshots associated with hello original destination blob remain intact.</span></span>
* <span data-ttu-id="09e53-136">Quando você cria um instantâneo de um blob de bloco, lista de blocos confirmados do blob Olá também é copiado toohello instantâneo.</span><span class="sxs-lookup"><span data-stu-id="09e53-136">When you create a snapshot of a block blob, hello blob's committed block list is also copied toohello snapshot.</span></span> <span data-ttu-id="09e53-137">Todos os blocos não confirmados não são copiados.</span><span class="sxs-lookup"><span data-stu-id="09e53-137">Any uncommitted blocks are not copied.</span></span>

## <a name="specify-an-access-condition"></a><span data-ttu-id="09e53-138">Especificar uma condição de acesso</span><span class="sxs-lookup"><span data-stu-id="09e53-138">Specify an access condition</span></span>
<span data-ttu-id="09e53-139">Quando você chama [CreateSnapshotAsync][dotnet_CreateSnapshotAsync], você pode especificar uma condição de acesso para que hello instantâneo é criado somente se uma condição for atendida.</span><span class="sxs-lookup"><span data-stu-id="09e53-139">When you call [CreateSnapshotAsync][dotnet_CreateSnapshotAsync], you can specify an access condition so that hello snapshot is created only if a condition is met.</span></span> <span data-ttu-id="09e53-140">toospecify uma condição de acesso, use Olá [AccessCondition] [ dotnet_AccessCondition] parâmetro.</span><span class="sxs-lookup"><span data-stu-id="09e53-140">toospecify an access condition, use hello [AccessCondition][dotnet_AccessCondition] parameter.</span></span> <span data-ttu-id="09e53-141">Se Olá especificado condição não for atendida, Olá instantâneo não será criado e Olá serviço Blob retornará o código de status [HTTPStatusCode][dotnet_HTTPStatusCode]. PreconditionFailed.</span><span class="sxs-lookup"><span data-stu-id="09e53-141">If hello specified condition is not met, hello snapshot is not created, and hello Blob service returns status code [HTTPStatusCode][dotnet_HTTPStatusCode].PreconditionFailed.</span></span>

## <a name="delete-snapshots"></a><span data-ttu-id="09e53-142">Excluir instantâneos</span><span class="sxs-lookup"><span data-stu-id="09e53-142">Delete snapshots</span></span>
<span data-ttu-id="09e53-143">Você não pode excluir um blob com instantâneos, a menos que os instantâneos de saudação também são excluídos.</span><span class="sxs-lookup"><span data-stu-id="09e53-143">You can't delete a blob with snapshots unless hello snapshots are also deleted.</span></span> <span data-ttu-id="09e53-144">Você pode excluir um instantâneo individualmente ou especificar que todos os instantâneos de ser excluída quando o blob de origem Olá é excluído.</span><span class="sxs-lookup"><span data-stu-id="09e53-144">You can delete a snapshot individually, or specify that all snapshots be deleted when hello source blob is deleted.</span></span> <span data-ttu-id="09e53-145">Se você tentar toodelete um blob que ainda possui instantâneos, ocorrerá um erro.</span><span class="sxs-lookup"><span data-stu-id="09e53-145">If you attempt toodelete a blob that still has snapshots, an error results.</span></span>

<span data-ttu-id="09e53-146">Olá mostra exemplo de código a seguir como toodelete um blob e seus instantâneos no .NET, onde `blockBlob` é um objeto do tipo [CloudBlockBlob][dotnet_CloudBlockBlob]:</span><span class="sxs-lookup"><span data-stu-id="09e53-146">hello following code example shows how toodelete a blob and its snapshots in .NET, where `blockBlob` is an object of type [CloudBlockBlob][dotnet_CloudBlockBlob]:</span></span>

```csharp
await blockBlob.DeleteIfExistsAsync(DeleteSnapshotsOption.IncludeSnapshots, null, null, null);
```

## <a name="snapshots-with-azure-premium-storage"></a><span data-ttu-id="09e53-147">Instantâneos com Armazenamento Premium do Azure</span><span class="sxs-lookup"><span data-stu-id="09e53-147">Snapshots with Azure Premium Storage</span></span>
<span data-ttu-id="09e53-148">Ao usar instantâneos com o armazenamento Premium, Olá regras a seguir se aplicam:</span><span class="sxs-lookup"><span data-stu-id="09e53-148">When using snapshots with Premium Storage, hello following rules apply:</span></span>

* <span data-ttu-id="09e53-149">Olá o número máximo de instantâneos por blob de página em uma conta de armazenamento premium é 100.</span><span class="sxs-lookup"><span data-stu-id="09e53-149">hello maximum number of snapshots per page blob in a premium storage account is 100.</span></span> <span data-ttu-id="09e53-150">Se esse limite for excedido, Olá operação de instantâneo de Blob retornará o código de erro 409 (`SnapshotCountExceeded`).</span><span class="sxs-lookup"><span data-stu-id="09e53-150">If that limit is exceeded, hello Snapshot Blob operation returns error code 409 (`SnapshotCountExceeded`).</span></span>
* <span data-ttu-id="09e53-151">Você pode criar um instantâneo de um blob de páginas em uma conta de armazenamento premium uma vez a cada 10 minutos.</span><span class="sxs-lookup"><span data-stu-id="09e53-151">You can take a snapshot of a page blob in a premium storage account once every 10 minutes.</span></span> <span data-ttu-id="09e53-152">Se essa taxa for excedida, Olá operação de Blob de instantâneo retornará o código de erro 409 (`SnapshotOperationRateExceeded`).</span><span class="sxs-lookup"><span data-stu-id="09e53-152">If that rate is exceeded, hello Snapshot Blob operation returns error code 409 (`SnapshotOperationRateExceeded`).</span></span>
* <span data-ttu-id="09e53-153">tooread um instantâneo, você pode usar o hello copiar Blob operação toocopy um blob de páginas do instantâneo tooanother na conta de saudação.</span><span class="sxs-lookup"><span data-stu-id="09e53-153">tooread a snapshot, you can use hello Copy Blob operation toocopy a snapshot tooanother page blob in hello account.</span></span> <span data-ttu-id="09e53-154">blob de destino Olá Olá operação de cópia não deve ter nenhum instantâneo existente.</span><span class="sxs-lookup"><span data-stu-id="09e53-154">hello destination blob for hello copy operation must not have any existing snapshots.</span></span> <span data-ttu-id="09e53-155">Se o blob de destino Olá tiver instantâneos, Olá operação Copiar Blob retornará o código de erro 409 (`SnapshotsPresent`).</span><span class="sxs-lookup"><span data-stu-id="09e53-155">If hello destination blob does have snapshots, then hello Copy Blob operation returns error code 409 (`SnapshotsPresent`).</span></span>

## <a name="return-hello-absolute-uri-tooa-snapshot"></a><span data-ttu-id="09e53-156">Instantâneo de tooa URI absoluto Olá retorno</span><span class="sxs-lookup"><span data-stu-id="09e53-156">Return hello absolute URI tooa snapshot</span></span>
<span data-ttu-id="09e53-157">Este exemplo de código c# cria um instantâneo e grava Olá URI absoluto para o local primário hello.</span><span class="sxs-lookup"><span data-stu-id="09e53-157">This C# code example creates a snapshot and writes out hello absolute URI for hello primary location.</span></span>

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

## <a name="understand-how-snapshots-accrue-charges"></a><span data-ttu-id="09e53-158">Entender como instantâneos acumulam cobranças</span><span class="sxs-lookup"><span data-stu-id="09e53-158">Understand how snapshots accrue charges</span></span>
<span data-ttu-id="09e53-159">Criando um instantâneo, que é uma cópia somente leitura de um blob, pode resultar na conta de tooyour de encargos de armazenamento de dados adicionais.</span><span class="sxs-lookup"><span data-stu-id="09e53-159">Creating a snapshot, which is a read-only copy of a blob, can result in additional data storage charges tooyour account.</span></span> <span data-ttu-id="09e53-160">Ao projetar seu aplicativo, é importante toobe ciente de como essas cobranças podem se acumulam para que você pode minimizar os custos.</span><span class="sxs-lookup"><span data-stu-id="09e53-160">When designing your application, it is important toobe aware of how these charges might accrue so that you can minimize costs.</span></span>

### <a name="important-billing-considerations"></a><span data-ttu-id="09e53-161">Considerações importantes sobre cobrança</span><span class="sxs-lookup"><span data-stu-id="09e53-161">Important billing considerations</span></span>
<span data-ttu-id="09e53-162">Olá lista a seguir inclui tooconsider pontos importantes ao criar um instantâneo.</span><span class="sxs-lookup"><span data-stu-id="09e53-162">hello following list includes key points tooconsider when creating a snapshot.</span></span>

* <span data-ttu-id="09e53-163">Sua conta de armazenamento incorre em encargos para blocos exclusivos ou páginas, independentemente de estarem no blob hello ou no instantâneo de saudação.</span><span class="sxs-lookup"><span data-stu-id="09e53-163">Your storage account incurs charges for unique blocks or pages, whether they are in hello blob or in hello snapshot.</span></span> <span data-ttu-id="09e53-164">Sua conta não incorrerá em cobranças adicionais para instantâneos associados a um blob até que você atualize o blob Olá no qual eles se baseiam.</span><span class="sxs-lookup"><span data-stu-id="09e53-164">Your account does not incur additional charges for snapshots associated with a blob until you update hello blob on which they are based.</span></span> <span data-ttu-id="09e53-165">Depois de atualizar o blob de base hello, ele divergirá dos instantâneos.</span><span class="sxs-lookup"><span data-stu-id="09e53-165">After you update hello base blob, it diverges from its snapshots.</span></span> <span data-ttu-id="09e53-166">Quando isso acontece, você é cobrado para blocos exclusivos hello ou páginas em cada blob ou instantâneo.</span><span class="sxs-lookup"><span data-stu-id="09e53-166">When this happens, you are charged for hello unique blocks or pages in each blob or snapshot.</span></span>
* <span data-ttu-id="09e53-167">Quando você substituir um bloco em um blob de blocos, esse bloco será cobrado subsequentemente como um único bloco.</span><span class="sxs-lookup"><span data-stu-id="09e53-167">When you replace a block within a block blob, that block is subsequently charged as a unique block.</span></span> <span data-ttu-id="09e53-168">Isso é verdadeiro mesmo se o bloco de saudação tem Olá a mesma ID do bloco e Olá mesmo dados porque ela tem no instantâneo de saudação.</span><span class="sxs-lookup"><span data-stu-id="09e53-168">This is true even if hello block has hello same block ID and hello same data as it has in hello snapshot.</span></span> <span data-ttu-id="09e53-169">Depois de saudação bloco for confirmado novamente, ele divergirá de sua contraparte em qualquer instantâneo e você será cobrado por seus dados.</span><span class="sxs-lookup"><span data-stu-id="09e53-169">After hello block is committed again, it diverges from its counterpart in any snapshot, and you will be charged for its data.</span></span> <span data-ttu-id="09e53-170">Olá que mesmo é válido para uma página em um blob de página é atualizado com dados idênticos.</span><span class="sxs-lookup"><span data-stu-id="09e53-170">hello same holds true for a page in a page blob that's updated with identical data.</span></span>
* <span data-ttu-id="09e53-171">Substituindo um blob de bloco por chamada hello [UploadFromFile][dotnet_UploadFromFile], [UploadText][dotnet_UploadText], [UploadFromStream] [ dotnet_UploadFromStream], ou [UploadFromByteArray] [ dotnet_UploadFromByteArray] método substitui todos os blocos no blob de saudação.</span><span class="sxs-lookup"><span data-stu-id="09e53-171">Replacing a block blob by calling hello [UploadFromFile][dotnet_UploadFromFile], [UploadText][dotnet_UploadText], [UploadFromStream][dotnet_UploadFromStream], or [UploadFromByteArray][dotnet_UploadFromByteArray] method replaces all blocks in hello blob.</span></span> <span data-ttu-id="09e53-172">Se você tiver um instantâneo associado a esse blob, todos os blocos no blob base hello e instantâneo agora divergem e você será cobrado por todos os blocos de saudação em ambos os blobs.</span><span class="sxs-lookup"><span data-stu-id="09e53-172">If you have a snapshot associated with that blob, all blocks in hello base blob and snapshot now diverge, and you will be charged for all hello blocks in both blobs.</span></span> <span data-ttu-id="09e53-173">Isso é verdadeiro mesmo se os dados de saudação no blob base hello e instantâneo Olá permanecem idênticos.</span><span class="sxs-lookup"><span data-stu-id="09e53-173">This is true even if hello data in hello base blob and hello snapshot remain identical.</span></span>
* <span data-ttu-id="09e53-174">Olá serviço Blob do Azure não tem um toodetermine significa que se dois blocos contêm dados idênticos.</span><span class="sxs-lookup"><span data-stu-id="09e53-174">hello Azure Blob service does not have a means toodetermine whether two blocks contain identical data.</span></span> <span data-ttu-id="09e53-175">Cada bloco que é carregado e confirmado é tratado como exclusivo, mesmo se ele tem Olá mesmo dados e hello mesmo bloco ID.</span><span class="sxs-lookup"><span data-stu-id="09e53-175">Each block that is uploaded and committed is treated as unique, even if it has hello same data and hello same block ID.</span></span> <span data-ttu-id="09e53-176">Como cobranças se acumulam para blocos exclusivos, é importante tooconsider que atualizar um blob que tem um instantâneo resulta em blocos exclusivos adicionais e cobranças adicionais.</span><span class="sxs-lookup"><span data-stu-id="09e53-176">Because charges accrue for unique blocks, it's important tooconsider that updating a blob that has a snapshot results in additional unique blocks and additional charges.</span></span>

### <a name="minimize-cost-with-snapshot-management"></a><span data-ttu-id="09e53-177">Minimizar o custo com gerenciamento de instantâneos</span><span class="sxs-lookup"><span data-stu-id="09e53-177">Minimize cost with snapshot management</span></span>

<span data-ttu-id="09e53-178">É recomendável gerenciar seus instantâneos com cuidado tooavoid encargos adicionais.</span><span class="sxs-lookup"><span data-stu-id="09e53-178">We recommend managing your snapshots carefully tooavoid extra charges.</span></span> <span data-ttu-id="09e53-179">Você pode seguir estas práticas recomendadas toohelp minimizar Olá custos de armazenamento de saudação de seus instantâneos:</span><span class="sxs-lookup"><span data-stu-id="09e53-179">You can follow these best practices toohelp minimize hello costs incurred by hello storage of your snapshots:</span></span>

* <span data-ttu-id="09e53-180">Exclua e recrie instantâneos associados a um blob sempre que você atualizar o blob hello, mesmo se você estiver atualizando com dados idênticos, a menos que o projeto do seu aplicativo requer que você mantenha instantâneos.</span><span class="sxs-lookup"><span data-stu-id="09e53-180">Delete and re-create snapshots associated with a blob whenever you update hello blob, even if you are updating with identical data, unless your application design requires that you maintain snapshots.</span></span> <span data-ttu-id="09e53-181">Excluindo e recriando em instantâneos do blob Olá, você pode garantir instantâneos e blob Olá não divergem.</span><span class="sxs-lookup"><span data-stu-id="09e53-181">By deleting and re-creating hello blob's snapshots, you can ensure that hello blob and snapshots do not diverge.</span></span>
* <span data-ttu-id="09e53-182">Se você estiver mantendo instantâneos para um blob, evite chamar [UploadFromFile][dotnet_UploadFromFile], [UploadText][dotnet_UploadText], [ UploadFromStream][dotnet_UploadFromStream], ou [UploadFromByteArray] [ dotnet_UploadFromByteArray] tooupdate blob de saudação.</span><span class="sxs-lookup"><span data-stu-id="09e53-182">If you are maintaining snapshots for a blob, avoid calling [UploadFromFile][dotnet_UploadFromFile], [UploadText][dotnet_UploadText], [UploadFromStream][dotnet_UploadFromStream], or [UploadFromByteArray][dotnet_UploadFromByteArray] tooupdate hello blob.</span></span> <span data-ttu-id="09e53-183">Esses métodos substituem todos os blocos de saudação no blob hello, fazendo com que o blob de base e seu instantâneos toodiverge significativamente.</span><span class="sxs-lookup"><span data-stu-id="09e53-183">These methods replace all of hello blocks in hello blob, causing your base blob and its snapshots toodiverge significantly.</span></span> <span data-ttu-id="09e53-184">Em vez disso, a atualização Olá menor número possível de blocos usando Olá [PutBlock] [ dotnet_PutBlock] e [PutBlockList] [ dotnet_PutBlockList] métodos.</span><span class="sxs-lookup"><span data-stu-id="09e53-184">Instead, update hello fewest possible number of blocks by using hello [PutBlock][dotnet_PutBlock] and [PutBlockList][dotnet_PutBlockList] methods.</span></span>

### <a name="snapshot-billing-scenarios"></a><span data-ttu-id="09e53-185">Cenários de cobrança de instantâneo</span><span class="sxs-lookup"><span data-stu-id="09e53-185">Snapshot billing scenarios</span></span>
<span data-ttu-id="09e53-186">Olá cenários a seguir demonstram como cobranças se acumulam para um blob de bloco e seus instantâneos.</span><span class="sxs-lookup"><span data-stu-id="09e53-186">hello following scenarios demonstrate how charges accrue for a block blob and its snapshots.</span></span>

<span data-ttu-id="09e53-187">**Cenário 1**</span><span class="sxs-lookup"><span data-stu-id="09e53-187">**Scenario 1**</span></span>

<span data-ttu-id="09e53-188">No cenário 1, blob base Olá não foi atualizada depois Olá instantâneo foi tirado, para que as cobranças incorrem apenas para blocos exclusivos 1, 2 e 3.</span><span class="sxs-lookup"><span data-stu-id="09e53-188">In scenario 1, hello base blob has not been updated after hello snapshot was taken, so charges are incurred only for unique blocks 1, 2, and 3.</span></span>

![Recursos de Armazenamento do Azure](./media/storage-blob-snapshots/storage-blob-snapshots-billing-scenario-1.png)

<span data-ttu-id="09e53-190">**Cenário 2**</span><span class="sxs-lookup"><span data-stu-id="09e53-190">**Scenario 2**</span></span>

<span data-ttu-id="09e53-191">No cenário 2, Olá blob de base tiver sido atualizado, mas instantâneo Olá não tem.</span><span class="sxs-lookup"><span data-stu-id="09e53-191">In scenario 2, hello base blob has been updated, but hello snapshot has not.</span></span> <span data-ttu-id="09e53-192">O bloco 3 foi atualizado e mesmo que ele contém Olá os mesmos dados e Olá a mesma ID, é não Olá igual ao bloco 3 no instantâneo de saudação.</span><span class="sxs-lookup"><span data-stu-id="09e53-192">Block 3 was updated, and even though it contains hello same data and hello same ID, it is not hello same as block 3 in hello snapshot.</span></span> <span data-ttu-id="09e53-193">Como resultado, a conta de saudação é cobrada por quatro blocos.</span><span class="sxs-lookup"><span data-stu-id="09e53-193">As a result, hello account is charged for four blocks.</span></span>

![Recursos de Armazenamento do Azure](./media/storage-blob-snapshots/storage-blob-snapshots-billing-scenario-2.png)

<span data-ttu-id="09e53-195">**Cenário 3**</span><span class="sxs-lookup"><span data-stu-id="09e53-195">**Scenario 3**</span></span>

<span data-ttu-id="09e53-196">No cenário 3, Olá blob de base tiver sido atualizado, mas instantâneo Olá não tem.</span><span class="sxs-lookup"><span data-stu-id="09e53-196">In scenario 3, hello base blob has been updated, but hello snapshot has not.</span></span> <span data-ttu-id="09e53-197">O bloco 3 foi substituído pelo bloco 4 no blob base hello, mas Olá instantâneo ainda reflete o bloco 3.</span><span class="sxs-lookup"><span data-stu-id="09e53-197">Block 3 was replaced with block 4 in hello base blob, but hello snapshot still reflects block 3.</span></span> <span data-ttu-id="09e53-198">Como resultado, a conta de saudação é cobrada por quatro blocos.</span><span class="sxs-lookup"><span data-stu-id="09e53-198">As a result, hello account is charged for four blocks.</span></span>

![Recursos de Armazenamento do Azure](./media/storage-blob-snapshots/storage-blob-snapshots-billing-scenario-3.png)

<span data-ttu-id="09e53-200">**Cenário 4**</span><span class="sxs-lookup"><span data-stu-id="09e53-200">**Scenario 4**</span></span>

<span data-ttu-id="09e53-201">Cenário 4, blob base Olá foi completamente atualizado e não contém nenhum dos seus blocos originais.</span><span class="sxs-lookup"><span data-stu-id="09e53-201">In scenario 4, hello base blob has been completely updated and contains none of its original blocks.</span></span> <span data-ttu-id="09e53-202">Como resultado, a conta de saudação é cobrada por todos os oito blocos exclusivos.</span><span class="sxs-lookup"><span data-stu-id="09e53-202">As a result, hello account is charged for all eight unique blocks.</span></span> <span data-ttu-id="09e53-203">Esse cenário pode ocorrer se você estiver usando um método de atualização, como [UploadFromFile][dotnet_UploadFromFile], [UploadText][dotnet_UploadText], [ UploadFromStream][dotnet_UploadFromStream], ou [UploadFromByteArray][dotnet_UploadFromByteArray], pois esses métodos substituem todo o conteúdo de saudação de um blob.</span><span class="sxs-lookup"><span data-stu-id="09e53-203">This scenario can occur if you are using an update method such as [UploadFromFile][dotnet_UploadFromFile], [UploadText][dotnet_UploadText], [UploadFromStream][dotnet_UploadFromStream], or [UploadFromByteArray][dotnet_UploadFromByteArray], because these methods replace all of hello contents of a blob.</span></span>

![Recursos de Armazenamento do Azure](./media/storage-blob-snapshots/storage-blob-snapshots-billing-scenario-4.png)

## <a name="next-steps"></a><span data-ttu-id="09e53-205">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="09e53-205">Next steps</span></span>

* <span data-ttu-id="09e53-206">Você pode encontrar mais informações sobre como trabalhar com instantâneos de disco de VM (máquina virtual) em [Fazer backup dos discos não gerenciados de VM do Azure com instantâneos incrementais](storage-incremental-snapshots.md)</span><span class="sxs-lookup"><span data-stu-id="09e53-206">You can find more information about working with virtual machine (VM) disk snapshots in [Back up Azure unmanaged VM disks with incremental snapshots](storage-incremental-snapshots.md)</span></span>

* <span data-ttu-id="09e53-207">Para obter exemplos de código adicionais usando o Armazenamento de Blobs, confira [Exemplos de código do Azure](https://azure.microsoft.com/documentation/samples/?service=storage&term=blob).</span><span class="sxs-lookup"><span data-stu-id="09e53-207">For additional code examples using Blob storage, see [Azure Code Samples](https://azure.microsoft.com/documentation/samples/?service=storage&term=blob).</span></span> <span data-ttu-id="09e53-208">Você pode baixar um aplicativo de exemplo e executá-lo ou procurar Olá código no GitHub.</span><span class="sxs-lookup"><span data-stu-id="09e53-208">You can download a sample application and run it, or browse hello code on GitHub.</span></span>

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