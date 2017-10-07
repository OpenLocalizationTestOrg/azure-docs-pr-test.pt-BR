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
# <a name="create-hdinsight-clusters-with-data-lake-store-as-default-storage-by-using-powershell"></a>Criar clusters HDInsight com o Data Lake Store como armazenamento padrão usando o PowerShell
> [!div class="op_single_selector"]
> * [Use Olá portal do Azure](data-lake-store-hdinsight-hadoop-use-portal.md)
> * [Usar o PowerShell (para armazenamento padrão)](data-lake-store-hdinsight-hadoop-use-powershell-for-default-storage.md)
> * [Usar o PowerShell (para armazenamento adicional)](data-lake-store-hdinsight-hadoop-use-powershell.md)
> * [Usar o Resource Manager](data-lake-store-hdinsight-hadoop-use-resource-manager-template.md)

Saiba como clusters de toouse tooconfigure de PowerShell do Azure HDInsight do Azure com repositório Azure Data Lake, como o armazenamento padrão. Para obter instruções sobre como criar um cluster HDInsight com o Data Lake Store como armazenamento adicional, consulte [Criar um cluster HDInsight com o Data Lake Store como armazenamento adicional](data-lake-store-hdinsight-hadoop-use-powershell.md).

Aqui estão algumas considerações importantes para usar o HDInsight com o Data Lake Store:

* clusters de HDInsight do Hello opção toocreate com acesso tooData Lake repositório como armazenamento padrão está disponível para HDInsight versão 3.5 e 3.6.

* Olá opção toocreate clusters de HDInsight com acesso tooData Lake repositório como o armazenamento padrão é *não disponível* para clusters de HDInsight Premium.

tooconfigure toowork de HDInsight com repositório Data Lake usando o PowerShell, siga as instruções de saudação nas seções de cinco hello.

## <a name="prerequisites"></a>Pré-requisitos
Antes de começar este tutorial, certifique-se de atender Olá requisitos a seguir:

