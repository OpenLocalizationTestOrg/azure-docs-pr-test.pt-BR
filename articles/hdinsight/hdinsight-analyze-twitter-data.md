---
title: aaaAnalyze dados Twitter com Hadoop no HDInsight - Azure | Microsoft Docs
description: "Saiba como toouse Hive tooanalyze Twitter dados no Hadoop em HDInsight toofind Olá frequência de uso de uma palavra específica."
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 78e4ea33-9714-424d-ac07-3d60ecaebf2e
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ROBOTS: NOINDEX
ms.openlocfilehash: 40c0a1afbc1fff10c070d22a99cd9d32d42f230a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-twitter-data-using-hive-in-hdinsight"></a>Analisar dados do Twitter usando o Hive no HDInsight
Sites sociais são uma saudação principais forças para adoção de dados grandes. APIs públicas fornecidas por sites, como o Twitter, são uma fonte útil de dados para analisar e compreender as tendências populares.
Neste tutorial, você obterá tweets usando um API de streaming de Twitter e, em seguida, usar o Apache Hive no Azure HDInsight tooget uma lista de usuários do Twitter que enviou Olá tweets mais que continha uma palavra específica.

> [!IMPORTANT]
> Olá, as etapas neste documento exigem um cluster HDInsight baseados no Windows. Linux é Olá sistema operacional somente de usado no HDInsight versão 3.4 ou posterior. Para obter mais informações, confira [baixa do HDInsight no Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement). Para etapas específicas tooa baseados em Linux cluster consulte [Twitter analisar dados usando Hive no HDInsight (Linux)](hdinsight-analyze-twitter-data-linux.md).

## <a name="prerequisites"></a>Pré-requisitos
Antes de começar este tutorial, você deve ter o seguinte hello:

* **Uma estação de trabalho** com o PowerShell do Azure instalado e configurado.

    tooexecute scripts do Windows PowerShell, você deve executar o Azure PowerShell como administrador e definir a política de execução Olá muito*RemoteSigned*. Consulte [Executar scripts do Windows PowerShell][powershell-script].

    Antes de executar scripts do Windows PowerShell, verifique se que você está conectado tooyour assinatura do Azure usando Olá cmdlet a seguir:

    ```powershell
    Login-AzureRmAccount
    ```

    Se você tiver várias assinaturas do Azure, use Olá assinatura atual do cmdlet tooset Olá a seguir:

    ```powershell
    Select-AzureRmSubscription -SubscriptionID <Azure Subscription ID>
    ```

    > [!IMPORTANT]
    > O suporte do Azure PowerShell para gerenciar os recursos do HDInsight usando o Gerenciador de Serviços do Azure está **preterido** e foi removido em 1º de janeiro de 2017. Olá etapas para esse documento use Olá novos cmdlets do HDInsight que funcionam com o Gerenciador de recursos do Azure.
    >
    > Siga as etapas de saudação em [instalar e configurar o Azure PowerShell](/powershell/azureps-cmdlets-docs) tooinstall Olá última versão do PowerShell do Azure. Se você tiver scripts que toobe necessidade modificado toouse Olá novos cmdlets que funcionam com o Gerenciador de recursos do Azure, consulte [tooAzure migrando desenvolvimento baseado no Gerenciador de recursos de ferramentas para clusters de HDInsight](hdinsight-hadoop-development-using-azure-resource-manager.md) para obter mais informações.

* **Um cluster Azure HDInsight**. Para obter informações sobre como provisionar um cluster, consulte [Introdução ao HDInsight][hdinsight-get-started] ou [Provisionar clusters HDInsight][hdinsight-provision]. Você precisará nome do cluster hello mais tarde no tutorial de saudação.

Olá tabela a seguir lista os arquivos de saudação usados neste tutorial:

| Arquivos | Descrição |
| --- | --- |
| /tutorials/twitter/data/tweets.txt |dados de origem Olá para o trabalho de Hive hello. |
| /tutorials/twitter/output |Olá a pasta de saída para o trabalho de Hive hello. Olá nome de arquivo de saída padrão Hive trabalho é **000000_0**. |
| tutorials/twitter/twitter.hql |arquivo de script HiveQL Hello. |
| /tutorials/twitter/jobstatus |Olá status do trabalho Hadoop. |

## <a name="get-twitter-feed"></a>Obter feed do Twitter
Neste tutorial, você usará Olá [APIs de streaming do Twitter][twitter-streaming-api]. Olá específico Twitter streaming API que você usará é [status/filtro][twitter-statuses-filter].

