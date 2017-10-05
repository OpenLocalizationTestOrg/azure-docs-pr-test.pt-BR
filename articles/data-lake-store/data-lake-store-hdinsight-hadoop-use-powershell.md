---
title: 'PowerShell: cluster HDInsight do Azure Data Lake Store como o armazenamento do complemento | Microsoft Docs'
services: data-lake-store,hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 164ada5a-222e-4be2-bd32-e51dbe993bc0
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/08/2017
ms.author: nitinme
ms.openlocfilehash: 7a7069adab5742a9dae2833c13a1db57337a41a0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="use-azure-powershell-to-create-an-hdinsight-cluster-with-data-lake-store-as-additional-storage"></a><span data-ttu-id="71881-102">Use o Azure PowerShell para criar um cluster HDInsight com o Data Lake Store (como o armazenamento adicional)</span><span class="sxs-lookup"><span data-stu-id="71881-102">Use Azure PowerShell to create an HDInsight cluster with Data Lake Store (as additional storage)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="71881-103">Usando o Portal</span><span class="sxs-lookup"><span data-stu-id="71881-103">Using Portal</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)
> * [<span data-ttu-id="71881-104">Usando o PowerShell (para o armazenamento padrão)</span><span class="sxs-lookup"><span data-stu-id="71881-104">Using PowerShell (for default storage)</span></span>](data-lake-store-hdinsight-hadoop-use-powershell-for-default-storage.md)
> * [<span data-ttu-id="71881-105">Usando o PowerShell (para o armazenamento adicional)</span><span class="sxs-lookup"><span data-stu-id="71881-105">Using PowerShell (for additional storage)</span></span>](data-lake-store-hdinsight-hadoop-use-powershell.md)
> * [<span data-ttu-id="71881-106">Usando o Gerenciador de Recursos</span><span class="sxs-lookup"><span data-stu-id="71881-106">Using Resource Manager</span></span>](data-lake-store-hdinsight-hadoop-use-resource-manager-template.md)
>
>

<span data-ttu-id="71881-107">Aprenda a usar o Azure PowerShell para configurar um cluster HDInsight com o Azure Data Lake Store **como armazenamento adicional**.</span><span class="sxs-lookup"><span data-stu-id="71881-107">Learn how to use Azure PowerShell to configure an HDInsight cluster with Azure Data Lake Store, **as additional storage**.</span></span> <span data-ttu-id="71881-108">Para obter instruções sobre como criar um cluster HDInsight com o Azure Data Lake Store como armazenamento padrão, veja [Criar um cluster HDInsight com o Data Lake Store como armazenamento padrão](data-lake-store-hdinsight-hadoop-use-powershell-for-default-storage.md).</span><span class="sxs-lookup"><span data-stu-id="71881-108">For instructions on how to create an HDInsight cluster with Azure Data Lake Store as default storage, see [Create an HDInsight cluster with Data Lake Store as default storage](data-lake-store-hdinsight-hadoop-use-powershell-for-default-storage.md).</span></span>

> [!NOTE]
> <span data-ttu-id="71881-109">Se você pretende usar o Azure Data Lake Store como armazenamento adicional para o cluster HDInsight, é altamente recomendável que faça isso ao criar o cluster, conforme descrito neste artigo.</span><span class="sxs-lookup"><span data-stu-id="71881-109">If you are going to use Azure Data Lake Store as additional storage for HDInsight cluster, we strongly recommend that you do this while you create the cluster as described in this article.</span></span> <span data-ttu-id="71881-110">Adicionar o Azure Data Lake Store como mais armazenamento para um cluster HDInsight existente é um processo complicado e propenso a erros.</span><span class="sxs-lookup"><span data-stu-id="71881-110">Adding Azure Data Lake Store as additional storage to an existing HDInsight cluster is a complicated process and prone to errors.</span></span>
>

<span data-ttu-id="71881-111">Para tipos de cluster com suporte, o Data Lake Store pode ser usado como um armazenamento padrão ou uma conta de armazenamento adicional.</span><span class="sxs-lookup"><span data-stu-id="71881-111">For supported cluster types, Data Lake Store can be used as a default storage or additional storage account.</span></span> <span data-ttu-id="71881-112">Quando o Data Lake Store é usado como armazenamento adicional, a conta de armazenamento padrão para os clusters ainda será Blobs de Armazenamento do Azure (WASB) e os arquivos relacionados ao cluster (como logs, etc.) ainda serão gravados no armazenamento padrão, embora os dados que você queira processar possam ser armazenados em uma conta do Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="71881-112">When Data Lake Store is used as additional storage, the default storage account for the clusters will still be Azure Storage Blobs (WASB) and the cluster-related files (such as logs, etc.) are still written to the default storage, while the data that you want to process can be stored in a Data Lake Store account.</span></span> <span data-ttu-id="71881-113">O uso do Repositório Data Lake como uma conta de armazenamento adicional não afeta o desempenho ou a capacidade de leitura/gravação no armazenamento do cluster.</span><span class="sxs-lookup"><span data-stu-id="71881-113">Using Data Lake Store as an additional storage account does not impact performance or the ability to read/write to the storage from the cluster.</span></span>

