---
título: aaa "PowerShell: cluster de HDInsight do Azure com o repositório Data Lake como armazenamento de complemento | Serviços Microsoft Docs":-repositório data lake-hdinsight documentationcenter: ' autor: manager nitinme: jhubbard editor: cgronlun

MS. AssetID: 164ada5a-222e-4be2-bd32-e51dbe993bc0 MS. Service: MS. devlang do repositório do data lake: na MS. Topic: artigo tgt_pltfrm: na Workload: grandes dados MS. Date: 08/06/2017 Author: nitinme

---
# <a name="use-azure-powershell-toocreate-an-hdinsight-cluster-with-data-lake-store-as-additional-storage"></a>Use o Azure PowerShell toocreate um cluster HDInsight com repositório Data Lake (como armazenamento adicional)
> [!div class="op_single_selector"]
> * [Usando o Portal](data-lake-store-hdinsight-hadoop-use-portal.md)
> * [Usando o PowerShell (para o armazenamento padrão)](data-lake-store-hdinsight-hadoop-use-powershell-for-default-storage.md)
> * [Usando o PowerShell (para o armazenamento adicional)](data-lake-store-hdinsight-hadoop-use-powershell.md)
> * [Usando o Gerenciador de Recursos](data-lake-store-hdinsight-hadoop-use-resource-manager-template.md)
>
>

Saiba como toouse do Azure PowerShell tooconfigure um HDInsight cluster com repositório Azure Data Lake, **como armazenamento adicional**. Para obter instruções sobre como toocreate uma HDInsight cluster com repositório Azure Data Lake como armazenamento padrão, consulte [criar um cluster HDInsight com repositório Data Lake como armazenamento padrão](data-lake-store-hdinsight-hadoop-use-powershell-for-default-storage.md).

> [!NOTE]
> Se você for repositório toouse Azure Data Lake como armazenamento adicional para o cluster HDInsight, é altamente recomendável que você faça isso durante a criação de cluster Olá conforme descrito neste artigo. Adicionar repositório Azure Data Lake como armazenamento adicional tooan cluster HDInsight existente é um processo complicado e sujeito a tooerrors.
>

Para tipos de cluster com suporte, o Data Lake Store pode ser usado como um armazenamento padrão ou uma conta de armazenamento adicional. Quando o repositório Data Lake é usado como armazenamento adicional, conta de armazenamento padrão Olá para clusters de saudação ainda estará Blobs de armazenamento do Azure (WASB) e arquivos relacionados ao cluster de saudação (como logs, etc.) são gravados ainda armazenamento padrão de toohello, enquanto os dados de saudação que você deseja tooprocess podem ser armazenados em uma conta do repositório Data Lake. Usando o repositório Data Lake como uma conta de armazenamento adicional não afeta o desempenho e o hello capacidade tooread/gravação toohello armazenamento de cluster hello.

## <a name="using-data-lake-store-for-hdinsight-cluster-storage"></a>Usando o Data Lake Store para armazenamento do cluster HDInsight

Aqui estão algumas considerações importantes para usar o HDInsight com o Data Lake Store:

* Clusters de HDInsight toocreate opção com acesso tooData Lake repositório como armazenamento adicional está disponível para HDInsight versões 3.2, 3.4, 3.5 e 3.6.

Configuração do HDInsight toowork com repositório Data Lake usando o PowerShell envolve Olá etapas a seguir:

* Criar um Repositório Azure Data Lake
* Configurar a autenticação para baseado em função acessar o repositório de Lake tooData
* Criar o cluster HDInsight com autenticação tooData Lake repositório
* Executar um trabalho de teste no cluster Olá

## <a name="prerequisites"></a>Pré-requisitos
Antes de começar este tutorial, você deve ter o seguinte hello:

