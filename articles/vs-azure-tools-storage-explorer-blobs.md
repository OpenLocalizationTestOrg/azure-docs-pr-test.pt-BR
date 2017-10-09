---
title: "aaaManage recursos de armazenamento de BLOBs do Azure com o Gerenciador de armazenamento (visualização) | Microsoft Docs"
description: "Gerenciar os contêineres de blob e blobs do Azure com o Gerenciador de Armazenamento (Preview)"
services: storage
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 2f09e545-ec94-4d89-b96c-14783cc9d7a9
ms.service: storage
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/18/2016
ms.author: kraigb
ms.openlocfilehash: 503dd061b205875da127378ab48e8d465800fc09
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-blob-storage-resources-with-storage-explorer-preview"></a><span data-ttu-id="46c52-103">Gerenciar os recursos de Armazenamento de Blobs do Azure com o Gerenciador de Armazenamento (Preview)</span><span class="sxs-lookup"><span data-stu-id="46c52-103">Manage Azure Blob Storage resources with Storage Explorer (Preview)</span></span>
## <a name="overview"></a><span data-ttu-id="46c52-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="46c52-104">Overview</span></span>
<span data-ttu-id="46c52-105">[Armazenamento de BLOBs do Azure](storage/blobs/storage-dotnet-how-to-use-blobs.md) é um serviço para armazenar grandes quantidades de dados não estruturados, como texto ou dados binários, que podem ser acessados de qualquer lugar Olá, mundo via HTTP ou HTTPS.</span><span class="sxs-lookup"><span data-stu-id="46c52-105">[Azure Blob Storage](storage/blobs/storage-dotnet-how-to-use-blobs.md) is a service for storing large amounts of unstructured data, such as text or binary data, that can be accessed from anywhere in hello world via HTTP or HTTPS.</span></span>
<span data-ttu-id="46c52-106">Você pode usar dados de tooexpose de armazenamento de Blob publicamente toohello mundo ou toostore dados de aplicativo em particular.</span><span class="sxs-lookup"><span data-stu-id="46c52-106">You can use Blob storage tooexpose data publicly toohello world, or toostore application data privately.</span></span> <span data-ttu-id="46c52-107">Neste artigo, você aprenderá como toouse toowork de Gerenciador de armazenamento (visualização) com os contêineres de blob e blobs.</span><span class="sxs-lookup"><span data-stu-id="46c52-107">In this article, you'll learn how toouse Storage Explorer (Preview) toowork with blob containers and blobs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="46c52-108">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="46c52-108">Prerequisites</span></span>
<span data-ttu-id="46c52-109">toocomplete Olá etapas neste artigo, você precisará seguir hello:</span><span class="sxs-lookup"><span data-stu-id="46c52-109">toocomplete hello steps in this article, you'll need hello following:</span></span>