> [!NOTE]
> Um arquivo contendo 10.000 tweets e o arquivo de script de Hive hello (abordado na próxima seção, Olá) foi carregado em um contêiner de Blob público. Você pode ignorar esta seção se você quiser toouse Olá carregar arquivos.

[TWEETS dados](https://dev.twitter.com/docs/platform-objects/tweets) são armazenados em formato de notação JSON (JavaScript Object) Olá que contém uma estrutura aninhada complexa. Em vez de escrever várias linhas de código usando uma linguagem de programação convencional, você pode transformar essa estrutura aninhada em uma tabela do Hive para que possa ser consultada por uma linguagem semelhante à SQL chamada HiveQL.

Twitter usa OAuth tooprovide autorizado acesso tooits API. OAuth é um protocolo de autenticação que permite que os usuários tooapprove aplicativos tooact em seu nome sem compartilhar sua senha. Mais informações podem ser encontradas em [oauth.net](http://oauth.net/) ou em Olá excelente [tooOAuth de guia do Iniciante](http://hueniverse.com/oauth/) de Hueniverse.

saudação de primeira etapa toouse OAuth é toocreate um novo aplicativo no site do desenvolvedor do Twitter hello.

**toocreate um aplicativo do Twitter**

1. Entrar muito[https://apps.twitter.com/](https://apps.twitter.com/). Clique em Olá **inscrever-se agora** link se você não tiver uma conta do Twitter.
2. Clique em **Criar Novo Aplicativo**.
3. Digite o **Nome**, a **Descrição** e o **Site**. Você pode fazer backup de uma URL para Olá **site** campo. Olá, a tabela a seguir mostra algumas toouse de valores de exemplo:

   | Campo | Valor |
   | --- | --- |
   |  Nome |MyHDInsightApp |
   |  Descrição |MyHDInsightApp |
   |  Site |http://www.myhdinsightapp.com |
4. Marque **Sim, eu concordo** e, em seguida, clique em **Criar seu aplicativo do Twitter**.
5. Clique em Olá **permissões** guia saudação padrão permissão é **somente leitura**. Isso é suficiente para este tutorial.
6. Clique em Olá **chaves e Tokens de acesso** guia.
7. Clique em **Criar meu token de acesso**.
8. Clique em **teste OAuth** no canto superior direito de saudação da página de saudação.
9. Anote a **chave do consumidor**, o **Segredo do consumidor**, o **Token de acesso** e o **Segredo do token de acesso**. Você precisará valores hello mais tarde no tutorial de saudação.

Neste tutorial, você usará a chamada de serviço da web do Windows PowerShell toomake hello. Para ver um exemplo de C# .NET, consulte [Analisar sentimento no Twitter em tempo real com HBase no HDInsight][hdinsight-hbase-twitter-sentiment]. Olá outras chamadas de serviço web popular ferramenta toomake é [ *Curl*][curl]. O Curl pode ser baixado [aqui][curl-download].

> [!NOTE]
> Quando você usar o comando de ondulação Olá no Windows, use aspas duplas em vez de aspas simples para os valores de opção hello.

**tweets tooget**

1. Abra Olá Windows PowerShell Integrated Scripting ISE (ambiente). (Na tela inicial do Windows 8 hello, digite **PowerShell_ISE** e, em seguida, clique em **o Windows PowerShell ISE**. Consulte [Iniciar o Windows PowerShell no Windows 8 e no Windows][powershell-start].)
2. Copie Olá script a seguir no painel de script hello:

    ```powershell
    #region - variables and constants
    $clusterName = "<HDInsightClusterName>" # Enter hello HDInsight cluster name

    # Enter hello OAuth information for your Twitter application
    $oauth_consumer_key = "<TwitterAppConsumerKey>";
    $oauth_consumer_secret = "<TwitterAppConsumerSecret>";
    $oauth_token = "<TwitterAppAccessToken>";
    $oauth_token_secret = "<TwitterAppAccessTokenSecret>";

    $destBlobName = "tutorials/twitter/data/tweets.txt" # This script saves hello tweets into this blob.

    $trackString = "Azure, Cloud, HDInsight" # This script gets hello tweets containing these keywords.
    $track = [System.Uri]::EscapeDataString($trackString);
    $lineMax = 10000  # hello script will get this number of tweets. It is about 3 minutes every 100 lines.
    #endregion

    #region - Connect tooAzure subscription
    Write-Host "`nConnecting tooyour Azure subscription ..." -ForegroundColor Green
    Login-AzureRmAccount
    #endregion

    #region - Create a block blob object for writing tweets into Blob storage
    Write-Host "Get hello default storage account name and Blob container name using hello cluster name ..." -ForegroundColor Green
    $myCluster = Get-AzureRmHDInsightCluster -Name $clusterName
    $resourceGroupName = $myCluster.ResourceGroup
    $storageAccountName = $myCluster.DefaultStorageAccount.Replace(".blob.core.windows.net", "")
    $containerName = $myCluster.DefaultStorageContainer
    Write-Host "`tThe storage account name is $storageAccountName." -ForegroundColor Yellow
    Write-Host "`tThe blob container name is $containerName." -ForegroundColor Yellow

    Write-Host "Define hello Azure storage connection string ..." -ForegroundColor Green
    $storageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $storageAccountName)[0].Value
    $storageConnectionString = "DefaultEndpointsProtocol=https;AccountName=$storageAccountName;AccountKey=$storageAccountKey"
    Write-Host "`tThe connection string is $storageConnectionString." -ForegroundColor Yellow

    Write-Host "Create block blob object ..." -ForegroundColor Green
    $storageAccount = [Microsoft.WindowsAzure.Storage.CloudStorageAccount]::Parse($storageConnectionString)
    $storageClient = $storageAccount.CreateCloudBlobClient();
    $storageContainer = $storageClient.GetContainerReference($containerName)
    $destBlob = $storageContainer.GetBlockBlobReference($destBlobName)
    #end region

    # region - Format OAuth strings
    Write-Host "Format oauth strings ..." -ForegroundColor Green
    $oauth_nonce = [System.Convert]::ToBase64String([System.Text.Encoding]::ASCII.GetBytes([System.DateTime]::Now.Ticks.ToString()));
    $ts = [System.DateTime]::UtcNow - [System.DateTime]::ParseExact("01/01/1970", "dd/MM/yyyy", $null)
    $oauth_timestamp = [System.Convert]::ToInt64($ts.TotalSeconds).ToString();

    $signature = "POST&";
    $signature += [System.Uri]::EscapeDataString("https://stream.twitter.com/1.1/statuses/filter.json") + "&";
    $signature += [System.Uri]::EscapeDataString("oauth_consumer_key=" + $oauth_consumer_key + "&");
    $signature += [System.Uri]::EscapeDataString("oauth_nonce=" + $oauth_nonce + "&");
    $signature += [System.Uri]::EscapeDataString("oauth_signature_method=HMAC-SHA1&");
    $signature += [System.Uri]::EscapeDataString("oauth_timestamp=" + $oauth_timestamp + "&");
    $signature += [System.Uri]::EscapeDataString("oauth_token=" + $oauth_token + "&");
    $signature += [System.Uri]::EscapeDataString("oauth_version=1.0&");
    $signature += [System.Uri]::EscapeDataString("track=" + $track);

    $signature_key = [System.Uri]::EscapeDataString($oauth_consumer_secret) + "&" + [System.Uri]::EscapeDataString($oauth_token_secret);

    $hmacsha1 = new-object System.Security.Cryptography.HMACSHA1;
    $hmacsha1.Key = [System.Text.Encoding]::ASCII.GetBytes($signature_key);
    $oauth_signature = [System.Convert]::ToBase64String($hmacsha1.ComputeHash([System.Text.Encoding]::ASCII.GetBytes($signature)));

    $oauth_authorization = 'OAuth ';
    $oauth_authorization += 'oauth_consumer_key="' + [System.Uri]::EscapeDataString($oauth_consumer_key) + '",';
    $oauth_authorization += 'oauth_nonce="' + [System.Uri]::EscapeDataString($oauth_nonce) + '",';
    $oauth_authorization += 'oauth_signature="' + [System.Uri]::EscapeDataString($oauth_signature) + '",';
    $oauth_authorization += 'oauth_signature_method="HMAC-SHA1",'
    $oauth_authorization += 'oauth_timestamp="' + [System.Uri]::EscapeDataString($oauth_timestamp) + '",'
    $oauth_authorization += 'oauth_token="' + [System.Uri]::EscapeDataString($oauth_token) + '",';
    $oauth_authorization += 'oauth_version="1.0"';

    $post_body = [System.Text.Encoding]::ASCII.GetBytes("track=" + $track);
    #endregion

    #region - Read tweets
    Write-Host "Create HTTP web request ..." -ForegroundColor Green
    [System.Net.HttpWebRequest] $request = [System.Net.WebRequest]::Create("https://stream.twitter.com/1.1/statuses/filter.json");
    $request.Method = "POST";
    $request.Headers.Add("Authorization", $oauth_authorization);
    $request.ContentType = "application/x-www-form-urlencoded";
    $body = $request.GetRequestStream();

    $body.write($post_body, 0, $post_body.length);
    $body.flush();
    $body.close();
    $response = $request.GetResponse() ;

    Write-Host "Start stream reading ..." -ForegroundColor Green

    Write-Host "Define a MemoryStream and a StreamWriter for writing ..." -ForegroundColor Green
    $memStream = New-Object System.IO.MemoryStream
    $writeStream = New-Object System.IO.StreamWriter $memStream

    $sReader = New-Object System.IO.StreamReader($response.GetResponseStream())

    $inrec = $sReader.ReadLine()
    $count = 0
    while (($inrec -ne $null) -and ($count -le $lineMax))
    {
        if ($inrec -ne "")
        {
            Write-Host "`n`t $count tweets received." -ForegroundColor Yellow

            $writeStream.WriteLine($inrec)
            $count ++
        }

        $inrec=$sReader.ReadLine()
    }
    #endregion

    #region - Write tweets tooBlob storage
    Write-Host "Write toohello destination blob ..." -ForegroundColor Green
    $writeStream.Flush()
    $memStream.Seek(0, "Begin")
    $destBlob.UploadFromStream($memStream)

    $sReader.close()
    #endregion

    Write-Host "Completed!" -ForegroundColor Green
    ```

3. Defina as variáveis de tooeight cinco primeiros da saudação no script hello:

    Variável|Descrição
    ---|---
    $clusterName|Este é o nome de saudação do cluster do HDInsight Olá onde você deseja que o aplicativo de hello toorun.
    $oauth_consumer_key|Este é o aplicativo do Twitter hello **chave do consumidor** você anotou anteriormente quando você criou o aplicativo do Twitter hello.
    $oauth_consumer_secret|Este é o aplicativo do Twitter hello **segredo do consumidor** você anotou anteriormente.
    $oauth_token|Este é o aplicativo do Twitter hello **token de acesso** você anotou anteriormente.
    $oauth_token_secret|Este é o aplicativo do Twitter hello **segredo do token de acesso** você anotou anteriormente.
    $destBlobName|Este é o nome de blob de saída de hello. valor padrão de saudação é **tutorials/twitter/data/tweets.txt**. Se você alterar o valor padrão de saudação, você precisará scripts de Windows PowerShell Olá tooupdate adequadamente.
    $trackString|serviço web de saudação retornará toothese relacionados de tweets palavras-chave. valor padrão de saudação é **HDInsight do Azure, a nuvem,**. Se você alterar o valor padrão de saudação, você atualizará scripts do Windows PowerShell Olá adequadamente.
    $lineMax|valor de Olá determina quantos script hello de tweets será lida. Leva aproximadamente três minutos tooread 100 tweets. Você pode definir um número maior, mas levará mais toodownload de tempo.

1. Pressione **F5** toorun script de saudação. Se você tiver problemas, como alternativa, selecione todas as linhas de saudação e, em seguida, pressione **F8**.
2. Você deverá ver a mensagem "Concluído!" no final da saudação da saída de hello. Qualquer mensagem de erro será exibida em vermelho.

Como um procedimento de validação, você pode verificar o arquivo de saída de hello, **/tutorials/twitter/data/tweets.txt**, no armazenamento de BLOBs do Azure usando um Gerenciador de armazenamento do Azure ou o PowerShell do Azure. Para um exemplo de script do Windows PowerShell para listagem de arquivos, consulte [Usar o Armazenamento de Blobs com o HDInsight][hdinsight-storage-powershell].

## <a name="create-hiveql-script"></a>Criar o script HiveQL
Usando o PowerShell do Azure, você pode executar várias instruções HiveQL um em uma hora ou instrução de estilo de saudação de pacote em um arquivo de script. Neste tutorial, você irá criar um script HiveQL. arquivo de script Hello deve ser carregado tooAzure armazenamento de Blob. Na próxima seção, Olá, execute o arquivo de script hello usando o PowerShell do Azure.

> [!NOTE]
> arquivo de script de Hive Hello e um arquivo que contém a 10.000 tweets foi carregados em um contêiner de Blob público. Você pode ignorar esta seção se você quiser toouse Olá carregar arquivos.

Olá script HiveQL executará o seguinte hello:

1. **Descartar Olá tweets_raw tabela** no caso de Olá tabela já existir.
2. **Criar tabela de Hive Olá tweets_raw**. Essa seção temporária estruturada tabela contém dados de saudação para mais extrair, transformar e carregar o processamento (ETL). Para obter informações sobre partições, consulte o [tutorial do Hive][apache-hive-tutorial].
3. **Carregar dados** da pasta de origem hello, /tutorials/twitter/data. Olá tweets grande conjunto de dados no formato aninhado de JSON agora foi transformado em uma estrutura de tabela temporária do Hive.
4. **A tabela DROP Olá tweets** no caso de Olá tabela já existir.
5. **Criar tabela de tweets Olá**. Antes que você pode consultar o conjunto de dados do hello tweets usando Hive, é necessário toorun outro processo ETL. Esse processo ETL define um esquema de tabela mais detalhado para dados Olá armazenado na tabela de "twitter_raw" hello.
6. **Insira tabela de substituição**. Esse script de Hive complexas para iniciar um conjunto de trabalhos de MapReduce longo por cluster de Hadoop de saudação. Dependendo de seu conjunto de dados e hello o tamanho do cluster, isso pode levar cerca de 10 minutos.
7. **Insira diretório de substituição**. Execute um arquivo de tooa de conjunto de dados de saudação de consulta e de saída. Essa consulta retornará uma lista de usuários do Twitter que enviou a maioria dos tweets que contêm a palavra de hello "Azure".

**toocreate uma seção de script e carregá-lo tooAzure**

1. Abra o ISE do Windows PowerShell.
2. Copie Olá script a seguir no painel de script hello:

    ```powershell
    #region - variables and constants
    $clusterName = "<Existing HDInsight Cluster Name>" # Enter your HDInsight cluster name
    $subscriptionID = "<Azure Subscription ID>"

    $sourceDataPath = "/tutorials/twitter/data"
    $outputPath = "/tutorials/twitter/output"
    $hqlScriptFile = "tutorials/twitter/twitter.hql"

    $hqlStatements = @"
    set hive.exec.dynamic.partition = true;
    set hive.exec.dynamic.partition.mode = nonstrict;

    DROP TABLE tweets_raw;
    CREATE EXTERNAL TABLE tweets_raw (
        json_response STRING
    )
    STORED AS TEXTFILE LOCATION '$sourceDataPath';

    DROP TABLE tweets;
    CREATE TABLE tweets
    (
        id BIGINT,
        created_at STRING,
        created_at_date STRING,
        created_at_year STRING,
        created_at_month STRING,
        created_at_day STRING,
        created_at_time STRING,
        in_reply_to_user_id_str STRING,
        text STRING,
        contributors STRING,
        retweeted STRING,
        truncated STRING,
        coordinates STRING,
        source STRING,
        retweet_count INT,
        url STRING,
        hashtags array<STRING>,
        user_mentions array<STRING>,
        first_hashtag STRING,
        first_user_mention STRING,
        screen_name STRING,
        name STRING,
        followers_count INT,
        listed_count INT,
        friends_count INT,
        lang STRING,
        user_location STRING,
        time_zone STRING,
        profile_image_url STRING,
        json_response STRING
    );

    FROM tweets_raw
    INSERT OVERWRITE TABLE tweets
    SELECT
        cast(get_json_object(json_response, '$.id_str') as BIGINT),
        get_json_object(json_response, '$.created_at'),
        concat(substr (get_json_object(json_response, '$.created_at'),1,10),' ',
        substr (get_json_object(json_response, '$.created_at'),27,4)),
        substr (get_json_object(json_response, '$.created_at'),27,4),
        case substr (get_json_object(json_response, '$.created_at'),5,3)
            when "Jan" then "01"
            when "Feb" then "02"
            when "Mar" then "03"
            when "Apr" then "04"
            when "May" then "05"
            when "Jun" then "06"
            when "Jul" then "07"
            when "Aug" then "08"
            when "Sep" then "09"
            when "Oct" then "10"
            when "Nov" then "11"
            when "Dec" then "12" end,
        substr (get_json_object(json_response, '$.created_at'),9,2),
        substr (get_json_object(json_response, '$.created_at'),12,8),
        get_json_object(json_response, '$.in_reply_to_user_id_str'),
        get_json_object(json_response, '$.text'),
        get_json_object(json_response, '$.contributors'),
        get_json_object(json_response, '$.retweeted'),
        get_json_object(json_response, '$.truncated'),
        get_json_object(json_response, '$.coordinates'),
        get_json_object(json_response, '$.source'),
        cast (get_json_object(json_response, '$.retweet_count') as INT),
        get_json_object(json_response, '$.entities.display_url'),
        array(
            trim(lower(get_json_object(json_response, '$.entities.hashtags[0].text'))),
            trim(lower(get_json_object(json_response, '$.entities.hashtags[1].text'))),
            trim(lower(get_json_object(json_response, '$.entities.hashtags[2].text'))),
            trim(lower(get_json_object(json_response, '$.entities.hashtags[3].text'))),
            trim(lower(get_json_object(json_response, '$.entities.hashtags[4].text')))),
        array(
            trim(lower(get_json_object(json_response, '$.entities.user_mentions[0].screen_name'))),
            trim(lower(get_json_object(json_response, '$.entities.user_mentions[1].screen_name'))),
            trim(lower(get_json_object(json_response, '$.entities.user_mentions[2].screen_name'))),
            trim(lower(get_json_object(json_response, '$.entities.user_mentions[3].screen_name'))),
            trim(lower(get_json_object(json_response, '$.entities.user_mentions[4].screen_name')))),
        trim(lower(get_json_object(json_response, '$.entities.hashtags[0].text'))),
        trim(lower(get_json_object(json_response, '$.entities.user_mentions[0].screen_name'))),
        get_json_object(json_response, '$.user.screen_name'),
        get_json_object(json_response, '$.user.name'),
        cast (get_json_object(json_response, '$.user.followers_count') as INT),
        cast (get_json_object(json_response, '$.user.listed_count') as INT),
        cast (get_json_object(json_response, '$.user.friends_count') as INT),
        get_json_object(json_response, '$.user.lang'),
        get_json_object(json_response, '$.user.location'),
        get_json_object(json_response, '$.user.time_zone'),
        get_json_object(json_response, '$.user.profile_image_url'),
        json_response
    WHERE (length(json_response) > 500);

    INSERT OVERWRITE DIRECTORY '$outputPath'
    SELECT name, screen_name, count(1) as cc
        FROM tweets
        WHERE text like "%Azure%"
        GROUP BY name,screen_name
        ORDER BY cc DESC LIMIT 10;
    "@
    #endregion

    #region - Connect tooAzure subscription
    Write-Host "`nConnecting tooyour Azure subscription ..." -ForegroundColor Green

    Try{
        Get-AzureRmSubscription
    }
    Catch{
        Login-AzureRmAccount
    }

    Select-AzureRmSubscription -SubscriptionId $subscriptionID

    #endregion

    #region - Create a block blob object for writing hello Hive script file
    Write-Host "Get hello default storage account name and container name based on hello cluster name ..." -ForegroundColor Green
    $myCluster = Get-AzureRmHDInsightCluster -ClusterName $clusterName
    $resourceGroupName = $myCluster.ResourceGroup
    $defaultStorageAccountName = $myCluster.DefaultStorageAccount.Replace(".blob.core.windows.net", "")
    $defaultBlobContainerName = $myCluster.DefaultStorageContainer
    Write-Host "`tThe storage account name is $defaultStorageAccountName." -ForegroundColor Yellow
    Write-Host "`tThe blob container name is $defaultBlobContainerName." -ForegroundColor Yellow

    Write-Host "Define hello connection string ..." -ForegroundColor Green
    $defaultStorageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $defaultStorageAccountName)[0].Value
    $storageConnectionString = "DefaultEndpointsProtocol=https;AccountName=$defaultStorageAccountName;AccountKey=$defaultStorageAccountKey"

    Write-Host "Create block blob objects referencing hello hql script file" -ForegroundColor Green
    $storageAccount = [Microsoft.WindowsAzure.Storage.CloudStorageAccount]::Parse($storageConnectionString)
    $storageClient = $storageAccount.CreateCloudBlobClient();
    $storageContainer = $storageClient.GetContainerReference($defaultBlobContainerName)
    $hqlScriptBlob = $storageContainer.GetBlockBlobReference($hqlScriptFile)

    Write-Host "Define a MemoryStream and a StreamWriter for writing ... " -ForegroundColor Green
    $memStream = New-Object System.IO.MemoryStream
    $writeStream = New-Object System.IO.StreamWriter $memStream
    $writeStream.Writeline($hqlStatements)
    #endregion

    #region - Write hello Hive script file tooBlob storage
    Write-Host "Write toohello destination blob ... " -ForegroundColor Green
    $writeStream.Flush()
    $memStream.Seek(0, "Begin")
    $hqlScriptBlob.UploadFromStream($memStream)
    #endregion

    Write-Host "Completed!" -ForegroundColor Green
    ```

3. Defina primeiro duas variáveis de saudação no script hello:

   | Variável | Descrição |
   | --- | --- |
   |  $clusterName |Insira o nome do cluster HDInsight Olá onde você deseja que o aplicativo de hello toorun. |
   |  $subscriptionID |Insira sua ID da assinatura do Azure. |
   |  $sourceDataPath |Olá local de armazenamento de BLOBs do Azure, onde consultas de Hive Olá lê dados de saudação do. Você não precisa toochange essa variável. |
   |  $outputPath |Olá onde a consultas de Hive Olá produzirá resultados da saudação de local de armazenamento de BLOBs do Azure. Você não precisa toochange essa variável. |
   |  $hqlScriptFile |local de Hello e nome do arquivo Olá Olá HiveQL do arquivo de script. Você não precisa toochange essa variável. |
4. Pressione **F5** toorun script de saudação. Se você tiver problemas, como alternativa, selecione todas as linhas de saudação e, em seguida, pressione **F8**.
5. Você deverá ver a mensagem "Concluído!" no final da saudação da saída de hello. Qualquer mensagem de erro será exibida em vermelho.

Como um procedimento de validação, você pode verificar o arquivo de saída de hello, **/tutorials/twitter/twitter.hql**, no armazenamento de BLOBs do Azure usando um Gerenciador de armazenamento do Azure ou o PowerShell do Azure. Para um exemplo de script do Windows PowerShell para listagem de arquivos, consulte [Usar o Armazenamento de Blobs com o HDInsight][hdinsight-storage-powershell].

## <a name="process-twitter-data-by-using-hive"></a>Processar os dados do Twitter usando o Hive
Você concluiu a todo o trabalho de preparação hello. Agora, você pode invocar o script do Hive hello e Olá resultados da verificação.

### <a name="submit-a-hive-job"></a>Enviar um trabalho do Hive
Use Olá a seguir de script do Windows PowerShell script toorun Olá Hive. Você precisará primeira variável do tooset hello.

> [!NOTE]
> Olá toouse tweets e Olá script HiveQL carregado em duas últimas seções hello, conjunto $hqlScriptFile too"/tutorials/twitter/twitter.hql". Olá toouse aqueles que foram carregados blob público tooa para você, defina $hqlScriptFile muito"wasb://twittertrend@hditutorialdata.blob.core.windows.net/twitter.hql".

```powershell
#region variables and constants
$clusterName = "<Existing Azure HDInsight Cluster Name>"
$httpUserName = "admin"
$httpUserPassword = "<HDInsight Cluster HTTP User Password>"

#use one of hello following
$hqlScriptFile = "wasb://twittertrend@hditutorialdata.blob.core.windows.net/twitter.hql"
$hqlScriptFile = "/tutorials/twitter/twitter.hql"

$statusFolder = "/tutorials/twitter/jobstatus"
#endregion

$myCluster = Get-AzureRmHDInsightCluster -ClusterName $clusterName
$resourceGroupName = $myCluster.ResourceGroup
$defaultStorageAccountName = $myCluster.DefaultStorageAccount.Replace(".blob.core.windows.net", "")
$defaultStorageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $defaultStorageAccountName)[0].Value

