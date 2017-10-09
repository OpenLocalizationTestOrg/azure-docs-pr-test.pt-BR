---
title: aaaMigrate tooAzure Gerenciador de recursos de ferramentas para HDInsight | Microsoft Docs
description: Como as ferramentas de toomigrate tooAzure Gerenciador de recursos de desenvolvimento para clusters de HDInsight
services: hdinsight
editor: cgronlun
manager: jhubbard
author: nitinme
documentationcenter: 
ms.assetid: 05efedb5-6456-4552-87ff-156d77fbe2e1
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: c087ae63d2544e5badae6be9c258f783aa92e2ef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="migrating-tooazure-resource-manager-based-development-tools-for-hdinsight-clusters"></a>Ferramentas de desenvolvimento com base no Gerenciador de recursos tooAzure migrando para clusters de HDInsight

O HDInsight está preterindo as ferramentas baseadas em ASM (Azure Service Manager) para o HDInsight. Se você tiver sido usar Azure PowerShell, CLI do Azure ou Olá HDInsight .NET SDK toowork com clusters de HDInsight, você está toouse incentivados hello Azure Resource Manager ARM versões do PowerShell, CLI e .NET SDK no futuro. Este artigo fornece ponteiros sobre como toomigrate toohello nova baseado em ARM abordagem. Onde aplicável, este artigo também aponta diferenças Olá entre Olá abordagens ASM e ARM para HDInsight.

> [!IMPORTANT]
> suporte a saudação ASM com base em PowerShell, CLI, e .NET SDK será descontinuado em **1 de janeiro de 2017**.
> 
> 

## <a name="migrating-azure-cli-tooazure-resource-manager"></a>Migrando tooAzure de CLI do Azure Resource Manager
Olá CLI do Azure agora padrões tooAzure modo de Resource Manager (ARM), a menos que você estiver atualizando de uma instalação anterior; Nesse caso, talvez seja necessário toouse Olá `azure config mode arm` modo do comando tooswitch tooARM.

comandos de saudação que Olá CLI do Azure acompanha toowork HDInsight usando o gerenciamento de serviço do Azure (ASM) são Olá mesmo ao usar ARM; No entanto alguns parâmetros e comutadores podem ter novos nomes, e há muitos novos parâmetros disponíveis ao usar ARM. Por exemplo, você pode agora usar `azure hdinsight cluster create` toospecify Olá rede Virtual do Azure que deve ser criado em um cluster ou Hive e Oozie metastore informações.

Os comandos básicos para trabalhar com o HDInsight por meio do Azure Resource Manager são:

* `azure hdinsight cluster create` - cria um novo cluster HDInsight
* `azure hdinsight cluster delete` - exclui um cluster HDInsight existente
* `azure hdinsight cluster show` - exibe informações sobre um cluster existente
* `azure hdinsight cluster list` - lista os clusters HDInsight de sua assinatura do Azure

Saudação de uso `-h` alternar parâmetros de saudação tooinspect e as opções disponíveis para cada comando.

### <a name="new-commands"></a>Novos comandos
Os novos comandos disponíveis no Azure Resource Manager são:

* `azure hdinsight cluster resize`-dinamicamente as alterações Olá número de nós de trabalho no cluster Olá
* `azure hdinsight cluster enable-http-access`-permite que o cluster de toohello acesso HTTPs (em por padrão)
* `azure hdinsight cluster disable-http-access`-desativa o cluster de toohello acesso HTTPs
* `azure hdinsight script-action` - fornece comandos para criar/gerenciar as Ações de Script em um cluster
* `azure hdinsight config`-fornece comandos para criar um arquivo de configuração que pode ser usado com hello `hdinsight cluster create` comando tooprovide informações de configuração.

### <a name="deprecated-commands"></a>Comandos preteridos
Se você usar o hello `azure hdinsight job` comandos toosubmit trabalhos tooyour HDInsight cluster não estiverem disponíveis por meio de comandos ARM hello. Se você precisar tooprogrammatically tooHDInsight de trabalhos de envio de scripts, em vez disso, você deve usar Olá APIs de REST fornecida pelo HDInsight. Para obter mais informações sobre como enviar trabalhos usando APIs REST, consulte Olá documentos a seguir.

