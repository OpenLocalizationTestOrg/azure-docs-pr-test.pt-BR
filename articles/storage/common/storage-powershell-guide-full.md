---
title: aaaUsing PowerShell do Azure com o armazenamento do Azure | Microsoft Docs
description: "Saiba como toouse Olá cmdlets do PowerShell do Azure para armazenamento do Azure toocreate e gerenciar contas de armazenamento; trabalhar com tabelas, blobs, filas e arquivos; Configurar a análise de armazenamento de consulta e criar assinaturas de acesso compartilhado."
services: storage
documentationcenter: na
author: robinsh
manager: timlt
ms.assetid: f4704f58-abc6-4f89-8b6d-1b1659746f5a
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/03/2017
ms.author: robinsh
ms.openlocfilehash: 17d638e741911ceafb9777d5c2fce7bfe533e50c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="using-azure-powershell-with-azure-storage"></a><span data-ttu-id="e3b61-103">Usando o PowerShell do Azure com o Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="e3b61-103">Using Azure PowerShell with Azure Storage</span></span>
## <a name="overview"></a><span data-ttu-id="e3b61-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="e3b61-104">Overview</span></span>
<span data-ttu-id="e3b61-105">PowerShell do Azure é um módulo que fornece toomanage de cmdlets do Azure por meio do Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e3b61-105">Azure PowerShell is a module that provides cmdlets toomanage Azure through Windows PowerShell.</span></span> <span data-ttu-id="e3b61-106">Ele é um shell de linha de comando baseado em tarefa e linguagem de script criado especialmente para administração do sistema.</span><span class="sxs-lookup"><span data-stu-id="e3b61-106">It is a task-based command-line shell and scripting language designed especially for system administration.</span></span> <span data-ttu-id="e3b61-107">Com o PowerShell, você pode facilmente controlar e automatizar a administração de saudação de aplicativos e serviços do Azure.</span><span class="sxs-lookup"><span data-stu-id="e3b61-107">With PowerShell, you can easily control and automate hello administration of your Azure services and applications.</span></span> <span data-ttu-id="e3b61-108">Por exemplo, você pode usar Olá cmdlets tooperform Olá mesmas tarefas que você pode executar por Olá [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="e3b61-108">For example, you can use hello cmdlets tooperform hello same tasks that you can perform through hello [Azure portal](https://portal.azure.com).</span></span>

