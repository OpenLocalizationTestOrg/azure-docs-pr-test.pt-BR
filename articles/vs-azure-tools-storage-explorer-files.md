---
title: "aaaUsing Gerenciador de armazenamento (visualização) com o armazenamento de arquivo do Azure | Microsoft Docs"
description: "Saiba como aprender como toouse toowork de Gerenciador de armazenamento (visualização) com o arquivo de compartilhamentos e arquivos."
services: storage
documentationcenter: na
author: cawaMS
manager: paulyuk
editor: 
ms.assetid: 
ms.service: storage
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/09/2017
ms.author: cawa
ms.openlocfilehash: 98eb3cde711ae3dbfdb6ffaec23ae24f822370e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="using-storage-explorer-preview-with-azure-file-storage"></a><span data-ttu-id="99e42-103">Usando o Gerenciador de Armazenamento (Visualização) com o Armazenamento de Arquivos do Azure</span><span class="sxs-lookup"><span data-stu-id="99e42-103">Using Storage Explorer (Preview) with Azure File storage</span></span>

<span data-ttu-id="99e42-104">Arquivo do Azure, o armazenamento é um serviço que oferece arquivo compartilha Olá nuvem usando Olá protocolo padrão do bloco de mensagens de servidor (SMB).</span><span class="sxs-lookup"><span data-stu-id="99e42-104">Azure File storage is a service that offers file shares in hello cloud using hello standard Server Message Block (SMB) Protocol.</span></span> <span data-ttu-id="99e42-105">Há suporte ao SMB 2.1 e ao 3.0 SMB.</span><span class="sxs-lookup"><span data-stu-id="99e42-105">Both SMB 2.1 and SMB 3.0 are supported.</span></span> <span data-ttu-id="99e42-106">Com o armazenamento de arquivo do Azure, você pode migrar aplicativos herdados que dependem de tooAzure de compartilhamentos de arquivo rapidamente e sem regravações caras.</span><span class="sxs-lookup"><span data-stu-id="99e42-106">With Azure File storage, you can migrate legacy applications that rely on file shares tooAzure quickly and without costly rewrites.</span></span> <span data-ttu-id="99e42-107">Você pode usar dados do arquivo armazenamento tooexpose publicamente toohello mundo ou toostore dados de aplicativo em particular.</span><span class="sxs-lookup"><span data-stu-id="99e42-107">You can use File storage tooexpose data publicly toohello world, or toostore application data privately.</span></span> <span data-ttu-id="99e42-108">Neste artigo, você aprenderá como toouse toowork de Gerenciador de armazenamento (visualização) com o arquivo de compartilhamentos e arquivos.</span><span class="sxs-lookup"><span data-stu-id="99e42-108">In this article, you'll learn how toouse Storage Explorer (Preview) toowork with file shares and files.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="99e42-109">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="99e42-109">Prerequisites</span></span>

<span data-ttu-id="99e42-110">toocomplete Olá etapas neste artigo, você precisará seguir hello:</span><span class="sxs-lookup"><span data-stu-id="99e42-110">toocomplete hello steps in this article, you'll need hello following:</span></span>

