---
title: Gerenciar recursos do Armazenamento de Blobs do Azure com o Gerenciador de Armazenamento (Preview) | Microsoft Docs
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
ms.openlocfilehash: f833027203441e12340bd93f3570de073d297223
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="manage-azure-blob-storage-resources-with-storage-explorer-preview"></a><span data-ttu-id="6d7d0-103">Gerenciar os recursos de Armazenamento de Blobs do Azure com o Gerenciador de Armazenamento (Preview)</span><span class="sxs-lookup"><span data-stu-id="6d7d0-103">Manage Azure Blob Storage resources with Storage Explorer (Preview)</span></span>
## <a name="overview"></a><span data-ttu-id="6d7d0-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="6d7d0-104">Overview</span></span>
<span data-ttu-id="6d7d0-105">O [Armazenamento de Blobs do Azure](storage/blobs/storage-dotnet-how-to-use-blobs.md) é um serviço para armazenar grandes quantidades de dados não estruturados, como texto ou dados binários, que podem ser acessados de qualquer lugar do mundo por meio de HTTP ou HTTPS.</span><span class="sxs-lookup"><span data-stu-id="6d7d0-105">[Azure Blob Storage](storage/blobs/storage-dotnet-how-to-use-blobs.md) is a service for storing large amounts of unstructured data, such as text or binary data, that can be accessed from anywhere in the world via HTTP or HTTPS.</span></span>
<span data-ttu-id="6d7d0-106">Você pode usar o armazenamento de Blob para expor dados publicamente para o mundo ou para armazenar dados do aplicativo de forma privada.</span><span class="sxs-lookup"><span data-stu-id="6d7d0-106">You can use Blob storage to expose data publicly to the world, or to store application data privately.</span></span> <span data-ttu-id="6d7d0-107">Neste artigo, você aprenderá a usar o Gerenciador de Armazenamento (Preview) para trabalhar com contêineres de blob e blobs.</span><span class="sxs-lookup"><span data-stu-id="6d7d0-107">In this article, you'll learn how to use Storage Explorer (Preview) to work with blob containers and blobs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6d7d0-108">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="6d7d0-108">Prerequisites</span></span>
<span data-ttu-id="6d7d0-109">Para concluir as etapas neste artigo, você precisará do seguinte:</span><span class="sxs-lookup"><span data-stu-id="6d7d0-109">To complete the steps in this article, you'll need the following:</span></span>

