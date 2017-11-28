---
title: "aaaCreate HDInsight clusters com repositório Data Lake como armazenamento padrão usando o PowerShell | Microsoft Docs"
description: "Usar o Azure PowerShell toocreate e usar clusters de HDInsight com repositório Azure Data Lake"
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
ms.openlocfilehash: a5c0ad416da6ad9bd07204af2ebb6b7470916085
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-hdinsight-clusters-with-data-lake-store-as-default-storage-by-using-powershell"></a><span data-ttu-id="04e30-103">Criar clusters HDInsight com o Data Lake Store como armazenamento padrão usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="04e30-103">Create HDInsight clusters with Data Lake Store as default storage by using PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="04e30-104">Use Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="04e30-104">Use hello Azure portal</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)
> * [<span data-ttu-id="04e30-105">Usar o PowerShell (para armazenamento padrão)</span><span class="sxs-lookup"><span data-stu-id="04e30-105">Use PowerShell (for default storage)</span></span>](data-lake-store-hdinsight-hadoop-use-powershell-for-default-storage.md)
> * [<span data-ttu-id="04e30-106">Usar o PowerShell (para armazenamento adicional)</span><span class="sxs-lookup"><span data-stu-id="04e30-106">Use PowerShell (for additional storage)</span></span>](data-lake-store-hdinsight-hadoop-use-powershell.md)
> * [<span data-ttu-id="04e30-107">Usar o Resource Manager</span><span class="sxs-lookup"><span data-stu-id="04e30-107">Use Resource Manager</span></span>](data-lake-store-hdinsight-hadoop-use-resource-manager-template.md)