* [Executar trabalhos do MapReduce com o Hadoop no HDInsight usando a cURL](hdinsight-hadoop-use-mapreduce-curl.md)
* [Executar consultas do Hive com o Hadoop no HDInsight usando a cURL](hdinsight-hadoop-use-hive-curl.md)
* [Executar trabalhos do Pig com o Hadoop no HDInsight usando a cURL](hdinsight-hadoop-use-pig-curl.md)

Para obter informações sobre outra maneiras de toorun MapReduce, Hive e Pig interativamente, consulte [Use MapReduce com Hadoop no HDInsight](hdinsight-use-mapreduce.md), [uso de Hive do Hadoop no HDInsight](hdinsight-use-hive.md), e [usar o Pig com Hadoop no HDInsight](hdinsight-use-pig.md).

### <a name="examples"></a>Exemplos
**Criando um cluster**

* Comando antigo (ASM) - `azure hdinsight cluster create myhdicluster --location northeurope --osType linux --storageAccountName mystorage --storageAccountKey <storagekey> --storageContainer mycontainer --userName admin --password mypassword --sshUserName sshuser --sshPassword mypassword`
* Novo comando (ARM) - `azure hdinsight cluster create myhdicluster -g myresourcegroup --location northeurope --osType linux --clusterType hadoop --defaultStorageAccountName mystorage --defaultStorageAccountKey <storagekey> --defaultStorageContainer mycontainer --userName admin -password mypassword --sshUserName sshuser --sshPassword mypassword`

**Excluindo um cluster**

* Comando antigo (ASM) - `azure hdinsight cluster delete myhdicluster`
* Novo comando (ARM) - `azure hdinsight cluster delete mycluster -g myresourcegroup`

**Listar clusters**

* Comando antigo (ASM) - `azure hdinsight cluster list`
* Novo comando (ARM) - `azure hdinsight cluster list`

> [!NOTE]
> Para o comando lista hello, especificando hello usando o recurso grupo `-g` retornará apenas os clusters Olá no grupo de recursos especificado hello.
> 
> 

**Mostrar informações de cluster**

* Comando antigo (ASM) - `azure hdinsight cluster show myhdicluster`
* Novo comando (ARM) - `azure hdinsight cluster show myhdicluster -g myresourcegroup`

## <a name="migrating-azure-powershell-tooazure-resource-manager"></a>Migração do Azure PowerShell tooAzure Gerenciador de recursos
Olá informações gerais sobre o Azure PowerShell no modo do hello Azure Resource Manager (ARM) podem ser encontradas em [usando o PowerShell do Azure com o Azure Resource Manager](../powershell-azure-resource-manager.md).

Olá cmdlets do Azure PowerShell ARM pode ser instalada lado a lado com hello ASM cmdlets. cmdlets de saudação de dois modos de saudação podem ser diferenciados por seus nomes.  o modo ARM Olá tem *AzureRmHDInsight* em nomes de cmdlet Olá comparando muito*AzureHDInsight* no modo ASM hello.  Por exemplo, *New-AzureRmHDInsightCluster* versus *New-AzureHDInsightCluster*. Os parâmetros e as opções podem ter nomes novos, e há muitos novos parâmetros disponíveis ao usar o ARM.  Por exemplo, vários cmdlets exigem uma nova opção chamada *-ResourceGroupName*. 

Antes de usar cmdlets do HDInsight Olá, você deve conectar tooyour conta do Azure e criar um novo grupo de recursos:

