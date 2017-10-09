---
title: aaaRun Sqoop Apache trabalhos com o Azure HDInsight (Hadoop) | Microsoft Docs
description: "Saiba como toouse PowerShell do Azure de uma estação de trabalho de toorun Sqoop de importação e exportação entre um cluster de Hadoop e um banco de dados do SQL Azure."
editor: cgronlun
manager: jhubbard
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
ms.assetid: 2fdcc6b7-6ad5-4397-a30b-e7e389b66c7a
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ROBOTS: NOINDEX
ms.openlocfilehash: bdac507704937d77921c9c13d70aa2434c7e3be4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-sqoop-with-hadoop-in-hdinsight"></a>Use Sqoop com Hadoop no HDInsight
[!INCLUDE [sqoop-selector](../../includes/hdinsight-selector-use-sqoop.md)]

Saiba como toouse Sqoop em HDInsight tooimport e exportar entre o cluster HDInsight e o banco de dados do SQL Azure ou o banco de dados do SQL Server.

Embora Hadoop é uma opção natural para processar dados semi-estruturados e não estruturados, como logs e arquivos, também pode haver uma necessidade de dados tooprocess estruturados armazenados em bancos de dados relacionais.

[Sqoop] [ sqoop-user-guide-1.4.4] é uma ferramenta desenvolvida tootransfer dados entre bancos de dados relacionais e clusters de Hadoop. Você pode usá-lo tooimport dados de um sistema de gerenciamento de banco de dados relacional (RDBMS), como SQL Server, MySQL ou Oracle no sistema de arquivo hello distribuído de Hadoop (HDFS), transformar dados Olá no Hadoop MapReduce ou Hive e, em seguida, exportar dados de saudação volta para um RDBMS. Neste tutorial, você está usando um Banco de Dados SQL como seu banco de dados relacional.

Para versões de Sqoop que têm suporte em clusters de HDInsight, consulte [Novidades nas versões de cluster Olá fornecidas pelo HDInsight?][hdinsight-versions]

## <a name="understand-hello-scenario"></a>Entender o cenário de saudação

O cluster HDInsight é fornecido com alguns dados de exemplo. Use o hello dois exemplos a seguir:

* Um arquivo de log log4j localizado em */example/data/sample.log*. Olá logs a seguir é extraído do arquivo hello:
  
        2012-02-03 18:35:34 SampleClass6 [INFO] everything normal for id 577725851
        2012-02-03 18:35:34 SampleClass4 [FATAL] system problem at id 1991281254
        2012-02-03 18:35:34 SampleClass3 [DEBUG] detail for id 1304807656
        ...
* Uma tabela de Hive denominada *hivesampletable*, que referências Olá arquivo de dados localizado em */hive/warehouse/hivesampletable*. Olá tabela contém alguns dados de dispositivo móvel. 
  
  | Campo | Tipo de dados |
  | --- | --- |
  | clientid |string |
  | querytime |string |
  | market |string |
  | deviceplatform |string |
  | devicemake |string |
  | devicemodel |string |
  | state |string |
  | country |string |
  | querydwelltime |double |
  | sessionid |bigint |
  | sessionpagevieworder |bigint |

Primeiro, você exportar *sample.log* e *hivesampletable* toohello banco de dados do SQL Azure ou tooSQL servidor e, em seguida, importação de tabela Olá que contém dados do dispositivo móvel Olá fazer tooHDInsight usando Olá caminho a seguir:

    /tutorials/usesqoop/importeddata

