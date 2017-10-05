---
title: "Criar clusters HDInsight com o Data Lake Store como armazenamento padrão usando o PowerShell | Microsoft Docs"
description: Usar o Azure PowerShell para criar e usar clusters HDInsight com o Azure Data Lake Store
services: data-lake-store,hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 8917af15-8e37-46cf-87ad-4e6d5d67ecdb
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/08/2017
ms.author: nitinme
ms.openlocfilehash: 77eb83b80312eca401e6f60d57ed6a5668ea442e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="create-hdinsight-clusters-with-data-lake-store-as-default-storage-by-using-powershell"></a><span data-ttu-id="45766-103">Criar clusters HDInsight com o Data Lake Store como armazenamento padrão usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="45766-103">Create HDInsight clusters with Data Lake Store as default storage by using PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="45766-104">Usar o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="45766-104">Use the Azure portal</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)
> * [<span data-ttu-id="45766-105">Usar o PowerShell (para armazenamento padrão)</span><span class="sxs-lookup"><span data-stu-id="45766-105">Use PowerShell (for default storage)</span></span>](data-lake-store-hdinsight-hadoop-use-powershell-for-default-storage.md)
> * [<span data-ttu-id="45766-106">Usar o PowerShell (para armazenamento adicional)</span><span class="sxs-lookup"><span data-stu-id="45766-106">Use PowerShell (for additional storage)</span></span>](data-lake-store-hdinsight-hadoop-use-powershell.md)
> * [<span data-ttu-id="45766-107">Usar o Resource Manager</span><span class="sxs-lookup"><span data-stu-id="45766-107">Use Resource Manager</span></span>](data-lake-store-hdinsight-hadoop-use-resource-manager-template.md)

