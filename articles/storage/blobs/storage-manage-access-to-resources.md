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
# <a name="manage-anonymous-read-access-toocontainers-and-blobs"></a><span data-ttu-id="224b1-103">Gerenciar blobs e acesso de leitura anônimo toocontainers</span><span class="sxs-lookup"><span data-stu-id="224b1-103">Manage anonymous read access toocontainers and blobs</span></span>
<span data-ttu-id="224b1-104">Você pode habilitar o acesso de leitura anônimo, public tooa contêiner e seus blobs no armazenamento de BLOBs do Azure.</span><span class="sxs-lookup"><span data-stu-id="224b1-104">You can enable anonymous, public read access tooa container and its blobs in Azure Blob storage.</span></span> <span data-ttu-id="224b1-105">Fazendo isso, você pode conceder recursos do acesso somente leitura toothese sem compartilhar sua chave de conta e sem a necessidade de uma assinatura de acesso compartilhado (SAS).</span><span class="sxs-lookup"><span data-stu-id="224b1-105">By doing so, you can grant read-only access toothese resources without sharing your account key, and without requiring a shared access signature (SAS).</span></span>

<span data-ttu-id="224b1-106">Acesso de leitura público é melhor para cenários onde você deseja que determinados blobs tooalways esteja disponível para acesso de leitura anônimo.</span><span class="sxs-lookup"><span data-stu-id="224b1-106">Public read access is best for scenarios where you want certain blobs tooalways be available for anonymous read access.</span></span> <span data-ttu-id="224b1-107">Para ter um controle mais refinado, você pode criar uma assinatura de acesso compartilhado.</span><span class="sxs-lookup"><span data-stu-id="224b1-107">For more fine-grained control, you can create a shared access signature.</span></span> <span data-ttu-id="224b1-108">Assinaturas de acesso compartilhado permitem acesso de tooprovide restringido usando permissões diferentes, por um período de tempo específico.</span><span class="sxs-lookup"><span data-stu-id="224b1-108">Shared access signatures enable you tooprovide restricted access using different permissions, for a specific time period.</span></span> <span data-ttu-id="224b1-109">Para saber mais sobre como criar assinaturas de acesso compartilhado, veja [Usando SAS (Assinaturas de Acesso Compartilhado) no Armazenamento do Azure](../common/storage-dotnet-shared-access-signature-part-1.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="224b1-109">For more information about creating shared access signatures, see [Using shared access signatures (SAS) in Azure Storage](../common/storage-dotnet-shared-access-signature-part-1.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json).</span></span>

## <a name="grant-anonymous-users-permissions-toocontainers-and-blobs"></a><span data-ttu-id="224b1-110">Conceder a usuários anônimos permissões toocontainers e blobs</span><span class="sxs-lookup"><span data-stu-id="224b1-110">Grant anonymous users permissions toocontainers and blobs</span></span>
<span data-ttu-id="224b1-111">Por padrão, um contêiner e todos os blobs dentro dele podem ser acessados somente pelo proprietário Olá Olá da conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="224b1-111">By default, a container and any blobs within it may be accessed only by hello owner of hello storage account.</span></span> <span data-ttu-id="224b1-112">contêiner de tooa toogive usuários anônimos permissões de leitura e seus blobs, você pode definir o acesso público do hello contêiner permissões tooallow.</span><span class="sxs-lookup"><span data-stu-id="224b1-112">toogive anonymous users read permissions tooa container and its blobs, you can set hello container permissions tooallow public access.</span></span> <span data-ttu-id="224b1-113">Usuários anônimos podem ler blobs dentro de um contêiner publicamente acessível sem autenticar a solicitação de saudação.</span><span class="sxs-lookup"><span data-stu-id="224b1-113">Anonymous users can read blobs within a publicly accessible container without authenticating hello request.</span></span>

<span data-ttu-id="224b1-114">Você pode configurar um contêiner com hello as seguintes permissões:</span><span class="sxs-lookup"><span data-stu-id="224b1-114">You can configure a container with hello following permissions:</span></span>

* <span data-ttu-id="224b1-115">**Acesso de leitura não público:** Olá contêiner e seus blobs podem ser acessados somente pelo proprietário da conta de armazenamento hello.</span><span class="sxs-lookup"><span data-stu-id="224b1-115">**No public read access:** hello container and its blobs can be accessed only by hello storage account owner.</span></span> <span data-ttu-id="224b1-116">Esse é o padrão de Olá para todos os novos contêineres.</span><span class="sxs-lookup"><span data-stu-id="224b1-116">This is hello default for all new containers.</span></span>
* <span data-ttu-id="224b1-117">**Acesso para blobs somente de leitura público:** Blobs no contêiner Olá podem ser lidos por solicitação anônima, mas os dados do contêiner não estão disponíveis.</span><span class="sxs-lookup"><span data-stu-id="224b1-117">**Public read access for blobs only:** Blobs within hello container can be read by anonymous request, but container data is not available.</span></span> <span data-ttu-id="224b1-118">Clientes anônimos não é possível enumerar blobs hello dentro do contêiner de saudação.</span><span class="sxs-lookup"><span data-stu-id="224b1-118">Anonymous clients cannot enumerate hello blobs within hello container.</span></span>
* <span data-ttu-id="224b1-119">**Acesso de leitura público completo:** todos os dados de contêiner e blob podem ser lidos por solicitação anônima.</span><span class="sxs-lookup"><span data-stu-id="224b1-119">**Full public read access:** All container and blob data can be read by anonymous request.</span></span> <span data-ttu-id="224b1-120">Os clientes podem enumerar blobs no contêiner de saudação por solicitação anônima, mas não é possível enumerar os contêineres na conta de armazenamento hello.</span><span class="sxs-lookup"><span data-stu-id="224b1-120">Clients can enumerate blobs within hello container by anonymous request, but cannot enumerate containers within hello storage account.</span></span>

<span data-ttu-id="224b1-121">Você pode usar as seguintes permissões de contêiner de tooset de saudação:</span><span class="sxs-lookup"><span data-stu-id="224b1-121">You can use hello following tooset container permissions:</span></span>

* [<span data-ttu-id="224b1-122">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="224b1-122">Azure portal</span></span>](https://portal.azure.com)
* [<span data-ttu-id="224b1-123">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="224b1-123">Azure PowerShell</span></span>](../common/storage-powershell-guide-full.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json#how-to-manage-azure-blobs)
* [<span data-ttu-id="224b1-124">CLI 2.0 do Azure</span><span class="sxs-lookup"><span data-stu-id="224b1-124">Azure CLI 2.0</span></span>](../common/storage-azure-cli.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json#create-and-manage-blobs)
* <span data-ttu-id="224b1-125">Programaticamente, usando uma das bibliotecas de cliente de armazenamento hello ou hello API REST</span><span class="sxs-lookup"><span data-stu-id="224b1-125">Programmatically, by using one of hello storage client libraries or hello REST API</span></span>

### <a name="set-container-permissions-in-hello-azure-portal"></a><span data-ttu-id="224b1-126">Definir permissões de contêiner de saudação portal do Azure</span><span class="sxs-lookup"><span data-stu-id="224b1-126">Set container permissions in hello Azure portal</span></span>
<span data-ttu-id="224b1-127">permissões do contêiner tooset no hello [portal do Azure](https://portal.azure.com), siga estas etapas:</span><span class="sxs-lookup"><span data-stu-id="224b1-127">tooset container permissions in hello [Azure portal](https://portal.azure.com), follow these steps:</span></span>

1. <span data-ttu-id="224b1-128">Abra o **conta de armazenamento** folha no portal de saudação.</span><span class="sxs-lookup"><span data-stu-id="224b1-128">Open your **Storage account** blade in hello portal.</span></span> <span data-ttu-id="224b1-129">Você pode encontrar sua conta de armazenamento selecionando **contas de armazenamento** na folha do menu principal do portal de saudação.</span><span class="sxs-lookup"><span data-stu-id="224b1-129">You can find your storage account by selecting **Storage accounts** in hello main portal menu blade.</span></span>
1. <span data-ttu-id="224b1-130">Em **serviço BLOB** na folha de menu hello, selecione **contêineres**.</span><span class="sxs-lookup"><span data-stu-id="224b1-130">Under **BLOB SERVICE** on hello menu blade, select **Containers**.</span></span>
1. <span data-ttu-id="224b1-131">Clique na linha do contêiner de saudação ou do contêiner do hello selecione reticências tooopen Olá **menu de contexto**.</span><span class="sxs-lookup"><span data-stu-id="224b1-131">Right-click on hello container row or select hello ellipsis tooopen hello container's **Context menu**.</span></span>
1. <span data-ttu-id="224b1-132">Selecione **política de acesso** no menu de contexto de saudação.</span><span class="sxs-lookup"><span data-stu-id="224b1-132">Select **Access policy** in hello context menu.</span></span>
1. <span data-ttu-id="224b1-133">Selecione um **tipo de acesso** de saudação menu suspenso.</span><span class="sxs-lookup"><span data-stu-id="224b1-133">Select an **Access type** from hello drop down menu.</span></span>

    ![Caixa de diálogo Editar Metadados do Contêiner](./media/storage-manage-access-to-resources/storage-manage-access-to-resources-0.png)

### <a name="set-container-permissions-with-net"></a><span data-ttu-id="224b1-135">Definir permissões de contêiner com .NET</span><span class="sxs-lookup"><span data-stu-id="224b1-135">Set container permissions with .NET</span></span>
<span data-ttu-id="224b1-136">tooset permissões para um contêiner usando o c# e hello biblioteca de cliente de armazenamento para .NET, recuperar as permissões existentes do contêiner Olá por chamada hello **GetPermissions** método.</span><span class="sxs-lookup"><span data-stu-id="224b1-136">tooset permissions for a container using C# and hello Storage Client Library for .NET, first retrieve hello container's existing permissions by calling hello **GetPermissions** method.</span></span> <span data-ttu-id="224b1-137">Saudação de conjunto, em seguida, **PublicAccess** propriedade Olá **BlobContainerPermissions** objeto que é retornado pelo Olá **GetPermissions** método.</span><span class="sxs-lookup"><span data-stu-id="224b1-137">Then set hello **PublicAccess** property for hello **BlobContainerPermissions** object that is returned by hello **GetPermissions** method.</span></span> <span data-ttu-id="224b1-138">Finalmente, chame Olá **SetPermissions** método com hello atualizado permissões.</span><span class="sxs-lookup"><span data-stu-id="224b1-138">Finally, call hello **SetPermissions** method with hello updated permissions.</span></span>

<span data-ttu-id="224b1-139">saudação de exemplo a seguir define permissões do contêiner Olá toofull acesso de leitura público.</span><span class="sxs-lookup"><span data-stu-id="224b1-139">hello following example sets hello container's permissions toofull public read access.</span></span> <span data-ttu-id="224b1-140">tooset permissões toopublic acesso de leitura para blobs, defina Olá **PublicAccess** propriedade muito**BlobContainerPublicAccessType.Blob**.</span><span class="sxs-lookup"><span data-stu-id="224b1-140">tooset permissions toopublic read access for blobs only, set hello **PublicAccess** property too**BlobContainerPublicAccessType.Blob**.</span></span> <span data-ttu-id="224b1-141">conjunto de todas as permissões para usuários anônimos, tooremove Olá propriedade muito**BlobContainerPublicAccessType.Off**.</span><span class="sxs-lookup"><span data-stu-id="224b1-141">tooremove all permissions for anonymous users, set hello property too**BlobContainerPublicAccessType.Off**.</span></span>

```csharp
public static void SetPublicContainerPermissions(CloudBlobContainer container)
{
    BlobContainerPermissions permissions = container.GetPermissions();
    permissions.PublicAccess = BlobContainerPublicAccessType.Container;
    container.SetPermissions(permissions);
}
```

## <a name="access-containers-and-blobs-anonymously"></a><span data-ttu-id="224b1-142">Acessar contêineres e blobs anonimamente</span><span class="sxs-lookup"><span data-stu-id="224b1-142">Access containers and blobs anonymously</span></span>
<span data-ttu-id="224b1-143">Um cliente que acessa contêineres e blobs anonimamente pode usar construtores que não necessitam de credenciais.</span><span class="sxs-lookup"><span data-stu-id="224b1-143">A client that accesses containers and blobs anonymously can use constructors that do not require credentials.</span></span> <span data-ttu-id="224b1-144">Olá exemplos a seguir mostra algumas maneiras diferentes de recursos do serviço Blob tooreference anonimamente.</span><span class="sxs-lookup"><span data-stu-id="224b1-144">hello following examples show a few different ways tooreference Blob service resources anonymously.</span></span>

### <a name="create-an-anonymous-client-object"></a><span data-ttu-id="224b1-145">Criar um objeto de cliente anônimo</span><span class="sxs-lookup"><span data-stu-id="224b1-145">Create an anonymous client object</span></span>
<span data-ttu-id="224b1-146">Você pode criar um novo objeto de cliente de serviço para acesso anônimo, fornecendo o ponto de extremidade de serviço de Blob Olá para conta de saudação.</span><span class="sxs-lookup"><span data-stu-id="224b1-146">You can create a new service client object for anonymous access by providing hello Blob service endpoint for hello account.</span></span> <span data-ttu-id="224b1-147">No entanto, você também deve saber o nome de saudação de um contêiner nessa conta que está disponível para acesso anônimo.</span><span class="sxs-lookup"><span data-stu-id="224b1-147">However, you must also know hello name of a container in that account that's available for anonymous access.</span></span>

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

### <a name="reference-a-container-anonymously"></a><span data-ttu-id="224b1-148">Fazer referência a um contêiner anonimamente</span><span class="sxs-lookup"><span data-stu-id="224b1-148">Reference a container anonymously</span></span>
<span data-ttu-id="224b1-149">Se você tiver Olá URL tooa contêiner anonimamente disponível, você pode usá-lo contêiner de saudação tooreference diretamente.</span><span class="sxs-lookup"><span data-stu-id="224b1-149">If you have hello URL tooa container that is anonymously available, you can use it tooreference hello container directly.</span></span>

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

### <a name="reference-a-blob-anonymously"></a><span data-ttu-id="224b1-150">Fazer referência a um blob anonimamente</span><span class="sxs-lookup"><span data-stu-id="224b1-150">Reference a blob anonymously</span></span>
<span data-ttu-id="224b1-151">Se você tiver um blob Olá de tooa de URL que está disponível para acesso anônimo, você pode referenciar blob Olá diretamente usando essa URL:</span><span class="sxs-lookup"><span data-stu-id="224b1-151">If you have hello URL tooa blob that is available for anonymous access, you can reference hello blob directly using that URL:</span></span>

```csharp
public static void DownloadBlobAnonymously()
{
    CloudBlockBlob blob = new CloudBlockBlob(new Uri(@"https://storagesample.blob.core.windows.net/sample-container/logfile.txt"));
    blob.DownloadToFile(@"C:\Temp\logfile.txt", System.IO.FileMode.Create);
}
```

## <a name="features-available-tooanonymous-users"></a><span data-ttu-id="224b1-152">Recursos que os usuários tooanonymous disponíveis</span><span class="sxs-lookup"><span data-stu-id="224b1-152">Features available tooanonymous users</span></span>
<span data-ttu-id="224b1-153">Olá, a tabela a seguir mostra quais operações podem ser chamadas por usuários anônimos quando a ACL do contêiner é definir o acesso público de tooallow.</span><span class="sxs-lookup"><span data-stu-id="224b1-153">hello following table shows which operations may be called by anonymous users when a container's ACL is set tooallow public access.</span></span>

| <span data-ttu-id="224b1-154">Operação REST</span><span class="sxs-lookup"><span data-stu-id="224b1-154">REST Operation</span></span> | <span data-ttu-id="224b1-155">Permissão com acesso de leitura público completo</span><span class="sxs-lookup"><span data-stu-id="224b1-155">Permission with full public read access</span></span> | <span data-ttu-id="224b1-156">Permissão de acesso de leitura público apenas para blobs</span><span class="sxs-lookup"><span data-stu-id="224b1-156">Permission with public read access for blobs only</span></span> |
| --- | --- | --- |
| <span data-ttu-id="224b1-157">Listar contêineres</span><span class="sxs-lookup"><span data-stu-id="224b1-157">List Containers</span></span> |<span data-ttu-id="224b1-158">Somente proprietário</span><span class="sxs-lookup"><span data-stu-id="224b1-158">Owner only</span></span> |<span data-ttu-id="224b1-159">Somente proprietário</span><span class="sxs-lookup"><span data-stu-id="224b1-159">Owner only</span></span> |
| <span data-ttu-id="224b1-160">Create Container</span><span class="sxs-lookup"><span data-stu-id="224b1-160">Create Container</span></span> |<span data-ttu-id="224b1-161">Somente proprietário</span><span class="sxs-lookup"><span data-stu-id="224b1-161">Owner only</span></span> |<span data-ttu-id="224b1-162">Somente proprietário</span><span class="sxs-lookup"><span data-stu-id="224b1-162">Owner only</span></span> |
| <span data-ttu-id="224b1-163">Get Container Properties</span><span class="sxs-lookup"><span data-stu-id="224b1-163">Get Container Properties</span></span> |<span data-ttu-id="224b1-164">Todos</span><span class="sxs-lookup"><span data-stu-id="224b1-164">All</span></span> |<span data-ttu-id="224b1-165">Somente proprietário</span><span class="sxs-lookup"><span data-stu-id="224b1-165">Owner only</span></span> |
| <span data-ttu-id="224b1-166">Get Container Metadata</span><span class="sxs-lookup"><span data-stu-id="224b1-166">Get Container Metadata</span></span> |<span data-ttu-id="224b1-167">Todos</span><span class="sxs-lookup"><span data-stu-id="224b1-167">All</span></span> |<span data-ttu-id="224b1-168">Somente proprietário</span><span class="sxs-lookup"><span data-stu-id="224b1-168">Owner only</span></span> |
| <span data-ttu-id="224b1-169">Set Container Metadata</span><span class="sxs-lookup"><span data-stu-id="224b1-169">Set Container Metadata</span></span> |<span data-ttu-id="224b1-170">Somente proprietário</span><span class="sxs-lookup"><span data-stu-id="224b1-170">Owner only</span></span> |<span data-ttu-id="224b1-171">Somente proprietário</span><span class="sxs-lookup"><span data-stu-id="224b1-171">Owner only</span></span> |
| <span data-ttu-id="224b1-172">Get Container ACL</span><span class="sxs-lookup"><span data-stu-id="224b1-172">Get Container ACL</span></span> |<span data-ttu-id="224b1-173">Somente proprietário</span><span class="sxs-lookup"><span data-stu-id="224b1-173">Owner only</span></span> |<span data-ttu-id="224b1-174">Somente proprietário</span><span class="sxs-lookup"><span data-stu-id="224b1-174">Owner only</span></span> |
| <span data-ttu-id="224b1-175">Set Container ACL</span><span class="sxs-lookup"><span data-stu-id="224b1-175">Set Container ACL</span></span> |<span data-ttu-id="224b1-176">Somente proprietário</span><span class="sxs-lookup"><span data-stu-id="224b1-176">Owner only</span></span> |<span data-ttu-id="224b1-177">Somente proprietário</span><span class="sxs-lookup"><span data-stu-id="224b1-177">Owner only</span></span> |
| <span data-ttu-id="224b1-178">Delete Container</span><span class="sxs-lookup"><span data-stu-id="224b1-178">Delete Container</span></span> |<span data-ttu-id="224b1-179">Somente proprietário</span><span class="sxs-lookup"><span data-stu-id="224b1-179">Owner only</span></span> |<span data-ttu-id="224b1-180">Somente proprietário</span><span class="sxs-lookup"><span data-stu-id="224b1-180">Owner only</span></span> |
| <span data-ttu-id="224b1-181">Listar Blobs</span><span class="sxs-lookup"><span data-stu-id="224b1-181">List Blobs</span></span> |<span data-ttu-id="224b1-182">Todos</span><span class="sxs-lookup"><span data-stu-id="224b1-182">All</span></span> |<span data-ttu-id="224b1-183">Somente proprietário</span><span class="sxs-lookup"><span data-stu-id="224b1-183">Owner only</span></span> |
| <span data-ttu-id="224b1-184">Put Blob</span><span class="sxs-lookup"><span data-stu-id="224b1-184">Put Blob</span></span> |<span data-ttu-id="224b1-185">Somente proprietário</span><span class="sxs-lookup"><span data-stu-id="224b1-185">Owner only</span></span> |<span data-ttu-id="224b1-186">Somente proprietário</span><span class="sxs-lookup"><span data-stu-id="224b1-186">Owner only</span></span> |
| <span data-ttu-id="224b1-187">Get Blob</span><span class="sxs-lookup"><span data-stu-id="224b1-187">Get Blob</span></span> |<span data-ttu-id="224b1-188">Todos</span><span class="sxs-lookup"><span data-stu-id="224b1-188">All</span></span> |<span data-ttu-id="224b1-189">Todos</span><span class="sxs-lookup"><span data-stu-id="224b1-189">All</span></span> |
| <span data-ttu-id="224b1-190">Get Blob Properties</span><span class="sxs-lookup"><span data-stu-id="224b1-190">Get Blob Properties</span></span> |<span data-ttu-id="224b1-191">Todos</span><span class="sxs-lookup"><span data-stu-id="224b1-191">All</span></span> |<span data-ttu-id="224b1-192">Todos</span><span class="sxs-lookup"><span data-stu-id="224b1-192">All</span></span> |
| <span data-ttu-id="224b1-193">Set Blob Properties</span><span class="sxs-lookup"><span data-stu-id="224b1-193">Set Blob Properties</span></span> |<span data-ttu-id="224b1-194">Somente proprietário</span><span class="sxs-lookup"><span data-stu-id="224b1-194">Owner only</span></span> |<span data-ttu-id="224b1-195">Somente proprietário</span><span class="sxs-lookup"><span data-stu-id="224b1-195">Owner only</span></span> |
| <span data-ttu-id="224b1-196">Get Blob Metadata</span><span class="sxs-lookup"><span data-stu-id="224b1-196">Get Blob Metadata</span></span> |<span data-ttu-id="224b1-197">Todos</span><span class="sxs-lookup"><span data-stu-id="224b1-197">All</span></span> |<span data-ttu-id="224b1-198">Todos</span><span class="sxs-lookup"><span data-stu-id="224b1-198">All</span></span> |
| <span data-ttu-id="224b1-199">Set Blob Metadata</span><span class="sxs-lookup"><span data-stu-id="224b1-199">Set Blob Metadata</span></span> |<span data-ttu-id="224b1-200">Somente proprietário</span><span class="sxs-lookup"><span data-stu-id="224b1-200">Owner only</span></span> |<span data-ttu-id="224b1-201">Somente proprietário</span><span class="sxs-lookup"><span data-stu-id="224b1-201">Owner only</span></span> |
| <span data-ttu-id="224b1-202">Put Block</span><span class="sxs-lookup"><span data-stu-id="224b1-202">Put Block</span></span> |<span data-ttu-id="224b1-203">Somente proprietário</span><span class="sxs-lookup"><span data-stu-id="224b1-203">Owner only</span></span> |<span data-ttu-id="224b1-204">Somente proprietário</span><span class="sxs-lookup"><span data-stu-id="224b1-204">Owner only</span></span> |
| <span data-ttu-id="224b1-205">Obter lista de blocos (somente blocos confirmados)</span><span class="sxs-lookup"><span data-stu-id="224b1-205">Get Block List (committed blocks only)</span></span> |<span data-ttu-id="224b1-206">Todos</span><span class="sxs-lookup"><span data-stu-id="224b1-206">All</span></span> |<span data-ttu-id="224b1-207">Todos</span><span class="sxs-lookup"><span data-stu-id="224b1-207">All</span></span> |
| <span data-ttu-id="224b1-208">Obter lista de blocos (somente blocos não confirmados ou todos os blocos)</span><span class="sxs-lookup"><span data-stu-id="224b1-208">Get Block List (uncommitted blocks only or all blocks)</span></span> |<span data-ttu-id="224b1-209">Somente proprietário</span><span class="sxs-lookup"><span data-stu-id="224b1-209">Owner only</span></span> |<span data-ttu-id="224b1-210">Somente proprietário</span><span class="sxs-lookup"><span data-stu-id="224b1-210">Owner only</span></span> |
| <span data-ttu-id="224b1-211">Put Block List</span><span class="sxs-lookup"><span data-stu-id="224b1-211">Put Block List</span></span> |<span data-ttu-id="224b1-212">Somente proprietário</span><span class="sxs-lookup"><span data-stu-id="224b1-212">Owner only</span></span> |<span data-ttu-id="224b1-213">Somente proprietário</span><span class="sxs-lookup"><span data-stu-id="224b1-213">Owner only</span></span> |
| <span data-ttu-id="224b1-214">Delete Blob</span><span class="sxs-lookup"><span data-stu-id="224b1-214">Delete Blob</span></span> |<span data-ttu-id="224b1-215">Somente proprietário</span><span class="sxs-lookup"><span data-stu-id="224b1-215">Owner only</span></span> |<span data-ttu-id="224b1-216">Somente proprietário</span><span class="sxs-lookup"><span data-stu-id="224b1-216">Owner only</span></span> |
| <span data-ttu-id="224b1-217">Copiar blob</span><span class="sxs-lookup"><span data-stu-id="224b1-217">Copy Blob</span></span> |<span data-ttu-id="224b1-218">Somente proprietário</span><span class="sxs-lookup"><span data-stu-id="224b1-218">Owner only</span></span> |<span data-ttu-id="224b1-219">Somente proprietário</span><span class="sxs-lookup"><span data-stu-id="224b1-219">Owner only</span></span> |
| <span data-ttu-id="224b1-220">Blob de instantâneo</span><span class="sxs-lookup"><span data-stu-id="224b1-220">Snapshot Blob</span></span> |<span data-ttu-id="224b1-221">Somente proprietário</span><span class="sxs-lookup"><span data-stu-id="224b1-221">Owner only</span></span> |<span data-ttu-id="224b1-222">Somente proprietário</span><span class="sxs-lookup"><span data-stu-id="224b1-222">Owner only</span></span> |
| <span data-ttu-id="224b1-223">Lease Blob</span><span class="sxs-lookup"><span data-stu-id="224b1-223">Lease Blob</span></span> |<span data-ttu-id="224b1-224">Somente proprietário</span><span class="sxs-lookup"><span data-stu-id="224b1-224">Owner only</span></span> |<span data-ttu-id="224b1-225">Somente proprietário</span><span class="sxs-lookup"><span data-stu-id="224b1-225">Owner only</span></span> |
| <span data-ttu-id="224b1-226">Put Page</span><span class="sxs-lookup"><span data-stu-id="224b1-226">Put Page</span></span> |<span data-ttu-id="224b1-227">Somente proprietário</span><span class="sxs-lookup"><span data-stu-id="224b1-227">Owner only</span></span> |<span data-ttu-id="224b1-228">Somente proprietário</span><span class="sxs-lookup"><span data-stu-id="224b1-228">Owner only</span></span> |
| <span data-ttu-id="224b1-229">Get Page Ranges</span><span class="sxs-lookup"><span data-stu-id="224b1-229">Get Page Ranges</span></span> |<span data-ttu-id="224b1-230">Todos</span><span class="sxs-lookup"><span data-stu-id="224b1-230">All</span></span> |<span data-ttu-id="224b1-231">Todos</span><span class="sxs-lookup"><span data-stu-id="224b1-231">All</span></span> |
| <span data-ttu-id="224b1-232">Acrescentar blob</span><span class="sxs-lookup"><span data-stu-id="224b1-232">Append Blob</span></span> |<span data-ttu-id="224b1-233">Somente proprietário</span><span class="sxs-lookup"><span data-stu-id="224b1-233">Owner only</span></span> |<span data-ttu-id="224b1-234">Somente proprietário</span><span class="sxs-lookup"><span data-stu-id="224b1-234">Owner only</span></span> |

## <a name="next-steps"></a><span data-ttu-id="224b1-235">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="224b1-235">Next steps</span></span>

* [<span data-ttu-id="224b1-236">Autenticação para Olá serviços de armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="224b1-236">Authentication for hello Azure Storage Services</span></span>](https://msdn.microsoft.com/library/azure/dd179428.aspx)
* [<span data-ttu-id="224b1-237">Uso de SAS (Assinaturas de Acesso Compartilhado)</span><span class="sxs-lookup"><span data-stu-id="224b1-237">Using Shared Access Signatures (SAS)</span></span>](../common/storage-dotnet-shared-access-signature-part-1.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json)
* [<span data-ttu-id="224b1-238">Delegando acesso com uma assinatura de acesso compartilhado</span><span class="sxs-lookup"><span data-stu-id="224b1-238">Delegating Access with a Shared Access Signature</span></span>](https://msdn.microsoft.com/library/azure/ee395415.aspx)
