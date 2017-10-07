---
title: "aaaUse toocreate de modelos do Azure HDInsight e repositório Data Lake | Microsoft Docs"
description: "Use o Gerenciador de recursos do Azure modelos toocreate e usar clusters de HDInsight com repositório Azure Data Lake"
services: data-lake-store,hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 8ef8152f-2121-461e-956c-51c55144919d
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/04/2017
ms.author: nitinme
ms.openlocfilehash: eb88a626f2837dcc29295f3f73a91757059c3bb8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-hdinsight-cluster-with-data-lake-store-using-azure-resource-manager-template"></a>Criar o cluster HDInsight com o Data Lake Store usando o modelo do Resource Manager do Azure
> [!div class="op_single_selector"]
> * [Usando o Portal](data-lake-store-hdinsight-hadoop-use-portal.md)
> * [Usando o PowerShell (para o armazenamento padrão)](data-lake-store-hdinsight-hadoop-use-powershell-for-default-storage.md)
> * [Usando o PowerShell (para o armazenamento adicional)](data-lake-store-hdinsight-hadoop-use-powershell.md)
> * [Usando o Gerenciador de Recursos](data-lake-store-hdinsight-hadoop-use-resource-manager-template.md)
>
>

Saiba como toouse do Azure PowerShell tooconfigure um HDInsight cluster com repositório Azure Data Lake, **como armazenamento adicional**.

Para tipos de cluster compatíveis, o Data Lake Store pode ser usado como um armazenamento padrão ou uma conta de armazenamento adicional. Quando o repositório Data Lake é usado como armazenamento adicional, conta de armazenamento padrão Olá para clusters de saudação ainda estará Blobs de armazenamento do Azure (WASB) e arquivos relacionados ao cluster de saudação (como logs, etc.) são gravados ainda armazenamento padrão de toohello, enquanto os dados de saudação que você deseja tooprocess podem ser armazenados em uma conta do repositório Data Lake. Usando o repositório Data Lake como uma conta de armazenamento adicional não afeta o desempenho e o hello capacidade tooread/gravação toohello armazenamento de cluster hello.

## <a name="using-data-lake-store-for-hdinsight-cluster-storage"></a>Usando o Data Lake Store para armazenamento do cluster HDInsight

Aqui estão algumas considerações importantes para usar o HDInsight com o Data Lake Store:

* Clusters de HDInsight toocreate opção com acesso tooData Lake repositório como armazenamento padrão está disponível para HDInsight versão 3.5 e 3.6.

* Clusters de HDInsight toocreate opção com acesso tooData Lake repositório como armazenamento adicional está disponível para HDInsight versões 3.2, 3.4, 3.5 e 3.6.

Neste artigo, provisionaremos um cluster Hadoop com o Repositório Data Lake como armazenamento adicional. Para obter instruções sobre como toocreate um Hadoop de cluster com o repositório Data Lake como armazenamento padrão, consulte [criar um cluster HDInsight com repositório Data Lake usando o Portal do Azure](data-lake-store-hdinsight-hadoop-use-portal.md).

## <a name="prerequisites"></a>Pré-requisitos
Antes de começar este tutorial, você deve ter o seguinte hello:

* **Uma assinatura do Azure**. Consulte [Obter avaliação gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/).
* **Azure PowerShell 1.0 ou superior**. Consulte [como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview).
* **Entidade de serviço do Azure Active Directory**. As etapas deste tutorial fornecem instruções sobre como toocreate uma entidade de serviço no AD do Azure. No entanto, você deve ser um toocreate capaz do AD do Azure administrador toobe uma entidade de serviço. Se você for um administrador do AD do Azure, você pode ignorar esse pré-requisito e continuar com o tutorial hello.

    **Se você não for um administrador do AD do Azure**, não será capaz de tooperform Olá etapas necessárias toocreate uma entidade de serviço. Nesse caso, o administrador do Azure AD deverá primeiro criar uma entidade de serviço antes de criar um cluster HDInsight com Data Lake Store. Além disso, Olá entidade de serviço deve ser criada usando um certificado, conforme descrito em [criar uma entidade de serviço com certificado](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-certificate-from-certificate-authority).

