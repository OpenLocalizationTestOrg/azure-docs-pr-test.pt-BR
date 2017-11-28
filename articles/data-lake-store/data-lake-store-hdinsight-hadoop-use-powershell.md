---
<span data-ttu-id="fd116-101">título: aaa "PowerShell: cluster de HDInsight do Azure com o repositório Data Lake como armazenamento de complemento | Serviços Microsoft Docs":-repositório data lake-hdinsight documentationcenter: ' autor: manager nitinme: jhubbard editor: cgronlun</span><span class="sxs-lookup"><span data-stu-id="fd116-101">title: aaa"PowerShell: Azure HDInsight cluster with Data Lake Store as add-on storage | Microsoft Docs" services: data-lake-store,hdinsight documentationcenter: '' author: nitinme manager: jhubbard editor: cgronlun</span></span>

<span data-ttu-id="fd116-102">MS. AssetID: 164ada5a-222e-4be2-bd32-e51dbe993bc0 MS. Service: MS. devlang do repositório do data lake: na MS. Topic: artigo tgt_pltfrm: na Workload: grandes dados MS. Date: 08/06/2017 Author: nitinme</span><span class="sxs-lookup"><span data-stu-id="fd116-102">ms.assetid: 164ada5a-222e-4be2-bd32-e51dbe993bc0 ms.service: data-lake-store ms.devlang: na ms.topic: article ms.tgt_pltfrm: na ms.workload: big-data ms.date: 06/08/2017 ms.author: nitinme</span></span>

---
# <a name="use-azure-powershell-toocreate-an-hdinsight-cluster-with-data-lake-store-as-additional-storage"></a><span data-ttu-id="fd116-103">Use o Azure PowerShell toocreate um cluster HDInsight com repositório Data Lake (como armazenamento adicional)</span><span class="sxs-lookup"><span data-stu-id="fd116-103">Use Azure PowerShell toocreate an HDInsight cluster with Data Lake Store (as additional storage)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="fd116-104">Usando o Portal</span><span class="sxs-lookup"><span data-stu-id="fd116-104">Using Portal</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)
> * [<span data-ttu-id="fd116-105">Usando o PowerShell (para o armazenamento padrão)</span><span class="sxs-lookup"><span data-stu-id="fd116-105">Using PowerShell (for default storage)</span></span>](data-lake-store-hdinsight-hadoop-use-powershell-for-default-storage.md)
> * [<span data-ttu-id="fd116-106">Usando o PowerShell (para o armazenamento adicional)</span><span class="sxs-lookup"><span data-stu-id="fd116-106">Using PowerShell (for additional storage)</span></span>](data-lake-store-hdinsight-hadoop-use-powershell.md)
> * [<span data-ttu-id="fd116-107">Usando o Gerenciador de Recursos</span><span class="sxs-lookup"><span data-stu-id="fd116-107">Using Resource Manager</span></span>](data-lake-store-hdinsight-hadoop-use-resource-manager-template.md)
>
>

<span data-ttu-id="fd116-108">Saiba como toouse do Azure PowerShell tooconfigure um HDInsight cluster com repositório Azure Data Lake, **como armazenamento adicional**.</span><span class="sxs-lookup"><span data-stu-id="fd116-108">Learn how toouse Azure PowerShell tooconfigure an HDInsight cluster with Azure Data Lake Store, **as additional storage**.</span></span> <span data-ttu-id="fd116-109">Para obter instruções sobre como toocreate uma HDInsight cluster com repositório Azure Data Lake como armazenamento padrão, consulte [criar um cluster HDInsight com repositório Data Lake como armazenamento padrão](data-lake-store-hdinsight-hadoop-use-powershell-for-default-storage.md).</span><span class="sxs-lookup"><span data-stu-id="fd116-109">For instructions on how toocreate an HDInsight cluster with Azure Data Lake Store as default storage, see [Create an HDInsight cluster with Data Lake Store as default storage](data-lake-store-hdinsight-hadoop-use-powershell-for-default-storage.md).</span></span>

> [!NOTE]
> <span data-ttu-id="fd116-110">Se você for repositório toouse Azure Data Lake como armazenamento adicional para o cluster HDInsight, é altamente recomendável que você faça isso durante a criação de cluster Olá conforme descrito neste artigo.</span><span class="sxs-lookup"><span data-stu-id="fd116-110">If you are going toouse Azure Data Lake Store as additional storage for HDInsight cluster, we strongly recommend that you do this while you create hello cluster as described in this article.</span></span> <span data-ttu-id="fd116-111">Adicionar repositório Azure Data Lake como armazenamento adicional tooan cluster HDInsight existente é um processo complicado e sujeito a tooerrors.</span><span class="sxs-lookup"><span data-stu-id="fd116-111">Adding Azure Data Lake Store as additional storage tooan existing HDInsight cluster is a complicated process and prone tooerrors.</span></span>
>