* Login-AzureRmAccount ou [Select-AzureRmProfile](https://msdn.microsoft.com/library/mt619310.aspx). Veja [Autenticando uma entidade de serviço com o Azure Resource Manager](../azure-resource-manager/resource-group-authenticate-service-principal.md)
* [New-AzureRmResourceGroup](https://msdn.microsoft.com/library/mt603739.aspx)

### <a name="renamed-cmdlets"></a>Cmdlets renomeados
Olá toolist cmdlets de HDInsight ASM no console do Windows PowerShell:

    help *azurermhdinsight*

Olá tabela a seguir lista Olá ASM cmdlets e os nomes no modo ARM hello:

| Cmdlets do ASM | Cmdlets do ARM |
| --- | --- |
| Add-AzureHDInsightConfigValues |[Add-AzureRmHDInsightConfigValues](https://msdn.microsoft.com/library/mt603530.aspx) |
| Add-AzureHDInsightMetastore |[Add-AzureRmHDInsightMetastore](https://msdn.microsoft.com/library/mt603670.aspx) |
| Add-AzureHDInsightScriptAction |[Add-AzureRmHDInsightScriptAction](https://msdn.microsoft.com/library/mt603527.aspx) |
| Add-AzureHDInsightStorage |[Add-AzureRmHDInsightStorage](https://msdn.microsoft.com/library/mt619445.aspx) |
| Get-AzureHDInsightCluster |[Get-AzureRmHDInsightCluster](https://msdn.microsoft.com/library/mt619371.aspx) |
| Get-AzureHDInsightJob |[Get-AzureRmHDInsightJob](https://msdn.microsoft.com/library/mt603590.aspx) |
| Get-AzureHDInsightJobOutput |[Get-AzureRmHDInsightJobOutput](https://msdn.microsoft.com/library/mt603793.aspx) |
| Get-AzureHDInsightProperties |[Get-AzureRmHDInsightProperties](https://msdn.microsoft.com/library/mt603546.aspx) |
| Grant-AzureHDInsightHttpServicesAccess |[Grant-AzureRmHDInsightHttpServicesAccess](https://msdn.microsoft.com/library/mt619407.aspx) |
| Grant-AzureHdinsightRdpAccess |[Grant-AzureRmHDInsightRdpServicesAccess](https://msdn.microsoft.com/library/mt603717.aspx) |
| Invoke-AzureHDInsightHiveJob |[Invoke-AzureRmHDInsightHiveJob](https://msdn.microsoft.com/library/mt603593.aspx) |
| New-AzureHDInsightCluster |[New-AzureRmHDInsightCluster](https://msdn.microsoft.com/library/mt619331.aspx) |
| New-AzureHDInsightClusterConfig |[New-AzureRmHDInsightClusterConfig](https://msdn.microsoft.com/library/mt603700.aspx) |
| New-AzureHDInsightHiveJobDefinition |[New-AzureRmHDInsightHiveJobDefinition](https://msdn.microsoft.com/library/mt619448.aspx) |
| New-AzureHDInsightMapReduceJobDefinition |[New-AzureRmHDInsightMapReduceJobDefinition](https://msdn.microsoft.com/library/mt603626.aspx) |
| New-AzureHDInsightPigJobDefinition |[New-AzureRmHDInsightPigJobDefinition](https://msdn.microsoft.com/library/mt603671.aspx) |
| New-AzureHDInsightSqoopJobDefinition |[New-AzureRmHDInsightSqoopJobDefinition](https://msdn.microsoft.com/library/mt608551.aspx) |
| New-AzureHDInsightStreamingMapReduceJobDefinition |[New-AzureRmHDInsightStreamingMapReduceJobDefinition](https://msdn.microsoft.com/library/mt603626.aspx) |
| Remove-AzureHDInsightCluster |[Remove-AzureRmHDInsightCluster](https://msdn.microsoft.com/library/mt619431.aspx) |
| Revoke-AzureHDInsightHttpServicesAccess |[Revoke-AzureRmHDInsightHttpServicesAccess](https://msdn.microsoft.com/library/mt619375.aspx) |
| Revoke-AzureHdinsightRdpAccess |[Revoke-AzureRmHDInsightRdpServicesAccess](https://msdn.microsoft.com/library/mt603523.aspx) |
| Set-AzureHDInsightClusterSize |[Set-AzureRmHDInsightClusterSize](https://msdn.microsoft.com/library/mt603513.aspx) |
| Set-AzureHDInsightDefaultStorage |[Set-AzureRmHDInsightDefaultStorage](https://msdn.microsoft.com/library/mt603486.aspx) |
| Start-AzureHDInsightJob |[Start-AzureRmHDInsightJob](https://msdn.microsoft.com/library/mt603798.aspx) |
| Stop-AzureHDInsightJob |[Stop-AzureRmHDInsightJob](https://msdn.microsoft.com/library/mt619424.aspx) |
| Use-AzureHDInsightCluster |[Use-AzureRmHDInsightCluster](https://msdn.microsoft.com/library/mt619442.aspx) |
| Wait-AzureHDInsightJob |[Wait-AzureRmHDInsightJob](https://msdn.microsoft.com/library/mt603834.aspx) |

### <a name="new-cmdlets"></a>Novos cmdlets
Olá seguem Olá novos cmdlets que só estão disponíveis no modo ARM hello. 

**Cmdlets relacionados à ação de script:**

* **Get-AzureRmHDInsightPersistedScriptAction**: Olá obtém persistentes ações de script para um cluster de lista em ordem cronológica e obtém os detalhes para uma ação de script persistentes especificado. 
* **Get-AzureRmHDInsightScriptActionHistory**: obtém o histórico de ação de script hello para um cluster e lista em ordem cronológica inversa ou obtém os detalhes de uma ação de script executado anteriormente. 
* **Remove-AzureRmHDInsightPersistedScriptAction**: remove uma ação de script persistente de um cluster HDInsight.
* **Conjunto AzureRmHDInsightPersistedScriptAction**: define um toobe de ação do script executado anteriormente uma ação de script persistentes.
* **Enviar AzureRmHDInsightScriptAction**: envia um novo cluster de HDInsight do Azure de tooan de ação de script. 

Para obter mais informações de uso, veja [Personalizar clusters HDInsight baseados em Linux usando a Ação de Script](hdinsight-hadoop-customize-cluster-linux.md).

**Cmdlets relacionados à identidade do cluster:**

* **Adicionar AzureRmHDInsightClusterIdentity**: adiciona um objeto de configuração de cluster do cluster identidade tooa para que hello cluster HDInsight pode acessar repositórios do Azure Data Lake. Veja [Criar um cluster HDInsight com o Repositório Data Lake usando o Azure PowerShell](../data-lake-store/data-lake-store-hdinsight-hadoop-use-powershell.md).

### <a name="examples"></a>Exemplos
**Criar cluster**

Comando antigo (ASM): 

    New-AzureHDInsightCluster `
        -Name $clusterName `
        -Location $location `
        -DefaultStorageAccountName "$storageAccountName.blob.core.windows.net" `
        -DefaultStorageAccountKey $storageAccountKey `
        -DefaultStorageContainerName $containerName `
        -ClusterSizeInNodes 2 `
        -ClusterType Hadoop `
        -OSType Linux `
        -Version "3.2" `
        -Credential $httpCredential `
        -SshCredential $sshCredential

Novo comando (ARM):

    New-AzureRmHDInsightCluster `
        -ClusterName $clusterName `
        -ResourceGroupName $resourceGroupName `
        -Location $location `
        -DefaultStorageAccountName "$storageAccountName.blob.core.windows.net" `
        -DefaultStorageAccountKey $storageAccountKey `
        -DefaultStorageContainer $containerName  `
        -ClusterSizeInNodes 2 `
        -ClusterType Hadoop `
        -OSType Linux `
        -Version "3.2" `
        -HttpCredential $httpcredentials `
        -SshCredential $sshCredentials


**Excluir cluster**

Comando antigo (ASM):

    Remove-AzureHDInsightCluster -name $clusterName 

Novo comando (ARM):

    Remove-AzureRmHDInsightCluster -ResourceGroupName $resourceGroupName -ClusterName $clusterName 

**Listar clusters**

Comando antigo (ASM):

    Get-AzureHDInsightCluster

Novo comando (ARM):

    Get-AzureRmHDInsightCluster 

**Mostrar cluster**

Comando antigo (ASM):

    Get-AzureHDInsightCluster -Name $clusterName

Novo comando (ARM):

    Get-AzureRmHDInsightCluster -ResourceGroupName $resourceGroupName -clusterName $clusterName


#### <a name="other-samples"></a>Outras amostras
* [Criar clusters HDInsight](hdinsight-hadoop-create-linux-clusters-azure-powershell.md)
* [Enviar trabalhos Hive](hdinsight-hadoop-use-hive-powershell.md)
* [Enviar trabalhos do Pig](hdinsight-hadoop-use-pig-powershell.md)
* [Enviar trabalhos do Sqoop](hdinsight-hadoop-use-sqoop-powershell.md)

## <a name="migrating-toohello-arm-based-hdinsight-net-sdk"></a>Migrando toohello baseado em ARM HDInsight .NET SDK
Olá baseados no gerenciamento de serviço do Azure [(ASM) HDInsight .NET SDK](https://msdn.microsoft.com/library/azure/mt416619.aspx) agora está obsoleta. São incentivado toouse Olá baseados no gerenciamento de recursos do Azure [(ARM) HDInsight .NET SDK](https://msdn.microsoft.com/library/azure/mt271028.aspx). Olá seguintes pacotes de HDInsight com base em ASM estão sendo substituídos.

* `Microsoft.WindowsAzure.Management.HDInsight`
* `Microsoft.Hadoop.Client`

Esta seção fornece ponteiros toomore informações sobre como tooperform certas tarefas usando Olá SDK baseado em ARM.

| Como … usando Olá baseado em ARM HDInsight SDK | Links |
| --- | --- |
| Criar clusters HDInsight usando o SDK do .NET |Veja [Criar clusters HDInsight usando o SDK do .NET](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md) |
| Personalizar um cluster usando a Ação de Script com o SDK do .NET |Veja [Personalizar os clusters HDInsight do Linux usando a Ação de Script](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md#use-script-action) |
| Autenticar aplicativos de forma interativa usando o Azure Active Directory com o SDK do .NET |Veja [Executar consultas do Hive usando o SDK do .NET](hdinsight-hadoop-use-hive-dotnet-sdk.md). trecho de código Olá neste artigo usa o método de autenticação interativa do hello. |
| Autenticar aplicativos de forma não interativa usando o Azure Active Directory com o SDK do .NET |Veja [Criar aplicativos não interativos para o HDInsight](hdinsight-create-non-interactive-authentication-dotnet-applications.md) |
| Enviar um trabalho do Hive usando o SDK do .NET |Veja [Enviar trabalhos do Hive](hdinsight-hadoop-use-hive-dotnet-sdk.md) |
| Enviar um trabalho do Pig usando o SDK do .NET |Veja [Enviar trabalhos do Pig](hdinsight-hadoop-use-pig-dotnet-sdk.md) |
| Enviar um trabalho do Sqoop usando o SDK do .NET |Veja [Enviar trabalhos do Sqoop](hdinsight-hadoop-use-sqoop-dotnet-sdk.md) |
| Listar clusters HDInsight usando o SDK do .NET |Veja [Listar os clusters HDInsight](hdinsight-administer-use-dotnet-sdk.md#list-clusters) |
| Escalar clusters HDInsight usando o SDK do .NET |Veja [Escalar clusters HDInsight](hdinsight-administer-use-dotnet-sdk.md#scale-clusters) |
| Grant/revoke acesso tooHDInsight clusters usando o SDK do .NET |Consulte [clusters de tooHDInsight acesso Grant/revoke](hdinsight-administer-use-dotnet-sdk.md#grantrevoke-access) |
| Atualizar credenciais de usuário HTTP de clusters HDInsight usando o SDK do .NET |Veja [Atualizar credenciais de usuário HTTP de clusters HDInsight](hdinsight-administer-use-dotnet-sdk.md#update-http-user-credentials) |
| Localizar a conta de armazenamento padrão Olá para clusters HDInsight usando o SDK do .NET |Consulte [localizar a conta de armazenamento padrão Olá para clusters de HDInsight](hdinsight-administer-use-dotnet-sdk.md#find-the-default-storage-account) |
| Excluir clusters HDInsight usando o SDK do .NET |Veja [Excluir clusters HDInsight](hdinsight-administer-use-dotnet-sdk.md#delete-clusters) |

### <a name="examples"></a>Exemplos
Estes são alguns exemplos de como uma operação é executada usando hello SDK do ASM e trecho de código equivalentes Olá para Olá SDK baseado em ARM.

**Criando um cliente CRUD do cluster**

* Comando antigo (ASM)
  
        //Certificate auth
        //This logs hello application in using a subscription administration certificate, which is not offered in Azure Resource Manager (ARM)
  
        const string subid = "454467d4-60ca-4dfd-a556-216eeeeeeee1";
        var cred = new HDInsightCertificateCredential(new Guid(subid), new X509Certificate2(@"path\to\certificate.cer"));
        var client = HDInsightClient.Connect(cred);
* Novo comando (ARM) (Autorização de entidade de serviço)
  
        //Service principal auth
        //This will log hello application in as itself, rather than on behalf of a specific user.
        //For details, including how tooset up hello application, see:
        //   https://azure.microsoft.com/en-us/documentation/articles/hdinsight-create-non-interactive-authentication-dotnet-applications/
  
        var authFactory = new AuthenticationFactory();
  
        var account = new AzureAccount { Type = AzureAccount.AccountType.ServicePrincipal, Id = clientId };
  
        var env = AzureEnvironment.PublicEnvironments[EnvironmentName.AzureCloud];
  
        var accessToken = authFactory.Authenticate(account, env, tenantId, secretKey, ShowDialog.Never).AccessToken;
  
        var creds = new TokenCloudCredentials(subId.ToString(), accessToken);
  
        _hdiManagementClient = new HDInsightManagementClient(creds);
* Novo comando (ARM) (Autorização de usuário)
  
        //User auth
        //This will log hello application in on behalf of hello user.
        //hello end-user will see a login popup.
  
        var authFactory = new AuthenticationFactory();
  
        var account = new AzureAccount { Type = AzureAccount.AccountType.User, Id = username };
  
        var env = AzureEnvironment.PublicEnvironments[EnvironmentName.AzureCloud];
  
        var accessToken = authFactory.Authenticate(account, env, AuthenticationFactory.CommonAdTenant, password, ShowDialog.Auto).AccessToken;
  
        var creds = new TokenCloudCredentials(subId.ToString(), accessToken);
  
        _hdiManagementClient = new HDInsightManagementClient(creds);

**Criando um cluster**

* Comando antigo (ASM)
  
        var clusterInfo = new ClusterCreateParameters
                    {
                        Name = dnsName,
                        DefaultStorageAccountKey = key,
                        DefaultStorageContainer = defaultStorageContainer,
                        DefaultStorageAccountName = storageAccountDnsName,
                        ClusterSizeInNodes = 1,
                        ClusterType = type,
                        Location = "West US",
                        UserName = "admin",
                        Password = "*******",
                        Version = version,
                        HeadNodeSize = NodeVMSize.Large,
                    };
        clusterInfo.CoreConfiguration.Add(new KeyValuePair<string, string>("config1", "value1"));
        client.CreateCluster(clusterInfo);
* Novo comando (ARM)
  
        var clusterCreateParameters = new ClusterCreateParameters
            {
                Location = "West US",
                ClusterType = "Hadoop",
                Version = "3.1",
                OSType = OSType.Linux,
                DefaultStorageAccountName = "mystorage.blob.core.windows.net",
                DefaultStorageAccountKey =
                    "O9EQvp3A3AjXq/W27rst1GQfLllhp0gUeiUUn2D8zX2lU3taiXSSfqkZlcPv+nQcYUxYw==",
                UserName = "hadoopuser",
                Password = "*******",
                HeadNodeSize = "ExtraLarge",
                RdpUsername = "hdirp",
                RdpPassword = ""*******",
                RdpAccessExpiry = new DateTime(2025, 3, 1),
                ClusterSizeInNodes = 5
            };
        var coreConfigs = new Dictionary<string, string> {{"config1", "value1"}};
        clusterCreateParameters.Configurations.Add(ConfigurationKey.CoreSite, coreConfigs);

**Habilitando o acesso HTTP**

* Comando antigo (ASM)
  
        client.EnableHttp(dnsName, "West US", "admin", "*******");
* Novo comando (ARM)
  
        var httpParams = new HttpSettingsParameters
        {
               HttpUserEnabled = true,
               HttpUsername = "admin",
               HttpPassword = "*******",
        };
        client.Clusters.ConfigureHttpSettings(resourceGroup, dnsname, httpParams);

**Excluindo um cluster**

* Comando antigo (ASM)
  
        client.DeleteCluster(dnsName);
* Novo comando (ARM)
  
        client.Clusters.Delete(resourceGroup, dnsname);