## <a name="create-an-hdinsight-cluster-with-azure-data-lake-store"></a>Criar um cluster HDInsight com o Azure Data Lake Store
modelo do Gerenciador de recursos de saudação e Olá pré-requisitos para usar o modelo de hello, estão disponíveis no GitHub em [implantar um cluster HDInsight Linux com o novo repositório do Data Lake](https://github.com/Azure/azure-quickstart-templates/tree/master/201-hdinsight-datalake-store-azure-storage). Siga as instruções de Olá fornecidas no toocreate link um cluster HDInsight com repositório Azure Data Lake como armazenamento adicional da saudação.

instruções de Olá Olá link mencionados acima exigem o PowerShell. Antes de iniciar as instruções, verifique se que você fizer logon no tooyour conta do Azure. Na área de trabalho, abra uma nova janela do PowerShell do Azure e insira Olá trechos de código a seguir. Quando solicitada toolog, certifique-se de você fazer logon como uma saudação admininistrators/proprietário da assinatura:

```
# Log in tooyour Azure account
Login-AzureRmAccount

# List all hello subscriptions associated tooyour account
Get-AzureRmSubscription

# Select a subscription
Set-AzureRmContext -SubscriptionId <subscription ID>
```

## <a name="upload-sample-data-toohello-azure-data-lake-store"></a>Carregar repositório exemplo dados toohello Azure Data Lake
modelo do Gerenciador de recursos de saudação cria uma nova conta do repositório Data Lake e associa ao cluster do HDInsight hello. Agora, você deve carregar alguns dados de exemplo toohello repositório Data Lake. Você precisará esses dados posteriormente em trabalhos toorun tutorial Olá de um cluster HDInsight que acessam dados em Olá repositório Data Lake. Para obter instruções sobre como tooupload dados, consulte [carregar um arquivo tooyour repositório Data Lake](data-lake-store-get-started-portal.md#uploaddata). Se você estiver procurando por alguns tooupload de dados de exemplo, você pode obter Olá **ambulância dados** pasta Olá [repositório Git do Azure Data Lake](https://github.com/Azure/usql/tree/master/Examples/Samples/Data/AmbulanceData).

## <a name="set-relevant-acls-on-hello-sample-data"></a>Definir ACLs relevantes em dados de exemplo hello
toomake se os dados de exemplo hello que você carregar são acessíveis do cluster do HDInsight hello, você deve garantir que o aplicativo hello AD do Azure que é a identidade tooestablish usado entre o cluster do HDInsight hello e repositório Data Lake tenha acesso toohello arquivo/pasta é a tentativa de tooaccess. toodo isso, execute Olá etapas a seguir.

1. Localize o nome de saudação do hello aplicativo AD do Azure que está associado ao cluster HDInsight e Olá repositório Data Lake. Toolook unidirecional para nome hello é criada usando o modelo do Gerenciador de recursos de saudação folha de cluster tooopen Olá HDInsight, clique em Olá **Cluster AAD identidade** guia e procure o valor de saudação do **entidade de serviço Nome de exibição**.
2. Agora, fornecem acesso toothis aplicativo AD do Azure no hello arquivo/pasta que você deseja tooaccess do cluster do HDInsight hello. o direito de saudação de tooset ACLs Olá arquivo/pasta no repositório Data Lake, consulte [proteção de dados no repositório Data Lake](data-lake-store-secure-data.md#filepermissions).

## <a name="run-test-jobs-on-hello-hdinsight-cluster-toouse-hello-data-lake-store"></a>Executar trabalhos de teste em Olá HDInsight cluster toouse Olá repositório Data Lake
Depois de configurar um cluster HDInsight, você pode executar trabalhos de teste em Olá cluster tootest que Olá HDInsight cluster pode acessar o repositório Data Lake. toodo assim, iremos executar um trabalho de Hive de exemplo que cria uma tabela usando dados de exemplo hello que você carregou anteriormente repositório tooyour Data Lake.

Nesta seção, você vai SSH em um cluster HDInsight Linux e execução Olá um exemplo de consulta de Hive. Se você está usando um cliente Windows, é recomendável usar o **PuTTY**, que pode ser baixado de [http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html).

Para saber mais sobre a utilização do PuTTY, confira [Usar SSH com o Hadoop baseado em Linux no HDInsight no Windows ](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).

1. Uma vez conectado, inicie Olá CLI do Hive usando Olá comando a seguir:

   ```
   hive
   ```
2. Usando Olá CLI, insira Olá seguindo as instruções toocreate uma nova tabela nomeada **veículos** com dados de exemplo hello Olá repositório Data Lake:

   ```
   DROP TABLE vehicles;
   CREATE EXTERNAL TABLE vehicles (str string) LOCATION 'adl://<mydatalakestore>.azuredatalakestore.net:443/';
   SELECT * FROM vehicles LIMIT 10;
   ```

   Você verá uma saída semelhante toohello a seguir:

   ```
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
   ```


## <a name="access-data-lake-store-using-hdfs-commands"></a>Repositório Data Lake usando comandos do HDFS
Quando você tiver configurado o repositório Data Lake do toouse de cluster de HDInsight hello, você pode usar comandos de shell do hello HDFS tooaccess Olá repositório.

Nesta seção, você vai SSH em um cluster HDInsight Linux e execução Olá comandos HDFS. Se você está usando um cliente Windows, é recomendável usar o **PuTTY**, que pode ser baixado de [http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html).

Para saber mais sobre a utilização do PuTTY, confira [Usar SSH com o Hadoop baseado em Linux no HDInsight no Windows ](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).

Uma vez conectado, use Olá arquivos HDFS filesystem comando toolist Olá no hello repositório Data Lake a seguir.

```
hdfs dfs -ls adl://<Data Lake Store account name>.azuredatalakestore.net:443/
```

Isso deve listar arquivo hello que você carregou anteriormente repositório toohello Data Lake.

```
15/09/17 21:41:15 INFO web.CaboWebHdfsFileSystem: Replacing original urlConnectionFactory with org.apache.hadoop.hdfs.web.URLConnectionFactory@21a728d6
Found 1 items
-rwxrwxrwx   0 NotSupportYet NotSupportYet     671388 2015-09-16 22:16 adl://mydatalakestore.azuredatalakestore.net:443/mynewfolder
```

Você também pode usar o hello `hdfs dfs -put` comando tooupload toohello alguns arquivos repositório Data Lake e, em seguida, usar `hdfs dfs -ls` tooverify arquivos Olá foram carregados com êxito.


## <a name="next-steps"></a>Próximas etapas
* [Copiar dados do repositório Azure armazenamento de Blobs tooData Lake](data-lake-store-copy-data-wasb-distcp.md)