* [<span data-ttu-id="6d7d0-110">Baixe e instale o Gerenciador de Armazenamento (preview)</span><span class="sxs-lookup"><span data-stu-id="6d7d0-110">Download and install Storage Explorer (preview)</span></span>](http://www.storageexplorer.com)
* [<span data-ttu-id="6d7d0-111">Conectar-se a uma conta de armazenamento ou serviço do Azure</span><span class="sxs-lookup"><span data-stu-id="6d7d0-111">Connect to a Azure storage account or service</span></span>](vs-azure-tools-storage-manage-with-storage-explorer.md#connect-to-a-storage-account-or-service)

## <a name="create-a-blob-container"></a><span data-ttu-id="6d7d0-112">Criar um contêiner de blob</span><span class="sxs-lookup"><span data-stu-id="6d7d0-112">Create a blob container</span></span>
<span data-ttu-id="6d7d0-113">Todos os blobs devem residir em um contêiner de blob, que é simplesmente um agrupamento lógico de blobs.</span><span class="sxs-lookup"><span data-stu-id="6d7d0-113">All blobs must reside in a blob container, which is simply a logical grouping of blobs.</span></span> <span data-ttu-id="6d7d0-114">Uma conta pode conter um número ilimitado de contêineres, e cada contêiner pode armazenar um número ilimitado de blobs.</span><span class="sxs-lookup"><span data-stu-id="6d7d0-114">An account can contain an unlimited number of containers, and each container can store an unlimited number of blobs.</span></span>

<span data-ttu-id="6d7d0-115">As etapas a seguir ilustram como criar um contêiner de blobs no Gerenciador de Armazenamento (Preview).</span><span class="sxs-lookup"><span data-stu-id="6d7d0-115">The following steps illustrate how to create a blob container within Storage Explorer (Preview).</span></span>

1. <span data-ttu-id="6d7d0-116">Abra o Gerenciador de Armazenamento (Preview).</span><span class="sxs-lookup"><span data-stu-id="6d7d0-116">Open Storage Explorer (Preview).</span></span>
2. <span data-ttu-id="6d7d0-117">No painel esquerdo, expanda a conta de armazenamento na qual você deseja criar o contêiner de blobs.</span><span class="sxs-lookup"><span data-stu-id="6d7d0-117">In the left pane, expand the storage account within which you wish to create the blob container.</span></span>
3. <span data-ttu-id="6d7d0-118">Clique com botão direito em **Contêineres de Blob** e, no menu de contexto, selecione **Criar Contêiner de Blobs**.</span><span class="sxs-lookup"><span data-stu-id="6d7d0-118">Right-click **Blob Containers**, and - from the context menu - select **Create Blob Container**.</span></span>

   ![Menu de contexto Criar contêineres de blob][0]
4. <span data-ttu-id="6d7d0-120">Uma caixa de texto será exibida abaixo da pasta **Contêineres de Blob** .</span><span class="sxs-lookup"><span data-stu-id="6d7d0-120">A text box will appear below the **Blob Containers** folder.</span></span> <span data-ttu-id="6d7d0-121">Insira o nome de seu contêiner de blobs.</span><span class="sxs-lookup"><span data-stu-id="6d7d0-121">Enter the name for your blob container.</span></span> <span data-ttu-id="6d7d0-122">Confira a seção [Regras de nomenclatura do contêiner](storage/blobs/storage-dotnet-how-to-use-blobs.md#create-a-container) para obter uma lista de regras e restrições sobre como nomear os contêineres de blob.</span><span class="sxs-lookup"><span data-stu-id="6d7d0-122">See the [Container naming rules](storage/blobs/storage-dotnet-how-to-use-blobs.md#create-a-container) section for a list of rules and restrictions on naming blob containers.</span></span>

   ![Caixa de texto Criar Contêineres de Blob][1]
5. <span data-ttu-id="6d7d0-124">Pressione **Enter** quanto terminar de criar o contêiner de blobs ou **Esc** para cancelar.</span><span class="sxs-lookup"><span data-stu-id="6d7d0-124">Press **Enter** when done to create the blob container, or **Esc** to cancel.</span></span> <span data-ttu-id="6d7d0-125">Após a criação do contêiner de blobs, ele será exibido na pasta **Contêineres de Blob** da conta de armazenamento selecionada.</span><span class="sxs-lookup"><span data-stu-id="6d7d0-125">Once the blob container has been successfully created, it will be displayed under the **Blob Containers** folder for the selected storage account.</span></span>

   ![Contêiner de blob criado][2]

## <a name="view-a-blob-containers-contents"></a><span data-ttu-id="6d7d0-127">Exibir o conteúdo de um contêiner de blobs</span><span class="sxs-lookup"><span data-stu-id="6d7d0-127">View a blob container's contents</span></span>
<span data-ttu-id="6d7d0-128">Os contêineres de blob contêm blobs e pastas (que também podem conter blobs).</span><span class="sxs-lookup"><span data-stu-id="6d7d0-128">Blob containers contain blobs and folders (that can also contain blobs).</span></span>

<span data-ttu-id="6d7d0-129">As etapas a seguir ilustram como exibir o conteúdo de um contêiner de blobs no Gerenciador de Armazenamento (Preview):</span><span class="sxs-lookup"><span data-stu-id="6d7d0-129">The following steps illustrate how to view the contents of a blob container within Storage Explorer (Preview):</span></span>

1. <span data-ttu-id="6d7d0-130">Abra o Gerenciador de Armazenamento (Preview).</span><span class="sxs-lookup"><span data-stu-id="6d7d0-130">Open Storage Explorer (Preview).</span></span>
2. <span data-ttu-id="6d7d0-131">No painel esquerdo, expanda a conta de armazenamento que contém o contêiner de blobs que você deseja exibir.</span><span class="sxs-lookup"><span data-stu-id="6d7d0-131">In the left pane, expand the storage account containing the blob container you wish to view.</span></span>
3. <span data-ttu-id="6d7d0-132">Expanda os **Contêineres de Blob**da conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="6d7d0-132">Expand the storage account's **Blob Containers**.</span></span>
4. <span data-ttu-id="6d7d0-133">Clique com o botão direito no contêiner de blob que você deseja exibir e, no menu de contexto, selecione **Abrir Editor do Contêiner de Blobs**.</span><span class="sxs-lookup"><span data-stu-id="6d7d0-133">Right-click the blob container you wish to view, and - from the context menu - select **Open Blob Container Editor**.</span></span>
   <span data-ttu-id="6d7d0-134">Você também pode clicar duas vezes no contêiner de blobs que deseja exibir.</span><span class="sxs-lookup"><span data-stu-id="6d7d0-134">You can also double-click the blob container you wish to view.</span></span>

   ![Menu de contexto Abrir editor do contêiner de blobs][19]
5. <span data-ttu-id="6d7d0-136">O painel principal exibirá o conteúdo do contêiner de blobs.</span><span class="sxs-lookup"><span data-stu-id="6d7d0-136">The main pane will display the blob container's contents.</span></span>

   ![Editor do Contêiner de blobs][3]

## <a name="delete-a-blob-container"></a><span data-ttu-id="6d7d0-138">Excluir um contêiner de blob</span><span class="sxs-lookup"><span data-stu-id="6d7d0-138">Delete a blob container</span></span>
<span data-ttu-id="6d7d0-139">Os contêineres de blob podem ser facilmente criados e excluídos conforme o necessário.</span><span class="sxs-lookup"><span data-stu-id="6d7d0-139">Blob containers can be easily created and deleted as needed.</span></span> <span data-ttu-id="6d7d0-140">(Para saber como excluir blobs individuais, confira a seção [Gerenciando blobs em um contêiner de blobs](#managing-blobs-in-a-blob-container).)</span><span class="sxs-lookup"><span data-stu-id="6d7d0-140">(To see how to delete individual blobs, refer to the section, [Managing blobs in a blob container](#managing-blobs-in-a-blob-container).)</span></span>

<span data-ttu-id="6d7d0-141">As etapas a seguir ilustram como excluir um contêiner de blobs no Gerenciador de Armazenamento (Preview):</span><span class="sxs-lookup"><span data-stu-id="6d7d0-141">The following steps illustrate how to delete a blob container within Storage Explorer (Preview):</span></span>

1. <span data-ttu-id="6d7d0-142">Abra o Gerenciador de Armazenamento (Preview).</span><span class="sxs-lookup"><span data-stu-id="6d7d0-142">Open Storage Explorer (Preview).</span></span>
2. <span data-ttu-id="6d7d0-143">No painel esquerdo, expanda a conta de armazenamento que contém o contêiner de blobs que você deseja exibir.</span><span class="sxs-lookup"><span data-stu-id="6d7d0-143">In the left pane, expand the storage account containing the blob container you wish to view.</span></span>
3. <span data-ttu-id="6d7d0-144">Expanda os **Contêineres de Blob**da conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="6d7d0-144">Expand the storage account's **Blob Containers**.</span></span>
4. <span data-ttu-id="6d7d0-145">Clique com o botão direito no contêiner de blobs que você deseja excluir e, no menu de contexto, escolha **Excluir**.</span><span class="sxs-lookup"><span data-stu-id="6d7d0-145">Right-click the blob container you wish to delete, and - from the context menu - select **Delete**.</span></span>
   <span data-ttu-id="6d7d0-146">Você também pode pressionar **Excluir** para excluir o contêiner de blobs selecionado atualmente.</span><span class="sxs-lookup"><span data-stu-id="6d7d0-146">You can also press **Delete** to delete the currently selected blob container.</span></span>

   ![Menu de contexto Excluir contêiner de blobs][4]
5. <span data-ttu-id="6d7d0-148">Escolha **Sim** na caixa de diálogo de confirmação.</span><span class="sxs-lookup"><span data-stu-id="6d7d0-148">Select **Yes** to the confirmation dialog.</span></span>

   ![Confirmação de exclusão do contêiner de blobs][5]

## <a name="copy-a-blob-container"></a><span data-ttu-id="6d7d0-150">Copiar um contêiner de blobs</span><span class="sxs-lookup"><span data-stu-id="6d7d0-150">Copy a blob container</span></span>
<span data-ttu-id="6d7d0-151">O Gerenciador de Armazenamento (Preview) permite que você copie um contêiner de blobs na área de transferência e cole esse contêiner de blobs em outra conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="6d7d0-151">Storage Explorer (Preview) enables you to copy a blob container to the clipboard, and then paste that blob container into another storage account.</span></span> <span data-ttu-id="6d7d0-152">(Para saber como copiar blobs individuais, confira a seção [Gerenciando blobs em um contêiner de blobs](#managing-blobs-in-a-blob-container).)</span><span class="sxs-lookup"><span data-stu-id="6d7d0-152">(To see how to copy individual blobs, refer to the section, [Managing blobs in a blob container](#managing-blobs-in-a-blob-container).)</span></span>

<span data-ttu-id="6d7d0-153">As etapas a seguir ilustram como copiar um contêiner de blobs de uma conta de armazenamento para outra.</span><span class="sxs-lookup"><span data-stu-id="6d7d0-153">The following steps illustrate how to copy a blob container from one storage account to another.</span></span>

1. <span data-ttu-id="6d7d0-154">Abra o Gerenciador de Armazenamento (Preview).</span><span class="sxs-lookup"><span data-stu-id="6d7d0-154">Open Storage Explorer (Preview).</span></span>
2. <span data-ttu-id="6d7d0-155">No painel esquerdo, expanda a conta de armazenamento que contém o contêiner de blobs que você deseja copiar.</span><span class="sxs-lookup"><span data-stu-id="6d7d0-155">In the left pane, expand the storage account containing the blob container you wish to copy.</span></span>
3. <span data-ttu-id="6d7d0-156">Expanda os **Contêineres de Blob**da conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="6d7d0-156">Expand the storage account's **Blob Containers**.</span></span>
4. <span data-ttu-id="6d7d0-157">Clique com o botão direito no contêiner de blobs que você deseja copiar e, no menu de contexto, escolha **Copiar Contêiner de Blobs**.</span><span class="sxs-lookup"><span data-stu-id="6d7d0-157">Right-click the blob container you wish to copy, and - from the context menu - select **Copy Blob Container**.</span></span>

   ![Menu de contexto Copiar contêiner de blobs][6]
5. <span data-ttu-id="6d7d0-159">Clique com botão direito na conta de armazenamento de "destino" na qual você deseja colar o contêiner de blobs e, no menu de contexto, escolha **Colar Contêiner de Blobs**.</span><span class="sxs-lookup"><span data-stu-id="6d7d0-159">Right-click the desired "target" storage account into which you want to paste the blob container, and - from the context menu - select **Paste Blob Container**.</span></span>

   ![Menu de contexto Colar contêiner de blobs][7]

## <a name="get-the-sas-for-a-blob-container"></a><span data-ttu-id="6d7d0-161">Obter a SAS para um contêiner de blob</span><span class="sxs-lookup"><span data-stu-id="6d7d0-161">Get the SAS for a blob container</span></span>
<span data-ttu-id="6d7d0-162">Uma [SAS (Assinatura de Acesso Compartilhado)](storage/common/storage-dotnet-shared-access-signature-part-1.md) fornece acesso delegado aos recursos da sua conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="6d7d0-162">A [shared access signature (SAS)](storage/common/storage-dotnet-shared-access-signature-part-1.md) provides delegated access to resources in your storage account.</span></span>
<span data-ttu-id="6d7d0-163">Isso significa que você pode conceder a um cliente permissões limitadas a objetos na sua conta de armazenamento por um período especificado e com um conjunto determinado de permissões, sem precisar compartilhar suas chaves de acesso de conta.</span><span class="sxs-lookup"><span data-stu-id="6d7d0-163">This means that you can grant a client limited permissions to objects in your storage account for a specified period of time and with a specified set of permissions, without having to share your account access keys.</span></span>

<span data-ttu-id="6d7d0-164">As etapas a seguir ilustram como criar uma SAS para um contêiner de blobs:</span><span class="sxs-lookup"><span data-stu-id="6d7d0-164">The following steps illustrate how to create a SAS for a blob container:</span></span>

1. <span data-ttu-id="6d7d0-165">Abra o Gerenciador de Armazenamento (Preview).</span><span class="sxs-lookup"><span data-stu-id="6d7d0-165">Open Storage Explorer (Preview).</span></span>
2. <span data-ttu-id="6d7d0-166">No painel esquerdo, expanda a conta de armazenamento que contém o contêiner de blobs para o qual você deseja obter uma SAS.</span><span class="sxs-lookup"><span data-stu-id="6d7d0-166">In the left pane, expand the storage account containing the blob container for which you wish to get a SAS.</span></span>
3. <span data-ttu-id="6d7d0-167">Expanda os **Contêineres de Blob**da conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="6d7d0-167">Expand the storage account's **Blob Containers**.</span></span>
4. <span data-ttu-id="6d7d0-168">Clique com o botão direito no contêiner de blobs desejado e, no menu de contexto, escolha **Obter Assinatura de Acesso Compartilhado**.</span><span class="sxs-lookup"><span data-stu-id="6d7d0-168">Right-click the desired blob container, and - from the context menu - select **Get Shared Access Signature**.</span></span>

   ![Menu de contexto Obter SAS][8]
5. <span data-ttu-id="6d7d0-170">Na caixa de diálogo **Assinatura de Acesso Compartilhado** , especifique a política, as datas de início e de vencimento, o fuso horário e os níveis de acesso que você deseja para o recurso.</span><span class="sxs-lookup"><span data-stu-id="6d7d0-170">In the **Shared Access Signature** dialog, specify the policy, start and expiration dates, time zone, and access levels you want for the resource.</span></span>

   ![Opções de Obter SAS][9]
6. <span data-ttu-id="6d7d0-172">Ao terminar de especificar as opções de SAS, escolha **Criar**.</span><span class="sxs-lookup"><span data-stu-id="6d7d0-172">When you're finished specifying the SAS options, select **Create**.</span></span>
7. <span data-ttu-id="6d7d0-173">Uma segunda caixa de diálogo de **Assinatura de Acesso Compartilhado** será exibida listando o contêiner de blobs juntamente com a URL e as QueryStrings que você pode usar para acessar o recurso de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="6d7d0-173">A second **Shared Access Signature** dialog will then display that lists the blob container along with the URL and QueryStrings you can use to access the storage resource.</span></span>
   <span data-ttu-id="6d7d0-174">Escolha **Copiar** próximo à URL que você deseja copiar na área de transferência.</span><span class="sxs-lookup"><span data-stu-id="6d7d0-174">Select **Copy** next to the URL you wish to copy to the clipboard.</span></span>

   ![Copiar URLs de SAS][10]
8. <span data-ttu-id="6d7d0-176">Ao terminar, escolha **Fechar**.</span><span class="sxs-lookup"><span data-stu-id="6d7d0-176">When done, select **Close**.</span></span>

## <a name="manage-access-policies-for-a-blob-container"></a><span data-ttu-id="6d7d0-177">Gerenciar políticas de acesso para um contêiner de blobs</span><span class="sxs-lookup"><span data-stu-id="6d7d0-177">Manage Access Policies for a blob container</span></span>
<span data-ttu-id="6d7d0-178">As etapas a seguir ilustram como gerenciar (adicionar e remover) políticas de acesso para um contêiner de blobs:</span><span class="sxs-lookup"><span data-stu-id="6d7d0-178">The following steps illustrate how to manage (add and remove) access policies for a blob container:</span></span>

1. <span data-ttu-id="6d7d0-179">Abra o Gerenciador de Armazenamento (Preview).</span><span class="sxs-lookup"><span data-stu-id="6d7d0-179">Open Storage Explorer (Preview).</span></span>
2. <span data-ttu-id="6d7d0-180">No painel esquerdo, expanda a conta de armazenamento que contém o contêiner de blobs cujas políticas de acesso você deseja gerenciar.</span><span class="sxs-lookup"><span data-stu-id="6d7d0-180">In the left pane, expand the storage account containing the blob container whose access policies you wish to manage.</span></span>
3. <span data-ttu-id="6d7d0-181">Expanda os **Contêineres de Blob**da conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="6d7d0-181">Expand the storage account's **Blob Containers**.</span></span>
4. <span data-ttu-id="6d7d0-182">Escolha o contêiner de blobs desejado e, no menu de contexto, escolha **Gerenciar Políticas de Acesso**.</span><span class="sxs-lookup"><span data-stu-id="6d7d0-182">Select the desired blob container, and - from the context menu - select **Manage Access Policies**.</span></span>

   ![Menu de contexto Gerenciar políticas de acesso][11]
5. <span data-ttu-id="6d7d0-184">A caixa de diálogo **Políticas de Acesso** listará todas as políticas de acesso que já foram criadas para o contêiner de blobs selecionado.</span><span class="sxs-lookup"><span data-stu-id="6d7d0-184">The **Access Policies** dialog will list any access policies already created for the selected blob container.</span></span>

   ![Opções de Política de Acesso][12]        
6. <span data-ttu-id="6d7d0-186">Execute estas etapas, dependendo da tarefa de gerenciamento de política de acesso:</span><span class="sxs-lookup"><span data-stu-id="6d7d0-186">Follow these steps depending on the access policy management task:</span></span>

   * <span data-ttu-id="6d7d0-187">**Adicionar uma nova política de acesso** — escolha **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="6d7d0-187">**Add a new access policy** - Select **Add**.</span></span> <span data-ttu-id="6d7d0-188">Uma vez gerada, a caixa de diálogo **Políticas de Acesso** exibirá a política de acesso recém-adicionada (com configurações padrão).</span><span class="sxs-lookup"><span data-stu-id="6d7d0-188">Once generated, the **Access Policies** dialog will display the newly added access policy (with default settings).</span></span>
   * <span data-ttu-id="6d7d0-189">**Editar uma política de acesso** — faça as edições desejadas e escolha **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="6d7d0-189">**Edit an access policy** -  Make any desired edits, and select **Save**.</span></span>
   * <span data-ttu-id="6d7d0-190">**Remover uma política de acesso** — escolha **Remover** ao lado da política de acesso que você deseja remover.</span><span class="sxs-lookup"><span data-stu-id="6d7d0-190">**Remove an access policy** - Select **Remove** next to the access policy you wish to remove.</span></span>

## <a name="set-the-public-access-level-for-a-blob-container"></a><span data-ttu-id="6d7d0-191">Definir o nível de acesso público para um contêiner de blobs</span><span class="sxs-lookup"><span data-stu-id="6d7d0-191">Set the Public Access Level for a blob container</span></span>
<span data-ttu-id="6d7d0-192">Por padrão, cada contêiner de blobs é definido como "Sem acesso público".</span><span class="sxs-lookup"><span data-stu-id="6d7d0-192">By default, every blob container is set to "No public access".</span></span>

<span data-ttu-id="6d7d0-193">As etapas a seguir ilustram como especificar um nível de acesso público para um contêiner de blobs.</span><span class="sxs-lookup"><span data-stu-id="6d7d0-193">The following steps illustrate how to specify a public access level for a blob container.</span></span>

1. <span data-ttu-id="6d7d0-194">Abra o Gerenciador de Armazenamento (Preview).</span><span class="sxs-lookup"><span data-stu-id="6d7d0-194">Open Storage Explorer (Preview).</span></span>
2. <span data-ttu-id="6d7d0-195">No painel esquerdo, expanda a conta de armazenamento que contém o contêiner de blobs cujas políticas de acesso você deseja gerenciar.</span><span class="sxs-lookup"><span data-stu-id="6d7d0-195">In the left pane, expand the storage account containing the blob container whose access policies you wish to manage.</span></span>
3. <span data-ttu-id="6d7d0-196">Expanda os **Contêineres de Blob**da conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="6d7d0-196">Expand the storage account's **Blob Containers**.</span></span>
4. <span data-ttu-id="6d7d0-197">Escolha o contêiner de blobs desejado e, no menu de contexto, escolha **Definir o Nível de Acesso Público**.</span><span class="sxs-lookup"><span data-stu-id="6d7d0-197">Select the desired blob container, and - from the context menu - select **Set Public Access Level**.</span></span>

   ![Menu de contexto Definir nível de acesso público][13]
5. <span data-ttu-id="6d7d0-199">Na caixa de diálogo **Definir o Nível de Acesso Público do Contêiner** , especifique o nível de acesso desejado.</span><span class="sxs-lookup"><span data-stu-id="6d7d0-199">In the **Set Container Public Access Level** dialog, specify the desired access level.</span></span>

   ![Opções de Definir nível de acesso público][14]
6. <span data-ttu-id="6d7d0-201">Escolha **Aplicar**.</span><span class="sxs-lookup"><span data-stu-id="6d7d0-201">Select **Apply**.</span></span>

## <a name="managing-blobs-in-a-blob-container"></a><span data-ttu-id="6d7d0-202">Gerenciamento de blobs em um contêiner de blobs</span><span class="sxs-lookup"><span data-stu-id="6d7d0-202">Managing blobs in a blob container</span></span>
<span data-ttu-id="6d7d0-203">Depois de criar um contêiner de blob, você pode carregar um blob nesse contêiner de blob, baixar um blob em seu computador local, abrir um blob em seu computador local e muito mais.</span><span class="sxs-lookup"><span data-stu-id="6d7d0-203">Once you've created a blob container, you can upload a blob to that blob container, download a blob to your local computer, open a blob on your local computer, and much more.</span></span>

<span data-ttu-id="6d7d0-204">As etapas a seguir ilustram como gerenciar os blobs (e pastas) dentro de um contêiner de blobs.</span><span class="sxs-lookup"><span data-stu-id="6d7d0-204">The following steps illustrate how to manage the blobs (and folders) within a blob container.</span></span>

1. <span data-ttu-id="6d7d0-205">Abra o Gerenciador de Armazenamento (Preview).</span><span class="sxs-lookup"><span data-stu-id="6d7d0-205">Open Storage Explorer (Preview).</span></span>
2. <span data-ttu-id="6d7d0-206">No painel esquerdo, expanda a conta de armazenamento que contém o contêiner de blobs que você deseja gerenciar.</span><span class="sxs-lookup"><span data-stu-id="6d7d0-206">In the left pane, expand the storage account containing the blob container you wish to manage.</span></span>
3. <span data-ttu-id="6d7d0-207">Expanda os **Contêineres de Blob**da conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="6d7d0-207">Expand the storage account's **Blob Containers**.</span></span>
4. <span data-ttu-id="6d7d0-208">Clique duas vezes no contêiner de blobs que você deseja exibir.</span><span class="sxs-lookup"><span data-stu-id="6d7d0-208">Double-click the blob container you wish to view.</span></span>
5. <span data-ttu-id="6d7d0-209">O painel principal exibirá o conteúdo do contêiner de blobs.</span><span class="sxs-lookup"><span data-stu-id="6d7d0-209">The main pane will display the blob container's contents.</span></span>

   ![Exibir contêiner de blobs][3]
6. <span data-ttu-id="6d7d0-211">O painel principal exibirá o conteúdo do contêiner de blobs.</span><span class="sxs-lookup"><span data-stu-id="6d7d0-211">The main pane will display the blob container's contents.</span></span>
7. <span data-ttu-id="6d7d0-212">Execute estas etapas, dependendo da tarefa que deseja executar:</span><span class="sxs-lookup"><span data-stu-id="6d7d0-212">Follow these steps depending on the task you wish to perform:</span></span>

   * <span data-ttu-id="6d7d0-213">**Carregar arquivos em um contêiner de blobs**</span><span class="sxs-lookup"><span data-stu-id="6d7d0-213">**Upload files to a blob container**</span></span>

     1. <span data-ttu-id="6d7d0-214">Na barra de ferramentas do painel principal, escolha **Carregar** e **Carregar Arquivos** no menu suspenso.</span><span class="sxs-lookup"><span data-stu-id="6d7d0-214">On the main pane's toolbar, select **Upload**, and then **Upload Files** from the drop-down menu.</span></span>

        ![Menu Carregar arquivos][15]
     2. <span data-ttu-id="6d7d0-216">Na caixa de diálogo **Carregar arquivos**, escolha o botão de reticências (**...**) no lado direito da caixa de texto **Arquivos** para selecionar os arquivos que você deseja carregar.</span><span class="sxs-lookup"><span data-stu-id="6d7d0-216">In the **Upload files** dialog, select the ellipsis (**…**) button on the right side of the **Files** text box to select the file(s) you wish to upload.</span></span>

        ![Opções de Carregar arquivos][16]
     3. <span data-ttu-id="6d7d0-218">Especifique o tipo de **Tipo de blob**.</span><span class="sxs-lookup"><span data-stu-id="6d7d0-218">Specify the type of **Blob type**.</span></span> <span data-ttu-id="6d7d0-219">O artigo [Introdução ao Armazenamento de Blobs do Azure usando o .NET](storage/blobs/storage-dotnet-how-to-use-blobs.md#blob-service-concepts) explica as diferenças entre os vários tipos de blob.</span><span class="sxs-lookup"><span data-stu-id="6d7d0-219">The article [Get started with Azure Blob storage using .NET](storage/blobs/storage-dotnet-how-to-use-blobs.md#blob-service-concepts) explains the differences between the various blob types.</span></span>
     4. <span data-ttu-id="6d7d0-220">Como opção, especifique uma pasta de destino na qual os arquivos selecionados serão carregados.</span><span class="sxs-lookup"><span data-stu-id="6d7d0-220">Optionally, specify a target folder into which the selected file(s) will be uploaded.</span></span> <span data-ttu-id="6d7d0-221">Se a pasta de destino não existir, ela será criada.</span><span class="sxs-lookup"><span data-stu-id="6d7d0-221">If the target folder doesn’t exist, it will be created.</span></span>
     5. <span data-ttu-id="6d7d0-222">Escolha **Carregar**.</span><span class="sxs-lookup"><span data-stu-id="6d7d0-222">Select **Upload**.</span></span>
   * <span data-ttu-id="6d7d0-223">**Carregar uma pasta em um contêiner de blobs**</span><span class="sxs-lookup"><span data-stu-id="6d7d0-223">**Upload a folder to a blob container**</span></span>

     1. <span data-ttu-id="6d7d0-224">Na barra de ferramentas do painel principal, escolha **Carregar** e **Carregar Pasta** no menu suspenso.</span><span class="sxs-lookup"><span data-stu-id="6d7d0-224">On the main pane's toolbar, select **Upload**, and then **Upload Folder** from the drop-down menu.</span></span>

        ![Menu Carregar pasta][17]
     2. <span data-ttu-id="6d7d0-226">Na caixa de diálogo **Carregar pasta**, escolha o botão de reticências (**...**) no lado direito da caixa de texto **Pasta** para selecionar a pasta cujo conteúdo você deseja carregar.</span><span class="sxs-lookup"><span data-stu-id="6d7d0-226">In the **Upload folder** dialog, select the ellipsis (**…**) button on the right side of the **Folder** text box to select the folder whose contents you wish to upload.</span></span>

        ![Opções de Carregar pasta][18]
     3. <span data-ttu-id="6d7d0-228">Especifique o tipo de **Tipo de blob**.</span><span class="sxs-lookup"><span data-stu-id="6d7d0-228">Specify the type of **Blob type**.</span></span> <span data-ttu-id="6d7d0-229">O artigo [Introdução ao Armazenamento de Blobs do Azure usando o .NET](storage/blobs/storage-dotnet-how-to-use-blobs.md#blob-service-concepts) explica as diferenças entre os vários tipos de blob.</span><span class="sxs-lookup"><span data-stu-id="6d7d0-229">The article [Get started with Azure Blob storage using .NET](storage/blobs/storage-dotnet-how-to-use-blobs.md#blob-service-concepts) explains the differences between the various blob types.</span></span>
     4. <span data-ttu-id="6d7d0-230">Como opção, especifique uma pasta de destino na qual o conteúdo da pasta selecionada será carregado.</span><span class="sxs-lookup"><span data-stu-id="6d7d0-230">Optionally, specify a target folder into which the selected folder's contents will be uploaded.</span></span> <span data-ttu-id="6d7d0-231">Se a pasta de destino não existir, ela será criada.</span><span class="sxs-lookup"><span data-stu-id="6d7d0-231">If the target folder doesn’t exist, it will be created.</span></span>
     5. <span data-ttu-id="6d7d0-232">Escolha **Carregar**.</span><span class="sxs-lookup"><span data-stu-id="6d7d0-232">Select **Upload**.</span></span>
   * <span data-ttu-id="6d7d0-233">**Baixar um blob em seu computador local**</span><span class="sxs-lookup"><span data-stu-id="6d7d0-233">**Download a blob to your local computer**</span></span>

     1. <span data-ttu-id="6d7d0-234">Selecione o blob que você deseja baixar.</span><span class="sxs-lookup"><span data-stu-id="6d7d0-234">Select the blob you wish to download.</span></span>
     2. <span data-ttu-id="6d7d0-235">Na barra de ferramentas do painel principal, escolha **Baixar**.</span><span class="sxs-lookup"><span data-stu-id="6d7d0-235">On the main pane's toolbar, select **Download**.</span></span>
     3. <span data-ttu-id="6d7d0-236">Na caixa de diálogo **Especifique onde salvar o blob baixado** , especifique o local onde você deseja baixar o blob, e o nome que deseja dar a ele.</span><span class="sxs-lookup"><span data-stu-id="6d7d0-236">In the **Specify where to save the downloaded blob** dialog, specify the location where you want the blob downloaded, and the name you wish to give it.</span></span>  
     4. <span data-ttu-id="6d7d0-237">Selecione **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="6d7d0-237">Select **Save**.</span></span>
   * <span data-ttu-id="6d7d0-238">**Abrir um blob em seu computador local**</span><span class="sxs-lookup"><span data-stu-id="6d7d0-238">**Open a blob on your local computer**</span></span>

     1. <span data-ttu-id="6d7d0-239">Selecione o blob que você deseja abrir.</span><span class="sxs-lookup"><span data-stu-id="6d7d0-239">Select the blob you wish to open.</span></span>
     2. <span data-ttu-id="6d7d0-240">Na barra de ferramentas do painel principal, escolha **Abrir**.</span><span class="sxs-lookup"><span data-stu-id="6d7d0-240">On the main pane's toolbar, select **Open**.</span></span>
     3. <span data-ttu-id="6d7d0-241">O blob será baixado e aberto usando o aplicativo associado ao tipo de arquivo subjacente do blob.</span><span class="sxs-lookup"><span data-stu-id="6d7d0-241">The blob will be downloaded and opened using the application associated with the blob's underlying file type.</span></span>
   * <span data-ttu-id="6d7d0-242">**Copiar um blob na área de transferência**</span><span class="sxs-lookup"><span data-stu-id="6d7d0-242">**Copy a blob to the clipboard**</span></span>

     1. <span data-ttu-id="6d7d0-243">Escolha o blob que você deseja copiar.</span><span class="sxs-lookup"><span data-stu-id="6d7d0-243">Select the blob you wish to copy.</span></span>
     2. <span data-ttu-id="6d7d0-244">Na barra de ferramentas do painel principal, escolha **Copiar**.</span><span class="sxs-lookup"><span data-stu-id="6d7d0-244">On the main pane's toolbar, select **Copy**.</span></span>
     3. <span data-ttu-id="6d7d0-245">No painel esquerdo, navegue até outro contêiner de blobs e clique duas vezes nele para exibi-lo no painel principal.</span><span class="sxs-lookup"><span data-stu-id="6d7d0-245">In the left pane, navigate to another blob container, and double-click it to view it in the main pane.</span></span>
     4. <span data-ttu-id="6d7d0-246">Na barra de ferramentas do painel principal, escolha **Colar** para criar uma cópia do blob.</span><span class="sxs-lookup"><span data-stu-id="6d7d0-246">On the main pane's toolbar, select **Paste** to create a copy of the blob.</span></span>
   * <span data-ttu-id="6d7d0-247">**Excluir um blob**</span><span class="sxs-lookup"><span data-stu-id="6d7d0-247">**Delete a blob**</span></span>

     1. <span data-ttu-id="6d7d0-248">Selecione o blob que você deseja excluir.</span><span class="sxs-lookup"><span data-stu-id="6d7d0-248">Select the blob you wish to delete.</span></span>
     2. <span data-ttu-id="6d7d0-249">Na barra de ferramentas do painel principal, escolha **Excluir**.</span><span class="sxs-lookup"><span data-stu-id="6d7d0-249">On the main pane's toolbar, select **Delete**.</span></span>
     3. <span data-ttu-id="6d7d0-250">Escolha **Sim** na caixa de diálogo de confirmação.</span><span class="sxs-lookup"><span data-stu-id="6d7d0-250">Select **Yes** to the confirmation dialog.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6d7d0-251">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="6d7d0-251">Next steps</span></span>
* <span data-ttu-id="6d7d0-252">Veja as [Notas de versão e vídeos mais recentes do Gerenciador de Armazenamento (Preview)](http://www.storageexplorer.com).</span><span class="sxs-lookup"><span data-stu-id="6d7d0-252">View the [latest Storage Explorer (Preview) release notes and videos](http://www.storageexplorer.com).</span></span>
* <span data-ttu-id="6d7d0-253">Saiba como [criar aplicativos usando os blobs, tabelas, filas e arquivos do Azure](https://azure.microsoft.com/documentation/services/storage/).</span><span class="sxs-lookup"><span data-stu-id="6d7d0-253">Learn how to [create applications using Azure blobs, tables, queues, and files](https://azure.microsoft.com/documentation/services/storage/).</span></span>

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