- [<span data-ttu-id="99e42-111">Baixe e instale o Gerenciador de Armazenamento (preview)</span><span class="sxs-lookup"><span data-stu-id="99e42-111">Download and install Storage Explorer (preview)</span></span>](http://www.storageexplorer.com/)

- [<span data-ttu-id="99e42-112">Conecte-se a conta de armazenamento do Azure tooa ou serviço</span><span class="sxs-lookup"><span data-stu-id="99e42-112">Connect tooa Azure storage account or service</span></span>](https://docs.microsoft.com//azure/vs-azure-tools-storage-manage-with-storage-explorer#connect-to-a-storage-account-or-service)

## <a name="create-a-file-share"></a><span data-ttu-id="99e42-113">Criar um compartilhamento de arquivos</span><span class="sxs-lookup"><span data-stu-id="99e42-113">Create a File Share</span></span>

<span data-ttu-id="99e42-114">Todos os arquivos devem residir em um compartilhamento de arquivos, que é simplesmente um agrupamento lógico de arquivos.</span><span class="sxs-lookup"><span data-stu-id="99e42-114">All files must reside in a file share, which is simply a logical grouping of files.</span></span> <span data-ttu-id="99e42-115">Uma conta pode conter um número ilimitado de compartilhamentos de arquivo, e cada compartilhamento pode armazenar um número ilimitado de arquivos.</span><span class="sxs-lookup"><span data-stu-id="99e42-115">An account can contain an unlimited number of file shares, and each share can store an unlimited number of files.</span></span>

<span data-ttu-id="99e42-116">Olá, as etapas a seguir ilustra como toocreate um compartilhamento de arquivo no Gerenciador de armazenamento (visualização).</span><span class="sxs-lookup"><span data-stu-id="99e42-116">hello following steps illustrate how toocreate a file share within Storage Explorer (Preview).</span></span>

1. <span data-ttu-id="99e42-117">Abra o Gerenciador de Armazenamento (Preview).</span><span class="sxs-lookup"><span data-stu-id="99e42-117">Open Storage Explorer (Preview).</span></span>

2. <span data-ttu-id="99e42-118">No painel esquerdo do hello, expanda a conta de armazenamento hello dentro da qual você deseja toocreate Olá compartilhamento de arquivos</span><span class="sxs-lookup"><span data-stu-id="99e42-118">In hello left pane, expand hello storage account within which you wish toocreate hello File Share</span></span>

3. <span data-ttu-id="99e42-119">Clique com botão direito **compartilhamentos de arquivos**e - no menu de contexto Olá - selecione **criar compartilhamento de arquivos**.</span><span class="sxs-lookup"><span data-stu-id="99e42-119">Right-click **File Shares**, and - from hello context menu - select **Create File Share**.</span></span>

    ![Criar o compartilhamento de arquivos](media/vs-azure-tools-storage-explorer-files/image1.png)

4. <span data-ttu-id="99e42-121">Será exibida uma caixa de texto abaixo Olá **compartilhamentos de arquivos** pasta.</span><span class="sxs-lookup"><span data-stu-id="99e42-121">A text box will appear below hello **File Shares** folder.</span></span> <span data-ttu-id="99e42-122">Insira o nome de saudação para o compartilhamento de arquivos.</span><span class="sxs-lookup"><span data-stu-id="99e42-122">Enter hello name for your file share.</span></span> <span data-ttu-id="99e42-123">Consulte Olá [compartilhar as regras de nomenclatura](https://docs.microsoft.com//azure/storage/storage-dotnet-how-to-use-blobs#create-a-container) seção para obter uma lista de regras e restrições de nomenclatura de compartilhamentos de arquivos.</span><span class="sxs-lookup"><span data-stu-id="99e42-123">See hello [Share naming rules](https://docs.microsoft.com//azure/storage/storage-dotnet-how-to-use-blobs#create-a-container) section for a list of rules and restrictions on naming file shares.</span></span>

    ![Compartilhamento de saudação de nomenclatura](media/vs-azure-tools-storage-explorer-files/image2.png)

5. <span data-ttu-id="99e42-125">Pressione **Enter** quando concluído toocreate Olá compartilhamento de arquivos, ou **Esc** toocancel.</span><span class="sxs-lookup"><span data-stu-id="99e42-125">Press **Enter** when done toocreate hello file share, or **Esc** toocancel.</span></span> <span data-ttu-id="99e42-126">Depois que o compartilhamento de arquivo hello foi criado com êxito, ele será exibido em Olá **compartilhamentos de arquivos** pasta para Olá selecionada a conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="99e42-126">Once hello file share has been successfully created, it will be displayed under hello **File Shares** folder for hello selected storage account.</span></span>

    ![novo compartilhamento de saudação](media/vs-azure-tools-storage-explorer-files/image3.png)

## <a name="view-a-file-shares-contents"></a><span data-ttu-id="99e42-128">Exibir o conteúdo de um compartilhamento de arquivos</span><span class="sxs-lookup"><span data-stu-id="99e42-128">View a file share's contents</span></span>

<span data-ttu-id="99e42-129">Compartilhamentos de arquivos contêm arquivos e pastas (que também podem conter arquivos).</span><span class="sxs-lookup"><span data-stu-id="99e42-129">File shares contain files and folders (that can also contain files).</span></span>

<span data-ttu-id="99e42-130">Olá etapas a seguir ilustram como tooview Olá conteúdo de um arquivo de compartilhamento de dentro do Gerenciador de armazenamento (visualização): +</span><span class="sxs-lookup"><span data-stu-id="99e42-130">hello following steps illustrate how tooview hello contents of a file share within Storage Explorer (Preview):+</span></span>

1. <span data-ttu-id="99e42-131">Abra o Gerenciador de Armazenamento (Preview).</span><span class="sxs-lookup"><span data-stu-id="99e42-131">Open Storage Explorer (Preview).</span></span>

2. <span data-ttu-id="99e42-132">No painel esquerdo do hello, expanda a conta de armazenamento de saudação contendo o compartilhamento de arquivo hello desejar tooview.</span><span class="sxs-lookup"><span data-stu-id="99e42-132">In hello left pane, expand hello storage account containing hello file share you wish tooview.</span></span>

3. <span data-ttu-id="99e42-133">Expanda a conta de armazenamento Olá **compartilhamentos de arquivos**.</span><span class="sxs-lookup"><span data-stu-id="99e42-133">Expand hello storage account's **File Shares**.</span></span>

4. <span data-ttu-id="99e42-134">Compartilhamento de arquivos com o botão direito Olá seu gosto tooview e - no menu de contexto Olá - selecione **abrir**.</span><span class="sxs-lookup"><span data-stu-id="99e42-134">Right-click hello file share you wish tooview, and - from hello context menu - select **Open**.</span></span> <span data-ttu-id="99e42-135">Você também pode clicar duas vezes desejar tooview de compartilhamento de arquivo hello.</span><span class="sxs-lookup"><span data-stu-id="99e42-135">You can also double-click hello file share you wish tooview.</span></span>

    ![Abrir compartilhamento](media/vs-azure-tools-storage-explorer-files/image4.png)

5. <span data-ttu-id="99e42-137">painel principal Olá exibirá o conteúdo do compartilhamento de arquivo hello.</span><span class="sxs-lookup"><span data-stu-id="99e42-137">hello main pane will display hello file share's contents.</span></span>
    
    ![Olá conteúdo do compartilhamento](media/vs-azure-tools-storage-explorer-files/image5.png)

## <a name="delete-a-file-share"></a><span data-ttu-id="99e42-139">Excluir um compartilhamento de arquivos</span><span class="sxs-lookup"><span data-stu-id="99e42-139">Delete a file share</span></span>

<span data-ttu-id="99e42-140">Os compartilhamentos de arquivos podem ser criados e excluídos facilmente conforme a necessidade.</span><span class="sxs-lookup"><span data-stu-id="99e42-140">File shares can be easily created and deleted as needed.</span></span> <span data-ttu-id="99e42-141">(toosee como toodelete de arquivos individuais, consulte a seção toohello, [gerenciar arquivos em um compartilhamento de arquivo](https://docs.microsoft.com//azure/vs-azure-tools-storage-explorer-blobs#managing-blobs-in-a-blob-container).)</span><span class="sxs-lookup"><span data-stu-id="99e42-141">(toosee how toodelete individual files, refer toohello section, [Managing files in a file share](https://docs.microsoft.com//azure/vs-azure-tools-storage-explorer-blobs#managing-blobs-in-a-blob-container).)</span></span>

<span data-ttu-id="99e42-142">Olá, as etapas a seguir ilustra como toodelete um compartilhamento de arquivo no Gerenciador de armazenamento (visualização):</span><span class="sxs-lookup"><span data-stu-id="99e42-142">hello following steps illustrate how toodelete a file share within Storage Explorer (Preview):</span></span>

1. <span data-ttu-id="99e42-143">Abra o Gerenciador de Armazenamento (Preview).</span><span class="sxs-lookup"><span data-stu-id="99e42-143">Open Storage Explorer (Preview).</span></span>

2. <span data-ttu-id="99e42-144">No painel esquerdo do hello, expanda a conta de armazenamento de saudação contendo o compartilhamento de arquivo hello desejar tooview.</span><span class="sxs-lookup"><span data-stu-id="99e42-144">In hello left pane, expand hello storage account containing hello file share you wish tooview.</span></span>

3. <span data-ttu-id="99e42-145">Expanda a conta de armazenamento Olá **compartilhamentos de arquivos**.</span><span class="sxs-lookup"><span data-stu-id="99e42-145">Expand hello storage account's **File Shares**.</span></span>

4. <span data-ttu-id="99e42-146">Compartilhamento de arquivos com o botão direito Olá seu gosto toodelete e - no menu de contexto Olá - selecione **excluir**.</span><span class="sxs-lookup"><span data-stu-id="99e42-146">Right-click hello file share you wish toodelete, and - from hello context menu - select **Delete**.</span></span> <span data-ttu-id="99e42-147">Você também pode pressionar **excluir** compartilhamento de arquivo atualmente selecionado Olá toodelete.</span><span class="sxs-lookup"><span data-stu-id="99e42-147">You can also press **Delete** toodelete hello currently selected file share.</span></span>

    ![Exclusão](media/vs-azure-tools-storage-explorer-files/image6.png)

5. <span data-ttu-id="99e42-149">Selecione **Sim** toohello caixa de diálogo de confirmação.</span><span class="sxs-lookup"><span data-stu-id="99e42-149">Select **Yes** toohello confirmation dialog.</span></span>
    
    ![Diálogo de confirmação](media/vs-azure-tools-storage-explorer-files/image7.png)

## <a name="copy-a-file-share"></a><span data-ttu-id="99e42-151">Copiar um compartilhamento de arquivos</span><span class="sxs-lookup"><span data-stu-id="99e42-151">Copy a file share</span></span>

<span data-ttu-id="99e42-152">O Gerenciador de armazenamento (visualização) permite que você toocopy uma área de transferência de toohello de compartilhamento de arquivo e, em seguida, cole o compartilhamento de arquivos em outra conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="99e42-152">Storage Explorer (Preview) enables you toocopy a file share toohello clipboard, and then paste that file share into another storage account.</span></span> <span data-ttu-id="99e42-153">(toosee como toocopy de arquivos individuais, consulte a seção toohello, [gerenciar arquivos em um compartilhamento de arquivo](https://docs.microsoft.com//azure/vs-azure-tools-storage-explorer-blobs#managing-blobs-in-a-blob-container).)</span><span class="sxs-lookup"><span data-stu-id="99e42-153">(toosee how toocopy individual files, refer toohello section, [Managing files in a file share](https://docs.microsoft.com//azure/vs-azure-tools-storage-explorer-blobs#managing-blobs-in-a-blob-container).)</span></span>

<span data-ttu-id="99e42-154">Olá, as etapas a seguir ilustra como toocopy um arquivo de compartilhamento de um tooanother de conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="99e42-154">hello following steps illustrate how toocopy a file share from one storage account tooanother.</span></span>

1. <span data-ttu-id="99e42-155">Abra o Gerenciador de Armazenamento (Preview).</span><span class="sxs-lookup"><span data-stu-id="99e42-155">Open Storage Explorer (Preview).</span></span>

2. <span data-ttu-id="99e42-156">No painel esquerdo do hello, expanda a conta de armazenamento de saudação contendo o compartilhamento de arquivo hello desejar toocopy.</span><span class="sxs-lookup"><span data-stu-id="99e42-156">In hello left pane, expand hello storage account containing hello file share you wish toocopy.</span></span>

3. <span data-ttu-id="99e42-157">Expanda a conta de armazenamento Olá **compartilhamentos de arquivos**.</span><span class="sxs-lookup"><span data-stu-id="99e42-157">Expand hello storage account's **File Shares**.</span></span>

4. <span data-ttu-id="99e42-158">Compartilhamento de arquivos com o botão direito Olá seu gosto toocopy e - no menu de contexto Olá - selecione **compartilhamento de arquivo de cópia**.</span><span class="sxs-lookup"><span data-stu-id="99e42-158">Right-click hello file share you wish toocopy, and - from hello context menu - select **Copy File Share**.</span></span>

    ![Copiar o compartilhamento de arquivos](media/vs-azure-tools-storage-explorer-files/image8.png)

5. <span data-ttu-id="99e42-160">Clique em destino"hello desejado" conta de armazenamento no qual você deseja compartilhamento de arquivo hello toopaste e - no menu de contexto Olá - selecione **de compartilhamento de arquivo colar**.</span><span class="sxs-lookup"><span data-stu-id="99e42-160">Right-click hello desired "target" storage account into which you want toopaste hello file share, and - from hello context menu - select **Paste File Share**.</span></span>

    ![Colar o compartilhamento de arquivos](media/vs-azure-tools-storage-explorer-files/image9.png)

## <a name="get-hello-sas-for-a-file-share"></a><span data-ttu-id="99e42-162">Obter Olá SAS para um compartilhamento de arquivos</span><span class="sxs-lookup"><span data-stu-id="99e42-162">Get hello SAS for a file share</span></span>

<span data-ttu-id="99e42-163">Um [assinatura de acesso compartilhado (SAS)](https://docs.microsoft.com//azure/storage/storage-dotnet-shared-access-signature-part-1) fornece acesso delegado tooresources na sua conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="99e42-163">A [shared access signature (SAS)](https://docs.microsoft.com//azure/storage/storage-dotnet-shared-access-signature-part-1) provides delegated access tooresources in your storage account.</span></span> <span data-ttu-id="99e42-164">Isso significa que você pode conceder a que um cliente limitado tooobjects permissões na conta de armazenamento para um determinado período de tempo e com um conjunto especificado de permissões, sem ter que tooshare suas chaves de acesso da conta.</span><span class="sxs-lookup"><span data-stu-id="99e42-164">This means that you can grant a client limited permissions tooobjects in your storage account for a specified period of time and with a specified set of permissions, without having tooshare your account access keys.</span></span>

<span data-ttu-id="99e42-165">Olá etapas a seguir ilustram como toocreate um SAS para um arquivo de compartilhar: +</span><span class="sxs-lookup"><span data-stu-id="99e42-165">hello following steps illustrate how toocreate a SAS for a file share:+</span></span>

1. <span data-ttu-id="99e42-166">Abra o Gerenciador de Armazenamento (Preview).</span><span class="sxs-lookup"><span data-stu-id="99e42-166">Open Storage Explorer (Preview).</span></span>

2. <span data-ttu-id="99e42-167">No painel esquerdo do hello, expanda a conta de armazenamento de saudação contendo o compartilhamento de arquivos Olá para o qual você deseja tooget um SAS.</span><span class="sxs-lookup"><span data-stu-id="99e42-167">In hello left pane, expand hello storage account containing hello file share for which you wish tooget a SAS.</span></span>

3. <span data-ttu-id="99e42-168">Expanda a conta de armazenamento Olá **compartilhamentos de arquivos**.</span><span class="sxs-lookup"><span data-stu-id="99e42-168">Expand hello storage account's **File Shares**.</span></span>

4. <span data-ttu-id="99e42-169">Compartilhamento de arquivo desejado hello e - no menu de contexto Olá - selecione **obter assinatura de acesso compartilhado**.</span><span class="sxs-lookup"><span data-stu-id="99e42-169">Right-click hello desired file share, and - from hello context menu - select **Get Shared Access Signature**.</span></span>

    ![Obter Assinatura de Acesso Compartilhado](media/vs-azure-tools-storage-explorer-files/image10.png)

5. <span data-ttu-id="99e42-171">Em Olá **assinatura de acesso compartilhado** caixa de diálogo, especifique política hello, datas de início e vencimento, fuso horário e você deseja para o recurso de saudação de níveis de acesso.</span><span class="sxs-lookup"><span data-stu-id="99e42-171">In hello **Shared Access Signature** dialog, specify hello policy, start and expiration dates, time zone, and access levels you want for hello resource.</span></span>

    ![Diálogo Obter SAS](media/vs-azure-tools-storage-explorer-files/image11.png)

6. <span data-ttu-id="99e42-173">Quando tiver terminado de especificar opções de SAS hello, selecione **criar**.</span><span class="sxs-lookup"><span data-stu-id="99e42-173">When you're finished specifying hello SAS options, select **Create**.</span></span>

7. <span data-ttu-id="99e42-174">Um segundo **assinatura de acesso compartilhado** caixa de diálogo, em seguida, exibirá que listas Olá compartilhamento de arquivos juntamente com a URL de saudação e QueryStrings que você pode usar tooaccess Olá recurso de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="99e42-174">A second **Shared Access Signature** dialog will then display that lists hello file share along with hello URL and QueryStrings you can use tooaccess hello storage resource.</span></span> <span data-ttu-id="99e42-175">Selecione **cópia** próximo URL toohello desejar toocopy toohello da área de transferência.</span><span class="sxs-lookup"><span data-stu-id="99e42-175">Select **Copy** next toohello URL you wish toocopy toohello clipboard.</span></span>
    
    ![Segundo diálogo SAS](media/vs-azure-tools-storage-explorer-files/image12.png)

8. <span data-ttu-id="99e42-177">Ao terminar, escolha **Fechar**.</span><span class="sxs-lookup"><span data-stu-id="99e42-177">When done, select **Close**.</span></span>

## <a name="manage-access-policies-for-a-file-share"></a><span data-ttu-id="99e42-178">Gerenciar políticas de acesso para um compartilhamento de arquivos</span><span class="sxs-lookup"><span data-stu-id="99e42-178">Manage Access Policies for a file share</span></span>

<span data-ttu-id="99e42-179">Olá etapas a seguir ilustram como toomanage (Adicionar e remover) políticas de acesso para um compartilhamento de arquivos: +.</span><span class="sxs-lookup"><span data-stu-id="99e42-179">hello following steps illustrate how toomanage (add and remove) access policies for a file share:+ .</span></span> <span data-ttu-id="99e42-180">Olá políticas de acesso é usada para criar URLs da SAS por meio do qual as pessoas podem usar Olá tooaccess recursos de arquivo de armazenamento durante um período de tempo definido.</span><span class="sxs-lookup"><span data-stu-id="99e42-180">hello Access Policies is used for creating SAS URLs through which people can use tooaccess hello Storage File resource during a defined period of time.</span></span>

1. <span data-ttu-id="99e42-181">Abra o Gerenciador de Armazenamento (Preview).</span><span class="sxs-lookup"><span data-stu-id="99e42-181">Open Storage Explorer (Preview).</span></span>

2. <span data-ttu-id="99e42-182">No painel esquerdo do hello, expanda conta de armazenamento de saudação contendo o compartilhamento de arquivo hello cujas desejar toomanage as políticas de acesso.</span><span class="sxs-lookup"><span data-stu-id="99e42-182">In hello left pane, expand hello storage account containing hello file share whose access policies you wish toomanage.</span></span>

3. <span data-ttu-id="99e42-183">Expanda a conta de armazenamento Olá **compartilhamentos de arquivos**.</span><span class="sxs-lookup"><span data-stu-id="99e42-183">Expand hello storage account's **File Shares**.</span></span>

4. <span data-ttu-id="99e42-184">Selecione Compartilhamento de arquivo desejado hello e - no menu de contexto Olá - **gerenciar políticas de acesso**.</span><span class="sxs-lookup"><span data-stu-id="99e42-184">Select hello desired file share, and - from hello context menu - select **Manage Access Policies**.</span></span>

    ![Menu de contexto Gerenciar políticas de acesso](media/vs-azure-tools-storage-explorer-files/image13.png)

5. <span data-ttu-id="99e42-186">Olá **políticas de acesso** diálogo listará todas as políticas de acesso já criadas para o compartilhamento de arquivo selecionado hello.</span><span class="sxs-lookup"><span data-stu-id="99e42-186">hello **Access Policies** dialog will list any access policies already created for hello selected file share.</span></span>
    
    ![Políticas de acesso](media/vs-azure-tools-storage-explorer-files/image14.png)

6. <span data-ttu-id="99e42-188">Siga estas etapas, dependendo da tarefa de gerenciamento de política de acesso de saudação:</span><span class="sxs-lookup"><span data-stu-id="99e42-188">Follow these steps depending on hello access policy management task:</span></span>
    
    - <span data-ttu-id="99e42-189">**Adicionar uma nova política de acesso** — escolha **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="99e42-189">**Add a new access policy** - Select **Add**.</span></span> <span data-ttu-id="99e42-190">Uma vez gerado, Olá **políticas de acesso** caixa de diálogo exibirá Olá recém-adicionado acessar política (com configurações padrão).</span><span class="sxs-lookup"><span data-stu-id="99e42-190">Once generated, hello **Access Policies** dialog will display hello newly added access policy (with default settings).</span></span>

    - <span data-ttu-id="99e42-191">**Editar uma política de acesso** — faça as edições desejadas e escolha **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="99e42-191">**Edit an access policy** - Make any desired edits, and select **Save**.</span></span>

    - <span data-ttu-id="99e42-192">**Remover uma política de acesso** - selecione **remover** próximo toohello de política de acesso você deseja tooremove.</span><span class="sxs-lookup"><span data-stu-id="99e42-192">**Remove an access policy** - Select **Remove** next toohello access policy you wish tooremove.</span></span>

7. <span data-ttu-id="99e42-193">Crie uma nova URL de SAS usando Olá política de acesso que você criou anteriormente:</span><span class="sxs-lookup"><span data-stu-id="99e42-193">Create a new SAS URL using hello Access Policy you created earlier:</span></span>
    
    ![Obter SAS](media/vs-azure-tools-storage-explorer-files/image15.png)
    
    ![Nome e propriedades SAS](media/vs-azure-tools-storage-explorer-files/image16.png)

## <a name="managing-files-in-a-file-share"></a><span data-ttu-id="99e42-196">Gerenciando arquivos em um compartilhamento de arquivos</span><span class="sxs-lookup"><span data-stu-id="99e42-196">Managing files in a file share</span></span>

<span data-ttu-id="99e42-197">Depois de criar um compartilhamento de arquivos, você pode carregar um compartilhamento de arquivos do arquivo toothat, faça o download de um computador local do arquivo tooyour, abrir um arquivo em seu computador local e muito mais.</span><span class="sxs-lookup"><span data-stu-id="99e42-197">Once you've created a file share, you can upload a file toothat file share, download a file tooyour local computer, open a file on your local computer, and much more.</span></span>

<span data-ttu-id="99e42-198">Olá etapas a seguir ilustram como compartilham a toomanage Olá arquivos (e pastas) dentro de um arquivo.</span><span class="sxs-lookup"><span data-stu-id="99e42-198">hello following steps illustrate how toomanage hello files (and folders) within a file share.</span></span>

1.  <span data-ttu-id="99e42-199">Abra o Gerenciador de Armazenamento (Preview).</span><span class="sxs-lookup"><span data-stu-id="99e42-199">Open Storage Explorer (Preview).</span></span>

2.  <span data-ttu-id="99e42-200">No painel esquerdo do hello, expanda a conta de armazenamento de saudação contendo o compartilhamento de arquivo hello desejar toomanage.</span><span class="sxs-lookup"><span data-stu-id="99e42-200">In hello left pane, expand hello storage account containing hello file share you wish toomanage.</span></span>

3.  <span data-ttu-id="99e42-201">Expanda a conta de armazenamento Olá **compartilhamentos de arquivos**.</span><span class="sxs-lookup"><span data-stu-id="99e42-201">Expand hello storage account's **File Shares**.</span></span>

4.  <span data-ttu-id="99e42-202">Clique duas vezes desejar tooview de compartilhamento de arquivo hello.</span><span class="sxs-lookup"><span data-stu-id="99e42-202">Double-click hello file share you wish tooview.</span></span>

5.  <span data-ttu-id="99e42-203">painel principal Olá exibirá o conteúdo do compartilhamento de arquivo hello.</span><span class="sxs-lookup"><span data-stu-id="99e42-203">hello main pane will display hello file share's contents.</span></span>

    ![Olá conteúdo do compartilhamento](media/vs-azure-tools-storage-explorer-files/image17.png)

6.  <span data-ttu-id="99e42-205">painel principal Olá exibirá o conteúdo do compartilhamento de arquivo hello.</span><span class="sxs-lookup"><span data-stu-id="99e42-205">hello main pane will display hello file share's contents.</span></span>

7.  <span data-ttu-id="99e42-206">Siga estas que etapas, dependendo da tarefa Olá desejar tooperform:</span><span class="sxs-lookup"><span data-stu-id="99e42-206">Follow these steps depending on hello task you wish tooperform:</span></span>

    - <span data-ttu-id="99e42-207">**Carregar o compartilhamento de arquivos de tooa de arquivos**</span><span class="sxs-lookup"><span data-stu-id="99e42-207">**Upload files tooa file share**</span></span>

        <span data-ttu-id="99e42-208">a.</span><span class="sxs-lookup"><span data-stu-id="99e42-208">a.</span></span>  <span data-ttu-id="99e42-209">Na barra de ferramentas do painel Olá principal, selecione **carregar**e, em seguida, **carregar arquivos** do menu suspenso de saudação.</span><span class="sxs-lookup"><span data-stu-id="99e42-209">On hello main pane's toolbar, select **Upload**, and then **Upload Files** from hello drop-down menu.</span></span>

        ![Carregar arquivos](media/vs-azure-tools-storage-explorer-files/image18.png)
        
        <span data-ttu-id="99e42-211">b.</span><span class="sxs-lookup"><span data-stu-id="99e42-211">b.</span></span> <span data-ttu-id="99e42-212">Em Olá **carregar arquivos** caixa de diálogo, reticências Olá select (**...** ) botão no lado direito de saudação do hello **arquivos** tooselect Olá arquivos desejar tooupload da caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="99e42-212">In hello **Upload files** dialog, select hello ellipsis (**…**) button on hello right side of hello **Files** text box tooselect hello file(s) you wish tooupload.</span></span>

        ![Adicionando arquivos](media/vs-azure-tools-storage-explorer-files/image19.png)

        <span data-ttu-id="99e42-214">c.</span><span class="sxs-lookup"><span data-stu-id="99e42-214">c.</span></span> <span data-ttu-id="99e42-215">Escolha **Carregar**.</span><span class="sxs-lookup"><span data-stu-id="99e42-215">Select **Upload**.</span></span>

    - <span data-ttu-id="99e42-216">**Carregar uma pasta de compartilhamento de arquivo de tooa**</span><span class="sxs-lookup"><span data-stu-id="99e42-216">**Upload a folder tooa file share**</span></span>
        
        <span data-ttu-id="99e42-217">a.</span><span class="sxs-lookup"><span data-stu-id="99e42-217">a.</span></span> <span data-ttu-id="99e42-218">Na barra de ferramentas do painel Olá principal, selecione **carregar**e, em seguida, **carregar pasta** do menu suspenso de saudação.</span><span class="sxs-lookup"><span data-stu-id="99e42-218">On hello main pane's toolbar, select **Upload**, and then **Upload Folder** from hello drop-down menu.</span></span>

        ![Menu Carregar pasta](media/vs-azure-tools-storage-explorer-files/image20.png)

        <span data-ttu-id="99e42-220">b.</span><span class="sxs-lookup"><span data-stu-id="99e42-220">b.</span></span> <span data-ttu-id="99e42-221">Em Olá **pasta carregamento** caixa de diálogo, reticências Olá select (**...** ) botão no lado direito de saudação do hello **pasta** pasta de saudação de tooselect de caixa de texto cujo conteúdo você deseja tooupload.</span><span class="sxs-lookup"><span data-stu-id="99e42-221">In hello **Upload folder** dialog, select hello ellipsis (**…**) button on hello right side of hello **Folder** text box tooselect hello folder whose contents you wish tooupload.</span></span>

        <span data-ttu-id="99e42-222">c.</span><span class="sxs-lookup"><span data-stu-id="99e42-222">c.</span></span> <span data-ttu-id="99e42-223">Opcionalmente, especifique uma pasta de destino no qual Olá conteúdo da pasta selecionada será carregado.</span><span class="sxs-lookup"><span data-stu-id="99e42-223">Optionally, specify a target folder into which hello selected folder's contents will be uploaded.</span></span> <span data-ttu-id="99e42-224">Se a pasta de destino de saudação não existir, ele será criado.</span><span class="sxs-lookup"><span data-stu-id="99e42-224">If hello target folder doesn’t exist, it will be created.</span></span>

        <span data-ttu-id="99e42-225">d.</span><span class="sxs-lookup"><span data-stu-id="99e42-225">d.</span></span> <span data-ttu-id="99e42-226">Escolha **Carregar**.</span><span class="sxs-lookup"><span data-stu-id="99e42-226">Select **Upload**.</span></span>

    - <span data-ttu-id="99e42-227">**Fazer o download de um computador local do arquivo tooyour**</span><span class="sxs-lookup"><span data-stu-id="99e42-227">**Download a file tooyour local computer**</span></span>
        
        <span data-ttu-id="99e42-228">a.</span><span class="sxs-lookup"><span data-stu-id="99e42-228">a.</span></span> <span data-ttu-id="99e42-229">Selecione arquivo hello desejar toodownload.</span><span class="sxs-lookup"><span data-stu-id="99e42-229">Select hello file you wish toodownload.</span></span>
        
        <span data-ttu-id="99e42-230">b.</span><span class="sxs-lookup"><span data-stu-id="99e42-230">b.</span></span> <span data-ttu-id="99e42-231">Na barra de ferramentas do painel Olá principal, selecione **baixar**.</span><span class="sxs-lookup"><span data-stu-id="99e42-231">On hello main pane's toolbar, select **Download**.</span></span>
        
        <span data-ttu-id="99e42-232">c.</span><span class="sxs-lookup"><span data-stu-id="99e42-232">c.</span></span> <span data-ttu-id="99e42-233">Em Olá **especifique onde toosave Olá baixou o arquivo** caixa de diálogo, especifique Olá local onde você deseja que o arquivo hello baixado e Olá nome você deseja toogive-lo.</span><span class="sxs-lookup"><span data-stu-id="99e42-233">In hello **Specify where toosave hello downloaded file** dialog, specify hello location where you want hello file downloaded, and hello name you wish toogive it.</span></span>

        <span data-ttu-id="99e42-234">d.</span><span class="sxs-lookup"><span data-stu-id="99e42-234">d.</span></span> <span data-ttu-id="99e42-235">Selecione **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="99e42-235">Select **Save**.</span></span>

    - <span data-ttu-id="99e42-236">**Abrir um arquivo em seu computador local**</span><span class="sxs-lookup"><span data-stu-id="99e42-236">**Open a file on your local computer**</span></span>
        
        <span data-ttu-id="99e42-237">a.</span><span class="sxs-lookup"><span data-stu-id="99e42-237">a.</span></span>  <span data-ttu-id="99e42-238">Selecione arquivo hello desejar tooopen.</span><span class="sxs-lookup"><span data-stu-id="99e42-238">Select hello file you wish tooopen.</span></span>
        
        <span data-ttu-id="99e42-239">b.</span><span class="sxs-lookup"><span data-stu-id="99e42-239">b.</span></span>  <span data-ttu-id="99e42-240">Na barra de ferramentas do painel Olá principal, selecione **abrir**.</span><span class="sxs-lookup"><span data-stu-id="99e42-240">On hello main pane's toolbar, select **Open**.</span></span>
        
        <span data-ttu-id="99e42-241">c.</span><span class="sxs-lookup"><span data-stu-id="99e42-241">c.</span></span>  <span data-ttu-id="99e42-242">arquivo Hello será baixado e abertos usando o aplicativo hello associado com o tipo subjacente de arquivo do arquivo hello.</span><span class="sxs-lookup"><span data-stu-id="99e42-242">hello file will be downloaded and opened using hello application associated with hello file's underlying file type.</span></span>

    - <span data-ttu-id="99e42-243">**Copiar uma área de transferência do arquivo toohello**</span><span class="sxs-lookup"><span data-stu-id="99e42-243">**Copy a file toohello clipboard**</span></span>

        <span data-ttu-id="99e42-244">a.</span><span class="sxs-lookup"><span data-stu-id="99e42-244">a.</span></span> <span data-ttu-id="99e42-245">Selecione arquivo hello desejar toocopy.</span><span class="sxs-lookup"><span data-stu-id="99e42-245">Select hello file you wish toocopy.</span></span>

        <span data-ttu-id="99e42-246">b.</span><span class="sxs-lookup"><span data-stu-id="99e42-246">b.</span></span> <span data-ttu-id="99e42-247">Na barra de ferramentas do painel Olá principal, selecione **cópia**.</span><span class="sxs-lookup"><span data-stu-id="99e42-247">On hello main pane's toolbar, select **Copy**.</span></span>

        <span data-ttu-id="99e42-248">c.</span><span class="sxs-lookup"><span data-stu-id="99e42-248">c.</span></span> <span data-ttu-id="99e42-249">No painel esquerdo do hello, navegar tooanother compartilhamento de arquivo e clique duas vezes nele tooview-lo no painel principal hello.</span><span class="sxs-lookup"><span data-stu-id="99e42-249">In hello left pane, navigate tooanother file share, and double-click it tooview it in hello main pane.</span></span>

        <span data-ttu-id="99e42-250">d.</span><span class="sxs-lookup"><span data-stu-id="99e42-250">d.</span></span> <span data-ttu-id="99e42-251">Na barra de ferramentas do painel Olá principal, selecione **colar** toocreate uma cópia do arquivo hello.</span><span class="sxs-lookup"><span data-stu-id="99e42-251">On hello main pane's toolbar, select **Paste** toocreate a copy of hello file.</span></span>

    - <span data-ttu-id="99e42-252">**Excluir um arquivo**</span><span class="sxs-lookup"><span data-stu-id="99e42-252">**Delete a file**</span></span>

        <span data-ttu-id="99e42-253">a.</span><span class="sxs-lookup"><span data-stu-id="99e42-253">a.</span></span> <span data-ttu-id="99e42-254">Selecione arquivo hello desejar toodelete.</span><span class="sxs-lookup"><span data-stu-id="99e42-254">Select hello file you wish toodelete.</span></span>

        <span data-ttu-id="99e42-255">b.</span><span class="sxs-lookup"><span data-stu-id="99e42-255">b.</span></span> <span data-ttu-id="99e42-256">Na barra de ferramentas do painel Olá principal, selecione **excluir**.</span><span class="sxs-lookup"><span data-stu-id="99e42-256">On hello main pane's toolbar, select **Delete**.</span></span>

        <span data-ttu-id="99e42-257">c.</span><span class="sxs-lookup"><span data-stu-id="99e42-257">c.</span></span> <span data-ttu-id="99e42-258">Selecione **Sim** toohello caixa de diálogo de confirmação.</span><span class="sxs-lookup"><span data-stu-id="99e42-258">Select **Yes** toohello confirmation dialog.</span></span>

## <a name="next-steps"></a><span data-ttu-id="99e42-259">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="99e42-259">Next steps</span></span>

- <span data-ttu-id="99e42-260">Saudação de exibição [notas de versão do Gerenciador de armazenamento (visualização) e vídeos mais recentes](http://www.storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="99e42-260">View hello [latest Storage Explorer (Preview) release notes and videos](http://www.storageexplorer.com/).</span></span>

- <span data-ttu-id="99e42-261">Saiba como muito[criar aplicativos usando blobs do Azure, tabelas, filas e arquivos](https://azure.microsoft.com/documentation/services/storage/).</span><span class="sxs-lookup"><span data-stu-id="99e42-261">Learn how too[create applications using Azure blobs, tables, queues, and files](https://azure.microsoft.com/documentation/services/storage/).</span></span>