<span data-ttu-id="fd116-112">Para tipos de cluster com suporte, o Data Lake Store pode ser usado como um armazenamento padrão ou uma conta de armazenamento adicional.</span><span class="sxs-lookup"><span data-stu-id="fd116-112">For supported cluster types, Data Lake Store can be used as a default storage or additional storage account.</span></span> <span data-ttu-id="fd116-113">Quando o repositório Data Lake é usado como armazenamento adicional, conta de armazenamento padrão Olá para clusters de saudação ainda estará Blobs de armazenamento do Azure (WASB) e arquivos relacionados ao cluster de saudação (como logs, etc.) são gravados ainda armazenamento padrão de toohello, enquanto os dados de saudação que você deseja tooprocess podem ser armazenados em uma conta do repositório Data Lake.</span><span class="sxs-lookup"><span data-stu-id="fd116-113">When Data Lake Store is used as additional storage, hello default storage account for hello clusters will still be Azure Storage Blobs (WASB) and hello cluster-related files (such as logs, etc.) are still written toohello default storage, while hello data that you want tooprocess can be stored in a Data Lake Store account.</span></span> <span data-ttu-id="fd116-114">Usando o repositório Data Lake como uma conta de armazenamento adicional não afeta o desempenho e o hello capacidade tooread/gravação toohello armazenamento de cluster hello.</span><span class="sxs-lookup"><span data-stu-id="fd116-114">Using Data Lake Store as an additional storage account does not impact performance or hello ability tooread/write toohello storage from hello cluster.</span></span>

## <a name="using-data-lake-store-for-hdinsight-cluster-storage"></a><span data-ttu-id="fd116-115">Usando o Data Lake Store para armazenamento do cluster HDInsight</span><span class="sxs-lookup"><span data-stu-id="fd116-115">Using Data Lake Store for HDInsight cluster storage</span></span>

<span data-ttu-id="fd116-116">Aqui estão algumas considerações importantes para usar o HDInsight com o Data Lake Store:</span><span class="sxs-lookup"><span data-stu-id="fd116-116">Here are some important considerations for using HDInsight with Data Lake Store:</span></span>

* <span data-ttu-id="fd116-117">Clusters de HDInsight toocreate opção com acesso tooData Lake repositório como armazenamento adicional está disponível para HDInsight versões 3.2, 3.4, 3.5 e 3.6.</span><span class="sxs-lookup"><span data-stu-id="fd116-117">Option toocreate HDInsight clusters with access tooData Lake Store as additional storage is available for HDInsight versions 3.2, 3.4, 3.5, and 3.6.</span></span>

<span data-ttu-id="fd116-118">Configuração do HDInsight toowork com repositório Data Lake usando o PowerShell envolve Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="fd116-118">Configuring HDInsight toowork with Data Lake Store using PowerShell involves hello following steps:</span></span>

* <span data-ttu-id="fd116-119">Criar um Repositório Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="fd116-119">Create an Azure Data Lake Store</span></span>
* <span data-ttu-id="fd116-120">Configurar a autenticação para baseado em função acessar o repositório de Lake tooData</span><span class="sxs-lookup"><span data-stu-id="fd116-120">Set up authentication for role-based access tooData Lake Store</span></span>
* <span data-ttu-id="fd116-121">Criar o cluster HDInsight com autenticação tooData Lake repositório</span><span class="sxs-lookup"><span data-stu-id="fd116-121">Create HDInsight cluster with authentication tooData Lake Store</span></span>
* <span data-ttu-id="fd116-122">Executar um trabalho de teste no cluster Olá</span><span class="sxs-lookup"><span data-stu-id="fd116-122">Run a test job on hello cluster</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fd116-123">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="fd116-123">Prerequisites</span></span>
<span data-ttu-id="fd116-124">Antes de começar este tutorial, você deve ter o seguinte hello:</span><span class="sxs-lookup"><span data-stu-id="fd116-124">Before you begin this tutorial, you must have hello following:</span></span>