$defaultBlobContainerName = $myCluster.DefaultStorageContainer

#region - Invoke Hive
Write-Host "Invoke Hive ... " -ForegroundColor Green

# Create hello HDInsight cluster
$pw = ConvertTo-SecureString -String $httpUserPassword -AsPlainText -Force
$httpCredential = New-Object System.Management.Automation.PSCredential($httpUserName,$pw)

Use-AzureRmHDInsightCluster -ResourceGroupName $resourceGroupName -ClusterName $clusterName -HttpCredential $httpCredential
$response = Invoke-AzureRmHDInsightHiveJob -DefaultStorageAccountName $defaultStorageAccountName -DefaultStorageAccountKey $defaultStorageAccountKey -DefaultContainer $defaultBlobContainerName -file $hqlScriptFile -StatusFolder $statusFolder #-OutVariable $outVariable

Write-Host "Display hello standard error log ... " -ForegroundColor Green
$jobID = ($response | Select-String job_ | Select-Object -First 1) -replace ‘\s*$’ -replace ‘.*\s’
Get-AzureRmHDInsightJobOutput -ClusterName $clusterName -JobId $jobID -DefaultContainer $defaultBlobContainerName -DefaultStorageAccountName $defaultStorageAccountName -DefaultStorageAccountKey $defaultStorageAccountKey -HttpCredential $httpCredential
#endregion
```

### <a name="check-hello-results"></a>Resultados da verificação de saudação
Saudação de uso após a saída de trabalho do Windows PowerShell script toocheck hello Hive. Você precisará primeiro duas variáveis do tooset hello.

```powershell
#region variables and constants
$clusterName = "<Existing Azure HDInsight Cluster Name>"