* [<span data-ttu-id="46c52-110">Baixe e instale o Gerenciador de Armazenamento (preview)</span><span class="sxs-lookup"><span data-stu-id="46c52-110">Download and install Storage Explorer (preview)</span></span>](http://www.storageexplorer.com)
* [<span data-ttu-id="46c52-111">Conecte-se a conta de armazenamento do Azure tooa ou serviço</span><span class="sxs-lookup"><span data-stu-id="46c52-111">Connect tooa Azure storage account or service</span></span>](vs-azure-tools-storage-manage-with-storage-explorer.md#connect-to-a-storage-account-or-service)

## <a name="create-a-blob-container"></a><span data-ttu-id="46c52-112">Criar um contêiner de blob</span><span class="sxs-lookup"><span data-stu-id="46c52-112">Create a blob container</span></span>
<span data-ttu-id="46c52-113">Todos os blobs devem residir em um contêiner de blob, que é simplesmente um agrupamento lógico de blobs.</span><span class="sxs-lookup"><span data-stu-id="46c52-113">All blobs must reside in a blob container, which is simply a logical grouping of blobs.</span></span> <span data-ttu-id="46c52-114">Uma conta pode conter um número ilimitado de contêineres, e cada contêiner pode armazenar um número ilimitado de blobs.</span><span class="sxs-lookup"><span data-stu-id="46c52-114">An account can contain an unlimited number of containers, and each container can store an unlimited number of blobs.</span></span>

<span data-ttu-id="46c52-115">Olá etapas a seguir ilustram como toocreate um contêiner de blob no Gerenciador de armazenamento (visualização).</span><span class="sxs-lookup"><span data-stu-id="46c52-115">hello following steps illustrate how toocreate a blob container within Storage Explorer (Preview).</span></span>

1. <span data-ttu-id="46c52-116">Abra o Gerenciador de Armazenamento (Preview).</span><span class="sxs-lookup"><span data-stu-id="46c52-116">Open Storage Explorer (Preview).</span></span>
2. <span data-ttu-id="46c52-117">No painel esquerdo do hello, expanda conta de armazenamento hello dentro da qual você deseja que o contêiner de blob toocreate hello.</span><span class="sxs-lookup"><span data-stu-id="46c52-117">In hello left pane, expand hello storage account within which you wish toocreate hello blob container.</span></span>
3. <span data-ttu-id="46c52-118">Clique com botão direito **contêineres de Blob**e - no menu de contexto Olá - selecione **criar contêiner de Blob**.</span><span class="sxs-lookup"><span data-stu-id="46c52-118">Right-click **Blob Containers**, and - from hello context menu - select **Create Blob Container**.</span></span>

   ![Menu de contexto Criar contêineres de blob][0]
4. <span data-ttu-id="46c52-120">Será exibida uma caixa de texto abaixo Olá **contêineres de Blob** pasta.</span><span class="sxs-lookup"><span data-stu-id="46c52-120">A text box will appear below hello **Blob Containers** folder.</span></span> <span data-ttu-id="46c52-121">Insira o nome de saudação para seu contêiner de blob.</span><span class="sxs-lookup"><span data-stu-id="46c52-121">Enter hello name for your blob container.</span></span> <span data-ttu-id="46c52-122">Consulte Olá [as regras de nomenclatura do contêiner](storage/blobs/storage-dotnet-how-to-use-blobs.md#create-a-container) seção para obter uma lista de regras e restrições de nomenclatura de contêineres de blob.</span><span class="sxs-lookup"><span data-stu-id="46c52-122">See hello [Container naming rules](storage/blobs/storage-dotnet-how-to-use-blobs.md#create-a-container) section for a list of rules and restrictions on naming blob containers.</span></span>

   ![Caixa de texto Criar Contêineres de Blob][1]
5. <span data-ttu-id="46c52-124">Pressione **Enter** quando terminar de contêiner de blob do toocreate hello, ou **Esc** toocancel.</span><span class="sxs-lookup"><span data-stu-id="46c52-124">Press **Enter** when done toocreate hello blob container, or **Esc** toocancel.</span></span> <span data-ttu-id="46c52-125">Depois que o contêiner de blob Olá foi criado com êxito, ele será exibido em Olá **contêineres de Blob** pasta para Olá selecionada a conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="46c52-125">Once hello blob container has been successfully created, it will be displayed under hello **Blob Containers** folder for hello selected storage account.</span></span>

   ![Contêiner de blob criado][2]

## <a name="view-a-blob-containers-contents"></a><span data-ttu-id="46c52-127">Exibir o conteúdo de um contêiner de blobs</span><span class="sxs-lookup"><span data-stu-id="46c52-127">View a blob container's contents</span></span>
<span data-ttu-id="46c52-128">Os contêineres de blob contêm blobs e pastas (que também podem conter blobs).</span><span class="sxs-lookup"><span data-stu-id="46c52-128">Blob containers contain blobs and folders (that can also contain blobs).</span></span>

<span data-ttu-id="46c52-129">Olá etapas a seguir ilustram como conteúdo de saudação do tooview de um contêiner de blob no Gerenciador de armazenamento (visualização):</span><span class="sxs-lookup"><span data-stu-id="46c52-129">hello following steps illustrate how tooview hello contents of a blob container within Storage Explorer (Preview):</span></span>

1. <span data-ttu-id="46c52-130">Abra o Gerenciador de Armazenamento (Preview).</span><span class="sxs-lookup"><span data-stu-id="46c52-130">Open Storage Explorer (Preview).</span></span>
2. <span data-ttu-id="46c52-131">No painel esquerdo do hello, expanda conta de armazenamento Olá que contém o contêiner de blob Olá desejar tooview.</span><span class="sxs-lookup"><span data-stu-id="46c52-131">In hello left pane, expand hello storage account containing hello blob container you wish tooview.</span></span>
3. <span data-ttu-id="46c52-132">Expanda a conta de armazenamento Olá **contêineres de Blob**.</span><span class="sxs-lookup"><span data-stu-id="46c52-132">Expand hello storage account's **Blob Containers**.</span></span>
4. <span data-ttu-id="46c52-133">Contêiner de blob de saudação do botão direito do mouse seu gosto tooview e - no menu de contexto Olá - selecione **abrir Editor de contêiner de Blob**.</span><span class="sxs-lookup"><span data-stu-id="46c52-133">Right-click hello blob container you wish tooview, and - from hello context menu - select **Open Blob Container Editor**.</span></span>
   <span data-ttu-id="46c52-134">Você também pode clicar duas vezes desejar tooview de contêiner de blob hello.</span><span class="sxs-lookup"><span data-stu-id="46c52-134">You can also double-click hello blob container you wish tooview.</span></span>

   ![Menu de contexto Abrir editor do contêiner de blobs][19]
5. <span data-ttu-id="46c52-136">painel principal Olá exibirá o conteúdo do contêiner de blob hello.</span><span class="sxs-lookup"><span data-stu-id="46c52-136">hello main pane will display hello blob container's contents.</span></span>

   ![Editor do Contêiner de blobs][3]

## <a name="delete-a-blob-container"></a><span data-ttu-id="46c52-138">Excluir um contêiner de blob</span><span class="sxs-lookup"><span data-stu-id="46c52-138">Delete a blob container</span></span>
<span data-ttu-id="46c52-139">Os contêineres de blob podem ser facilmente criados e excluídos conforme o necessário.</span><span class="sxs-lookup"><span data-stu-id="46c52-139">Blob containers can be easily created and deleted as needed.</span></span> <span data-ttu-id="46c52-140">(toosee como blobs toodelete individuais, consulte a seção toohello, [Gerenciando blobs em um contêiner de blob](#managing-blobs-in-a-blob-container).)</span><span class="sxs-lookup"><span data-stu-id="46c52-140">(toosee how toodelete individual blobs, refer toohello section, [Managing blobs in a blob container](#managing-blobs-in-a-blob-container).)</span></span>

<span data-ttu-id="46c52-141">Olá etapas a seguir ilustram como toodelete um contêiner de blob no Gerenciador de armazenamento (visualização):</span><span class="sxs-lookup"><span data-stu-id="46c52-141">hello following steps illustrate how toodelete a blob container within Storage Explorer (Preview):</span></span>

1. <span data-ttu-id="46c52-142">Abra o Gerenciador de Armazenamento (Preview).</span><span class="sxs-lookup"><span data-stu-id="46c52-142">Open Storage Explorer (Preview).</span></span>
2. <span data-ttu-id="46c52-143">No painel esquerdo do hello, expanda conta de armazenamento Olá que contém o contêiner de blob Olá desejar tooview.</span><span class="sxs-lookup"><span data-stu-id="46c52-143">In hello left pane, expand hello storage account containing hello blob container you wish tooview.</span></span>
3. <span data-ttu-id="46c52-144">Expanda a conta de armazenamento Olá **contêineres de Blob**.</span><span class="sxs-lookup"><span data-stu-id="46c52-144">Expand hello storage account's **Blob Containers**.</span></span>
4. <span data-ttu-id="46c52-145">Contêiner de blob de saudação do botão direito do mouse seu gosto toodelete e - no menu de contexto Olá - selecione **excluir**.</span><span class="sxs-lookup"><span data-stu-id="46c52-145">Right-click hello blob container you wish toodelete, and - from hello context menu - select **Delete**.</span></span>
   <span data-ttu-id="46c52-146">Você também pode pressionar **excluir** contêiner de blob atualmente selecionado Olá toodelete.</span><span class="sxs-lookup"><span data-stu-id="46c52-146">You can also press **Delete** toodelete hello currently selected blob container.</span></span>

   ![Menu de contexto Excluir contêiner de blobs][4]
5. <span data-ttu-id="46c52-148">Selecione **Sim** toohello caixa de diálogo de confirmação.</span><span class="sxs-lookup"><span data-stu-id="46c52-148">Select **Yes** toohello confirmation dialog.</span></span>

   ![Confirmação de exclusão do contêiner de blobs][5]

## <a name="copy-a-blob-container"></a><span data-ttu-id="46c52-150">Copiar um contêiner de blobs</span><span class="sxs-lookup"><span data-stu-id="46c52-150">Copy a blob container</span></span>
<span data-ttu-id="46c52-151">O Gerenciador de armazenamento (visualização) permite que você toocopy uma área de transferência de toohello de contêiner de blob e cole que o contêiner de blob em outra conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="46c52-151">Storage Explorer (Preview) enables you toocopy a blob container toohello clipboard, and then paste that blob container into another storage account.</span></span> <span data-ttu-id="46c52-152">(toosee como blobs toocopy individuais, consulte a seção toohello, [Gerenciando blobs em um contêiner de blob](#managing-blobs-in-a-blob-container).)</span><span class="sxs-lookup"><span data-stu-id="46c52-152">(toosee how toocopy individual blobs, refer toohello section, [Managing blobs in a blob container](#managing-blobs-in-a-blob-container).)</span></span>

<span data-ttu-id="46c52-153">Olá, as etapas a seguir ilustra como toocopy um contêiner de blob do armazenamento de uma conta tooanother.</span><span class="sxs-lookup"><span data-stu-id="46c52-153">hello following steps illustrate how toocopy a blob container from one storage account tooanother.</span></span>

1. <span data-ttu-id="46c52-154">Abra o Gerenciador de Armazenamento (Preview).</span><span class="sxs-lookup"><span data-stu-id="46c52-154">Open Storage Explorer (Preview).</span></span>
2. <span data-ttu-id="46c52-155">No painel esquerdo do hello, expanda conta de armazenamento Olá que contém o contêiner de blob Olá desejar toocopy.</span><span class="sxs-lookup"><span data-stu-id="46c52-155">In hello left pane, expand hello storage account containing hello blob container you wish toocopy.</span></span>
3. <span data-ttu-id="46c52-156">Expanda a conta de armazenamento Olá **contêineres de Blob**.</span><span class="sxs-lookup"><span data-stu-id="46c52-156">Expand hello storage account's **Blob Containers**.</span></span>
4. <span data-ttu-id="46c52-157">Contêiner de blob de saudação do botão direito do mouse seu gosto toocopy e - no menu de contexto Olá - selecione **contêiner de Blob de cópia**.</span><span class="sxs-lookup"><span data-stu-id="46c52-157">Right-click hello blob container you wish toocopy, and - from hello context menu - select **Copy Blob Container**.</span></span>

   ![Menu de contexto Copiar contêiner de blobs][6]
5. <span data-ttu-id="46c52-159">Clique em destino"hello desejado" conta de armazenamento no qual você deseja contêiner de blob toopaste Olá e - no menu de contexto Olá - selecione **contêiner de Blob de colar**.</span><span class="sxs-lookup"><span data-stu-id="46c52-159">Right-click hello desired "target" storage account into which you want toopaste hello blob container, and - from hello context menu - select **Paste Blob Container**.</span></span>

   ![Menu de contexto Colar contêiner de blobs][7]

## <a name="get-hello-sas-for-a-blob-container"></a><span data-ttu-id="46c52-161">Obter Olá SAS para um contêiner de blob</span><span class="sxs-lookup"><span data-stu-id="46c52-161">Get hello SAS for a blob container</span></span>
<span data-ttu-id="46c52-162">Um [assinatura de acesso compartilhado (SAS)](storage/common/storage-dotnet-shared-access-signature-part-1.md) fornece acesso delegado tooresources na sua conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="46c52-162">A [shared access signature (SAS)](storage/common/storage-dotnet-shared-access-signature-part-1.md) provides delegated access tooresources in your storage account.</span></span>
<span data-ttu-id="46c52-163">Isso significa que você pode conceder a que um cliente limitada tooobjects permissões na conta de armazenamento para um determinado período de tempo e com um conjunto especificado de permissões, sem a necessidade de compartilhar as chaves de acesso da conta.</span><span class="sxs-lookup"><span data-stu-id="46c52-163">This means that you can grant a client limited permissions tooobjects in your storage account for a specified period of time and with a specified set of permissions, without having to share your account access keys.</span></span>

<span data-ttu-id="46c52-164">Olá etapas a seguir ilustram como toocreate um SAS para um contêiner de blob:</span><span class="sxs-lookup"><span data-stu-id="46c52-164">hello following steps illustrate how toocreate a SAS for a blob container:</span></span>

1. <span data-ttu-id="46c52-165">Abra o Gerenciador de Armazenamento (Preview).</span><span class="sxs-lookup"><span data-stu-id="46c52-165">Open Storage Explorer (Preview).</span></span>
2. <span data-ttu-id="46c52-166">No painel esquerdo do hello, expanda a conta de armazenamento Olá que contém o contêiner de blob Olá para o qual você deseja tooget uma SAS.</span><span class="sxs-lookup"><span data-stu-id="46c52-166">In hello left pane, expand hello storage account containing hello blob container for which you wish tooget a SAS.</span></span>
3. <span data-ttu-id="46c52-167">Expanda a conta de armazenamento Olá **contêineres de Blob**.</span><span class="sxs-lookup"><span data-stu-id="46c52-167">Expand hello storage account's **Blob Containers**.</span></span>
4. <span data-ttu-id="46c52-168">Contêiner de BLOBs desejado hello e - no menu de contexto Olá - selecione **obter assinatura de acesso compartilhado**.</span><span class="sxs-lookup"><span data-stu-id="46c52-168">Right-click hello desired blob container, and - from hello context menu - select **Get Shared Access Signature**.</span></span>

   ![Menu de contexto Obter SAS][8]
5. <span data-ttu-id="46c52-170">Em Olá **assinatura de acesso compartilhado** caixa de diálogo, especifique política hello, datas de início e vencimento, fuso horário e você deseja para o recurso de saudação de níveis de acesso.</span><span class="sxs-lookup"><span data-stu-id="46c52-170">In hello **Shared Access Signature** dialog, specify hello policy, start and expiration dates, time zone, and access levels you want for hello resource.</span></span>

   ![Opções de Obter SAS][9]
6. <span data-ttu-id="46c52-172">Quando tiver terminado de especificar opções de SAS hello, selecione **criar**.</span><span class="sxs-lookup"><span data-stu-id="46c52-172">When you're finished specifying hello SAS options, select **Create**.</span></span>
7. <span data-ttu-id="46c52-173">Um segundo **assinatura de acesso compartilhado** caixa de diálogo, em seguida, exibirá que listas Olá contêiner de blob juntamente com a URL de saudação e QueryStrings que você pode usar tooaccess Olá recurso de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="46c52-173">A second **Shared Access Signature** dialog will then display that lists hello blob container along with hello URL and QueryStrings you can use tooaccess hello storage resource.</span></span>
   <span data-ttu-id="46c52-174">Selecione **cópia** próximo URL toohello desejar toocopy toohello da área de transferência.</span><span class="sxs-lookup"><span data-stu-id="46c52-174">Select **Copy** next toohello URL you wish toocopy toohello clipboard.</span></span>

   ![Copiar URLs de SAS][10]
8. <span data-ttu-id="46c52-176">Ao terminar, escolha **Fechar**.</span><span class="sxs-lookup"><span data-stu-id="46c52-176">When done, select **Close**.</span></span>

## <a name="manage-access-policies-for-a-blob-container"></a><span data-ttu-id="46c52-177">Gerenciar políticas de acesso para um contêiner de blobs</span><span class="sxs-lookup"><span data-stu-id="46c52-177">Manage Access Policies for a blob container</span></span>
<span data-ttu-id="46c52-178">Olá etapas a seguir ilustram como toomanage (Adicionar e remover) políticas de acesso para um contêiner de blob:</span><span class="sxs-lookup"><span data-stu-id="46c52-178">hello following steps illustrate how toomanage (add and remove) access policies for a blob container:</span></span>

1. <span data-ttu-id="46c52-179">Abra o Gerenciador de Armazenamento (Preview).</span><span class="sxs-lookup"><span data-stu-id="46c52-179">Open Storage Explorer (Preview).</span></span>
2. <span data-ttu-id="46c52-180">No painel esquerdo do hello, expanda que contém o contêiner de blob Olá cujas desejar toomanage as políticas de acesso de conta de armazenamento hello.</span><span class="sxs-lookup"><span data-stu-id="46c52-180">In hello left pane, expand hello storage account containing hello blob container whose access policies you wish toomanage.</span></span>
3. <span data-ttu-id="46c52-181">Expanda a conta de armazenamento Olá **contêineres de Blob**.</span><span class="sxs-lookup"><span data-stu-id="46c52-181">Expand hello storage account's **Blob Containers**.</span></span>
4. <span data-ttu-id="46c52-182">Selecione o contêiner de BLOBs desejado hello e - no menu de contexto Olá - selecione **gerenciar políticas de acesso**.</span><span class="sxs-lookup"><span data-stu-id="46c52-182">Select hello desired blob container, and - from hello context menu - select **Manage Access Policies**.</span></span>

   ![Menu de contexto Gerenciar políticas de acesso][11]
5. <span data-ttu-id="46c52-184">Olá **políticas de acesso** diálogo listará todas as políticas de acesso já foi criadas para o contêiner de BLOBs selecionados hello.</span><span class="sxs-lookup"><span data-stu-id="46c52-184">hello **Access Policies** dialog will list any access policies already created for hello selected blob container.</span></span>

   ![Opções de Política de Acesso][12]        
6. <span data-ttu-id="46c52-186">Siga estas etapas, dependendo da tarefa de gerenciamento de política de acesso de saudação:</span><span class="sxs-lookup"><span data-stu-id="46c52-186">Follow these steps depending on hello access policy management task:</span></span>

   * <span data-ttu-id="46c52-187">**Adicionar uma nova política de acesso** — escolha **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="46c52-187">**Add a new access policy** - Select **Add**.</span></span> <span data-ttu-id="46c52-188">Uma vez gerado, Olá **políticas de acesso** caixa de diálogo exibirá Olá recém-adicionado acessar política (com configurações padrão).</span><span class="sxs-lookup"><span data-stu-id="46c52-188">Once generated, hello **Access Policies** dialog will display hello newly added access policy (with default settings).</span></span>
   * <span data-ttu-id="46c52-189">**Editar uma política de acesso** — faça as edições desejadas e escolha **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="46c52-189">**Edit an access policy** -  Make any desired edits, and select **Save**.</span></span>
   * <span data-ttu-id="46c52-190">**Remover uma política de acesso** - selecione **remover** próximo toohello de política de acesso você deseja tooremove.</span><span class="sxs-lookup"><span data-stu-id="46c52-190">**Remove an access policy** - Select **Remove** next toohello access policy you wish tooremove.</span></span>

## <a name="set-hello-public-access-level-for-a-blob-container"></a><span data-ttu-id="46c52-191">Saudação de conjunto de nível de acesso público para um contêiner de blob</span><span class="sxs-lookup"><span data-stu-id="46c52-191">Set hello Public Access Level for a blob container</span></span>
<span data-ttu-id="46c52-192">Por padrão, cada contêiner de blob está definido muito "Nenhum acesso público".</span><span class="sxs-lookup"><span data-stu-id="46c52-192">By default, every blob container is set too"No public access".</span></span>

<span data-ttu-id="46c52-193">Olá etapas a seguir ilustram como toospecify um público acesso nível para um contêiner de blob.</span><span class="sxs-lookup"><span data-stu-id="46c52-193">hello following steps illustrate how toospecify a public access level for a blob container.</span></span>

1. <span data-ttu-id="46c52-194">Abra o Gerenciador de Armazenamento (Preview).</span><span class="sxs-lookup"><span data-stu-id="46c52-194">Open Storage Explorer (Preview).</span></span>
2. <span data-ttu-id="46c52-195">No painel esquerdo do hello, expanda que contém o contêiner de blob Olá cujas desejar toomanage as políticas de acesso de conta de armazenamento hello.</span><span class="sxs-lookup"><span data-stu-id="46c52-195">In hello left pane, expand hello storage account containing hello blob container whose access policies you wish toomanage.</span></span>
3. <span data-ttu-id="46c52-196">Expanda a conta de armazenamento Olá **contêineres de Blob**.</span><span class="sxs-lookup"><span data-stu-id="46c52-196">Expand hello storage account's **Blob Containers**.</span></span>
4. <span data-ttu-id="46c52-197">Selecione o contêiner de BLOBs desejado hello e - no menu de contexto Olá - selecione **definir o nível de acesso público**.</span><span class="sxs-lookup"><span data-stu-id="46c52-197">Select hello desired blob container, and - from hello context menu - select **Set Public Access Level**.</span></span>

   ![Menu de contexto Definir nível de acesso público][13]
5. <span data-ttu-id="46c52-199">Em Olá **definir o nível de acesso público de contêiner** caixa de diálogo, especifique o nível de acesso de saudação desejada.</span><span class="sxs-lookup"><span data-stu-id="46c52-199">In hello **Set Container Public Access Level** dialog, specify hello desired access level.</span></span>

   ![Opções de Definir nível de acesso público][14]
6. <span data-ttu-id="46c52-201">Escolha **Aplicar**.</span><span class="sxs-lookup"><span data-stu-id="46c52-201">Select **Apply**.</span></span>

## <a name="managing-blobs-in-a-blob-container"></a><span data-ttu-id="46c52-202">Gerenciamento de blobs em um contêiner de blobs</span><span class="sxs-lookup"><span data-stu-id="46c52-202">Managing blobs in a blob container</span></span>
<span data-ttu-id="46c52-203">Depois de criar um contêiner de blob, você pode carregar um contêiner de blob do blob toothat, fazer o download de um computador local do blob tooyour, abrir um blob em seu computador local e muito mais.</span><span class="sxs-lookup"><span data-stu-id="46c52-203">Once you've created a blob container, you can upload a blob toothat blob container, download a blob tooyour local computer, open a blob on your local computer, and much more.</span></span>

<span data-ttu-id="46c52-204">Olá, as etapas a seguir ilustra como toomanage Olá blobs (e pastas) em um contêiner de blob.</span><span class="sxs-lookup"><span data-stu-id="46c52-204">hello following steps illustrate how toomanage hello blobs (and folders) within a blob container.</span></span>

1. <span data-ttu-id="46c52-205">Abra o Gerenciador de Armazenamento (Preview).</span><span class="sxs-lookup"><span data-stu-id="46c52-205">Open Storage Explorer (Preview).</span></span>
2. <span data-ttu-id="46c52-206">No painel esquerdo do hello, expanda conta de armazenamento Olá que contém o contêiner de blob Olá desejar toomanage.</span><span class="sxs-lookup"><span data-stu-id="46c52-206">In hello left pane, expand hello storage account containing hello blob container you wish toomanage.</span></span>
3. <span data-ttu-id="46c52-207">Expanda a conta de armazenamento Olá **contêineres de Blob**.</span><span class="sxs-lookup"><span data-stu-id="46c52-207">Expand hello storage account's **Blob Containers**.</span></span>
4. <span data-ttu-id="46c52-208">Clique duas vezes no contêiner de blob Olá desejar tooview.</span><span class="sxs-lookup"><span data-stu-id="46c52-208">Double-click hello blob container you wish tooview.</span></span>
5. <span data-ttu-id="46c52-209">painel principal Olá exibirá o conteúdo do contêiner de blob hello.</span><span class="sxs-lookup"><span data-stu-id="46c52-209">hello main pane will display hello blob container's contents.</span></span>

   ![Exibir contêiner de blobs][3]
6. <span data-ttu-id="46c52-211">painel principal Olá exibirá o conteúdo do contêiner de blob hello.</span><span class="sxs-lookup"><span data-stu-id="46c52-211">hello main pane will display hello blob container's contents.</span></span>
7. <span data-ttu-id="46c52-212">Siga estas que etapas, dependendo da tarefa Olá desejar tooperform:</span><span class="sxs-lookup"><span data-stu-id="46c52-212">Follow these steps depending on hello task you wish tooperform:</span></span>

   * <span data-ttu-id="46c52-213">**Carregar o contêiner de blob tooa arquivos**</span><span class="sxs-lookup"><span data-stu-id="46c52-213">**Upload files tooa blob container**</span></span>

     1. <span data-ttu-id="46c52-214">Na barra de ferramentas do painel Olá principal, selecione **carregar**e, em seguida, **carregar arquivos** do menu suspenso de saudação.</span><span class="sxs-lookup"><span data-stu-id="46c52-214">On hello main pane's toolbar, select **Upload**, and then **Upload Files** from hello drop-down menu.</span></span>

        ![Menu Carregar arquivos][15]
     2. <span data-ttu-id="46c52-216">Em Olá **carregar arquivos** caixa de diálogo, reticências Olá select (**...** ) botão no lado direito de saudação do hello **arquivos** tooselect Olá arquivos desejar tooupload da caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="46c52-216">In hello **Upload files** dialog, select hello ellipsis (**…**) button on hello right side of hello **Files** text box tooselect hello file(s) you wish tooupload.</span></span>

        ![Opções de Carregar arquivos][16]
     3. <span data-ttu-id="46c52-218">Especificar o tipo de saudação do **Blob tipo**.</span><span class="sxs-lookup"><span data-stu-id="46c52-218">Specify hello type of **Blob type**.</span></span> <span data-ttu-id="46c52-219">artigo Olá [Introdução ao armazenamento de BLOBs do Azure usando o .NET](storage/blobs/storage-dotnet-how-to-use-blobs.md#blob-service-concepts) explica as diferenças de saudação entre hello vários tipos de blob.</span><span class="sxs-lookup"><span data-stu-id="46c52-219">hello article [Get started with Azure Blob storage using .NET](storage/blobs/storage-dotnet-how-to-use-blobs.md#blob-service-concepts) explains hello differences between hello various blob types.</span></span>
     4. <span data-ttu-id="46c52-220">Opcionalmente, especifique uma pasta de destino na qual arquivos selecionados hello serão carregados.</span><span class="sxs-lookup"><span data-stu-id="46c52-220">Optionally, specify a target folder into which hello selected file(s) will be uploaded.</span></span> <span data-ttu-id="46c52-221">Se a pasta de destino de saudação não existir, ele será criado.</span><span class="sxs-lookup"><span data-stu-id="46c52-221">If hello target folder doesn’t exist, it will be created.</span></span>
     5. <span data-ttu-id="46c52-222">Escolha **Carregar**.</span><span class="sxs-lookup"><span data-stu-id="46c52-222">Select **Upload**.</span></span>
   * <span data-ttu-id="46c52-223">**Carregar um contêiner de blob de tooa de pasta**</span><span class="sxs-lookup"><span data-stu-id="46c52-223">**Upload a folder tooa blob container**</span></span>

     1. <span data-ttu-id="46c52-224">Na barra de ferramentas do painel Olá principal, selecione **carregar**e, em seguida, **carregar pasta** do menu suspenso de saudação.</span><span class="sxs-lookup"><span data-stu-id="46c52-224">On hello main pane's toolbar, select **Upload**, and then **Upload Folder** from hello drop-down menu.</span></span>

        ![Menu Carregar pasta][17]
     2. <span data-ttu-id="46c52-226">Em Olá **pasta carregamento** caixa de diálogo, reticências Olá select (**...** ) botão no lado direito de saudação do hello **pasta** pasta de saudação de tooselect de caixa de texto cujo conteúdo você deseja tooupload.</span><span class="sxs-lookup"><span data-stu-id="46c52-226">In hello **Upload folder** dialog, select hello ellipsis (**…**) button on hello right side of hello **Folder** text box tooselect hello folder whose contents you wish tooupload.</span></span>

        ![Opções de Carregar pasta][18]
     3. <span data-ttu-id="46c52-228">Especificar o tipo de saudação do **Blob tipo**.</span><span class="sxs-lookup"><span data-stu-id="46c52-228">Specify hello type of **Blob type**.</span></span> <span data-ttu-id="46c52-229">artigo Olá [Introdução ao armazenamento de BLOBs do Azure usando o .NET](storage/blobs/storage-dotnet-how-to-use-blobs.md#blob-service-concepts) explica as diferenças de saudação entre hello vários tipos de blob.</span><span class="sxs-lookup"><span data-stu-id="46c52-229">hello article [Get started with Azure Blob storage using .NET](storage/blobs/storage-dotnet-how-to-use-blobs.md#blob-service-concepts) explains hello differences between hello various blob types.</span></span>
     4. <span data-ttu-id="46c52-230">Opcionalmente, especifique uma pasta de destino no qual Olá conteúdo da pasta selecionada será carregado.</span><span class="sxs-lookup"><span data-stu-id="46c52-230">Optionally, specify a target folder into which hello selected folder's contents will be uploaded.</span></span> <span data-ttu-id="46c52-231">Se a pasta de destino de saudação não existir, ele será criado.</span><span class="sxs-lookup"><span data-stu-id="46c52-231">If hello target folder doesn’t exist, it will be created.</span></span>
     5. <span data-ttu-id="46c52-232">Escolha **Carregar**.</span><span class="sxs-lookup"><span data-stu-id="46c52-232">Select **Upload**.</span></span>
   * <span data-ttu-id="46c52-233">**Fazer o download de um computador local do blob tooyour**</span><span class="sxs-lookup"><span data-stu-id="46c52-233">**Download a blob tooyour local computer**</span></span>

     1. <span data-ttu-id="46c52-234">Selecione blob Olá desejar toodownload.</span><span class="sxs-lookup"><span data-stu-id="46c52-234">Select hello blob you wish toodownload.</span></span>
     2. <span data-ttu-id="46c52-235">Na barra de ferramentas do painel Olá principal, selecione **baixar**.</span><span class="sxs-lookup"><span data-stu-id="46c52-235">On hello main pane's toolbar, select **Download**.</span></span>
     3. <span data-ttu-id="46c52-236">Em Olá **especifique onde toosave Olá baixou blob** caixa de diálogo, especifique Olá local onde você deseja que o blob Olá baixado e Olá nome você deseja toogive-lo.</span><span class="sxs-lookup"><span data-stu-id="46c52-236">In hello **Specify where toosave hello downloaded blob** dialog, specify hello location where you want hello blob downloaded, and hello name you wish toogive it.</span></span>  
     4. <span data-ttu-id="46c52-237">Selecione **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="46c52-237">Select **Save**.</span></span>
   * <span data-ttu-id="46c52-238">**Abrir um blob em seu computador local**</span><span class="sxs-lookup"><span data-stu-id="46c52-238">**Open a blob on your local computer**</span></span>

     1. <span data-ttu-id="46c52-239">Selecione blob Olá desejar tooopen.</span><span class="sxs-lookup"><span data-stu-id="46c52-239">Select hello blob you wish tooopen.</span></span>
     2. <span data-ttu-id="46c52-240">Na barra de ferramentas do painel Olá principal, selecione **abrir**.</span><span class="sxs-lookup"><span data-stu-id="46c52-240">On hello main pane's toolbar, select **Open**.</span></span>
     3. <span data-ttu-id="46c52-241">blob Olá será baixado e aberto usando o aplicativo hello associado com o tipo subjacente de arquivo do blob hello.</span><span class="sxs-lookup"><span data-stu-id="46c52-241">hello blob will be downloaded and opened using hello application associated with hello blob's underlying file type.</span></span>
   * <span data-ttu-id="46c52-242">**Copiar uma área de transferência do blob toohello**</span><span class="sxs-lookup"><span data-stu-id="46c52-242">**Copy a blob toohello clipboard**</span></span>

     1. <span data-ttu-id="46c52-243">Selecione blob Olá desejar toocopy.</span><span class="sxs-lookup"><span data-stu-id="46c52-243">Select hello blob you wish toocopy.</span></span>
     2. <span data-ttu-id="46c52-244">Na barra de ferramentas do painel Olá principal, selecione **cópia**.</span><span class="sxs-lookup"><span data-stu-id="46c52-244">On hello main pane's toolbar, select **Copy**.</span></span>
     3. <span data-ttu-id="46c52-245">No painel esquerdo do hello, navegar tooanother contêiner de blob e clique duas vezes nele tooview-lo no painel principal hello.</span><span class="sxs-lookup"><span data-stu-id="46c52-245">In hello left pane, navigate tooanother blob container, and double-click it tooview it in hello main pane.</span></span>
     4. <span data-ttu-id="46c52-246">Na barra de ferramentas do painel Olá principal, selecione **colar** toocreate uma cópia de blob de saudação.</span><span class="sxs-lookup"><span data-stu-id="46c52-246">On hello main pane's toolbar, select **Paste** toocreate a copy of hello blob.</span></span>
   * <span data-ttu-id="46c52-247">**Excluir um blob**</span><span class="sxs-lookup"><span data-stu-id="46c52-247">**Delete a blob**</span></span>

     1. <span data-ttu-id="46c52-248">Selecione blob Olá desejar toodelete.</span><span class="sxs-lookup"><span data-stu-id="46c52-248">Select hello blob you wish toodelete.</span></span>
     2. <span data-ttu-id="46c52-249">Na barra de ferramentas do painel Olá principal, selecione **excluir**.</span><span class="sxs-lookup"><span data-stu-id="46c52-249">On hello main pane's toolbar, select **Delete**.</span></span>
     3. <span data-ttu-id="46c52-250">Selecione **Sim** toohello caixa de diálogo de confirmação.</span><span class="sxs-lookup"><span data-stu-id="46c52-250">Select **Yes** toohello confirmation dialog.</span></span>

## <a name="next-steps"></a><span data-ttu-id="46c52-251">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="46c52-251">Next steps</span></span>
* <span data-ttu-id="46c52-252">Saudação de exibição [notas de versão do Gerenciador de armazenamento (visualização) e vídeos mais recentes](http://www.storageexplorer.com).</span><span class="sxs-lookup"><span data-stu-id="46c52-252">View hello [latest Storage Explorer (Preview) release notes and videos](http://www.storageexplorer.com).</span></span>
* <span data-ttu-id="46c52-253">Saiba como muito[criar aplicativos usando blobs do Azure, tabelas, filas e arquivos](https://azure.microsoft.com/documentation/services/storage/).</span><span class="sxs-lookup"><span data-stu-id="46c52-253">Learn how too[create applications using Azure blobs, tables, queues, and files](https://azure.microsoft.com/documentation/services/storage/).</span></span>

[0]: ./media/vs-azure-tools-storage-explorer-blobs/blob-containers-create-context-menu.png
[1]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-create.png
[2]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-create-done.png
[3]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-editor.png
[4]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-delete-context-menu.png
[5]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-delete-confirmation.png
[6]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-copy-context-menu.png
[7]: ./media/vs-azure-tools-storage-explorer-blobs/blob-containers-paste-context-menu.png
[8]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-get-sas-context-menu.png
[9]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-get-sas-options.png
[10]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-get-sas-urls.png
[11]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-manage-access-policies-context-menu.png
[12]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-manage-access-policies-options.png
[13]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-set-public-access-level-context-menu.png
[14]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-set-public-access-level-options.png
[15]: ./media/vs-azure-tools-storage-explorer-blobs/blob-upload-files-menu.png
[16]: ./media/vs-azure-tools-storage-explorer-blobs/blob-upload-files-options.png
[17]: ./media/vs-azure-tools-storage-explorer-blobs/blob-upload-folder-menu.png
[18]: ./media/vs-azure-tools-storage-explorer-blobs/blob-upload-folder-options.png
[19]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-open-editor-context-menu.png