## <a name="create-cluster-and-sql-database"></a>Criar o cluster e o Banco de dados SQL
Esta seção mostra como toocreate um cluster, um banco de dados SQL e esquemas de banco de dados SQL Olá para em execução Olá tutorial usando Olá portal do Azure e um modelo do Gerenciador de recursos do Azure. Olá modelo pode ser encontrado no [modelos de início rápido do Azure](https://azure.microsoft.com/resources/templates/101-hdinsight-linux-with-sql-database/). modelo do Gerenciador de recursos de saudação chama um bacpac pacote toodeploy Olá tabela esquemas tooSQL banco de dados.  pacote de bacpac Hello está localizado em um contêiner de blob público, https://hditutorialdata.blob.core.windows.net/usesqoop/SqoopTutorial-2016-2-23-11-2.bacpac. Se você quiser toouse um contêiner privado para arquivos de bacpac Olá, use Olá valores no modelo de saudação a seguir:
   
        "storageKeyType": "Primary",
        "storageKey": "<TheAzureStorageAccountKey>",

Se preferir que o cluster de saudação de toocreate toouse PowerShell do Azure e hello banco de dados SQL, consulte [Apêndice A](#appendix-a---a-powershell-sample).

1. Clique em Olá imagem tooopen um modelo do Gerenciador de recursos no portal do Azure de saudação a seguir.         
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-linux-with-sql-database%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-use-sqoop/deploy-to-azure.png" alt="Deploy tooAzure"></a>
   

2. Digite hello propriedades a seguir:

    - **Subscription:** insira sua assinatura do Azure.
    - **Grupo de Recursos**: crie um novo grupo de recursos do Azure ou escolha um grupo de recursos existente.  Um grupo de recursos é para fins de gerenciamento.  Ele é um contêiner para objetos.
    - **Localização**: selecione uma região.
    - **ClusterName**: insira um nome para o cluster de Hadoop hello.
    - **Nome de logon e senha do cluster**: nome de logon do saudação padrão é Admin.
    - **Nome de usuário e senha de SSH**.
    - **Nome de logon e senha do servidor de banco de dados SQL**.
    - **_artifacts local**: usar o valor padrão de saudação, a menos que você deseja toouse seu próprio arquivo backpac em um local diferente.
    - **Token Sas do local de_artifacts**: deixe-o em branco.
    - **Nome do arquivo Bacpac**: usar o valor de padrão de saudação, a menos que você deseja toouse seu próprio arquivo de backpac.
     
     Olá valores a seguir é embutidos em código na seção de variáveis de saudação:
     
     | Nome da conta de armazenamento padrão | <CluterName>repositório |
     | --- | --- |
     | Nome do servidor de banco de dados SQL do Azure. |<ClusterName>dbserver |
     | Nome do banco de dados SQL do Azure |<ClusterName>db |
     
     Anote esses valores.  Você precisa-los mais tarde no tutorial de saudação.

3. clique em **Okey** toosave parâmetros de saudação.

4. de saudação **implantação personalizada** folha, clique em **grupo de recursos** suspensa caixa e, em seguida, clique em **novo** toocreate um novo grupo de recursos. grupo de recursos de saudação é um contêiner que agrupa cluster hello, conta de armazenamento dependente de saudação e outros recursos vinculados.

5. Clique em **Termos legais** e em **Criar**.

6. Clique em **Criar**. Você poderá ver um novo bloco intitulado Como enviar a implantação para a implantação do modelo. Demora cerca de cluster de saudação toocreate aproximadamente 20 minutos e o banco de dados SQL.

Se você escolher o banco de dados do SQL Azure existente toouse ou Microsoft SQL Server

* **Banco de dados do SQL Azure**: você deve configurar uma regra de firewall para Olá acesso tooallow ao servidor de banco de dados SQL do Azure de sua estação de trabalho. Para obter instruções sobre como criar um banco de dados do SQL Azure e configurando o firewall do hello, consulte [começar a usar o banco de dados do SQL Azure][sqldatabase-get-started]. 
  
  > [!NOTE]
  > Por padrão, um banco de dados SQL do Azure permite conexões de serviços do Azure, como o Azure HDInsight. Se essa configuração de firewall estiver desabilitada, você precisa tooenable de saudação portal do Azure. Para obter instruções sobre como criar um Banco de Dados SQL do Azure e configurar as regras de firewall, confira [Criar e configurar o Banco de Dados SQL][sqldatabase-create-configue].
  > 
  > 
* **SQL Server**: se o seu cluster HDInsight está em Olá mesma rede virtual no Azure como o SQL Server, você pode usar etapas Olá neste artigo tooimport e exportar dados tooa do SQL Server banco de dados.
  
  > [!NOTE]
  > O Azure HDInsight oferece suporte somente a redes virtuais baseadas no local, e não trabalha atualmente com redes virtuais baseadas em grupos de afinidade.
  > 
  > 
  
  * toocreate e configurar uma rede virtual, consulte [criar uma rede virtual usando o portal do Azure de saudação](../virtual-network/virtual-networks-create-vnet-arm-pportal.md).
    
    * Quando você estiver usando o SQL Server em seu data center, você deve configurar a rede virtual hello como *site a site* ou *ponto a site*.
      
      > [!NOTE]
      > Para **ponto a site** redes virtuais, o SQL Server devem estar em execução do cliente VPN Olá aplicativo de configuração, que está disponível no hello **painel** da sua configuração de rede virtual do Azure.
      > 
      > 
    * Quando você estiver usando o SQL Server em uma máquina virtual do Azure, qualquer configuração de rede virtual pode ser usada se a máquina virtual de saudação hospedando o SQL Server é um membro da saudação mesma rede virtual HDInsight.
  * toocreate um cluster HDInsight em uma rede virtual, consulte [Hadoop criar clusters de HDInsight usando opções personalizadas](hdinsight-hadoop-provision-linux-clusters.md)
    
    > [!NOTE]
    > O SQL Server também deve permitir autenticação. Você deve usar um SQL Server saudação do logon toocomplete as etapas neste artigo.
    > 
    > 

## <a name="run-sqoop-jobs"></a>Executar trabalhos do Sqoop
O HDInsight pode executar trabalhos do Sqoop usando vários métodos. Usar o hello toodecide tabela qual método é ideal para você a seguir, siga o link Olá para obter uma explicação.

| **Use** se quiser... | ...um shell **interativo** | ...Processamento em**lotes** | ... com esse **sistema operacional de cluster** | ... desse **sistema operacional cliente** |
|:--- |:---:|:---:|:--- |:--- |
| [SSH](hdinsight-use-sqoop-mac-linux.md) |✔ |✔ |Linux |Linux, Unix, Mac OS X ou Windows |
| [SDK .NET para Hadoop](hdinsight-hadoop-use-sqoop-dotnet-sdk.md) |&nbsp; |✔ |Linux ou Windows |Windows (por enquanto) |
| [PowerShell do Azure](hdinsight-hadoop-use-sqoop-powershell.md) |&nbsp; |✔ |Linux ou Windows |Windows |

## <a name="limitations"></a>Limitações
* A exportação em massa - HDInsight baseados em Linux com, Olá Sqoop conector usado tooexport dados tooMicrosoft do SQL Server ou banco de dados do SQL Azure atualmente não dá suporte para inserções em massa.
* Envio em lote - com HDInsight baseados em Linux, ao usar o hello `-batch` opção ao executar inserções, Sqoop executa várias inserções em vez de envio em lote as operações de inserção hello.

## <a name="next-steps"></a>Próximas etapas
Agora que você aprendeu como toouse Sqoop. toolearn mais, consulte:

* [Usar o Hive com o HDInsight](hdinsight-use-hive.md)
* [Usar o Pig com o HDInsight](hdinsight-use-pig.md)
* [Usar o Oozie com o HDInsight][hdinsight-use-oozie]: use a ação do Sqoop no fluxo de trabalho do Oozie.
* [Analisar dados de atraso de voo usando HDInsight][hdinsight-analyze-flight-data]: usar Hive tooanalyze voo atrasar dados e, em seguida, usar o banco de dados do Sqoop tooexport dados tooan SQL Azure.
* [Carregar dados tooHDInsight][hdinsight-upload-data]: encontrar outros métodos para carregar o armazenamento de BLOBs do Azure/tooHDInsight de dados.

## <a name="appendix-a---a-powershell-sample"></a>Apêndice A - um exemplo do PowerShell
exemplo do PowerShell Olá executa Olá etapas a seguir:

1. Conecte-se tooAzure.
2. Crie um grupo de recursos do Azure. Para obter mais informações, consulte [Usando o PowerShell do Azure com o Gerenciador de Recursos do Azure](../powershell-azure-resource-manager.md)
3. Crie um servidor de Banco de Dados SQL do Azure, um banco de dados SQL do Azure e duas tabelas. 
   
    Se você usar o SQL Server em vez disso, use Olá instruções toocreate Olá tabelas seguintes:
   
        CREATE TABLE [dbo].[log4jlogs](
         [t1] [nvarchar](50),
         [t2] [nvarchar](50),
         [t3] [nvarchar](50),
         [t4] [nvarchar](50),
         [t5] [nvarchar](50),
         [t6] [nvarchar](50),
         [t7] [nvarchar](50))
   
        CREATE TABLE [dbo].[mobiledata](
         [clientid] [nvarchar](50),
         [querytime] [nvarchar](50),
         [market] [nvarchar](50),
         [deviceplatform] [nvarchar](50),
         [devicemake] [nvarchar](50),
         [devicemodel] [nvarchar](50),
         [state] [nvarchar](50),
         [country] [nvarchar](50),
         [querydwelltime] [float],
         [sessionid] [bigint],
         [sessionpagevieworder][bigint])
   
    tabelas e o banco de dados do hello mais fácil maneira tooexamine Olá é toouse Visual Studio. servidor de banco de dados de saudação e o banco de dados de saudação podem ser examinadas usando Olá portal do Azure.
4. Crie um cluster HDInsight.
   
    cluster de saudação tooexamine, você pode usar o hello portal do Azure ou o Azure PowerShell.
5. Pré-processe o arquivo de dados de origem de saudação.
   
    Neste tutorial, você pode exportar um arquivo de log log4j (um arquivo delimitado) e um banco de dados do Hive tabela tooan SQL Azure. Olá arquivo delimitado é chamado */example/data/sample.log*. Anteriormente no tutorial hello, você viu alguns exemplos de log4j logs. No arquivo de log hello, há algumas linhas vazias e alguns toothese semelhantes de linhas:
   
        java.lang.Exception: 2012-02-03 20:11:35 SampleClass2 [FATAL] unrecoverable system problem at id 609774657
            at com.osa.mocklogger.MockLogger$2.run(MockLogger.java:83)
   
    Isso é bom para obter outros exemplos que usam esses dados, mas é necessário remover essas exceções antes podemos importar no banco de dados do SQL Azure hello ou SQL Server. Exportação de Sqoop falha se houver uma cadeia de caracteres vazia ou uma linha com menos elementos que número de saudação de campos definidos na tabela de banco de dados do SQL Azure hello. tabela de log4jlogs Olá tem 7 campos de tipo de cadeia de caracteres.
   
    Este procedimento cria um novo arquivo em cluster Olá: tutorials/usesqoop/data/sample.log. tooexamine arquivo de dados modificados hello, você pode usar o hello portal do Azure, uma ferramenta de Gerenciador de armazenamento do Azure ou do PowerShell do Azure. [Introdução ao HDInsight] [ hdinsight-get-started] tem um código de exemplo para usar o Azure PowerShell toodownload um arquivo e exibir o conteúdo do arquivo hello.
6. Exporte um banco de dados de SQL do Azure de toohello do arquivo de dados.
   
    arquivo de origem de saudação é tutorials/usesqoop/data/sample.log. Olá tabela onde Olá dados exportados toois chamado log4jlogs.
   
   > [!NOTE]
   > Diferente de informações da cadeia de conexão, etapas Olá nesta seção devem funcionar para um banco de dados do SQL Azure ou SQL Server. Essas etapas foram testadas usando Olá a seguinte configuração:
   > 
   > * **Configuração de ponto para site de rede virtual do Azure**: uma rede virtual conectado tooa cluster HDInsight saudação do SQL Server em um datacenter particular. Consulte [configurar uma VPN ponto a Site no Portal de gerenciamento de saudação](../vpn-gateway/vpn-gateway-point-to-site-create.md) para obter mais informações.
   > * **Azure HDInsight 3.1**: confira [Crie clusters Hadoop no HDInsight usando opções de personalização](hdinsight-hadoop-provision-linux-clusters.md) para saber mais sobre a criação de um cluster em uma rede virtual.
   > * **SQL Server 2014**: configurada autenticação tooallow e tooconnect de pacote de configuração de cliente do hello VPN em execução com segurança rede virtual toohello.
   > 
   > 
7. Exporte um banco de dados do Hive tabela toohello SQL Azure.
8. Importe o cluster HDInsight do hello mobiledata tabela toohello.
   
    tooexamine arquivo de dados modificados hello, você pode usar o hello portal do Azure, uma ferramenta de Gerenciador de armazenamento do Azure ou do PowerShell do Azure.  [Introdução ao HDInsight] [ hdinsight-get-started] tem um código de exemplo sobre como usar o Azure PowerShell toodownload um arquivo e exibir o conteúdo do arquivo hello.

### <a name="hello-powershell-sample"></a>exemplo do PowerShell Olá
    # Prepare an Azure SQL database toobe used by hello Sqoop tutorial

    #region - provide hello following values

    $subscriptionID = "<Enter your Azure Subscription ID>"

    $sqlDatabaseLogin = "<Enter a SQL Database Login name>" #SQL Database server login
    $sqlDatabasePassword = "<Enter a Password>"

    $httpUserName = "admin"  #HDInsight cluster username
    $httpPassword = "<Enter a Password>"

    # used for creating Azure service names
    $nameToken = "<Enter an alias>" 
    $namePrefix = $nameToken.ToLower() + (Get-Date -Format "MMdd")
    #endregion

    #region - variables

    # Resource group variables
    $resourceGroupName = $namePrefix + "rg"
    $location = "East US 2" # used by all Azure services defined in this tutorial

    # SQL database varialbes
    $sqlDatabaseServerName = $namePrefix + "sqldbserver"
    $sqlDatabaseName = $namePrefix + "sqldb"
    $sqlDatabaseConnectionString = "Data Source=$sqlDatabaseServerName.database.windows.net;Initial Catalog=$sqlDatabaseName;User ID=$sqlDatabaseLogin;Password=$sqlDatabasePassword;Encrypt=true;Trusted_Connection=false;"
    $sqlDatabaseMaxSizeGB = 10

    # Used for retrieving external IP address and creating firewall rules
    $ipAddressRestService = "http://bot.whatismyipaddress.com"
    $fireWallRuleName = "UseSqoop"

    # Used for creating tables and clustered indexes
    $cmdCreateLog4jTable = "CREATE TABLE [dbo].[log4jlogs](
        [t1] [nvarchar](50),
        [t2] [nvarchar](50),
        [t3] [nvarchar](50),
        [t4] [nvarchar](50),
        [t5] [nvarchar](50),
        [t6] [nvarchar](50),
        [t7] [nvarchar](50))"

    $cmdCreateLog4jClusteredIndex = "CREATE CLUSTERED INDEX log4jlogs_clustered_index on log4jlogs(t1)"

    $cmdCreateMobileTable = " CREATE TABLE [dbo].[mobiledata](
    [clientid] [nvarchar](50),
    [querytime] [nvarchar](50),
    [market] [nvarchar](50),
    [deviceplatform] [nvarchar](50),
    [devicemake] [nvarchar](50),
    [devicemodel] [nvarchar](50),
    [state] [nvarchar](50),
    [country] [nvarchar](50),
    [querydwelltime] [float],
    [sessionid] [bigint],
    [sessionpagevieworder][bigint])"

    $cmdCreateMobileDataClusteredIndex = "CREATE CLUSTERED INDEX mobiledata_clustered_index on mobiledata(clientid)"

    # HDInsight variables
    $hdinsightClusterName = $namePrefix + "hdi"
    $defaultStorageAccountName = $namePrefix + "store"
    $defaultBlobContainerName = $hdinsightClusterName
    #endregion

    # Treat all errors as terminating
    $ErrorActionPreference = "Stop"

    #region - Connect tooAzure subscription
    Write-Host "`nConnecting tooyour Azure subscription ..." -ForegroundColor Green
    try{Get-AzureRmContext}
    catch{Login-AzureRmAccount}
    #endregion

    #region - Create Azure resouce group
    Write-Host "`nCreating an Azure resource group ..." -ForegroundColor Green
    try{
        Get-AzureRmResourceGroup -Name $resourceGroupName
    }
    catch{
        New-AzureRmResourceGroup -Name $resourceGroupName -Location $location
    }
    #endregion

    #region - Create Azure SQL database server
    Write-Host "`nCreating an Azure SQL Database server ..." -ForegroundColor Green
    try{
        Get-AzureRmSqlServer -ServerName $sqlDatabaseServerName -ResourceGroupName $resourceGroupName}
    catch{
        Write-Host "`nCreating SQL Database server ..."  -ForegroundColor Green

        $sqlDatabasePW = ConvertTo-SecureString -String $sqlDatabasePassword -AsPlainText -Force
        $credential = New-Object System.Management.Automation.PSCredential($sqlDatabaseLogin,$sqlDatabasePW)

        $sqlDatabaseServerName = (New-AzureRmSqlServer `
                                    -ResourceGroupName $resourceGroupName `
                                    -ServerName $sqlDatabaseServerName `
                                    -SqlAdministratorCredentials $credential `
                                    -Location $location).ServerName
        Write-Host "`tThe new SQL database server name is $sqlDatabaseServerName." -ForegroundColor Cyan

        Write-Host "`nCreating firewall rule, $fireWallRuleName ..." -ForegroundColor Green
        $workstationIPAddress = Invoke-RestMethod $ipAddressRestService
        New-AzureRmSqlServerFirewallRule `
            -ResourceGroupName $resourceGroupName `
            -ServerName $sqlDatabaseServerName `
            -FirewallRuleName "$fireWallRuleName-workstation" `
            -StartIpAddress $workstationIPAddress `
            -EndIpAddress $workstationIPAddress

        #tooallow other Azure services tooaccess hello server add a firewall rule and set both hello StartIpAddress and EndIpAddress too0.0.0.0. 
        #Note that this allows Azure traffic from any Azure subscription tooaccess hello server.
        New-AzureRmSqlServerFirewallRule `
            -ResourceGroupName $resourceGroupName `
            -ServerName $sqlDatabaseServerName `
            -FirewallRuleName "$fireWallRuleName-Azureservices" `
            -StartIpAddress "0.0.0.0" `
            -EndIpAddress "0.0.0.0"
    }

    #endregion

    #region - Create and validate Azure SQL database
    Write-Host "`nCreating an Azure SQL database ..." -ForegroundColor Green

    try {
        Get-AzureRmSqlDatabase `
            -ResourceGroupName $resourceGroupName `
            -ServerName $sqlDatabaseServerName `
            -DatabaseName $sqlDatabaseName
    }
    catch {
        Write-Host "`nCreating SQL Database, $sqlDatabaseName ..."  -ForegroundColor Green
        New-AzureRMSqlDatabase `
            -ResourceGroupName $resourceGroupName `
            -ServerName $sqlDatabaseServerName `
            -DatabaseName $sqlDatabaseName `
            -Edition "Standard" `
            -RequestedServiceObjectiveName "S1"
    }

    #endregion

    #region - Create tables
    Write-Host "Creating hello log4jlogs table and hello mobiledata table ..." -ForegroundColor Green

    $conn = New-Object System.Data.SqlClient.SqlConnection
    $conn.ConnectionString = $sqlDatabaseConnectionString
    $conn.Open()

    # Create hello log4jlogs table and index
    $cmd = New-Object System.Data.SqlClient.SqlCommand
    $cmd.Connection = $conn
    $cmd.CommandText = $cmdCreateLog4jTable
    $ret = $cmd.ExecuteNonQuery()
    $cmd.CommandText = $cmdCreateLog4jClusteredIndex
    $cmd.ExecuteNonQuery()

    # Create hello mobiledata table and index
    $cmd.CommandText = $cmdCreateMobileTable
    $cmd.ExecuteNonQuery()
    $cmd.CommandText = $cmdCreateMobileDataClusteredIndex
    $cmd.ExecuteNonQuery()

    $conn.close()

    #endregion


    #region - Create HDInsight cluster

    Write-Host "Creating hello HDInsight cluster and hello dependent services ..." -ForegroundColor Green

    # Create hello default storage account
    New-AzureRmStorageAccount `
        -ResourceGroupName $resourceGroupName `
        -Name $defaultStorageAccountName `
        -Location $location `
        -Type Standard_LRS

    # Create hello default Blob container
    $defaultStorageAccountKey = (Get-AzureRmStorageAccountKey `
                                    -ResourceGroupName $resourceGroupName `
                                    -Name $defaultStorageAccountName)[0].Value
    $defaultStorageAccountContext = New-AzureStorageContext `
                                        -StorageAccountName $defaultStorageAccountName `
                                        -StorageAccountKey $defaultStorageAccountKey 
    New-AzureStorageContainer `
        -Name $defaultBlobContainerName `
        -Context $defaultStorageAccountContext 

    # Create hello HDInsight cluster
    $pw = ConvertTo-SecureString -String $httpPassword -AsPlainText -Force
    $httpCredential = New-Object System.Management.Automation.PSCredential($httpUserName,$pw)

    New-AzureRmHDInsightCluster `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $HDInsightClusterName `
        -Location $location `
        -ClusterType Hadoop `
        -OSType Windows `
        -ClusterSizeInNodes 2 `
        -HttpCredential $httpCredential `
        -DefaultStorageAccountName "$defaultStorageAccountName.blob.core.windows.net" `
        -DefaultStorageAccountKey $defaultStorageAccountKey `
        -DefaultStorageContainer $defaultBlobContainerName 

    # Validate hello cluster
    Get-AzureRmHDInsightCluster -ClusterName $hdinsightClusterName
    #endregion

    #region - pre-process hello source file

    Write-Host "Preprocessing hello source file ..." -ForegroundColor Green

    # This procedure creates a new file with $destBlobName
    $sourceBlobName = "example/data/sample.log"
    $destBlobName = "tutorials/usesqoop/data/sample.log"

    # Define hello connection string
    $storageConnectionString = "DefaultEndpointsProtocol=https;AccountName=$defaultStorageAccountName;AccountKey=$defaultStorageAccountKey"

    # Create block blob objects referencing hello source and destination blob.
    $storageAccount = [Microsoft.WindowsAzure.Storage.CloudStorageAccount]::Parse($storageConnectionString)
    $storageClient = $storageAccount.CreateCloudBlobClient();
    $storageContainer = $storageClient.GetContainerReference($defaultBlobContainerName)
    $sourceBlob = $storageContainer.GetBlockBlobReference($sourceBlobName)
    $destBlob = $storageContainer.GetBlockBlobReference($destBlobName)

    # Define a MemoryStream and a StreamReader for reading from hello source file
    $stream = New-Object System.IO.MemoryStream
    $stream = $sourceBlob.OpenRead()
    $sReader = New-Object System.IO.StreamReader($stream)

    # Define a MemoryStream and a StreamWriter for writing into hello destination file
    $memStream = New-Object System.IO.MemoryStream
    $writeStream = New-Object System.IO.StreamWriter $memStream

    # Pre-process hello source blob
    $exString = "java.lang.Exception:"
    while(-Not $sReader.EndOfStream){
        $line = $sReader.ReadLine()
        $split = $line.Split(" ")

        # remove hello "java.lang.Exception" from hello first element of hello array
        # for example: java.lang.Exception: 2012-02-03 19:11:02 SampleClass8 [WARN] problem finding id 153454612
        if ($split[0] -eq $exString){
            #create a new ArrayList tooremove $split[0]
            $newArray = [System.Collections.ArrayList] $split
            $newArray.Remove($exString)

            # update $split and $line
            $split = $newArray
            $line = $newArray -join(" ")
        }

        # remove hello lines that has less than 7 elements
        if ($split.count -ge 7){
            write-host $line
            $writeStream.WriteLine($line)
        }
    }

    # Write toohello destination blob
    $writeStream.Flush()
    $memStream.Seek(0, "Begin")
    $destBlob.UploadFromStream($memStream)

    #endregion

    #region - export a log file from hello cluster toohello SQL database

    Write-Host "Preprocessing hello source file ..." -ForegroundColor Green

    $tableName_log4j = "log4jlogs"

    # Connection string for Azure SQL Database.
    # Comment if using SQL Server
    $connectionString = "jdbc:sqlserver://$sqlDatabaseServerName.database.windows.net;user=$sqlDatabaseLogin@$sqlDatabaseServerName;password=$sqlDatabasePassword;database=$sqlDatabaseName"
    # Connection string for SQL Server.
    # Uncomment if using SQL Server.
    #$connectionString = "jdbc:sqlserver://$sqlDatabaseServerName;user=$sqlDatabaseLogin;password=$sqlDatabasePassword;database=$sqlDatabaseName"

    $exportDir_log4j = "/tutorials/usesqoop/data"

    # Submit a Sqoop job
    $sqoopDef = New-AzureRmHDInsightSqoopJobDefinition `
        -Command "export --connect $connectionString --table $tableName_log4j --export-dir $exportDir_log4j --input-fields-terminated-by \0x20 -m 1"
    $sqoopJob = Start-AzureRmHDInsightJob `
                    -ClusterName $hdinsightClusterName `
                    -HttpCredential $httpCredential `
                    -JobDefinition $sqoopDef #-Debug -Verbose
    Wait-AzureRmHDInsightJob `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $hdinsightClusterName `
        -HttpCredential $httpCredential `
        -JobId $sqoopJob.JobId

    Write-Host "Standard Error" -BackgroundColor Green
    Get-AzureRmHDInsightJobOutput -ResourceGroupName $resourceGroupName -ClusterName $hdinsightClusterName -DefaultStorageAccountName $defaultStorageAccountName -DefaultStorageAccountKey $defaultStorageAccountKey -DefaultContainer $defaultBlobContainerName -HttpCredential $httpCredential -JobId $sqoopJob.JobId -DisplayOutputType StandardError
    Write-Host "Standard Output" -BackgroundColor Green
    Get-AzureRmHDInsightJobOutput -ResourceGroupName $resourceGroupName -ClusterName $hdinsightClusterName -DefaultStorageAccountName $defaultStorageAccountName -DefaultStorageAccountKey $defaultStorageAccountKey -DefaultContainer $defaultBlobContainerName -HttpCredential $httpCredential -JobId $sqoopJob.JobId -DisplayOutputType StandardOutput

    #endregion

    #region - export a Hive table

    $tableName_mobile = "mobiledata"
    $exportDir_mobile = "/hive/warehouse/hivesampletable"

    $sqoopDef = New-AzureRmHDInsightSqoopJobDefinition `
        -Command "export --connect $connectionString --table $tableName_mobile --export-dir $exportDir_mobile --fields-terminated-by \t -m 1"
    $sqoopJob = Start-AzureRmHDInsightJob `
                    -ClusterName $hdinsightClusterName `
                    -HttpCredential $httpCredential `
                    -JobDefinition $sqoopDef #-Debug -Verbose

    Wait-AzureRmHDInsightJob `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $hdinsightClusterName `
        -HttpCredential $httpCredential `
        -JobId $sqoopJob.JobId

    Write-Host "Standard Error" -BackgroundColor Green
    Get-AzureRmHDInsightJobOutput `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $hdinsightClusterName `
        -DefaultStorageAccountName $defaultStorageAccountName `
        -DefaultStorageAccountKey $defaultStorageAccountKey `
        -DefaultContainer $defaultBlobContainerName `
        -HttpCredential $httpCredential `
        -JobId $sqoopJob.JobId `
        -DisplayOutputType StandardError

    Write-Host "Standard Output" -BackgroundColor Green
    Get-AzureRmHDInsightJobOutput `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $hdinsightClusterName `
        -DefaultStorageAccountName $defaultStorageAccountName `
        -DefaultStorageAccountKey $defaultStorageAccountKey `
        -DefaultContainer $defaultBlobContainerName `
        -HttpCredential $httpCredential `
        -JobId $sqoopJob.JobId `
        -DisplayOutputType StandardOutput

    #endregion

    #region - import a database

    $targetDir_mobile = "/tutorials/usesqoop/importeddata/"

    $sqoopDef = New-AzureRmHDInsightSqoopJobDefinition `
        -Command "import --connect $connectionString --table $tableName_mobile --target-dir $targetDir_mobile --fields-terminated-by \t --lines-terminated-by \n -m 1"

    $sqoopJob = Start-AzureRmHDInsightJob `
                    -ClusterName $hdinsightClusterName `
                    -HttpCredential $httpCredential `
                    -JobDefinition $sqoopDef #-Debug -Verbose

    Wait-AzureRmHDInsightJob `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $hdinsightClusterName `
        -HttpCredential $httpCredential `
        -JobId $sqoopJob.JobId

    Write-Host "Standard Error" -BackgroundColor Green
    Get-AzureRmHDInsightJobOutput `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $hdinsightClusterName `
        -DefaultStorageAccountName $defaultStorageAccountName `
        -DefaultStorageAccountKey $defaultStorageAccountKey `
        -DefaultContainer $defaultBlobContainerName `
        -HttpCredential $httpCredential `
        -JobId $sqoopJob.JobId `
        -DisplayOutputType StandardError

    Write-Host "Standard Output" -BackgroundColor Green
    Get-AzureRmHDInsightJobOutput `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $hdinsightClusterName `
        -DefaultStorageAccountName $defaultStorageAccountName `
        -DefaultStorageAccountKey $defaultStorageAccountKey `
        -DefaultContainer $defaultBlobContainerName `
        -HttpCredential $httpCredential `
        -JobId $sqoopJob.JobId `
        -DisplayOutputType StandardOutput

    #endregion



[azure-management-portal]: https://portal.azure.com/

[hdinsight-versions]:  hdinsight-component-versioning.md
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-storage]: ../hdinsight-hadoop-use-blob-storage.md
[hdinsight-analyze-flight-data]: hdinsight-analyze-flight-delay-data.md
[hdinsight-use-oozie]: hdinsight-use-oozie.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md

[sqldatabase-get-started]: ../sql-database/sql-database-get-started.md
[sqldatabase-create-configue]: ../sql-database/sql-database-get-started.md

[powershell-start]: http://technet.microsoft.com/library/hh847889.aspx
[powershell-install]: /powershell/azureps-cmdlets-docs
[powershell-script]: http://technet.microsoft.com/library/ee176949.aspx

[sqoop-user-guide-1.4.4]: https://sqoop.apache.org/docs/1.4.4/SqoopUserGuide.html