<span data-ttu-id="04e30-108">Saiba como clusters de toouse tooconfigure de PowerShell do Azure HDInsight do Azure com repositório Azure Data Lake, como o armazenamento padrão.</span><span class="sxs-lookup"><span data-stu-id="04e30-108">Learn how toouse Azure PowerShell tooconfigure Azure HDInsight clusters with Azure Data Lake Store, as default storage.</span></span> <span data-ttu-id="04e30-109">Para obter instruções sobre como criar um cluster HDInsight com o Data Lake Store como armazenamento adicional, consulte [Criar um cluster HDInsight com o Data Lake Store como armazenamento adicional](data-lake-store-hdinsight-hadoop-use-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="04e30-109">For instructions on creating an HDInsight cluster with Data Lake Store as additional storage, see [Create an HDInsight cluster with Data Lake Store as additional storage](data-lake-store-hdinsight-hadoop-use-powershell.md).</span></span>

<span data-ttu-id="04e30-110">Aqui estão algumas considerações importantes para usar o HDInsight com o Data Lake Store:</span><span class="sxs-lookup"><span data-stu-id="04e30-110">Here are some important considerations for using HDInsight with Data Lake Store:</span></span>

* <span data-ttu-id="04e30-111">clusters de HDInsight do Hello opção toocreate com acesso tooData Lake repositório como armazenamento padrão está disponível para HDInsight versão 3.5 e 3.6.</span><span class="sxs-lookup"><span data-stu-id="04e30-111">hello option toocreate HDInsight clusters with access tooData Lake Store as default storage is available for HDInsight version 3.5 and 3.6.</span></span>

* <span data-ttu-id="04e30-112">Olá opção toocreate clusters de HDInsight com acesso tooData Lake repositório como o armazenamento padrão é *não disponível* para clusters de HDInsight Premium.</span><span class="sxs-lookup"><span data-stu-id="04e30-112">hello option toocreate HDInsight clusters with access tooData Lake Store as default storage is *not available* for HDInsight Premium clusters.</span></span>

<span data-ttu-id="04e30-113">tooconfigure toowork de HDInsight com repositório Data Lake usando o PowerShell, siga as instruções de saudação nas seções de cinco hello.</span><span class="sxs-lookup"><span data-stu-id="04e30-113">tooconfigure HDInsight toowork with Data Lake Store by using PowerShell, follow hello instructions in hello next five sections.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="04e30-114">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="04e30-114">Prerequisites</span></span>
<span data-ttu-id="04e30-115">Antes de começar este tutorial, certifique-se de atender Olá requisitos a seguir:</span><span class="sxs-lookup"><span data-stu-id="04e30-115">Before you begin this tutorial, make sure that you meet hello following requirements:</span></span>

* <span data-ttu-id="04e30-116">**Uma assinatura do Azure**: ir muito[avaliação gratuita do Azure obter](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="04e30-116">**An Azure subscription**: Go too[Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="04e30-117">**O Azure PowerShell 1.0 ou maior**: consulte [como tooinstall e configurar o PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="04e30-117">**Azure PowerShell 1.0 or greater**: See [How tooinstall and configure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="04e30-118">**Windows Software Development Kit (SDK)**: tooinstall SDK do Windows, vá muito[Downloads e ferramentas para Windows 10](https://dev.windows.com/en-us/downloads).</span><span class="sxs-lookup"><span data-stu-id="04e30-118">**Windows Software Development Kit (SDK)**: tooinstall Windows SDK, go too[Downloads and tools for Windows 10](https://dev.windows.com/en-us/downloads).</span></span> <span data-ttu-id="04e30-119">Olá SDK é toocreate usado um certificado de segurança.</span><span class="sxs-lookup"><span data-stu-id="04e30-119">hello SDK is used toocreate a security certificate.</span></span>
* <span data-ttu-id="04e30-120">**Entidade de serviço do Active Directory do Azure**: Este tutorial descreve como toocreate uma entidade de serviço no Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="04e30-120">**Azure Active Directory service principal**: This tutorial describes how toocreate a service principal in Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="04e30-121">No entanto, toocreate uma entidade de serviço, você deve ser um administrador do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="04e30-121">However, toocreate a service principal, you must be an Azure AD administrator.</span></span> <span data-ttu-id="04e30-122">Se você for um administrador, você pode ignorar esse pré-requisito e continuar com o tutorial hello.</span><span class="sxs-lookup"><span data-stu-id="04e30-122">If you are an administrator, you can skip this prerequisite and proceed with hello tutorial.</span></span>

    >[!NOTE]
    ><span data-ttu-id="04e30-123">Você poderá criar uma entidade de serviço somente se for um administrador do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="04e30-123">You can create a service principal only if you are an Azure AD administrator.</span></span> <span data-ttu-id="04e30-124">O administrador do Azure AD deverá criar uma entidade de serviço antes que você possa criar um cluster HDInsight com o Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="04e30-124">Your Azure AD administrator must create a service principal before you can create an HDInsight cluster with Data Lake Store.</span></span> <span data-ttu-id="04e30-125">Olá entidade de serviço deve ser criada com um certificado, conforme descrito em [criar uma entidade de serviço com certificado](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-certificate-from-certificate-authority).</span><span class="sxs-lookup"><span data-stu-id="04e30-125">hello service principal must be created with a certificate, as described in [Create a service principal with certificate](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-certificate-from-certificate-authority).</span></span>
    >

## <a name="create-a-data-lake-store-account"></a><span data-ttu-id="04e30-126">Criar uma conta do Repositório Data Lake</span><span class="sxs-lookup"><span data-stu-id="04e30-126">Create a Data Lake Store account</span></span>
<span data-ttu-id="04e30-127">toocreate uma conta do repositório Data Lake, Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="04e30-127">toocreate a Data Lake Store account, do hello following:</span></span>

1. <span data-ttu-id="04e30-128">Na área de trabalho, abra uma janela do PowerShell e, em seguida, inserir trechos de código Olá abaixo.</span><span class="sxs-lookup"><span data-stu-id="04e30-128">From your desktop, open a PowerShell window, and then enter hello snippets below.</span></span> <span data-ttu-id="04e30-129">Quando você estiver toosign solicitada na entrada como um dos administradores de assinatura de saudação ou proprietários.</span><span class="sxs-lookup"><span data-stu-id="04e30-129">When you are prompted toosign in, sign in as one of hello subscription administrators or owners.</span></span> 

        # Sign in tooyour Azure account
        Login-AzureRmAccount

        # List all hello subscriptions associated tooyour account
        Get-AzureRmSubscription

        # Select a subscription
        Set-AzureRmContext -SubscriptionId <subscription ID>

        # Register for Data Lake Store
        Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.DataLakeStore"

    > [!NOTE]
    > <span data-ttu-id="04e30-130">Se você registrar o provedor de recursos do repositório Data Lake hello e receber um erro semelhante muito`Register-AzureRmResourceProvider : InvalidResourceNamespace: hello resource namespace 'Microsoft.DataLakeStore' is invalid`, sua assinatura não pode estar na lista de permissões para o repositório Data Lake.</span><span class="sxs-lookup"><span data-stu-id="04e30-130">If you register hello Data Lake Store resource provider and receive an error similar too`Register-AzureRmResourceProvider : InvalidResourceNamespace: hello resource namespace 'Microsoft.DataLakeStore' is invalid`, your subscription might not be whitelisted for Data Lake Store.</span></span> <span data-ttu-id="04e30-131">tooenable a sua assinatura do Azure para a visualização pública do repositório Data Lake hello, siga instruções Olá [Introdução ao repositório Azure Data Lake usando o portal do Azure de saudação](data-lake-store-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="04e30-131">tooenable your Azure subscription for hello Data Lake Store public preview, follow hello instructions in [Get started with Azure Data Lake Store by using hello Azure portal](data-lake-store-get-started-portal.md).</span></span>
    >

2. <span data-ttu-id="04e30-132">Uma conta do Data Lake Store está associada a um grupo de recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="04e30-132">A Data Lake Store account is associated with an Azure resource group.</span></span> <span data-ttu-id="04e30-133">Comece criando um grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="04e30-133">Start by creating a resource group.</span></span>

        $resourceGroupName = "<your new resource group name>"
        New-AzureRmResourceGroup -Name $resourceGroupName -Location "East US 2"

    <span data-ttu-id="04e30-134">Você verá uma saída semelhante à seguinte:</span><span class="sxs-lookup"><span data-stu-id="04e30-134">You should see an output like this:</span></span>

        ResourceGroupName : hdiadlgrp
        Location          : eastus2
        ProvisioningState : Succeeded
        Tags              :
        ResourceId        : /subscriptions/<subscription-id>/resourceGroups/hdiadlgrp

3. <span data-ttu-id="04e30-135">Crie uma conta do Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="04e30-135">Create a Data Lake Store account.</span></span> <span data-ttu-id="04e30-136">conta de saudação nome que você especificar deve conter somente letras minúsculas e números.</span><span class="sxs-lookup"><span data-stu-id="04e30-136">hello account name you specify must contain only lowercase letters and numbers.</span></span>

        $dataLakeStoreName = "<your new Data Lake Store name>"
        New-AzureRmDataLakeStoreAccount -ResourceGroupName $resourceGroupName -Name $dataLakeStoreName -Location "East US 2"

    <span data-ttu-id="04e30-137">Você verá uma saída semelhante Olá seguinte:</span><span class="sxs-lookup"><span data-stu-id="04e30-137">You should see an output like hello following:</span></span>

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

4. <span data-ttu-id="04e30-138">O uso do repositório Data Lake como armazenamento padrão requer toospecify que um arquivos de específicas do cluster raiz caminho toowhich Olá são copiados durante a criação do cluster.</span><span class="sxs-lookup"><span data-stu-id="04e30-138">Using Data Lake Store as default storage requires you toospecify a root path toowhich hello cluster-specific files are copied during cluster creation.</span></span> <span data-ttu-id="04e30-139">toocreate um caminho raiz, que é **clusters/hdiadlcluster** no trecho hello, use Olá cmdlets a seguir:</span><span class="sxs-lookup"><span data-stu-id="04e30-139">toocreate a root path, which is **/clusters/hdiadlcluster** in hello  snippet, use hello following cmdlets:</span></span>

        $myrootdir = "/"
        New-AzureRmDataLakeStoreItem -Folder -AccountName $dataLakeStoreName -Path $myrootdir/clusters/hdiadlcluster


## <a name="set-up-authentication-for-role-based-access-toodata-lake-store"></a><span data-ttu-id="04e30-140">Configurar a autenticação para baseado em função acessar o repositório de Lake tooData</span><span class="sxs-lookup"><span data-stu-id="04e30-140">Set up authentication for role-based access tooData Lake Store</span></span>
<span data-ttu-id="04e30-141">Cada assinatura do Azure está associada a uma entidade do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="04e30-141">Every Azure subscription is associated with an Azure AD entity.</span></span> <span data-ttu-id="04e30-142">Usuários e serviços que os recursos de assinatura de acesso usando Olá portal do Azure ou Olá API do Gerenciador de recursos do Azure devem primeiro autenticar com o AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="04e30-142">Users and services that access subscription resources by using hello Azure portal or hello Azure Resource Manager API must first authenticate with Azure AD.</span></span> <span data-ttu-id="04e30-143">Acesso tooAzure assinaturas e serviços, atribuindo-lhes a função apropriada de saudação em um recurso do Azure.</span><span class="sxs-lookup"><span data-stu-id="04e30-143">Access is granted tooAzure subscriptions and services by assigning them hello appropriate role on an Azure resource.</span></span> <span data-ttu-id="04e30-144">Para serviços, uma entidade de serviço identifica o serviço Olá no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="04e30-144">For services, a service principal identifies hello service in Azure AD.</span></span>

<span data-ttu-id="04e30-145">Esta seção ilustra como toogrant um aplicativo de serviço, como HDInsight, tooan de acesso a recursos do Azure (Olá conta do repositório Data Lake que você criou anteriormente).</span><span class="sxs-lookup"><span data-stu-id="04e30-145">This section illustrates how toogrant an application service, such as HDInsight, access tooan Azure resource (hello Data Lake Store account that you created earlier).</span></span> <span data-ttu-id="04e30-146">Você pode fazer isso criando um serviço principal para o aplicativo hello e atribuindo funções tooit por meio do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="04e30-146">You do so by creating a service principal for hello application and assigning roles tooit via PowerShell.</span></span>

<span data-ttu-id="04e30-147">tooset a autenticação do Active Directory para o Azure Data Lake, execute tarefas de Olá Olá duas seções a seguir.</span><span class="sxs-lookup"><span data-stu-id="04e30-147">tooset up Active Directory authentication for Azure Data Lake, perform hello tasks in hello following two sections.</span></span>

### <a name="create-a-self-signed-certificate"></a><span data-ttu-id="04e30-148">Crie um certificado autoassinado</span><span class="sxs-lookup"><span data-stu-id="04e30-148">Create a self-signed certificate</span></span>
<span data-ttu-id="04e30-149">Verifique se você tem [SDK do Windows](https://dev.windows.com/en-us/downloads) instalado antes de prosseguir com a saudação as etapas nesta seção.</span><span class="sxs-lookup"><span data-stu-id="04e30-149">Make sure you have [Windows SDK](https://dev.windows.com/en-us/downloads) installed before proceeding with hello steps in this section.</span></span> <span data-ttu-id="04e30-150">Você deve também criou um diretório, como *C:\mycertdir*, em que você criar o certificado de saudação.</span><span class="sxs-lookup"><span data-stu-id="04e30-150">You must have also created a directory, such as *C:\mycertdir*, where you create hello certificate.</span></span>

1. <span data-ttu-id="04e30-151">Na janela do PowerShell Olá, vá toohello local onde você instalou o SDK do Windows (normalmente, *C:\Program Files (x86) \Windows Kits\10\bin\x86*) e usar o hello [MakeCert] [ makecert] toocreate utilitário um certificado autoassinado e uma chave privada.</span><span class="sxs-lookup"><span data-stu-id="04e30-151">From hello PowerShell window, go toohello location where you installed Windows SDK (typically, *C:\Program Files (x86)\Windows Kits\10\bin\x86*) and use hello [MakeCert][makecert] utility toocreate a self-signed certificate and a private key.</span></span> <span data-ttu-id="04e30-152">Use Olá comandos a seguir:</span><span class="sxs-lookup"><span data-stu-id="04e30-152">Use hello following commands:</span></span>

        $certificateFileDir = "<my certificate directory>"
        cd $certificateFileDir

        makecert -sv mykey.pvk -n "cn=HDI-ADL-SP" CertFile.cer -r -len 2048

    <span data-ttu-id="04e30-153">Será a senha da chave privada tooenter solicitadas hello.</span><span class="sxs-lookup"><span data-stu-id="04e30-153">You will be prompted tooenter hello private key password.</span></span> <span data-ttu-id="04e30-154">Depois que o comando Olá é executado com êxito, você deverá ver **CertFile.cer** e **mykey.pvk** Olá certificado no diretório em que você especificou.</span><span class="sxs-lookup"><span data-stu-id="04e30-154">After hello command is successfully executed, you should see **CertFile.cer** and **mykey.pvk** in hello certificate directory that you specified.</span></span>
2. <span data-ttu-id="04e30-155">Saudação de uso [Pvk2Pfx] [ pvk2pfx] . pvk do utilitário tooconvert hello e. cer arquivos de arquivo. pfx criado tooa MakeCert.</span><span class="sxs-lookup"><span data-stu-id="04e30-155">Use hello [Pvk2Pfx][pvk2pfx] utility tooconvert hello .pvk and .cer files that MakeCert created tooa .pfx file.</span></span> <span data-ttu-id="04e30-156">Execute Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="04e30-156">Run hello following command:</span></span>

        pvk2pfx -pvk mykey.pvk -spc CertFile.cer -pfx CertFile.pfx -po <password>

    <span data-ttu-id="04e30-157">Quando for solicitado, digite Olá senha da chave privada que você especificou anteriormente.</span><span class="sxs-lookup"><span data-stu-id="04e30-157">When you are prompted, enter hello private key password that you specified earlier.</span></span> <span data-ttu-id="04e30-158">Olá valor especificado para Olá **-po** parâmetro é a senha de saudação que está associado ao arquivo. pfx de saudação.</span><span class="sxs-lookup"><span data-stu-id="04e30-158">hello value you specify for hello **-po** parameter is hello password that's associated with hello .pfx file.</span></span> <span data-ttu-id="04e30-159">Depois que o comando Olá foi concluído com êxito, você também deverá ver um **CertFile.pfx** Olá certificado no diretório em que você especificou.</span><span class="sxs-lookup"><span data-stu-id="04e30-159">After hello command has been completed successfully, you should also see a **CertFile.pfx** in hello certificate directory that you specified.</span></span>

### <a name="create-an-azure-ad-and-a-service-principal"></a><span data-ttu-id="04e30-160">Criar um Azure AD e uma entidade de serviço</span><span class="sxs-lookup"><span data-stu-id="04e30-160">Create an Azure AD and a service principal</span></span>
<span data-ttu-id="04e30-161">Nesta seção, criar uma entidade de serviço para um aplicativo do AD do Azure, atribua uma entidade de serviço de toohello de função e autenticar como entidade de serviço hello, fornecendo um certificado.</span><span class="sxs-lookup"><span data-stu-id="04e30-161">In this section, you create a service principal for an Azure AD application, assign a role toohello service principal, and authenticate as hello service principal by providing a certificate.</span></span> <span data-ttu-id="04e30-162">toocreate um aplicativo no AD do Azure, execute Olá comandos a seguir:</span><span class="sxs-lookup"><span data-stu-id="04e30-162">toocreate an application in Azure AD, run hello following commands:</span></span>

1. <span data-ttu-id="04e30-163">Colar Olá cmdlets na janela de console do PowerShell Olá a seguir.</span><span class="sxs-lookup"><span data-stu-id="04e30-163">Paste hello following cmdlets in hello PowerShell console window.</span></span> <span data-ttu-id="04e30-164">Verifique se esse valor Olá você especificar para Olá **- DisplayName** propriedade é exclusiva.</span><span class="sxs-lookup"><span data-stu-id="04e30-164">Make sure that hello value you specify for hello **-DisplayName** property is unique.</span></span> <span data-ttu-id="04e30-165">Olá valores para **- home page** e **- IdentiferUris** são valores de espaço reservado e não são verificadas.</span><span class="sxs-lookup"><span data-stu-id="04e30-165">hello values for **-HomePage** and **-IdentiferUris** are placeholder values and are not verified.</span></span>

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
2. <span data-ttu-id="04e30-166">Criar uma entidade de serviço usando a ID do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="04e30-166">Create a service principal by using hello application ID.</span></span>

        $servicePrincipal = New-AzureRmADServicePrincipal -ApplicationId $applicationId

        $objectId = $servicePrincipal.Id
3. <span data-ttu-id="04e30-167">Conceda Olá serviço acesso principal toohello repositório Data Lake pastas raiz e todos os Olá no caminho de raiz de saudação que você especificou anteriormente.</span><span class="sxs-lookup"><span data-stu-id="04e30-167">Grant hello service principal access toohello Data Lake Store root and all hello folders in hello root path that you specified earlier.</span></span> <span data-ttu-id="04e30-168">Use Olá cmdlets a seguir:</span><span class="sxs-lookup"><span data-stu-id="04e30-168">Use hello following cmdlets:</span></span>

        Set-AzureRmDataLakeStoreItemAclEntry -AccountName $dataLakeStoreName -Path / -AceType User -Id $objectId -Permissions All
        Set-AzureRmDataLakeStoreItemAclEntry -AccountName $dataLakeStoreName -Path /clusters -AceType User -Id $objectId -Permissions All
        Set-AzureRmDataLakeStoreItemAclEntry -AccountName $dataLakeStoreName -Path /clusters/hdiadlcluster -AceType User -Id $objectId -Permissions All

## <a name="create-an-hdinsight-linux-cluster-with-data-lake-store-as-hello-default-storage"></a><span data-ttu-id="04e30-169">Criar um cluster HDInsight Linux com repositório Data Lake como armazenamento de padrão de saudação</span><span class="sxs-lookup"><span data-stu-id="04e30-169">Create an HDInsight Linux cluster with Data Lake Store as hello default storage</span></span>

<span data-ttu-id="04e30-170">Nesta seção, você cria um cluster HDInsight Hadoop Linux com repositório Data Lake como armazenamento padrão da saudação.</span><span class="sxs-lookup"><span data-stu-id="04e30-170">In this section, you create an HDInsight Hadoop Linux cluster with Data Lake Store as hello default storage.</span></span> <span data-ttu-id="04e30-171">Para esta versão, Olá cluster HDInsight e repositório Data Lake deve estar no hello mesmo local.</span><span class="sxs-lookup"><span data-stu-id="04e30-171">For this release, hello HDInsight cluster and Data Lake Store must be in hello same location.</span></span>

1. <span data-ttu-id="04e30-172">Recuperar a ID de locatário de assinatura hello e armazená-lo toouse mais tarde.</span><span class="sxs-lookup"><span data-stu-id="04e30-172">Retrieve hello subscription tenant ID, and store it toouse later.</span></span>

        $tenantID = (Get-AzureRmContext).Tenant.TenantId

2. <span data-ttu-id="04e30-173">Crie o cluster do HDInsight hello usando Olá cmdlets a seguir:</span><span class="sxs-lookup"><span data-stu-id="04e30-173">Create hello HDInsight cluster by using hello following cmdlets:</span></span>

        # Set these variables

        $location = "East US 2"
        $storageAccountName = $dataLakeStoreName                       # Data Lake Store account name
        $storageRootPath = "<Storage root path you specified earlier>" # E.g. /clusters/hdiadlcluster
        $clusterName = "<unique cluster name>"
        $clusterNodes = <ClusterSizeInNodes>            # hello number of nodes in hello HDInsight cluster
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

    <span data-ttu-id="04e30-174">Depois que o cmdlet Olá foi concluída com êxito, você verá uma saída que lista detalhes do cluster hello.</span><span class="sxs-lookup"><span data-stu-id="04e30-174">After hello cmdlet has been successfully completed, you should see an output that lists hello cluster details.</span></span>

## <a name="run-test-jobs-on-hello-hdinsight-cluster-toouse-data-lake-store"></a><span data-ttu-id="04e30-175">Executar trabalhos de teste no hello HDInsight cluster toouse repositório Data Lake</span><span class="sxs-lookup"><span data-stu-id="04e30-175">Run test jobs on hello HDInsight cluster toouse Data Lake Store</span></span>
<span data-ttu-id="04e30-176">Depois de configurar um cluster HDInsight, você pode executar trabalhos de teste nele tooensure que ele pode acessar o repositório Data Lake.</span><span class="sxs-lookup"><span data-stu-id="04e30-176">After you have configured an HDInsight cluster, you can run test jobs on it tooensure that it can access Data Lake Store.</span></span> <span data-ttu-id="04e30-177">toodo assim, executar um toocreate de trabalho de Hive exemplo uma tabela que usa dados de exemplo hello que já estão disponíveis no repositório Data Lake em  *<cluster root>/example/data/sample.log*.</span><span class="sxs-lookup"><span data-stu-id="04e30-177">toodo so, run a sample Hive job toocreate a table that uses hello sample data that's already available in Data Lake Store at *<cluster root>/example/data/sample.log*.</span></span>

<span data-ttu-id="04e30-178">Nesta seção, você faz uma conexão Secure Shell (SSH) em Olá cluster HDInsight Linux que você criou e, em seguida, você pode executar um exemplo de consulta de Hive.</span><span class="sxs-lookup"><span data-stu-id="04e30-178">In this section, you make a Secure Shell (SSH) connection into hello HDInsight Linux cluster that you created, and then you run a sample Hive query.</span></span>

* <span data-ttu-id="04e30-179">Se você estiver usando um cliente de Windows toomake uma conexão SSH em cluster hello, consulte [usar SSH com baseados em Linux Hadoop no HDInsight do Windows](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).</span><span class="sxs-lookup"><span data-stu-id="04e30-179">If you are using a Windows client toomake an SSH connection into hello cluster, see [Use SSH with Linux-based Hadoop on HDInsight from Windows](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).</span></span>
* <span data-ttu-id="04e30-180">Se você estiver usando um cliente de Linux toomake uma conexão SSH em cluster hello, consulte [usar SSH com baseados em Linux Hadoop no HDInsight do Linux](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="04e30-180">If you are using a Linux client toomake an SSH connection into hello cluster, see [Use SSH with Linux-based Hadoop on HDInsight from Linux](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

1. <span data-ttu-id="04e30-181">Depois de ter feito conexão hello, inicie interface de linha de comando de Hive hello (CLI) usando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="04e30-181">After you have made hello connection, start hello Hive command-line interface (CLI) by using hello following command:</span></span>

        hive
2. <span data-ttu-id="04e30-182">Use Olá CLI tooenter Olá seguindo as instruções toocreate uma nova tabela nomeada **veículos** usando dados de exemplo hello no repositório Data Lake:</span><span class="sxs-lookup"><span data-stu-id="04e30-182">Use hello CLI tooenter hello following statements toocreate a new table named **vehicles** by using hello sample data in Data Lake Store:</span></span>

        DROP TABLE log4jLogs;
        CREATE EXTERNAL TABLE log4jLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
        ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
        STORED AS TEXTFILE LOCATION 'adl:///example/data/';
        SELECT t4 AS sev, COUNT(*) AS count FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log' GROUP BY t4;

    <span data-ttu-id="04e30-183">Você deve ver a saída da consulta Olá no console do SSH hello.</span><span class="sxs-lookup"><span data-stu-id="04e30-183">You should see hello query output on hello SSH console.</span></span>

    >[!NOTE]
    ><span data-ttu-id="04e30-184">Olá dados de exemplo do caminho toohello no hello precede o comando CREATE TABLE são `adl:///example/data/`, onde `adl:///` é Olá cluster raiz.</span><span class="sxs-lookup"><span data-stu-id="04e30-184">hello path toohello sample data in hello preceding CREATE TABLE command is `adl:///example/data/`, where `adl:///` is hello cluster root.</span></span> <span data-ttu-id="04e30-185">Seguindo o exemplo hello da raiz do cluster Olá especificado neste tutorial, o comando de saudação é `adl://hdiadlstore.azuredatalakestore.net/clusters/hdiadlcluster`.</span><span class="sxs-lookup"><span data-stu-id="04e30-185">Following hello example of hello cluster root that's specified in this tutorial, hello command is `adl://hdiadlstore.azuredatalakestore.net/clusters/hdiadlcluster`.</span></span> <span data-ttu-id="04e30-186">Você pode usar alternativo mais curto hello ou fornecer raiz de cluster de toohello Olá caminho completo.</span><span class="sxs-lookup"><span data-stu-id="04e30-186">You can either use hello shorter alternative or provide hello complete path toohello cluster root.</span></span>
    >

## <a name="access-data-lake-store-by-using-hdfs-commands"></a><span data-ttu-id="04e30-187">Acessar o Data Lake Store usando comandos do HDFS</span><span class="sxs-lookup"><span data-stu-id="04e30-187">Access Data Lake Store by using HDFS commands</span></span>
<span data-ttu-id="04e30-188">Depois que você tiver configurado o repositório Data Lake do toouse de cluster de HDInsight hello, você pode usar o repositório de saudação do sistema de arquivos distribuído da Hadoop (HDFS) shell comandos tooaccess.</span><span class="sxs-lookup"><span data-stu-id="04e30-188">After you have configured hello HDInsight cluster toouse Data Lake Store, you can use Hadoop Distributed File System (HDFS) shell commands tooaccess hello store.</span></span>

<span data-ttu-id="04e30-189">Nesta seção, você faz uma conexão SSH em Olá cluster HDInsight Linux que você criou e, em seguida, executar comandos HDFS hello.</span><span class="sxs-lookup"><span data-stu-id="04e30-189">In this section, you make an SSH connection into hello HDInsight Linux cluster that you created, and then you run hello HDFS commands.</span></span>

* <span data-ttu-id="04e30-190">Se você estiver usando um cliente de Windows toomake uma conexão SSH em cluster hello, consulte [usar SSH com baseados em Linux Hadoop no HDInsight do Windows](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).</span><span class="sxs-lookup"><span data-stu-id="04e30-190">If you are using a Windows client toomake an SSH connection into hello cluster, see [Use SSH with Linux-based Hadoop on HDInsight from Windows](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).</span></span>
* <span data-ttu-id="04e30-191">Se você estiver usando um cliente de Linux toomake uma conexão SSH em cluster hello, consulte [usar SSH com baseados em Linux Hadoop no HDInsight do Linux](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="04e30-191">If you are using a Linux client toomake an SSH connection into hello cluster, see [Use SSH with Linux-based Hadoop on HDInsight from Linux](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

<span data-ttu-id="04e30-192">Depois de ter feito conexão hello, liste arquivos Olá no repositório Data Lake usando Olá após o comando de sistema de arquivo HDFS.</span><span class="sxs-lookup"><span data-stu-id="04e30-192">After you've made hello connection, list hello files in Data Lake Store by using hello following HDFS file system command.</span></span>

    hdfs dfs -ls adl:///

<span data-ttu-id="04e30-193">Você também pode usar o hello `hdfs dfs -put` comando tooupload alguns repositório de Lake tooData arquivos e, em seguida, usar `hdfs dfs -ls` tooverify arquivos Olá foram carregados com êxito.</span><span class="sxs-lookup"><span data-stu-id="04e30-193">You can also use hello `hdfs dfs -put` command tooupload some files tooData Lake Store, and then use `hdfs dfs -ls` tooverify whether hello files were successfully uploaded.</span></span>

## <a name="see-also"></a><span data-ttu-id="04e30-194">Consulte também</span><span class="sxs-lookup"><span data-stu-id="04e30-194">See also</span></span>
* [<span data-ttu-id="04e30-195">Portal do Azure: criar um cluster de HDInsight toouse repositório Data Lake</span><span class="sxs-lookup"><span data-stu-id="04e30-195">Azure portal: Create an HDInsight cluster toouse Data Lake Store</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)

[makecert]: https://msdn.microsoft.com/library/windows/desktop/ff548309(v=vs.85).aspx
[pvk2pfx]: https://msdn.microsoft.com/library/windows/desktop/ff550672(v=vs.85).aspx