* **Uma assinatura do Azure**: ir muito[avaliação gratuita do Azure obter](https://azure.microsoft.com/pricing/free-trial/).
* **O Azure PowerShell 1.0 ou maior**: consulte [como tooinstall e configurar o PowerShell](/powershell/azure/overview).
* **Windows Software Development Kit (SDK)**: tooinstall SDK do Windows, vá muito[Downloads e ferramentas para Windows 10](https://dev.windows.com/en-us/downloads). Olá SDK é toocreate usado um certificado de segurança.
* **Entidade de serviço do Active Directory do Azure**: Este tutorial descreve como toocreate uma entidade de serviço no Azure Active Directory (AD do Azure). No entanto, toocreate uma entidade de serviço, você deve ser um administrador do AD do Azure. Se você for um administrador, você pode ignorar esse pré-requisito e continuar com o tutorial hello.

    >[!NOTE]
    >Você poderá criar uma entidade de serviço somente se for um administrador do Azure AD. O administrador do Azure AD deverá criar uma entidade de serviço antes que você possa criar um cluster HDInsight com o Data Lake Store. Olá entidade de serviço deve ser criada com um certificado, conforme descrito em [criar uma entidade de serviço com certificado](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-certificate-from-certificate-authority).
    >

## <a name="create-a-data-lake-store-account"></a>Criar uma conta do Repositório Data Lake
toocreate uma conta do repositório Data Lake, Olá a seguir:

1. Na área de trabalho, abra uma janela do PowerShell e, em seguida, inserir trechos de código Olá abaixo. Quando você estiver toosign solicitada na entrada como um dos administradores de assinatura de saudação ou proprietários. 

        # Sign in tooyour Azure account
        Login-AzureRmAccount

        # List all hello subscriptions associated tooyour account
        Get-AzureRmSubscription

        # Select a subscription
        Set-AzureRmContext -SubscriptionId <subscription ID>

        # Register for Data Lake Store
        Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.DataLakeStore"

    > [!NOTE]
    > Se você registrar o provedor de recursos do repositório Data Lake hello e receber um erro semelhante muito`Register-AzureRmResourceProvider : InvalidResourceNamespace: hello resource namespace 'Microsoft.DataLakeStore' is invalid`, sua assinatura não pode estar na lista de permissões para o repositório Data Lake. tooenable a sua assinatura do Azure para a visualização pública do repositório Data Lake hello, siga instruções Olá [Introdução ao repositório Azure Data Lake usando o portal do Azure de saudação](data-lake-store-get-started-portal.md).
    >

2. Uma conta do Data Lake Store está associada a um grupo de recursos do Azure. Comece criando um grupo de recursos.

        $resourceGroupName = "<your new resource group name>"
        New-AzureRmResourceGroup -Name $resourceGroupName -Location "East US 2"

    Você verá uma saída semelhante à seguinte:

        ResourceGroupName : hdiadlgrp
        Location          : eastus2
        ProvisioningState : Succeeded
        Tags              :
        ResourceId        : /subscriptions/<subscription-id>/resourceGroups/hdiadlgrp

3. Crie uma conta do Data Lake Store. conta de saudação nome que você especificar deve conter somente letras minúsculas e números.

        $dataLakeStoreName = "<your new Data Lake Store name>"
        New-AzureRmDataLakeStoreAccount -ResourceGroupName $resourceGroupName -Name $dataLakeStoreName -Location "East US 2"

    Você verá uma saída semelhante Olá seguinte:

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

4. O uso do repositório Data Lake como armazenamento padrão requer toospecify que um arquivos de específicas do cluster raiz caminho toowhich Olá são copiados durante a criação do cluster. toocreate um caminho raiz, que é **clusters/hdiadlcluster** no trecho hello, use Olá cmdlets a seguir:

        $myrootdir = "/"
        New-AzureRmDataLakeStoreItem -Folder -AccountName $dataLakeStoreName -Path $myrootdir/clusters/hdiadlcluster


## <a name="set-up-authentication-for-role-based-access-toodata-lake-store"></a>Configurar a autenticação para baseado em função acessar o repositório de Lake tooData
Cada assinatura do Azure está associada a uma entidade do Azure AD. Usuários e serviços que os recursos de assinatura de acesso usando Olá portal do Azure ou Olá API do Gerenciador de recursos do Azure devem primeiro autenticar com o AD do Azure. Acesso tooAzure assinaturas e serviços, atribuindo-lhes a função apropriada de saudação em um recurso do Azure. Para serviços, uma entidade de serviço identifica o serviço Olá no AD do Azure.

Esta seção ilustra como toogrant um aplicativo de serviço, como HDInsight, tooan de acesso a recursos do Azure (Olá conta do repositório Data Lake que você criou anteriormente). Você pode fazer isso criando um serviço principal para o aplicativo hello e atribuindo funções tooit por meio do PowerShell.

tooset a autenticação do Active Directory para o Azure Data Lake, execute tarefas de Olá Olá duas seções a seguir.

### <a name="create-a-self-signed-certificate"></a>Crie um certificado autoassinado
Verifique se você tem [SDK do Windows](https://dev.windows.com/en-us/downloads) instalado antes de prosseguir com a saudação as etapas nesta seção. Você deve também criou um diretório, como *C:\mycertdir*, em que você criar o certificado de saudação.

1. Na janela do PowerShell Olá, vá toohello local onde você instalou o SDK do Windows (normalmente, *C:\Program Files (x86) \Windows Kits\10\bin\x86*) e usar o hello [MakeCert] [ makecert] toocreate utilitário um certificado autoassinado e uma chave privada. Use Olá comandos a seguir:

        $certificateFileDir = "<my certificate directory>"
        cd $certificateFileDir

        makecert -sv mykey.pvk -n "cn=HDI-ADL-SP" CertFile.cer -r -len 2048

    Será a senha da chave privada tooenter solicitadas hello. Depois que o comando Olá é executado com êxito, você deverá ver **CertFile.cer** e **mykey.pvk** Olá certificado no diretório em que você especificou.
2. Saudação de uso [Pvk2Pfx] [ pvk2pfx] . pvk do utilitário tooconvert hello e. cer arquivos de arquivo. pfx criado tooa MakeCert. Execute Olá comando a seguir:

        pvk2pfx -pvk mykey.pvk -spc CertFile.cer -pfx CertFile.pfx -po <password>

    Quando for solicitado, digite Olá senha da chave privada que você especificou anteriormente. Olá valor especificado para Olá **-po** parâmetro é a senha de saudação que está associado ao arquivo. pfx de saudação. Depois que o comando Olá foi concluído com êxito, você também deverá ver um **CertFile.pfx** Olá certificado no diretório em que você especificou.

### <a name="create-an-azure-ad-and-a-service-principal"></a>Criar um Azure AD e uma entidade de serviço
Nesta seção, criar uma entidade de serviço para um aplicativo do AD do Azure, atribua uma entidade de serviço de toohello de função e autenticar como entidade de serviço hello, fornecendo um certificado. toocreate um aplicativo no AD do Azure, execute Olá comandos a seguir:

1. Colar Olá cmdlets na janela de console do PowerShell Olá a seguir. Verifique se esse valor Olá você especificar para Olá **- DisplayName** propriedade é exclusiva. Olá valores para **- home page** e **- IdentiferUris** são valores de espaço reservado e não são verificadas.

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
2. Criar uma entidade de serviço usando a ID do aplicativo hello.

        $servicePrincipal = New-AzureRmADServicePrincipal -ApplicationId $applicationId

        $objectId = $servicePrincipal.Id
3. Conceda Olá serviço acesso principal toohello repositório Data Lake pastas raiz e todos os Olá no caminho de raiz de saudação que você especificou anteriormente. Use Olá cmdlets a seguir:

        Set-AzureRmDataLakeStoreItemAclEntry -AccountName $dataLakeStoreName -Path / -AceType User -Id $objectId -Permissions All
        Set-AzureRmDataLakeStoreItemAclEntry -AccountName $dataLakeStoreName -Path /clusters -AceType User -Id $objectId -Permissions All
        Set-AzureRmDataLakeStoreItemAclEntry -AccountName $dataLakeStoreName -Path /clusters/hdiadlcluster -AceType User -Id $objectId -Permissions All

## <a name="create-an-hdinsight-linux-cluster-with-data-lake-store-as-hello-default-storage"></a>Criar um cluster HDInsight Linux com repositório Data Lake como armazenamento de padrão de saudação

Nesta seção, você cria um cluster HDInsight Hadoop Linux com repositório Data Lake como armazenamento padrão da saudação. Para esta versão, Olá cluster HDInsight e repositório Data Lake deve estar no hello mesmo local.

1. Recuperar a ID de locatário de assinatura hello e armazená-lo toouse mais tarde.

        $tenantID = (Get-AzureRmContext).Tenant.TenantId

2. Crie o cluster do HDInsight hello usando Olá cmdlets a seguir:

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

    Depois que o cmdlet Olá foi concluída com êxito, você verá uma saída que lista detalhes do cluster hello.

## <a name="run-test-jobs-on-hello-hdinsight-cluster-toouse-data-lake-store"></a>Executar trabalhos de teste no hello HDInsight cluster toouse repositório Data Lake
Depois de configurar um cluster HDInsight, você pode executar trabalhos de teste nele tooensure que ele pode acessar o repositório Data Lake. toodo assim, executar um toocreate de trabalho de Hive exemplo uma tabela que usa dados de exemplo hello que já estão disponíveis no repositório Data Lake em  *<cluster root>/example/data/sample.log*.

Nesta seção, você faz uma conexão Secure Shell (SSH) em Olá cluster HDInsight Linux que você criou e, em seguida, você pode executar um exemplo de consulta de Hive.

* Se você estiver usando um cliente de Windows toomake uma conexão SSH em cluster hello, consulte [usar SSH com baseados em Linux Hadoop no HDInsight do Windows](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).
* Se você estiver usando um cliente de Linux toomake uma conexão SSH em cluster hello, consulte [usar SSH com baseados em Linux Hadoop no HDInsight do Linux](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md).

1. Depois de ter feito conexão hello, inicie interface de linha de comando de Hive hello (CLI) usando Olá comando a seguir:

        hive
2. Use Olá CLI tooenter Olá seguindo as instruções toocreate uma nova tabela nomeada **veículos** usando dados de exemplo hello no repositório Data Lake:

        DROP TABLE log4jLogs;
        CREATE EXTERNAL TABLE log4jLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
        ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
        STORED AS TEXTFILE LOCATION 'adl:///example/data/';
        SELECT t4 AS sev, COUNT(*) AS count FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log' GROUP BY t4;

    Você deve ver a saída da consulta Olá no console do SSH hello.

    >[!NOTE]
    >Olá dados de exemplo do caminho toohello no hello precede o comando CREATE TABLE são `adl:///example/data/`, onde `adl:///` é Olá cluster raiz. Seguindo o exemplo hello da raiz do cluster Olá especificado neste tutorial, o comando de saudação é `adl://hdiadlstore.azuredatalakestore.net/clusters/hdiadlcluster`. Você pode usar alternativo mais curto hello ou fornecer raiz de cluster de toohello Olá caminho completo.
    >

## <a name="access-data-lake-store-by-using-hdfs-commands"></a>Acessar o Data Lake Store usando comandos do HDFS
Depois que você tiver configurado o repositório Data Lake do toouse de cluster de HDInsight hello, você pode usar o repositório de saudação do sistema de arquivos distribuído da Hadoop (HDFS) shell comandos tooaccess.

Nesta seção, você faz uma conexão SSH em Olá cluster HDInsight Linux que você criou e, em seguida, executar comandos HDFS hello.

* Se você estiver usando um cliente de Windows toomake uma conexão SSH em cluster hello, consulte [usar SSH com baseados em Linux Hadoop no HDInsight do Windows](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).
* Se você estiver usando um cliente de Linux toomake uma conexão SSH em cluster hello, consulte [usar SSH com baseados em Linux Hadoop no HDInsight do Linux](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md).

Depois de ter feito conexão hello, liste arquivos Olá no repositório Data Lake usando Olá após o comando de sistema de arquivo HDFS.

    hdfs dfs -ls adl:///

Você também pode usar o hello `hdfs dfs -put` comando tooupload alguns repositório de Lake tooData arquivos e, em seguida, usar `hdfs dfs -ls` tooverify arquivos Olá foram carregados com êxito.

## <a name="see-also"></a>Consulte também
* [Portal do Azure: criar um cluster de HDInsight toouse repositório Data Lake](data-lake-store-hdinsight-hadoop-use-portal.md)

[makecert]: https://msdn.microsoft.com/library/windows/desktop/ff548309(v=vs.85).aspx
[pvk2pfx]: https://msdn.microsoft.com/library/windows/desktop/ff550672(v=vs.85).aspx