## <a name="using-data-lake-store-for-hdinsight-cluster-storage"></a><span data-ttu-id="71881-114">Usando o Data Lake Store para armazenamento do cluster HDInsight</span><span class="sxs-lookup"><span data-stu-id="71881-114">Using Data Lake Store for HDInsight cluster storage</span></span>

<span data-ttu-id="71881-115">Aqui estão algumas considerações importantes para usar o HDInsight com o Data Lake Store:</span><span class="sxs-lookup"><span data-stu-id="71881-115">Here are some important considerations for using HDInsight with Data Lake Store:</span></span>

* <span data-ttu-id="71881-116">A opção para criar clusters HDInsight com acesso ao Data Lake Store como armazenamento adicional está disponível para o HDInsight versões 3.2, 3.4, 3.5 e 3.6.</span><span class="sxs-lookup"><span data-stu-id="71881-116">Option to create HDInsight clusters with access to Data Lake Store as additional storage is available for HDInsight versions 3.2, 3.4, 3.5, and 3.6.</span></span>

<span data-ttu-id="71881-117">A configuração do HDInsight para trabalhar com o Repositório Data Lake usando o PowerShell envolve as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="71881-117">Configuring HDInsight to work with Data Lake Store using PowerShell involves the following steps:</span></span>

* <span data-ttu-id="71881-118">Criar um Repositório Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="71881-118">Create an Azure Data Lake Store</span></span>
* <span data-ttu-id="71881-119">Configurar a autenticação para acesso baseado em dados ao Repositório Data Lake</span><span class="sxs-lookup"><span data-stu-id="71881-119">Set up authentication for role-based access to Data Lake Store</span></span>
* <span data-ttu-id="71881-120">Criar o cluster HDInsight com a autenticação para o Repositório Data Lake</span><span class="sxs-lookup"><span data-stu-id="71881-120">Create HDInsight cluster with authentication to Data Lake Store</span></span>
* <span data-ttu-id="71881-121">Executar um trabalho de teste no cluster</span><span class="sxs-lookup"><span data-stu-id="71881-121">Run a test job on the cluster</span></span>

## <a name="prerequisites"></a><span data-ttu-id="71881-122">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="71881-122">Prerequisites</span></span>
<span data-ttu-id="71881-123">Antes de começar este tutorial, você deve ter o seguinte:</span><span class="sxs-lookup"><span data-stu-id="71881-123">Before you begin this tutorial, you must have the following:</span></span>