<span data-ttu-id="45766-108">Saiba como usar o Azure PowerShell para configurar clusters Azure HDInsight com o Azure Data Lake Store como armazenamento padrão.</span><span class="sxs-lookup"><span data-stu-id="45766-108">Learn how to use Azure PowerShell to configure Azure HDInsight clusters with Azure Data Lake Store, as default storage.</span></span> <span data-ttu-id="45766-109">Para obter instruções sobre como criar um cluster HDInsight com o Data Lake Store como armazenamento adicional, consulte [Criar um cluster HDInsight com o Data Lake Store como armazenamento adicional](data-lake-store-hdinsight-hadoop-use-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="45766-109">For instructions on creating an HDInsight cluster with Data Lake Store as additional storage, see [Create an HDInsight cluster with Data Lake Store as additional storage](data-lake-store-hdinsight-hadoop-use-powershell.md).</span></span>

<span data-ttu-id="45766-110">Aqui estão algumas considerações importantes para usar o HDInsight com o Data Lake Store:</span><span class="sxs-lookup"><span data-stu-id="45766-110">Here are some important considerations for using HDInsight with Data Lake Store:</span></span>

* <span data-ttu-id="45766-111">A opção de criar clusters do HDInsight com acesso ao Data Lake Store como armazenamento padrão está disponível para o HDInsight versões 3.5 e 3.6.</span><span class="sxs-lookup"><span data-stu-id="45766-111">The option to create HDInsight clusters with access to Data Lake Store as default storage is available for HDInsight version 3.5 and 3.6.</span></span>

* <span data-ttu-id="45766-112">A opção para criar clusters HDInsight com acesso ao Data Lake Store como armazenamento padrão *não está disponível* para clusters HDInsight Premium.</span><span class="sxs-lookup"><span data-stu-id="45766-112">The option to create HDInsight clusters with access to Data Lake Store as default storage is *not available* for HDInsight Premium clusters.</span></span>

<span data-ttu-id="45766-113">Para configurar o HDInsight para trabalhar com o Data Lake Store usando o PowerShell, siga as instruções das próximas cinco seções.</span><span class="sxs-lookup"><span data-stu-id="45766-113">To configure HDInsight to work with Data Lake Store by using PowerShell, follow the instructions in the next five sections.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="45766-114">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="45766-114">Prerequisites</span></span>
<span data-ttu-id="45766-115">Antes de começar este tutorial, verifique se você atende aos seguintes requisitos:</span><span class="sxs-lookup"><span data-stu-id="45766-115">Before you begin this tutorial, make sure that you meet the following requirements:</span></span>

* <span data-ttu-id="45766-116">**Uma assinatura do Azure**: acesse [Obter uma avaliação gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="45766-116">**An Azure subscription**: Go to [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="45766-117">**Azure PowerShell 1.0 ou superior**: consulte [Como instalar e configurar o PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="45766-117">**Azure PowerShell 1.0 or greater**: See [How to install and configure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="45766-118">**Software Development Kit do Windows (SDK do Windows)**: para instalar o SDK do Windows, acesse [Downloads e ferramentas para o Windows 10](https://dev.windows.com/en-us/downloads).</span><span class="sxs-lookup"><span data-stu-id="45766-118">**Windows Software Development Kit (SDK)**: To install Windows SDK, go to [Downloads and tools for Windows 10](https://dev.windows.com/en-us/downloads).</span></span> <span data-ttu-id="45766-119">O SDK é usado para criar um certificado de segurança.</span><span class="sxs-lookup"><span data-stu-id="45766-119">The SDK is used to create a security certificate.</span></span>
* <span data-ttu-id="45766-120">**Entidade de serviço do Azure Active Directory**: este tutorial descreve como criar uma entidade de serviço no Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="45766-120">**Azure Active Directory service principal**: This tutorial describes how to create a service principal in Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="45766-121">No entanto, para criar uma entidade de serviço, você deve ser um administrador do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="45766-121">However, to create a service principal, you must be an Azure AD administrator.</span></span> <span data-ttu-id="45766-122">Se você for um administrador, ignore esse pré-requisito e continue com o tutorial.</span><span class="sxs-lookup"><span data-stu-id="45766-122">If you are an administrator, you can skip this prerequisite and proceed with the tutorial.</span></span>

    >[!NOTE]
    ><span data-ttu-id="45766-123">Você poderá criar uma entidade de serviço somente se for um administrador do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="45766-123">You can create a service principal only if you are an Azure AD administrator.</span></span> <span data-ttu-id="45766-124">O administrador do Azure AD deverá criar uma entidade de serviço antes que você possa criar um cluster HDInsight com o Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="45766-124">Your Azure AD administrator must create a service principal before you can create an HDInsight cluster with Data Lake Store.</span></span> <span data-ttu-id="45766-125">A entidade de serviço deve ser criada com um certificado, conforme descrito em [Criar uma entidade de serviço com certificado](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-certificate-from-certificate-authority).</span><span class="sxs-lookup"><span data-stu-id="45766-125">The service principal must be created with a certificate, as described in [Create a service principal with certificate](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-certificate-from-certificate-authority).</span></span>
    >

## <a name="create-a-data-lake-store-account"></a><span data-ttu-id="45766-126">Criar uma conta do Repositório Data Lake</span><span class="sxs-lookup"><span data-stu-id="45766-126">Create a Data Lake Store account</span></span>
<span data-ttu-id="45766-127">Para criar uma conta do Data Lake Store, faça o seguinte:</span><span class="sxs-lookup"><span data-stu-id="45766-127">To create a Data Lake Store account, do the following:</span></span>

1. <span data-ttu-id="45766-128">Na área de trabalho, abra uma janela do PowerShell e insira os trechos abaixo.</span><span class="sxs-lookup"><span data-stu-id="45766-128">From your desktop, open a PowerShell window, and then enter the snippets below.</span></span> <span data-ttu-id="45766-129">Quando receber uma solicitação para se conectar, conecte-se como um dos administradores ou proprietários da assinatura.</span><span class="sxs-lookup"><span data-stu-id="45766-129">When you are prompted to sign in, sign in as one of the subscription administrators or owners.</span></span> 

        # Sign in to your Azure account
        Login-AzureRmAccount

        # List all the subscriptions associated to your account
        Get-AzureRmSubscription

        # Select a subscription
        Set-AzureRmContext -SubscriptionId <subscription ID>

        # Register for Data Lake Store
        Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.DataLakeStore"

    > [!NOTE]
    > <span data-ttu-id="45766-130">Se você registrar o provedor de recursos do Data Lake Store e receber um erro semelhante a `Register-AzureRmResourceProvider : InvalidResourceNamespace: The resource namespace 'Microsoft.DataLakeStore' is invalid`, sua assinatura poderá não ter sido adicionada à lista de permissões do Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="45766-130">If you register the Data Lake Store resource provider and receive an error similar to `Register-AzureRmResourceProvider : InvalidResourceNamespace: The resource namespace 'Microsoft.DataLakeStore' is invalid`, your subscription might not be whitelisted for Data Lake Store.</span></span> <span data-ttu-id="45766-131">Para habilitar sua assinatura do Azure para a visualização pública do Data Lake Store, siga as instruções em [Introdução ao Azure Data Lake Store usando o portal do Azure](data-lake-store-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="45766-131">To enable your Azure subscription for the Data Lake Store public preview, follow the instructions in [Get started with Azure Data Lake Store by using the Azure portal](data-lake-store-get-started-portal.md).</span></span>
    >

2. <span data-ttu-id="45766-132">Uma conta do Data Lake Store está associada a um grupo de recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="45766-132">A Data Lake Store account is associated with an Azure resource group.</span></span> <span data-ttu-id="45766-133">Comece criando um grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="45766-133">Start by creating a resource group.</span></span>

        $resourceGroupName = "<your new resource group name>"
        New-AzureRmResourceGroup -Name $resourceGroupName -Location "East US 2"

    <span data-ttu-id="45766-134">Você verá uma saída semelhante à seguinte:</span><span class="sxs-lookup"><span data-stu-id="45766-134">You should see an output like this:</span></span>

        ResourceGroupName : hdiadlgrp
        Location          : eastus2
        ProvisioningState : Succeeded
        Tags              :
        ResourceId        : /subscriptions/<subscription-id>/resourceGroups/hdiadlgrp

3. <span data-ttu-id="45766-135">Crie uma conta do Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="45766-135">Create a Data Lake Store account.</span></span> <span data-ttu-id="45766-136">O nome de conta especificado deve conter apenas letras minúsculas e números.</span><span class="sxs-lookup"><span data-stu-id="45766-136">The account name you specify must contain only lowercase letters and numbers.</span></span>

        $dataLakeStoreName = "<your new Data Lake Store name>"
        New-AzureRmDataLakeStoreAccount -ResourceGroupName $resourceGroupName -Name $dataLakeStoreName -Location "East US 2"

    <span data-ttu-id="45766-137">Você verá algo semelhante ao mostrado a seguir:</span><span class="sxs-lookup"><span data-stu-id="45766-137">You should see an output like the following:</span></span>

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

4. <span data-ttu-id="45766-138">Usar o Data Lake Store como armazenamento padrão exige a especificação de um caminho raiz para o qual os arquivos específicos ao cluster são copiados durante a criação do cluster.</span><span class="sxs-lookup"><span data-stu-id="45766-138">Using Data Lake Store as default storage requires you to specify a root path to which the cluster-specific files are copied during cluster creation.</span></span> <span data-ttu-id="45766-139">Para criar um caminho raiz, que é **/clusters/hdiadlcluster** no trecho, use os seguintes cmdlets:</span><span class="sxs-lookup"><span data-stu-id="45766-139">To create a root path, which is **/clusters/hdiadlcluster** in the  snippet, use the following cmdlets:</span></span>

        $myrootdir = "/"
        New-AzureRmDataLakeStoreItem -Folder -AccountName $dataLakeStoreName -Path $myrootdir/clusters/hdiadlcluster


## <a name="set-up-authentication-for-role-based-access-to-data-lake-store"></a><span data-ttu-id="45766-140">Configurar a autenticação para acesso baseado em dados ao Repositório Data Lake</span><span class="sxs-lookup"><span data-stu-id="45766-140">Set up authentication for role-based access to Data Lake Store</span></span>
<span data-ttu-id="45766-141">Cada assinatura do Azure está associada a uma entidade do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="45766-141">Every Azure subscription is associated with an Azure AD entity.</span></span> <span data-ttu-id="45766-142">Os usuários e serviços que acessam os recursos da assinatura usando o portal do Azure ou a API do Azure Resource Manager devem primeiro se autenticar no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="45766-142">Users and services that access subscription resources by using the Azure portal or the Azure Resource Manager API must first authenticate with Azure AD.</span></span> <span data-ttu-id="45766-143">O acesso é concedido às assinaturas e serviços do Azure atribuindo a função apropriada para eles em um recurso do Azure.</span><span class="sxs-lookup"><span data-stu-id="45766-143">Access is granted to Azure subscriptions and services by assigning them the appropriate role on an Azure resource.</span></span> <span data-ttu-id="45766-144">Para serviços, uma entidade de serviço identifica o serviço no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="45766-144">For services, a service principal identifies the service in Azure AD.</span></span>

<span data-ttu-id="45766-145">Esta seção ilustra como conceder a um serviço de aplicativo, como o HDInsight, o acesso a um recurso do Azure (a conta do Data Lake Store criada anteriormente).</span><span class="sxs-lookup"><span data-stu-id="45766-145">This section illustrates how to grant an application service, such as HDInsight, access to an Azure resource (the Data Lake Store account that you created earlier).</span></span> <span data-ttu-id="45766-146">Isso é feito pela criação de uma entidade de serviço para o aplicativo e pela atribuição de funções a ela por meio do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="45766-146">You do so by creating a service principal for the application and assigning roles to it via PowerShell.</span></span>

<span data-ttu-id="45766-147">Para configurar a autenticação do Active Directory para o Azure Data Lake, realize as tarefas das próximas duas seções.</span><span class="sxs-lookup"><span data-stu-id="45766-147">To set up Active Directory authentication for Azure Data Lake, perform the tasks in the following two sections.</span></span>

### <a name="create-a-self-signed-certificate"></a><span data-ttu-id="45766-148">Crie um certificado autoassinado</span><span class="sxs-lookup"><span data-stu-id="45766-148">Create a self-signed certificate</span></span>
<span data-ttu-id="45766-149">Verifique se o [SDK do Windows](https://dev.windows.com/en-us/downloads) está instalado antes de continuar com as etapas nesta seção.</span><span class="sxs-lookup"><span data-stu-id="45766-149">Make sure you have [Windows SDK](https://dev.windows.com/en-us/downloads) installed before proceeding with the steps in this section.</span></span> <span data-ttu-id="45766-150">Também é necessário ter criado um diretório, como *C:\mycertdir*, no qual o certificado é criado.</span><span class="sxs-lookup"><span data-stu-id="45766-150">You must have also created a directory, such as *C:\mycertdir*, where you create the certificate.</span></span>

1. <span data-ttu-id="45766-151">Na janela do PowerShell, acesse a localização em que você instalou o SDK do Windows (normalmente, *C:\Program Files (x86)\Windows Kits\10\bin\x86*) e use o utilitário [MakeCert][makecert] para criar um certificado autoassinado e uma chave privada.</span><span class="sxs-lookup"><span data-stu-id="45766-151">From the PowerShell window, go to the location where you installed Windows SDK (typically, *C:\Program Files (x86)\Windows Kits\10\bin\x86*) and use the [MakeCert][makecert] utility to create a self-signed certificate and a private key.</span></span> <span data-ttu-id="45766-152">Use os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="45766-152">Use the following commands:</span></span>

        $certificateFileDir = "<my certificate directory>"
        cd $certificateFileDir

        makecert -sv mykey.pvk -n "cn=HDI-ADL-SP" CertFile.cer -r -len 2048

    <span data-ttu-id="45766-153">Você receberá uma solicitação para inserir a senha da chave privada.</span><span class="sxs-lookup"><span data-stu-id="45766-153">You will be prompted to enter the private key password.</span></span> <span data-ttu-id="45766-154">Após a execução bem-sucedida do comando, você deverá ver **CertFile.cer** e **mykey.pvk** no diretório de certificado especificado.</span><span class="sxs-lookup"><span data-stu-id="45766-154">After the command is successfully executed, you should see **CertFile.cer** and **mykey.pvk** in the certificate directory that you specified.</span></span>
2. <span data-ttu-id="45766-155">Use o utilitário [Pvk2Pfx][pvk2pfx] para converter os arquivos .pvk e .cer criados pelo MakeCert em um arquivo .pfx.</span><span class="sxs-lookup"><span data-stu-id="45766-155">Use the [Pvk2Pfx][pvk2pfx] utility to convert the .pvk and .cer files that MakeCert created to a .pfx file.</span></span> <span data-ttu-id="45766-156">Execute o comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="45766-156">Run the following command:</span></span>

        pvk2pfx -pvk mykey.pvk -spc CertFile.cer -pfx CertFile.pfx -po <password>

    <span data-ttu-id="45766-157">Quando receber a solicitação, insira a senha da chave privada especificada anteriormente.</span><span class="sxs-lookup"><span data-stu-id="45766-157">When you are prompted, enter the private key password that you specified earlier.</span></span> <span data-ttu-id="45766-158">O valor especificado para o parâmetro **-po** é a senha associada ao arquivo .pfx.</span><span class="sxs-lookup"><span data-stu-id="45766-158">The value you specify for the **-po** parameter is the password that's associated with the .pfx file.</span></span> <span data-ttu-id="45766-159">Após a conclusão bem-sucedida do comando, você também deverá ver um arquivo **CertFile.pfx** no diretório de certificado especificado.</span><span class="sxs-lookup"><span data-stu-id="45766-159">After the command has been completed successfully, you should also see a **CertFile.pfx** in the certificate directory that you specified.</span></span>

### <a name="create-an-azure-ad-and-a-service-principal"></a><span data-ttu-id="45766-160">Criar um Azure AD e uma entidade de serviço</span><span class="sxs-lookup"><span data-stu-id="45766-160">Create an Azure AD and a service principal</span></span>
<span data-ttu-id="45766-161">Nesta seção, você cria uma entidade de serviço para um aplicativo do Azure AD, atribui uma função à entidade de serviço e se autentica como a entidade de serviço fornecendo um certificado.</span><span class="sxs-lookup"><span data-stu-id="45766-161">In this section, you create a service principal for an Azure AD application, assign a role to the service principal, and authenticate as the service principal by providing a certificate.</span></span> <span data-ttu-id="45766-162">Para criar um aplicativo no Azure AD, execute os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="45766-162">To create an application in Azure AD, run the following commands:</span></span>

1. <span data-ttu-id="45766-163">Cole os seguintes cmdlets na janela do console do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="45766-163">Paste the following cmdlets in the PowerShell console window.</span></span> <span data-ttu-id="45766-164">Verifique se o valor especificado para a propriedade **-DisplayName** é exclusivo.</span><span class="sxs-lookup"><span data-stu-id="45766-164">Make sure that the value you specify for the **-DisplayName** property is unique.</span></span> <span data-ttu-id="45766-165">Os valores de **-HomePage** e **-IdentiferUris** são valores de espaço reservado e não são verificados.</span><span class="sxs-lookup"><span data-stu-id="45766-165">The values for **-HomePage** and **-IdentiferUris** are placeholder values and are not verified.</span></span>

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
2. <span data-ttu-id="45766-166">Crie uma entidade de serviço usando a ID do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="45766-166">Create a service principal by using the application ID.</span></span>

        $servicePrincipal = New-AzureRmADServicePrincipal -ApplicationId $applicationId

        $objectId = $servicePrincipal.Id
3. <span data-ttu-id="45766-167">Conceda acesso à raiz do Data Lake Store e a todas as pastas no caminho raiz especificado anteriormente à entidade de serviço.</span><span class="sxs-lookup"><span data-stu-id="45766-167">Grant the service principal access to the Data Lake Store root and all the folders in the root path that you specified earlier.</span></span> <span data-ttu-id="45766-168">Use os seguintes cmdlets:</span><span class="sxs-lookup"><span data-stu-id="45766-168">Use the following cmdlets:</span></span>

        Set-AzureRmDataLakeStoreItemAclEntry -AccountName $dataLakeStoreName -Path / -AceType User -Id $objectId -Permissions All
        Set-AzureRmDataLakeStoreItemAclEntry -AccountName $dataLakeStoreName -Path /clusters -AceType User -Id $objectId -Permissions All
        Set-AzureRmDataLakeStoreItemAclEntry -AccountName $dataLakeStoreName -Path /clusters/hdiadlcluster -AceType User -Id $objectId -Permissions All

## <a name="create-an-hdinsight-linux-cluster-with-data-lake-store-as-the-default-storage"></a><span data-ttu-id="45766-169">Criar um cluster Linux HDInsight com o Data Lake Store como o armazenamento padrão</span><span class="sxs-lookup"><span data-stu-id="45766-169">Create an HDInsight Linux cluster with Data Lake Store as the default storage</span></span>

<span data-ttu-id="45766-170">Nesta seção, você cria um cluster Linux Hadoop HDInsight com o Data Lake Store como o armazenamento padrão.</span><span class="sxs-lookup"><span data-stu-id="45766-170">In this section, you create an HDInsight Hadoop Linux cluster with Data Lake Store as the default storage.</span></span> <span data-ttu-id="45766-171">Para esta versão, o cluster HDInsight e o Data Lake Store devem estar na mesma localização.</span><span class="sxs-lookup"><span data-stu-id="45766-171">For this release, the HDInsight cluster and Data Lake Store must be in the same location.</span></span>

1. <span data-ttu-id="45766-172">Recupere a ID de locatário da assinatura e armazene-a para uso futuro.</span><span class="sxs-lookup"><span data-stu-id="45766-172">Retrieve the subscription tenant ID, and store it to use later.</span></span>

        $tenantID = (Get-AzureRmContext).Tenant.TenantId

2. <span data-ttu-id="45766-173">Crie o cluster HDInsight usando os seguintes cmdlets:</span><span class="sxs-lookup"><span data-stu-id="45766-173">Create the HDInsight cluster by using the following cmdlets:</span></span>

        # Set these variables

        $location = "East US 2"
        $storageAccountName = $dataLakeStoreName                       # Data Lake Store account name
        $storageRootPath = "<Storage root path you specified earlier>" # E.g. /clusters/hdiadlcluster
        $clusterName = "<unique cluster name>"
        $clusterNodes = <ClusterSizeInNodes>            # The number of nodes in the HDInsight cluster
        $httpCredentials = Get-Credential
        $sshCredentials = Get-Credential

        New-AzureRmHDInsightCluster `
               -ClusterType Hadoop `
               -OSType Linux `
               -ClusterSizeInNodes $clusterNodes `
               -ResourceGroupName $resourceGroupName `
               -ClusterName $clusterName `
               -HttpCredential $httpCredentials `
               -Location $location `
               -DefaultStorageAccountType AzureDataLakeStore `
               -DefaultStorageAccountName "$storageAccountName.azuredatalakestore.net" `
               -DefaultStorageRootPath $storageRootPath `
               -Version "3.6" `
               -SshCredential $sshCredentials `
               -AadTenantId $tenantId `
               -ObjectId $objectId `
               -CertificateFilePath $certificateFilePath `
               -CertificatePassword $password

    <span data-ttu-id="45766-174">Após a conclusão bem-sucedida do cmdlet, você deverá ver uma saída que lista os detalhes do cluster.</span><span class="sxs-lookup"><span data-stu-id="45766-174">After the cmdlet has been successfully completed, you should see an output that lists the cluster details.</span></span>

## <a name="run-test-jobs-on-the-hdinsight-cluster-to-use-data-lake-store"></a><span data-ttu-id="45766-175">Executar trabalhos de teste no cluster HDInsight para usar o Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="45766-175">Run test jobs on the HDInsight cluster to use Data Lake Store</span></span>
<span data-ttu-id="45766-176">Depois de configurar um cluster HDInsight, é possível executar trabalhos de teste nele para garantir que ele pode acessar o Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="45766-176">After you have configured an HDInsight cluster, you can run test jobs on it to ensure that it can access Data Lake Store.</span></span> <span data-ttu-id="45766-177">Para fazer isso, execute um trabalho do Hive de exemplo para criar uma tabela que usa os dados de exemplo que já estão disponíveis no Data Lake Store em *<cluster root>/example/data/sample.log*.</span><span class="sxs-lookup"><span data-stu-id="45766-177">To do so, run a sample Hive job to create a table that uses the sample data that's already available in Data Lake Store at *<cluster root>/example/data/sample.log*.</span></span>

<span data-ttu-id="45766-178">Nesta seção, você estabelece uma conexão SSH (Secure Shell) com o cluster Linux HDInsight criado e, em seguida, executa uma consulta do Hive de exemplo.</span><span class="sxs-lookup"><span data-stu-id="45766-178">In this section, you make a Secure Shell (SSH) connection into the HDInsight Linux cluster that you created, and then you run a sample Hive query.</span></span>

* <span data-ttu-id="45766-179">Se estiver usando um cliente do Windows para estabelecer uma conexão SSH com o cluster, consulte [Usar o SSH com o Hadoop baseado em Linux no HDInsight por meio do Windows](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).</span><span class="sxs-lookup"><span data-stu-id="45766-179">If you are using a Windows client to make an SSH connection into the cluster, see [Use SSH with Linux-based Hadoop on HDInsight from Windows](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).</span></span>
* <span data-ttu-id="45766-180">Se estiver usando um cliente do Linux para estabelecer uma conexão SSH com o cluster, consulte [Usar o SSH com o Hadoop baseado em Linux no HDInsight por meio do Linux](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="45766-180">If you are using a Linux client to make an SSH connection into the cluster, see [Use SSH with Linux-based Hadoop on HDInsight from Linux](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

1. <span data-ttu-id="45766-181">Depois de estabelecer a conexão, inicie a CLI (interface de linha de comando) do Hive usando o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="45766-181">After you have made the connection, start the Hive command-line interface (CLI) by using the following command:</span></span>

        hive
2. <span data-ttu-id="45766-182">Use a CLI para inserir as seguintes instruções para criar uma nova tabela chamada **vehicles** usando os dados de exemplo do Data Lake Store:</span><span class="sxs-lookup"><span data-stu-id="45766-182">Use the CLI to enter the following statements to create a new table named **vehicles** by using the sample data in Data Lake Store:</span></span>

        DROP TABLE log4jLogs;
        CREATE EXTERNAL TABLE log4jLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
        ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
        STORED AS TEXTFILE LOCATION 'adl:///example/data/';
        SELECT t4 AS sev, COUNT(*) AS count FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log' GROUP BY t4;

    <span data-ttu-id="45766-183">Você deve ver a saída da consulta no console do SSH.</span><span class="sxs-lookup"><span data-stu-id="45766-183">You should see the query output on the SSH console.</span></span>

    >[!NOTE]
    ><span data-ttu-id="45766-184">O caminho para os dados de exemplo no comando CREATE TABLE anterior é `adl:///example/data/`, em que `adl:///` é a raiz do cluster.</span><span class="sxs-lookup"><span data-stu-id="45766-184">The path to the sample data in the preceding CREATE TABLE command is `adl:///example/data/`, where `adl:///` is the cluster root.</span></span> <span data-ttu-id="45766-185">Seguindo o exemplo da raiz do cluster especificada neste tutorial, o comando é `adl://hdiadlstore.azuredatalakestore.net/clusters/hdiadlcluster`.</span><span class="sxs-lookup"><span data-stu-id="45766-185">Following the example of the cluster root that's specified in this tutorial, the command is `adl://hdiadlstore.azuredatalakestore.net/clusters/hdiadlcluster`.</span></span> <span data-ttu-id="45766-186">É possível usar a alternativa mais curta ou fornecer o caminho completo para a raiz do cluster.</span><span class="sxs-lookup"><span data-stu-id="45766-186">You can either use the shorter alternative or provide the complete path to the cluster root.</span></span>
    >

## <a name="access-data-lake-store-by-using-hdfs-commands"></a><span data-ttu-id="45766-187">Acessar o Data Lake Store usando comandos do HDFS</span><span class="sxs-lookup"><span data-stu-id="45766-187">Access Data Lake Store by using HDFS commands</span></span>
<span data-ttu-id="45766-188">Depois de configurar o cluster HDInsight para usar o Data Lake Store, você poderá usar os comandos do shell do HDFS (Sistema de Arquivos Distribuído Hadoop) para acessar o repositório.</span><span class="sxs-lookup"><span data-stu-id="45766-188">After you have configured the HDInsight cluster to use Data Lake Store, you can use Hadoop Distributed File System (HDFS) shell commands to access the store.</span></span>

<span data-ttu-id="45766-189">Nesta seção, você estabelece uma conexão SSH com o cluster Linux HDInsight criado e, em seguida, executa os comandos do HDFS.</span><span class="sxs-lookup"><span data-stu-id="45766-189">In this section, you make an SSH connection into the HDInsight Linux cluster that you created, and then you run the HDFS commands.</span></span>

* <span data-ttu-id="45766-190">Se estiver usando um cliente do Windows para estabelecer uma conexão SSH com o cluster, consulte [Usar o SSH com o Hadoop baseado em Linux no HDInsight por meio do Windows](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).</span><span class="sxs-lookup"><span data-stu-id="45766-190">If you are using a Windows client to make an SSH connection into the cluster, see [Use SSH with Linux-based Hadoop on HDInsight from Windows](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).</span></span>
* <span data-ttu-id="45766-191">Se estiver usando um cliente do Linux para estabelecer uma conexão SSH com o cluster, consulte [Usar o SSH com o Hadoop baseado em Linux no HDInsight por meio do Linux](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="45766-191">If you are using a Linux client to make an SSH connection into the cluster, see [Use SSH with Linux-based Hadoop on HDInsight from Linux](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

<span data-ttu-id="45766-192">Depois de estabelecer a conexão, liste os arquivos do Data Lake Store usando o comando do sistema de arquivos HDFS a seguir.</span><span class="sxs-lookup"><span data-stu-id="45766-192">After you've made the connection, list the files in Data Lake Store by using the following HDFS file system command.</span></span>

    hdfs dfs -ls adl:///

<span data-ttu-id="45766-193">Também é possível usar o comando `hdfs dfs -put` para carregar alguns arquivos no Data Lake Store e, em seguida, usar `hdfs dfs -ls` para verificar se os arquivos foram carregados com êxito.</span><span class="sxs-lookup"><span data-stu-id="45766-193">You can also use the `hdfs dfs -put` command to upload some files to Data Lake Store, and then use `hdfs dfs -ls` to verify whether the files were successfully uploaded.</span></span>

## <a name="see-also"></a><span data-ttu-id="45766-194">Consulte também</span><span class="sxs-lookup"><span data-stu-id="45766-194">See also</span></span>
* [<span data-ttu-id="45766-195">Portal do Azure: Criar um cluster HDInsight para usar o Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="45766-195">Azure portal: Create an HDInsight cluster to use Data Lake Store</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)

[makecert]: https://msdn.microsoft.com/library/windows/desktop/ff548309(v=vs.85).aspx
[pvk2pfx]: https://msdn.microsoft.com/library/windows/desktop/ff550672(v=vs.85).aspx