<span data-ttu-id="e3b61-109">Neste guia, exploraremos como Olá toouse [Cmdlets de armazenamento do Azure](/powershell/module/azurerm.storage/#storage) tooperform uma variedade de tarefas de administração e desenvolvimento com o armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="e3b61-109">In this guide, we'll explore how toouse hello [Azure Storage Cmdlets](/powershell/module/azurerm.storage/#storage) tooperform a variety of development and administration tasks with Azure Storage.</span></span>

<span data-ttu-id="e3b61-110">Este guia pressupõe que você tenha usado anteriormente o [Armazenamento do Azure](https://azure.microsoft.com/documentation/services/storage/) e o [Windows PowerShell](http://technet.microsoft.com/library/bb978526.aspx).</span><span class="sxs-lookup"><span data-stu-id="e3b61-110">This guide assumes that you have prior experience using [Azure Storage](https://azure.microsoft.com/documentation/services/storage/) and [Windows PowerShell](http://technet.microsoft.com/library/bb978526.aspx).</span></span> <span data-ttu-id="e3b61-111">Guia de saudação fornece vários scripts toodemonstrate uso de saudação do PowerShell com o armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="e3b61-111">hello guide provides a number of scripts toodemonstrate hello usage of PowerShell with Azure Storage.</span></span> <span data-ttu-id="e3b61-112">Você deve atualizar as variáveis de script hello com base na sua configuração antes de executar cada script.</span><span class="sxs-lookup"><span data-stu-id="e3b61-112">You should update hello script variables based on your configuration before running each script.</span></span>

<span data-ttu-id="e3b61-113">a primeira seção Olá neste guia fornece uma visão geral rápida do PowerShell e de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="e3b61-113">hello first section in this guide provides a quick glance at Azure Storage and PowerShell.</span></span> <span data-ttu-id="e3b61-114">Para obter informações detalhadas e instruções, iniciar de saudação [pré-requisitos para usar o PowerShell do Azure com o armazenamento do Azure](#prerequisites-for-using-azure-powershell-with-azure-storage).</span><span class="sxs-lookup"><span data-stu-id="e3b61-114">For detailed information and instructions, start from hello [Prerequisites for using Azure PowerShell with Azure Storage](#prerequisites-for-using-azure-powershell-with-azure-storage).</span></span>

## <a name="getting-started-with-azure-storage-and-powershell-in-5-minutes"></a><span data-ttu-id="e3b61-115">Introdução ao Armazenamento do Azure e ao PowerShell em 5 minutos</span><span class="sxs-lookup"><span data-stu-id="e3b61-115">Getting started with Azure Storage and PowerShell in 5 minutes</span></span>
<span data-ttu-id="e3b61-116">Esta seção mostra como tooaccess armazenamento do Azure por meio do PowerShell em 5 minutos.</span><span class="sxs-lookup"><span data-stu-id="e3b61-116">This section shows you how tooaccess Azure Storage via PowerShell in 5 minutes.</span></span>

<span data-ttu-id="e3b61-117">**Novo tooAzure:** obter uma assinatura Microsoft Azure e uma conta da Microsoft associada à assinatura.</span><span class="sxs-lookup"><span data-stu-id="e3b61-117">**New tooAzure:** Get a Microsoft Azure subscription and a Microsoft account associated with that subscription.</span></span> <span data-ttu-id="e3b61-118">Para saber mais sobre as opções de compra do Azure, confira [Avaliação gratuita](https://azure.microsoft.com/pricing/free-trial/), [Opções de compra](https://azure.microsoft.com/pricing/purchase-options/) e [Ofertas para membros](https://azure.microsoft.com/pricing/member-offers/) (para membros do MSDN, Microsoft Partner Network e BizSpark, entre outros programas da Microsoft).</span><span class="sxs-lookup"><span data-stu-id="e3b61-118">For information on Azure purchase options, see [Free Trial](https://azure.microsoft.com/pricing/free-trial/), [Purchase Options](https://azure.microsoft.com/pricing/purchase-options/), and [Member Offers](https://azure.microsoft.com/pricing/member-offers/) (for members of MSDN, Microsoft Partner Network, and BizSpark, and other Microsoft programs).</span></span>

<span data-ttu-id="e3b61-119">Consulte [Atribuindo funções de administrador no Azure AD (Azure Active Directory)](https://msdn.microsoft.com/library/azure/hh531793.aspx) para obter mais informações sobre as assinaturas do Azure.</span><span class="sxs-lookup"><span data-stu-id="e3b61-119">See [Assigning administrator roles in Azure Active Directory (Azure AD)](https://msdn.microsoft.com/library/azure/hh531793.aspx) for more information about Azure subscriptions.</span></span>

<span data-ttu-id="e3b61-120">**Depois de criar uma assinatura e conta do Microsoft Azure:**</span><span class="sxs-lookup"><span data-stu-id="e3b61-120">**After creating a Microsoft Azure subscription and account:**</span></span>

1. <span data-ttu-id="e3b61-121">Baixe e instale o hello mais recente [Azure PowerShell](https://github.com/Azure/azure-powershell/releases/latest).</span><span class="sxs-lookup"><span data-stu-id="e3b61-121">Download and install hello latest [Azure PowerShell](https://github.com/Azure/azure-powershell/releases/latest).</span></span>
2. <span data-ttu-id="e3b61-122">Iniciar Windows PowerShell script ambiente integrado (ISE): No computador local, vá toohello **iniciar** menu.</span><span class="sxs-lookup"><span data-stu-id="e3b61-122">Start Windows PowerShell Integrated Scripting Environment (ISE): In your local computer, go toohello **Start** menu.</span></span> <span data-ttu-id="e3b61-123">Tipo **ferramentas administrativas** e clique em toorun-lo.</span><span class="sxs-lookup"><span data-stu-id="e3b61-123">Type **Administrative Tools** and click toorun it.</span></span> <span data-ttu-id="e3b61-124">Em Olá **ferramentas administrativas** janela, clique com botão direito **o Windows PowerShell ISE**, clique em **executar como administrador**.</span><span class="sxs-lookup"><span data-stu-id="e3b61-124">In hello **Administrative Tools** window, right-click **Windows PowerShell ISE**, click **Run as Administrator**.</span></span>
3. <span data-ttu-id="e3b61-125">Em **o Windows PowerShell ISE**, clique em **arquivo** > **novo** toocreate um novo arquivo de script.</span><span class="sxs-lookup"><span data-stu-id="e3b61-125">In **Windows PowerShell ISE**, click **File** > **New** toocreate a new script file.</span></span>
4. <span data-ttu-id="e3b61-126">Agora, vamos dar um script simples que mostra o básico tooaccess de comandos do PowerShell armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="e3b61-126">Now, we'll give you a simple script that shows basic PowerShell commands tooaccess Azure Storage.</span></span> <span data-ttu-id="e3b61-127">script Hello primeiro solicitará sua tooadd de credenciais de conta do Azure o ambiente do PowerShell do Azure conta toohello local.</span><span class="sxs-lookup"><span data-stu-id="e3b61-127">hello script will first ask your Azure account credentials tooadd your Azure account toohello local PowerShell environment.</span></span> <span data-ttu-id="e3b61-128">Em seguida, script hello definir saudação padrão assinatura do Azure e criar uma nova conta de armazenamento no Azure.</span><span class="sxs-lookup"><span data-stu-id="e3b61-128">Then, hello script will set hello default Azure subscription and create a new storage account in Azure.</span></span> <span data-ttu-id="e3b61-129">Em seguida, script hello criará um novo contêiner nessa nova conta de armazenamento e carregar um contêiner de toothat de (blob) do arquivo de imagem existente.</span><span class="sxs-lookup"><span data-stu-id="e3b61-129">Next, hello script will create a new container in this new storage account and upload an existing image file (blob) toothat container.</span></span> <span data-ttu-id="e3b61-130">Depois que o script hello lista todos os blobs nesse contêiner, ele cria um novo diretório de destino no computador local e baixar o arquivo de imagem de saudação.</span><span class="sxs-lookup"><span data-stu-id="e3b61-130">After hello script lists all blobs in that container, it will create a new destination directory in your local computer and download hello image file.</span></span>
5. <span data-ttu-id="e3b61-131">No hello seção de código a seguir, selecione o script hello entre Olá comentários **#begin** e **#end**.</span><span class="sxs-lookup"><span data-stu-id="e3b61-131">In hello following code section, select hello script between hello remarks **#begin** and **#end**.</span></span> <span data-ttu-id="e3b61-132">Pressione CTRL + C toocopy-toohello área de transferência.</span><span class="sxs-lookup"><span data-stu-id="e3b61-132">Press CTRL+C toocopy it toohello clipboard.</span></span>

    ```powershell
    # begin
    # Update with hello name of your subscription.
    $SubscriptionName = "YourSubscriptionName"
       
    # Give a name tooyour new storage account. It must be lowercase!
    $StorageAccountName = "yourstorageaccountname"
       
    # Choose "West US" as an example.
    $Location = "West US"
       
    # Give a name tooyour new container.
    $ContainerName = "imagecontainer"
       
    # Have an image file and a source directory in your local computer.
    $ImageToUpload = "C:\Images\HelloWorld.png"
       
    # A destination directory in your local computer.
    $DestinationFolder = "C:\DownloadImages"
       
    # Add your Azure account toohello local PowerShell environment.
    Add-AzureAccount
       
    # Set a default Azure subscription.
    Select-AzureSubscription -SubscriptionName $SubscriptionName –Default
       
    # Create a new storage account.
    New-AzureStorageAccount –StorageAccountName $StorageAccountName -Location $Location
       
    # Set a default storage account.
    Set-AzureSubscription -CurrentStorageAccountName $StorageAccountName -SubscriptionName $SubscriptionName
       
    # Create a new container.
    New-AzureStorageContainer -Name $ContainerName -Permission Off
       
    # Upload a blob into a container.
    Set-AzureStorageBlobContent -Container $ContainerName -File $ImageToUpload
       
    # List all blobs in a container.
    Get-AzureStorageBlob -Container $ContainerName
       
    # Download blobs from hello container:
    # Get a reference tooa list of all blobs in a container.
    $blobs = Get-AzureStorageBlob -Container $ContainerName
       
    # Create hello destination directory.
    New-Item -Path $DestinationFolder -ItemType Directory -Force  
       
    # Download blobs into hello local destination directory.
    $blobs | Get-AzureStorageBlobContent –Destination $DestinationFolder
       
    # end
    ```

6. <span data-ttu-id="e3b61-133">Em **o Windows PowerShell ISE**, pressione o script de saudação toocopy CTRL + V.</span><span class="sxs-lookup"><span data-stu-id="e3b61-133">In **Windows PowerShell ISE**, press CTRL+V toocopy hello script.</span></span> <span data-ttu-id="e3b61-134">Clique em **Arquivo** > **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="e3b61-134">Click **File** > **Save**.</span></span> <span data-ttu-id="e3b61-135">Em Olá **Salvar como** janela da caixa de diálogo, digite o nome de Olá Olá do arquivo de script, como "mystoragescript".</span><span class="sxs-lookup"><span data-stu-id="e3b61-135">In hello **Save As** dialog window, type hello name of hello script file, such as "mystoragescript."</span></span> <span data-ttu-id="e3b61-136">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="e3b61-136">Click **Save**.</span></span>
7. <span data-ttu-id="e3b61-137">Agora, você precisa de variáveis de script hello tooupdate com base em suas definições de configuração.</span><span class="sxs-lookup"><span data-stu-id="e3b61-137">Now, you need tooupdate hello script variables based on your configuration settings.</span></span> <span data-ttu-id="e3b61-138">Você deve atualizar Olá **$SubscriptionName** variável com sua própria assinatura.</span><span class="sxs-lookup"><span data-stu-id="e3b61-138">You must update hello **$SubscriptionName** variable with your own subscription.</span></span> <span data-ttu-id="e3b61-139">Você pode manter Olá outras variáveis como especificado no script hello ou atualizá-los como quiser.</span><span class="sxs-lookup"><span data-stu-id="e3b61-139">You can keep hello other variables as specified in hello script or update them as you wish.</span></span>
   
   * <span data-ttu-id="e3b61-140">**$SubscriptionName:** você deve atualizar essa variável com o nome de sua própria assinatura.</span><span class="sxs-lookup"><span data-stu-id="e3b61-140">**$SubscriptionName:** You must update this variable with your own subscription name.</span></span> <span data-ttu-id="e3b61-141">Execute uma saudação após três maneiras toolocate Olá nome da sua assinatura:</span><span class="sxs-lookup"><span data-stu-id="e3b61-141">Follow one of hello following three ways toolocate hello name of your subscription:</span></span>
     
    <span data-ttu-id="e3b61-142">a.</span><span class="sxs-lookup"><span data-stu-id="e3b61-142">a.</span></span> <span data-ttu-id="e3b61-143">Em **o Windows PowerShell ISE**, clique em **arquivo** > **novo** toocreate um novo arquivo de script.</span><span class="sxs-lookup"><span data-stu-id="e3b61-143">In **Windows PowerShell ISE**, click **File** > **New** toocreate a new script file.</span></span> <span data-ttu-id="e3b61-144">A seguir Olá cópia toohello novo arquivo de script do script e clique em **depurar** > **executar**.</span><span class="sxs-lookup"><span data-stu-id="e3b61-144">Copy hello following script toohello new script file and click **Debug** > **Run**.</span></span> <span data-ttu-id="e3b61-145">Olá script a seguir será seu tooadd de credenciais de conta do Azure primeiro solicitar uma conta do Azure toohello PowerShell ambiente local e, em seguida, Mostrar todas as assinaturas de saudação que são conectados toohello sessão local do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e3b61-145">hello following script will first ask your Azure account credentials tooadd your Azure account toohello local PowerShell environment and then show all hello subscriptions that are connected toohello local PowerShell session.</span></span> <span data-ttu-id="e3b61-146">Anote uma saudação nome de assinatura de saudação que você deseja toouse ao seguir este tutorial:</span><span class="sxs-lookup"><span data-stu-id="e3b61-146">Take a note of hello name of hello subscription that you want toouse while following this tutorial:</span></span>
     
    ```powershell
    Add-AzureAccount 
      Get-AzureSubscription | Format-Table SubscriptionName, IsDefault, IsCurrent, CurrentStorageAccountName
    ```

    <span data-ttu-id="e3b61-147">b.</span><span class="sxs-lookup"><span data-stu-id="e3b61-147">b.</span></span> <span data-ttu-id="e3b61-148">toolocate e copiar nome de sua assinatura no hello [portal do Azure](https://portal.azure.com), no hello menu Hub saudação à esquerda, clique em **assinaturas**.</span><span class="sxs-lookup"><span data-stu-id="e3b61-148">toolocate and copy your subscription name in hello [Azure portal](https://portal.azure.com), in hello Hub menu on hello left, click **Subscriptions**.</span></span> <span data-ttu-id="e3b61-149">Copie o nome de saudação de assinatura que você deseja toouse durante a execução de scripts de saudação neste guia.</span><span class="sxs-lookup"><span data-stu-id="e3b61-149">Copy hello name of subscription that you want toouse while running hello scripts in this guide.</span></span>
     
     ![Portal do Azure](./media/storage-powershell-guide-full/Subscription_Previewportal.png)

    <span data-ttu-id="e3b61-151">c.</span><span class="sxs-lookup"><span data-stu-id="e3b61-151">c.</span></span> <span data-ttu-id="e3b61-152">toolocate e copiar nome de sua assinatura no hello [Portal clássico do Azure](https://manage.windowsazure.com/), role para baixo e clique em **configurações** em Olá esquerda do portal de saudação.</span><span class="sxs-lookup"><span data-stu-id="e3b61-152">toolocate and copy your subscription name in hello [Azure Classic Portal](https://manage.windowsazure.com/), scroll down and click **Settings** on hello left side of hello portal.</span></span> <span data-ttu-id="e3b61-153">Clique em **assinaturas** toosee uma lista de suas assinaturas.</span><span class="sxs-lookup"><span data-stu-id="e3b61-153">Click **Subscriptions** toosee a list of your subscriptions.</span></span> <span data-ttu-id="e3b61-154">Nome de saudação de cópia de assinatura que você deseja toouse durante a execução de scripts de saudação fornecidos neste guia.</span><span class="sxs-lookup"><span data-stu-id="e3b61-154">Copy hello name of subscription that you want toouse while running hello scripts given in this guide.</span></span>
     
     ![Portal clássico do Azure](./media/storage-powershell-guide-full/Subscription_currentportal.png)

   * <span data-ttu-id="e3b61-156">**$StorageAccountName:** usar Olá considerando o nome do script hello ou digitar um novo nome para sua conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="e3b61-156">**$StorageAccountName:** Use hello given name in hello script or enter a new name for your storage account.</span></span> <span data-ttu-id="e3b61-157">**Importante:** nome Olá Olá da conta de armazenamento deve ser exclusivo no Azure.</span><span class="sxs-lookup"><span data-stu-id="e3b61-157">**Important:** hello name of hello storage account must be unique in Azure.</span></span> <span data-ttu-id="e3b61-158">Ele também deve ter somente letras minúsculas!</span><span class="sxs-lookup"><span data-stu-id="e3b61-158">It must be lowercase, too!</span></span>
   * <span data-ttu-id="e3b61-159">**$Location:** usar Olá fornecido "US West" no script hello ou escolher outros locais do Azure, como Leste dos EUA, Norte da Europa e assim por diante.</span><span class="sxs-lookup"><span data-stu-id="e3b61-159">**$Location:** Use hello given "West US" in hello script or choose other Azure locations, such as East US, North Europe, and so on.</span></span>
   * <span data-ttu-id="e3b61-160">**$ContainerName:** use Olá considerando o nome do script hello ou digite um novo nome para seu contêiner.</span><span class="sxs-lookup"><span data-stu-id="e3b61-160">**$ContainerName:** Use hello given name in hello script or enter a new name for your container.</span></span>
   * <span data-ttu-id="e3b61-161">**$ImageToUpload:** inserir uma imagem de tooa caminho no computador local, como: "C:\Images\HelloWorld.png".</span><span class="sxs-lookup"><span data-stu-id="e3b61-161">**$ImageToUpload:** Enter a path tooa picture on your local computer, such as: "C:\Images\HelloWorld.png".</span></span>
   * <span data-ttu-id="e3b61-162">**$DestinationFolder:** Enter um arquivos de toostore de diretório local do caminho tooa baixado do armazenamento do Azure, como: "C:\DownloadImages".</span><span class="sxs-lookup"><span data-stu-id="e3b61-162">**$DestinationFolder:** Enter a path tooa local directory toostore files downloaded from Azure Storage, such as: "C:\DownloadImages".</span></span>
8. <span data-ttu-id="e3b61-163">Depois de atualizar as variáveis de script hello no arquivo de "mystoragescript.ps1" Olá, clique em **arquivo** > **salvar**.</span><span class="sxs-lookup"><span data-stu-id="e3b61-163">After updating hello script variables in hello "mystoragescript.ps1" file, click **File** > **Save**.</span></span> <span data-ttu-id="e3b61-164">Em seguida, clique em **depurar** > **executar** ou pressione **F5** toorun script de saudação.</span><span class="sxs-lookup"><span data-stu-id="e3b61-164">Then, click **Debug** > **Run** or press **F5** toorun hello script.</span></span>  

<span data-ttu-id="e3b61-165">Após a execução do script hello, você deve ter uma pasta de destino que inclui o arquivo de imagem Olá baixado.</span><span class="sxs-lookup"><span data-stu-id="e3b61-165">After hello script runs, you should have a local destination folder that includes hello downloaded image file.</span></span> <span data-ttu-id="e3b61-166">Olá captura de tela a seguir mostra um exemplo de saída:</span><span class="sxs-lookup"><span data-stu-id="e3b61-166">hello following screenshot shows an example output:</span></span>

![Baixar blobs](./media/storage-powershell-guide-full/Blobdownload.png)

> [!NOTE]
> <span data-ttu-id="e3b61-168">Hello "Introdução ao armazenamento do Azure e do PowerShell em 5 minutos" forneceu uma rápida introdução sobre como toouse PowerShell do Azure com o armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="e3b61-168">hello "Getting started with Azure Storage and PowerShell in 5 minutes" section provided a quick introduction on how toouse Azure PowerShell with Azure Storage.</span></span> <span data-ttu-id="e3b61-169">Para obter informações detalhadas e instruções, recomendamos que você Olá tooread seções a seguir.</span><span class="sxs-lookup"><span data-stu-id="e3b61-169">For detailed information and instructions, we encourage you tooread hello following sections.</span></span>
> 

## <a name="prerequisites-for-using-azure-powershell-with-azure-storage"></a><span data-ttu-id="e3b61-170">Pré-requisitos para usar o Azure PowerShell com o armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="e3b61-170">Prerequisites for using Azure PowerShell with Azure Storage</span></span>
<span data-ttu-id="e3b61-171">Você precisa de uma conta e assinatura toorun Olá cmdlets do Azure PowerShell fornecido neste guia, conforme descrito acima.</span><span class="sxs-lookup"><span data-stu-id="e3b61-171">You need an Azure subscription and account toorun hello PowerShell cmdlets given in this guide, as described above.</span></span>

<span data-ttu-id="e3b61-172">PowerShell do Azure é um módulo que fornece toomanage de cmdlets do Azure por meio do Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e3b61-172">Azure PowerShell is a module that provides cmdlets toomanage Azure through Windows PowerShell.</span></span> <span data-ttu-id="e3b61-173">Para obter informações sobre como instalar e configurar o Azure PowerShell, consulte [como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="e3b61-173">For information on installing and setting up Azure PowerShell, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span> <span data-ttu-id="e3b61-174">É recomendável baixar e instalar ou atualizar o módulo PowerShell do Azure mais recente de toohello antes de usar este guia.</span><span class="sxs-lookup"><span data-stu-id="e3b61-174">We recommend that you download and install or upgrade toohello latest Azure PowerShell module before using this guide.</span></span>

<span data-ttu-id="e3b61-175">Você pode executar cmdlets Olá Olá padrão do Windows PowerShell no console de ou Olá Windows PowerShell Integrated Scripting ISE (ambiente).</span><span class="sxs-lookup"><span data-stu-id="e3b61-175">You can run hello cmdlets in hello standard Windows PowerShell console or hello Windows PowerShell Integrated Scripting Environment (ISE).</span></span> <span data-ttu-id="e3b61-176">Por exemplo, tooopen **o Windows PowerShell ISE**, vá toohello menu de início, digite ferramentas administrativas e clique em toorun-lo.</span><span class="sxs-lookup"><span data-stu-id="e3b61-176">For example, tooopen **Windows PowerShell ISE**, go toohello Start menu, type Administrative Tools and click toorun it.</span></span> <span data-ttu-id="e3b61-177">Na janela de ferramentas administrativas hello, clique o ISE do Windows PowerShell, clique em Executar como administrador.</span><span class="sxs-lookup"><span data-stu-id="e3b61-177">In hello Administrative Tools window, right-click Windows PowerShell ISE, click Run as Administrator.</span></span>

## <a name="how-toomanage-storage-accounts-in-azure"></a><span data-ttu-id="e3b61-178">Como o armazenamento toomanage contas no Azure</span><span class="sxs-lookup"><span data-stu-id="e3b61-178">How toomanage storage accounts in Azure</span></span>

<span data-ttu-id="e3b61-179">Vejamos agora o gerenciamento de contas de armazenamento no Azure com o PowerShell</span><span class="sxs-lookup"><span data-stu-id="e3b61-179">Let's take a look at managing storage accounts in Azure with PowerShell</span></span>

### <a name="how-tooset-a-default-azure-subscription"></a><span data-ttu-id="e3b61-180">Como tooset um padrão de assinatura do Azure</span><span class="sxs-lookup"><span data-stu-id="e3b61-180">How tooset a default Azure subscription</span></span>
<span data-ttu-id="e3b61-181">toomanage o armazenamento do Azure usando o PowerShell do Azure, você precisa tooauthenticate seu ambiente do cliente com o Azure por meio de autenticação do Azure Active Directory ou a autenticação baseada em certificado.</span><span class="sxs-lookup"><span data-stu-id="e3b61-181">toomanage Azure Storage using Azure PowerShell, you need tooauthenticate your client environment with Azure via Azure Active Directory authentication or certificate-based authentication.</span></span> <span data-ttu-id="e3b61-182">Para obter informações detalhadas, consulte [como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview) tutorial.</span><span class="sxs-lookup"><span data-stu-id="e3b61-182">For detailed information, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) tutorial.</span></span> <span data-ttu-id="e3b61-183">Este guia usa a autenticação do Active Directory do Azure hello.</span><span class="sxs-lookup"><span data-stu-id="e3b61-183">This guide uses hello Azure Active Directory authentication.</span></span>

1. <span data-ttu-id="e3b61-184">No ISE do Windows PowerShell, digite Olá tooadd de comando a seguir o ambiente do PowerShell do Azure conta toohello local:</span><span class="sxs-lookup"><span data-stu-id="e3b61-184">In Windows PowerShell ISE, type hello following command tooadd your Azure account toohello local PowerShell environment:</span></span>

    ```powershell
    Add-AzureAccount
    ```

2. <span data-ttu-id="e3b61-185">Na janela de "Entrar tooMicrosoft Azure" Olá, digite Olá o endereço de email e senha associada à sua conta.</span><span class="sxs-lookup"><span data-stu-id="e3b61-185">In hello "Sign in tooMicrosoft Azure" window, type hello email address and password associated with your account.</span></span> <span data-ttu-id="e3b61-186">Azure autentica e salva informações de credencial hello e, em seguida, fecha a janela de saudação.</span><span class="sxs-lookup"><span data-stu-id="e3b61-186">Azure authenticates and saves hello credential information, and then closes hello window.</span></span>

3. <span data-ttu-id="e3b61-187">Em seguida, execute Olá Olá tooview de comando Azure contas no ambiente do PowerShell local e verifique se sua conta está listada a seguir:</span><span class="sxs-lookup"><span data-stu-id="e3b61-187">Next, run hello following command tooview hello Azure accounts in your local PowerShell environment, and verify that your account is listed:</span></span>
   
    ```powershell
    Get-AzureAccount
    ```
4. <span data-ttu-id="e3b61-188">Em seguida, execute Olá tooview cmdlet a seguir todas as assinaturas de saudação que são conectados toohello sessão local do PowerShell e verificar se sua assinatura está listada:</span><span class="sxs-lookup"><span data-stu-id="e3b61-188">Then, run hello following cmdlet tooview all hello subscriptions that are connected toohello local PowerShell session, and verify that your subscription is listed:</span></span>

    ```powershell
    Get-AzureSubscription | Format-Table SubscriptionName, IsDefault, IsCurrent, CurrentStorageAccountName`
    ```
5. <span data-ttu-id="e3b61-189">tooset um padrão de assinatura do Azure, execute o cmdlet Select-AzureSubscription de saudação:</span><span class="sxs-lookup"><span data-stu-id="e3b61-189">tooset a default Azure subscription, run hello Select-AzureSubscription cmdlet:</span></span>

    ```powershell
    $SubscriptionName = 'Your subscription Name'
    Select-AzureSubscription -SubscriptionName $SubscriptionName –Default
    ```

6. <span data-ttu-id="e3b61-190">Verifique o nome de saudação de assinatura de padrão de saudação executando o cmdlet Get-AzureSubscription de saudação:</span><span class="sxs-lookup"><span data-stu-id="e3b61-190">Verify hello name of hello default subscription by running hello Get-AzureSubscription cmdlet:</span></span>

    ```powershell
    Get-AzureSubscription -Default
    ```

7. <span data-ttu-id="e3b61-191">toosee todos os Olá cmdlets do PowerShell disponíveis para o armazenamento do Azure, execute:</span><span class="sxs-lookup"><span data-stu-id="e3b61-191">toosee all hello available PowerShell cmdlets for Azure Storage, run:</span></span>
    
    ```powershell
    Get-Command -Module Azure -Noun *Storage*`
    ```

### <a name="how-toocreate-a-new-azure-storage-account"></a><span data-ttu-id="e3b61-192">Como toocreate uma nova conta de armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="e3b61-192">How toocreate a new Azure storage account</span></span>
<span data-ttu-id="e3b61-193">toouse armazenamento do Azure, você precisará de uma conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="e3b61-193">toouse Azure storage, you will need a storage account.</span></span> <span data-ttu-id="e3b61-194">Depois de configurar sua assinatura do computador tooconnect tooyour, você pode criar uma nova conta de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="e3b61-194">You can create a new Azure storage account after you have configured your computer tooconnect tooyour subscription.</span></span>

1. <span data-ttu-id="e3b61-195">Execute Olá Get-AzureLocation cmdlet toofind todos os locais de datacenters disponíveis hello:</span><span class="sxs-lookup"><span data-stu-id="e3b61-195">Run hello Get-AzureLocation cmdlet toofind all hello available datacenter locations:</span></span>

    ```powershell
    Get-AzureLocation | Format-Table -Property Name, AvailableServices, StorageAccountTypes
    ```

2. <span data-ttu-id="e3b61-196">Em seguida, execute uma nova conta de armazenamento toocreate de cmdlet New-AzureStorageAccount hello.</span><span class="sxs-lookup"><span data-stu-id="e3b61-196">Next, run hello New-AzureStorageAccount cmdlet toocreate a new storage account.</span></span> <span data-ttu-id="e3b61-197">Olá exemplo a seguir cria uma nova conta de armazenamento no data center de "US West" hello.</span><span class="sxs-lookup"><span data-stu-id="e3b61-197">hello following example creates a new storage account in hello "West US" datacenter.</span></span>
   
    ```powershell
    $location = "West US"
    $StorageAccountName = "yourstorageaccount"
    New-AzureStorageAccount –StorageAccountName $StorageAccountName -Location $location
    ```

> [!IMPORTANT]
> <span data-ttu-id="e3b61-198">nome de saudação da sua conta de armazenamento deve ser exclusivo dentro do Azure e deve estar em minúscula.</span><span class="sxs-lookup"><span data-stu-id="e3b61-198">hello name of your storage account must be unique within Azure and must be lowercase.</span></span> <span data-ttu-id="e3b61-199">Para ver as convenções e restrições de nomenclatura, confira [Sobre as contas de armazenamento do Azure](../storage-create-storage-account.md) e [Naming and Referencing Containers, Blobs, and Metadata](http://msdn.microsoft.com/library/azure/dd135715.aspx) (Nomeando e referenciando contêineres, blobs e metadados).</span><span class="sxs-lookup"><span data-stu-id="e3b61-199">For naming conventions and restrictions, see [About Azure Storage Accounts](../storage-create-storage-account.md) and [Naming and Referencing Containers, Blobs, and Metadata](http://msdn.microsoft.com/library/azure/dd135715.aspx).</span></span>
> 
> 

### <a name="how-tooset-a-default-azure-storage-account"></a><span data-ttu-id="e3b61-200">Como tooset uma conta de armazenamento do Azure padrão</span><span class="sxs-lookup"><span data-stu-id="e3b61-200">How tooset a default Azure storage account</span></span>
<span data-ttu-id="e3b61-201">Você pode ter várias contas de armazenamento na sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="e3b61-201">You can have multiple storage accounts in your subscription.</span></span> <span data-ttu-id="e3b61-202">Você pode escolher um deles e defini-lo como a conta de armazenamento saudação padrão para todos os Olá armazenamento comandos no hello mesma sessão do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e3b61-202">You can choose one of them and set it as hello default storage account for all hello storage commands in hello same PowerShell session.</span></span> <span data-ttu-id="e3b61-203">Isso permite que você comandos de armazenamento toorun saudação do Azure PowerShell sem especificar explicitamente o contexto de armazenamento hello.</span><span class="sxs-lookup"><span data-stu-id="e3b61-203">This enables you toorun hello Azure PowerShell storage commands without specifying hello storage context explicitly.</span></span>

1. <span data-ttu-id="e3b61-204">tooset uma conta de armazenamento padrão para a sua assinatura, você pode executar o cmdlet de Set-AzureSubscription hello.</span><span class="sxs-lookup"><span data-stu-id="e3b61-204">tooset a default storage account for your subscription, you can run hello Set-AzureSubscription cmdlet.</span></span>

    ```powershell
    $SubscriptionName = "Your subscription name"
    $StorageAccountName = "yourstorageaccount"  
    Set-AzureSubscription -CurrentStorageAccountName $StorageAccountName -SubscriptionName $SubscriptionName
    ```

2. <span data-ttu-id="e3b61-205">Em seguida, execute Olá Get-AzureSubscription cmdlet tooverify que a conta de armazenamento de saudação é associada à sua conta de assinatura padrão.</span><span class="sxs-lookup"><span data-stu-id="e3b61-205">Next, run hello Get-AzureSubscription cmdlet tooverify that hello storage account is associated with your default subscription account.</span></span> <span data-ttu-id="e3b61-206">Esse comando retorna propriedades de assinatura de saudação na assinatura atual do hello incluindo sua conta de armazenamento atual.</span><span class="sxs-lookup"><span data-stu-id="e3b61-206">This command returns hello subscription properties on hello current subscription including its current storage account.</span></span>

    ```powershell
    Get-AzureSubscription –Current
    ```

### <a name="how-toolist-all-azure-storage-accounts-in-a-subscription"></a><span data-ttu-id="e3b61-207">Como toolist todo o armazenamento do Azure contas em uma assinatura</span><span class="sxs-lookup"><span data-stu-id="e3b61-207">How toolist all Azure storage accounts in a subscription</span></span>
<span data-ttu-id="e3b61-208">Cada assinatura do Azure pode ter até too100 contas de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="e3b61-208">Each Azure subscription can have up too100 storage accounts.</span></span> <span data-ttu-id="e3b61-209">Para obter informações mais atualizadas sobre os limites de hello, consulte [assinatura do Azure e limites de serviço, cotas e restrições](../../azure-subscription-service-limits.md).</span><span class="sxs-lookup"><span data-stu-id="e3b61-209">For hello most up-to-date information on limits, see [Azure Subscription and Service Limits, Quotas, and Constraints](../../azure-subscription-service-limits.md).</span></span>

<span data-ttu-id="e3b61-210">Execute Olá cmdlet toofind nome hello e status Olá de contas de armazenamento na assinatura atual Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="e3b61-210">Run hello following cmdlet toofind out hello name and status of hello storage accounts in hello current subscription:</span></span>

```powershell
Get-AzureStorageAccount | Format-Table -Property StorageAccountName, Location, AccountType, StorageAccountStatus
```

### <a name="how-toocreate-an-azure-storage-context"></a><span data-ttu-id="e3b61-211">Como toocreate um contexto de armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="e3b61-211">How toocreate an Azure storage context</span></span>
<span data-ttu-id="e3b61-212">Contexto de armazenamento do Azure é um objeto de credenciais de armazenamento do PowerShell tooencapsulate hello.</span><span class="sxs-lookup"><span data-stu-id="e3b61-212">Azure storage context is an object in PowerShell tooencapsulate hello storage credentials.</span></span> <span data-ttu-id="e3b61-213">Usando um contexto de armazenamento durante a execução de qualquer cmdlet subsequente permite que você tooauthenticate sua solicitação sem especificar a conta de armazenamento hello e sua chave de acesso explicitamente.</span><span class="sxs-lookup"><span data-stu-id="e3b61-213">Using a storage context while running any subsequent cmdlet enables you tooauthenticate your request without specifying hello storage account and its access key explicitly.</span></span> <span data-ttu-id="e3b61-214">Você pode criar um contexto de armazenamento de várias maneiras, como usando a chave de acesso e do nome da conta de armazenamento, o token de SAS (assinatura de acesso compartilhado), cadeia de conexão ou anonimamente.</span><span class="sxs-lookup"><span data-stu-id="e3b61-214">You can create a storage context in many ways, such as using storage account name and access key, shared access signature (SAS) token, connection string, or anonymous.</span></span> <span data-ttu-id="e3b61-215">Para obter mais informações, consulte [New-AzureStorageContext](/powershell/module/azure.storage/new-azurestoragecontext).</span><span class="sxs-lookup"><span data-stu-id="e3b61-215">For more information, see [New-AzureStorageContext](/powershell/module/azure.storage/new-azurestoragecontext).</span></span>  

<span data-ttu-id="e3b61-216">Use um contexto de armazenamento uma saudação toocreate de três maneiras a seguir:</span><span class="sxs-lookup"><span data-stu-id="e3b61-216">Use one of hello following three ways toocreate a storage context:</span></span>

* <span data-ttu-id="e3b61-217">Executar Olá [Get-AzureStorageKey](/powershell/module/azure.storage/get-azurestoragekey) toofind cmdlet chave de acesso de armazenamento primário Olá para sua conta de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="e3b61-217">Run hello [Get-AzureStorageKey](/powershell/module/azure.storage/get-azurestoragekey) cmdlet toofind out hello primary storage access key for your Azure storage account.</span></span> <span data-ttu-id="e3b61-218">Em seguida, chame Olá [AzureStorageContext novo](/powershell/module/azure.storage/new-azurestoragecontext) cmdlet toocreate um contexto de armazenamento:</span><span class="sxs-lookup"><span data-stu-id="e3b61-218">Next, call hello [New-AzureStorageContext](/powershell/module/azure.storage/new-azurestoragecontext) cmdlet toocreate a storage context:</span></span>

    ```powershell
    $StorageAccountName = "yourstorageaccount"
    $StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
    $Ctx = New-AzureStorageContext $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary
    ```

* <span data-ttu-id="e3b61-219">Gerar um token de assinatura de acesso compartilhado para um contêiner de armazenamento do Azure e usá-lo toocreate um contexto de armazenamento:</span><span class="sxs-lookup"><span data-stu-id="e3b61-219">Generate a shared access signature token for an Azure storage container and use it toocreate a storage context:</span></span>

    ```powershell
    $sasToken = New-AzureStorageContainerSASToken -Container abc -Permission rl
    $Ctx = New-AzureStorageContext -StorageAccountName $StorageAccountName -SasToken $sasToken
    ```

    <span data-ttu-id="e3b61-220">Para saber mais, veja [New-AzureStorageContainerSASToken](/powershell/module/azure.storage/new-azurestoragecontainersastoken) e [Uso de SAS (Assinaturas de Acesso Compartilhado)](../storage-dotnet-shared-access-signature-part-1.md).</span><span class="sxs-lookup"><span data-stu-id="e3b61-220">For more information, see [New-AzureStorageContainerSASToken](/powershell/module/azure.storage/new-azurestoragecontainersastoken) and [Using Shared Access Signatures (SAS)](../storage-dotnet-shared-access-signature-part-1.md).</span></span>

* <span data-ttu-id="e3b61-221">Em alguns casos, convém pontos de extremidade do serviço toospecify hello quando você cria um novo contexto de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="e3b61-221">In some cases, you may want toospecify hello service endpoints when you create a new storage context.</span></span> <span data-ttu-id="e3b61-222">Isso pode ser necessário quando você registrou um nome de domínio personalizado para sua conta de armazenamento com o serviço Blob hello ou desejar toouse uma assinatura de acesso compartilhado para acessar recursos de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="e3b61-222">This might be necessary when you have registered a custom domain name for your storage account with hello Blob service or you want toouse a shared access signature for accessing storage resources.</span></span> <span data-ttu-id="e3b61-223">Definir pontos de extremidade de serviço de saudação em uma cadeia de conexão e usá-lo toocreate um novo contexto de armazenamento conforme mostrado abaixo:</span><span class="sxs-lookup"><span data-stu-id="e3b61-223">Set hello service endpoints in a connection string and use it toocreate a new storage context as shown below:</span></span>

    ```powershell
    $ConnectionString = "DefaultEndpointsProtocol=http;BlobEndpoint=<blobEndpoint>;QueueEndpoint=<QueueEndpoint>;TableEndpoint=<TableEndpoint>;AccountName=<AccountName>;AccountKey=<AccountKey>"
    $Ctx = New-AzureStorageContext -ConnectionString $ConnectionString
    ```

<span data-ttu-id="e3b61-224">Para obter mais informações sobre como tooconfigure uma cadeia de caracteres de conexão de armazenamento, consulte [Configurando cadeias de caracteres de Conexão](../storage-configure-connection-string.md).</span><span class="sxs-lookup"><span data-stu-id="e3b61-224">For more information on how tooconfigure a storage connection string, see [Configuring Connection Strings](../storage-configure-connection-string.md).</span></span>

<span data-ttu-id="e3b61-225">Agora que você tiver configurado seu computador e aprendeu como toomanage assinaturas e contas de armazenamento usando o PowerShell do Azure, vá toohello próxima seção toolearn como toomanage Azure blobs e instantâneos de blob.</span><span class="sxs-lookup"><span data-stu-id="e3b61-225">Now that you have set up your computer and learned how toomanage subscriptions and storage accounts using Azure PowerShell, go toohello next section toolearn how toomanage Azure blobs and blob snapshots.</span></span>

### <a name="how-tooretrieve-and-regenerate-azure-storage-keys"></a><span data-ttu-id="e3b61-226">Como tooretrieve e regenerar chaves de armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="e3b61-226">How tooretrieve and regenerate Azure storage keys</span></span>
<span data-ttu-id="e3b61-227">Uma conta de armazenamento do Azure é fornecida com duas chaves de conta.</span><span class="sxs-lookup"><span data-stu-id="e3b61-227">An Azure Storage account comes with two account keys.</span></span> <span data-ttu-id="e3b61-228">Você pode usar o hello tooretrieve cmdlet a seguir suas chaves.</span><span class="sxs-lookup"><span data-stu-id="e3b61-228">You can use hello following cmdlet tooretrieve your keys.</span></span>

```powershell
Get-AzureStorageKey -StorageAccountName "yourstorageaccount"
```

<span data-ttu-id="e3b61-229">Use Olá cmdlet tooretrieve uma chave específica a seguir.</span><span class="sxs-lookup"><span data-stu-id="e3b61-229">Use hello following cmdlet tooretrieve a specific key.</span></span> <span data-ttu-id="e3b61-230">Os valores válidos são Primary e Secondary.</span><span class="sxs-lookup"><span data-stu-id="e3b61-230">Valid values are Primary and Secondary.</span></span>  

```powershell
(Get-AzureStorageKey -StorageAccountName $StorageAccountName).Primary
    
(Get-AzureStorageKey -StorageAccountName $StorageAccountName).Secondary
```

<span data-ttu-id="e3b61-231">Se você quiser tooregenerate suas chaves, use Olá cmdlet a seguir.</span><span class="sxs-lookup"><span data-stu-id="e3b61-231">If you would like tooregenerate your keys, use hello following cmdlet.</span></span> <span data-ttu-id="e3b61-232">Os valores válidos para -KeyType são "Primary" e "Secundary"</span><span class="sxs-lookup"><span data-stu-id="e3b61-232">Valid values for -KeyType are "Primary" and "Secondary"</span></span>

```powershell
New-AzureStorageKey -StorageAccountName $StorageAccountName -KeyType "Primary"
    
New-AzureStorageKey -StorageAccountName $StorageAccountName -KeyType "Secondary"
```

## <a name="how-toomanage-azure-blobs"></a><span data-ttu-id="e3b61-233">Como os blobs de toomanage do Azure</span><span class="sxs-lookup"><span data-stu-id="e3b61-233">How toomanage Azure blobs</span></span>
<span data-ttu-id="e3b61-234">Armazenamento de BLOBs do Azure é um serviço para armazenar grandes quantidades de dados não estruturados, como texto ou dados binários, que podem ser acessados de qualquer lugar Olá, mundo via HTTP ou HTTPS.</span><span class="sxs-lookup"><span data-stu-id="e3b61-234">Azure Blob storage is a service for storing large amounts of unstructured data, such as text or binary data, that can be accessed from anywhere in hello world via HTTP or HTTPS.</span></span> <span data-ttu-id="e3b61-235">Esta seção pressupõe que você já esteja familiarizado com os conceitos do serviço de armazenamento de BLOBs do Azure hello.</span><span class="sxs-lookup"><span data-stu-id="e3b61-235">This section assumes that you are already familiar with hello Azure Blob Storage Service concepts.</span></span> <span data-ttu-id="e3b61-236">Para obter informações detalhadas, confira [Introdução ao Armazenamento de Blobs usando o .NET](../blobs/storage-dotnet-how-to-use-blobs.md) e [Blob Service Concepts](http://msdn.microsoft.com/library/azure/dd179376.aspx) (Conceitos do serviço Blob).</span><span class="sxs-lookup"><span data-stu-id="e3b61-236">For detailed information, see [Get started with Blob storage using .NET](../blobs/storage-dotnet-how-to-use-blobs.md) and [Blob Service Concepts](http://msdn.microsoft.com/library/azure/dd179376.aspx).</span></span>

### <a name="how-toocreate-a-container"></a><span data-ttu-id="e3b61-237">Como um contêiner de toocreate</span><span class="sxs-lookup"><span data-stu-id="e3b61-237">How toocreate a container</span></span>
<span data-ttu-id="e3b61-238">Todos os blobs no armazenamento do Azure devem residir em um contêiner.</span><span class="sxs-lookup"><span data-stu-id="e3b61-238">Every blob in Azure storage must be in a container.</span></span> <span data-ttu-id="e3b61-239">Você pode criar um contêiner privado, usando o cmdlet New-AzureStorageContainer de saudação:</span><span class="sxs-lookup"><span data-stu-id="e3b61-239">You can create a private container using hello New-AzureStorageContainer cmdlet:</span></span>

```powershell
$StorageContainerName = "yourcontainername"
New-AzureStorageContainer -Name $StorageContainerName -Permission Off
```

> [!NOTE]
> <span data-ttu-id="e3b61-240">Há três níveis de acesso de leitura anônimo: **Desativado**, **Blob** e **Contêiner**.</span><span class="sxs-lookup"><span data-stu-id="e3b61-240">There are three levels of anonymous read access: **Off**, **Blob**, and **Container**.</span></span> <span data-ttu-id="e3b61-241">tooprevent anônimo acessar tooblobs, Olá permissão parâmetro muito**Off**.</span><span class="sxs-lookup"><span data-stu-id="e3b61-241">tooprevent anonymous access tooblobs, set hello Permission parameter too**Off**.</span></span> <span data-ttu-id="e3b61-242">Por padrão, o novo contêiner de saudação é particular e pode ser acessado somente pelo proprietário da conta hello.</span><span class="sxs-lookup"><span data-stu-id="e3b61-242">By default, hello new container is private and can be accessed only by hello account owner.</span></span> <span data-ttu-id="e3b61-243">público anônimo tooallow leitura tooblob acessar os recursos, mas não toocontainer metadados ou toohello a lista de blobs no contêiner Olá, defina o parâmetro de permissão de saudação muito**Blob**.</span><span class="sxs-lookup"><span data-stu-id="e3b61-243">tooallow anonymous public read access tooblob resources, but not toocontainer metadata or toohello list of blobs in hello container, set hello Permission parameter too**Blob**.</span></span> <span data-ttu-id="e3b61-244">público completo tooallow leitura tooblob acessar os recursos, os metadados de contêiner e lista de saudação de blobs no contêiner de saudação, defina o parâmetro de permissão de saudação muito**contêiner**.</span><span class="sxs-lookup"><span data-stu-id="e3b61-244">tooallow full public read access tooblob resources, container metadata, and hello list of blobs in hello container, set hello Permission parameter too**Container**.</span></span> <span data-ttu-id="e3b61-245">Para obter mais informações, consulte [gerenciar o acesso de leitura anônimo toocontainers e blobs](../blobs/storage-manage-access-to-resources.md).</span><span class="sxs-lookup"><span data-stu-id="e3b61-245">For more information, see [Manage anonymous read access toocontainers and blobs](../blobs/storage-manage-access-to-resources.md).</span></span>
> 
> 

### <a name="how-tooupload-a-blob-into-a-container"></a><span data-ttu-id="e3b61-246">Como tooupload um blob em um contêiner</span><span class="sxs-lookup"><span data-stu-id="e3b61-246">How tooupload a blob into a container</span></span>
<span data-ttu-id="e3b61-247">O Armazenamento de Blob do Azure oferece suporte a blobs de blocos e a blobs de páginas.</span><span class="sxs-lookup"><span data-stu-id="e3b61-247">Azure Blob Storage supports block blobs and page blobs.</span></span> <span data-ttu-id="e3b61-248">Para obter mais informações, confira [Compreendendo Blobs de blocos, Blobs de apêndice e Blobs de páginas](http://msdn.microsoft.com/library/azure/ee691964.aspx).</span><span class="sxs-lookup"><span data-stu-id="e3b61-248">For more information, see [Understanding Block Blobs, Append BLobs, and Page Blobs](http://msdn.microsoft.com/library/azure/ee691964.aspx).</span></span>

<span data-ttu-id="e3b61-249">blobs tooupload tooa contêiner, você pode usar o hello [Set-AzureStorageBlobContent](/powershell/module/azure.storage/set-azurestorageblobcontent) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="e3b61-249">tooupload blobs in tooa container, you can use hello [Set-AzureStorageBlobContent](/powershell/module/azure.storage/set-azurestorageblobcontent) cmdlet.</span></span> <span data-ttu-id="e3b61-250">Por padrão, esse comando carrega o blob de blocos de tooa Olá arquivos locais.</span><span class="sxs-lookup"><span data-stu-id="e3b61-250">By default, this command uploads hello local files tooa block blob.</span></span> <span data-ttu-id="e3b61-251">tipo de saudação toospecify blob hello, você pode usar o parâmetro de - BlobType de saudação.</span><span class="sxs-lookup"><span data-stu-id="e3b61-251">toospecify hello type for hello blob, you can use hello -BlobType parameter.</span></span>

<span data-ttu-id="e3b61-252">exemplo Hello executa Olá [Get-ChildItem](http://technet.microsoft.com/library/hh849800.aspx) tooget cmdlet Olá todos os arquivos na pasta especificada hello e passa-los toohello próximo cmdlet usando o operador de pipeline hello.</span><span class="sxs-lookup"><span data-stu-id="e3b61-252">hello following example runs hello [Get-ChildItem](http://technet.microsoft.com/library/hh849800.aspx) cmdlet tooget all hello files in hello specified folder, and then passes them toohello next cmdlet by using hello pipeline operator.</span></span> <span data-ttu-id="e3b61-253">Olá [Set-AzureStorageBlobContent](/powershell/module/azure.storage/set-azurestorageblobcontent) cmdlet carrega o contêiner de tooyour Olá arquivos locais:</span><span class="sxs-lookup"><span data-stu-id="e3b61-253">hello [Set-AzureStorageBlobContent](/powershell/module/azure.storage/set-azurestorageblobcontent) cmdlet uploads hello local files tooyour container:</span></span>

```powershell
Get-ChildItem –Path C:\Images\* | Set-AzureStorageBlobContent -Container "yourcontainername"
```

### <a name="how-toodownload-blobs-from-a-container"></a><span data-ttu-id="e3b61-254">Como toodownload blobs de um contêiner</span><span class="sxs-lookup"><span data-stu-id="e3b61-254">How toodownload blobs from a container</span></span>
<span data-ttu-id="e3b61-255">saudação de exemplo a seguir demonstra como toodownload blobs de um contêiner.</span><span class="sxs-lookup"><span data-stu-id="e3b61-255">hello following example demonstrates how toodownload blobs from a container.</span></span> <span data-ttu-id="e3b61-256">exemplo Hello primeiro estabelece uma conexão tooAzure armazenamento usando o contexto de conta de armazenamento hello, que inclui o nome de conta de armazenamento hello e sua chave de acesso primário.</span><span class="sxs-lookup"><span data-stu-id="e3b61-256">hello example first establishes a connection tooAzure Storage using hello storage account context, which includes hello storage account name and its primary access key.</span></span> <span data-ttu-id="e3b61-257">Em seguida, o exemplo hello recupera uma referência de blob usando Olá [AzureStorageBlob Get](/powershell/module/azure.storage/get-azurestorageblob) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="e3b61-257">Then, hello example retrieves a blob reference using hello [Get-AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) cmdlet.</span></span> <span data-ttu-id="e3b61-258">Em seguida, o exemplo hello usa Olá [Get-AzureStorageBlobContent](/powershell/module/azure.storage/get-azurestorageblobcontent) blobs do cmdlet toodownload na pasta de destino local hello.</span><span class="sxs-lookup"><span data-stu-id="e3b61-258">Next, hello example uses hello [Get-AzureStorageBlobContent](/powershell/module/azure.storage/get-azurestorageblobcontent) cmdlet toodownload blobs into hello local destination folder.</span></span>

```powershell
#Define hello variables.
$ContainerName = "yourcontainername"
$DestinationFolder = "C:\DownloadImages"

#Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = "Storage key for yourstorageaccount ends with =="
$Ctx = New-AzureStorageContext -StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey

#List all blobs in a container.
$blobs = Get-AzureStorageBlob -Container $ContainerName -Context $Ctx

#Download blobs from a container.
New-Item -Path $DestinationFolder -ItemType Directory -Force
$blobs | Get-AzureStorageBlobContent -Destination $DestinationFolder -Context $Ctx
```

### <a name="how-toocopy-blobs-from-one-storage-container-tooanother"></a><span data-ttu-id="e3b61-259">Como toocopy blobs de um tooanother de contêiner de armazenamento</span><span class="sxs-lookup"><span data-stu-id="e3b61-259">How toocopy blobs from one storage container tooanother</span></span>
<span data-ttu-id="e3b61-260">Você pode copiar blobs em regiões e contas de armazenamento de forma assíncrona.</span><span class="sxs-lookup"><span data-stu-id="e3b61-260">You can copy blobs across storage accounts and regions asynchronously.</span></span> <span data-ttu-id="e3b61-261">Olá exemplo a seguir demonstra como toocopy blobs de armazenamento de um contêiner tooanother em duas contas de armazenamento diferente.</span><span class="sxs-lookup"><span data-stu-id="e3b61-261">hello following example demonstrates how toocopy blobs from one storage container tooanother in two different storage accounts.</span></span> <span data-ttu-id="e3b61-262">exemplo Hello primeiro define variáveis para contas de armazenamento de origem e de destino e, em seguida, cria um contexto de armazenamento para cada conta.</span><span class="sxs-lookup"><span data-stu-id="e3b61-262">hello example first sets variables for source and destination storage accounts, and then creates a storage context for each account.</span></span> <span data-ttu-id="e3b61-263">Em seguida, o exemplo hello copia blobs do contêiner Olá fonte contêiner toohello destino usando Olá [AzureStorageBlobCopy início](/powershell/module/azure.storage/start-azurestorageblobcopy) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="e3b61-263">Next, hello example copies blobs from hello source container toohello destination container using hello [Start-AzureStorageBlobCopy](/powershell/module/azure.storage/start-azurestorageblobcopy) cmdlet.</span></span> <span data-ttu-id="e3b61-264">exemplo Hello pressupõe que contêineres e contas de armazenamento de origem e destino Olá já existem.</span><span class="sxs-lookup"><span data-stu-id="e3b61-264">hello example assumes that hello source and destination storage accounts and containers already exist.</span></span>

```powershell
#Define hello source storage account and context.
$SourceStorageAccountName = "yoursourcestorageaccount"
$SourceStorageAccountKey = "Storage key for yoursourcestorageaccount"
$SrcContainerName = "yoursrccontainername"
$SourceContext = New-AzureStorageContext -StorageAccountName $SourceStorageAccountName -StorageAccountKey $SourceStorageAccountKey

#Define hello destination storage account and context.
$DestStorageAccountName = "yourdeststorageaccount"
$DestStorageAccountKey = "Storage key for yourdeststorageaccount"
$DestContainerName = "destcontainername"
$DestContext = New-AzureStorageContext -StorageAccountName $DestStorageAccountName -StorageAccountKey $DestStorageAccountKey

#Get a reference tooblobs in hello source container.
$blobs = Get-AzureStorageBlob -Container $SrcContainerName -Context $SourceContext

#Copy blobs from one container tooanother.
$blobs| Start-AzureStorageBlobCopy -DestContainer $DestContainerName -DestContext $DestContext
```

<span data-ttu-id="e3b61-265">Observe que este exemplo executa uma cópia assíncrona.</span><span class="sxs-lookup"><span data-stu-id="e3b61-265">Note that this example performs an asynchronous copy.</span></span> <span data-ttu-id="e3b61-266">Você pode monitorar o status de saudação de cada cópia executando Olá [AzureStorageBlobCopyState Get](/powershell/module/azure.storage/start-azurestorageblobcopystate) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="e3b61-266">You can monitor hello status of each copy by running hello [Get-AzureStorageBlobCopyState](/powershell/module/azure.storage/start-azurestorageblobcopystate) cmdlet.</span></span>

### <a name="how-toocopy-blobs-from-a-secondary-location"></a><span data-ttu-id="e3b61-267">Como toocopy blobs de um local secundário</span><span class="sxs-lookup"><span data-stu-id="e3b61-267">How toocopy blobs from a secondary location</span></span>
<span data-ttu-id="e3b61-268">Você pode copiar blobs do local secundário de saudação de uma conta ativada por RA-GRS.</span><span class="sxs-lookup"><span data-stu-id="e3b61-268">You can copy blobs from hello secondary location of a RA-GRS-enabled account.</span></span>

```powershell
#define secondary storage context using a connection string constructed from secondary endpoints.
$SrcContext = New-AzureStorageContext -ConnectionString "DefaultEndpointsProtocol=https;AccountName=***;AccountKey=***;BlobEndpoint=http://***-secondary.blob.core.windows.net;FileEndpoint=http://***-secondary.file.core.windows.net;QueueEndpoint=http://***-secondary.queue.core.windows.net; TableEndpoint=http://***-secondary.table.core.windows.net;"
Start-AzureStorageBlobCopy –Container *** -Blob *** -Context $SrcContext –DestContainer *** -DestBlob *** -DestContext $DestContext
```

### <a name="how-toodelete-a-blob"></a><span data-ttu-id="e3b61-269">Como toodelete um blob</span><span class="sxs-lookup"><span data-stu-id="e3b61-269">How toodelete a blob</span></span>
<span data-ttu-id="e3b61-270">toodelete um blob, primeiro obter uma referência de blob e, em seguida, chamar hello remover AzureStorageBlob cmdlet.</span><span class="sxs-lookup"><span data-stu-id="e3b61-270">toodelete a blob, first get a blob reference and then call hello Remove-AzureStorageBlob cmdlet on it.</span></span> <span data-ttu-id="e3b61-271">saudação de exemplo a seguir exclui todos os blobs de saudação em um contêiner específico.</span><span class="sxs-lookup"><span data-stu-id="e3b61-271">hello following example deletes all hello blobs in a given container.</span></span> <span data-ttu-id="e3b61-272">exemplo Hello primeiro define variáveis para uma conta de armazenamento e, em seguida, cria um contexto de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="e3b61-272">hello example first sets variables for a storage account, and then creates a storage context.</span></span> <span data-ttu-id="e3b61-273">Em seguida, o exemplo hello recupera uma referência de blob usando Olá [Get-AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) Olá cmdlet e executa [AzureStorageBlob remover](/powershell/module/azure.storage/remove-azurestorageblob) cmdlet tooremove blobs de um contêiner no armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="e3b61-273">Next, hello example retrieves a blob reference using hello [Get-AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) cmdlet and runs hello [Remove-AzureStorageBlob](/powershell/module/azure.storage/remove-azurestorageblob) cmdlet tooremove blobs from a container in Azure storage.</span></span>

```powershell
#Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = "Storage key for yourstorageaccount ends with =="
$ContainerName = "containername"
$Ctx = New-AzureStorageContext -StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey

#Get a reference tooall hello blobs in hello container.
$blobs = Get-AzureStorageBlob -Container $ContainerName -Context $Ctx

#Delete blobs in a specified container.
$blobs| Remove-AzureStorageBlob
```

## <a name="how-toomanage-azure-blob-snapshots"></a><span data-ttu-id="e3b61-274">Como instantâneos de blob toomanage do Azure</span><span class="sxs-lookup"><span data-stu-id="e3b61-274">How toomanage Azure blob snapshots</span></span>
<span data-ttu-id="e3b61-275">O Azure permite criar um instantâneo de um blob.</span><span class="sxs-lookup"><span data-stu-id="e3b61-275">Azure lets you create a snapshot of a blob.</span></span> <span data-ttu-id="e3b61-276">Um instantâneo é uma versão somente leitura de um blob capturada em um momento no tempo.</span><span class="sxs-lookup"><span data-stu-id="e3b61-276">A snapshot is a read-only version of a blob that's taken at a point in time.</span></span> <span data-ttu-id="e3b61-277">Quando um instantâneo tiver sido criado, ele pode ser lido, copiado ou excluído, mas não modificado.</span><span class="sxs-lookup"><span data-stu-id="e3b61-277">Once a snapshot has been created, it can be read, copied, or deleted, but not modified.</span></span> <span data-ttu-id="e3b61-278">Os instantâneos fornecem uma tooback de forma a um blob conforme ele aparece em um momento específico.</span><span class="sxs-lookup"><span data-stu-id="e3b61-278">Snapshots provide a way tooback up a blob as it appears at a moment in time.</span></span> <span data-ttu-id="e3b61-279">Para obter mais informações, consulte [Criar um instantâneo de um blob](http://msdn.microsoft.com/library/azure/hh488361.aspx).</span><span class="sxs-lookup"><span data-stu-id="e3b61-279">For more information, see [Creating a Snapshot of a Blob](http://msdn.microsoft.com/library/azure/hh488361.aspx).</span></span>

### <a name="how-toocreate-a-blob-snapshot"></a><span data-ttu-id="e3b61-280">Como toocreate um instantâneo de blob</span><span class="sxs-lookup"><span data-stu-id="e3b61-280">How toocreate a blob snapshot</span></span>
<span data-ttu-id="e3b61-281">toocreate um instantâneo de um blob, primeiro obter uma referência de blob e, em seguida, chamar hello `ICloudBlob.CreateSnapshot` método nele.</span><span class="sxs-lookup"><span data-stu-id="e3b61-281">toocreate a snaphot of a blob, first get a blob reference and then call hello `ICloudBlob.CreateSnapshot` method on it.</span></span> <span data-ttu-id="e3b61-282">Olá exemplo a seguir define primeiramente variáveis para uma conta de armazenamento e, em seguida, cria um contexto de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="e3b61-282">hello following example first sets variables for a storage account, and then creates a storage context.</span></span> <span data-ttu-id="e3b61-283">Em seguida, o exemplo hello recupera uma referência de blob usando Olá [Get-AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) Olá cmdlet e executa [ICloudBlob.CreateSnapshot](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.icloudblob.aspx) método toocreate um instantâneo.</span><span class="sxs-lookup"><span data-stu-id="e3b61-283">Next, hello example retrieves a blob reference using hello [Get-AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) cmdlet and runs hello [ICloudBlob.CreateSnapshot](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.icloudblob.aspx) method toocreate a snapshot.</span></span>

```powershell
#Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = "Storage key for yourstorageaccount ends with =="
$ContainerName = "yourcontainername"
$BlobName = "yourblobname"
$Ctx = New-AzureStorageContext -StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey

#Get a reference tooa blob.
$blob = Get-AzureStorageBlob -Context $Ctx -Container $ContainerName -Blob $BlobName

#Create a snapshot of hello blob.
$snap = $blob.ICloudBlob.CreateSnapshot()
```

### <a name="how-toolist-a-blobs-snapshots"></a><span data-ttu-id="e3b61-284">Como os instantâneos de toolist um blob</span><span class="sxs-lookup"><span data-stu-id="e3b61-284">How toolist a blob's snapshots</span></span>
<span data-ttu-id="e3b61-285">Você pode criar tantos snapshots quanto desejar para um blob.</span><span class="sxs-lookup"><span data-stu-id="e3b61-285">You can create as many snapshots as you want for a blob.</span></span> <span data-ttu-id="e3b61-286">Você pode listar instantâneos Olá associados com o blob tootrack seus instantâneos atuais.</span><span class="sxs-lookup"><span data-stu-id="e3b61-286">You can list hello snapshots associated with your blob tootrack your current snapshots.</span></span> <span data-ttu-id="e3b61-287">Olá, exemplo a seguir usa uma saudação predefinida de blob e chama [AzureStorageBlob Get](/powershell/module/azure.storage/get-azurestorageblob) instantâneos de saudação do cmdlet toolist desse blob.</span><span class="sxs-lookup"><span data-stu-id="e3b61-287">hello following example uses a predefined blob and calls hello [Get-AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) cmdlet toolist hello snapshots of that blob.</span></span>  

```powershell
#Define hello blob name.
$BlobName = "yourblobname"

#List hello snapshots of a blob.
Get-AzureStorageBlob –Context $Ctx -Prefix $BlobName -Container $ContainerName  | Where-Object  { $_.ICloudBlob.IsSnapshot -and $_.Name -eq $BlobName }
```

### <a name="how-toocopy-a-snapshot-of-a-blob"></a><span data-ttu-id="e3b61-288">Como toocopy um instantâneo de um blob</span><span class="sxs-lookup"><span data-stu-id="e3b61-288">How toocopy a snapshot of a blob</span></span>
<span data-ttu-id="e3b61-289">Você pode copiar um instantâneo de um instantâneo do blob toorestore hello.</span><span class="sxs-lookup"><span data-stu-id="e3b61-289">You can copy a snapshot of a blob toorestore hello snapshot.</span></span> <span data-ttu-id="e3b61-290">Para obter informações detalhadas e restrições, consulte [Criar um instantâneo de um Blob](http://msdn.microsoft.com/library/azure/hh488361.aspx).</span><span class="sxs-lookup"><span data-stu-id="e3b61-290">For detailed information and restrictions, see [Creating a Snapshot of a Blob](http://msdn.microsoft.com/library/azure/hh488361.aspx).</span></span> <span data-ttu-id="e3b61-291">Olá exemplo a seguir define primeiramente variáveis para uma conta de armazenamento e, em seguida, cria um contexto de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="e3b61-291">hello following example first sets variables for a storage account, and then creates a storage context.</span></span> <span data-ttu-id="e3b61-292">Em seguida, o exemplo hello define variáveis de nome de contêiner e blob hello.</span><span class="sxs-lookup"><span data-stu-id="e3b61-292">Next, hello example defines hello container and blob name variables.</span></span> <span data-ttu-id="e3b61-293">exemplo Hello recupera uma referência de blob usando Olá [Get-AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) Olá cmdlet e executa [ICloudBlob.CreateSnapshot](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.icloudblob.aspx) método toocreate um instantâneo.</span><span class="sxs-lookup"><span data-stu-id="e3b61-293">hello example retrieves a blob reference using hello [Get-AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) cmdlet and runs hello [ICloudBlob.CreateSnapshot](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.icloudblob.aspx) method toocreate a snapshot.</span></span> <span data-ttu-id="e3b61-294">Em seguida, o exemplo hello executa Olá [AzureStorageBlobCopy início](/powershell/module/azure.storage/start-azurestorageblobcopy) instantâneo de saudação do cmdlet toocopy de um blob usando o objeto de ICloudBlob Olá para o blob de origem hello.</span><span class="sxs-lookup"><span data-stu-id="e3b61-294">Then, hello example runs hello [Start-AzureStorageBlobCopy](/powershell/module/azure.storage/start-azurestorageblobcopy) cmdlet toocopy hello snapshot of a blob using hello ICloudBlob object for hello source blob.</span></span> <span data-ttu-id="e3b61-295">Se tooupdate variáveis de saudação basear-se em sua configuração de exemplo de hello em execução.</span><span class="sxs-lookup"><span data-stu-id="e3b61-295">Be sure tooupdate hello variables based on your configuration before running hello example.</span></span> <span data-ttu-id="e3b61-296">Observe que Olá no exemplo a seguir supõe que Olá contêineres de origem e de destino e o blob de origem Olá já existe.</span><span class="sxs-lookup"><span data-stu-id="e3b61-296">Note that hello following example assumes that hello source and destination containers, and hello source blob already exist.</span></span>

```powershell
#Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = "Storage key for yourstorageaccount ends with =="
$Ctx = New-AzureStorageContext -StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey

#Define hello variables.
$SrcContainerName = "yoursourcecontainername"
$DestContainerName = "yourdestcontainername"
$SrcBlobName = "yourblobname"
$DestBlobName = "CopyBlobName"

#Get a reference tooa blob.
$blob = Get-AzureStorageBlob -Context $Ctx -Container $SrcContainerName -Blob $SrcBlobName

#Create a snapshot of a blob.
$snap = $blob.ICloudBlob.CreateSnapshot()

#Copy hello snapshot tooanother container.
Start-AzureStorageBlobCopy –Context $Ctx -ICloudBlob $snap -DestBlob $DestBlobName -DestContainer $DestContainerName
```

<span data-ttu-id="e3b61-297">Agora que você aprendeu como toomanage Azure blobs e instantâneos com o Azure PowerShell de blob, vá toohello próxima seção toolearn como toomanage tabelas, filas e arquivos.</span><span class="sxs-lookup"><span data-stu-id="e3b61-297">Now that you have learned how toomanage Azure blobs and blob snapshots with Azure PowerShell, go toohello next section toolearn how toomanage tables, queues, and files.</span></span>

## <a name="how-toomanage-azure-tables-and-table-entities"></a><span data-ttu-id="e3b61-298">Como toomanage Azure tabelas e entidades de tabela</span><span class="sxs-lookup"><span data-stu-id="e3b61-298">How toomanage Azure tables and table entities</span></span>
<span data-ttu-id="e3b61-299">Serviço de armazenamento de tabela do Azure é um repositório de dados NoSQL, que você pode usar conjuntos de enorme toostore e consulta de dados estruturados e não relacionais.</span><span class="sxs-lookup"><span data-stu-id="e3b61-299">Azure Table storage service is a NoSQL datastore, which you can use toostore and query huge sets of structured, non-relational data.</span></span> <span data-ttu-id="e3b61-300">Olá principais componentes do serviço de saudação são tabelas, entidades e propriedades.</span><span class="sxs-lookup"><span data-stu-id="e3b61-300">hello main components of hello service are tables, entities, and properties.</span></span> <span data-ttu-id="e3b61-301">Uma tabela é uma coleção de entidades.</span><span class="sxs-lookup"><span data-stu-id="e3b61-301">A table is a collection of entities.</span></span> <span data-ttu-id="e3b61-302">Uma entidade é um conjunto de propriedades.</span><span class="sxs-lookup"><span data-stu-id="e3b61-302">An entity is a set of properties.</span></span> <span data-ttu-id="e3b61-303">Cada entidade pode ter propriedades too252, que são todos os pares nome-valor.</span><span class="sxs-lookup"><span data-stu-id="e3b61-303">Each entity can have up too252 properties, which are all name-value pairs.</span></span> <span data-ttu-id="e3b61-304">Esta seção pressupõe que você já esteja familiarizado com os conceitos do serviço de armazenamento de tabela do Azure hello.</span><span class="sxs-lookup"><span data-stu-id="e3b61-304">This section assumes that you are already familiar with hello Azure Table Storage Service concepts.</span></span> <span data-ttu-id="e3b61-305">Para obter informações detalhadas, consulte [Olá Noções básicas sobre modelo de dados do serviço de tabela](http://msdn.microsoft.com/library/azure/dd179338.aspx) e [Introdução ao armazenamento de tabela do Azure usando o .NET](../../cosmos-db/table-storage-how-to-use-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="e3b61-305">For detailed information, see [Understanding hello Table Service Data Model](http://msdn.microsoft.com/library/azure/dd179338.aspx) and [Get started with Azure Table storage using .NET](../../cosmos-db/table-storage-how-to-use-dotnet.md).</span></span>

<span data-ttu-id="e3b61-306">Olá subseções a seguir, você aprenderá como toomanage armazenamento de tabela do Azure do serviço usando o PowerShell do Azure.</span><span class="sxs-lookup"><span data-stu-id="e3b61-306">In hello following subsections, you'll learn how toomanage Azure Table storage service using Azure PowerShell.</span></span> <span data-ttu-id="e3b61-307">Olá cenários abordados incluem **criando**, **excluindo**, e **recuperar** **tabelas**, bem como **adicionando**, **consultando**, e **excluir entidades de tabela**.</span><span class="sxs-lookup"><span data-stu-id="e3b61-307">hello scenarios covered include **creating**, **deleting**, and **retrieving** **tables**, as well as **adding**, **querying**, and **deleting table entities**.</span></span>

### <a name="how-toocreate-a-table"></a><span data-ttu-id="e3b61-308">Como toocreate uma tabela</span><span class="sxs-lookup"><span data-stu-id="e3b61-308">How toocreate a table</span></span>
<span data-ttu-id="e3b61-309">Cada tabela deve residir em uma conta de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="e3b61-309">Every table must reside in an Azure storage account.</span></span> <span data-ttu-id="e3b61-310">Olá exemplo a seguir demonstra como toocreate uma tabela no armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="e3b61-310">hello following example demonstrates how toocreate a table in Azure Storage.</span></span> <span data-ttu-id="e3b61-311">exemplo Hello primeiro estabelece uma conexão tooAzure armazenamento usando o contexto de conta de armazenamento hello, que inclui o nome de conta de armazenamento hello e sua chave de acesso.</span><span class="sxs-lookup"><span data-stu-id="e3b61-311">hello example first establishes a connection tooAzure Storage using hello storage account context, which includes hello storage account name and its access key.</span></span> <span data-ttu-id="e3b61-312">Em seguida, ele usa Olá [AzureStorageTable novo](/powershell/module/azure.storage/new-azurestoragetable) cmdlet toocreate uma tabela no armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="e3b61-312">Next, it uses hello [New-AzureStorageTable](/powershell/module/azure.storage/new-azurestoragetable) cmdlet toocreate a table in Azure Storage.</span></span>

```powershell
#Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = "Storage key for yourstorageaccount ends with =="
$Ctx = New-AzureStorageContext $StorageAccountName -StorageAccountKey $StorageAccountKey

#Create a new table.
$tabName = "yourtablename"
New-AzureStorageTable –Name $tabName –Context $Ctx
```

### <a name="how-tooretrieve-a-table"></a><span data-ttu-id="e3b61-313">Como tooretrieve uma tabela</span><span class="sxs-lookup"><span data-stu-id="e3b61-313">How tooretrieve a table</span></span>
<span data-ttu-id="e3b61-314">Você pode consultar e recuperar uma ou todas as tabelas em uma conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="e3b61-314">You can query and retrieve one or all tables in a Storage account.</span></span> <span data-ttu-id="e3b61-315">Olá exemplo a seguir demonstra como tooretrieve usando uma determinada tabela Olá [AzureStorageTable Get](/powershell/module/azure.storage/get-azurestoragetable) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="e3b61-315">hello following example demonstrates how tooretrieve a given table using hello [Get-AzureStorageTable](/powershell/module/azure.storage/get-azurestoragetable) cmdlet.</span></span>

```powershell
#Retrieve a table.
$tabName = "yourtablename"
Get-AzureStorageTable –Name $tabName –Context $Ctx
```

<span data-ttu-id="e3b61-316">Se você chamar hello Get-AzureStorageTable cmdlet sem parâmetros, ele obtém todas as tabelas de armazenamento para uma conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="e3b61-316">If you call hello Get-AzureStorageTable cmdlet without any parameters, it gets all storage tables for a Storage account.</span></span>

### <a name="how-toodelete-a-table"></a><span data-ttu-id="e3b61-317">Como toodelete uma tabela</span><span class="sxs-lookup"><span data-stu-id="e3b61-317">How toodelete a table</span></span>
<span data-ttu-id="e3b61-318">Você pode excluir uma tabela de uma conta de armazenamento usando Olá [AzureStorageTable remover](/powershell/module/azure.storage/remove-azurestoragetable) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="e3b61-318">You can delete a table from a storage account by using hello [Remove-AzureStorageTable](/powershell/module/azure.storage/remove-azurestoragetable) cmdlet.</span></span>  

```powershell
#Delete a table.
$tabName = "yourtablename"
Remove-AzureStorageTable –Name $tabName –Context $Ctx
```

### <a name="how-toomanage-table-entities"></a><span data-ttu-id="e3b61-319">Como toomanage tabela entidades</span><span class="sxs-lookup"><span data-stu-id="e3b61-319">How toomanage table entities</span></span>
<span data-ttu-id="e3b61-320">No momento, do PowerShell do Azure não fornece cmdlets toomanage de entidades de tabela diretamente.</span><span class="sxs-lookup"><span data-stu-id="e3b61-320">Currently, Azure PowerShell does not provide cmdlets toomanage table entities directly.</span></span> <span data-ttu-id="e3b61-321">tooperform operações em entidades de tabela, você pode usar classes de saudação fornecidos em Olá [biblioteca de cliente de armazenamento do Azure para .NET](http://msdn.microsoft.com/library/azure/wa_storage_30_reference_home.aspx).</span><span class="sxs-lookup"><span data-stu-id="e3b61-321">tooperform operations on table entities, you can use hello classes given in hello [Azure Storage Client Library for .NET](http://msdn.microsoft.com/library/azure/wa_storage_30_reference_home.aspx).</span></span>

#### <a name="how-tooadd-table-entities"></a><span data-ttu-id="e3b61-322">Como tooadd tabela entidades</span><span class="sxs-lookup"><span data-stu-id="e3b61-322">How tooadd table entities</span></span>
<span data-ttu-id="e3b61-323">tooadd uma tabela de tooa de entidade, primeiro crie um objeto que define as propriedades de entidade.</span><span class="sxs-lookup"><span data-stu-id="e3b61-323">tooadd an entity tooa table, first create an object that defines your entity properties.</span></span> <span data-ttu-id="e3b61-324">Uma entidade pode ter até too255 propriedades, incluindo 3 Propriedades do sistema: **PartitionKey**, **RowKey**, e **Timestamp**.</span><span class="sxs-lookup"><span data-stu-id="e3b61-324">An entity can have up too255 properties, including 3 system properties: **PartitionKey**, **RowKey**, and **Timestamp**.</span></span> <span data-ttu-id="e3b61-325">Você é responsável por inserir e atualizar valores de saudação do **PartitionKey** e **RowKey**.</span><span class="sxs-lookup"><span data-stu-id="e3b61-325">You are responsible for inserting and updating hello values of **PartitionKey** and **RowKey**.</span></span> <span data-ttu-id="e3b61-326">servidor Hello gerencia valor Olá **Timestamp**, que não pode ser modificado.</span><span class="sxs-lookup"><span data-stu-id="e3b61-326">hello server manages hello value of **Timestamp**, which cannot be modified.</span></span> <span data-ttu-id="e3b61-327">Olá junto **PartitionKey** e **RowKey** identificam exclusivamente cada entidade dentro de uma tabela.</span><span class="sxs-lookup"><span data-stu-id="e3b61-327">Together hello **PartitionKey** and **RowKey** uniquely identify every entity within a table.</span></span>

* <span data-ttu-id="e3b61-328">**PartitionKey**: determina partição Olá Olá entidade será armazenada no.</span><span class="sxs-lookup"><span data-stu-id="e3b61-328">**PartitionKey**: Determines hello partition that hello entity is stored in.</span></span>
* <span data-ttu-id="e3b61-329">**RowKey**: identifica exclusivamente a entidade Olá na partição de saudação.</span><span class="sxs-lookup"><span data-stu-id="e3b61-329">**RowKey**: Uniquely identifies hello entity within hello partition.</span></span>

<span data-ttu-id="e3b61-330">Você pode definir as propriedades personalizadas de too252 para uma entidade.</span><span class="sxs-lookup"><span data-stu-id="e3b61-330">You may define up too252 custom properties for an entity.</span></span> <span data-ttu-id="e3b61-331">Para obter mais informações, consulte [Olá Noções básicas sobre modelo de dados do serviço de tabela](http://msdn.microsoft.com/library/azure/dd179338.aspx).</span><span class="sxs-lookup"><span data-stu-id="e3b61-331">For more information, see [Understanding hello Table Service Data Model](http://msdn.microsoft.com/library/azure/dd179338.aspx).</span></span>

<span data-ttu-id="e3b61-332">Olá exemplo a seguir demonstra como tabela de tooa tooadd entidades.</span><span class="sxs-lookup"><span data-stu-id="e3b61-332">hello following example demonstrates how tooadd entities tooa table.</span></span> <span data-ttu-id="e3b61-333">exemplo Hello mostra como tooretrieve Olá tabela employee e adicionar várias entidades para ele.</span><span class="sxs-lookup"><span data-stu-id="e3b61-333">hello example shows how tooretrieve hello employee table and add several entities into it.</span></span> <span data-ttu-id="e3b61-334">Primeiro, ele estabelece uma conexão tooAzure armazenamento usando o contexto de conta de armazenamento hello, que inclui o nome de conta de armazenamento hello e sua chave de acesso.</span><span class="sxs-lookup"><span data-stu-id="e3b61-334">First, it establishes a connection tooAzure Storage using hello storage account context, which includes hello storage account name and its access key.</span></span> <span data-ttu-id="e3b61-335">Em seguida, ele recupera Olá tabela usando Olá [AzureStorageTable Get](/powershell/module/azure.storage/get-azurestoragetable) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="e3b61-335">Next, it retrieves hello given table using hello [Get-AzureStorageTable](/powershell/module/azure.storage/get-azurestoragetable) cmdlet.</span></span> <span data-ttu-id="e3b61-336">Se não existir tabela hello, Olá [AzureStorageTable novo](/powershell/module/azure.storage/new-azurestoragetable) cmdlet é usado toocreate uma tabela no armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="e3b61-336">If hello table does not exist, hello [New-AzureStorageTable](/powershell/module/azure.storage/new-azurestoragetable) cmdlet is used toocreate a table in Azure Storage.</span></span> <span data-ttu-id="e3b61-337">Em seguida, o exemplo hello define uma função personalizada toohello tabela a adicionar entidade tooadd entidades especificando a partição de cada entidade e a chave de linha.</span><span class="sxs-lookup"><span data-stu-id="e3b61-337">Next, hello example defines a custom function Add-Entity tooadd entities toohello table by specifying each entity's partition and row key.</span></span> <span data-ttu-id="e3b61-338">saudação de chamadas de função Hello Adicionar entidade [New-Object](http://technet.microsoft.com/library/hh849885.aspx) cmdlet Olá [Microsoft.WindowsAzure.Storage.Table.DynamicTableEntity](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.dynamictableentity.aspx) toocreate classe um objeto de entidade.</span><span class="sxs-lookup"><span data-stu-id="e3b61-338">hello Add-Entity function calls hello [New-Object](http://technet.microsoft.com/library/hh849885.aspx) cmdlet on hello [Microsoft.WindowsAzure.Storage.Table.DynamicTableEntity](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.dynamictableentity.aspx) class toocreate an entity object.</span></span> <span data-ttu-id="e3b61-339">Posteriormente, o exemplo hello chama Olá [Microsoft.WindowsAzure.Storage.Table.TableOperation.Insert](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.tableoperation.insert.aspx) método essa tooadd de objeto de entidade-tooa tabela.</span><span class="sxs-lookup"><span data-stu-id="e3b61-339">Later, hello example calls hello [Microsoft.WindowsAzure.Storage.Table.TableOperation.Insert](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.tableoperation.insert.aspx) method on this entity object tooadd it tooa table.</span></span>

```powershell
#Function Add-Entity: Adds an employee entity tooa table.
function Add-Entity() {
    [CmdletBinding()]
    param(
       $table,
       [String]$partitionKey,
       [String]$rowKey,
       [String]$name,
       [Int]$id
    )

  $entity = New-Object -TypeName Microsoft.WindowsAzure.Storage.Table.DynamicTableEntity -ArgumentList $partitionKey, $rowKey
  $entity.Properties.Add("Name", $name)
  $entity.Properties.Add("ID", $id)

  $result = $table.CloudTable.Execute([Microsoft.WindowsAzure.Storage.Table.TableOperation]::Insert($entity))
}

#Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
$Ctx = New-AzureStorageContext $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary
$TableName = "Employees"

#Retrieve hello table if it already exists.
$table = Get-AzureStorageTable –Name $TableName -Context $Ctx -ErrorAction Ignore

#Create a new table if it does not exist.
if ($table -eq $null)
{
   $table = New-AzureStorageTable –Name $TableName -Context $Ctx
}

#Add multiple entities tooa table.
Add-Entity -Table $table -PartitionKey Partition1 -RowKey Row1 -Name Chris -Id 1
Add-Entity -Table $table -PartitionKey Partition1 -RowKey Row2 -Name Jessie -Id 2
Add-Entity -Table $table -PartitionKey Partition2 -RowKey Row1 -Name Christine -Id 3
Add-Entity -Table $table -PartitionKey Partition2 -RowKey Row2 -Name Steven -Id 4
```

#### <a name="how-tooquery-table-entities"></a><span data-ttu-id="e3b61-340">Como tooquery tabela entidades</span><span class="sxs-lookup"><span data-stu-id="e3b61-340">How tooquery table entities</span></span>
<span data-ttu-id="e3b61-341">tooquery uma tabela, use Olá [Microsoft.WindowsAzure.Storage.Table.TableQuery](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.tablequery.aspx) classe.</span><span class="sxs-lookup"><span data-stu-id="e3b61-341">tooquery a table, use hello [Microsoft.WindowsAzure.Storage.Table.TableQuery](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.tablequery.aspx) class.</span></span> <span data-ttu-id="e3b61-342">Olá exemplo a seguir supõe que você já tiver executado o script hello fornecido em hello como tooadd seção entidades deste guia.</span><span class="sxs-lookup"><span data-stu-id="e3b61-342">hello following example assumes that you've already run hello script given in hello How tooadd entities section of this guide.</span></span> <span data-ttu-id="e3b61-343">exemplo Hello primeiro estabelece uma conexão tooAzure armazenamento usando o contexto de armazenamento hello, que inclui o nome de conta de armazenamento hello e sua chave de acesso.</span><span class="sxs-lookup"><span data-stu-id="e3b61-343">hello example first establishes a connection tooAzure Storage using hello storage context, which includes hello storage account name and its access key.</span></span> <span data-ttu-id="e3b61-344">Em seguida, ele tenta tooretrieve tabela de "Funcionários" hello criado anteriormente usando Olá [AzureStorageTable Get](/powershell/module/azure.storage/get-azurestoragetable) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="e3b61-344">Next, it tries tooretrieve hello previously created "Employees" table using hello [Get-AzureStorageTable](/powershell/module/azure.storage/get-azurestoragetable) cmdlet.</span></span> <span data-ttu-id="e3b61-345">Olá chamada [New-Object](http://technet.microsoft.com/library/hh849885.aspx) cmdlet Olá Microsoft.WindowsAzure.Storage.Table.TableQuery classe cria um novo objeto de consulta.</span><span class="sxs-lookup"><span data-stu-id="e3b61-345">Calling hello [New-Object](http://technet.microsoft.com/library/hh849885.aspx) cmdlet on hello Microsoft.WindowsAzure.Storage.Table.TableQuery class creates a new query object.</span></span> <span data-ttu-id="e3b61-346">exemplo Hello procura entidades Olá que têm uma coluna de 'ID' cujo valor é 1, conforme especificado em um filtro de cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="e3b61-346">hello example looks for hello entities that have an 'ID' column whose value is 1 as specified in a string filter.</span></span> <span data-ttu-id="e3b61-347">Para obter informações detalhadas, consulte [Consultando tabelas e entidades](http://msdn.microsoft.com/library/azure/dd894031.aspx).</span><span class="sxs-lookup"><span data-stu-id="e3b61-347">For detailed information, see [Querying Tables and Entities](http://msdn.microsoft.com/library/azure/dd894031.aspx).</span></span> <span data-ttu-id="e3b61-348">Quando você executa essa consulta, ele retorna todas as entidades que correspondem aos critérios de filtro de saudação.</span><span class="sxs-lookup"><span data-stu-id="e3b61-348">When you run this query, it returns all entities that match hello filter criteria.</span></span>

```powershell
#Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
$Ctx = New-AzureStorageContext –StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary
$TableName = "Employees"

#Get a reference tooa table.
$table = Get-AzureStorageTable –Name $TableName -Context $Ctx

#Create a table query.
$query = New-Object Microsoft.WindowsAzure.Storage.Table.TableQuery

#Define columns tooselect.
$list = New-Object System.Collections.Generic.List[string]
$list.Add("RowKey")
$list.Add("ID")
$list.Add("Name")

#Set query details.
$query.FilterString = "ID gt 0"
$query.SelectColumns = $list
$query.TakeCount = 20

#Execute hello query.
$entities = $table.CloudTable.ExecuteQuery($query)

#Display entity properties with hello table format.
$entities  | Format-Table PartitionKey, RowKey, @{ Label = "Name"; Expression={$_.Properties["Name"].StringValue}}, @{ Label = "ID"; Expression={$_.Properties["ID"].Int32Value}} -AutoSize
```

#### <a name="how-toodelete-table-entities"></a><span data-ttu-id="e3b61-349">Como toodelete tabela entidades</span><span class="sxs-lookup"><span data-stu-id="e3b61-349">How toodelete table entities</span></span>
<span data-ttu-id="e3b61-350">Você pode excluir uma entidade usando suas chaves de partição e de linha.</span><span class="sxs-lookup"><span data-stu-id="e3b61-350">You can delete an entity using its partition and row keys.</span></span> <span data-ttu-id="e3b61-351">Olá exemplo a seguir supõe que você já tiver executado o script hello fornecido em hello como tooadd seção entidades deste guia.</span><span class="sxs-lookup"><span data-stu-id="e3b61-351">hello following example assumes that you've already run hello script given in hello How tooadd entities section of this guide.</span></span> <span data-ttu-id="e3b61-352">exemplo Hello primeiro estabelece uma conexão tooAzure armazenamento usando o contexto de armazenamento hello, que inclui o nome de conta de armazenamento hello e sua chave de acesso.</span><span class="sxs-lookup"><span data-stu-id="e3b61-352">hello example first establishes a connection tooAzure Storage using hello storage context, which includes hello storage account name and its access key.</span></span> <span data-ttu-id="e3b61-353">Em seguida, ele tenta tooretrieve tabela de "Funcionários" hello criado anteriormente usando Olá [AzureStorageTable Get](/powershell/module/azure.storage/get-azurestoragetable) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="e3b61-353">Next, it tries tooretrieve hello previously created "Employees" table using hello [Get-AzureStorageTable](/powershell/module/azure.storage/get-azurestoragetable) cmdlet.</span></span> <span data-ttu-id="e3b61-354">Se Olá tabela existir, o exemplo hello chama Olá [Microsoft.WindowsAzure.Storage.Table.TableOperation.Retrieve](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.tableoperation.retrieve.aspx) tooretrieve método uma entidade com base em seus valores de chave de partição e de linha.</span><span class="sxs-lookup"><span data-stu-id="e3b61-354">If hello table exists, hello example calls hello [Microsoft.WindowsAzure.Storage.Table.TableOperation.Retrieve](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.tableoperation.retrieve.aspx) method tooretrieve an entity based on its partition and row key values.</span></span> <span data-ttu-id="e3b61-355">Em seguida, passe Olá entidade toohello [Microsoft.WindowsAzure.Storage.Table.TableOperation.Delete](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.tableoperation.delete.aspx) toodelete de método.</span><span class="sxs-lookup"><span data-stu-id="e3b61-355">Then, pass hello entity toohello [Microsoft.WindowsAzure.Storage.Table.TableOperation.Delete](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.tableoperation.delete.aspx) method toodelete.</span></span>

```powershell
#Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
$Ctx = New-AzureStorageContext –StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary

#Retrieve hello table.
$TableName = "Employees"
$table = Get-AzureStorageTable -Name $TableName -Context $Ctx -ErrorAction Ignore

#If hello table exists, start deleting its entities.
if ($table -ne $null) 
{
    #Together hello PartitionKey and RowKey uniquely identify every  
    #entity within a table.
    $tableResult = $table.CloudTable.Execute([Microsoft.WindowsAzure.Storage.Table.TableOperation]::Retrieve("Partition2", "Row1"))
    $entity = $tableResult.Result
    if ($entity -ne $null)
    {
        #Delete hello entity.
        $table.CloudTable.Execute([Microsoft.WindowsAzure.Storage.Table.TableOperation]::Delete($entity))
    }
}
```

## <a name="how-toomanage-azure-queues-and-queue-messages"></a><span data-ttu-id="e3b61-356">Como toomanage Azure as filas e mensagens da fila</span><span class="sxs-lookup"><span data-stu-id="e3b61-356">How toomanage Azure queues and queue messages</span></span>
<span data-ttu-id="e3b61-357">Armazenamento de fila do Azure é um serviço para armazenar grandes quantidades de mensagens que podem ser acessadas de qualquer lugar Olá, mundo por meio de chamadas autenticadas usando HTTP ou HTTPS.</span><span class="sxs-lookup"><span data-stu-id="e3b61-357">Azure Queue storage is a service for storing large numbers of messages that can be accessed from anywhere in hello world via authenticated calls using HTTP or HTTPS.</span></span> <span data-ttu-id="e3b61-358">Esta seção pressupõe que você já esteja familiarizado com os conceitos do serviço de armazenamento de fila do Azure hello.</span><span class="sxs-lookup"><span data-stu-id="e3b61-358">This section assumes that you are already familiar with hello Azure Queue Storage Service concepts.</span></span> <span data-ttu-id="e3b61-359">Para obter informações detalhadas, confira [Introdução ao Armazenamento de Filas do Azure usando o .NET](../storage-dotnet-how-to-use-queues.md).</span><span class="sxs-lookup"><span data-stu-id="e3b61-359">For detailed information, see [Get started with Azure Queue storage using .NET](../storage-dotnet-how-to-use-queues.md).</span></span>

<span data-ttu-id="e3b61-360">Esta seção mostrará como toomanage armazenamento de fila do Azure do serviço usando o PowerShell do Azure.</span><span class="sxs-lookup"><span data-stu-id="e3b61-360">This section will show you how toomanage Azure Queue storage service using Azure PowerShell.</span></span> <span data-ttu-id="e3b61-361">Olá cenários abordados incluem **inserindo** e **excluindo** Enfileirar mensagens, bem como **criando**, **excluindo**e **recuperar filas**.</span><span class="sxs-lookup"><span data-stu-id="e3b61-361">hello scenarios covered include **inserting** and **deleting** queue messages, as well as **creating**, **deleting**, and **retrieving queues**.</span></span>

### <a name="how-toocreate-a-queue"></a><span data-ttu-id="e3b61-362">Como toocreate uma fila</span><span class="sxs-lookup"><span data-stu-id="e3b61-362">How toocreate a queue</span></span>
<span data-ttu-id="e3b61-363">Olá exemplo a seguir primeiro estabelece uma conexão tooAzure armazenamento usando o contexto de conta de armazenamento hello, que inclui o nome de conta de armazenamento hello e sua chave de acesso.</span><span class="sxs-lookup"><span data-stu-id="e3b61-363">hello following example first establishes a connection tooAzure Storage using hello storage account context, which includes hello storage account name and its access key.</span></span> <span data-ttu-id="e3b61-364">Em seguida, ele chama [AzureStorageQueue novo](/powershell/module/azure.storage/new-azurestoragequeue) cmdlet toocreate uma fila denominada 'queuename'.</span><span class="sxs-lookup"><span data-stu-id="e3b61-364">Next, it calls [New-AzureStorageQueue](/powershell/module/azure.storage/new-azurestoragequeue) cmdlet toocreate a queue named 'queuename'.</span></span>

```powershell
#Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
$Ctx = New-AzureStorageContext –StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary
$QueueName = "queuename"
$Queue = New-AzureStorageQueue –Name $QueueName -Context $Ctx
```

<span data-ttu-id="e3b61-365">Para obter informações sobre convenções de nomenclatura do serviço Fila do Azure, consulte [Nomear filas e metadados](http://msdn.microsoft.com/library/azure/dd179349.aspx).</span><span class="sxs-lookup"><span data-stu-id="e3b61-365">For information on naming conventions for Azure Queue Service, see [Naming Queues and Metadata](http://msdn.microsoft.com/library/azure/dd179349.aspx).</span></span>

### <a name="how-tooretrieve-a-queue"></a><span data-ttu-id="e3b61-366">Como tooretrieve uma fila</span><span class="sxs-lookup"><span data-stu-id="e3b61-366">How tooretrieve a queue</span></span>
<span data-ttu-id="e3b61-367">Você pode consultar e recuperar uma lista de todas as filas de saudação em uma conta de armazenamento ou de uma fila específica.</span><span class="sxs-lookup"><span data-stu-id="e3b61-367">You can query and retrieve a specific queue or a list of all hello queues in a Storage account.</span></span> <span data-ttu-id="e3b61-368">Olá exemplo a seguir demonstra como tooretrieve uma fila especificada usando Olá [AzureStorageQueue Get](/powershell/module/azure.storage/get-azurestoragequeue) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="e3b61-368">hello following example demonstrates how tooretrieve a specified queue using hello [Get-AzureStorageQueue](/powershell/module/azure.storage/get-azurestoragequeue) cmdlet.</span></span>

```powershell
#Retrieve a queue.
$QueueName = "queuename"
$Queue = Get-AzureStorageQueue –Name $QueueName –Context $Ctx
```

<span data-ttu-id="e3b61-369">Se você chamar hello [AzureStorageQueue Get](/powershell/module/azure.storage/get-azurestoragequeue) cmdlet sem parâmetros, ele obtém uma lista de todas as filas de saudação.</span><span class="sxs-lookup"><span data-stu-id="e3b61-369">If you call hello [Get-AzureStorageQueue](/powershell/module/azure.storage/get-azurestoragequeue) cmdlet without any parameters, it gets a list of all hello queues.</span></span>

### <a name="how-toodelete-a-queue"></a><span data-ttu-id="e3b61-370">Como toodelete uma fila</span><span class="sxs-lookup"><span data-stu-id="e3b61-370">How toodelete a queue</span></span>
<span data-ttu-id="e3b61-371">toodelete uma fila e todas as mensagens de saudação contidos nele, chamada hello remover AzureStorageQueue cmdlet.</span><span class="sxs-lookup"><span data-stu-id="e3b61-371">toodelete a queue and all hello messages contained in it, call hello Remove-AzureStorageQueue cmdlet.</span></span> <span data-ttu-id="e3b61-372">saudação de exemplo a seguir mostra como toodelete uma fila especificada usando Olá cmdlet Remove-AzureStorageQueue.</span><span class="sxs-lookup"><span data-stu-id="e3b61-372">hello following example shows how toodelete a specified queue using hello Remove-AzureStorageQueue cmdlet.</span></span>

```powershell
#Delete a queue.
$QueueName = "yourqueuename"
Remove-AzureStorageQueue –Name $QueueName –Context $Ctx
```

#### <a name="how-tooinsert-a-message-into-a-queue"></a><span data-ttu-id="e3b61-373">Como tooinsert uma mensagem em uma fila</span><span class="sxs-lookup"><span data-stu-id="e3b61-373">How tooinsert a message into a queue</span></span>
<span data-ttu-id="e3b61-374">tooinsert uma mensagem em uma fila existente, primeiro crie uma nova instância da saudação [Microsoft.WindowsAzure.Storage.Queue.CloudQueueMessage](http://msdn.microsoft.com/library/azure/jj732474.aspx) classe.</span><span class="sxs-lookup"><span data-stu-id="e3b61-374">tooinsert a message into an existing queue, first create a new instance of hello [Microsoft.WindowsAzure.Storage.Queue.CloudQueueMessage](http://msdn.microsoft.com/library/azure/jj732474.aspx) class.</span></span> <span data-ttu-id="e3b61-375">Em seguida, chame Olá [AddMessage](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.addmessage.aspx) método.</span><span class="sxs-lookup"><span data-stu-id="e3b61-375">Next, call hello [AddMessage](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.addmessage.aspx) method.</span></span> <span data-ttu-id="e3b61-376">Um CloudQueueMessage pode ser criado por meio de uma cadeia de caracteres (em formato UTF-8) ou de uma matriz de bytes.</span><span class="sxs-lookup"><span data-stu-id="e3b61-376">A CloudQueueMessage can be created from either a string (in UTF-8 format) or a byte array.</span></span>

<span data-ttu-id="e3b61-377">saudação de exemplo a seguir demonstra como tooadd tooa fila de mensagens.</span><span class="sxs-lookup"><span data-stu-id="e3b61-377">hello following example demonstrates how tooadd message tooa queue.</span></span> <span data-ttu-id="e3b61-378">exemplo Hello primeiro estabelece uma conexão tooAzure armazenamento usando o contexto de conta de armazenamento hello, que inclui o nome de conta de armazenamento hello e sua chave de acesso.</span><span class="sxs-lookup"><span data-stu-id="e3b61-378">hello example first establishes a connection tooAzure Storage using hello storage account context, which includes hello storage account name and its access key.</span></span> <span data-ttu-id="e3b61-379">Em seguida, ele recupera fila especificada de saudação usando Olá [AzureStorageQueue Get](https://msdn.microsoft.com/library/azure/dn806377.aspx) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="e3b61-379">Next, it retrieves hello specified queue using hello [Get-AzureStorageQueue](https://msdn.microsoft.com/library/azure/dn806377.aspx) cmdlet.</span></span> <span data-ttu-id="e3b61-380">Se a fila Olá existir, hello [New-Object](http://technet.microsoft.com/library/hh849885.aspx) cmdlet é usado toocreate uma instância do hello [Microsoft.WindowsAzure.Storage.Queue.CloudQueueMessage](http://msdn.microsoft.com/library/azure/jj732474.aspx) classe.</span><span class="sxs-lookup"><span data-stu-id="e3b61-380">If hello queue exists, hello [New-Object](http://technet.microsoft.com/library/hh849885.aspx) cmdlet is used toocreate an instance of hello [Microsoft.WindowsAzure.Storage.Queue.CloudQueueMessage](http://msdn.microsoft.com/library/azure/jj732474.aspx) class.</span></span> <span data-ttu-id="e3b61-381">Posteriormente, o exemplo hello chama Olá [AddMessage](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.addmessage.aspx) método essa tooadd de objeto de mensagem-fila tooa.</span><span class="sxs-lookup"><span data-stu-id="e3b61-381">Later, hello example calls hello [AddMessage](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.addmessage.aspx) method on this message object tooadd it tooa queue.</span></span> <span data-ttu-id="e3b61-382">Aqui está o código que recupera uma fila e insere a mensagem de saudação 'MessageInfo':</span><span class="sxs-lookup"><span data-stu-id="e3b61-382">Here is code which retrieves a queue and inserts hello message 'MessageInfo':</span></span>

```powershell
#Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
$Ctx = New-AzureStorageContext –StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary

#Retrieve hello queue.
$QueueName = "queuename"
$Queue = Get-AzureStorageQueue -Name $QueueName -Context $ctx

#If hello queue exists, add a new message.
if ($Queue -ne $null) {
   # Create a new message using a constructor of hello CloudQueueMessage class.
   $QueueMessage = New-Object -TypeName Microsoft.WindowsAzure.Storage.Queue.CloudQueueMessage -ArgumentList MessageInfo

   # Add a new message toohello queue.
   $Queue.CloudQueue.AddMessage($QueueMessage)
}
```

#### <a name="how-toode-queue-at-hello-next-message"></a><span data-ttu-id="e3b61-383">Como toode-fila em Olá próxima mensagem</span><span class="sxs-lookup"><span data-stu-id="e3b61-383">How toode-queue at hello next message</span></span>
<span data-ttu-id="e3b61-384">Seu código remove uma mensagem de um fila em duas etapas.</span><span class="sxs-lookup"><span data-stu-id="e3b61-384">Your code de-queues a message from a queue in two steps.</span></span> <span data-ttu-id="e3b61-385">Quando você chama Olá [Microsoft.WindowsAzure.Storage.Queue.CloudQueue.GetMessage](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.getmessage.aspx) método, você obter próxima mensagem de saudação em uma fila.</span><span class="sxs-lookup"><span data-stu-id="e3b61-385">When you call hello [Microsoft.WindowsAzure.Storage.Queue.CloudQueue.GetMessage](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.getmessage.aspx) method, you get hello next message in a queue.</span></span> <span data-ttu-id="e3b61-386">Uma mensagem retornada de **GetMessage** se torna invisível tooany outro código de leitura de mensagens dessa fila.</span><span class="sxs-lookup"><span data-stu-id="e3b61-386">A message returned from **GetMessage** becomes invisible tooany other code reading messages from this queue.</span></span> <span data-ttu-id="e3b61-387">toofinish mensagem de saudação remover da fila hello, você também deve chamar hello [Microsoft.WindowsAzure.Storage.Queue.CloudQueue.DeleteMessage](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.deletemessage.aspx) método.</span><span class="sxs-lookup"><span data-stu-id="e3b61-387">toofinish removing hello message from hello queue, you must also call hello [Microsoft.WindowsAzure.Storage.Queue.CloudQueue.DeleteMessage](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.deletemessage.aspx) method.</span></span> <span data-ttu-id="e3b61-388">Esse processo de duas etapas de remoção de uma mensagem garante que se seu código falha tooprocess que uma mensagem devido a falha de toohardware ou software, outra instância do seu código pode obter Olá a mesma mensagem e tente novamente.</span><span class="sxs-lookup"><span data-stu-id="e3b61-388">This two-step process of removing a message assures that if your code fails tooprocess a message due toohardware or software failure, another instance of your code can get hello same message and try again.</span></span> <span data-ttu-id="e3b61-389">Seu código chama **DeleteMessage** logo depois que a mensagem de saudação foi processada.</span><span class="sxs-lookup"><span data-stu-id="e3b61-389">Your code calls **DeleteMessage** right after hello message has been processed.</span></span>

```powershell
# Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
$Ctx = New-AzureStorageContext –StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary

# Retrieve hello queue.
$QueueName = "queuename"
$Queue = Get-AzureStorageQueue -Name $QueueName -Context $ctx

$InvisibleTimeout = [System.TimeSpan]::FromSeconds(10)

# Get hello message object from hello queue.
$QueueMessage = $Queue.CloudQueue.GetMessage($InvisibleTimeout)
# Delete hello message.
$Queue.CloudQueue.DeleteMessage($QueueMessage)
```

## <a name="how-toomanage-azure-file-shares-and-files"></a><span data-ttu-id="e3b61-390">Como toomanage arquivo Azure compartilhamentos e arquivos</span><span class="sxs-lookup"><span data-stu-id="e3b61-390">How toomanage Azure file shares and files</span></span>
<span data-ttu-id="e3b61-391">Armazenamento de arquivo do Azure oferece armazenamento compartilhado para aplicativos que usam protocolo SMB padrão de saudação.</span><span class="sxs-lookup"><span data-stu-id="e3b61-391">Azure File storage offers shared storage for applications using hello standard SMB protocol.</span></span> <span data-ttu-id="e3b61-392">Serviços de nuvem e máquinas virtuais do Microsoft Azure podem compartilhar dados de arquivo entre componentes de aplicativos por meio de compartilhamentos montados e aplicativos locais podem acessar dados de arquivo em um compartilhamento via API de armazenamento do arquivo hello ou o Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e3b61-392">Microsoft Azure virtual machines and cloud services can share file data across application components via mounted shares, and on-premises applications can access file data in a share via hello File storage API or Azure PowerShell.</span></span>

<span data-ttu-id="e3b61-393">Para obter mais informações sobre o armazenamento de Arquivos do Azure, confira [Introdução ao Armazenamento de Arquivos do Azure no Windows](../storage-dotnet-how-to-use-files.md) e [File Service REST API](http://msdn.microsoft.com/library/azure/dn167006.aspx) (API REST do serviço Arquivo).</span><span class="sxs-lookup"><span data-stu-id="e3b61-393">For more information on Azure File storage, see [Get started with Azure File storage on Windows](../storage-dotnet-how-to-use-files.md) and [File Service REST API](http://msdn.microsoft.com/library/azure/dn167006.aspx).</span></span>

## <a name="how-tooset-and-query-storage-analytics"></a><span data-ttu-id="e3b61-394">Como tooset e consulta de análise de armazenamento</span><span class="sxs-lookup"><span data-stu-id="e3b61-394">How tooset and query storage analytics</span></span>
<span data-ttu-id="e3b61-395">Você pode usar [Azure Storage Analytics](../storage-analytics.md) toocollect métricas para suas contas de armazenamento do Azure e dados de log sobre solicitações enviadas tooyour conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="e3b61-395">You can use [Azure Storage Analytics](../storage-analytics.md) toocollect metrics for your Azure storage accounts and log data about requests sent tooyour storage account.</span></span> <span data-ttu-id="e3b61-396">Você pode usar a integridade do armazenamento métricas toomonitor saudação de uma conta de armazenamento e armazenamento toodiagnose de registro em log e solucionar problemas com sua conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="e3b61-396">You can use storage metrics toomonitor hello health of a storage account, and storage logging toodiagnose and troubleshoot issues with your storage account.</span></span> <span data-ttu-id="e3b61-397">Você pode configurar o monitoramento usando Olá portal do Azure ou o Windows PowerShell ou programaticamente usando a biblioteca de cliente de armazenamento hello.</span><span class="sxs-lookup"><span data-stu-id="e3b61-397">You can configure monitoring using hello Azure portal or Windows PowerShell, or programmatically using hello storage client library.</span></span> <span data-ttu-id="e3b61-398">O log de armazenamento ocorre no lado do servidor e permite que você toorecord detalhes de solicitações bem-sucedidas e com falhas na conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="e3b61-398">Storage logging happens server-side and enables you toorecord details for both successful and failed requests in your storage account.</span></span> <span data-ttu-id="e3b61-399">Esses logs o habilitam toosee detalhes de leitura, gravação e operações de exclusão em relação a tabelas, filas e blobs bem como motivos Olá para solicitações com falha.</span><span class="sxs-lookup"><span data-stu-id="e3b61-399">These logs enable you toosee details of read, write, and delete operations against your tables, queues, and blobs as well as hello reasons for failed requests.</span></span>

<span data-ttu-id="e3b61-400">toolearn como tooenable e exibir dados de métricas de armazenamento usando o PowerShell, consulte [como tooenable as métricas de armazenamento usando o PowerShell](http://msdn.microsoft.com/library/azure/dn782843.aspx#HowtoenableStorageMetricsusingPowerShell).</span><span class="sxs-lookup"><span data-stu-id="e3b61-400">toolearn how tooenable and view Storage Metrics data using PowerShell, see [How tooenable Storage Metrics using PowerShell](http://msdn.microsoft.com/library/azure/dn782843.aspx#HowtoenableStorageMetricsusingPowerShell).</span></span>

<span data-ttu-id="e3b61-401">toolearn como tooenable e recuperar o log de armazenamento de dados usando o PowerShell, consulte [como tooenable armazenamento de log usando o PowerShell](http://msdn.microsoft.com/library/azure/dn782840.aspx#HowtoenableStorageLoggingusingPowerShell) e [localizar os dados de log do log de armazenamento](http://msdn.microsoft.com/library/azure/dn782840.aspx#FindingyourStorageLogginglogdata).</span><span class="sxs-lookup"><span data-stu-id="e3b61-401">toolearn how tooenable and retrieve Storage Logging data using PowerShell, see [How tooenable Storage Logging using PowerShell](http://msdn.microsoft.com/library/azure/dn782840.aspx#HowtoenableStorageLoggingusingPowerShell) and [Finding your Storage Logging log data](http://msdn.microsoft.com/library/azure/dn782840.aspx#FindingyourStorageLogginglogdata).</span></span>
<span data-ttu-id="e3b61-402">Para obter informações detalhadas sobre o uso de métricas de armazenamento e tootroubleshoot problemas de armazenamento de log de armazenamento, consulte [monitorando, diagnosticando e Solucionando problemas de armazenamento do Microsoft Azure](../storage-monitoring-diagnosing-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="e3b61-402">For detailed information on using Storage Metrics and Storage Logging tootroubleshoot storage issues, see [Monitoring, Diagnosing, and Troubleshooting Microsoft Azure Storage](../storage-monitoring-diagnosing-troubleshooting.md).</span></span>

## <a name="how-toomanage-shared-access-signature-sas-and-stored-access-policy"></a><span data-ttu-id="e3b61-403">Como toomanage compartilhado (SAS) de assinatura de acesso e política de acesso armazenada</span><span class="sxs-lookup"><span data-stu-id="e3b61-403">How toomanage Shared Access Signature (SAS) and Stored Access Policy</span></span>
<span data-ttu-id="e3b61-404">Assinaturas de acesso compartilhado são uma parte importante do modelo de segurança Olá para qualquer aplicativo usando o armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="e3b61-404">Shared access signatures are an important part of hello security model for any application using Azure Storage.</span></span> <span data-ttu-id="e3b61-405">Eles são úteis para fornecer permissões limitadas tooyour armazenamento conta tooclients que não deve ter a chave da conta hello.</span><span class="sxs-lookup"><span data-stu-id="e3b61-405">They are useful for providing limited permissions tooyour storage account tooclients that should not have hello account key.</span></span> <span data-ttu-id="e3b61-406">Por padrão, somente o proprietário de Olá da conta de armazenamento Olá pode acessar blobs, tabelas e filas nessa conta.</span><span class="sxs-lookup"><span data-stu-id="e3b61-406">By default, only hello owner of hello storage account may access blobs, tables, and queues within that account.</span></span> <span data-ttu-id="e3b61-407">Se seu aplicativo ou serviço precisa toomake esses clientes tooother disponíveis de recursos sem compartilhar sua chave de acesso, você terá três opções:</span><span class="sxs-lookup"><span data-stu-id="e3b61-407">If your service or application needs toomake these resources available tooother clients without sharing your access key, you have three options:</span></span>

* <span data-ttu-id="e3b61-408">Defina o contêiner de toohello do contêiner permissões toopermit acesso de leitura anônimo e seus blobs.</span><span class="sxs-lookup"><span data-stu-id="e3b61-408">Set a container's permissions toopermit anonymous read access toohello container and its blobs.</span></span> <span data-ttu-id="e3b61-409">Isso não é permitido para tabelas ou filas.</span><span class="sxs-lookup"><span data-stu-id="e3b61-409">This is not allowed for tables or queues.</span></span>
* <span data-ttu-id="e3b61-410">Use uma assinatura de acesso compartilhado que concede toocontainers de direitos de acesso restrito, blobs, filas e tabelas para um intervalo de tempo específico.</span><span class="sxs-lookup"><span data-stu-id="e3b61-410">Use a shared access signature that grants restricted access rights toocontainers, blobs, queues, and tables for a specific time interval.</span></span>
* <span data-ttu-id="e3b61-411">Use uma política de acesso armazenada tooobtain um nível adicional de controle sobre assinaturas de acesso compartilhado para um contêiner ou seus blobs, para uma fila ou de uma tabela.</span><span class="sxs-lookup"><span data-stu-id="e3b61-411">Use a stored access policy tooobtain an additional level of control over shared access signatures for a container or its blobs, for a queue, or for a table.</span></span> <span data-ttu-id="e3b61-412">Olá política de acesso armazenado permite que você toochange a hora de início hello, tempo de expiração ou permissões para uma assinatura, ou toorevoke-lo depois que ele tiver sido emitida.</span><span class="sxs-lookup"><span data-stu-id="e3b61-412">hello stored access policy allows you toochange hello start time, expiry time, or permissions for a signature, or toorevoke it after it has been issued.</span></span>

<span data-ttu-id="e3b61-413">Uma assinatura de acesso compartilhado pode estar em uma das duas formas:</span><span class="sxs-lookup"><span data-stu-id="e3b61-413">A shared access signature can be in one of two forms:</span></span>

* <span data-ttu-id="e3b61-414">**SAS ad-hoc**: quando você cria um SAS ad hoc, a hora de início de saudação, o tempo de expiração e permissões para Olá SAS são especificadas em Olá URI SAS.</span><span class="sxs-lookup"><span data-stu-id="e3b61-414">**Ad hoc SAS**: When you create an ad hoc SAS, hello start time, expiry time, and permissions for hello SAS are all specified on hello SAS URI.</span></span> <span data-ttu-id="e3b61-415">Esse tipo de SAS pode ser criado em um contêiner, blob, tabela ou fila e não pode ser revogado.</span><span class="sxs-lookup"><span data-stu-id="e3b61-415">This type of SAS may be created on a container, blob, table, or queue and it is non-revocable.</span></span>
* <span data-ttu-id="e3b61-416">**SAS com a política de acesso armazenada**: uma política de acesso armazenada é definida em um contêiner de recursos um contêiner de blob, tabela ou fila - e você pode usá-lo toomanage restrições para uma ou mais assinaturas de acesso compartilhado.</span><span class="sxs-lookup"><span data-stu-id="e3b61-416">**SAS with stored access policy**: A stored access policy is defined on a resource container a blob container, table, or queue - and you can use it toomanage constraints for one or more shared access signatures.</span></span> <span data-ttu-id="e3b61-417">Quando você associa uma SAS com uma política de acesso armazenada, Olá SAS herda restrições Olá - Olá hora de início, hora de expiração e permissões - definidas para a política de acesso Olá armazenado.</span><span class="sxs-lookup"><span data-stu-id="e3b61-417">When you associate a SAS with a stored access policy, hello SAS inherits hello constraints - hello start time, expiry time, and permissions - defined for hello stored access policy.</span></span> <span data-ttu-id="e3b61-418">Esse tipo de SAS pode ser revogado.</span><span class="sxs-lookup"><span data-stu-id="e3b61-418">This type of SAS is revocable.</span></span>

<span data-ttu-id="e3b61-419">Para obter mais informações, consulte [usando assinaturas (SAS de acesso compartilhado)](../storage-dotnet-shared-access-signature-part-1.md) e [gerenciar o acesso de leitura anônimo toocontainers e blobs](../blobs/storage-manage-access-to-resources.md).</span><span class="sxs-lookup"><span data-stu-id="e3b61-419">For more information, see [Using Shared Access Signatures (SAS)](../storage-dotnet-shared-access-signature-part-1.md) and [Manage anonymous read access toocontainers and blobs](../blobs/storage-manage-access-to-resources.md).</span></span>

<span data-ttu-id="e3b61-420">Seções a seguir hello, você aprenderá como toocreate uma política de acesso armazenado e token de assinatura de acesso compartilhado para tabelas do Azure.</span><span class="sxs-lookup"><span data-stu-id="e3b61-420">In hello next sections, you will learn how toocreate a shared access signature token and stored access policy for Azure tables.</span></span> <span data-ttu-id="e3b61-421">O PowerShell do Azure fornece cmdlets semelhantes para contêineres, blobs e filas.</span><span class="sxs-lookup"><span data-stu-id="e3b61-421">Azure PowerShell provides similar cmdlets for containers, blobs, and queues as well.</span></span> <span data-ttu-id="e3b61-422">scripts de saudação toorun nesta seção, faça o download Olá [Azure PowerShell versão 0.8.14](http://go.microsoft.com/?linkid=9811175&clcid=0x409) ou posterior.</span><span class="sxs-lookup"><span data-stu-id="e3b61-422">toorun hello scripts in this section, download hello [Azure PowerShell version 0.8.14](http://go.microsoft.com/?linkid=9811175&clcid=0x409) or later.</span></span>

### <a name="how-toocreate-a-policy-based-shared-access-signature-token"></a><span data-ttu-id="e3b61-423">Como toocreate uma política com base em token de assinatura de acesso compartilhado</span><span class="sxs-lookup"><span data-stu-id="e3b61-423">How toocreate a policy-based Shared Access Signature token</span></span>
<span data-ttu-id="e3b61-424">Use Olá AzureStorageTableStoredAccessPolicy novo cmdlet toocreate uma nova política de acesso armazenada.</span><span class="sxs-lookup"><span data-stu-id="e3b61-424">Use hello New-AzureStorageTableStoredAccessPolicy cmdlet toocreate a new stored access policy.</span></span> <span data-ttu-id="e3b61-425">Em seguida, chame Olá [AzureStorageTableSASToken novo](/powershell/module/azure.storage/new-azurestoragetablesastoken) cmdlet toocreate um novo token de assinatura com base na política de acesso compartilhado para uma tabela de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="e3b61-425">Then, call hello [New-AzureStorageTableSASToken](/powershell/module/azure.storage/new-azurestoragetablesastoken) cmdlet toocreate a new policy-based shared access signature token for an Azure Storage table.</span></span>

```powershell
$policy = "policy1"
New-AzureStorageTableStoredAccessPolicy -Name $tableName -Policy $policy -Permission "rd" -StartTime "2015-01-01" -ExpiryTime "2016-01-01" -Context $Ctx
New-AzureStorageTableSASToken -Name $tableName -Policy $policy -Context $Ctx
```

### <a name="how-toocreate-an-ad-hoc-non-revocable-shared-access-signature-token"></a><span data-ttu-id="e3b61-426">Como toocreate um token de assinatura de acesso compartilhado (não revogável) ad hoc</span><span class="sxs-lookup"><span data-stu-id="e3b61-426">How toocreate an ad hoc (non-revocable) Shared Access Signature token</span></span>
<span data-ttu-id="e3b61-427">Saudação de uso [AzureStorageTableSASToken novo](/powershell/module/azure.storage/new-azurestoragetablesastoken) cmdlet toocreate um novo ad hoc (não revogável) token SAS para uma tabela de armazenamento do Azure:</span><span class="sxs-lookup"><span data-stu-id="e3b61-427">Use hello [New-AzureStorageTableSASToken](/powershell/module/azure.storage/new-azurestoragetablesastoken) cmdlet toocreate a new ad hoc (non-revocable) Shared Access Signature token for an Azure Storage table:</span></span>

```powershell
New-AzureStorageTableSASToken -Name $tableName -Permission "rqud" -StartTime "2015-01-01" -ExpiryTime "2015-02-01" -Context $Ctx
```
    
### <a name="how-toocreate-a-stored-access-policy"></a><span data-ttu-id="e3b61-428">Como toocreate uma política de acesso armazenada</span><span class="sxs-lookup"><span data-stu-id="e3b61-428">How toocreate a stored access policy</span></span>
<span data-ttu-id="e3b61-429">Use Olá AzureStorageTableStoredAccessPolicy novo cmdlet toocreate uma nova política de acesso armazenadas para uma tabela de armazenamento do Azure:</span><span class="sxs-lookup"><span data-stu-id="e3b61-429">Use hello New-AzureStorageTableStoredAccessPolicy cmdlet toocreate a new stored access policy for an Azure Storage table:</span></span>

```powershell
$policy = "policy1"
New-AzureStorageTableStoredAccessPolicy -Name $tableName -Policy $policy -Permission "rd" -StartTime "2015-01-01" -ExpiryTime "2016-01-01" -Context $Ctx
```
    
### <a name="how-tooupdate-a-stored-access-policy"></a><span data-ttu-id="e3b61-430">Como tooupdate uma política de acesso armazenada</span><span class="sxs-lookup"><span data-stu-id="e3b61-430">How tooupdate a stored access policy</span></span>
<span data-ttu-id="e3b61-431">Use Olá conjunto AzureStorageTableStoredAccessPolicy cmdlet tooupdate uma política de acesso armazenada existente para uma tabela de armazenamento do Azure:</span><span class="sxs-lookup"><span data-stu-id="e3b61-431">Use hello Set-AzureStorageTableStoredAccessPolicy cmdlet tooupdate an existing stored access policy for an Azure Storage table:</span></span>

```powershell
Set-AzureStorageTableStoredAccessPolicy -Policy $policy -Table $tableName -Permission "rd" -NoExpiryTime -NoStartTime -Context $Ctx
```

### <a name="how-toodelete-a-stored-access-policy"></a><span data-ttu-id="e3b61-432">Como toodelete uma política de acesso armazenada</span><span class="sxs-lookup"><span data-stu-id="e3b61-432">How toodelete a stored access policy</span></span>
<span data-ttu-id="e3b61-433">Use toodelete de cmdlet Olá AzureStorageTableStoredAccessPolicy remover uma política de acesso armazenada em uma tabela de armazenamento do Azure:</span><span class="sxs-lookup"><span data-stu-id="e3b61-433">Use hello Remove-AzureStorageTableStoredAccessPolicy cmdlet toodelete a stored access policy on an Azure Storage table:</span></span>

```powershell
Remove-AzureStorageTableStoredAccessPolicy -Policy $policy -Table $tableName -Context $Ctx
```

## <a name="how-toouse-azure-storage-for-us-government-and-azure-china"></a><span data-ttu-id="e3b61-434">Como toouse o armazenamento do Azure para governo dos Estados Unidos e do Azure na China</span><span class="sxs-lookup"><span data-stu-id="e3b61-434">How toouse Azure Storage for U.S. government and Azure China</span></span>
<span data-ttu-id="e3b61-435">Um ambiente do Azure é uma implantação independente do Microsoft Azure, como [Governo do Azure para o governo dos EUA](https://azure.microsoft.com/features/gov/), [AzureCloud para Azure global](https://portal.azure.com) e [AzureChinaCloud para o Azure operado pela 21Vianet](http://www.windowsazure.cn/) na China.</span><span class="sxs-lookup"><span data-stu-id="e3b61-435">An Azure environment is an independent deployment of Microsoft Azure, such as [Azure Government for U.S. government](https://azure.microsoft.com/features/gov/), [AzureCloud for global Azure](https://portal.azure.com), and [AzureChinaCloud for Azure operated by 21Vianet in China](http://www.windowsazure.cn/).</span></span> <span data-ttu-id="e3b61-436">Você pode implantar novos ambientes do Azure para o governo dos EUA e Azure China.</span><span class="sxs-lookup"><span data-stu-id="e3b61-436">You can deploy new Azure environments for U.S government and Azure China.</span></span>

<span data-ttu-id="e3b61-437">toouse armazenamento do Azure com AzureChinaCloud, é necessário toocreate um contexto de armazenamento que está associado a AzureChinaCloud.</span><span class="sxs-lookup"><span data-stu-id="e3b61-437">toouse Azure Storage with AzureChinaCloud, you need toocreate a storage context that is associated with AzureChinaCloud.</span></span> <span data-ttu-id="e3b61-438">Siga essas tooget etapas é iniciado:</span><span class="sxs-lookup"><span data-stu-id="e3b61-438">Follow these steps tooget you started:</span></span>

1. <span data-ttu-id="e3b61-439">Executar Olá [Get-AzureEnvironment](/powershell/module/azure/get-azureenvironment?view=azuresmps-3.7.0) toosee cmdlet Olá ambientes do Azure disponíveis:</span><span class="sxs-lookup"><span data-stu-id="e3b61-439">Run hello [Get-AzureEnvironment](/powershell/module/azure/get-azureenvironment?view=azuresmps-3.7.0) cmdlet toosee hello available Azure environments:</span></span>
   
    ```powershell
    Get-AzureEnvironment
    ```

2. <span data-ttu-id="e3b61-440">Adicione uma conta do Azure na China tooWindows PowerShell:</span><span class="sxs-lookup"><span data-stu-id="e3b61-440">Add an Azure China account tooWindows PowerShell:</span></span>
   
    ```powershell
    Add-AzureAccount –Environment AzureChinaCloud
    ```

3. <span data-ttu-id="e3b61-441">Crie um contexto de armazenamento para uma conta de AzureChinaCloud:</span><span class="sxs-lookup"><span data-stu-id="e3b61-441">Create a storage context for an AzureChinaCloud account:</span></span>
   
    ```powershell
    $Ctx = New-AzureStorageContext -StorageAccountName $AccountName -StorageAccountKey $AccountKey> -Environment AzureChinaCloud
    ```

<span data-ttu-id="e3b61-442">toouse armazenamento do Azure com [dos EUA dos EUA](https://azure.microsoft.com/features/gov/), você deve definir um novo ambiente e, em seguida, criar um novo contexto de armazenamento com esse ambiente:</span><span class="sxs-lookup"><span data-stu-id="e3b61-442">toouse Azure Storage with [U.S. Azure Government](https://azure.microsoft.com/features/gov/), you should define a new environment and then create a new storage context with this environment:</span></span>

1. <span data-ttu-id="e3b61-443">Executar Olá [Get-AzureEnvironment](/powershell/module/azure/get-azureenvironment?view=azuresmps-3.7.0) toosee cmdlet Olá ambientes do Azure disponíveis:</span><span class="sxs-lookup"><span data-stu-id="e3b61-443">Run hello [Get-AzureEnvironment](/powershell/module/azure/get-azureenvironment?view=azuresmps-3.7.0) cmdlet toosee hello available Azure environments:</span></span>

    ```powershell
    Get-AzureEnvironment
    ```

2. <span data-ttu-id="e3b61-444">Adicione uma conta de Azure US Government tooWindows PowerShell:</span><span class="sxs-lookup"><span data-stu-id="e3b61-444">Add an Azure US Government account tooWindows PowerShell:</span></span>
   
    ```powershell
    Add-AzureAccount –Environment AzureUSGovernment
    ```

3. <span data-ttu-id="e3b61-445">Crie um contexto de armazenamento para uma conta do AzureUSGovernment:</span><span class="sxs-lookup"><span data-stu-id="e3b61-445">Create a storage context for an AzureUSGovernment account:</span></span>
   
    ```powershell
    $Ctx = New-AzureStorageContext -StorageAccountName $AccountName -StorageAccountKey $AccountKey> -Environment AzureUSGovernment
    ```
     
<span data-ttu-id="e3b61-446">Para obter mais informações, consulte:</span><span class="sxs-lookup"><span data-stu-id="e3b61-446">For more information, see:</span></span>

* <span data-ttu-id="e3b61-447">[Guia do Desenvolvedor do Microsoft Azure Government](../../azure-government/documentation-government-developer-guide.md).</span><span class="sxs-lookup"><span data-stu-id="e3b61-447">[Microsoft Azure Government Developer Guide](../../azure-government/documentation-government-developer-guide.md).</span></span>
* [<span data-ttu-id="e3b61-448">Visão geral das diferenças ao criar um aplicativo no serviço na China</span><span class="sxs-lookup"><span data-stu-id="e3b61-448">Overview of Differences When Creating an Application on China Service</span></span>](https://msdn.microsoft.com/library/azure/dn578439.aspx)

## <a name="next-steps"></a><span data-ttu-id="e3b61-449">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="e3b61-449">Next Steps</span></span>
<span data-ttu-id="e3b61-450">Neste guia, você aprendeu como toomanage armazenamento do Azure com o Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e3b61-450">In this guide, you've learned how toomanage Azure Storage with Azure PowerShell.</span></span> <span data-ttu-id="e3b61-451">Estes são alguns artigos e recursos relacionados para saber mais sobre eles.</span><span class="sxs-lookup"><span data-stu-id="e3b61-451">Here are some related articles and resources for learning more about them.</span></span>

* [<span data-ttu-id="e3b61-452">Documentação do Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="e3b61-452">Azure Storage Documentation</span></span>](https://azure.microsoft.com/documentation/services/storage/)
* [<span data-ttu-id="e3b61-453">Cmdlets do PowerShell do Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="e3b61-453">Azure Storage PowerShell Cmdlets</span></span>](/powershell/module/azurerm.storage/#storage)
* [<span data-ttu-id="e3b61-454">Referência do Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="e3b61-454">Windows PowerShell Reference</span></span>](https://msdn.microsoft.com/library/ms714469.aspx)

[Getting started with Azure Storage and PowerShell in 5 minutes]: #getstart
[Prerequisites for using Azure PowerShell with Azure Storage]: #pre
[How toomanage storage accounts in Azure]: #manageaccount
[How tooset a default Azure subscription]: #setdefsub
[How toocreate a new Azure storage account]: #createaccount
[How tooset a default Azure storage account]: #defaultaccount
[How toolist all Azure storage accounts in a subscription]: #listaccounts
[How toocreate an Azure storage context]: #createctx
[How toomanage Azure blobs and blob snapshots]: #manageblobs
[How toocreate a container]: #container
[How tooupload a blob into a container]: #uploadblob
[How toodownload blobs from a container]: #downblob
[How toocopy blobs from one storage container tooanother]: #copyblob
[How toodelete a blob]: #deleteblob
[How toomanage Azure blob snapshots]: #manageshots
[How toocreate a blob snapshot]: #createshot
[How toolist snapshots of a blob]: #listshot
[How toocopy a snapshot of a blob]: #copyshot
[How toomanage Azure tables and table entities]: #managetables
[How toocreate a table]: #createtable
[How tooretrieve a table]: #gettable
[How toodelete a table]: #remtable
[How toomanage table entities]: #mngentity
[How tooadd table entities]: #addentity
[How tooquery table entities]: #queryentity
[How toodelete table entities]: #deleteentity
[How toomanage Azure queues and queue messages]: #managequeues
[How toocreate a queue]: #createqueue
[How tooretrieve a queue]: #getqueue
[How toodelete a queue]: #remqueue
[How toomanage queue messages]: #mngqueuemsg
[How tooinsert a message into a queue]: #addqueuemsg
[How toode-queue at hello next message]: #dequeuemsg
[How toomanage Azure file shares and files]: #files
[How tooset and query storage analytics]: #stganalytics
[How toomanage Shared Access Signature (SAS) and Stored Access Policy]: #sas
[How toouse Azure Storage for U.S. government and Azure China]: #gov
[Next Steps]: #next