* <span data-ttu-id="71881-124">**Uma assinatura do Azure**.</span><span class="sxs-lookup"><span data-stu-id="71881-124">**An Azure subscription**.</span></span> <span data-ttu-id="71881-125">Consulte [Obter avaliação gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="71881-125">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="71881-126">**Azure PowerShell 1.0 ou superior**.</span><span class="sxs-lookup"><span data-stu-id="71881-126">**Azure PowerShell 1.0 or greater**.</span></span> <span data-ttu-id="71881-127">Consulte [Como instalar e configurar o PowerShell do Azure](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="71881-127">See [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="71881-128">**SDK do Windows**.</span><span class="sxs-lookup"><span data-stu-id="71881-128">**Windows SDK**.</span></span> <span data-ttu-id="71881-129">Você pode instalá-lo clicando [aqui](https://dev.windows.com/en-us/downloads).</span><span class="sxs-lookup"><span data-stu-id="71881-129">You can install it from [here](https://dev.windows.com/en-us/downloads).</span></span> <span data-ttu-id="71881-130">Use isso para criar um certificado de segurança.</span><span class="sxs-lookup"><span data-stu-id="71881-130">You use this to create a security certificate.</span></span>
* <span data-ttu-id="71881-131">**Entidade de serviço do Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="71881-131">**Azure Active Directory Service Principal**.</span></span> <span data-ttu-id="71881-132">As etapas neste tutorial fornecem instruções sobre como criar uma entidade de serviço no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="71881-132">Steps in this tutorial provide instructions on how to create a service principal in Azure AD.</span></span> <span data-ttu-id="71881-133">No entanto, você deve ser administrador do Azure AD para poder criar uma entidade de serviço.</span><span class="sxs-lookup"><span data-stu-id="71881-133">However, you must be an Azure AD administrator to be able to create a service principal.</span></span> <span data-ttu-id="71881-134">Se você for administrador do Azure AD, poderá ignorar esse pré-requisito e continuar com o tutorial.</span><span class="sxs-lookup"><span data-stu-id="71881-134">If you are an Azure AD administrator, you can skip this prerequisite and proceed with the tutorial.</span></span>

    <span data-ttu-id="71881-135">**Se você não for um administrador do Azure AD**, não poderá executar as etapas necessárias para criar uma entidade de serviço.</span><span class="sxs-lookup"><span data-stu-id="71881-135">**If you are not an Azure AD administrator**, you will not be able to perform the steps required to create a service principal.</span></span> <span data-ttu-id="71881-136">Nesse caso, o administrador do Azure AD deverá primeiro criar uma entidade de serviço antes de criar um cluster HDInsight com Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="71881-136">In such a case, your Azure AD administrator must first create a service principal before you can create an HDInsight cluster with Data Lake Store.</span></span> <span data-ttu-id="71881-137">Além disso, a entidade de serviço deve ser criada usando um certificado, conforme descrito em [Criar uma entidade de serviço com certificado](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-certificate-from-certificate-authority).</span><span class="sxs-lookup"><span data-stu-id="71881-137">Also, the service principal must be created using a certificate, as described at [Create a service principal with certificate](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-certificate-from-certificate-authority).</span></span>

## <a name="create-an-azure-data-lake-store"></a><span data-ttu-id="71881-138">Criar um Repositório Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="71881-138">Create an Azure Data Lake Store</span></span>
<span data-ttu-id="71881-139">Execute estas etapas para criar um Repositório Data Lake.</span><span class="sxs-lookup"><span data-stu-id="71881-139">Follow these steps to create a Data Lake Store.</span></span>

1. <span data-ttu-id="71881-140">Na área de trabalho, abra uma nova janela do Azure PowerShell e insira o trecho a seguir.</span><span class="sxs-lookup"><span data-stu-id="71881-140">From your desktop, open a new Azure PowerShell window, and enter the following snippet.</span></span> <span data-ttu-id="71881-141">Quando solicitado a fazer logon, lembre-se de fazer logon como um dos proprietários/administradores da assinatura:</span><span class="sxs-lookup"><span data-stu-id="71881-141">When prompted to log in, make sure you log in as one of the subscription administrator/owner:</span></span>

        # Log in to your Azure account
        Login-AzureRmAccount

        # List all the subscriptions associated to your account
        Get-AzureRmSubscription

        # Select a subscription
        Set-AzureRmContext -SubscriptionId <subscription ID>

        # Register for Data Lake Store
        Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.DataLakeStore"

   > [!NOTE]
   > <span data-ttu-id="71881-142">Se você receber um erro semelhante a `Register-AzureRmResourceProvider : InvalidResourceNamespace: The resource namespace 'Microsoft.DataLakeStore' is invalid` ao registrar o provedor de recursos do Data Lake Store, é possível que sua assinatura não esteja na lista branca do Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="71881-142">If you receive an error similar to `Register-AzureRmResourceProvider : InvalidResourceNamespace: The resource namespace 'Microsoft.DataLakeStore' is invalid` when registering the Data Lake Store resource provider, it is possible that your subscription is not whitelisted for Azure Data Lake Store.</span></span> <span data-ttu-id="71881-143">Verifique se você habilitou sua assinatura do Azure para a visualização pública do Data Lake Store seguindo estas [instruções](data-lake-store-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="71881-143">Make sure you enable your Azure subscription for Data Lake Store public preview by following these [instructions](data-lake-store-get-started-portal.md).</span></span>
   >
   >
2. <span data-ttu-id="71881-144">Uma conta do Repositório Azure Data Lake está associada a um Grupo de Recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="71881-144">An Azure Data Lake Store account is associated with an Azure Resource Group.</span></span> <span data-ttu-id="71881-145">Comece criando um Grupo de Recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="71881-145">Start by creating an Azure Resource Group.</span></span>

        $resourceGroupName = "<your new resource group name>"
        New-AzureRmResourceGroup -Name $resourceGroupName -Location "East US 2"

    <span data-ttu-id="71881-146">Você verá uma saída semelhante à seguinte:</span><span class="sxs-lookup"><span data-stu-id="71881-146">You should see an output like this:</span></span>

        ResourceGroupName : hdiadlgrp
        Location          : eastus2
        ProvisioningState : Succeeded
        Tags              :
        ResourceId        : /subscriptions/<subscription-id>/resourceGroups/hdiadlgrp

3. <span data-ttu-id="71881-147">Crie uma conta do Repositório Azure Data Lake.</span><span class="sxs-lookup"><span data-stu-id="71881-147">Create an Azure Data Lake Store account.</span></span> <span data-ttu-id="71881-148">O nome especificado para a conta deve conter apenas letras minúsculas e números.</span><span class="sxs-lookup"><span data-stu-id="71881-148">The account name you specify must only contain lowercase letters and numbers.</span></span>

        $dataLakeStoreName = "<your new Data Lake Store name>"
        New-AzureRmDataLakeStoreAccount -ResourceGroupName $resourceGroupName -Name $dataLakeStoreName -Location "East US 2"

    <span data-ttu-id="71881-149">Você verá algo semelhante ao mostrado a seguir:</span><span class="sxs-lookup"><span data-stu-id="71881-149">You should see an output like the following:</span></span>

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

5. <span data-ttu-id="71881-150">Carregue alguns exemplos de dados no Azure Data Lake.</span><span class="sxs-lookup"><span data-stu-id="71881-150">Upload some sample data to Azure Data Lake.</span></span> <span data-ttu-id="71881-151">Usaremos isso posteriormente neste artigo para verificar se os dados podem ser acessados a partir de um cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="71881-151">We'll use this later in this article to verify that the data is accessible from an HDInsight cluster.</span></span> <span data-ttu-id="71881-152">Se estiver procurando alguns dados de exemplo para carregar, é possível obter a pasta **Dados da Ambulância** no [Repositório Git do Azure Data Lake](https://github.com/MicrosoftBigData/usql/tree/master/Examples/Samples/Data/AmbulanceData).</span><span class="sxs-lookup"><span data-stu-id="71881-152">If you are looking for some sample data to upload, you can get the **Ambulance Data** folder from the [Azure Data Lake Git Repository](https://github.com/MicrosoftBigData/usql/tree/master/Examples/Samples/Data/AmbulanceData).</span></span>

        $myrootdir = "/"
        Import-AzureRmDataLakeStoreItem -AccountName $dataLakeStoreName -Path "C:\<path to data>\vehicle1_09142014.csv" -Destination $myrootdir\vehicle1_09142014.csv


## <a name="set-up-authentication-for-role-based-access-to-data-lake-store"></a><span data-ttu-id="71881-153">Configurar a autenticação para acesso baseado em dados ao Repositório Data Lake</span><span class="sxs-lookup"><span data-stu-id="71881-153">Set up authentication for role-based access to Data Lake Store</span></span>
<span data-ttu-id="71881-154">Cada assinatura do Azure está associada com um Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="71881-154">Every Azure subscription is associated with an Azure Active Directory.</span></span> <span data-ttu-id="71881-155">Os usuários e serviços que acessam os recursos da assinatura usando o Portal Clássico do Azure ou a API do Azure Resource Manager primeiro precisam realizar a autenticação com o Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="71881-155">Users and services that access resources of the subscription using the Azure Classic Portal or Azure Resource Manager API must first authenticate with that Azure Active Directory.</span></span> <span data-ttu-id="71881-156">O acesso é concedido às assinaturas e serviços do Azure atribuindo a função apropriada para eles em um recurso do Azure.</span><span class="sxs-lookup"><span data-stu-id="71881-156">Access is granted to Azure subscriptions and services by assigning them the appropriate role on an Azure resource.</span></span>  <span data-ttu-id="71881-157">Para serviços, uma entidade de serviço identifica o serviço no Active Directory do Azure (AAD).</span><span class="sxs-lookup"><span data-stu-id="71881-157">For services, a service principal identifies the service in the Azure Active Directory (AAD).</span></span> <span data-ttu-id="71881-158">Esta seção ilustra como conceder a um serviço de aplicativo, como o HDInsight, acesso a um recurso do Azure (a conta do Repositório Azure Data Lake criada anteriormente), criando uma entidade de serviço para o aplicativo e atribuindo funções a ela por meio do Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="71881-158">This section illustrates how to grant an application service, like HDInsight, access to an Azure resource (the Azure Data Lake Store account you created earlier) by creating a service principal for the application and assigning roles to that via Azure PowerShell.</span></span>

<span data-ttu-id="71881-159">Para configurar a autenticação do Active Directory para o Azure Data Lake, você deve executar as seguintes tarefas.</span><span class="sxs-lookup"><span data-stu-id="71881-159">To set up Active Directory authentication for Azure Data Lake, you must perform the following tasks.</span></span>

* <span data-ttu-id="71881-160">Crie um certificado autoassinado</span><span class="sxs-lookup"><span data-stu-id="71881-160">Create a self-signed certificate</span></span>
* <span data-ttu-id="71881-161">Criar um aplicativo no Active Directory do Azure e uma entidade de serviço</span><span class="sxs-lookup"><span data-stu-id="71881-161">Create an application in Azure Active Directory and a Service Principal</span></span>

### <a name="create-a-self-signed-certificate"></a><span data-ttu-id="71881-162">Crie um certificado autoassinado</span><span class="sxs-lookup"><span data-stu-id="71881-162">Create a self-signed certificate</span></span>
<span data-ttu-id="71881-163">Verifique se o [SDK do Windows](https://dev.windows.com/en-us/downloads) está instalado antes de continuar com as etapas nesta seção.</span><span class="sxs-lookup"><span data-stu-id="71881-163">Make sure you have [Windows SDK](https://dev.windows.com/en-us/downloads) installed before proceeding with the steps in this section.</span></span> <span data-ttu-id="71881-164">Você também deve ter criado um diretório, como **C:\mycertdir**, no qual o certificado será criado.</span><span class="sxs-lookup"><span data-stu-id="71881-164">You must have also created a directory, such as **C:\mycertdir**, where the certificate will be created.</span></span>

1. <span data-ttu-id="71881-165">Na janela do PowerShell, navegue até o local no qual você instalou o SDK do Windows (normalmente, `C:\Program Files (x86)\Windows Kits\10\bin\x86` e use o utilitário [MakeCert][makecert] para criar um certificado autoassinado e uma chave privada.</span><span class="sxs-lookup"><span data-stu-id="71881-165">From the PowerShell window, navigate to the location where you installed Windows SDK (typically, `C:\Program Files (x86)\Windows Kits\10\bin\x86` and use the [MakeCert][makecert] utility to create a self-signed certificate and a private key.</span></span> <span data-ttu-id="71881-166">Use os seguintes comandos.</span><span class="sxs-lookup"><span data-stu-id="71881-166">Use the following commands.</span></span>

        $certificateFileDir = "<my certificate directory>"
        cd $certificateFileDir

        makecert -sv mykey.pvk -n "cn=HDI-ADL-SP" CertFile.cer -r -len 2048

    <span data-ttu-id="71881-167">Você receberá uma solicitação para inserir a senha da chave privada.</span><span class="sxs-lookup"><span data-stu-id="71881-167">You will be prompted to enter the private key password.</span></span> <span data-ttu-id="71881-168">Após a execução bem-sucedida do comando, você verá um **CertFile.cer** e **mykey.pvk** no diretório de certificado especificado.</span><span class="sxs-lookup"><span data-stu-id="71881-168">After the command successfully executes, you should see a **CertFile.cer** and **mykey.pvk** in the certificate directory you specified.</span></span>
2. <span data-ttu-id="71881-169">Use o utilitário [Pvk2Pfx][pvk2pfx] para converter os arquivos .pvk e .cer criados pelo MakeCert em um arquivo .pfx.</span><span class="sxs-lookup"><span data-stu-id="71881-169">Use the [Pvk2Pfx][pvk2pfx] utility to convert the .pvk and .cer files that MakeCert created to a .pfx file.</span></span> <span data-ttu-id="71881-170">Execute o comando a seguir.</span><span class="sxs-lookup"><span data-stu-id="71881-170">Run the following command.</span></span>

        pvk2pfx -pvk mykey.pvk -spc CertFile.cer -pfx CertFile.pfx -po <password>

    <span data-ttu-id="71881-171">Quando receber a solicitação, digite a senha da chave privada especificada anteriormente.</span><span class="sxs-lookup"><span data-stu-id="71881-171">When prompted enter the private key password you specified earlier.</span></span> <span data-ttu-id="71881-172">O valor especificado para o parâmetro **-po** é a senha que está associada ao arquivo .pfx.</span><span class="sxs-lookup"><span data-stu-id="71881-172">The value you specify for the **-po** parameter is the password that is associated with the .pfx file.</span></span> <span data-ttu-id="71881-173">Após a conclusão bem-sucedida do comando, você também verá um arquivo CertFile.pfx no diretório de certificado especificado.</span><span class="sxs-lookup"><span data-stu-id="71881-173">After the command successfully completes, you should also see a CertFile.pfx in the certificate directory you specified.</span></span>

### <a name="create-an-azure-active-directory-and-a-service-principal"></a><span data-ttu-id="71881-174">Criar um Active Directory do Azure e uma entidade de serviço</span><span class="sxs-lookup"><span data-stu-id="71881-174">Create an Azure Active Directory and a service principal</span></span>
<span data-ttu-id="71881-175">Nesta seção, você executará as etapas para criar uma entidade de serviço para um aplicativo do Active Directory do Azure, atribuir uma função à entidade de serviço e autenticar como a entidade de serviço ao fornecer um certificado.</span><span class="sxs-lookup"><span data-stu-id="71881-175">In this section, you perform the steps to create a service principal for an Azure Active Directory application, assign a role to the service principal, and authenticate as the service principal by providing a certificate.</span></span> <span data-ttu-id="71881-176">Execute os seguintes comandos para criar um aplicativo no Active Directory do Azure.</span><span class="sxs-lookup"><span data-stu-id="71881-176">Run the following commands to create an application in Azure Active Directory.</span></span>

1. <span data-ttu-id="71881-177">Cole os seguintes cmdlets na janela do console do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="71881-177">Paste the following cmdlets in the PowerShell console window.</span></span> <span data-ttu-id="71881-178">Verifique se o valor especificado para a propriedade **-DisplayName** é exclusivo.</span><span class="sxs-lookup"><span data-stu-id="71881-178">Make sure the value you specify for the **-DisplayName** property is unique.</span></span> <span data-ttu-id="71881-179">Além disso, os valores para **-HomePage** e **-IdentiferUris** são valores de espaço reservado e não são verificados.</span><span class="sxs-lookup"><span data-stu-id="71881-179">Also, the values for **-HomePage** and **-IdentiferUris** are placeholder values and are not verified.</span></span>

        $certificateFilePath = "$certificateFileDir\CertFile.pfx"

        $password = Read-Host –Prompt "Enter the password" # This is the password you specified for the .pfx file

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
2. <span data-ttu-id="71881-180">Crie uma entidade de serviço usando a ID do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="71881-180">Create a service principal using the application ID.</span></span>

        $servicePrincipal = New-AzureRmADServicePrincipal -ApplicationId $applicationId

        $objectId = $servicePrincipal.Id
3. <span data-ttu-id="71881-181">Conceda acesso à entidade de serviço para a pasta e o arquivo do Data Lake Store que você acessará do cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="71881-181">Grant the service principal access to the Data Lake Store folder and the file that you will access from the HDInsight cluster.</span></span> <span data-ttu-id="71881-182">O trecho a seguir fornece acesso à raiz da conta do Data Lake Store (onde você copiou o arquivo de dados de exemplo) e ao próprio arquivo.</span><span class="sxs-lookup"><span data-stu-id="71881-182">The snippet below provides access to the root of the Data Lake Store account (where you copied the sample data file), and the file itself.</span></span>

        Set-AzureRmDataLakeStoreItemAclEntry -AccountName $dataLakeStoreName -Path / -AceType User -Id $objectId -Permissions All
        Set-AzureRmDataLakeStoreItemAclEntry -AccountName $dataLakeStoreName -Path /vehicle1_09142014.csv -AceType User -Id $objectId -Permissions All

## <a name="create-an-hdinsight-linux-cluster-with-data-lake-store-as-additional-storage"></a><span data-ttu-id="71881-183">Criar um cluster Linux HDInsight com o Data Lake Store como armazenamento adicional</span><span class="sxs-lookup"><span data-stu-id="71881-183">Create an HDInsight Linux cluster with Data Lake Store as additional storage</span></span>

<span data-ttu-id="71881-184">Nesta seção, criamos um cluster Linux Hadoop HDInsight com o Data Lake Store como armazenamento adicional.</span><span class="sxs-lookup"><span data-stu-id="71881-184">In this section, we create an HDInsight Hadoop Linux cluster with Data Lake Store as additional storage.</span></span> <span data-ttu-id="71881-185">Para esta versão, o cluster HDInsight e o Data Lake Store devem estar no mesmo local.</span><span class="sxs-lookup"><span data-stu-id="71881-185">For this release, the HDInsight cluster and the Data Lake Store must be in the same location.</span></span>

1. <span data-ttu-id="71881-186">Comece recuperando a ID do locatário da assinatura.</span><span class="sxs-lookup"><span data-stu-id="71881-186">Start with retrieving the subscription tenant ID.</span></span> <span data-ttu-id="71881-187">Você precisará disso posteriormente.</span><span class="sxs-lookup"><span data-stu-id="71881-187">You will need that later.</span></span>

        $tenantID = (Get-AzureRmContext).Tenant.TenantId
2. <span data-ttu-id="71881-188">Para esta versão, para um cluster Hadoop, o Repositório Data Lake pode ser usado apenas como um armazenamento adicional para o cluster.</span><span class="sxs-lookup"><span data-stu-id="71881-188">For this release, for a Hadoop cluster, Data Lake Store can only be used as an additional storage for the cluster.</span></span> <span data-ttu-id="71881-189">O armazenamento padrão ainda será nos blobs de armazenamento do Azure (WASB).</span><span class="sxs-lookup"><span data-stu-id="71881-189">The default storage will still be the Azure storage blobs (WASB).</span></span> <span data-ttu-id="71881-190">Portanto, vamos criar primeiro a conta de armazenamento e os contêineres de armazenamento exigidos para o cluster.</span><span class="sxs-lookup"><span data-stu-id="71881-190">So, we'll first create the storage account and storage containers required for the cluster.</span></span>

        # Create an Azure storage account
        $location = "East US 2"
        $storageAccountName = "<StorageAcccountName>"   # Provide a Storage account name

        New-AzureRmStorageAccount -ResourceGroupName $resourceGroupName -StorageAccountName $storageAccountName -Location $location -Type Standard_GRS

        # Create an Azure Blob Storage container
        $containerName = "<ContainerName>"              # Provide a container name
        $storageAccountKey = (Get-AzureRmStorageAccountKey -Name $storageAccountName -ResourceGroupName $resourceGroupName)[0].Value
        $destContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey
        New-AzureStorageContainer -Name $containerName -Context $destContext
3. <span data-ttu-id="71881-191">Crie o cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="71881-191">Create the HDInsight cluster.</span></span> <span data-ttu-id="71881-192">Use os seguintes cmdlets.</span><span class="sxs-lookup"><span data-stu-id="71881-192">Use the following cmdlets.</span></span>

        # Set these variables
        $clusterName = $containerName                   # As a best practice, have the same name for the cluster and container
        $clusterNodes = <ClusterSizeInNodes>            # The number of nodes in the HDInsight cluster
        $httpCredentials = Get-Credential
        $sshCredentials = Get-Credential

        New-AzureRmHDInsightCluster -ClusterName $clusterName -ResourceGroupName $resourceGroupName -HttpCredential $httpCredentials -Location $location -DefaultStorageAccountName "$storageAccountName.blob.core.windows.net" -DefaultStorageAccountKey $storageAccountKey -DefaultStorageContainer $containerName  -ClusterSizeInNodes $clusterNodes -ClusterType Hadoop -Version "3.4" -OSType Linux -SshCredential $sshCredentials -ObjectID $objectId -AadTenantId $tenantID -CertificateFilePath $certificateFilePath -CertificatePassword $password

    <span data-ttu-id="71881-193">Após a conclusão do cmdlet, você verá uma saída listando os detalhes do cluster.</span><span class="sxs-lookup"><span data-stu-id="71881-193">After the cmdlet successfully completes, you should see an output listing the cluster details.</span></span>


## <a name="run-test-jobs-on-the-hdinsight-cluster-to-use-the-data-lake-store"></a><span data-ttu-id="71881-194">Executar trabalhos de teste no cluster HDInsight para usar o Repositório Data Lake</span><span class="sxs-lookup"><span data-stu-id="71881-194">Run test jobs on the HDInsight cluster to use the Data Lake Store</span></span>
<span data-ttu-id="71881-195">Após a configuração de um cluster HDInsight, você poderá executar trabalhos de teste no cluster a fim de testar se o cluster HDInsight pode acessar o Repositório Data Lake.</span><span class="sxs-lookup"><span data-stu-id="71881-195">After you have configured an HDInsight cluster, you can run test jobs on the cluster to test that the HDInsight cluster can access Data Lake Store.</span></span> <span data-ttu-id="71881-196">Para fazer isso, executaremos um exemplo de trabalho do Hive que cria uma tabela usando os exemplos de dados que você carregou anteriormente em seu Repositório Data Lake.</span><span class="sxs-lookup"><span data-stu-id="71881-196">To do so, we will run a sample Hive job that creates a table using the sample data that you uploaded earlier to your Data Lake Store.</span></span>

<span data-ttu-id="71881-197">Nesta seção, você acessará o cluster Linux HDInsight criado por você por SSH e executará uma consulta Hive de exemplo.</span><span class="sxs-lookup"><span data-stu-id="71881-197">In this section you will SSH into the HDInsight Linux cluster you created and run the a sample Hive query.</span></span>

* <span data-ttu-id="71881-198">Se você estiver usando um cliente Windows para acessar o cluster por SSH, veja [Usar SSH com Hadoop baseado em Linux no HDInsight do Windows](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).</span><span class="sxs-lookup"><span data-stu-id="71881-198">If you are using a Windows client to SSH into the cluster, see [Use SSH with Linux-based Hadoop on HDInsight from Windows](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).</span></span>
* <span data-ttu-id="71881-199">Se você estiver usando um cliente Linux para acessar o cluster por SSH, veja [Usar SSH com Hadoop baseado em Linux no HDInsight do Linux](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md)</span><span class="sxs-lookup"><span data-stu-id="71881-199">If you are using a Linux client to SSH into the cluster, see [Use SSH with Linux-based Hadoop on HDInsight from Linux](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md)</span></span>

1. <span data-ttu-id="71881-200">Uma vez conectado, inicie a CLI do Hive usando o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="71881-200">Once connected, start the Hive CLI by using the following command:</span></span>

        hive
2. <span data-ttu-id="71881-201">Usando a CLI, insira as instruções a seguir para criar uma nova tabela chamada **vehicles** usando os dados de exemplo no Repositório Data Lake:</span><span class="sxs-lookup"><span data-stu-id="71881-201">Using the CLI, enter the following statements to create a new table named **vehicles** by using the sample data in the Data Lake Store:</span></span>

        DROP TABLE vehicles;
        CREATE EXTERNAL TABLE vehicles (str string) LOCATION 'adl://<mydatalakestore>.azuredatalakestore.net:443/';
        SELECT * FROM vehicles LIMIT 10;

    <span data-ttu-id="71881-202">Você deverá ver um resultado semelhante ao seguinte:</span><span class="sxs-lookup"><span data-stu-id="71881-202">You should see an output similar to the following:</span></span>

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

## <a name="access-data-lake-store-using-hdfs-commands"></a><span data-ttu-id="71881-203">Repositório Data Lake usando comandos do HDFS</span><span class="sxs-lookup"><span data-stu-id="71881-203">Access Data Lake Store using HDFS commands</span></span>
<span data-ttu-id="71881-204">Após a configuração do cluster HDInsight para usar o Repositório Data Lake, você poderá usar os comandos do shell HDFS para acessar o armazenamento.</span><span class="sxs-lookup"><span data-stu-id="71881-204">Once you have configured the HDInsight cluster to use Data Lake Store, you can use the HDFS shell commands to access the store.</span></span>

<span data-ttu-id="71881-205">Nesta seção, você acessará o cluster Linux HDInsight criado por você por SSH e executará os comandos HDFS.</span><span class="sxs-lookup"><span data-stu-id="71881-205">In this section you will SSH into the HDInsight Linux cluster you created and run the HDFS commands.</span></span>

* <span data-ttu-id="71881-206">Se você estiver usando um cliente Windows para acessar o cluster por SSH, veja [Usar SSH com Hadoop baseado em Linux no HDInsight do Windows](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).</span><span class="sxs-lookup"><span data-stu-id="71881-206">If you are using a Windows client to SSH into the cluster, see [Use SSH with Linux-based Hadoop on HDInsight from Windows](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).</span></span>
* <span data-ttu-id="71881-207">Se você estiver usando um cliente Linux para acessar o cluster por SSH, veja [Usar SSH com Hadoop baseado em Linux no HDInsight do Linux](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md)</span><span class="sxs-lookup"><span data-stu-id="71881-207">If you are using a Linux client to SSH into the cluster, see [Use SSH with Linux-based Hadoop on HDInsight from Linux](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md)</span></span>

<span data-ttu-id="71881-208">Uma vez conectado, use o comando do sistema de arquivos HDFS a seguir para listar os arquivos no Repositório Data Lake.</span><span class="sxs-lookup"><span data-stu-id="71881-208">Once connected, use the following HDFS filesystem command to list the files in the Data Lake Store.</span></span>

    hdfs dfs -ls adl://<Data Lake Store account name>.azuredatalakestore.net:443/

<span data-ttu-id="71881-209">Isso deve listar o arquivo carregado anteriormente no Repositório Data Lake.</span><span class="sxs-lookup"><span data-stu-id="71881-209">This should list the file that you uploaded earlier to the Data Lake Store.</span></span>

    15/09/17 21:41:15 INFO web.CaboWebHdfsFileSystem: Replacing original urlConnectionFactory with org.apache.hadoop.hdfs.web.URLConnectionFactory@21a728d6
    Found 1 items
    -rwxrwxrwx   0 NotSupportYet NotSupportYet     671388 2015-09-16 22:16 adl://mydatalakestore.azuredatalakestore.net:443/mynewfolder

<span data-ttu-id="71881-210">Você também pode usar o comando `hdfs dfs -put` para carregar alguns arquivos no Repositório Data Lake e usar `hdfs dfs -ls` para verificar se os arquivos foram carregados com êxito.</span><span class="sxs-lookup"><span data-stu-id="71881-210">You can also use the `hdfs dfs -put` command to upload some files to the Data Lake Store, and then use `hdfs dfs -ls` to verify whether the files were successfully uploaded.</span></span>

## <a name="see-also"></a><span data-ttu-id="71881-211">Consulte também</span><span class="sxs-lookup"><span data-stu-id="71881-211">See Also</span></span>
* [<span data-ttu-id="71881-212">Portal: criar um cluster HDInsight para usar o Repositório Data Lake</span><span class="sxs-lookup"><span data-stu-id="71881-212">Portal: Create an HDInsight cluster to use Data Lake Store</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)

[makecert]: https://msdn.microsoft.com/library/windows/desktop/ff548309(v=vs.85).aspx
[pvk2pfx]: https://msdn.microsoft.com/library/windows/desktop/ff550672(v=vs.85).aspx