$blob = "tutorials/twitter/output/000000_0" # hello name of hello blob toobe downloaded.
#endregion

#region - Create an Azure storage context object
Write-Host "Get hello default storage account name and container name based on hello cluster name ..." -ForegroundColor Green
$myCluster = Get-AzureRmHDInsightCluster -ClusterName $clusterName
$resourceGroupName = $myCluster.ResourceGroup
$defaultStorageAccountName = $myCluster.DefaultStorageAccount.Replace(".blob.core.windows.net", "")
$defaultStorageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $defaultStorageAccountName)[0].Value
$defaultBlobContainerName = $myCluster.DefaultStorageContainer

Write-Host "`tThe storage account name is $defaultStorageAccountName." -ForegroundColor Yellow
Write-Host "`tThe blob container name is $defaultBlobContainerName." -ForegroundColor Yellow

Write-Host "Create a context object ... " -ForegroundColor Green
$storageContext = New-AzureStorageContext -StorageAccountName $defaultStorageAccountName -StorageAccountKey $defaultStorageAccountKey
#endregion

#region - Download blob and display blob
Write-Host "Download hello blob ..." -ForegroundColor Green
cd $HOME
Get-AzureStorageBlobContent -Container $defaultBlobContainerName -Blob $blob -Context $storageContext -Force