* <span data-ttu-id="fd116-125">**Uma assinatura do Azure**.</span><span class="sxs-lookup"><span data-stu-id="fd116-125">**An Azure subscription**.</span></span> <span data-ttu-id="fd116-126">Consulte [Obter avaliação gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="fd116-126">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="fd116-127">**Azure PowerShell 1.0 ou superior**.</span><span class="sxs-lookup"><span data-stu-id="fd116-127">**Azure PowerShell 1.0 or greater**.</span></span> <span data-ttu-id="fd116-128">Consulte [como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="fd116-128">See [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="fd116-129">**SDK do Windows**.</span><span class="sxs-lookup"><span data-stu-id="fd116-129">**Windows SDK**.</span></span> <span data-ttu-id="fd116-130">Você pode instalá-lo clicando [aqui](https://dev.windows.com/en-us/downloads).</span><span class="sxs-lookup"><span data-stu-id="fd116-130">You can install it from [here](https://dev.windows.com/en-us/downloads).</span></span> <span data-ttu-id="fd116-131">Você usa essa toocreate um certificado de segurança.</span><span class="sxs-lookup"><span data-stu-id="fd116-131">You use this toocreate a security certificate.</span></span>
* <span data-ttu-id="fd116-132">**Entidade de serviço do Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="fd116-132">**Azure Active Directory Service Principal**.</span></span> <span data-ttu-id="fd116-133">As etapas deste tutorial fornecem instruções sobre como toocreate uma entidade de serviço no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="fd116-133">Steps in this tutorial provide instructions on how toocreate a service principal in Azure AD.</span></span> <span data-ttu-id="fd116-134">No entanto, você deve ser um toocreate capaz do AD do Azure administrador toobe uma entidade de serviço.</span><span class="sxs-lookup"><span data-stu-id="fd116-134">However, you must be an Azure AD administrator toobe able toocreate a service principal.</span></span> <span data-ttu-id="fd116-135">Se você for um administrador do AD do Azure, você pode ignorar esse pré-requisito e continuar com o tutorial hello.</span><span class="sxs-lookup"><span data-stu-id="fd116-135">If you are an Azure AD administrator, you can skip this prerequisite and proceed with hello tutorial.</span></span>

    <span data-ttu-id="fd116-136">**Se você não for um administrador do AD do Azure**, não será capaz de tooperform Olá etapas necessárias toocreate uma entidade de serviço.</span><span class="sxs-lookup"><span data-stu-id="fd116-136">**If you are not an Azure AD administrator**, you will not be able tooperform hello steps required toocreate a service principal.</span></span> <span data-ttu-id="fd116-137">Nesse caso, o administrador do Azure AD deverá primeiro criar uma entidade de serviço antes de criar um cluster HDInsight com Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="fd116-137">In such a case, your Azure AD administrator must first create a service principal before you can create an HDInsight cluster with Data Lake Store.</span></span> <span data-ttu-id="fd116-138">Além disso, Olá entidade de serviço deve ser criada usando um certificado, conforme descrito em [criar uma entidade de serviço com certificado](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-certificate-from-certificate-authority).</span><span class="sxs-lookup"><span data-stu-id="fd116-138">Also, hello service principal must be created using a certificate, as described at [Create a service principal with certificate](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-certificate-from-certificate-authority).</span></span>

## <a name="create-an-azure-data-lake-store"></a><span data-ttu-id="fd116-139">Criar um Repositório Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="fd116-139">Create an Azure Data Lake Store</span></span>
<span data-ttu-id="fd116-140">Siga essas etapas toocreate um repositório Data Lake.</span><span class="sxs-lookup"><span data-stu-id="fd116-140">Follow these steps toocreate a Data Lake Store.</span></span>

1. <span data-ttu-id="fd116-141">Na área de trabalho, abra uma nova janela do PowerShell do Azure e insira Olá trecho de código a seguir.</span><span class="sxs-lookup"><span data-stu-id="fd116-141">From your desktop, open a new Azure PowerShell window, and enter hello following snippet.</span></span> <span data-ttu-id="fd116-142">Quando toolog solicitada, certifique-se de você fazer logon como um administrador/proprietário da assinatura hello:</span><span class="sxs-lookup"><span data-stu-id="fd116-142">When prompted toolog in, make sure you log in as one of hello subscription administrator/owner:</span></span>

        # Log in tooyour Azure account
        Login-AzureRmAccount

        # List all hello subscriptions associated tooyour account
        Get-AzureRmSubscription

        # Select a subscription
        Set-AzureRmContext -SubscriptionId <subscription ID>

        # Register for Data Lake Store
        Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.DataLakeStore"

   > [!NOTE]
   > <span data-ttu-id="fd116-143">Se você receber um erro semelhante muito`Register-AzureRmResourceProvider : InvalidResourceNamespace: hello resource namespace 'Microsoft.DataLakeStore' is invalid` ao registrar o provedor de recursos do repositório Data Lake Olá, é possível que a sua assinatura não está autorizado para repositório Azure Data Lake.</span><span class="sxs-lookup"><span data-stu-id="fd116-143">If you receive an error similar too`Register-AzureRmResourceProvider : InvalidResourceNamespace: hello resource namespace 'Microsoft.DataLakeStore' is invalid` when registering hello Data Lake Store resource provider, it is possible that your subscription is not whitelisted for Azure Data Lake Store.</span></span> <span data-ttu-id="fd116-144">Verifique se você habilitou sua assinatura do Azure para a visualização pública do Data Lake Store seguindo estas [instruções](data-lake-store-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="fd116-144">Make sure you enable your Azure subscription for Data Lake Store public preview by following these [instructions](data-lake-store-get-started-portal.md).</span></span>
   >
   >
2. <span data-ttu-id="fd116-145">Uma conta do Repositório Azure Data Lake está associada a um Grupo de Recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="fd116-145">An Azure Data Lake Store account is associated with an Azure Resource Group.</span></span> <span data-ttu-id="fd116-146">Comece criando um Grupo de Recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="fd116-146">Start by creating an Azure Resource Group.</span></span>

        $resourceGroupName = "<your new resource group name>"
        New-AzureRmResourceGroup -Name $resourceGroupName -Location "East US 2"

    <span data-ttu-id="fd116-147">Você verá uma saída semelhante à seguinte:</span><span class="sxs-lookup"><span data-stu-id="fd116-147">You should see an output like this:</span></span>

        ResourceGroupName : hdiadlgrp
        Location          : eastus2
        ProvisioningState : Succeeded
        Tags              :
        ResourceId        : /subscriptions/<subscription-id>/resourceGroups/hdiadlgrp

3. <span data-ttu-id="fd116-148">Crie uma conta do Repositório Azure Data Lake.</span><span class="sxs-lookup"><span data-stu-id="fd116-148">Create an Azure Data Lake Store account.</span></span> <span data-ttu-id="fd116-149">conta de saudação nome que você especificar deve conter apenas letras minúsculas e números.</span><span class="sxs-lookup"><span data-stu-id="fd116-149">hello account name you specify must only contain lowercase letters and numbers.</span></span>

        $dataLakeStoreName = "<your new Data Lake Store name>"
        New-AzureRmDataLakeStoreAccount -ResourceGroupName $resourceGroupName -Name $dataLakeStoreName -Location "East US 2"

    <span data-ttu-id="fd116-150">Você verá uma saída semelhante Olá seguinte:</span><span class="sxs-lookup"><span data-stu-id="fd116-150">You should see an output like hello following:</span></span>

        ...
        ProvisioningState           : Succeeded
        State                       : Active
        CreationTime                : 5/5/2017 10:53:56 PM
        EncryptionState             : Enabled
        ...
        LastModifiedTime            : 5/5/2017 10:53:56 PM
        Endpoint                    : hdiadlstore.azuredatalakestore.net
        DefaultGroup                :
        Id                          : /subscriptions/<subscription-id>/resourceGroups/hdiadlgrp/providers/Microsoft.DataLakeStore/accounts/hdiadlstore
        Name                        : hdiadlstore
        Type                        : Microsoft.DataLakeStore/accounts
        Location                    : East US 2
        Tags                        : {}

5. <span data-ttu-id="fd116-151">Carregar alguns dados de exemplo tooAzure Data Lake.</span><span class="sxs-lookup"><span data-stu-id="fd116-151">Upload some sample data tooAzure Data Lake.</span></span> <span data-ttu-id="fd116-152">Usaremos isso mais tarde neste tooverify artigo que dados saudação são acessíveis a partir de um cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="fd116-152">We'll use this later in this article tooverify that hello data is accessible from an HDInsight cluster.</span></span> <span data-ttu-id="fd116-153">Se você estiver procurando por alguns tooupload de dados de exemplo, você pode obter Olá **ambulância dados** pasta Olá [repositório Git do Azure Data Lake](https://github.com/MicrosoftBigData/usql/tree/master/Examples/Samples/Data/AmbulanceData).</span><span class="sxs-lookup"><span data-stu-id="fd116-153">If you are looking for some sample data tooupload, you can get hello **Ambulance Data** folder from hello [Azure Data Lake Git Repository](https://github.com/MicrosoftBigData/usql/tree/master/Examples/Samples/Data/AmbulanceData).</span></span>

        $myrootdir = "/"
        Import-AzureRmDataLakeStoreItem -AccountName $dataLakeStoreName -Path "C:\<path toodata>\vehicle1_09142014.csv" -Destination $myrootdir\vehicle1_09142014.csv


## <a name="set-up-authentication-for-role-based-access-toodata-lake-store"></a><span data-ttu-id="fd116-154">Configurar a autenticação para baseado em função acessar o repositório de Lake tooData</span><span class="sxs-lookup"><span data-stu-id="fd116-154">Set up authentication for role-based access tooData Lake Store</span></span>
<span data-ttu-id="fd116-155">Cada assinatura do Azure está associada com um Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="fd116-155">Every Azure subscription is associated with an Azure Active Directory.</span></span> <span data-ttu-id="fd116-156">Usuários e serviços que acessam os recursos de assinatura de saudação usando Olá Portal clássico do Azure ou API do Azure Resource Manager devem primeiro autenticar com que o Active Directory do Azure.</span><span class="sxs-lookup"><span data-stu-id="fd116-156">Users and services that access resources of hello subscription using hello Azure Classic Portal or Azure Resource Manager API must first authenticate with that Azure Active Directory.</span></span> <span data-ttu-id="fd116-157">Acesso tooAzure assinaturas e serviços, atribuindo-lhes a função apropriada de saudação em um recurso do Azure.</span><span class="sxs-lookup"><span data-stu-id="fd116-157">Access is granted tooAzure subscriptions and services by assigning them hello appropriate role on an Azure resource.</span></span>  <span data-ttu-id="fd116-158">Para serviços, uma entidade de serviço identifica o serviço Olá Olá Azure AAD (Active Directory).</span><span class="sxs-lookup"><span data-stu-id="fd116-158">For services, a service principal identifies hello service in hello Azure Active Directory (AAD).</span></span> <span data-ttu-id="fd116-159">Esta seção ilustra como toogrant um aplicativo de serviço, como HDInsight, tooan de acesso a recursos do Azure (Olá conta do repositório Azure Data Lake criado anteriormente), criar uma entidade de serviço para o aplicativo hello e atribuir funções toothat por meio do Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="fd116-159">This section illustrates how toogrant an application service, like HDInsight, access tooan Azure resource (hello Azure Data Lake Store account you created earlier) by creating a service principal for hello application and assigning roles toothat via Azure PowerShell.</span></span>

<span data-ttu-id="fd116-160">tooset a autenticação do Active Directory para o Azure Data Lake, você deve executar Olá tarefas a seguir.</span><span class="sxs-lookup"><span data-stu-id="fd116-160">tooset up Active Directory authentication for Azure Data Lake, you must perform hello following tasks.</span></span>

* <span data-ttu-id="fd116-161">Crie um certificado autoassinado</span><span class="sxs-lookup"><span data-stu-id="fd116-161">Create a self-signed certificate</span></span>
* <span data-ttu-id="fd116-162">Criar um aplicativo no Active Directory do Azure e uma entidade de serviço</span><span class="sxs-lookup"><span data-stu-id="fd116-162">Create an application in Azure Active Directory and a Service Principal</span></span>

### <a name="create-a-self-signed-certificate"></a><span data-ttu-id="fd116-163">Crie um certificado autoassinado</span><span class="sxs-lookup"><span data-stu-id="fd116-163">Create a self-signed certificate</span></span>
<span data-ttu-id="fd116-164">Verifique se você tem [SDK do Windows](https://dev.windows.com/en-us/downloads) instalado antes de prosseguir com a saudação as etapas nesta seção.</span><span class="sxs-lookup"><span data-stu-id="fd116-164">Make sure you have [Windows SDK](https://dev.windows.com/en-us/downloads) installed before proceeding with hello steps in this section.</span></span> <span data-ttu-id="fd116-165">Você deve também criou um diretório, como **C:\mycertdir**, qual certificado Olá será criado.</span><span class="sxs-lookup"><span data-stu-id="fd116-165">You must have also created a directory, such as **C:\mycertdir**, where hello certificate will be created.</span></span>

1. <span data-ttu-id="fd116-166">Na janela do PowerShell hello, navegar toohello local onde você instalou o SDK do Windows (normalmente, `C:\Program Files (x86)\Windows Kits\10\bin\x86` e usar Olá [MakeCert] [ makecert] toocreate utilitário um certificado autoassinado e uma chave privada.</span><span class="sxs-lookup"><span data-stu-id="fd116-166">From hello PowerShell window, navigate toohello location where you installed Windows SDK (typically, `C:\Program Files (x86)\Windows Kits\10\bin\x86` and use hello [MakeCert][makecert] utility toocreate a self-signed certificate and a private key.</span></span> <span data-ttu-id="fd116-167">Use Olá comandos a seguir.</span><span class="sxs-lookup"><span data-stu-id="fd116-167">Use hello following commands.</span></span>

        $certificateFileDir = "<my certificate directory>"
        cd $certificateFileDir

        makecert -sv mykey.pvk -n "cn=HDI-ADL-SP" CertFile.cer -r -len 2048

    <span data-ttu-id="fd116-168">Será a senha da chave privada tooenter solicitadas hello.</span><span class="sxs-lookup"><span data-stu-id="fd116-168">You will be prompted tooenter hello private key password.</span></span> <span data-ttu-id="fd116-169">Depois que o comando Olá for executado com êxito, você verá um **CertFile.cer** e **mykey.pvk** no diretório de certificado Olá especificado.</span><span class="sxs-lookup"><span data-stu-id="fd116-169">After hello command successfully executes, you should see a **CertFile.cer** and **mykey.pvk** in hello certificate directory you specified.</span></span>
2. <span data-ttu-id="fd116-170">Saudação de uso [Pvk2Pfx] [ pvk2pfx] . pvk do utilitário tooconvert hello e. cer arquivos de arquivo. pfx criado tooa MakeCert.</span><span class="sxs-lookup"><span data-stu-id="fd116-170">Use hello [Pvk2Pfx][pvk2pfx] utility tooconvert hello .pvk and .cer files that MakeCert created tooa .pfx file.</span></span> <span data-ttu-id="fd116-171">Execute Olá comando a seguir.</span><span class="sxs-lookup"><span data-stu-id="fd116-171">Run hello following command.</span></span>

        pvk2pfx -pvk mykey.pvk -spc CertFile.cer -pfx CertFile.pfx -po <password>

    <span data-ttu-id="fd116-172">Quando solicitado que digite Olá senha da chave privada especificado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="fd116-172">When prompted enter hello private key password you specified earlier.</span></span> <span data-ttu-id="fd116-173">Olá valor especificado para Olá **-po** parâmetro é a senha de saudação que está associada ao arquivo. pfx de saudação.</span><span class="sxs-lookup"><span data-stu-id="fd116-173">hello value you specify for hello **-po** parameter is hello password that is associated with hello .pfx file.</span></span> <span data-ttu-id="fd116-174">Após concluir com êxito do comando Olá, você verá também uma CertFile.pfx no diretório de certificado Olá especificado.</span><span class="sxs-lookup"><span data-stu-id="fd116-174">After hello command successfully completes, you should also see a CertFile.pfx in hello certificate directory you specified.</span></span>

### <a name="create-an-azure-active-directory-and-a-service-principal"></a><span data-ttu-id="fd116-175">Criar um Active Directory do Azure e uma entidade de serviço</span><span class="sxs-lookup"><span data-stu-id="fd116-175">Create an Azure Active Directory and a service principal</span></span>
<span data-ttu-id="fd116-176">Nesta seção, executar etapas de saudação toocreate uma entidade de serviço para um aplicativo do Active Directory do Azure, atribuir uma entidade de serviço de toohello de função e autenticar como entidade de serviço hello, fornecendo um certificado.</span><span class="sxs-lookup"><span data-stu-id="fd116-176">In this section, you perform hello steps toocreate a service principal for an Azure Active Directory application, assign a role toohello service principal, and authenticate as hello service principal by providing a certificate.</span></span> <span data-ttu-id="fd116-177">Olá toocreate comandos a seguir ao execute um aplicativo no Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="fd116-177">Run hello following commands toocreate an application in Azure Active Directory.</span></span>

1. <span data-ttu-id="fd116-178">Colar Olá cmdlets na janela de console do PowerShell Olá a seguir.</span><span class="sxs-lookup"><span data-stu-id="fd116-178">Paste hello following cmdlets in hello PowerShell console window.</span></span> <span data-ttu-id="fd116-179">Verifique se valor Olá você especificar para Olá **- DisplayName** propriedade é exclusiva.</span><span class="sxs-lookup"><span data-stu-id="fd116-179">Make sure hello value you specify for hello **-DisplayName** property is unique.</span></span> <span data-ttu-id="fd116-180">Além disso, Olá valores para **- home page** e **- IdentiferUris** são valores de espaço reservado e não são verificadas.</span><span class="sxs-lookup"><span data-stu-id="fd116-180">Also, hello values for **-HomePage** and **-IdentiferUris** are placeholder values and are not verified.</span></span>

        $certificateFilePath = "$certificateFileDir\CertFile.pfx"

        $password = Read-Host –Prompt "Enter hello password" # This is hello password you specified for hello .pfx file

        $certificatePFX = New-Object System.Security.Cryptography.X509Certificates.X509Certificate2($certificateFilePath, $password)

        $rawCertificateData = $certificatePFX.GetRawCertData()

        $credential = [System.Convert]::ToBase64String($rawCertificateData)

        $application = New-AzureRmADApplication `
            -DisplayName "HDIADL" `
            -HomePage "https://contoso.com" `
            -IdentifierUris "https://mycontoso.com" `
            -CertValue $credential  `
            -StartDate $certificatePFX.NotBefore  `
            -EndDate $certificatePFX.NotAfter

        $applicationId = $application.ApplicationId
2. <span data-ttu-id="fd116-181">Criar uma entidade de serviço usando a ID do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="fd116-181">Create a service principal using hello application ID.</span></span>

        $servicePrincipal = New-AzureRmADServicePrincipal -ApplicationId $applicationId

        $objectId = $servicePrincipal.Id
3. <span data-ttu-id="fd116-182">Conceder a pasta do repositório Data Lake do hello serviço de acesso principal toohello e arquivo hello que você irá acessar do cluster do HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="fd116-182">Grant hello service principal access toohello Data Lake Store folder and hello file that you will access from hello HDInsight cluster.</span></span> <span data-ttu-id="fd116-183">trecho de saudação abaixo fornece raiz toohello acesso Olá repositório Data Lake (onde você copiou o arquivo de dados de exemplo hello) de conta e Olá próprio arquivo.</span><span class="sxs-lookup"><span data-stu-id="fd116-183">hello snippet below provides access toohello root of hello Data Lake Store account (where you copied hello sample data file), and hello file itself.</span></span>

        Set-AzureRmDataLakeStoreItemAclEntry -AccountName $dataLakeStoreName -Path / -AceType User -Id $objectId -Permissions All
        Set-AzureRmDataLakeStoreItemAclEntry -AccountName $dataLakeStoreName -Path /vehicle1_09142014.csv -AceType User -Id $objectId -Permissions All

## <a name="create-an-hdinsight-linux-cluster-with-data-lake-store-as-additional-storage"></a><span data-ttu-id="fd116-184">Criar um cluster Linux HDInsight com o Data Lake Store como armazenamento adicional</span><span class="sxs-lookup"><span data-stu-id="fd116-184">Create an HDInsight Linux cluster with Data Lake Store as additional storage</span></span>

<span data-ttu-id="fd116-185">Nesta seção, criamos um cluster Linux Hadoop HDInsight com o Data Lake Store como armazenamento adicional.</span><span class="sxs-lookup"><span data-stu-id="fd116-185">In this section, we create an HDInsight Hadoop Linux cluster with Data Lake Store as additional storage.</span></span> <span data-ttu-id="fd116-186">Para esta versão, cluster de HDInsight hello e repositório Olá Data Lake devem estar no hello mesmo local.</span><span class="sxs-lookup"><span data-stu-id="fd116-186">For this release, hello HDInsight cluster and hello Data Lake Store must be in hello same location.</span></span>

1. <span data-ttu-id="fd116-187">Iniciar com a recuperação de ID de locatário de assinatura de saudação.</span><span class="sxs-lookup"><span data-stu-id="fd116-187">Start with retrieving hello subscription tenant ID.</span></span> <span data-ttu-id="fd116-188">Você precisará disso posteriormente.</span><span class="sxs-lookup"><span data-stu-id="fd116-188">You will need that later.</span></span>

        $tenantID = (Get-AzureRmContext).Tenant.TenantId
2. <span data-ttu-id="fd116-189">Para esta versão, para um cluster de Hadoop, repositório Data Lake pode ser usado somente como um armazenamento adicional para cluster hello.</span><span class="sxs-lookup"><span data-stu-id="fd116-189">For this release, for a Hadoop cluster, Data Lake Store can only be used as an additional storage for hello cluster.</span></span> <span data-ttu-id="fd116-190">armazenamento padrão da saudação ainda serão blobs de armazenamento do Azure hello (WASB).</span><span class="sxs-lookup"><span data-stu-id="fd116-190">hello default storage will still be hello Azure storage blobs (WASB).</span></span> <span data-ttu-id="fd116-191">Assim, vamos primeiro criar hello contêineres de armazenamento e a conta de armazenamento necessários para o cluster de saudação.</span><span class="sxs-lookup"><span data-stu-id="fd116-191">So, we'll first create hello storage account and storage containers required for hello cluster.</span></span>

        # Create an Azure storage account
        $location = "East US 2"
        $storageAccountName = "<StorageAcccountName>"   # Provide a Storage account name

        New-AzureRmStorageAccount -ResourceGroupName $resourceGroupName -StorageAccountName $storageAccountName -Location $location -Type Standard_GRS

        # Create an Azure Blob Storage container
        $containerName = "<ContainerName>"              # Provide a container name
        $storageAccountKey = (Get-AzureRmStorageAccountKey -Name $storageAccountName -ResourceGroupName $resourceGroupName)[0].Value
        $destContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey
        New-AzureStorageContainer -Name $containerName -Context $destContext
3. <span data-ttu-id="fd116-192">Crie cluster do HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="fd116-192">Create hello HDInsight cluster.</span></span> <span data-ttu-id="fd116-193">Use Olá cmdlets a seguir.</span><span class="sxs-lookup"><span data-stu-id="fd116-193">Use hello following cmdlets.</span></span>

        # Set these variables
        $clusterName = $containerName                   # As a best practice, have hello same name for hello cluster and container
        $clusterNodes = <ClusterSizeInNodes>            # hello number of nodes in hello HDInsight cluster
        $httpCredentials = Get-Credential
        $sshCredentials = Get-Credential

        New-AzureRmHDInsightCluster -ClusterName $clusterName -ResourceGroupName $resourceGroupName -HttpCredential $httpCredentials -Location $location -DefaultStorageAccountName "$storageAccountName.blob.core.windows.net" -DefaultStorageAccountKey $storageAccountKey -DefaultStorageContainer $containerName  -ClusterSizeInNodes $clusterNodes -ClusterType Hadoop -Version "3.4" -OSType Linux -SshCredential $sshCredentials -ObjectID $objectId -AadTenantId $tenantID -CertificateFilePath $certificateFilePath -CertificatePassword $password

    <span data-ttu-id="fd116-194">Depois que o cmdlet Olá for concluído com êxito, você verá uma saída listando os detalhes do cluster Olá.</span><span class="sxs-lookup"><span data-stu-id="fd116-194">After hello cmdlet successfully completes, you should see an output listing hello cluster details.</span></span>


## <a name="run-test-jobs-on-hello-hdinsight-cluster-toouse-hello-data-lake-store"></a><span data-ttu-id="fd116-195">Executar trabalhos de teste em Olá HDInsight cluster toouse Olá repositório Data Lake</span><span class="sxs-lookup"><span data-stu-id="fd116-195">Run test jobs on hello HDInsight cluster toouse hello Data Lake Store</span></span>
<span data-ttu-id="fd116-196">Depois de configurar um cluster HDInsight, você pode executar trabalhos de teste em Olá cluster tootest que Olá HDInsight cluster pode acessar o repositório Data Lake.</span><span class="sxs-lookup"><span data-stu-id="fd116-196">After you have configured an HDInsight cluster, you can run test jobs on hello cluster tootest that hello HDInsight cluster can access Data Lake Store.</span></span> <span data-ttu-id="fd116-197">toodo assim, iremos executar um trabalho de Hive de exemplo que cria uma tabela usando dados de exemplo hello que você carregou anteriormente repositório tooyour Data Lake.</span><span class="sxs-lookup"><span data-stu-id="fd116-197">toodo so, we will run a sample Hive job that creates a table using hello sample data that you uploaded earlier tooyour Data Lake Store.</span></span>

<span data-ttu-id="fd116-198">Nesta seção, você irá SSH para Olá HDInsight Linux do cluster é criado e executado Olá um exemplo de consulta de Hive.</span><span class="sxs-lookup"><span data-stu-id="fd116-198">In this section you will SSH into hello HDInsight Linux cluster you created and run hello a sample Hive query.</span></span>

* <span data-ttu-id="fd116-199">Se você estiver usando um tooSSH de cliente do Windows em cluster hello, consulte [usar SSH com baseados em Linux Hadoop no HDInsight do Windows](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).</span><span class="sxs-lookup"><span data-stu-id="fd116-199">If you are using a Windows client tooSSH into hello cluster, see [Use SSH with Linux-based Hadoop on HDInsight from Windows](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).</span></span>
* <span data-ttu-id="fd116-200">Se você estiver usando um tooSSH de cliente do Linux em cluster hello, consulte [usar SSH com baseados em Linux Hadoop no HDInsight do Linux](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md)</span><span class="sxs-lookup"><span data-stu-id="fd116-200">If you are using a Linux client tooSSH into hello cluster, see [Use SSH with Linux-based Hadoop on HDInsight from Linux](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md)</span></span>

1. <span data-ttu-id="fd116-201">Uma vez conectado, inicie Olá CLI do Hive usando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="fd116-201">Once connected, start hello Hive CLI by using hello following command:</span></span>

        hive
2. <span data-ttu-id="fd116-202">Usando Olá CLI, insira Olá seguindo as instruções toocreate uma nova tabela nomeada **veículos** com dados de exemplo hello Olá repositório Data Lake:</span><span class="sxs-lookup"><span data-stu-id="fd116-202">Using hello CLI, enter hello following statements toocreate a new table named **vehicles** by using hello sample data in hello Data Lake Store:</span></span>

        DROP TABLE vehicles;
        CREATE EXTERNAL TABLE vehicles (str string) LOCATION 'adl://<mydatalakestore>.azuredatalakestore.net:443/';
        SELECT * FROM vehicles LIMIT 10;

    <span data-ttu-id="fd116-203">Você verá uma saída semelhante toohello a seguir:</span><span class="sxs-lookup"><span data-stu-id="fd116-203">You should see an output similar toohello following:</span></span>

        1,1,2014-09-14 00:00:03,46.81006,-92.08174,51,S,1
        1,2,2014-09-14 00:00:06,46.81006,-92.08174,13,NE,1
        1,3,2014-09-14 00:00:09,46.81006,-92.08174,48,NE,1
        1,4,2014-09-14 00:00:12,46.81006,-92.08174,30,W,1
        1,5,2014-09-14 00:00:15,46.81006,-92.08174,47,S,1
        1,6,2014-09-14 00:00:18,46.81006,-92.08174,9,S,1
        1,7,2014-09-14 00:00:21,46.81006,-92.08174,53,N,1
        1,8,2014-09-14 00:00:24,46.81006,-92.08174,63,SW,1
        1,9,2014-09-14 00:00:27,46.81006,-92.08174,4,NE,1
        1,10,2014-09-14 00:00:30,46.81006,-92.08174,31,N,1

## <a name="access-data-lake-store-using-hdfs-commands"></a><span data-ttu-id="fd116-204">Repositório Data Lake usando comandos do HDFS</span><span class="sxs-lookup"><span data-stu-id="fd116-204">Access Data Lake Store using HDFS commands</span></span>
<span data-ttu-id="fd116-205">Quando você tiver configurado o repositório Data Lake do toouse de cluster de HDInsight hello, você pode usar comandos de shell do hello HDFS tooaccess Olá repositório.</span><span class="sxs-lookup"><span data-stu-id="fd116-205">Once you have configured hello HDInsight cluster toouse Data Lake Store, you can use hello HDFS shell commands tooaccess hello store.</span></span>

<span data-ttu-id="fd116-206">Nesta seção, você irá SSH para Olá HDInsight Linux criado e executar comandos HDFS de saudação do cluster.</span><span class="sxs-lookup"><span data-stu-id="fd116-206">In this section you will SSH into hello HDInsight Linux cluster you created and run hello HDFS commands.</span></span>

* <span data-ttu-id="fd116-207">Se você estiver usando um tooSSH de cliente do Windows em cluster hello, consulte [usar SSH com baseados em Linux Hadoop no HDInsight do Windows](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).</span><span class="sxs-lookup"><span data-stu-id="fd116-207">If you are using a Windows client tooSSH into hello cluster, see [Use SSH with Linux-based Hadoop on HDInsight from Windows](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).</span></span>
* <span data-ttu-id="fd116-208">Se você estiver usando um tooSSH de cliente do Linux em cluster hello, consulte [usar SSH com baseados em Linux Hadoop no HDInsight do Linux](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md)</span><span class="sxs-lookup"><span data-stu-id="fd116-208">If you are using a Linux client tooSSH into hello cluster, see [Use SSH with Linux-based Hadoop on HDInsight from Linux](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md)</span></span>

<span data-ttu-id="fd116-209">Uma vez conectado, use Olá arquivos HDFS filesystem comando toolist Olá no hello repositório Data Lake a seguir.</span><span class="sxs-lookup"><span data-stu-id="fd116-209">Once connected, use hello following HDFS filesystem command toolist hello files in hello Data Lake Store.</span></span>

    hdfs dfs -ls adl://<Data Lake Store account name>.azuredatalakestore.net:443/

<span data-ttu-id="fd116-210">Isso deve listar arquivo hello que você carregou anteriormente repositório toohello Data Lake.</span><span class="sxs-lookup"><span data-stu-id="fd116-210">This should list hello file that you uploaded earlier toohello Data Lake Store.</span></span>

    15/09/17 21:41:15 INFO web.CaboWebHdfsFileSystem: Replacing original urlConnectionFactory with org.apache.hadoop.hdfs.web.URLConnectionFactory@21a728d6
    Found 1 items
    -rwxrwxrwx   0 NotSupportYet NotSupportYet     671388 2015-09-16 22:16 adl://mydatalakestore.azuredatalakestore.net:443/mynewfolder

<span data-ttu-id="fd116-211">Você também pode usar o hello `hdfs dfs -put` comando tooupload toohello alguns arquivos repositório Data Lake e, em seguida, usar `hdfs dfs -ls` tooverify arquivos Olá foram carregados com êxito.</span><span class="sxs-lookup"><span data-stu-id="fd116-211">You can also use hello `hdfs dfs -put` command tooupload some files toohello Data Lake Store, and then use `hdfs dfs -ls` tooverify whether hello files were successfully uploaded.</span></span>

## <a name="see-also"></a><span data-ttu-id="fd116-212">Consulte também</span><span class="sxs-lookup"><span data-stu-id="fd116-212">See Also</span></span>
* [<span data-ttu-id="fd116-213">Portal: Criar um cluster de HDInsight toouse repositório Data Lake</span><span class="sxs-lookup"><span data-stu-id="fd116-213">Portal: Create an HDInsight cluster toouse Data Lake Store</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)

[makecert]: https://msdn.microsoft.com/library/windows/desktop/ff548309(v=vs.85).aspx
[pvk2pfx]: https://msdn.microsoft.com/library/windows/desktop/ff550672(v=vs.85).aspx
