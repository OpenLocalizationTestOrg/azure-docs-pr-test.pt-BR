---
title: Usando o Azure PowerShell com o Armazenamento do Azure | Microsoft Docs
description: "Aprenda a usar os cmdlets do PowerShell do Azure para Armazenamento do Azure, para criar e gerenciar contas de armazenamento; trabalhar com tabelas, blobs, filas e arquivos; configurar e consultar a análise de armazenamento e criar assinaturas de acesso compartilhado."
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
ms.openlocfilehash: 51e3e93ebedd31370857e61a00139294bcee9237
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="using-azure-powershell-with-azure-storage"></a><span data-ttu-id="2bb38-103">Usando o PowerShell do Azure com o Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="2bb38-103">Using Azure PowerShell with Azure Storage</span></span>
## <a name="overview"></a><span data-ttu-id="2bb38-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="2bb38-104">Overview</span></span>
<span data-ttu-id="2bb38-105">O PowerShell no Azure é um módulo que fornece cmdlets para gerenciar o Azure por meio do Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="2bb38-105">Azure PowerShell is a module that provides cmdlets to manage Azure through Windows PowerShell.</span></span> <span data-ttu-id="2bb38-106">Ele é um shell de linha de comando baseado em tarefa e linguagem de script criado especialmente para administração do sistema.</span><span class="sxs-lookup"><span data-stu-id="2bb38-106">It is a task-based command-line shell and scripting language designed especially for system administration.</span></span> <span data-ttu-id="2bb38-107">Com o PowerShell, você pode facilmente controlar e automatizar a administração dos seus aplicativos e serviços do Azure.</span><span class="sxs-lookup"><span data-stu-id="2bb38-107">With PowerShell, you can easily control and automate the administration of your Azure services and applications.</span></span> <span data-ttu-id="2bb38-108">Na maioria dos casos, é possível usar os cmdlets para executar as mesmas tarefas que você pode realizar por meio do [Portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="2bb38-108">For example, you can use the cmdlets to perform the same tasks that you can perform through the [Azure portal](https://portal.azure.com).</span></span>

<span data-ttu-id="2bb38-109">Neste guia, exploraremos como usar os [Cmdlets de Armazenamento do Azure](/powershell/module/azurerm.storage/#storage) para executar uma variedade de tarefas de desenvolvimento e administração com o Armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="2bb38-109">In this guide, we'll explore how to use the [Azure Storage Cmdlets](/powershell/module/azurerm.storage/#storage) to perform a variety of development and administration tasks with Azure Storage.</span></span>

<span data-ttu-id="2bb38-110">Este guia pressupõe que você tenha usado anteriormente o [Armazenamento do Azure](https://azure.microsoft.com/documentation/services/storage/) e o [Windows PowerShell](http://technet.microsoft.com/library/bb978526.aspx).</span><span class="sxs-lookup"><span data-stu-id="2bb38-110">This guide assumes that you have prior experience using [Azure Storage](https://azure.microsoft.com/documentation/services/storage/) and [Windows PowerShell](http://technet.microsoft.com/library/bb978526.aspx).</span></span> <span data-ttu-id="2bb38-111">Este guia fornece vários scripts para demonstrar o uso do PowerShell com o Armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="2bb38-111">The guide provides a number of scripts to demonstrate the usage of PowerShell with Azure Storage.</span></span> <span data-ttu-id="2bb38-112">Você deve atualizar as variáveis de script com base em sua configuração antes de executar cada script.</span><span class="sxs-lookup"><span data-stu-id="2bb38-112">You should update the script variables based on your configuration before running each script.</span></span>

<span data-ttu-id="2bb38-113">A primeira seção deste guia fornece uma visão rápida no Armazenamento do Azure e do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="2bb38-113">The first section in this guide provides a quick glance at Azure Storage and PowerShell.</span></span> <span data-ttu-id="2bb38-114">Para obter informações e instruções detalhadas, comece com os [Pré-requisitos para usar o Azure PowerShell com o armazenamento do Azure](#prerequisites-for-using-azure-powershell-with-azure-storage).</span><span class="sxs-lookup"><span data-stu-id="2bb38-114">For detailed information and instructions, start from the [Prerequisites for using Azure PowerShell with Azure Storage](#prerequisites-for-using-azure-powershell-with-azure-storage).</span></span>

## <a name="getting-started-with-azure-storage-and-powershell-in-5-minutes"></a><span data-ttu-id="2bb38-115">Introdução ao Armazenamento do Azure e ao PowerShell em 5 minutos</span><span class="sxs-lookup"><span data-stu-id="2bb38-115">Getting started with Azure Storage and PowerShell in 5 minutes</span></span>
<span data-ttu-id="2bb38-116">Esta seção mostra como acessar o Armazenamento do Azure por meio do PowerShell em 5 minutos.</span><span class="sxs-lookup"><span data-stu-id="2bb38-116">This section shows you how to access Azure Storage via PowerShell in 5 minutes.</span></span>

<span data-ttu-id="2bb38-117">**Novo no Azure:** obtenha uma assinatura do Microsoft Azure e uma conta da Microsoft associada a essa assinatura.</span><span class="sxs-lookup"><span data-stu-id="2bb38-117">**New to Azure:** Get a Microsoft Azure subscription and a Microsoft account associated with that subscription.</span></span> <span data-ttu-id="2bb38-118">Para saber mais sobre as opções de compra do Azure, confira [Avaliação gratuita](https://azure.microsoft.com/pricing/free-trial/), [Opções de compra](https://azure.microsoft.com/pricing/purchase-options/) e [Ofertas para membros](https://azure.microsoft.com/pricing/member-offers/) (para membros do MSDN, Microsoft Partner Network e BizSpark, entre outros programas da Microsoft).</span><span class="sxs-lookup"><span data-stu-id="2bb38-118">For information on Azure purchase options, see [Free Trial](https://azure.microsoft.com/pricing/free-trial/), [Purchase Options](https://azure.microsoft.com/pricing/purchase-options/), and [Member Offers](https://azure.microsoft.com/pricing/member-offers/) (for members of MSDN, Microsoft Partner Network, and BizSpark, and other Microsoft programs).</span></span>

<span data-ttu-id="2bb38-119">Consulte [Atribuindo funções de administrador no Azure AD (Azure Active Directory)](https://msdn.microsoft.com/library/azure/hh531793.aspx) para obter mais informações sobre as assinaturas do Azure.</span><span class="sxs-lookup"><span data-stu-id="2bb38-119">See [Assigning administrator roles in Azure Active Directory (Azure AD)](https://msdn.microsoft.com/library/azure/hh531793.aspx) for more information about Azure subscriptions.</span></span>

<span data-ttu-id="2bb38-120">**Depois de criar uma assinatura e conta do Microsoft Azure:**</span><span class="sxs-lookup"><span data-stu-id="2bb38-120">**After creating a Microsoft Azure subscription and account:**</span></span>

1. <span data-ttu-id="2bb38-121">Baixe e instale o [Azure PowerShell](https://github.com/Azure/azure-powershell/releases/latest) mais recente.</span><span class="sxs-lookup"><span data-stu-id="2bb38-121">Download and install the latest [Azure PowerShell](https://github.com/Azure/azure-powershell/releases/latest).</span></span>
2. <span data-ttu-id="2bb38-122">Inicie o Ambiente de Script Integrado (ISE) do Windows PowerShell: No seu computador local, vá até o menu **Iniciar** .</span><span class="sxs-lookup"><span data-stu-id="2bb38-122">Start Windows PowerShell Integrated Scripting Environment (ISE): In your local computer, go to the **Start** menu.</span></span> <span data-ttu-id="2bb38-123">Digite **Ferramentas Administrativas** e clique para executá-las.</span><span class="sxs-lookup"><span data-stu-id="2bb38-123">Type **Administrative Tools** and click to run it.</span></span> <span data-ttu-id="2bb38-124">Na janela **Ferramentas Administrativas**, clique com botão direito em **ISE do Windows PowerShell** e clique em **Executar como administrador**.</span><span class="sxs-lookup"><span data-stu-id="2bb38-124">In the **Administrative Tools** window, right-click **Windows PowerShell ISE**, click **Run as Administrator**.</span></span>
3. <span data-ttu-id="2bb38-125">No **ISE do Windows PowerShell**, clique em **Arquivo** > **Novo** para criar um novo arquivo de script.</span><span class="sxs-lookup"><span data-stu-id="2bb38-125">In **Windows PowerShell ISE**, click **File** > **New** to create a new script file.</span></span>
4. <span data-ttu-id="2bb38-126">Agora, você terá um script simples que mostra os comandos básicos do PowerShell para acessar o Armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="2bb38-126">Now, we'll give you a simple script that shows basic PowerShell commands to access Azure Storage.</span></span> <span data-ttu-id="2bb38-127">O script primeiro solicitará suas credenciais da conta do Azure para adicioná-la ao ambiente local do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="2bb38-127">The script will first ask your Azure account credentials to add your Azure account to the local PowerShell environment.</span></span> <span data-ttu-id="2bb38-128">Depois, o script definirá a assinatura padrão do Azure e criará uma nova conta de armazenamento no Azure.</span><span class="sxs-lookup"><span data-stu-id="2bb38-128">Then, the script will set the default Azure subscription and create a new storage account in Azure.</span></span> <span data-ttu-id="2bb38-129">Em seguida, o script criará um novo contêiner nessa nova conta de armazenamento e carregará um arquivo de imagem existente (blob) para esse contêiner.</span><span class="sxs-lookup"><span data-stu-id="2bb38-129">Next, the script will create a new container in this new storage account and upload an existing image file (blob) to that container.</span></span> <span data-ttu-id="2bb38-130">Depois que o script listar todos os blobs nesse contêiner, ele criará um novo diretório de destino no computador local e baixará o arquivo de imagem.</span><span class="sxs-lookup"><span data-stu-id="2bb38-130">After the script lists all blobs in that container, it will create a new destination directory in your local computer and download the image file.</span></span>
5. <span data-ttu-id="2bb38-131">Na seção de código a seguir, selecione o script entre os comentários **#begin** e **#end**.</span><span class="sxs-lookup"><span data-stu-id="2bb38-131">In the following code section, select the script between the remarks **#begin** and **#end**.</span></span> <span data-ttu-id="2bb38-132">Pressione CTRL + C para copiá-lo para a área de transferência.</span><span class="sxs-lookup"><span data-stu-id="2bb38-132">Press CTRL+C to copy it to the clipboard.</span></span>

    ```powershell
    # begin
    # Update with the name of your subscription.
    $SubscriptionName = "YourSubscriptionName"
       
    # Give a name to your new storage account. It must be lowercase!
    $StorageAccountName = "yourstorageaccountname"
       
    # Choose "West US" as an example.
    $Location = "West US"
       
    # Give a name to your new container.
    $ContainerName = "imagecontainer"
       
    # Have an image file and a source directory in your local computer.
    $ImageToUpload = "C:\Images\HelloWorld.png"
       
    # A destination directory in your local computer.
    $DestinationFolder = "C:\DownloadImages"
       
    # Add your Azure account to the local PowerShell environment.
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
       
    # Download blobs from the container:
    # Get a reference to a list of all blobs in a container.
    $blobs = Get-AzureStorageBlob -Container $ContainerName
       
    # Create the destination directory.
    New-Item -Path $DestinationFolder -ItemType Directory -Force  
       
    # Download blobs into the local destination directory.
    $blobs | Get-AzureStorageBlobContent –Destination $DestinationFolder
       
    # end
    ```

6. <span data-ttu-id="2bb38-133">Em **ISE do Windows PowerShell**, pressione CTRL + V para copiar o script.</span><span class="sxs-lookup"><span data-stu-id="2bb38-133">In **Windows PowerShell ISE**, press CTRL+V to copy the script.</span></span> <span data-ttu-id="2bb38-134">Clique em **Arquivo** > **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="2bb38-134">Click **File** > **Save**.</span></span> <span data-ttu-id="2bb38-135">Na janela de diálogo **Salvar como**, digite o nome do arquivo de script, como “meuscriptdearmazenamento”.</span><span class="sxs-lookup"><span data-stu-id="2bb38-135">In the **Save As** dialog window, type the name of the script file, such as "mystoragescript."</span></span> <span data-ttu-id="2bb38-136">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="2bb38-136">Click **Save**.</span></span>
7. <span data-ttu-id="2bb38-137">Agora, você precisa atualizar as variáveis de script com base nas suas configurações.</span><span class="sxs-lookup"><span data-stu-id="2bb38-137">Now, you need to update the script variables based on your configuration settings.</span></span> <span data-ttu-id="2bb38-138">Você deve atualizar a variável **$SubscriptionName** com sua própria assinatura.</span><span class="sxs-lookup"><span data-stu-id="2bb38-138">You must update the **$SubscriptionName** variable with your own subscription.</span></span> <span data-ttu-id="2bb38-139">Você pode manter as outras variáveis conforme especificado no script ou atualizá-las como desejar.</span><span class="sxs-lookup"><span data-stu-id="2bb38-139">You can keep the other variables as specified in the script or update them as you wish.</span></span>
   
   * <span data-ttu-id="2bb38-140">**$SubscriptionName:** você deve atualizar essa variável com o nome de sua própria assinatura.</span><span class="sxs-lookup"><span data-stu-id="2bb38-140">**$SubscriptionName:** You must update this variable with your own subscription name.</span></span> <span data-ttu-id="2bb38-141">Execute uma das três maneiras a seguir para localizar o nome de sua assinatura:</span><span class="sxs-lookup"><span data-stu-id="2bb38-141">Follow one of the following three ways to locate the name of your subscription:</span></span>
     
    <span data-ttu-id="2bb38-142">a.</span><span class="sxs-lookup"><span data-stu-id="2bb38-142">a.</span></span> <span data-ttu-id="2bb38-143">No **ISE do Windows PowerShell**, clique em **Arquivo** > **Novo** para criar um novo arquivo de script.</span><span class="sxs-lookup"><span data-stu-id="2bb38-143">In **Windows PowerShell ISE**, click **File** > **New** to create a new script file.</span></span> <span data-ttu-id="2bb38-144">Copie o script a seguir para o novo arquivo de script e clique em **Depurar** > **Executar**.</span><span class="sxs-lookup"><span data-stu-id="2bb38-144">Copy the following script to the new script file and click **Debug** > **Run**.</span></span> <span data-ttu-id="2bb38-145">O script a seguir primeiro solicitará suas credenciais de conta do Azure para adicioná-la ao ambiente do PowerShell local e, em seguida, mostrará todas as assinaturas que estão conectadas à sessão do PowerShell local.</span><span class="sxs-lookup"><span data-stu-id="2bb38-145">The following script will first ask your Azure account credentials to add your Azure account to the local PowerShell environment and then show all the subscriptions that are connected to the local PowerShell session.</span></span> <span data-ttu-id="2bb38-146">Anote o nome da assinatura que você deseja usar e siga este tutorial:</span><span class="sxs-lookup"><span data-stu-id="2bb38-146">Take a note of the name of the subscription that you want to use while following this tutorial:</span></span>
     
    ```powershell
    Add-AzureAccount 
      Get-AzureSubscription | Format-Table SubscriptionName, IsDefault, IsCurrent, CurrentStorageAccountName
    ```

    <span data-ttu-id="2bb38-147">b.</span><span class="sxs-lookup"><span data-stu-id="2bb38-147">b.</span></span> <span data-ttu-id="2bb38-148">Para localizar e copiar o nome da sua assinatura no [Portal do Azure](https://portal.azure.com), no menu de Hub à esquerda, clique em **Assinaturas**.</span><span class="sxs-lookup"><span data-stu-id="2bb38-148">To locate and copy your subscription name in the [Azure portal](https://portal.azure.com), in the Hub menu on the left, click **Subscriptions**.</span></span> <span data-ttu-id="2bb38-149">Copie o nome da assinatura que você deseja usar ao executar os scripts fornecidos neste guia.</span><span class="sxs-lookup"><span data-stu-id="2bb38-149">Copy the name of subscription that you want to use while running the scripts in this guide.</span></span>
     
     ![Portal do Azure](./media/storage-powershell-guide-full/Subscription_Previewportal.png)

    <span data-ttu-id="2bb38-151">c.</span><span class="sxs-lookup"><span data-stu-id="2bb38-151">c.</span></span> <span data-ttu-id="2bb38-152">Para localizar e copiar o nome da sua assinatura no [Portal clássico do Azure](https://manage.windowsazure.com/), role para baixo e clique em **Configurações** no lado esquerdo do portal.</span><span class="sxs-lookup"><span data-stu-id="2bb38-152">To locate and copy your subscription name in the [Azure Classic Portal](https://manage.windowsazure.com/), scroll down and click **Settings** on the left side of the portal.</span></span> <span data-ttu-id="2bb38-153">Clique em **Assinaturas** para ver uma lista das suas assinaturas.</span><span class="sxs-lookup"><span data-stu-id="2bb38-153">Click **Subscriptions** to see a list of your subscriptions.</span></span> <span data-ttu-id="2bb38-154">Copie o nome da assinatura que você deseja usar ao executar os scripts fornecidos neste guia.</span><span class="sxs-lookup"><span data-stu-id="2bb38-154">Copy the name of subscription that you want to use while running the scripts given in this guide.</span></span>
     
     ![Portal clássico do Azure](./media/storage-powershell-guide-full/Subscription_currentportal.png)

   * <span data-ttu-id="2bb38-156">**$StorageAccountName:** Use o nome fornecido no script ou insira um novo nome para a conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="2bb38-156">**$StorageAccountName:** Use the given name in the script or enter a new name for your storage account.</span></span> <span data-ttu-id="2bb38-157">**Importante:** o nome da conta de armazenamento deve ser exclusivo no Azure.</span><span class="sxs-lookup"><span data-stu-id="2bb38-157">**Important:** The name of the storage account must be unique in Azure.</span></span> <span data-ttu-id="2bb38-158">Ele também deve ter somente letras minúsculas!</span><span class="sxs-lookup"><span data-stu-id="2bb38-158">It must be lowercase, too!</span></span>
   * <span data-ttu-id="2bb38-159">**$Location:** use o "Oeste dos EUA" fornecido no script ou escolha outros locais do Azure, como Leste dos EUA, Norte da Europa e assim por diante.</span><span class="sxs-lookup"><span data-stu-id="2bb38-159">**$Location:** Use the given "West US" in the script or choose other Azure locations, such as East US, North Europe, and so on.</span></span>
   * <span data-ttu-id="2bb38-160">**$ContainerName:** use o nome fornecido no script ou insira um novo nome para seu contêiner.</span><span class="sxs-lookup"><span data-stu-id="2bb38-160">**$ContainerName:** Use the given name in the script or enter a new name for your container.</span></span>
   * <span data-ttu-id="2bb38-161">**$ImageToUpload**: insira um caminho para uma imagem em seu computador local, como: "C:\Images\HelloWorld.png".</span><span class="sxs-lookup"><span data-stu-id="2bb38-161">**$ImageToUpload:** Enter a path to a picture on your local computer, such as: "C:\Images\HelloWorld.png".</span></span>
   * <span data-ttu-id="2bb38-162">**$DestinationFolder**: insira um caminho para um diretório local de modo a armazenar os arquivos baixados do Armazenamento do Azure, tal como: "C:\DownloadImages".</span><span class="sxs-lookup"><span data-stu-id="2bb38-162">**$DestinationFolder:** Enter a path to a local directory to store files downloaded from Azure Storage, such as: "C:\DownloadImages".</span></span>
8. <span data-ttu-id="2bb38-163">Depois de atualizar as variáveis de script no arquivo "mystoragescript.ps1", clique em **Arquivo** > **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="2bb38-163">After updating the script variables in the "mystoragescript.ps1" file, click **File** > **Save**.</span></span> <span data-ttu-id="2bb38-164">Em seguida, clique em **Depurar** > **Executar** ou pressione **F5** para executar o script.</span><span class="sxs-lookup"><span data-stu-id="2bb38-164">Then, click **Debug** > **Run** or press **F5** to run the script.</span></span>  

<span data-ttu-id="2bb38-165">Depois que o script é executado, você deve ter uma pasta de destino que inclui o arquivo de imagem baixada.</span><span class="sxs-lookup"><span data-stu-id="2bb38-165">After the script runs, you should have a local destination folder that includes the downloaded image file.</span></span> <span data-ttu-id="2bb38-166">A captura de tela a seguir mostra um exemplo de saída:</span><span class="sxs-lookup"><span data-stu-id="2bb38-166">The following screenshot shows an example output:</span></span>

![Baixar blobs](./media/storage-powershell-guide-full/Blobdownload.png)

> [!NOTE]
> <span data-ttu-id="2bb38-168">A seção "Introdução ao armazenamento do Azure e ao PowerShell em 5 minutos" forneceu uma rápida introdução sobre como usar o PowerShell do Azure com o Armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="2bb38-168">The "Getting started with Azure Storage and PowerShell in 5 minutes" section provided a quick introduction on how to use Azure PowerShell with Azure Storage.</span></span> <span data-ttu-id="2bb38-169">Para obter informações e instruções detalhadas, recomendamos que você leia as seções a seguir.</span><span class="sxs-lookup"><span data-stu-id="2bb38-169">For detailed information and instructions, we encourage you to read the following sections.</span></span>
> 

## <a name="prerequisites-for-using-azure-powershell-with-azure-storage"></a><span data-ttu-id="2bb38-170">Pré-requisitos para usar o Azure PowerShell com o armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="2bb38-170">Prerequisites for using Azure PowerShell with Azure Storage</span></span>
<span data-ttu-id="2bb38-171">Você precisa de uma assinatura e conta do Azure para executar os cmdlets do PowerShell fornecidos neste guia, conforme descrito acima.</span><span class="sxs-lookup"><span data-stu-id="2bb38-171">You need an Azure subscription and account to run the PowerShell cmdlets given in this guide, as described above.</span></span>

<span data-ttu-id="2bb38-172">O PowerShell no Azure é um módulo que fornece cmdlets para gerenciar o Azure por meio do Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="2bb38-172">Azure PowerShell is a module that provides cmdlets to manage Azure through Windows PowerShell.</span></span> <span data-ttu-id="2bb38-173">Para obter informações sobre como instalar e configurar o Azure PowerShell, consulte [Como instalar e configurar o Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="2bb38-173">For information on installing and setting up Azure PowerShell, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span> <span data-ttu-id="2bb38-174">É recomendável baixar e instalar ou atualizar para o módulo PowerShell do Azure mais recente antes de usar este guia.</span><span class="sxs-lookup"><span data-stu-id="2bb38-174">We recommend that you download and install or upgrade to the latest Azure PowerShell module before using this guide.</span></span>

<span data-ttu-id="2bb38-175">Você pode executar os cmdlets no console do Windows PowerShell padrão ou no ISE (Integrated Scripting Environment) do Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="2bb38-175">You can run the cmdlets in the standard Windows PowerShell console or the Windows PowerShell Integrated Scripting Environment (ISE).</span></span> <span data-ttu-id="2bb38-176">Por exemplo, para abrir o **ISE do Windows PowerShell**, vá para o menu Iniciar, digite Ferramentas administrativas e clique para executá-las.</span><span class="sxs-lookup"><span data-stu-id="2bb38-176">For example, to open **Windows PowerShell ISE**, go to the Start menu, type Administrative Tools and click to run it.</span></span> <span data-ttu-id="2bb38-177">Na janela Ferramentas Administrativas, clique com botão direito em ISE do Windows PowerShell e clique em Executar como administrador.</span><span class="sxs-lookup"><span data-stu-id="2bb38-177">In the Administrative Tools window, right-click Windows PowerShell ISE, click Run as Administrator.</span></span>

## <a name="how-to-manage-storage-accounts-in-azure"></a><span data-ttu-id="2bb38-178">Como gerenciar contas de armazenamento no Azure</span><span class="sxs-lookup"><span data-stu-id="2bb38-178">How to manage storage accounts in Azure</span></span>

<span data-ttu-id="2bb38-179">Vejamos agora o gerenciamento de contas de armazenamento no Azure com o PowerShell</span><span class="sxs-lookup"><span data-stu-id="2bb38-179">Let's take a look at managing storage accounts in Azure with PowerShell</span></span>

### <a name="how-to-set-a-default-azure-subscription"></a><span data-ttu-id="2bb38-180">Como definir uma assinatura padrão do Azure</span><span class="sxs-lookup"><span data-stu-id="2bb38-180">How to set a default Azure subscription</span></span>
<span data-ttu-id="2bb38-181">Para gerenciar o armazenamento do Azure usando o Azure PowerShell, você precisa autenticar seu ambiente de cliente com o Azure por meio de autenticação do Azure Active Directory ou autenticação baseada em certificado.</span><span class="sxs-lookup"><span data-stu-id="2bb38-181">To manage Azure Storage using Azure PowerShell, you need to authenticate your client environment with Azure via Azure Active Directory authentication or certificate-based authentication.</span></span> <span data-ttu-id="2bb38-182">Para obter informações detalhadas, confira o tutorial [Como instalar e configurar o Azure PowerShell](/powershell/azure/overview) .</span><span class="sxs-lookup"><span data-stu-id="2bb38-182">For detailed information, see [How to install and configure Azure PowerShell](/powershell/azure/overview) tutorial.</span></span> <span data-ttu-id="2bb38-183">Este guia usa a autenticação do Active Directory do Azure.</span><span class="sxs-lookup"><span data-stu-id="2bb38-183">This guide uses the Azure Active Directory authentication.</span></span>

1. <span data-ttu-id="2bb38-184">No ISE do Windows PowerShell, digite o seguinte comando para adicionar a conta do Azure ao ambiente do PowerShell local:</span><span class="sxs-lookup"><span data-stu-id="2bb38-184">In Windows PowerShell ISE, type the following command to add your Azure account to the local PowerShell environment:</span></span>

    ```powershell
    Add-AzureAccount
    ```

2. <span data-ttu-id="2bb38-185">Na janela "Entrar no Microsoft Azure", digite o endereço de email e a senha associados à sua conta.</span><span class="sxs-lookup"><span data-stu-id="2bb38-185">In the "Sign in to Microsoft Azure" window, type the email address and password associated with your account.</span></span> <span data-ttu-id="2bb38-186">O Azure autentica e salva as informações de credenciais e, em seguida, fecha a janela.</span><span class="sxs-lookup"><span data-stu-id="2bb38-186">Azure authenticates and saves the credential information, and then closes the window.</span></span>

3. <span data-ttu-id="2bb38-187">Em seguida, execute o seguinte comando para exibir as contas do Azure no seu ambiente do PowerShell local e verifique se sua conta está listada:</span><span class="sxs-lookup"><span data-stu-id="2bb38-187">Next, run the following command to view the Azure accounts in your local PowerShell environment, and verify that your account is listed:</span></span>
   
    ```powershell
    Get-AzureAccount
    ```
4. <span data-ttu-id="2bb38-188">Em seguida, execute o seguinte cmdlet para exibir todas as assinaturas que estão conectadas à sessão do PowerShell local e verifique se sua assinatura está listada:</span><span class="sxs-lookup"><span data-stu-id="2bb38-188">Then, run the following cmdlet to view all the subscriptions that are connected to the local PowerShell session, and verify that your subscription is listed:</span></span>

    ```powershell
    Get-AzureSubscription | Format-Table SubscriptionName, IsDefault, IsCurrent, CurrentStorageAccountName`
    ```
5. <span data-ttu-id="2bb38-189">Para definir uma assinatura padrão do Azure, execute o cmdlet Select-AzureSubscription:</span><span class="sxs-lookup"><span data-stu-id="2bb38-189">To set a default Azure subscription, run the Select-AzureSubscription cmdlet:</span></span>

    ```powershell
    $SubscriptionName = 'Your subscription Name'
    Select-AzureSubscription -SubscriptionName $SubscriptionName –Default
    ```

6. <span data-ttu-id="2bb38-190">Verifique o nome da assinatura padrão executando o cmdlet Get-AzureSubscription:</span><span class="sxs-lookup"><span data-stu-id="2bb38-190">Verify the name of the default subscription by running the Get-AzureSubscription cmdlet:</span></span>

    ```powershell
    Get-AzureSubscription -Default
    ```

7. <span data-ttu-id="2bb38-191">Para ver todos os cmdlets do PowerShell disponíveis para o Armazenamento do Azure, execute:</span><span class="sxs-lookup"><span data-stu-id="2bb38-191">To see all the available PowerShell cmdlets for Azure Storage, run:</span></span>
    
    ```powershell
    Get-Command -Module Azure -Noun *Storage*`
    ```

### <a name="how-to-create-a-new-azure-storage-account"></a><span data-ttu-id="2bb38-192">Como criar uma nova conta de armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="2bb38-192">How to create a new Azure storage account</span></span>
<span data-ttu-id="2bb38-193">Você precisa de uma conta de armazenamento para usar o Armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="2bb38-193">To use Azure storage, you will need a storage account.</span></span> <span data-ttu-id="2bb38-194">Depois de configurar seu computador para se conectar à sua assinatura, você pode criar uma nova conta de Armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="2bb38-194">You can create a new Azure storage account after you have configured your computer to connect to your subscription.</span></span>

1. <span data-ttu-id="2bb38-195">Execute o cmdlet Get-AzureLocation para localizar todos os locais de datacenters disponíveis:</span><span class="sxs-lookup"><span data-stu-id="2bb38-195">Run the Get-AzureLocation cmdlet to find all the available datacenter locations:</span></span>

    ```powershell
    Get-AzureLocation | Format-Table -Property Name, AvailableServices, StorageAccountTypes
    ```

2. <span data-ttu-id="2bb38-196">Em seguida, execute o cmdlet New-AzureStorageAccount para criar uma nova conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="2bb38-196">Next, run the New-AzureStorageAccount cmdlet to create a new storage account.</span></span> <span data-ttu-id="2bb38-197">O exemplo a seguir cria uma nova conta de armazenamento no data center "Oeste dos Estados Unidos".</span><span class="sxs-lookup"><span data-stu-id="2bb38-197">The following example creates a new storage account in the "West US" datacenter.</span></span>
   
    ```powershell
    $location = "West US"
    $StorageAccountName = "yourstorageaccount"
    New-AzureStorageAccount –StorageAccountName $StorageAccountName -Location $location
    ```

> [!IMPORTANT]
> <span data-ttu-id="2bb38-198">O nome da conta de armazenamento deve ser exclusivo dentro do Azure e deve estar em minúsculas.</span><span class="sxs-lookup"><span data-stu-id="2bb38-198">The name of your storage account must be unique within Azure and must be lowercase.</span></span> <span data-ttu-id="2bb38-199">Para ver as convenções e restrições de nomenclatura, confira [Sobre as contas de armazenamento do Azure](storage-create-storage-account.md) e [Naming and Referencing Containers, Blobs, and Metadata](http://msdn.microsoft.com/library/azure/dd135715.aspx) (Nomeando e referenciando contêineres, blobs e metadados).</span><span class="sxs-lookup"><span data-stu-id="2bb38-199">For naming conventions and restrictions, see [About Azure Storage Accounts](storage-create-storage-account.md) and [Naming and Referencing Containers, Blobs, and Metadata](http://msdn.microsoft.com/library/azure/dd135715.aspx).</span></span>
> 
> 

### <a name="how-to-set-a-default-azure-storage-account"></a><span data-ttu-id="2bb38-200">Como configurar uma conta padrão de armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="2bb38-200">How to set a default Azure storage account</span></span>
<span data-ttu-id="2bb38-201">Você pode ter várias contas de armazenamento na sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="2bb38-201">You can have multiple storage accounts in your subscription.</span></span> <span data-ttu-id="2bb38-202">Você pode escolher uma delas e defini-la como a conta de armazenamento padrão para todos os comandos de armazenamento na mesma sessão do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="2bb38-202">You can choose one of them and set it as the default storage account for all the storage commands in the same PowerShell session.</span></span> <span data-ttu-id="2bb38-203">Isso permite que você execute os comandos de armazenamento do Azure PowerShell sem especificar explicitamente o contexto de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="2bb38-203">This enables you to run the Azure PowerShell storage commands without specifying the storage context explicitly.</span></span>

1. <span data-ttu-id="2bb38-204">Para definir uma conta de armazenamento padrão para a sua assinatura, você pode executar o cmdlet Set-AzureSubscription.</span><span class="sxs-lookup"><span data-stu-id="2bb38-204">To set a default storage account for your subscription, you can run the Set-AzureSubscription cmdlet.</span></span>

    ```powershell
    $SubscriptionName = "Your subscription name"
    $StorageAccountName = "yourstorageaccount"  
    Set-AzureSubscription -CurrentStorageAccountName $StorageAccountName -SubscriptionName $SubscriptionName
    ```

2. <span data-ttu-id="2bb38-205">Em seguida, execute o cmdlet Get-AzureSubscription para verificar se a conta de armazenamento está associada à sua conta de assinatura padrão.</span><span class="sxs-lookup"><span data-stu-id="2bb38-205">Next, run the Get-AzureSubscription cmdlet to verify that the storage account is associated with your default subscription account.</span></span> <span data-ttu-id="2bb38-206">Esse comando retorna as propriedades de assinatura da assinatura atual, incluindo sua conta de armazenamento atual.</span><span class="sxs-lookup"><span data-stu-id="2bb38-206">This command returns the subscription properties on the current subscription including its current storage account.</span></span>

    ```powershell
    Get-AzureSubscription –Current
    ```

### <a name="how-to-list-all-azure-storage-accounts-in-a-subscription"></a><span data-ttu-id="2bb38-207">Como listar todas as contas de armazenamento do Azure em uma assinatura</span><span class="sxs-lookup"><span data-stu-id="2bb38-207">How to list all Azure storage accounts in a subscription</span></span>
<span data-ttu-id="2bb38-208">Cada assinatura do Azure pode ter até 100 contas de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="2bb38-208">Each Azure subscription can have up to 100 storage accounts.</span></span> <span data-ttu-id="2bb38-209">Para obter as informações mais atualizadas sobre os limites, consulte [Assinatura do Azure e limites de serviço, cotas e restrições](../azure-subscription-service-limits.md).</span><span class="sxs-lookup"><span data-stu-id="2bb38-209">For the most up-to-date information on limits, see [Azure Subscription and Service Limits, Quotas, and Constraints](../azure-subscription-service-limits.md).</span></span>

<span data-ttu-id="2bb38-210">Execute o seguinte cmdlet para descobrir o nome e o status das contas de armazenamento na assinatura atual:</span><span class="sxs-lookup"><span data-stu-id="2bb38-210">Run the following cmdlet to find out the name and status of the storage accounts in the current subscription:</span></span>

```powershell
Get-AzureStorageAccount | Format-Table -Property StorageAccountName, Location, AccountType, StorageAccountStatus
```

### <a name="how-to-create-an-azure-storage-context"></a><span data-ttu-id="2bb38-211">Como criar um contexto de armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="2bb38-211">How to create an Azure storage context</span></span>
<span data-ttu-id="2bb38-212">O contexto de Armazenamento do Azure é um objeto no PowerShell para encapsular as credenciais de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="2bb38-212">Azure storage context is an object in PowerShell to encapsulate the storage credentials.</span></span> <span data-ttu-id="2bb38-213">Usar um contexto de armazenamento enquanto executa qualquer cmdlet subsequente permite autenticar a solicitação sem especificar a conta de armazenamento e sua chave de acesso explicitamente.</span><span class="sxs-lookup"><span data-stu-id="2bb38-213">Using a storage context while running any subsequent cmdlet enables you to authenticate your request without specifying the storage account and its access key explicitly.</span></span> <span data-ttu-id="2bb38-214">Você pode criar um contexto de armazenamento de várias maneiras, como usando a chave de acesso e do nome da conta de armazenamento, o token de SAS (assinatura de acesso compartilhado), cadeia de conexão ou anonimamente.</span><span class="sxs-lookup"><span data-stu-id="2bb38-214">You can create a storage context in many ways, such as using storage account name and access key, shared access signature (SAS) token, connection string, or anonymous.</span></span> <span data-ttu-id="2bb38-215">Para obter mais informações, consulte [New-AzureStorageContext](/powershell/module/azure.storage/new-azurestoragecontext).</span><span class="sxs-lookup"><span data-stu-id="2bb38-215">For more information, see [New-AzureStorageContext](/powershell/module/azure.storage/new-azurestoragecontext).</span></span>  

<span data-ttu-id="2bb38-216">Use um dos três procedimentos a seguir para criar um contexto de armazenamento:</span><span class="sxs-lookup"><span data-stu-id="2bb38-216">Use one of the following three ways to create a storage context:</span></span>

* <span data-ttu-id="2bb38-217">Execute o cmdlet [Get-AzureStorageKey](/powershell/module/azure.storage/get-azurestoragekey) para descobrir a chave de acesso de armazenamento principal para sua conta de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="2bb38-217">Run the [Get-AzureStorageKey](/powershell/module/azure.storage/get-azurestoragekey) cmdlet to find out the primary storage access key for your Azure storage account.</span></span> <span data-ttu-id="2bb38-218">Em seguida, chame o cmdlet [New-AzureStorageContext](/powershell/module/azure.storage/new-azurestoragecontext) para criar um contexto de armazenamento:</span><span class="sxs-lookup"><span data-stu-id="2bb38-218">Next, call the [New-AzureStorageContext](/powershell/module/azure.storage/new-azurestoragecontext) cmdlet to create a storage context:</span></span>

    ```powershell
    $StorageAccountName = "yourstorageaccount"
    $StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
    $Ctx = New-AzureStorageContext $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary
    ```

* <span data-ttu-id="2bb38-219">Gere um token de assinatura de acesso compartilhado para um contêiner de armazenamento do Azure e use-o para criar um contexto de armazenamento:</span><span class="sxs-lookup"><span data-stu-id="2bb38-219">Generate a shared access signature token for an Azure storage container and use it to create a storage context:</span></span>

    ```powershell
    $sasToken = New-AzureStorageContainerSASToken -Container abc -Permission rl
    $Ctx = New-AzureStorageContext -StorageAccountName $StorageAccountName -SasToken $sasToken
    ```

    <span data-ttu-id="2bb38-220">Para saber mais, veja [New-AzureStorageContainerSASToken](/powershell/module/azure.storage/new-azurestoragecontainersastoken) e [Uso de SAS (Assinaturas de Acesso Compartilhado)](storage-dotnet-shared-access-signature-part-1.md).</span><span class="sxs-lookup"><span data-stu-id="2bb38-220">For more information, see [New-AzureStorageContainerSASToken](/powershell/module/azure.storage/new-azurestoragecontainersastoken) and [Using Shared Access Signatures (SAS)](storage-dotnet-shared-access-signature-part-1.md).</span></span>

* <span data-ttu-id="2bb38-221">Em alguns casos, você talvez queira especificar os pontos de extremidade de serviço ao criar um novo contexto de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="2bb38-221">In some cases, you may want to specify the service endpoints when you create a new storage context.</span></span> <span data-ttu-id="2bb38-222">Isso pode ser necessário quando você registrou um nome de domínio personalizado para sua conta de armazenamento com o serviço Blob ou se desejar usar uma assinatura de acesso compartilhado para acessar recursos de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="2bb38-222">This might be necessary when you have registered a custom domain name for your storage account with the Blob service or you want to use a shared access signature for accessing storage resources.</span></span> <span data-ttu-id="2bb38-223">Defina os pontos de extremidade do serviço em uma cadeia de conexão e use-a para criar um novo contexto de armazenamento, conforme mostrado abaixo:</span><span class="sxs-lookup"><span data-stu-id="2bb38-223">Set the service endpoints in a connection string and use it to create a new storage context as shown below:</span></span>

    ```powershell
    $ConnectionString = "DefaultEndpointsProtocol=http;BlobEndpoint=<blobEndpoint>;QueueEndpoint=<QueueEndpoint>;TableEndpoint=<TableEndpoint>;AccountName=<AccountName>;AccountKey=<AccountKey>"
    $Ctx = New-AzureStorageContext -ConnectionString $ConnectionString
    ```

<span data-ttu-id="2bb38-224">Para obter mais informações sobre como configurar uma cadeia de conexão, consulte [Configurando cadeias de conexão](storage-configure-connection-string.md).</span><span class="sxs-lookup"><span data-stu-id="2bb38-224">For more information on how to configure a storage connection string, see [Configuring Connection Strings](storage-configure-connection-string.md).</span></span>

<span data-ttu-id="2bb38-225">Agora que você configurou o computador e sabe como gerenciar assinaturas e contas de armazenamento usando o Azure PowerShell, vá para a próxima seção para aprender a gerenciar blobs do Azure e instantâneos de blob.</span><span class="sxs-lookup"><span data-stu-id="2bb38-225">Now that you have set up your computer and learned how to manage subscriptions and storage accounts using Azure PowerShell, go to the next section to learn how to manage Azure blobs and blob snapshots.</span></span>

### <a name="how-to-retrieve-and-regenerate-azure-storage-keys"></a><span data-ttu-id="2bb38-226">Como recuperar e regenerar chaves de armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="2bb38-226">How to retrieve and regenerate Azure storage keys</span></span>
<span data-ttu-id="2bb38-227">Uma conta de armazenamento do Azure é fornecida com duas chaves de conta.</span><span class="sxs-lookup"><span data-stu-id="2bb38-227">An Azure Storage account comes with two account keys.</span></span> <span data-ttu-id="2bb38-228">É possível usar o cmdlet a seguir para recuperar suas chaves.</span><span class="sxs-lookup"><span data-stu-id="2bb38-228">You can use the following cmdlet to retrieve your keys.</span></span>

```powershell
Get-AzureStorageKey -StorageAccountName "yourstorageaccount"
```

<span data-ttu-id="2bb38-229">Use o seguinte cmdlet para recuperar uma chave específica.</span><span class="sxs-lookup"><span data-stu-id="2bb38-229">Use the following cmdlet to retrieve a specific key.</span></span> <span data-ttu-id="2bb38-230">Os valores válidos são Primary e Secondary.</span><span class="sxs-lookup"><span data-stu-id="2bb38-230">Valid values are Primary and Secondary.</span></span>  

```powershell
(Get-AzureStorageKey -StorageAccountName $StorageAccountName).Primary
    
(Get-AzureStorageKey -StorageAccountName $StorageAccountName).Secondary
```

<span data-ttu-id="2bb38-231">Se você desejar regerar suas chaves, use o seguinte cmdlet.</span><span class="sxs-lookup"><span data-stu-id="2bb38-231">If you would like to regenerate your keys, use the following cmdlet.</span></span> <span data-ttu-id="2bb38-232">Os valores válidos para -KeyType são "Primary" e "Secundary"</span><span class="sxs-lookup"><span data-stu-id="2bb38-232">Valid values for -KeyType are "Primary" and "Secondary"</span></span>

```powershell
New-AzureStorageKey -StorageAccountName $StorageAccountName -KeyType "Primary"
    
New-AzureStorageKey -StorageAccountName $StorageAccountName -KeyType "Secondary"
```

## <a name="how-to-manage-azure-blobs"></a><span data-ttu-id="2bb38-233">Como gerenciar blobs do Azure</span><span class="sxs-lookup"><span data-stu-id="2bb38-233">How to manage Azure blobs</span></span>
<span data-ttu-id="2bb38-234">O Armazenamento de Blobs do Azure é um serviço para armazenar grandes quantidades de dados não estruturados, como texto ou dados binários, que podem ser acessados de qualquer lugar do mundo por meio de HTTP ou HTTPS.</span><span class="sxs-lookup"><span data-stu-id="2bb38-234">Azure Blob storage is a service for storing large amounts of unstructured data, such as text or binary data, that can be accessed from anywhere in the world via HTTP or HTTPS.</span></span> <span data-ttu-id="2bb38-235">Esta seção pressupõe que você já esteja familiarizado com os conceitos do serviço de Armazenamento de Blobs do Azure.</span><span class="sxs-lookup"><span data-stu-id="2bb38-235">This section assumes that you are already familiar with the Azure Blob Storage Service concepts.</span></span> <span data-ttu-id="2bb38-236">Para obter informações detalhadas, confira [Introdução ao Armazenamento de Blobs usando o .NET](storage-dotnet-how-to-use-blobs.md) e [Blob Service Concepts](http://msdn.microsoft.com/library/azure/dd179376.aspx) (Conceitos do serviço Blob).</span><span class="sxs-lookup"><span data-stu-id="2bb38-236">For detailed information, see [Get started with Blob storage using .NET](storage-dotnet-how-to-use-blobs.md) and [Blob Service Concepts](http://msdn.microsoft.com/library/azure/dd179376.aspx).</span></span>

### <a name="how-to-create-a-container"></a><span data-ttu-id="2bb38-237">Como criar um contêiner</span><span class="sxs-lookup"><span data-stu-id="2bb38-237">How to create a container</span></span>
<span data-ttu-id="2bb38-238">Todos os blobs no armazenamento do Azure devem residir em um contêiner.</span><span class="sxs-lookup"><span data-stu-id="2bb38-238">Every blob in Azure storage must be in a container.</span></span> <span data-ttu-id="2bb38-239">Você pode criar um contêiner privado usando o cmdlet New-AzureStorageContainer:</span><span class="sxs-lookup"><span data-stu-id="2bb38-239">You can create a private container using the New-AzureStorageContainer cmdlet:</span></span>

```powershell
$StorageContainerName = "yourcontainername"
New-AzureStorageContainer -Name $StorageContainerName -Permission Off
```

> [!NOTE]
> <span data-ttu-id="2bb38-240">Há três níveis de acesso de leitura anônimo: **Desativado**, **Blob** e **Contêiner**.</span><span class="sxs-lookup"><span data-stu-id="2bb38-240">There are three levels of anonymous read access: **Off**, **Blob**, and **Container**.</span></span> <span data-ttu-id="2bb38-241">Para evitar o acesso anônimo a blobs, defina o parâmetro de permissão como **Desativado**.</span><span class="sxs-lookup"><span data-stu-id="2bb38-241">To prevent anonymous access to blobs, set the Permission parameter to **Off**.</span></span> <span data-ttu-id="2bb38-242">Por padrão, o novo contêiner é privado e pode ser acessado apenas pelo proprietário da conta.</span><span class="sxs-lookup"><span data-stu-id="2bb38-242">By default, the new container is private and can be accessed only by the account owner.</span></span> <span data-ttu-id="2bb38-243">Para permitir acesso de leitura público anônimo a recursos de blob, mas não aos metadados do contêiner ou à lista de blobs no contêiner, defina o parâmetro de permissão como **Blob**.</span><span class="sxs-lookup"><span data-stu-id="2bb38-243">To allow anonymous public read access to blob resources, but not to container metadata or to the list of blobs in the container, set the Permission parameter to **Blob**.</span></span> <span data-ttu-id="2bb38-244">Para permitir acesso de leitura público completo a recursos, metadados do contêiner e à lista de blobs no contêiner, defina o parâmetro de permissão como **Contêiner**.</span><span class="sxs-lookup"><span data-stu-id="2bb38-244">To allow full public read access to blob resources, container metadata, and the list of blobs in the container, set the Permission parameter to **Container**.</span></span> <span data-ttu-id="2bb38-245">Para obter mais informações, confira [Gerenciar acesso anônimo de leitura aos contêineres e blobs](storage-manage-access-to-resources.md).</span><span class="sxs-lookup"><span data-stu-id="2bb38-245">For more information, see [Manage anonymous read access to containers and blobs](storage-manage-access-to-resources.md).</span></span>
> 
> 

### <a name="how-to-upload-a-blob-into-a-container"></a><span data-ttu-id="2bb38-246">Como carregar um blob para um contêiner</span><span class="sxs-lookup"><span data-stu-id="2bb38-246">How to upload a blob into a container</span></span>
<span data-ttu-id="2bb38-247">O Armazenamento de Blob do Azure oferece suporte a blobs de blocos e a blobs de páginas.</span><span class="sxs-lookup"><span data-stu-id="2bb38-247">Azure Blob Storage supports block blobs and page blobs.</span></span> <span data-ttu-id="2bb38-248">Para obter mais informações, confira [Compreendendo Blobs de blocos, Blobs de apêndice e Blobs de páginas](http://msdn.microsoft.com/library/azure/ee691964.aspx).</span><span class="sxs-lookup"><span data-stu-id="2bb38-248">For more information, see [Understanding Block Blobs, Append BLobs, and Page Blobs](http://msdn.microsoft.com/library/azure/ee691964.aspx).</span></span>

<span data-ttu-id="2bb38-249">Para carregar blobs em um contêiner, você pode usar o cmdlet [Set-AzureStorageBlobContent](/powershell/module/azure.storage/set-azurestorageblobcontent) .</span><span class="sxs-lookup"><span data-stu-id="2bb38-249">To upload blobs in to a container, you can use the [Set-AzureStorageBlobContent](/powershell/module/azure.storage/set-azurestorageblobcontent) cmdlet.</span></span> <span data-ttu-id="2bb38-250">Por padrão, esse comando carrega os arquivos locais para um blob de blocos.</span><span class="sxs-lookup"><span data-stu-id="2bb38-250">By default, this command uploads the local files to a block blob.</span></span> <span data-ttu-id="2bb38-251">Para especificar o tipo do blob, você pode usar o parâmetro -BlobType.</span><span class="sxs-lookup"><span data-stu-id="2bb38-251">To specify the type for the blob, you can use the -BlobType parameter.</span></span>

<span data-ttu-id="2bb38-252">O exemplo a seguir executa o cmdlet [Get-ChildItem](http://technet.microsoft.com/library/hh849800.aspx) para obter todos os arquivos na pasta especificada e os passa para o próximo cmdlet usando o operador de pipeline.</span><span class="sxs-lookup"><span data-stu-id="2bb38-252">The following example runs the [Get-ChildItem](http://technet.microsoft.com/library/hh849800.aspx) cmdlet to get all the files in the specified folder, and then passes them to the next cmdlet by using the pipeline operator.</span></span> <span data-ttu-id="2bb38-253">O cmdlet [Set-AzureStorageBlobContent](/powershell/module/azure.storage/set-azurestorageblobcontent) carrega os arquivos locais para o contêiner:</span><span class="sxs-lookup"><span data-stu-id="2bb38-253">The [Set-AzureStorageBlobContent](/powershell/module/azure.storage/set-azurestorageblobcontent) cmdlet uploads the local files to your container:</span></span>

```powershell
Get-ChildItem –Path C:\Images\* | Set-AzureStorageBlobContent -Container "yourcontainername"
```

### <a name="how-to-download-blobs-from-a-container"></a><span data-ttu-id="2bb38-254">Como baixar blobs de um contêiner</span><span class="sxs-lookup"><span data-stu-id="2bb38-254">How to download blobs from a container</span></span>
<span data-ttu-id="2bb38-255">O exemplo a seguir demonstra como baixar blobs de um contêiner.</span><span class="sxs-lookup"><span data-stu-id="2bb38-255">The following example demonstrates how to download blobs from a container.</span></span> <span data-ttu-id="2bb38-256">O exemplo primeiro estabelece uma conexão com o armazenamento do Azure usando o contexto de conta de armazenamento, que inclui o nome da conta de armazenamento e sua chave de acesso primário.</span><span class="sxs-lookup"><span data-stu-id="2bb38-256">The example first establishes a connection to Azure Storage using the storage account context, which includes the storage account name and its primary access key.</span></span> <span data-ttu-id="2bb38-257">Em seguida, o exemplo recupera uma referência de blob usando o cmdlet [Get-AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) .</span><span class="sxs-lookup"><span data-stu-id="2bb38-257">Then, the example retrieves a blob reference using the [Get-AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) cmdlet.</span></span> <span data-ttu-id="2bb38-258">Em seguida, o exemplo usa o cmdlet [Get-AzureStorageBlobContent](/powershell/module/azure.storage/get-azurestorageblobcontent) para baixar blobs para a pasta de destino local.</span><span class="sxs-lookup"><span data-stu-id="2bb38-258">Next, the example uses the [Get-AzureStorageBlobContent](/powershell/module/azure.storage/get-azurestorageblobcontent) cmdlet to download blobs into the local destination folder.</span></span>

```powershell
#Define the variables.
$ContainerName = "yourcontainername"
$DestinationFolder = "C:\DownloadImages"

#Define the storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = "Storage key for yourstorageaccount ends with =="
$Ctx = New-AzureStorageContext -StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey

#List all blobs in a container.
$blobs = Get-AzureStorageBlob -Container $ContainerName -Context $Ctx

#Download blobs from a container.
New-Item -Path $DestinationFolder -ItemType Directory -Force
$blobs | Get-AzureStorageBlobContent -Destination $DestinationFolder -Context $Ctx
```

### <a name="how-to-copy-blobs-from-one-storage-container-to-another"></a><span data-ttu-id="2bb38-259">Como copiar blobs de um contêiner de armazenamento para outro</span><span class="sxs-lookup"><span data-stu-id="2bb38-259">How to copy blobs from one storage container to another</span></span>
<span data-ttu-id="2bb38-260">Você pode copiar blobs em regiões e contas de armazenamento de forma assíncrona.</span><span class="sxs-lookup"><span data-stu-id="2bb38-260">You can copy blobs across storage accounts and regions asynchronously.</span></span> <span data-ttu-id="2bb38-261">O exemplo a seguir demonstra como copiar blobs de um contêiner de armazenamento para outro em duas contas de armazenamento diferentes.</span><span class="sxs-lookup"><span data-stu-id="2bb38-261">The following example demonstrates how to copy blobs from one storage container to another in two different storage accounts.</span></span> <span data-ttu-id="2bb38-262">O exemplo primeiro define variáveis para contas de armazenamento de origem e de destino e, em seguida, cria um contexto de armazenamento para cada conta.</span><span class="sxs-lookup"><span data-stu-id="2bb38-262">The example first sets variables for source and destination storage accounts, and then creates a storage context for each account.</span></span> <span data-ttu-id="2bb38-263">Em seguida, o exemplo copia blobs do contêiner de origem para o contêiner de destino usando o cmdlet [Start-AzureStorageBlobCopy](/powershell/module/azure.storage/start-azurestorageblobcopy) .</span><span class="sxs-lookup"><span data-stu-id="2bb38-263">Next, the example copies blobs from the source container to the destination container using the [Start-AzureStorageBlobCopy](/powershell/module/azure.storage/start-azurestorageblobcopy) cmdlet.</span></span> <span data-ttu-id="2bb38-264">O exemplo supõe que as contas de armazenamento de origem e de destino e os contêineres já existem.</span><span class="sxs-lookup"><span data-stu-id="2bb38-264">The example assumes that the source and destination storage accounts and containers already exist.</span></span>

```powershell
#Define the source storage account and context.
$SourceStorageAccountName = "yoursourcestorageaccount"
$SourceStorageAccountKey = "Storage key for yoursourcestorageaccount"
$SrcContainerName = "yoursrccontainername"
$SourceContext = New-AzureStorageContext -StorageAccountName $SourceStorageAccountName -StorageAccountKey $SourceStorageAccountKey

#Define the destination storage account and context.
$DestStorageAccountName = "yourdeststorageaccount"
$DestStorageAccountKey = "Storage key for yourdeststorageaccount"
$DestContainerName = "destcontainername"
$DestContext = New-AzureStorageContext -StorageAccountName $DestStorageAccountName -StorageAccountKey $DestStorageAccountKey

#Get a reference to blobs in the source container.
$blobs = Get-AzureStorageBlob -Container $SrcContainerName -Context $SourceContext

#Copy blobs from one container to another.
$blobs| Start-AzureStorageBlobCopy -DestContainer $DestContainerName -DestContext $DestContext
```

<span data-ttu-id="2bb38-265">Observe que este exemplo executa uma cópia assíncrona.</span><span class="sxs-lookup"><span data-stu-id="2bb38-265">Note that this example performs an asynchronous copy.</span></span> <span data-ttu-id="2bb38-266">Você pode monitorar o status de cada cópia executando o cmdlet [Get-AzureStorageBlobCopyState](/powershell/module/azure.storage/start-azurestorageblobcopystate) .</span><span class="sxs-lookup"><span data-stu-id="2bb38-266">You can monitor the status of each copy by running the [Get-AzureStorageBlobCopyState](/powershell/module/azure.storage/start-azurestorageblobcopystate) cmdlet.</span></span>

### <a name="how-to-copy-blobs-from-a-secondary-location"></a><span data-ttu-id="2bb38-267">Como copiar blobs de um local secundário</span><span class="sxs-lookup"><span data-stu-id="2bb38-267">How to copy blobs from a secondary location</span></span>
<span data-ttu-id="2bb38-268">Você pode copiar blobs do local secundário de uma conta habilitada para RA-GRS.</span><span class="sxs-lookup"><span data-stu-id="2bb38-268">You can copy blobs from the secondary location of a RA-GRS-enabled account.</span></span>

```powershell
#define secondary storage context using a connection string constructed from secondary endpoints.
$SrcContext = New-AzureStorageContext -ConnectionString "DefaultEndpointsProtocol=https;AccountName=***;AccountKey=***;BlobEndpoint=http://***-secondary.blob.core.windows.net;FileEndpoint=http://***-secondary.file.core.windows.net;QueueEndpoint=http://***-secondary.queue.core.windows.net; TableEndpoint=http://***-secondary.table.core.windows.net;"
Start-AzureStorageBlobCopy –Container *** -Blob *** -Context $SrcContext –DestContainer *** -DestBlob *** -DestContext $DestContext
```

### <a name="how-to-delete-a-blob"></a><span data-ttu-id="2bb38-269">Como excluir um blob</span><span class="sxs-lookup"><span data-stu-id="2bb38-269">How to delete a blob</span></span>
<span data-ttu-id="2bb38-270">Para excluir um blob, primeiro obtenha uma referência de blob e, em seguida, chame o cmdlet Remove-AzureStorageBlob.</span><span class="sxs-lookup"><span data-stu-id="2bb38-270">To delete a blob, first get a blob reference and then call the Remove-AzureStorageBlob cmdlet on it.</span></span> <span data-ttu-id="2bb38-271">O exemplo a seguir exclui todos os blobs em um determinado contêiner.</span><span class="sxs-lookup"><span data-stu-id="2bb38-271">The following example deletes all the blobs in a given container.</span></span> <span data-ttu-id="2bb38-272">O exemplo primeiro define variáveis para uma conta de armazenamento e, em seguida, cria um contexto de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="2bb38-272">The example first sets variables for a storage account, and then creates a storage context.</span></span> <span data-ttu-id="2bb38-273">Em seguida, o exemplo recupera uma referência de blob usando o cmdlet [Get-AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) e executa o cmdlet [Remove-AzureStorageBlob](/powershell/module/azure.storage/remove-azurestorageblob) para remover os blobs de um contêiner no armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="2bb38-273">Next, the example retrieves a blob reference using the [Get-AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) cmdlet and runs the [Remove-AzureStorageBlob](/powershell/module/azure.storage/remove-azurestorageblob) cmdlet to remove blobs from a container in Azure storage.</span></span>

```powershell
#Define the storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = "Storage key for yourstorageaccount ends with =="
$ContainerName = "containername"
$Ctx = New-AzureStorageContext -StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey

#Get a reference to all the blobs in the container.
$blobs = Get-AzureStorageBlob -Container $ContainerName -Context $Ctx

#Delete blobs in a specified container.
$blobs| Remove-AzureStorageBlob
```

## <a name="how-to-manage-azure-blob-snapshots"></a><span data-ttu-id="2bb38-274">Como gerenciar instantâneos de blob do Azure</span><span class="sxs-lookup"><span data-stu-id="2bb38-274">How to manage Azure blob snapshots</span></span>
<span data-ttu-id="2bb38-275">O Azure permite criar um instantâneo de um blob.</span><span class="sxs-lookup"><span data-stu-id="2bb38-275">Azure lets you create a snapshot of a blob.</span></span> <span data-ttu-id="2bb38-276">Um instantâneo é uma versão somente leitura de um blob capturada em um momento no tempo.</span><span class="sxs-lookup"><span data-stu-id="2bb38-276">A snapshot is a read-only version of a blob that's taken at a point in time.</span></span> <span data-ttu-id="2bb38-277">Quando um instantâneo tiver sido criado, ele pode ser lido, copiado ou excluído, mas não modificado.</span><span class="sxs-lookup"><span data-stu-id="2bb38-277">Once a snapshot has been created, it can be read, copied, or deleted, but not modified.</span></span> <span data-ttu-id="2bb38-278">Os instantâneos fornecem uma maneira de fazer backup de um blob da maneira como ele aparece em um momento específico.</span><span class="sxs-lookup"><span data-stu-id="2bb38-278">Snapshots provide a way to back up a blob as it appears at a moment in time.</span></span> <span data-ttu-id="2bb38-279">Para obter mais informações, consulte [Criar um instantâneo de um blob](http://msdn.microsoft.com/library/azure/hh488361.aspx).</span><span class="sxs-lookup"><span data-stu-id="2bb38-279">For more information, see [Creating a Snapshot of a Blob](http://msdn.microsoft.com/library/azure/hh488361.aspx).</span></span>

### <a name="how-to-create-a-blob-snapshot"></a><span data-ttu-id="2bb38-280">Como criar um instantâneo de blob</span><span class="sxs-lookup"><span data-stu-id="2bb38-280">How to create a blob snapshot</span></span>
<span data-ttu-id="2bb38-281">Para criar um instantâneo de um blob, primeiro obtenha uma referência a um blob e, em seguida, chame o método `ICloudBlob.CreateSnapshot` sobre ele.</span><span class="sxs-lookup"><span data-stu-id="2bb38-281">To create a snaphot of a blob, first get a blob reference and then call the `ICloudBlob.CreateSnapshot` method on it.</span></span> <span data-ttu-id="2bb38-282">O exemplo a seguir define primeiro as variáveis para uma conta de armazenamento e, em seguida, cria um contexto de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="2bb38-282">The following example first sets variables for a storage account, and then creates a storage context.</span></span> <span data-ttu-id="2bb38-283">Em seguida, o exemplo recupera uma referência de blob usando o cmdlet [Get-AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) e executa o método [ICloudBlob.CreateSnapshot](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.icloudblob.aspx) para criar um instantâneo.</span><span class="sxs-lookup"><span data-stu-id="2bb38-283">Next, the example retrieves a blob reference using the [Get-AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) cmdlet and runs the [ICloudBlob.CreateSnapshot](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.icloudblob.aspx) method to create a snapshot.</span></span>

```powershell
#Define the storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = "Storage key for yourstorageaccount ends with =="
$ContainerName = "yourcontainername"
$BlobName = "yourblobname"
$Ctx = New-AzureStorageContext -StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey

#Get a reference to a blob.
$blob = Get-AzureStorageBlob -Context $Ctx -Container $ContainerName -Blob $BlobName

#Create a snapshot of the blob.
$snap = $blob.ICloudBlob.CreateSnapshot()
```

### <a name="how-to-list-a-blobs-snapshots"></a><span data-ttu-id="2bb38-284">Como listar instantâneos de um blob</span><span class="sxs-lookup"><span data-stu-id="2bb38-284">How to list a blob's snapshots</span></span>
<span data-ttu-id="2bb38-285">Você pode criar tantos snapshots quanto desejar para um blob.</span><span class="sxs-lookup"><span data-stu-id="2bb38-285">You can create as many snapshots as you want for a blob.</span></span> <span data-ttu-id="2bb38-286">Você pode listar os instantâneos associados ao seu blob para rastrear seus instantâneos atuais.</span><span class="sxs-lookup"><span data-stu-id="2bb38-286">You can list the snapshots associated with your blob to track your current snapshots.</span></span> <span data-ttu-id="2bb38-287">O exemplo a seguir usa um blob predefinido e chama o cmdlet [Get-AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) para listar os instantâneos desse blob.</span><span class="sxs-lookup"><span data-stu-id="2bb38-287">The following example uses a predefined blob and calls the [Get-AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) cmdlet to list the snapshots of that blob.</span></span>  

```powershell
#Define the blob name.
$BlobName = "yourblobname"

#List the snapshots of a blob.
Get-AzureStorageBlob –Context $Ctx -Prefix $BlobName -Container $ContainerName  | Where-Object  { $_.ICloudBlob.IsSnapshot -and $_.Name -eq $BlobName }
```

### <a name="how-to-copy-a-snapshot-of-a-blob"></a><span data-ttu-id="2bb38-288">Como copiar um instantâneo de um blob</span><span class="sxs-lookup"><span data-stu-id="2bb38-288">How to copy a snapshot of a blob</span></span>
<span data-ttu-id="2bb38-289">Você pode copiar um instantâneo de um blob para restaurar o instantâneo.</span><span class="sxs-lookup"><span data-stu-id="2bb38-289">You can copy a snapshot of a blob to restore the snapshot.</span></span> <span data-ttu-id="2bb38-290">Para obter informações detalhadas e restrições, consulte [Criar um instantâneo de um Blob](http://msdn.microsoft.com/library/azure/hh488361.aspx).</span><span class="sxs-lookup"><span data-stu-id="2bb38-290">For detailed information and restrictions, see [Creating a Snapshot of a Blob](http://msdn.microsoft.com/library/azure/hh488361.aspx).</span></span> <span data-ttu-id="2bb38-291">O exemplo a seguir define primeiro as variáveis para uma conta de armazenamento e, em seguida, cria um contexto de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="2bb38-291">The following example first sets variables for a storage account, and then creates a storage context.</span></span> <span data-ttu-id="2bb38-292">Em seguida, o exemplo define as variáveis de nome de contêiner e blob.</span><span class="sxs-lookup"><span data-stu-id="2bb38-292">Next, the example defines the container and blob name variables.</span></span> <span data-ttu-id="2bb38-293">O exemplo recupera uma referência de blob usando o cmdlet [Get-AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) e executa o método [ICloudBlob.CreateSnapshot](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.icloudblob.aspx) para criar um instantâneo.</span><span class="sxs-lookup"><span data-stu-id="2bb38-293">The example retrieves a blob reference using the [Get-AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) cmdlet and runs the [ICloudBlob.CreateSnapshot](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.icloudblob.aspx) method to create a snapshot.</span></span> <span data-ttu-id="2bb38-294">Em seguida, o exemplo executa o cmdlet [Start-AzureStorageBlobCopy](/powershell/module/azure.storage/start-azurestorageblobcopy) para copiar o instantâneo de um blob usando o objeto ICloudBlob como o blob de origem.</span><span class="sxs-lookup"><span data-stu-id="2bb38-294">Then, the example runs the [Start-AzureStorageBlobCopy](/powershell/module/azure.storage/start-azurestorageblobcopy) cmdlet to copy the snapshot of a blob using the ICloudBlob object for the source blob.</span></span> <span data-ttu-id="2bb38-295">Certifique-se de atualizar as variáveis com base na sua configuração antes de executar o exemplo.</span><span class="sxs-lookup"><span data-stu-id="2bb38-295">Be sure to update the variables based on your configuration before running the example.</span></span> <span data-ttu-id="2bb38-296">Observe que o exemplo a seguir supõe que os contêineres de origem e destino, e o blob de origem, já existem.</span><span class="sxs-lookup"><span data-stu-id="2bb38-296">Note that the following example assumes that the source and destination containers, and the source blob already exist.</span></span>

```powershell
#Define the storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = "Storage key for yourstorageaccount ends with =="
$Ctx = New-AzureStorageContext -StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey

#Define the variables.
$SrcContainerName = "yoursourcecontainername"
$DestContainerName = "yourdestcontainername"
$SrcBlobName = "yourblobname"
$DestBlobName = "CopyBlobName"

#Get a reference to a blob.
$blob = Get-AzureStorageBlob -Context $Ctx -Container $SrcContainerName -Blob $SrcBlobName

#Create a snapshot of a blob.
$snap = $blob.ICloudBlob.CreateSnapshot()

#Copy the snapshot to another container.
Start-AzureStorageBlobCopy –Context $Ctx -ICloudBlob $snap -DestBlob $DestBlobName -DestContainer $DestContainerName
```

<span data-ttu-id="2bb38-297">Agora que você aprendeu a gerenciar blobs do Azure e instantâneos de blob com o Azure PowerShell, vá para a próxima seção para aprender a gerenciar arquivos, filas e tabelas.</span><span class="sxs-lookup"><span data-stu-id="2bb38-297">Now that you have learned how to manage Azure blobs and blob snapshots with Azure PowerShell, go to the next section to learn how to manage tables, queues, and files.</span></span>

## <a name="how-to-manage-azure-tables-and-table-entities"></a><span data-ttu-id="2bb38-298">Como gerenciar tabelas do Azure e entidades de tabela</span><span class="sxs-lookup"><span data-stu-id="2bb38-298">How to manage Azure tables and table entities</span></span>
<span data-ttu-id="2bb38-299">O serviço de armazenamento de tabela do Azure é um armazenamento de dados NoSQL, que pode ser usado para armazenar e consultar grandes conjuntos de dados estruturados e não relacionais.</span><span class="sxs-lookup"><span data-stu-id="2bb38-299">Azure Table storage service is a NoSQL datastore, which you can use to store and query huge sets of structured, non-relational data.</span></span> <span data-ttu-id="2bb38-300">Os principais componentes do serviço são tabelas, entidades e propriedades.</span><span class="sxs-lookup"><span data-stu-id="2bb38-300">The main components of the service are tables, entities, and properties.</span></span> <span data-ttu-id="2bb38-301">Uma tabela é uma coleção de entidades.</span><span class="sxs-lookup"><span data-stu-id="2bb38-301">A table is a collection of entities.</span></span> <span data-ttu-id="2bb38-302">Uma entidade é um conjunto de propriedades.</span><span class="sxs-lookup"><span data-stu-id="2bb38-302">An entity is a set of properties.</span></span> <span data-ttu-id="2bb38-303">Cada entidade pode ter até 252 propriedades, que são todas pares de nome-valor.</span><span class="sxs-lookup"><span data-stu-id="2bb38-303">Each entity can have up to 252 properties, which are all name-value pairs.</span></span> <span data-ttu-id="2bb38-304">Esta seção pressupõe que você já esteja familiarizado com os conceitos do serviço de Armazenamento de Tabela do Azure.</span><span class="sxs-lookup"><span data-stu-id="2bb38-304">This section assumes that you are already familiar with the Azure Table Storage Service concepts.</span></span> <span data-ttu-id="2bb38-305">Para obter informações detalhadas, confira [Understanding the Table Service Data Model](http://msdn.microsoft.com/library/azure/dd179338.aspx) (Noções básicas do modelo de dados do serviço Tabela) e [Introdução ao Armazenamento de Tabelas do Azure usando o .NET](storage-dotnet-how-to-use-tables.md).</span><span class="sxs-lookup"><span data-stu-id="2bb38-305">For detailed information, see [Understanding the Table Service Data Model](http://msdn.microsoft.com/library/azure/dd179338.aspx) and [Get started with Azure Table storage using .NET](storage-dotnet-how-to-use-tables.md).</span></span>

<span data-ttu-id="2bb38-306">Nas subseções a seguir, você aprenderá como gerenciar o serviço de Armazenamento de Tabelas do Azure usando o Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="2bb38-306">In the following subsections, you'll learn how to manage Azure Table storage service using Azure PowerShell.</span></span> <span data-ttu-id="2bb38-307">Os cenários abordados incluem **criação**, **exclusão** e **recuperação** de **tabelas**, bem como **adição**, **consulta** e **exclusão de entidades de tabela**.</span><span class="sxs-lookup"><span data-stu-id="2bb38-307">The scenarios covered include **creating**, **deleting**, and **retrieving** **tables**, as well as **adding**, **querying**, and **deleting table entities**.</span></span>

### <a name="how-to-create-a-table"></a><span data-ttu-id="2bb38-308">Como criar uma tabela</span><span class="sxs-lookup"><span data-stu-id="2bb38-308">How to create a table</span></span>
<span data-ttu-id="2bb38-309">Cada tabela deve residir em uma conta de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="2bb38-309">Every table must reside in an Azure storage account.</span></span> <span data-ttu-id="2bb38-310">O exemplo a seguir demonstra como criar uma tabela no armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="2bb38-310">The following example demonstrates how to create a table in Azure Storage.</span></span> <span data-ttu-id="2bb38-311">O exemplo primeiro estabelece uma conexão com o armazenamento do Azure usando o contexto de conta de armazenamento, que inclui o nome da conta de armazenamento e sua chave de acesso.</span><span class="sxs-lookup"><span data-stu-id="2bb38-311">The example first establishes a connection to Azure Storage using the storage account context, which includes the storage account name and its access key.</span></span> <span data-ttu-id="2bb38-312">Em seguida, ele usa o cmdlet [New-AzureStorageTable](/powershell/module/azure.storage/new-azurestoragetable) para criar uma tabela no armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="2bb38-312">Next, it uses the [New-AzureStorageTable](/powershell/module/azure.storage/new-azurestoragetable) cmdlet to create a table in Azure Storage.</span></span>

```powershell
#Define the storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = "Storage key for yourstorageaccount ends with =="
$Ctx = New-AzureStorageContext $StorageAccountName -StorageAccountKey $StorageAccountKey

#Create a new table.
$tabName = "yourtablename"
New-AzureStorageTable –Name $tabName –Context $Ctx
```

### <a name="how-to-retrieve-a-table"></a><span data-ttu-id="2bb38-313">Como recuperar uma tabela</span><span class="sxs-lookup"><span data-stu-id="2bb38-313">How to retrieve a table</span></span>
<span data-ttu-id="2bb38-314">Você pode consultar e recuperar uma ou todas as tabelas em uma conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="2bb38-314">You can query and retrieve one or all tables in a Storage account.</span></span> <span data-ttu-id="2bb38-315">O exemplo a seguir demonstra como recuperar uma determinada tabela usando o cmdlet [Get-AzureStorageTable](/powershell/module/azure.storage/get-azurestoragetable) .</span><span class="sxs-lookup"><span data-stu-id="2bb38-315">The following example demonstrates how to retrieve a given table using the [Get-AzureStorageTable](/powershell/module/azure.storage/get-azurestoragetable) cmdlet.</span></span>

```powershell
#Retrieve a table.
$tabName = "yourtablename"
Get-AzureStorageTable –Name $tabName –Context $Ctx
```

<span data-ttu-id="2bb38-316">Se você chamar o cmdlet Get-AzureStorageTable sem parâmetros, ele obtém todas as tabelas de armazenamento para uma conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="2bb38-316">If you call the Get-AzureStorageTable cmdlet without any parameters, it gets all storage tables for a Storage account.</span></span>

### <a name="how-to-delete-a-table"></a><span data-ttu-id="2bb38-317">Como excluir uma tabela</span><span class="sxs-lookup"><span data-stu-id="2bb38-317">How to delete a table</span></span>
<span data-ttu-id="2bb38-318">Você pode excluir uma tabela de uma conta de armazenamento usando o cmdlet [Remove-AzureStorageTable](/powershell/module/azure.storage/remove-azurestoragetable) .</span><span class="sxs-lookup"><span data-stu-id="2bb38-318">You can delete a table from a storage account by using the [Remove-AzureStorageTable](/powershell/module/azure.storage/remove-azurestoragetable) cmdlet.</span></span>  

```powershell
#Delete a table.
$tabName = "yourtablename"
Remove-AzureStorageTable –Name $tabName –Context $Ctx
```

### <a name="how-to-manage-table-entities"></a><span data-ttu-id="2bb38-319">Como gerenciar entidades de tabela</span><span class="sxs-lookup"><span data-stu-id="2bb38-319">How to manage table entities</span></span>
<span data-ttu-id="2bb38-320">Atualmente, o PowerShell do Azure não fornece cmdlets para gerenciar entidades de tabela diretamente.</span><span class="sxs-lookup"><span data-stu-id="2bb38-320">Currently, Azure PowerShell does not provide cmdlets to manage table entities directly.</span></span> <span data-ttu-id="2bb38-321">Para executar operações em entidades de tabela, você pode usar as classes fornecidas na [Biblioteca de cliente de armazenamento do Azure para .NET](http://msdn.microsoft.com/library/azure/wa_storage_30_reference_home.aspx).</span><span class="sxs-lookup"><span data-stu-id="2bb38-321">To perform operations on table entities, you can use the classes given in the [Azure Storage Client Library for .NET](http://msdn.microsoft.com/library/azure/wa_storage_30_reference_home.aspx).</span></span>

#### <a name="how-to-add-table-entities"></a><span data-ttu-id="2bb38-322">Como adicionar entidades de tabela</span><span class="sxs-lookup"><span data-stu-id="2bb38-322">How to add table entities</span></span>
<span data-ttu-id="2bb38-323">Para adicionar uma entidade a uma tabela, primeiro crie um objeto que defina as propriedades da entidade.</span><span class="sxs-lookup"><span data-stu-id="2bb38-323">To add an entity to a table, first create an object that defines your entity properties.</span></span> <span data-ttu-id="2bb38-324">Uma entidade pode ter até 255 propriedades, incluindo três propriedades do sistema: **PartitionKey**, **RowKey** e **Timestamp**.</span><span class="sxs-lookup"><span data-stu-id="2bb38-324">An entity can have up to 255 properties, including 3 system properties: **PartitionKey**, **RowKey**, and **Timestamp**.</span></span> <span data-ttu-id="2bb38-325">Você é responsável por inserir e atualizar os valores de **PartitionKey** e **RowKey**.</span><span class="sxs-lookup"><span data-stu-id="2bb38-325">You are responsible for inserting and updating the values of **PartitionKey** and **RowKey**.</span></span> <span data-ttu-id="2bb38-326">O servidor gerencia o valor de **Timestamp**, que não pode ser modificado.</span><span class="sxs-lookup"><span data-stu-id="2bb38-326">The server manages the value of **Timestamp**, which cannot be modified.</span></span> <span data-ttu-id="2bb38-327">Juntas, **PartitionKey** e **RowKey** identificam exclusivamente cada entidade dentro de uma tabela.</span><span class="sxs-lookup"><span data-stu-id="2bb38-327">Together the **PartitionKey** and **RowKey** uniquely identify every entity within a table.</span></span>

* <span data-ttu-id="2bb38-328">**PartitionKey**: determina a partição em que a entidade está armazenada.</span><span class="sxs-lookup"><span data-stu-id="2bb38-328">**PartitionKey**: Determines the partition that the entity is stored in.</span></span>
* <span data-ttu-id="2bb38-329">**RowKey**: identifica exclusivamente a entidade dentro da partição.</span><span class="sxs-lookup"><span data-stu-id="2bb38-329">**RowKey**: Uniquely identifies the entity within the partition.</span></span>

<span data-ttu-id="2bb38-330">Você pode definir até 252 propriedades personalizadas para uma entidade.</span><span class="sxs-lookup"><span data-stu-id="2bb38-330">You may define up to 252 custom properties for an entity.</span></span> <span data-ttu-id="2bb38-331">Para obter informações, consulte [Noções básicas sobre o modelo de dados do serviço Tabela](http://msdn.microsoft.com/library/azure/dd179338.aspx).</span><span class="sxs-lookup"><span data-stu-id="2bb38-331">For more information, see [Understanding the Table Service Data Model](http://msdn.microsoft.com/library/azure/dd179338.aspx).</span></span>

<span data-ttu-id="2bb38-332">O exemplo a seguir demonstra como adicionar entidades a uma tabela.</span><span class="sxs-lookup"><span data-stu-id="2bb38-332">The following example demonstrates how to add entities to a table.</span></span> <span data-ttu-id="2bb38-333">O exemplo mostra como recuperar a tabela de funcionários e adicionar várias entidades a ela.</span><span class="sxs-lookup"><span data-stu-id="2bb38-333">The example shows how to retrieve the employee table and add several entities into it.</span></span> <span data-ttu-id="2bb38-334">Primeiro, ele estabelece uma conexão com o armazenamento do Azure usando o contexto de conta de armazenamento, que inclui o nome da conta de armazenamento e sua chave de acesso primário.</span><span class="sxs-lookup"><span data-stu-id="2bb38-334">First, it establishes a connection to Azure Storage using the storage account context, which includes the storage account name and its access key.</span></span> <span data-ttu-id="2bb38-335">Em seguida, ele recupera a tabela em questão usando o cmdlet [Get-AzureStorageTable](/powershell/module/azure.storage/get-azurestoragetable) .</span><span class="sxs-lookup"><span data-stu-id="2bb38-335">Next, it retrieves the given table using the [Get-AzureStorageTable](/powershell/module/azure.storage/get-azurestoragetable) cmdlet.</span></span> <span data-ttu-id="2bb38-336">Se a tabela não existir, o cmdlet [New-AzureStorageTable](/powershell/module/azure.storage/new-azurestoragetable) é usado para criar uma tabela no armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="2bb38-336">If the table does not exist, the [New-AzureStorageTable](/powershell/module/azure.storage/new-azurestoragetable) cmdlet is used to create a table in Azure Storage.</span></span> <span data-ttu-id="2bb38-337">Em seguida, o exemplo define uma função personalizada Add-Entity para adicionar entidades à tabela especificando a partição de cada entidade e a chave de linha.</span><span class="sxs-lookup"><span data-stu-id="2bb38-337">Next, the example defines a custom function Add-Entity to add entities to the table by specifying each entity's partition and row key.</span></span> <span data-ttu-id="2bb38-338">A função Add-Entity chama o cmdlet [New-Object](http://technet.microsoft.com/library/hh849885.aspx) na classe [Microsoft.WindowsAzure.Storage.Table.DynamicTableEntity](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.dynamictableentity.aspx) para criar um objeto de entidade.</span><span class="sxs-lookup"><span data-stu-id="2bb38-338">The Add-Entity function calls the [New-Object](http://technet.microsoft.com/library/hh849885.aspx) cmdlet on the [Microsoft.WindowsAzure.Storage.Table.DynamicTableEntity](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.dynamictableentity.aspx) class to create an entity object.</span></span> <span data-ttu-id="2bb38-339">Posteriormente, o exemplo chama o método [Microsoft.WindowsAzure.Storage.Table.TableOperation.Insert](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.tableoperation.insert.aspx) nesse objeto de entidade para adicioná-lo a uma tabela.</span><span class="sxs-lookup"><span data-stu-id="2bb38-339">Later, the example calls the [Microsoft.WindowsAzure.Storage.Table.TableOperation.Insert](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.tableoperation.insert.aspx) method on this entity object to add it to a table.</span></span>

```powershell
#Function Add-Entity: Adds an employee entity to a table.
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

#Define the storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
$Ctx = New-AzureStorageContext $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary
$TableName = "Employees"

#Retrieve the table if it already exists.
$table = Get-AzureStorageTable –Name $TableName -Context $Ctx -ErrorAction Ignore

#Create a new table if it does not exist.
if ($table -eq $null)
{
   $table = New-AzureStorageTable –Name $TableName -Context $Ctx
}

#Add multiple entities to a table.
Add-Entity -Table $table -PartitionKey Partition1 -RowKey Row1 -Name Chris -Id 1
Add-Entity -Table $table -PartitionKey Partition1 -RowKey Row2 -Name Jessie -Id 2
Add-Entity -Table $table -PartitionKey Partition2 -RowKey Row1 -Name Christine -Id 3
Add-Entity -Table $table -PartitionKey Partition2 -RowKey Row2 -Name Steven -Id 4
```

#### <a name="how-to-query-table-entities"></a><span data-ttu-id="2bb38-340">Como consultar entidades de tabela</span><span class="sxs-lookup"><span data-stu-id="2bb38-340">How to query table entities</span></span>
<span data-ttu-id="2bb38-341">Para consultar uma tabela, use a classe [Microsoft.WindowsAzure.Storage.Table.TableQuery](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.tablequery.aspx) .</span><span class="sxs-lookup"><span data-stu-id="2bb38-341">To query a table, use the [Microsoft.WindowsAzure.Storage.Table.TableQuery](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.tablequery.aspx) class.</span></span> <span data-ttu-id="2bb38-342">O exemplo a seguir pressupõe que você executou o script fornecido na seção "Como adicionar entidades" deste guia.</span><span class="sxs-lookup"><span data-stu-id="2bb38-342">The following example assumes that you've already run the script given in the How to add entities section of this guide.</span></span> <span data-ttu-id="2bb38-343">O exemplo primeiro estabelece uma conexão com o armazenamento do Azure usando o contexto de armazenamento, que inclui o nome da conta de armazenamento e sua chave de acesso primário.</span><span class="sxs-lookup"><span data-stu-id="2bb38-343">The example first establishes a connection to Azure Storage using the storage context, which includes the storage account name and its access key.</span></span> <span data-ttu-id="2bb38-344">Em seguida, ele tentará recuperar a tabela "Funcionários" criada anteriormente usando o cmdlet [Get-AzureStorageTable](/powershell/module/azure.storage/get-azurestoragetable).</span><span class="sxs-lookup"><span data-stu-id="2bb38-344">Next, it tries to retrieve the previously created "Employees" table using the [Get-AzureStorageTable](/powershell/module/azure.storage/get-azurestoragetable) cmdlet.</span></span> <span data-ttu-id="2bb38-345">Chamar o cmdlet [New-Object](http://technet.microsoft.com/library/hh849885.aspx) na classe Microsoft.WindowsAzure.Storage.Table.TableQuery cria um novo objeto de consulta.</span><span class="sxs-lookup"><span data-stu-id="2bb38-345">Calling the [New-Object](http://technet.microsoft.com/library/hh849885.aspx) cmdlet on the Microsoft.WindowsAzure.Storage.Table.TableQuery class creates a new query object.</span></span> <span data-ttu-id="2bb38-346">O exemplo procura as entidades que têm uma coluna 'ID' cujo valor é 1, conforme especificado em um filtro de cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="2bb38-346">The example looks for the entities that have an 'ID' column whose value is 1 as specified in a string filter.</span></span> <span data-ttu-id="2bb38-347">Para obter informações detalhadas, consulte [Consultando tabelas e entidades](http://msdn.microsoft.com/library/azure/dd894031.aspx).</span><span class="sxs-lookup"><span data-stu-id="2bb38-347">For detailed information, see [Querying Tables and Entities](http://msdn.microsoft.com/library/azure/dd894031.aspx).</span></span> <span data-ttu-id="2bb38-348">Quando você executa essa consulta, ela retorna todas as entidades que correspondem aos critérios de filtro.</span><span class="sxs-lookup"><span data-stu-id="2bb38-348">When you run this query, it returns all entities that match the filter criteria.</span></span>

```powershell
#Define the storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
$Ctx = New-AzureStorageContext –StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary
$TableName = "Employees"

#Get a reference to a table.
$table = Get-AzureStorageTable –Name $TableName -Context $Ctx

#Create a table query.
$query = New-Object Microsoft.WindowsAzure.Storage.Table.TableQuery

#Define columns to select.
$list = New-Object System.Collections.Generic.List[string]
$list.Add("RowKey")
$list.Add("ID")
$list.Add("Name")

#Set query details.
$query.FilterString = "ID gt 0"
$query.SelectColumns = $list
$query.TakeCount = 20

#Execute the query.
$entities = $table.CloudTable.ExecuteQuery($query)

#Display entity properties with the table format.
$entities  | Format-Table PartitionKey, RowKey, @{ Label = "Name"; Expression={$_.Properties["Name"].StringValue}}, @{ Label = "ID"; Expression={$_.Properties["ID"].Int32Value}} -AutoSize
```

#### <a name="how-to-delete-table-entities"></a><span data-ttu-id="2bb38-349">Como excluir entidades de tabela</span><span class="sxs-lookup"><span data-stu-id="2bb38-349">How to delete table entities</span></span>
<span data-ttu-id="2bb38-350">Você pode excluir uma entidade usando suas chaves de partição e de linha.</span><span class="sxs-lookup"><span data-stu-id="2bb38-350">You can delete an entity using its partition and row keys.</span></span> <span data-ttu-id="2bb38-351">O exemplo a seguir pressupõe que você executou o script fornecido na seção "Como adicionar entidades" deste guia.</span><span class="sxs-lookup"><span data-stu-id="2bb38-351">The following example assumes that you've already run the script given in the How to add entities section of this guide.</span></span> <span data-ttu-id="2bb38-352">O exemplo primeiro estabelece uma conexão com o armazenamento do Azure usando o contexto de armazenamento, que inclui o nome da conta de armazenamento e sua chave de acesso primário.</span><span class="sxs-lookup"><span data-stu-id="2bb38-352">The example first establishes a connection to Azure Storage using the storage context, which includes the storage account name and its access key.</span></span> <span data-ttu-id="2bb38-353">Em seguida, ele tentará recuperar a tabela "Funcionários" criada anteriormente usando o cmdlet [Get-AzureStorageTable](/powershell/module/azure.storage/get-azurestoragetable).</span><span class="sxs-lookup"><span data-stu-id="2bb38-353">Next, it tries to retrieve the previously created "Employees" table using the [Get-AzureStorageTable](/powershell/module/azure.storage/get-azurestoragetable) cmdlet.</span></span> <span data-ttu-id="2bb38-354">Se a tabela existir, o exemplo chamará o método [Microsoft.WindowsAzure.Storage.Table.TableOperation.Retrieve](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.tableoperation.retrieve.aspx) para recuperar uma entidade com base em seus valores de chave de partição e de linha.</span><span class="sxs-lookup"><span data-stu-id="2bb38-354">If the table exists, the example calls the [Microsoft.WindowsAzure.Storage.Table.TableOperation.Retrieve](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.tableoperation.retrieve.aspx) method to retrieve an entity based on its partition and row key values.</span></span> <span data-ttu-id="2bb38-355">Em seguida, transmita a entidade para o método [Microsoft.WindowsAzure.Storage.Table.TableOperation.Delete](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.tableoperation.delete.aspx) para excluir.</span><span class="sxs-lookup"><span data-stu-id="2bb38-355">Then, pass the entity to the [Microsoft.WindowsAzure.Storage.Table.TableOperation.Delete](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.tableoperation.delete.aspx) method to delete.</span></span>

```powershell
#Define the storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
$Ctx = New-AzureStorageContext –StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary

#Retrieve the table.
$TableName = "Employees"
$table = Get-AzureStorageTable -Name $TableName -Context $Ctx -ErrorAction Ignore

#If the table exists, start deleting its entities.
if ($table -ne $null) 
{
    #Together the PartitionKey and RowKey uniquely identify every  
    #entity within a table.
    $tableResult = $table.CloudTable.Execute([Microsoft.WindowsAzure.Storage.Table.TableOperation]::Retrieve("Partition2", "Row1"))
    $entity = $tableResult.Result
    if ($entity -ne $null)
    {
        #Delete the entity.
        $table.CloudTable.Execute([Microsoft.WindowsAzure.Storage.Table.TableOperation]::Delete($entity))
    }
}
```

## <a name="how-to-manage-azure-queues-and-queue-messages"></a><span data-ttu-id="2bb38-356">Como gerenciar filas do Azure e mensagens da fila</span><span class="sxs-lookup"><span data-stu-id="2bb38-356">How to manage Azure queues and queue messages</span></span>
<span data-ttu-id="2bb38-357">O armazenamento de filas do Azure é um serviço para armazenamento de um grande número de mensagens que podem ser acessadas de qualquer lugar do mundo por meio de chamadas autenticadas usando HTTP ou HTTPS.</span><span class="sxs-lookup"><span data-stu-id="2bb38-357">Azure Queue storage is a service for storing large numbers of messages that can be accessed from anywhere in the world via authenticated calls using HTTP or HTTPS.</span></span> <span data-ttu-id="2bb38-358">Esta seção pressupõe que você já esteja familiarizado com os conceitos do serviço de Armazenamento de Filas do Azure.</span><span class="sxs-lookup"><span data-stu-id="2bb38-358">This section assumes that you are already familiar with the Azure Queue Storage Service concepts.</span></span> <span data-ttu-id="2bb38-359">Para obter informações detalhadas, confira [Introdução ao Armazenamento de Filas do Azure usando o .NET](storage-dotnet-how-to-use-queues.md).</span><span class="sxs-lookup"><span data-stu-id="2bb38-359">For detailed information, see [Get started with Azure Queue storage using .NET](storage-dotnet-how-to-use-queues.md).</span></span>

<span data-ttu-id="2bb38-360">Esta seção mostrará como gerenciar o serviço de armazenamento de filas do Azure usando o PowerShell do Azure.</span><span class="sxs-lookup"><span data-stu-id="2bb38-360">This section will show you how to manage Azure Queue storage service using Azure PowerShell.</span></span> <span data-ttu-id="2bb38-361">Os cenários abordados incluem **inserção** e **exclusão** de mensagens da fila, bem como **criação**, **exclusão** e **recuperação de filas**.</span><span class="sxs-lookup"><span data-stu-id="2bb38-361">The scenarios covered include **inserting** and **deleting** queue messages, as well as **creating**, **deleting**, and **retrieving queues**.</span></span>

### <a name="how-to-create-a-queue"></a><span data-ttu-id="2bb38-362">Como criar uma fila</span><span class="sxs-lookup"><span data-stu-id="2bb38-362">How to create a queue</span></span>
<span data-ttu-id="2bb38-363">O exemplo a seguir primeiro estabelece uma conexão com o armazenamento do Azure usando o contexto de conta de armazenamento, que inclui o nome da conta de armazenamento e sua chave de acesso primária.</span><span class="sxs-lookup"><span data-stu-id="2bb38-363">The following example first establishes a connection to Azure Storage using the storage account context, which includes the storage account name and its access key.</span></span> <span data-ttu-id="2bb38-364">-Em seguida, ele chama o cmdlet [New-AzureStorageQueue](/powershell/module/azure.storage/new-azurestoragequeue) para criar uma fila denominada 'queuename'.</span><span class="sxs-lookup"><span data-stu-id="2bb38-364">Next, it calls [New-AzureStorageQueue](/powershell/module/azure.storage/new-azurestoragequeue) cmdlet to create a queue named 'queuename'.</span></span>

```powershell
#Define the storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
$Ctx = New-AzureStorageContext –StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary
$QueueName = "queuename"
$Queue = New-AzureStorageQueue –Name $QueueName -Context $Ctx
```

<span data-ttu-id="2bb38-365">Para obter informações sobre convenções de nomenclatura do serviço Fila do Azure, consulte [Nomear filas e metadados](http://msdn.microsoft.com/library/azure/dd179349.aspx).</span><span class="sxs-lookup"><span data-stu-id="2bb38-365">For information on naming conventions for Azure Queue Service, see [Naming Queues and Metadata](http://msdn.microsoft.com/library/azure/dd179349.aspx).</span></span>

### <a name="how-to-retrieve-a-queue"></a><span data-ttu-id="2bb38-366">Como recuperar uma fila</span><span class="sxs-lookup"><span data-stu-id="2bb38-366">How to retrieve a queue</span></span>
<span data-ttu-id="2bb38-367">Você pode consultar e recuperar uma lista de todas as filas em uma conta de armazenamento ou de uma fila específica.</span><span class="sxs-lookup"><span data-stu-id="2bb38-367">You can query and retrieve a specific queue or a list of all the queues in a Storage account.</span></span> <span data-ttu-id="2bb38-368">O exemplo a seguir demonstra como recuperar uma determinada fila usando o cmdlet [Get-AzureStorageQueue](/powershell/module/azure.storage/get-azurestoragequeue) .</span><span class="sxs-lookup"><span data-stu-id="2bb38-368">The following example demonstrates how to retrieve a specified queue using the [Get-AzureStorageQueue](/powershell/module/azure.storage/get-azurestoragequeue) cmdlet.</span></span>

```powershell
#Retrieve a queue.
$QueueName = "queuename"
$Queue = Get-AzureStorageQueue –Name $QueueName –Context $Ctx
```

<span data-ttu-id="2bb38-369">Se você chamar o cmdlet [Get-AzureStorageQueue](/powershell/module/azure.storage/get-azurestoragequeue) sem parâmetros, ele obtém uma lista de todas as filas.</span><span class="sxs-lookup"><span data-stu-id="2bb38-369">If you call the [Get-AzureStorageQueue](/powershell/module/azure.storage/get-azurestoragequeue) cmdlet without any parameters, it gets a list of all the queues.</span></span>

### <a name="how-to-delete-a-queue"></a><span data-ttu-id="2bb38-370">Como excluir uma fila</span><span class="sxs-lookup"><span data-stu-id="2bb38-370">How to delete a queue</span></span>
<span data-ttu-id="2bb38-371">Para excluir uma fila e todas as mensagens contidas nela, chame o cmdlet Remove-AzureStorageQueue.</span><span class="sxs-lookup"><span data-stu-id="2bb38-371">To delete a queue and all the messages contained in it, call the Remove-AzureStorageQueue cmdlet.</span></span> <span data-ttu-id="2bb38-372">O exemplo a seguir demonstra como excluir uma determinada fila usando o cmdlet Remove-AzureStorageQueue.</span><span class="sxs-lookup"><span data-stu-id="2bb38-372">The following example shows how to delete a specified queue using the Remove-AzureStorageQueue cmdlet.</span></span>

```powershell
#Delete a queue.
$QueueName = "yourqueuename"
Remove-AzureStorageQueue –Name $QueueName –Context $Ctx
```

#### <a name="how-to-insert-a-message-into-a-queue"></a><span data-ttu-id="2bb38-373">Como inserir uma mensagem em uma fila</span><span class="sxs-lookup"><span data-stu-id="2bb38-373">How to insert a message into a queue</span></span>
<span data-ttu-id="2bb38-374">Para inserir uma mensagem em uma fila existente, primeiro crie uma nova instância da classe [Microsoft.WindowsAzure.Storage.Queue.CloudQueueMessage](http://msdn.microsoft.com/library/azure/jj732474.aspx) .</span><span class="sxs-lookup"><span data-stu-id="2bb38-374">To insert a message into an existing queue, first create a new instance of the [Microsoft.WindowsAzure.Storage.Queue.CloudQueueMessage](http://msdn.microsoft.com/library/azure/jj732474.aspx) class.</span></span> <span data-ttu-id="2bb38-375">Em seguida, chame o método [AddMessage](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.addmessage.aspx) .</span><span class="sxs-lookup"><span data-stu-id="2bb38-375">Next, call the [AddMessage](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.addmessage.aspx) method.</span></span> <span data-ttu-id="2bb38-376">Um CloudQueueMessage pode ser criado por meio de uma cadeia de caracteres (em formato UTF-8) ou de uma matriz de bytes.</span><span class="sxs-lookup"><span data-stu-id="2bb38-376">A CloudQueueMessage can be created from either a string (in UTF-8 format) or a byte array.</span></span>

<span data-ttu-id="2bb38-377">O exemplo a seguir demonstra como adicionar uma mensagem a uma fila.</span><span class="sxs-lookup"><span data-stu-id="2bb38-377">The following example demonstrates how to add message to a queue.</span></span> <span data-ttu-id="2bb38-378">O exemplo primeiro estabelece uma conexão com o armazenamento do Azure usando o contexto de conta de armazenamento, que inclui o nome da conta de armazenamento e sua chave de acesso.</span><span class="sxs-lookup"><span data-stu-id="2bb38-378">The example first establishes a connection to Azure Storage using the storage account context, which includes the storage account name and its access key.</span></span> <span data-ttu-id="2bb38-379">Em seguida, ele recupera a fila especificada usando o cmdlet [Get-AzureStorageQueue](https://msdn.microsoft.com/library/azure/dn806377.aspx) .</span><span class="sxs-lookup"><span data-stu-id="2bb38-379">Next, it retrieves the specified queue using the [Get-AzureStorageQueue](https://msdn.microsoft.com/library/azure/dn806377.aspx) cmdlet.</span></span> <span data-ttu-id="2bb38-380">Se a fila existir, o cmdlet [New-Object](http://technet.microsoft.com/library/hh849885.aspx) será usado para criar uma instância da classe [Microsoft.WindowsAzure.Storage.Queue.CloudQueueMessage](http://msdn.microsoft.com/library/azure/jj732474.aspx).</span><span class="sxs-lookup"><span data-stu-id="2bb38-380">If the queue exists, the [New-Object](http://technet.microsoft.com/library/hh849885.aspx) cmdlet is used to create an instance of the [Microsoft.WindowsAzure.Storage.Queue.CloudQueueMessage](http://msdn.microsoft.com/library/azure/jj732474.aspx) class.</span></span> <span data-ttu-id="2bb38-381">Posteriormente, o exemplo chama o método [AddMessage](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.addmessage.aspx) nesse objeto de mensagem para adicioná-lo a uma fila.</span><span class="sxs-lookup"><span data-stu-id="2bb38-381">Later, the example calls the [AddMessage](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.addmessage.aspx) method on this message object to add it to a queue.</span></span> <span data-ttu-id="2bb38-382">Aqui está o código que recupera uma fila e insere a mensagem 'MessageInfo':</span><span class="sxs-lookup"><span data-stu-id="2bb38-382">Here is code which retrieves a queue and inserts the message 'MessageInfo':</span></span>

```powershell
#Define the storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
$Ctx = New-AzureStorageContext –StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary

#Retrieve the queue.
$QueueName = "queuename"
$Queue = Get-AzureStorageQueue -Name $QueueName -Context $ctx

#If the queue exists, add a new message.
if ($Queue -ne $null) {
   # Create a new message using a constructor of the CloudQueueMessage class.
   $QueueMessage = New-Object -TypeName Microsoft.WindowsAzure.Storage.Queue.CloudQueueMessage -ArgumentList MessageInfo

   # Add a new message to the queue.
   $Queue.CloudQueue.AddMessage($QueueMessage)
}
```

#### <a name="how-to-de-queue-at-the-next-message"></a><span data-ttu-id="2bb38-383">Como retirar a próxima mensagem da fila</span><span class="sxs-lookup"><span data-stu-id="2bb38-383">How to de-queue at the next message</span></span>
<span data-ttu-id="2bb38-384">Seu código remove uma mensagem de um fila em duas etapas.</span><span class="sxs-lookup"><span data-stu-id="2bb38-384">Your code de-queues a message from a queue in two steps.</span></span> <span data-ttu-id="2bb38-385">Quando você chamar o método [Microsoft.WindowsAzure.Storage.Queue.CloudQueue.GetMessage](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.getmessage.aspx) , receberá a próxima mensagem em uma fila.</span><span class="sxs-lookup"><span data-stu-id="2bb38-385">When you call the [Microsoft.WindowsAzure.Storage.Queue.CloudQueue.GetMessage](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.getmessage.aspx) method, you get the next message in a queue.</span></span> <span data-ttu-id="2bb38-386">Uma mensagem retornada de **GetMessage** torna-se invisível para todas as outras mensagens de leitura de código da fila.</span><span class="sxs-lookup"><span data-stu-id="2bb38-386">A message returned from **GetMessage** becomes invisible to any other code reading messages from this queue.</span></span> <span data-ttu-id="2bb38-387">Para concluir a remoção da mensagem da fila, você também deve chamar o método [Microsoft.WindowsAzure.Storage.Queue.CloudQueue.DeleteMessage](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.deletemessage.aspx) .</span><span class="sxs-lookup"><span data-stu-id="2bb38-387">To finish removing the message from the queue, you must also call the [Microsoft.WindowsAzure.Storage.Queue.CloudQueue.DeleteMessage](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.deletemessage.aspx) method.</span></span> <span data-ttu-id="2bb38-388">Este processo de duas etapas de remover uma mensagem garante que quando o código não processa uma mensagem devido à falhas de hardware ou de software, outra instância do seu código pode receber a mesma mensagem e tentar novamente.</span><span class="sxs-lookup"><span data-stu-id="2bb38-388">This two-step process of removing a message assures that if your code fails to process a message due to hardware or software failure, another instance of your code can get the same message and try again.</span></span> <span data-ttu-id="2bb38-389">Seu código chama **DeleteMessage** logo depois que a mensagem é processada.</span><span class="sxs-lookup"><span data-stu-id="2bb38-389">Your code calls **DeleteMessage** right after the message has been processed.</span></span>

```powershell
# Define the storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
$Ctx = New-AzureStorageContext –StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary

# Retrieve the queue.
$QueueName = "queuename"
$Queue = Get-AzureStorageQueue -Name $QueueName -Context $ctx

$InvisibleTimeout = [System.TimeSpan]::FromSeconds(10)

# Get the message object from the queue.
$QueueMessage = $Queue.CloudQueue.GetMessage($InvisibleTimeout)
# Delete the message.
$Queue.CloudQueue.DeleteMessage($QueueMessage)
```

## <a name="how-to-manage-azure-file-shares-and-files"></a><span data-ttu-id="2bb38-390">Como gerenciar arquivos e compartilhamentos de arquivos do Azure</span><span class="sxs-lookup"><span data-stu-id="2bb38-390">How to manage Azure file shares and files</span></span>
<span data-ttu-id="2bb38-391">O Armazenamento de Arquivos do Azure oferece o armazenamento compartilhado para aplicativos com o uso do protocolo SMB padrão.</span><span class="sxs-lookup"><span data-stu-id="2bb38-391">Azure File storage offers shared storage for applications using the standard SMB protocol.</span></span> <span data-ttu-id="2bb38-392">As máquinas virtuais e os serviços de nuvem do Microsoft Azure podem compartilhar dados de arquivos entre componentes de aplicativos por meio de compartilhamentos montados, e aplicativos locais podem acessar dados de arquivos em um compartilhamento por meio da API de armazenamento de arquivo ou o Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="2bb38-392">Microsoft Azure virtual machines and cloud services can share file data across application components via mounted shares, and on-premises applications can access file data in a share via the File storage API or Azure PowerShell.</span></span>

<span data-ttu-id="2bb38-393">Para obter mais informações sobre o armazenamento de Arquivos do Azure, confira [Introdução ao Armazenamento de Arquivos do Azure no Windows](storage-dotnet-how-to-use-files.md) e [File Service REST API](http://msdn.microsoft.com/library/azure/dn167006.aspx) (API REST do serviço Arquivo).</span><span class="sxs-lookup"><span data-stu-id="2bb38-393">For more information on Azure File storage, see [Get started with Azure File storage on Windows](storage-dotnet-how-to-use-files.md) and [File Service REST API](http://msdn.microsoft.com/library/azure/dn167006.aspx).</span></span>

## <a name="how-to-set-and-query-storage-analytics"></a><span data-ttu-id="2bb38-394">Como definir e consultar análises de armazenamento</span><span class="sxs-lookup"><span data-stu-id="2bb38-394">How to set and query storage analytics</span></span>
<span data-ttu-id="2bb38-395">Você pode usar a [Análise de armazenamento do Azure](storage-analytics.md) para coletar métricas para suas contas de armazenamento do Azure e registrar dados sobre solicitações enviadas à sua conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="2bb38-395">You can use [Azure Storage Analytics](storage-analytics.md) to collect metrics for your Azure storage accounts and log data about requests sent to your storage account.</span></span> <span data-ttu-id="2bb38-396">Você pode usar métricas de armazenamento para monitorar a integridade de uma conta de armazenamento, e log de armazenamento para diagnosticar e solucionar problemas com sua conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="2bb38-396">You can use storage metrics to monitor the health of a storage account, and storage logging to diagnose and troubleshoot issues with your storage account.</span></span> <span data-ttu-id="2bb38-397">Você pode configurar o monitoramento usando o Portal do Azure, o Windows PowerShell ou de forma programática usando a biblioteca de clientes de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="2bb38-397">You can configure monitoring using the Azure portal or Windows PowerShell, or programmatically using the storage client library.</span></span> <span data-ttu-id="2bb38-398">O log de armazenamento ocorre no lado do servidor e permite que você registre detalhes de solicitações bem-sucedidas e com falhas na conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="2bb38-398">Storage logging happens server-side and enables you to record details for both successful and failed requests in your storage account.</span></span> <span data-ttu-id="2bb38-399">Esses registros permitem ver detalhes de operações de leitura, gravação e exclusão em suas tabelas, filas e blobs bem como as razões para solicitações com falha.</span><span class="sxs-lookup"><span data-stu-id="2bb38-399">These logs enable you to see details of read, write, and delete operations against your tables, queues, and blobs as well as the reasons for failed requests.</span></span>

<span data-ttu-id="2bb38-400">Para saber como habilitar e exibir dados de métricas de armazenamento usando o PowerShell, consulte [Como habilitar métricas de armazenamento usando o PowerShell](http://msdn.microsoft.com/library/azure/dn782843.aspx#HowtoenableStorageMetricsusingPowerShell).</span><span class="sxs-lookup"><span data-stu-id="2bb38-400">To learn how to enable and view Storage Metrics data using PowerShell, see [How to enable Storage Metrics using PowerShell](http://msdn.microsoft.com/library/azure/dn782843.aspx#HowtoenableStorageMetricsusingPowerShell).</span></span>

<span data-ttu-id="2bb38-401">Para saber como habilitar e recuperar dados de log de armazenamento usando o PowerShell, confira [How to enable Storage Logging using PowerShell](http://msdn.microsoft.com/library/azure/dn782840.aspx#HowtoenableStorageLoggingusingPowerShell) (Como habilitar o log de armazenamento usando o PowerShell) e [Finding your Storage Logging log data](http://msdn.microsoft.com/library/azure/dn782840.aspx#FindingyourStorageLogginglogdata) (Localizando os dados do log de armazenamento).</span><span class="sxs-lookup"><span data-stu-id="2bb38-401">To learn how to enable and retrieve Storage Logging data using PowerShell, see [How to enable Storage Logging using PowerShell](http://msdn.microsoft.com/library/azure/dn782840.aspx#HowtoenableStorageLoggingusingPowerShell) and [Finding your Storage Logging log data](http://msdn.microsoft.com/library/azure/dn782840.aspx#FindingyourStorageLogginglogdata).</span></span>
<span data-ttu-id="2bb38-402">Para obter informações detalhadas sobre o uso de métricas de armazenamento e do armazenamento de log para solucionar problemas de armazenamento, consulte [Monitoramento, diagnóstico e solução de problemas de Armazenamento do Microsoft Azure](storage-monitoring-diagnosing-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="2bb38-402">For detailed information on using Storage Metrics and Storage Logging to troubleshoot storage issues, see [Monitoring, Diagnosing, and Troubleshooting Microsoft Azure Storage](storage-monitoring-diagnosing-troubleshooting.md).</span></span>

## <a name="how-to-manage-shared-access-signature-sas-and-stored-access-policy"></a><span data-ttu-id="2bb38-403">Como gerenciar a Assinatura de Acesso Compartilhado (SAS) e a Política de Acesso Armazenada</span><span class="sxs-lookup"><span data-stu-id="2bb38-403">How to manage Shared Access Signature (SAS) and Stored Access Policy</span></span>
<span data-ttu-id="2bb38-404">Assinaturas de acesso compartilhado são uma parte importante do modelo de segurança para qualquer aplicativo que utilize o Armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="2bb38-404">Shared access signatures are an important part of the security model for any application using Azure Storage.</span></span> <span data-ttu-id="2bb38-405">Elas são úteis para fornecer permissões limitadas para a sua conta de armazenamento aos clientes que não devem ter a chave de conta.</span><span class="sxs-lookup"><span data-stu-id="2bb38-405">They are useful for providing limited permissions to your storage account to clients that should not have the account key.</span></span> <span data-ttu-id="2bb38-406">Por padrão, somente o proprietário da conta de armazenamento pode acessar blobs, tabelas e filas nessa conta.</span><span class="sxs-lookup"><span data-stu-id="2bb38-406">By default, only the owner of the storage account may access blobs, tables, and queues within that account.</span></span> <span data-ttu-id="2bb38-407">Se seu serviço ou aplicativo precisar tornar esses recursos disponíveis para outros clientes sem compartilhar sua chave de acesso, você tem três opções:</span><span class="sxs-lookup"><span data-stu-id="2bb38-407">If your service or application needs to make these resources available to other clients without sharing your access key, you have three options:</span></span>

* <span data-ttu-id="2bb38-408">Definir permissões do contêiner para permitir o acesso anônimo de leitura para o contêiner e seus blobs.</span><span class="sxs-lookup"><span data-stu-id="2bb38-408">Set a container's permissions to permit anonymous read access to the container and its blobs.</span></span> <span data-ttu-id="2bb38-409">Isso não é permitido para tabelas ou filas.</span><span class="sxs-lookup"><span data-stu-id="2bb38-409">This is not allowed for tables or queues.</span></span>
* <span data-ttu-id="2bb38-410">Usar uma assinatura de acesso compartilhado que concede direitos de acesso restrito para contêineres, blobs, filas e tabelas por um intervalo de tempo específico.</span><span class="sxs-lookup"><span data-stu-id="2bb38-410">Use a shared access signature that grants restricted access rights to containers, blobs, queues, and tables for a specific time interval.</span></span>
* <span data-ttu-id="2bb38-411">Usar uma política de acesso armazenado para obter um nível adicional de controle sobre assinaturas de acesso compartilhado para um contêiner ou seus blobs, uma fila ou uma tabela.</span><span class="sxs-lookup"><span data-stu-id="2bb38-411">Use a stored access policy to obtain an additional level of control over shared access signatures for a container or its blobs, for a queue, or for a table.</span></span> <span data-ttu-id="2bb38-412">A política de acesso armazenado permite que você altere a hora de início, a hora de término ou as permissões para uma assinatura ou revogue-a depois que ela tiver sido emitida.</span><span class="sxs-lookup"><span data-stu-id="2bb38-412">The stored access policy allows you to change the start time, expiry time, or permissions for a signature, or to revoke it after it has been issued.</span></span>

<span data-ttu-id="2bb38-413">Uma assinatura de acesso compartilhado pode estar em uma das duas formas:</span><span class="sxs-lookup"><span data-stu-id="2bb38-413">A shared access signature can be in one of two forms:</span></span>

* <span data-ttu-id="2bb38-414">**SAS ad hoc**: quando você cria uma SAS ad hoc, a hora de início, a hora de término e as permissões para a SAS são especificadas no URI SAS.</span><span class="sxs-lookup"><span data-stu-id="2bb38-414">**Ad hoc SAS**: When you create an ad hoc SAS, the start time, expiry time, and permissions for the SAS are all specified on the SAS URI.</span></span> <span data-ttu-id="2bb38-415">Esse tipo de SAS pode ser criado em um contêiner, blob, tabela ou fila e não pode ser revogado.</span><span class="sxs-lookup"><span data-stu-id="2bb38-415">This type of SAS may be created on a container, blob, table, or queue and it is non-revocable.</span></span>
* <span data-ttu-id="2bb38-416">**SAS com política de acesso armazenada:**uma política de acesso armazenada é definida em um contêiner de recurso - um contêiner de blob, uma tabela ou uma fila - e pode ser usada para gerenciar as restrições de uma ou mais assinaturas de acesso compartilhado.</span><span class="sxs-lookup"><span data-stu-id="2bb38-416">**SAS with stored access policy**: A stored access policy is defined on a resource container a blob container, table, or queue - and you can use it to manage constraints for one or more shared access signatures.</span></span> <span data-ttu-id="2bb38-417">Quando você associa uma SAS a uma política de acesso armazenada, a SAS herda as restrições - a hora de início, a hora de expiração e as permissões - definidas para a política de acesso armazenada.</span><span class="sxs-lookup"><span data-stu-id="2bb38-417">When you associate a SAS with a stored access policy, the SAS inherits the constraints - the start time, expiry time, and permissions - defined for the stored access policy.</span></span> <span data-ttu-id="2bb38-418">Esse tipo de SAS pode ser revogado.</span><span class="sxs-lookup"><span data-stu-id="2bb38-418">This type of SAS is revocable.</span></span>

<span data-ttu-id="2bb38-419">Para saber mais, veja [Uso de SAS (Assinaturas de Acesso Compartilhado)](storage-dotnet-shared-access-signature-part-1.md) e [Gerenciar acesso de leitura anônimo aos contêineres e blobs](storage-manage-access-to-resources.md).</span><span class="sxs-lookup"><span data-stu-id="2bb38-419">For more information, see [Using Shared Access Signatures (SAS)](storage-dotnet-shared-access-signature-part-1.md) and [Manage anonymous read access to containers and blobs](storage-manage-access-to-resources.md).</span></span>

<span data-ttu-id="2bb38-420">Nas seções a seguir, você aprenderá a como criar uma política de acesso armazenado e um token de assinatura de acesso compartilhado para tabelas do Azure.</span><span class="sxs-lookup"><span data-stu-id="2bb38-420">In the next sections, you will learn how to create a shared access signature token and stored access policy for Azure tables.</span></span> <span data-ttu-id="2bb38-421">O PowerShell do Azure fornece cmdlets semelhantes para contêineres, blobs e filas.</span><span class="sxs-lookup"><span data-stu-id="2bb38-421">Azure PowerShell provides similar cmdlets for containers, blobs, and queues as well.</span></span> <span data-ttu-id="2bb38-422">Para executar os scripts nesta seção, baixe o [Azure PowerShell versão 0.8.14](http://go.microsoft.com/?linkid=9811175&clcid=0x409) ou posterior.</span><span class="sxs-lookup"><span data-stu-id="2bb38-422">To run the scripts in this section, download the [Azure PowerShell version 0.8.14](http://go.microsoft.com/?linkid=9811175&clcid=0x409) or later.</span></span>

### <a name="how-to-create-a-policy-based-shared-access-signature-token"></a><span data-ttu-id="2bb38-423">Como criar uma política baseada no token de Assinatura de Acesso Compartilhado</span><span class="sxs-lookup"><span data-stu-id="2bb38-423">How to create a policy-based Shared Access Signature token</span></span>
<span data-ttu-id="2bb38-424">Use o cmdlet New-AzureStorageTableStoredAccessPolicy para criar uma nova política de acesso armazenada.</span><span class="sxs-lookup"><span data-stu-id="2bb38-424">Use the New-AzureStorageTableStoredAccessPolicy cmdlet to create a new stored access policy.</span></span> <span data-ttu-id="2bb38-425">Em seguida, chame o cmdlet [New-AzureStorageTableSASToken](/powershell/module/azure.storage/new-azurestoragetablesastoken) para criar um novo token de assinatura de acesso compartilhado com base em política para uma Tabela de Armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="2bb38-425">Then, call the [New-AzureStorageTableSASToken](/powershell/module/azure.storage/new-azurestoragetablesastoken) cmdlet to create a new policy-based shared access signature token for an Azure Storage table.</span></span>

```powershell
$policy = "policy1"
New-AzureStorageTableStoredAccessPolicy -Name $tableName -Policy $policy -Permission "rd" -StartTime "2015-01-01" -ExpiryTime "2016-01-01" -Context $Ctx
New-AzureStorageTableSASToken -Name $tableName -Policy $policy -Context $Ctx
```

### <a name="how-to-create-an-ad-hoc-non-revocable-shared-access-signature-token"></a><span data-ttu-id="2bb38-426">Como criar um token ad hoc de Assinatura de Acesso Compartilhado (não revogável)</span><span class="sxs-lookup"><span data-stu-id="2bb38-426">How to create an ad hoc (non-revocable) Shared Access Signature token</span></span>
<span data-ttu-id="2bb38-427">Use o cmdlet [New-AzureStorageTableSASToken](/powershell/module/azure.storage/new-azurestoragetablesastoken) para criar um novo token ad hoc de Assinatura de Acesso Compartilhado (não revogável) para uma tabela de Armazenamento do Azure:</span><span class="sxs-lookup"><span data-stu-id="2bb38-427">Use the [New-AzureStorageTableSASToken](/powershell/module/azure.storage/new-azurestoragetablesastoken) cmdlet to create a new ad hoc (non-revocable) Shared Access Signature token for an Azure Storage table:</span></span>

```powershell
New-AzureStorageTableSASToken -Name $tableName -Permission "rqud" -StartTime "2015-01-01" -ExpiryTime "2015-02-01" -Context $Ctx
```
    
### <a name="how-to-create-a-stored-access-policy"></a><span data-ttu-id="2bb38-428">Como criar uma política de acesso armazenada</span><span class="sxs-lookup"><span data-stu-id="2bb38-428">How to create a stored access policy</span></span>
<span data-ttu-id="2bb38-429">Use o cmdlet New-AzureStorageTableStoredAccessPolicy para criar uma nova política de acesso armazenada para uma tabela de armazenamento do Azure:</span><span class="sxs-lookup"><span data-stu-id="2bb38-429">Use the New-AzureStorageTableStoredAccessPolicy cmdlet to create a new stored access policy for an Azure Storage table:</span></span>

```powershell
$policy = "policy1"
New-AzureStorageTableStoredAccessPolicy -Name $tableName -Policy $policy -Permission "rd" -StartTime "2015-01-01" -ExpiryTime "2016-01-01" -Context $Ctx
```
    
### <a name="how-to-update-a-stored-access-policy"></a><span data-ttu-id="2bb38-430">Como atualizar uma política de acesso armazenada</span><span class="sxs-lookup"><span data-stu-id="2bb38-430">How to update a stored access policy</span></span>
<span data-ttu-id="2bb38-431">Use o cmdlet Set-AzureStorageTableStoredAccessPolicy para atualizar uma política de acesso armazenada existente para uma tabela de armazenamento do Azure:</span><span class="sxs-lookup"><span data-stu-id="2bb38-431">Use the Set-AzureStorageTableStoredAccessPolicy cmdlet to update an existing stored access policy for an Azure Storage table:</span></span>

```powershell
Set-AzureStorageTableStoredAccessPolicy -Policy $policy -Table $tableName -Permission "rd" -NoExpiryTime -NoStartTime -Context $Ctx
```

### <a name="how-to-delete-a-stored-access-policy"></a><span data-ttu-id="2bb38-432">Como excluir uma política de acesso armazenada</span><span class="sxs-lookup"><span data-stu-id="2bb38-432">How to delete a stored access policy</span></span>
<span data-ttu-id="2bb38-433">Use o cmdlet Remove-AzureStorageTableStoredAccessPolicy para excluir uma política de acesso armazenada em uma tabela de armazenamento do Azure:</span><span class="sxs-lookup"><span data-stu-id="2bb38-433">Use the Remove-AzureStorageTableStoredAccessPolicy cmdlet to delete a stored access policy on an Azure Storage table:</span></span>

```powershell
Remove-AzureStorageTableStoredAccessPolicy -Policy $policy -Table $tableName -Context $Ctx
```

## <a name="how-to-use-azure-storage-for-us-government-and-azure-china"></a><span data-ttu-id="2bb38-434">Como usar o Armazenamento do Azure para o governo dos EUA e o Azure China</span><span class="sxs-lookup"><span data-stu-id="2bb38-434">How to use Azure Storage for U.S. government and Azure China</span></span>
<span data-ttu-id="2bb38-435">Um ambiente do Azure é uma implantação independente do Microsoft Azure, como [Governo do Azure para o governo dos EUA](https://azure.microsoft.com/features/gov/), [AzureCloud para Azure global](https://portal.azure.com) e [AzureChinaCloud para o Azure operado pela 21Vianet](http://www.windowsazure.cn/) na China.</span><span class="sxs-lookup"><span data-stu-id="2bb38-435">An Azure environment is an independent deployment of Microsoft Azure, such as [Azure Government for U.S. government](https://azure.microsoft.com/features/gov/), [AzureCloud for global Azure](https://portal.azure.com), and [AzureChinaCloud for Azure operated by 21Vianet in China](http://www.windowsazure.cn/).</span></span> <span data-ttu-id="2bb38-436">Você pode implantar novos ambientes do Azure para o governo dos EUA e Azure China.</span><span class="sxs-lookup"><span data-stu-id="2bb38-436">You can deploy new Azure environments for U.S government and Azure China.</span></span>

<span data-ttu-id="2bb38-437">Para usar o Armazenamento do Azure com AzureChinaCloud, você precisa criar um contexto de armazenamento associado à AzureChinaCloud.</span><span class="sxs-lookup"><span data-stu-id="2bb38-437">To use Azure Storage with AzureChinaCloud, you need to create a storage context that is associated with AzureChinaCloud.</span></span> <span data-ttu-id="2bb38-438">Siga estas etapas para começar:</span><span class="sxs-lookup"><span data-stu-id="2bb38-438">Follow these steps to get you started:</span></span>

1. <span data-ttu-id="2bb38-439">Execute o cmdlet [Get-AzureEnvironment](/powershell/module/azure/get-azureenvironment?view=azuresmps-3.7.0) para ver os ambientes do Azure disponíveis:</span><span class="sxs-lookup"><span data-stu-id="2bb38-439">Run the [Get-AzureEnvironment](/powershell/module/azure/get-azureenvironment?view=azuresmps-3.7.0) cmdlet to see the available Azure environments:</span></span>
   
    ```powershell
    Get-AzureEnvironment
    ```

2. <span data-ttu-id="2bb38-440">Adicionar uma conta do Azure China ao Windows PowerShell:</span><span class="sxs-lookup"><span data-stu-id="2bb38-440">Add an Azure China account to Windows PowerShell:</span></span>
   
    ```powershell
    Add-AzureAccount –Environment AzureChinaCloud
    ```

3. <span data-ttu-id="2bb38-441">Crie um contexto de armazenamento para uma conta de AzureChinaCloud:</span><span class="sxs-lookup"><span data-stu-id="2bb38-441">Create a storage context for an AzureChinaCloud account:</span></span>
   
    ```powershell
    $Ctx = New-AzureStorageContext -StorageAccountName $AccountName -StorageAccountKey $AccountKey> -Environment AzureChinaCloud
    ```

<span data-ttu-id="2bb38-442">Para usar o armazenamento do Azure com [Azure Government. dos EUA](https://azure.microsoft.com/features/gov/), você deve definir um novo ambiente e, em seguida, criar um novo contexto de armazenamento com esse ambiente:</span><span class="sxs-lookup"><span data-stu-id="2bb38-442">To use Azure Storage with [U.S. Azure Government](https://azure.microsoft.com/features/gov/), you should define a new environment and then create a new storage context with this environment:</span></span>

1. <span data-ttu-id="2bb38-443">Execute o cmdlet [Get-AzureEnvironment](/powershell/module/azure/get-azureenvironment?view=azuresmps-3.7.0) para ver os ambientes do Azure disponíveis:</span><span class="sxs-lookup"><span data-stu-id="2bb38-443">Run the [Get-AzureEnvironment](/powershell/module/azure/get-azureenvironment?view=azuresmps-3.7.0) cmdlet to see the available Azure environments:</span></span>

    ```powershell
    Get-AzureEnvironment
    ```

2. <span data-ttu-id="2bb38-444">Adicionar uma conta do Azure US Government ao Windows PowerShell:</span><span class="sxs-lookup"><span data-stu-id="2bb38-444">Add an Azure US Government account to Windows PowerShell:</span></span>
   
    ```powershell
    Add-AzureAccount –Environment AzureUSGovernment
    ```

3. <span data-ttu-id="2bb38-445">Crie um contexto de armazenamento para uma conta do AzureUSGovernment:</span><span class="sxs-lookup"><span data-stu-id="2bb38-445">Create a storage context for an AzureUSGovernment account:</span></span>
   
    ```powershell
    $Ctx = New-AzureStorageContext -StorageAccountName $AccountName -StorageAccountKey $AccountKey> -Environment AzureUSGovernment
    ```
     
<span data-ttu-id="2bb38-446">Para obter mais informações, consulte:</span><span class="sxs-lookup"><span data-stu-id="2bb38-446">For more information, see:</span></span>

* <span data-ttu-id="2bb38-447">[Guia do Desenvolvedor do Microsoft Azure Government](../azure-government-developer-guide.md).</span><span class="sxs-lookup"><span data-stu-id="2bb38-447">[Microsoft Azure Government Developer Guide](../azure-government-developer-guide.md).</span></span>
* [<span data-ttu-id="2bb38-448">Visão geral das diferenças ao criar um aplicativo no serviço na China</span><span class="sxs-lookup"><span data-stu-id="2bb38-448">Overview of Differences When Creating an Application on China Service</span></span>](https://msdn.microsoft.com/library/azure/dn578439.aspx)

## <a name="next-steps"></a><span data-ttu-id="2bb38-449">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="2bb38-449">Next Steps</span></span>
<span data-ttu-id="2bb38-450">Neste guia, você aprendeu como gerenciar o armazenamento do Azure com o PowerShell do Azure.</span><span class="sxs-lookup"><span data-stu-id="2bb38-450">In this guide, you've learned how to manage Azure Storage with Azure PowerShell.</span></span> <span data-ttu-id="2bb38-451">Estes são alguns artigos e recursos relacionados para saber mais sobre eles.</span><span class="sxs-lookup"><span data-stu-id="2bb38-451">Here are some related articles and resources for learning more about them.</span></span>

* [<span data-ttu-id="2bb38-452">Documentação do Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="2bb38-452">Azure Storage Documentation</span></span>](https://azure.microsoft.com/documentation/services/storage/)
* [<span data-ttu-id="2bb38-453">Cmdlets do PowerShell do Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="2bb38-453">Azure Storage PowerShell Cmdlets</span></span>](/powershell/module/azurerm.storage/#storage)
* [<span data-ttu-id="2bb38-454">Referência do Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="2bb38-454">Windows PowerShell Reference</span></span>](https://msdn.microsoft.com/library/ms714469.aspx)

[Getting started with Azure Storage and PowerShell in 5 minutes]: #getstart
[Prerequisites for using Azure PowerShell with Azure Storage]: #pre
[How to manage storage accounts in Azure]: #manageaccount
[How to set a default Azure subscription]: #setdefsub
[How to create a new Azure storage account]: #createaccount
[How to set a default Azure storage account]: #defaultaccount
[How to list all Azure storage accounts in a subscription]: #listaccounts
[How to create an Azure storage context]: #createctx
[How to manage Azure blobs and blob snapshots]: #manageblobs
[How to create a container]: #container
[How to upload a blob into a container]: #uploadblob
[How to download blobs from a container]: #downblob
[How to copy blobs from one storage container to another]: #copyblob
[How to delete a blob]: #deleteblob
[How to manage Azure blob snapshots]: #manageshots
[How to create a blob snapshot]: #createshot
[How to list snapshots of a blob]: #listshot
[How to copy a snapshot of a blob]: #copyshot
[How to manage Azure tables and table entities]: #managetables
[How to create a table]: #createtable
[How to retrieve a table]: #gettable
[How to delete a table]: #remtable
[How to manage table entities]: #mngentity
[How to add table entities]: #addentity
[How to query table entities]: #queryentity
[How to delete table entities]: #deleteentity
[How to manage Azure queues and queue messages]: #managequeues
[How to create a queue]: #createqueue
[How to retrieve a queue]: #getqueue
[How to delete a queue]: #remqueue
[How to manage queue messages]: #mngqueuemsg
[How to insert a message into a queue]: #addqueuemsg
[How to de-queue at the next message]: #dequeuemsg
[How to manage Azure file shares and files]: #files
[How to set and query storage analytics]: #stganalytics
[How to manage Shared Access Signature (SAS) and Stored Access Policy]: #sas
[How to use Azure Storage for U.S. government and Azure China]: #gov
[Next Steps]: #next