Write-Host "Display hello output ..." -ForegroundColor Green
Write-Host "==================================" -ForegroundColor Green
cat "./$blob"
Write-Host "==================================" -ForegroundColor Green
#end region
```

> [!NOTE]
> tabela de Hive Olá usa \001 Olá delimitador de campo. delimitador de saudação não estiver visível na saída de hello.

Depois que os resultados de análise de saudação foram colocados no armazenamento de BLOBs do Azure, exportar Olá dados tooan SQL Azure banco de dados/SQL server, exportar Olá dados tooExcel usando o Power Query ou conectar-se os dados do aplicativo toohello usando Olá Hive ODBC Driver. Para obter mais informações, consulte [Sqoop de uso com o HDInsight][hdinsight-use-sqoop], [analisar dados de atraso de voo usando HDInsight][hdinsight-analyze-flight-delay-data], [ Conectar Excel tooHDInsight com o Power Query][hdinsight-power-query], e [tooHDInsight Excel conectar-se com hello Microsoft ODBC Driver Hive][hdinsight-hive-odbc].

## <a name="next-steps"></a>Próximas etapas
Neste tutorial, vimos como tootransform um conjunto de dados JSON não estruturado em um tooquery estruturado de tabela de Hive, explorar e analisar dados do Twitter usando o HDInsight no Azure. toolearn mais, consulte:

* [Introdução ao HDInsight][hdinsight-get-started]
* [Analisar sentimento no Twitter em tempo real com HBase no HDInsight][hdinsight-hbase-twitter-sentiment]
* [Analisar dados de atraso de voo usando o HDInsight][hdinsight-analyze-flight-delay-data]
* [Conectar Excel tooHDInsight com o Power Query][hdinsight-power-query]
* [Conectar Excel tooHDInsight com hello Microsoft ODBC Driver Hive][hdinsight-hive-odbc]
* [Use o Sqoop com o HDInsight][hdinsight-use-sqoop]

[curl]: http://curl.haxx.se
[curl-download]: http://curl.haxx.se/download.html

[apache-hive-tutorial]: https://cwiki.apache.org/confluence/display/Hive/Tutorial

[twitter-streaming-api]: https://dev.twitter.com/docs/streaming-apis
[twitter-statuses-filter]: https://dev.twitter.com/docs/api/1.1/post/statuses/filter

[powershell-start]: http://technet.microsoft.com/library/hh847889.aspx
[powershell-install]: /powershell/azureps-cmdlets-docs
[powershell-script]: http://technet.microsoft.com/library/ee176961.aspx

[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-storage-powershell]:hdinsight-hadoop-use-blob-storage.md#access-blobs-using-azure-powershell
[hdinsight-analyze-flight-delay-data]: hdinsight-analyze-flight-delay-data.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md
[hdinsight-use-sqoop]: hdinsight-use-sqoop.md
[hdinsight-power-query]: hdinsight-connect-excel-power-query.md
[hdinsight-hive-odbc]: hdinsight-connect-excel-hive-odbc-driver.md
[hdinsight-hbase-twitter-sentiment]: hdinsight-hbase-analyze-twitter-sentiment.md
