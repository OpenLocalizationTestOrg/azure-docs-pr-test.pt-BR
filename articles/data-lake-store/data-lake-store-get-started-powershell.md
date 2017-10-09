---
title: "aaaUse PowerShell tooget Introdução ao repositório Azure Data Lake | Microsoft Docs"
description: "Usar o Azure PowerShell toocreate uma conta do repositório Data Lake e executar operações básicas"
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: bf85f369-f9aa-4ca1-9ae7-e03a78eb7290
ms.service: data-lake-store
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/29/2017
ms.author: nitinme
ms.openlocfilehash: 9c958bfd63e412ec0b0a4113a149f61aee026bc4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-data-lake-store-using-azure-powershell"></a><span data-ttu-id="9db98-103">Introdução ao Repositório Azure Data Lake usando o Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="9db98-103">Get started with Azure Data Lake Store using Azure PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="9db98-104">Portal</span><span class="sxs-lookup"><span data-stu-id="9db98-104">Portal</span></span>](data-lake-store-get-started-portal.md)
> * [<span data-ttu-id="9db98-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="9db98-105">PowerShell</span></span>](data-lake-store-get-started-powershell.md)
> * [<span data-ttu-id="9db98-106">SDK .NET</span><span class="sxs-lookup"><span data-stu-id="9db98-106">.NET SDK</span></span>](data-lake-store-get-started-net-sdk.md)
> * [<span data-ttu-id="9db98-107">Java SDK</span><span class="sxs-lookup"><span data-stu-id="9db98-107">Java SDK</span></span>](data-lake-store-get-started-java-sdk.md)
> * [<span data-ttu-id="9db98-108">API REST</span><span class="sxs-lookup"><span data-stu-id="9db98-108">REST API</span></span>](data-lake-store-get-started-rest-api.md)
> * [<span data-ttu-id="9db98-109">CLI 2.0 do Azure</span><span class="sxs-lookup"><span data-stu-id="9db98-109">Azure CLI 2.0</span></span>](data-lake-store-get-started-cli-2.0.md)
> * [<span data-ttu-id="9db98-110">Node.js</span><span class="sxs-lookup"><span data-stu-id="9db98-110">Node.js</span></span>](data-lake-store-manage-use-nodejs.md)
> * [<span data-ttu-id="9db98-111">Python</span><span class="sxs-lookup"><span data-stu-id="9db98-111">Python</span></span>](data-lake-store-get-started-python.md)
>
>

<span data-ttu-id="9db98-112">Saiba como toouse do Azure PowerShell toocreate uma Data Lake do Azure armazenam conta e executar operações básicas, como criar pastas, carregar e baixar arquivos de dados, excluir sua conta, etc. Para saber mais sobre o Data Lake Store, veja [Visão geral do Data Lake Store](data-lake-store-overview.md).</span><span class="sxs-lookup"><span data-stu-id="9db98-112">Learn how toouse Azure PowerShell toocreate an Azure Data Lake Store account and perform basic operations such as create folders, upload and download data files, delete your account, etc. For more information about Data Lake Store, see [Overview of Data Lake Store](data-lake-store-overview.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9db98-113">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="9db98-113">Prerequisites</span></span>
<span data-ttu-id="9db98-114">Antes de começar este tutorial, você deve ter o seguinte hello:</span><span class="sxs-lookup"><span data-stu-id="9db98-114">Before you begin this tutorial, you must have hello following:</span></span>

* <span data-ttu-id="9db98-115">**Uma assinatura do Azure**.</span><span class="sxs-lookup"><span data-stu-id="9db98-115">**An Azure subscription**.</span></span> <span data-ttu-id="9db98-116">Consulte [Obter avaliação gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="9db98-116">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="9db98-117">**Azure PowerShell 1.0 ou superior**.</span><span class="sxs-lookup"><span data-stu-id="9db98-117">**Azure PowerShell 1.0 or greater**.</span></span> <span data-ttu-id="9db98-118">Consulte [como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="9db98-118">See [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

## <a name="authentication"></a><span data-ttu-id="9db98-119">Autenticação</span><span class="sxs-lookup"><span data-stu-id="9db98-119">Authentication</span></span>
<span data-ttu-id="9db98-120">Este artigo usa uma abordagem mais simples de autenticação com repositório Data Lake onde você está tooenter solicitada as credenciais de conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="9db98-120">This article uses a simpler authentication approach with Data Lake Store where you are prompted tooenter your Azure account credentials.</span></span> <span data-ttu-id="9db98-121">Olá acesso nível tooData Lake repositório conta de sistema de arquivos e, em seguida, é controlado pelo nível de acesso de saudação do hello usuário conectado no.</span><span class="sxs-lookup"><span data-stu-id="9db98-121">hello access level tooData Lake Store account and file system is then governed by hello access level of hello logged in user.</span></span> <span data-ttu-id="9db98-122">No entanto, há outras abordagens como tooauthenticate bem com repositório Data Lake, que são **autenticação do usuário final** ou **autenticação de serviço a serviço**.</span><span class="sxs-lookup"><span data-stu-id="9db98-122">However, there are other approaches as well tooauthenticate with Data Lake Store, which are **end-user authentication** or **service-to-service authentication**.</span></span> <span data-ttu-id="9db98-123">Para obter instruções e mais informações sobre como tooauthenticate, consulte [autenticação do usuário final](data-lake-store-end-user-authenticate-using-active-directory.md) ou [autenticação de serviço a serviço](data-lake-store-authenticate-using-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="9db98-123">For instructions and more information on how tooauthenticate, see [End-user authentication](data-lake-store-end-user-authenticate-using-active-directory.md) or [Service-to-service authentication](data-lake-store-authenticate-using-active-directory.md).</span></span>

## <a name="create-an-azure-data-lake-store-account"></a><span data-ttu-id="9db98-124">Criar uma conta do Repositório Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="9db98-124">Create an Azure Data Lake Store account</span></span>
1. <span data-ttu-id="9db98-125">Da área de trabalho, abrir uma nova janela do Windows PowerShell, digite Olá seguinte trecho toolog em tooyour conta do Azure, definir Olá assinatura e registrar provedor de repositório Data Lake hello.</span><span class="sxs-lookup"><span data-stu-id="9db98-125">From your desktop, open a new Windows PowerShell window, and enter hello following snippet toolog in tooyour Azure account, set hello subscription, and register hello Data Lake Store provider.</span></span> <span data-ttu-id="9db98-126">Quando solicitada toolog, certifique-se de você fazer logon como uma saudação admininistrators/proprietário da assinatura:</span><span class="sxs-lookup"><span data-stu-id="9db98-126">When prompted toolog in, make sure you log in as one of hello subscription admininistrators/owner:</span></span>

        # Log in tooyour Azure account
        Login-AzureRmAccount

        # List all hello subscriptions associated tooyour account
        Get-AzureRmSubscription

        # Select a subscription
        Set-AzureRmContext -SubscriptionId <subscription ID>

        # Register for Azure Data Lake Store
        Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.DataLakeStore"
2. <span data-ttu-id="9db98-127">Uma conta do Repositório Azure Data Lake está associada a um Grupo de Recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="9db98-127">An Azure Data Lake Store account is associated with an Azure Resource Group.</span></span> <span data-ttu-id="9db98-128">Comece criando um Grupo de Recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="9db98-128">Start by creating an Azure Resource Group.</span></span>

        $resourceGroupName = "<your new resource group name>"
        New-AzureRmResourceGroup -Name $resourceGroupName -Location "East US 2"

    <span data-ttu-id="9db98-129">![Criar um Grupo de Recursos do Azure](./media/data-lake-store-get-started-powershell/ADL.PS.CreateResourceGroup.png "Criar um Grupo de Recursos do Azure")</span><span class="sxs-lookup"><span data-stu-id="9db98-129">![Create an Azure Resource Group](./media/data-lake-store-get-started-powershell/ADL.PS.CreateResourceGroup.png "Create an Azure Resource Group")</span></span>
3. <span data-ttu-id="9db98-130">Crie uma conta do Repositório Azure Data Lake.</span><span class="sxs-lookup"><span data-stu-id="9db98-130">Create an Azure Data Lake Store account.</span></span> <span data-ttu-id="9db98-131">nome de saudação especificado deve conter apenas letras minúsculas e números.</span><span class="sxs-lookup"><span data-stu-id="9db98-131">hello name you specify must only contain lowercase letters and numbers.</span></span>

        $dataLakeStoreName = "<your new Data Lake Store name>"
        New-AzureRmDataLakeStoreAccount -ResourceGroupName $resourceGroupName -Name $dataLakeStoreName -Location "East US 2"

    <span data-ttu-id="9db98-132">![Criar uma conta do Azure Data Lake Store](./media/data-lake-store-get-started-powershell/ADL.PS.CreateADLAcc.png "Criar uma conta do Azure Data Lake Store")</span><span class="sxs-lookup"><span data-stu-id="9db98-132">![Create an Azure Data Lake Store account](./media/data-lake-store-get-started-powershell/ADL.PS.CreateADLAcc.png "Create an Azure Data Lake Store account")</span></span>
4. <span data-ttu-id="9db98-133">Verifique se a conta de saudação é criada com êxito.</span><span class="sxs-lookup"><span data-stu-id="9db98-133">Verify that hello account is successfully created.</span></span>

        Test-AzureRmDataLakeStoreAccount -Name $dataLakeStoreName

    <span data-ttu-id="9db98-134">saudação de saída para isso deve ser **True**.</span><span class="sxs-lookup"><span data-stu-id="9db98-134">hello output for this should be **True**.</span></span>

## <a name="create-directory-structures-in-your-azure-data-lake-store"></a><span data-ttu-id="9db98-135">Criar estruturas de diretório no Repositório Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="9db98-135">Create directory structures in your Azure Data Lake Store</span></span>
<span data-ttu-id="9db98-136">Você pode criar diretórios sob o toomanage de conta do repositório Azure Data Lake e armazenar dados.</span><span class="sxs-lookup"><span data-stu-id="9db98-136">You can create directories under your Azure Data Lake Store account toomanage and store data.</span></span>

1. <span data-ttu-id="9db98-137">Especifique um diretório raiz.</span><span class="sxs-lookup"><span data-stu-id="9db98-137">Specify a root directory.</span></span>

        $myrootdir = "/"
2. <span data-ttu-id="9db98-138">Criar um novo diretório chamado **mynewdirectory** na raiz de saudação especificado.</span><span class="sxs-lookup"><span data-stu-id="9db98-138">Create a new directory called **mynewdirectory** under hello specified root.</span></span>

        New-AzureRmDataLakeStoreItem -Folder -AccountName $dataLakeStoreName -Path $myrootdir/mynewdirectory
3. <span data-ttu-id="9db98-139">Verifique se o que diretório Olá novo é criado com êxito.</span><span class="sxs-lookup"><span data-stu-id="9db98-139">Verify that hello new directory is successfully created.</span></span>

        Get-AzureRmDataLakeStoreChildItem -AccountName $dataLakeStoreName -Path $myrootdir

    <span data-ttu-id="9db98-140">Ele deverá mostrar uma saída semelhante Olá seguinte:</span><span class="sxs-lookup"><span data-stu-id="9db98-140">It should show an output like hello following:</span></span>

    <span data-ttu-id="9db98-141">![Verificar o Diretório](./media/data-lake-store-get-started-powershell/ADL.PS.Verify.Dir.Creation.png "Verificar o Diretório")</span><span class="sxs-lookup"><span data-stu-id="9db98-141">![Verify Directory](./media/data-lake-store-get-started-powershell/ADL.PS.Verify.Dir.Creation.png "Verify Directory")</span></span>

## <a name="upload-data-tooyour-azure-data-lake-store"></a><span data-ttu-id="9db98-142">Carregar o repositório de dados tooyour Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="9db98-142">Upload data tooyour Azure Data Lake Store</span></span>
<span data-ttu-id="9db98-143">Você pode carregar seu repositório data tooData Lake diretamente no hello nível ou tooa diretório raiz que você criou na conta de saudação.</span><span class="sxs-lookup"><span data-stu-id="9db98-143">You can upload your data tooData Lake Store directly at hello root level or tooa directory that you created within hello account.</span></span> <span data-ttu-id="9db98-144">trechos de saudação a seguir demonstram como tooupload alguns diretório de toohello de dados de exemplo (**mynewdirectory**) criado na seção anterior hello.</span><span class="sxs-lookup"><span data-stu-id="9db98-144">hello snippets below demonstrate how tooupload some sample data toohello directory (**mynewdirectory**) you created in hello previous section.</span></span>

<span data-ttu-id="9db98-145">Se você estiver procurando por alguns tooupload de dados de exemplo, você pode obter Olá **ambulância dados** pasta Olá [repositório Git do Azure Data Lake](https://github.com/MicrosoftBigData/usql/tree/master/Examples/Samples/Data/AmbulanceData).</span><span class="sxs-lookup"><span data-stu-id="9db98-145">If you are looking for some sample data tooupload, you can get hello **Ambulance Data** folder from hello [Azure Data Lake Git Repository](https://github.com/MicrosoftBigData/usql/tree/master/Examples/Samples/Data/AmbulanceData).</span></span> <span data-ttu-id="9db98-146">Baixe o arquivo hello e armazená-lo em um diretório local no seu computador, como C:\sampledata\.</span><span class="sxs-lookup"><span data-stu-id="9db98-146">Download hello file and store it in a local directory on your computer, such as  C:\sampledata\.</span></span>

    Import-AzureRmDataLakeStoreItem -AccountName $dataLakeStoreName -Path "C:\sampledata\vehicle1_09142014.csv" -Destination $myrootdir\mynewdirectory\vehicle1_09142014.csv


## <a name="rename-download-and-delete-data-from-your-data-lake-store"></a><span data-ttu-id="9db98-147">Renomear, baixar e excluir dados do Repositório Data Lake</span><span class="sxs-lookup"><span data-stu-id="9db98-147">Rename, download, and delete data from your Data Lake Store</span></span>
<span data-ttu-id="9db98-148">toorename um arquivo, use Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="9db98-148">toorename a file, use hello following command:</span></span>

    Move-AzureRmDataLakeStoreItem -AccountName $dataLakeStoreName -Path $myrootdir\mynewdirectory\vehicle1_09142014.csv -Destination $myrootdir\mynewdirectory\vehicle1_09142014_Copy.csv

<span data-ttu-id="9db98-149">toodownload um arquivo, use Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="9db98-149">toodownload a file, use hello following command:</span></span>

    Export-AzureRmDataLakeStoreItem -AccountName $dataLakeStoreName -Path $myrootdir\mynewdirectory\vehicle1_09142014_Copy.csv -Destination "C:\sampledata\vehicle1_09142014_Copy.csv"

<span data-ttu-id="9db98-150">toodelete um arquivo, use Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="9db98-150">toodelete a file, use hello following command:</span></span>

    Remove-AzureRmDataLakeStoreItem -AccountName $dataLakeStoreName -Paths $myrootdir\mynewdirectory\vehicle1_09142014_Copy.csv

<span data-ttu-id="9db98-151">Quando solicitado, insira **Y** toodelete item de saudação.</span><span class="sxs-lookup"><span data-stu-id="9db98-151">When prompted, enter **Y** toodelete hello item.</span></span> <span data-ttu-id="9db98-152">Se você tiver mais de um toodelete de arquivo, você pode fornecer todos os caminhos de saudação separados por vírgula.</span><span class="sxs-lookup"><span data-stu-id="9db98-152">If you have more than one file toodelete, you can provide all hello paths separated by comma.</span></span>

    Remove-AzureRmDataLakeStoreItem -AccountName $dataLakeStoreName -Paths $myrootdir\mynewdirectory\vehicle1_09142014.csv, $myrootdir\mynewdirectoryvehicle1_09142014_Copy.csv

## <a name="delete-your-azure-data-lake-store-account"></a><span data-ttu-id="9db98-153">Excluir sua conta do Repositório Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="9db98-153">Delete your Azure Data Lake Store account</span></span>
<span data-ttu-id="9db98-154">Use sua conta de repositório Data Lake de saudação toodelete de comando a seguir.</span><span class="sxs-lookup"><span data-stu-id="9db98-154">Use hello following command toodelete your Data Lake Store account.</span></span>

    Remove-AzureRmDataLakeStoreAccount -Name $dataLakeStoreName

<span data-ttu-id="9db98-155">Quando solicitado, insira **Y** toodelete conta de saudação.</span><span class="sxs-lookup"><span data-stu-id="9db98-155">When prompted, enter **Y** toodelete hello account.</span></span>

## <a name="performance-guidance-while-using-powershell"></a><span data-ttu-id="9db98-156">Diretrizes de desempenho durante o uso do PowerShell</span><span class="sxs-lookup"><span data-stu-id="9db98-156">Performance guidance while using PowerShell</span></span>

<span data-ttu-id="9db98-157">Abaixo está as configurações mais importantes que podem ser ajustadas tooget Olá melhor desempenho ao usar o PowerShell toowork com repositório Data Lake hello:</span><span class="sxs-lookup"><span data-stu-id="9db98-157">Below are hello most important settings that can be tuned tooget hello best performance while using PowerShell toowork with Data Lake Store:</span></span>

| <span data-ttu-id="9db98-158">Propriedade</span><span class="sxs-lookup"><span data-stu-id="9db98-158">Property</span></span>            | <span data-ttu-id="9db98-159">Padrão</span><span class="sxs-lookup"><span data-stu-id="9db98-159">Default</span></span> | <span data-ttu-id="9db98-160">Descrição</span><span class="sxs-lookup"><span data-stu-id="9db98-160">Description</span></span> |
|---------------------|---------|-------------|
| <span data-ttu-id="9db98-161">PerFileThreadCount</span><span class="sxs-lookup"><span data-stu-id="9db98-161">PerFileThreadCount</span></span>  | <span data-ttu-id="9db98-162">10</span><span class="sxs-lookup"><span data-stu-id="9db98-162">10</span></span>      | <span data-ttu-id="9db98-163">Esse parâmetro permite que você toochoose número de saudação de threads paralelos para carregamento ou download de cada arquivo.</span><span class="sxs-lookup"><span data-stu-id="9db98-163">This parameter enables you toochoose hello number of parallel threads for uploading or downloading each file.</span></span> <span data-ttu-id="9db98-164">Esse número representa Olá máximo de threads que pode ser alocado por arquivo, mas você pode receber menos threads dependendo do cenário (por exemplo, se você estiver carregando um arquivo de 1 KB, você obterá um thread mesmo se você pedir 20 segmentos).</span><span class="sxs-lookup"><span data-stu-id="9db98-164">This number represents hello max threads that can be allocated per file, but you may get less threads depending on your scenario (e.g. if you are uploading a 1KB file, you will get one thread even if you ask for 20 threads).</span></span>  |
| <span data-ttu-id="9db98-165">ConcurrentFileCount</span><span class="sxs-lookup"><span data-stu-id="9db98-165">ConcurrentFileCount</span></span> | <span data-ttu-id="9db98-166">10</span><span class="sxs-lookup"><span data-stu-id="9db98-166">10</span></span>      | <span data-ttu-id="9db98-167">Esse parâmetro é especificamente para carregar ou baixar pastas.</span><span class="sxs-lookup"><span data-stu-id="9db98-167">This parameter is specifically for uploading or downloading folders.</span></span> <span data-ttu-id="9db98-168">Esse parâmetro determina o número de saudação de arquivos simultâneos que podem ser carregadas ou baixadas.</span><span class="sxs-lookup"><span data-stu-id="9db98-168">This parameter determines hello number of concurrent files that can be uploaded or downloaded.</span></span> <span data-ttu-id="9db98-169">Esse número representa o número máximo de saudação de arquivos simultâneos que podem ser carregadas ou baixadas ao mesmo tempo, mas você pode receber menos simultaneidade dependendo do cenário (por exemplo, se você estiver carregando dois arquivos, você obterá duas carregamentos de arquivo simultâneas mesmo se você pedir 15).</span><span class="sxs-lookup"><span data-stu-id="9db98-169">This number represents hello maximum number of concurrent files that can be uploaded or downloaded at one time, but you may get less concurrency depending on your scenario (e.g. if you are uploading two files, you will get two concurrent file uploads even if you ask for 15).</span></span> |

<span data-ttu-id="9db98-170">**Exemplo**</span><span class="sxs-lookup"><span data-stu-id="9db98-170">**Example**</span></span>

<span data-ttu-id="9db98-171">Esse comando baixa os arquivos da unidade de local do usuário do repositório Azure Data Lake toohello usando 20 threads por arquivo e 100 arquivos simultâneos.</span><span class="sxs-lookup"><span data-stu-id="9db98-171">This command downloads files from Azure Data Lake Store toohello user's local drive using 20 threads per file and 100 concurrent files.</span></span>

    Export-AzureRmDataLakeStoreItem -AccountName <Data Lake Store account name> -PerFileThreadCount 20-ConcurrentFileCount 100 -Path /Powershell/100GB/ -Destination C:\Performance\ -Force -Recurse

### <a name="how-do-i-determine-hello-value-tooset-for-these-parameters"></a><span data-ttu-id="9db98-172">Como determinar o hello tooset de valor para esses parâmetros?</span><span class="sxs-lookup"><span data-stu-id="9db98-172">How do I determine hello value tooset for these parameters?</span></span>

<span data-ttu-id="9db98-173">Aqui estão algumas diretrizes que podem ser usadas.</span><span class="sxs-lookup"><span data-stu-id="9db98-173">Here's some guidance that you can use.</span></span>

* <span data-ttu-id="9db98-174">**Etapa 1: Determinar a contagem total de threads de saudação** -deve começar com calcular toouse de contagem total de threads de saudação.</span><span class="sxs-lookup"><span data-stu-id="9db98-174">**Step 1: Determine hello total thread count** - You should start by calculating hello total thread count toouse.</span></span> <span data-ttu-id="9db98-175">Como diretriz geral, você deve usar 6 threads para cada núcleo físico.</span><span class="sxs-lookup"><span data-stu-id="9db98-175">As a general guideline, you should use 6 threads for each physical core.</span></span>

        Total thread count = total physical cores * 6

    <span data-ttu-id="9db98-176">**Exemplo**</span><span class="sxs-lookup"><span data-stu-id="9db98-176">**Example**</span></span>

    <span data-ttu-id="9db98-177">Supondo que você estiver executando Olá PowerShell comandos de uma VM D14 que tem 16 núcleos</span><span class="sxs-lookup"><span data-stu-id="9db98-177">Assuming you are running hello PowerShell commands from a D14 VM that has 16 cores</span></span>

        Total thread count = 16 cores * 6 = 96 threads


* <span data-ttu-id="9db98-178">**Etapa 2: Calcular PerFileThreadCount** -calculamos nosso PerFileThreadCount com base no tamanho de saudação de arquivos de saudação.</span><span class="sxs-lookup"><span data-stu-id="9db98-178">**Step 2: Calculate PerFileThreadCount**  - We calculate our PerFileThreadCount based on hello size of hello files.</span></span> <span data-ttu-id="9db98-179">Para arquivos menores do que 2,5 GB, há toochange sem necessidade esse parâmetro porque saudação padrão de 10 é suficiente.</span><span class="sxs-lookup"><span data-stu-id="9db98-179">For files smaller than 2.5GB, there is no need toochange this parameter because hello default of 10 is sufficient.</span></span> <span data-ttu-id="9db98-180">Para arquivos maiores do que 2,5 GB, você deve usar 10 threads como base Olá Olá primeiro 2,5 GB e adicionar 1 thread de cada aumento de 256 MB adicionais no tamanho do arquivo.</span><span class="sxs-lookup"><span data-stu-id="9db98-180">For files larger than 2.5GB, you should use 10 threads as hello base for hello first 2.5GB and add 1 thread for each additional 256MB increase in file size.</span></span> <span data-ttu-id="9db98-181">Se você estiver copiando uma pasta com uma grande variedade de tamanhos de arquivo, considere agrupá-los em tamanhos de arquivo semelhantes.</span><span class="sxs-lookup"><span data-stu-id="9db98-181">If you are copying a folder with a large range of file sizes, consider grouping them into similar file sizes.</span></span> <span data-ttu-id="9db98-182">Ter tamanhos de arquivo diferentes pode fazer com que o desempenho não seja o ideal.</span><span class="sxs-lookup"><span data-stu-id="9db98-182">Having dissimilar file sizes may cause non-optimal performance.</span></span> <span data-ttu-id="9db98-183">Se isso não for possível toogroup semelhante tamanhos de arquivos, você deve definir PerFileThreadCount com base no maior tamanho de arquivo hello.</span><span class="sxs-lookup"><span data-stu-id="9db98-183">If that's not possible toogroup similar file sizes, you should set PerFileThreadCount based on hello largest file size.</span></span>

        PerFileThreadCount = 10 threads for hello first 2.5GB + 1 thread for each additional 256MB increase in file size

    <span data-ttu-id="9db98-184">**Exemplo**</span><span class="sxs-lookup"><span data-stu-id="9db98-184">**Example**</span></span>

    <span data-ttu-id="9db98-185">Supondo que você tiver 100 arquivos que variam de 1GB too10GB, usamos Olá 10GB como Olá maior tamanho da equação, que lê como Olá seguinte do arquivo.</span><span class="sxs-lookup"><span data-stu-id="9db98-185">Assuming you have 100 files ranging from 1GB too10GB, we use hello 10GB as hello largest file size for equation, which would read like hello following.</span></span>

        PerFileThreadCount = 10 + ((10GB - 2.5GB) / 256MB) = 40 threads

* <span data-ttu-id="9db98-186">**Etapa 3: Calcular ConcurrentFilecount** -contagem de uso total de threads de saudação e PerFileThreadCount toocalculate ConcurrentFileCount com base em Olá equação a seguir.</span><span class="sxs-lookup"><span data-stu-id="9db98-186">**Step 3: Calculate ConcurrentFilecount** - Use hello total thread count and PerFileThreadCount toocalculate ConcurrentFileCount based on hello following equation.</span></span>

        Total thread count = PerFileThreadCount * ConcurrentFileCount

    <span data-ttu-id="9db98-187">**Exemplo**</span><span class="sxs-lookup"><span data-stu-id="9db98-187">**Example**</span></span>

    <span data-ttu-id="9db98-188">Com base nos valores de exemplo hello que utilizamos</span><span class="sxs-lookup"><span data-stu-id="9db98-188">Based on hello example values we have been using</span></span>

        96 = 40 * ConcurrentFileCount

    <span data-ttu-id="9db98-189">Portanto, **ConcurrentFileCount** é **2.4**, que podemos pode arredondar muito**2**.</span><span class="sxs-lookup"><span data-stu-id="9db98-189">So, **ConcurrentFileCount** is **2.4**, which we can round off too**2**.</span></span>

### <a name="further-tuning"></a><span data-ttu-id="9db98-190">Ajuste adicional</span><span class="sxs-lookup"><span data-stu-id="9db98-190">Further tuning</span></span>

<span data-ttu-id="9db98-191">Você pode precisar de mais ajuste porque há uma variedade de toowork de tamanhos de arquivo com.</span><span class="sxs-lookup"><span data-stu-id="9db98-191">You might require further tuning because there is a range of file sizes toowork with.</span></span> <span data-ttu-id="9db98-192">Olá acima cálculo funcionará bem se todos ou a maioria dos arquivos de saudação é toohello maiores e mais próximo intervalo de 10GB.</span><span class="sxs-lookup"><span data-stu-id="9db98-192">hello above calculation works well if all or most of hello files are larger and closer toohello 10GB range.</span></span> <span data-ttu-id="9db98-193">Se em vez disso houver vários tamanhos de arquivos diferentes com muitos arquivos sendo menores, você poderá reduzir PerFileThreadCount.</span><span class="sxs-lookup"><span data-stu-id="9db98-193">If instead, there are many different files sizes with many files being smaller, then you could reduce PerFileThreadCount.</span></span> <span data-ttu-id="9db98-194">Reduzindo Olá PerFileThreadCount, podemos aumentar ConcurrentFileCount.</span><span class="sxs-lookup"><span data-stu-id="9db98-194">By reducing hello PerFileThreadCount, we can increase ConcurrentFileCount.</span></span> <span data-ttu-id="9db98-195">Portanto, se vamos supor que a maioria dos arquivos menor no intervalo de 5GB hello, podemos novamente fazer nosso cálculo:</span><span class="sxs-lookup"><span data-stu-id="9db98-195">So, if we assume that most of our files are smaller in hello 5GB range, we can re-do our calculation:</span></span>

    PerFileThreadCount = 10 + ((5GB - 2.5GB) / 256MB) = 20

<span data-ttu-id="9db98-196">Portanto, **ConcurrentFileCount** será agora 96/20, que é 4.8, arredondado muito**4**.</span><span class="sxs-lookup"><span data-stu-id="9db98-196">So, **ConcurrentFileCount** will now be 96/20, which is 4.8, rounded off too**4**.</span></span>

<span data-ttu-id="9db98-197">Você pode continuar tootune essas configurações alterando Olá **PerFileThreadCount** para cima e para baixo dependendo da distribuição Olá seus tamanhos de arquivos de.</span><span class="sxs-lookup"><span data-stu-id="9db98-197">You can continue tootune these settings by changing hello **PerFileThreadCount** up and down depending on hello distribution of your file sizes.</span></span>

### <a name="limitation"></a><span data-ttu-id="9db98-198">Limitações</span><span class="sxs-lookup"><span data-stu-id="9db98-198">Limitation</span></span>

* <span data-ttu-id="9db98-199">**Número de arquivos é menor do que ConcurrentFileCount**: se o número de saudação de arquivos que você está carregando seja menor que Olá **ConcurrentFileCount** calculado e, depois, você deve reduzir  **ConcurrentFileCount** toobe toohello igual número de arquivos.</span><span class="sxs-lookup"><span data-stu-id="9db98-199">**Number of files is less than ConcurrentFileCount**: If hello number of files you are uploading is smaller than hello **ConcurrentFileCount** that you calculated, then you should reduce **ConcurrentFileCount** toobe equal toohello number of files.</span></span> <span data-ttu-id="9db98-200">Você pode usar qualquer tooincrease segmentos restantes **PerFileThreadCount**.</span><span class="sxs-lookup"><span data-stu-id="9db98-200">You can use any remaining threads tooincrease **PerFileThreadCount**.</span></span>

* <span data-ttu-id="9db98-201">**Muitos threads**: se você aumentar o thread contagem muito sem aumentar o tamanho do cluster, você corre o risco de saudação de degradação do desempenho.</span><span class="sxs-lookup"><span data-stu-id="9db98-201">**Too many threads**: If you increase thread count too much without increasing your cluster size, you run hello risk of degraded performance.</span></span> <span data-ttu-id="9db98-202">Pode haver problemas de contenção quando a alternância de contexto em Olá da CPU.</span><span class="sxs-lookup"><span data-stu-id="9db98-202">There can be contention issues when context-switching on hello CPU.</span></span>

* <span data-ttu-id="9db98-203">**Simultaneidade insuficiente**: se simultaneidade Olá não é suficiente, o cluster pode ser muito pequeno.</span><span class="sxs-lookup"><span data-stu-id="9db98-203">**Insufficient concurrency**: If hello concurrency is not sufficient, then your cluster may be too small.</span></span> <span data-ttu-id="9db98-204">Você pode aumentar o número de saudação de nós no cluster que lhe dará mais simultaneidade.</span><span class="sxs-lookup"><span data-stu-id="9db98-204">You can increase hello number of nodes in your cluster which will give you more concurrency.</span></span>

* <span data-ttu-id="9db98-205">**Erros de limitação**: você pode ver erros de limitação se a simultaneidade for muito alta.</span><span class="sxs-lookup"><span data-stu-id="9db98-205">**Throttling errors**: You may see throttling errors if your concurrency is too high.</span></span> <span data-ttu-id="9db98-206">Se você estiver vendo erros de limitação, reduzir a simultaneidade de saudação ou entre em contato conosco.</span><span class="sxs-lookup"><span data-stu-id="9db98-206">If you are seeing throttling errors, you should either reduce hello concurrency or contact us.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9db98-207">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="9db98-207">Next steps</span></span>
* [<span data-ttu-id="9db98-208">Proteger dados no Repositório Data Lake</span><span class="sxs-lookup"><span data-stu-id="9db98-208">Secure data in Data Lake Store</span></span>](data-lake-store-secure-data.md)
* [<span data-ttu-id="9db98-209">Usar a Análise Data Lake do Azure com o Repositório Data Lake</span><span class="sxs-lookup"><span data-stu-id="9db98-209">Use Azure Data Lake Analytics with Data Lake Store</span></span>](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="9db98-210">Usar o Azure HDInsight com o Repositório Data Lake</span><span class="sxs-lookup"><span data-stu-id="9db98-210">Use Azure HDInsight with Data Lake Store</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)