* **Uma assinatura do Azure**. Consulte [Obter avaliação gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/).
* **Azure PowerShell 1.0 ou superior**. Consulte [como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview).
* **SDK do Windows**. Você pode instalá-lo clicando [aqui](https://dev.windows.com/en-us/downloads). Você usa essa toocreate um certificado de segurança.
* **Entidade de serviço do Azure Active Directory**. As etapas deste tutorial fornecem instruções sobre como toocreate uma entidade de serviço no AD do Azure. No entanto, você deve ser um toocreate capaz do AD do Azure administrador toobe uma entidade de serviço. Se você for um administrador do AD do Azure, você pode ignorar esse pré-requisito e continuar com o tutorial hello.

    **Se você não for um administrador do AD do Azure**, não será capaz de tooperform Olá etapas necessárias toocreate uma entidade de serviço. Nesse caso, o administrador do Azure AD deverá primeiro criar uma entidade de serviço antes de criar um cluster HDInsight com Data Lake Store. Além disso, Olá entidade de serviço deve ser criada usando um certificado, conforme descrito em [criar uma entidade de serviço com certificado](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-certificate-from-certificate-authority).

## <a name="create-an-azure-data-lake-store"></a>Criar um Repositório Azure Data Lake
Siga essas etapas toocreate um repositório Data Lake.

1. Na área de trabalho, abra uma nova janela do PowerShell do Azure e insira Olá trecho de código a seguir. Quando toolog solicitada, certifique-se de você fazer logon como um administrador/proprietário da assinatura hello:

        # Log in tooyour Azure account
        Login-AzureRmAccount

        # List all hello subscriptions associated tooyour account
        Get-AzureRmSubscription

        # Select a subscription
        Set-AzureRmContext -SubscriptionId <subscription ID>

        # Register for Data Lake Store
        Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.DataLakeStore"

   > [!NOTE]
   > Se você receber um erro semelhante muito`Register-AzureRmResourceProvider : InvalidResourceNamespace: hello resource namespace 'Microsoft.DataLakeStore' is invalid` ao registrar o provedor de recursos do repositório Data Lake Olá, é possível que a sua assinatura não está autorizado para repositório Azure Data Lake. Verifique se você habilitou sua assinatura do Azure para a visualização pública do Data Lake Store seguindo estas [instruções](data-lake-store-get-started-portal.md).
   >
   >
2. Uma conta do Repositório Azure Data Lake está associada a um Grupo de Recursos do Azure. Comece criando um Grupo de Recursos do Azure.

        $resourceGroupName = "<your new resource group name>"
        New-AzureRmResourceGroup -Name $resourceGroupName -Location "East US 2"

    Você verá uma saída semelhante à seguinte:

        ResourceGroupName : hdiadlgrp
        Location          : eastus2
        ProvisioningState : Succeeded
        Tags              :
        ResourceId        : /subscriptions/<subscription-id>/resourceGroups/hdiadlgrp

3. Crie uma conta do Repositório Azure Data Lake. conta de saudação nome que você especificar deve conter apenas letras minúsculas e números.

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

5. Carregar alguns dados de exemplo tooAzure Data Lake. Usaremos isso mais tarde neste tooverify artigo que dados saudação são acessíveis a partir de um cluster HDInsight. Se você estiver procurando por alguns tooupload de dados de exemplo, você pode obter Olá **ambulância dados** pasta Olá [repositório Git do Azure Data Lake](https://github.com/MicrosoftBigData/usql/tree/master/Examples/Samples/Data/AmbulanceData).

        $myrootdir = "/"
        Import-AzureRmDataLakeStoreItem -AccountName $dataLakeStoreName -Path "C:\<path toodata>\vehicle1_09142014.csv" -Destination $myrootdir\vehicle1_09142014.csv


## <a name="set-up-authentication-for-role-based-access-toodata-lake-store"></a>Configurar a autenticação para baseado em função acessar o repositório de Lake tooData
Cada assinatura do Azure está associada com um Azure Active Directory. Usuários e serviços que acessam os recursos de assinatura de saudação usando Olá Portal clássico do Azure ou API do Azure Resource Manager devem primeiro autenticar com que o Active Directory do Azure. Acesso tooAzure assinaturas e serviços, atribuindo-lhes a função apropriada de saudação em um recurso do Azure.  Para serviços, uma entidade de serviço identifica o serviço Olá Olá Azure AAD (Active Directory). Esta seção ilustra como toogrant um aplicativo de serviço, como HDInsight, tooan de acesso a recursos do Azure (Olá conta do repositório Azure Data Lake criado anteriormente), criar uma entidade de serviço para o aplicativo hello e atribuir funções toothat por meio do Azure PowerShell.

tooset a autenticação do Active Directory para o Azure Data Lake, você deve executar Olá tarefas a seguir.

* Crie um certificado autoassinado
* Criar um aplicativo no Active Directory do Azure e uma entidade de serviço

### <a name="create-a-self-signed-certificate"></a>Crie um certificado autoassinado
Verifique se você tem [SDK do Windows](https://dev.windows.com/en-us/downloads) instalado antes de prosseguir com a saudação as etapas nesta seção. Você deve também criou um diretório, como **C:\mycertdir**, qual certificado Olá será criado.

1. Na janela do PowerShell hello, navegar toohello local onde você instalou o SDK do Windows (normalmente, `C:\Program Files (x86)\Windows Kits\10\bin\x86` e usar Olá [MakeCert] [ makecert] toocreate utilitário um certificado autoassinado e uma chave privada. Use Olá comandos a seguir.

        $certificateFileDir = "<my certificate directory>"
        cd $certificateFileDir

        makecert -sv mykey.pvk -n "cn=HDI-ADL-SP" CertFile.cer -r -len 2048

    Será a senha da chave privada tooenter solicitadas hello. Depois que o comando Olá for executado com êxito, você verá um **CertFile.cer** e **mykey.pvk** no diretório de certificado Olá especificado.
2. Saudação de uso [Pvk2Pfx] [ pvk2pfx] . pvk do utilitário tooconvert hello e. cer arquivos de arquivo. pfx criado tooa MakeCert. Execute Olá comando a seguir.

        pvk2pfx -pvk mykey.pvk -spc CertFile.cer -pfx CertFile.pfx -po <password>

    Quando solicitado que digite Olá senha da chave privada especificado anteriormente. Olá valor especificado para Olá **-po** parâmetro é a senha de saudação que está associada ao arquivo. pfx de saudação. Após concluir com êxito do comando Olá, você verá também uma CertFile.pfx no diretório de certificado Olá especificado.

### <a name="create-an-azure-active-directory-and-a-service-principal"></a>Criar um Active Directory do Azure e uma entidade de serviço
Nesta seção, executar etapas de saudação toocreate uma entidade de serviço para um aplicativo do Active Directory do Azure, atribuir uma entidade de serviço de toohello de função e autenticar como entidade de serviço hello, fornecendo um certificado. Olá toocreate comandos a seguir ao execute um aplicativo no Azure Active Directory.

1. Colar Olá cmdlets na janela de console do PowerShell Olá a seguir. Verifique se valor Olá você especificar para Olá **- DisplayName** propriedade é exclusiva. Além disso, Olá valores para **- home page** e **- IdentiferUris** são valores de espaço reservado e não são verificadas.

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
3. Conceder a pasta do repositório Data Lake do hello serviço de acesso principal toohello e arquivo hello que você irá acessar do cluster do HDInsight hello. trecho de saudação abaixo fornece raiz toohello acesso Olá repositório Data Lake (onde você copiou o arquivo de dados de exemplo hello) de conta e Olá próprio arquivo.

        Set-AzureRmDataLakeStoreItemAclEntry -AccountName $dataLakeStoreName -Path / -AceType User -Id $objectId -Permissions All
        Set-AzureRmDataLakeStoreItemAclEntry -AccountName $dataLakeStoreName -Path /vehicle1_09142014.csv -AceType User -Id $objectId -Permissions All

## <a name="create-an-hdinsight-linux-cluster-with-data-lake-store-as-additional-storage"></a>Criar um cluster Linux HDInsight com o Data Lake Store como armazenamento adicional

Nesta seção, criamos um cluster Linux Hadoop HDInsight com o Data Lake Store como armazenamento adicional. Para esta versão, cluster de HDInsight hello e repositório Olá Data Lake devem estar no hello mesmo local.

1. Iniciar com a recuperação de ID de locatário de assinatura de saudação. Você precisará disso posteriormente.

        $tenantID = (Get-AzureRmContext).Tenant.TenantId
2. Para esta versão, para um cluster de Hadoop, repositório Data Lake pode ser usado somente como um armazenamento adicional para cluster hello. armazenamento padrão da saudação ainda serão blobs de armazenamento do Azure hello (WASB). Assim, vamos primeiro criar hello contêineres de armazenamento e a conta de armazenamento necessários para o cluster de saudação.

        # Create an Azure storage account
        $location = "East US 2"
        $storageAccountName = "<StorageAcccountName>"   # Provide a Storage account name

        New-AzureRmStorageAccount -ResourceGroupName $resourceGroupName -StorageAccountName $storageAccountName -Location $location -Type Standard_GRS

        # Create an Azure Blob Storage container
        $containerName = "<ContainerName>"              # Provide a container name
        $storageAccountKey = (Get-AzureRmStorageAccountKey -Name $storageAccountName -ResourceGroupName $resourceGroupName)[0].Value
        $destContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey
        New-AzureStorageContainer -Name $containerName -Context $destContext
3. Crie cluster do HDInsight hello. Use Olá cmdlets a seguir.

        # Set these variables
        $clusterName = $containerName                   # As a best practice, have hello same name for hello cluster and container
        $clusterNodes = <ClusterSizeInNodes>            # hello number of nodes in hello HDInsight cluster
        $httpCredentials = Get-Credential
        $sshCredentials = Get-Credential

        New-AzureRmHDInsightCluster -ClusterName $clusterName -ResourceGroupName $resourceGroupName -HttpCredential $httpCredentials -Location $location -DefaultStorageAccountName "$storageAccountName.blob.core.windows.net" -DefaultStorageAccountKey $storageAccountKey -DefaultStorageContainer $containerName  -ClusterSizeInNodes $clusterNodes -ClusterType Hadoop -Version "3.4" -OSType Linux -SshCredential $sshCredentials -ObjectID $objectId -AadTenantId $tenantID -CertificateFilePath $certificateFilePath -CertificatePassword $password

    Depois que o cmdlet Olá for concluído com êxito, você verá uma saída listando os detalhes do cluster Olá.


## <a name="run-test-jobs-on-hello-hdinsight-cluster-toouse-hello-data-lake-store"></a>Executar trabalhos de teste em Olá HDInsight cluster toouse Olá repositório Data Lake
Depois de configurar um cluster HDInsight, você pode executar trabalhos de teste em Olá cluster tootest que Olá HDInsight cluster pode acessar o repositório Data Lake. toodo assim, iremos executar um trabalho de Hive de exemplo que cria uma tabela usando dados de exemplo hello que você carregou anteriormente repositório tooyour Data Lake.

Nesta seção, você irá SSH para Olá HDInsight Linux do cluster é criado e executado Olá um exemplo de consulta de Hive.

* Se você estiver usando um tooSSH de cliente do Windows em cluster hello, consulte [usar SSH com baseados em Linux Hadoop no HDInsight do Windows](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).
* Se você estiver usando um tooSSH de cliente do Linux em cluster hello, consulte [usar SSH com baseados em Linux Hadoop no HDInsight do Linux](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md)

1. Uma vez conectado, inicie Olá CLI do Hive usando Olá comando a seguir:

        hive
2. Usando Olá CLI, insira Olá seguindo as instruções toocreate uma nova tabela nomeada **veículos** com dados de exemplo hello Olá repositório Data Lake:

        DROP TABLE vehicles;
        CREATE EXTERNAL TABLE vehicles (str string) LOCATION 'adl://<mydatalakestore>.azuredatalakestore.net:443/';
        SELECT * FROM vehicles LIMIT 10;

    Você verá uma saída semelhante toohello a seguir:

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

## <a name="access-data-lake-store-using-hdfs-commands"></a>Repositório Data Lake usando comandos do HDFS
Quando você tiver configurado o repositório Data Lake do toouse de cluster de HDInsight hello, você pode usar comandos de shell do hello HDFS tooaccess Olá repositório.

Nesta seção, você irá SSH para Olá HDInsight Linux criado e executar comandos HDFS de saudação do cluster.

* Se você estiver usando um tooSSH de cliente do Windows em cluster hello, consulte [usar SSH com baseados em Linux Hadoop no HDInsight do Windows](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).
* Se você estiver usando um tooSSH de cliente do Linux em cluster hello, consulte [usar SSH com baseados em Linux Hadoop no HDInsight do Linux](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md)

Uma vez conectado, use Olá arquivos HDFS filesystem comando toolist Olá no hello repositório Data Lake a seguir.

    hdfs dfs -ls adl://<Data Lake Store account name>.azuredatalakestore.net:443/

Isso deve listar arquivo hello que você carregou anteriormente repositório toohello Data Lake.

    15/09/17 21:41:15 INFO web.CaboWebHdfsFileSystem: Replacing original urlConnectionFactory with org.apache.hadoop.hdfs.web.URLConnectionFactory@21a728d6
    Found 1 items
    -rwxrwxrwx   0 NotSupportYet NotSupportYet     671388 2015-09-16 22:16 adl://mydatalakestore.azuredatalakestore.net:443/mynewfolder

Você também pode usar o hello `hdfs dfs -put` comando tooupload toohello alguns arquivos repositório Data Lake e, em seguida, usar `hdfs dfs -ls` tooverify arquivos Olá foram carregados com êxito.

## <a name="see-also"></a>Consulte também
* [Portal: Criar um cluster de HDInsight toouse repositório Data Lake](data-lake-store-hdinsight-hadoop-use-portal.md)

[makecert]: https://msdn.microsoft.com/library/windows/desktop/ff548309(v=vs.85).aspx
[pvk2pfx]: https://msdn.microsoft.com/library/windows/desktop/ff550672(v=vs.85).aspx
