---
title: "Analisar dados do Twitter com o Apache Hive – Azure HDInsight | Microsoft Docs"
description: "Saiba como usar o Hive e Hadoop no HDInsight para transformar dados brutos do Twitter em uma tabela do Hive pesquisável."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: e1e249ed-5f57-40d6-b3bc-a1b4d9a871d3
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/07/2017
ms.author: larryfr
ms.custom: H1Hack27Feb2017,hdinsightactive
ms.openlocfilehash: b8656123fa9c5158f366872ab050f370080ec18a
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="analyze-twitter-data-using-hive-and-hadoop-on-hdinsight"></a><span data-ttu-id="dc4ce-103">Analisar dados do Twitter usando o Hive e Hadoop no HDInsight</span><span class="sxs-lookup"><span data-stu-id="dc4ce-103">Analyze Twitter data using Hive and Hadoop on HDInsight</span></span>

<span data-ttu-id="dc4ce-104">Saiba como usar o Apache Hive para processar dados do Twitter.</span><span class="sxs-lookup"><span data-stu-id="dc4ce-104">Learn how to use Apache Hive to process Twitter data.</span></span> <span data-ttu-id="dc4ce-105">O resultado será uma lista de usuários do Twitter que enviaram a maioria dos tweets que contêm uma determinada palavra.</span><span class="sxs-lookup"><span data-stu-id="dc4ce-105">The result is a list of Twitter users who sent the most tweets that contain a certain word.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="dc4ce-106">As etapas deste documento foram testadas no HDInsight 3.6.</span><span class="sxs-lookup"><span data-stu-id="dc4ce-106">The steps in this document were tested on HDInsight 3.6.</span></span>
>
> <span data-ttu-id="dc4ce-107">O Linux é o único sistema operacional usado no HDInsight versão 3.4 ou superior.</span><span class="sxs-lookup"><span data-stu-id="dc4ce-107">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="dc4ce-108">Para obter mais informações, confira [baixa do HDInsight no Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="dc4ce-108">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <a name="get-the-data"></a><span data-ttu-id="dc4ce-109">Obter os dados</span><span class="sxs-lookup"><span data-stu-id="dc4ce-109">Get the data</span></span>

<span data-ttu-id="dc4ce-110">O Twitter permite que você recupere os [dados de cada tweet](https://dev.twitter.com/docs/platform-objects/tweets) como um documento JSON (JavaScript Object Notation) por meio de uma API REST.</span><span class="sxs-lookup"><span data-stu-id="dc4ce-110">Twitter allows you to retrieve the [data for each tweet](https://dev.twitter.com/docs/platform-objects/tweets) as a JavaScript Object Notation (JSON) document through a REST API.</span></span> <span data-ttu-id="dc4ce-111">[OAuth](http://oauth.net) é necessário para autenticação na API.</span><span class="sxs-lookup"><span data-stu-id="dc4ce-111">[OAuth](http://oauth.net) is required for authentication to the API.</span></span>

### <a name="create-a-twitter-application"></a><span data-ttu-id="dc4ce-112">Criar um aplicativo do Twitter</span><span class="sxs-lookup"><span data-stu-id="dc4ce-112">Create a Twitter application</span></span>

1. <span data-ttu-id="dc4ce-113">Em um navegador da Web, entre em [https://apps.twitter.com/](https://apps.twitter.com/).</span><span class="sxs-lookup"><span data-stu-id="dc4ce-113">From a web browser, sign in to [https://apps.twitter.com/](https://apps.twitter.com/).</span></span> <span data-ttu-id="dc4ce-114">Clique no link **Inscreva-se agora** se você não tem uma conta do Twitter.</span><span class="sxs-lookup"><span data-stu-id="dc4ce-114">Click the **Sign-up now** link if you don't have a Twitter account.</span></span>

2. <span data-ttu-id="dc4ce-115">Clique em **Criar Novo Aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="dc4ce-115">Click **Create New App**.</span></span>

3. <span data-ttu-id="dc4ce-116">Digite o **Nome**, a **Descrição** e o **Site**.</span><span class="sxs-lookup"><span data-stu-id="dc4ce-116">Enter **Name**, **Description**, **Website**.</span></span> <span data-ttu-id="dc4ce-117">Você pode fazer uma URL para o campo **Site** .</span><span class="sxs-lookup"><span data-stu-id="dc4ce-117">You can make up a URL for the **Website** field.</span></span> <span data-ttu-id="dc4ce-118">A tabela a seguir mostra alguns valores de exemplo para usar:</span><span class="sxs-lookup"><span data-stu-id="dc4ce-118">The following table shows some sample values to use:</span></span>

   | <span data-ttu-id="dc4ce-119">Campo</span><span class="sxs-lookup"><span data-stu-id="dc4ce-119">Field</span></span> | <span data-ttu-id="dc4ce-120">Valor</span><span class="sxs-lookup"><span data-stu-id="dc4ce-120">Value</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="dc4ce-121">Nome</span><span class="sxs-lookup"><span data-stu-id="dc4ce-121">Name</span></span> |<span data-ttu-id="dc4ce-122">MyHDInsightApp</span><span class="sxs-lookup"><span data-stu-id="dc4ce-122">MyHDInsightApp</span></span> |
   | <span data-ttu-id="dc4ce-123">Descrição</span><span class="sxs-lookup"><span data-stu-id="dc4ce-123">Description</span></span> |<span data-ttu-id="dc4ce-124">MyHDInsightApp</span><span class="sxs-lookup"><span data-stu-id="dc4ce-124">MyHDInsightApp</span></span> |
   | <span data-ttu-id="dc4ce-125">Site</span><span class="sxs-lookup"><span data-stu-id="dc4ce-125">Website</span></span> |<span data-ttu-id="dc4ce-126">http://www.myhdinsightapp.com</span><span class="sxs-lookup"><span data-stu-id="dc4ce-126">http://www.myhdinsightapp.com</span></span> |

4. <span data-ttu-id="dc4ce-127">Marque **Sim, eu concordo** e, em seguida, clique em **Criar seu aplicativo do Twitter**.</span><span class="sxs-lookup"><span data-stu-id="dc4ce-127">Check **Yes, I agree**, and then click **Create your Twitter application**.</span></span>

5. <span data-ttu-id="dc4ce-128">Clique na guia **Permissões** . A permissão padrão é **Somente leitura**.</span><span class="sxs-lookup"><span data-stu-id="dc4ce-128">Click the **Permissions** tab. The default permission is **Read only**.</span></span>

6. <span data-ttu-id="dc4ce-129">Clique na guia **Chaves e Tokens de acesso** .</span><span class="sxs-lookup"><span data-stu-id="dc4ce-129">Click the **Keys and Access Tokens** tab.</span></span>

7. <span data-ttu-id="dc4ce-130">Clique em **Criar meu token de acesso**.</span><span class="sxs-lookup"><span data-stu-id="dc4ce-130">Click **Create my access token**.</span></span>

8. <span data-ttu-id="dc4ce-131">Clique em **OAuth de teste** no canto superior direito da página.</span><span class="sxs-lookup"><span data-stu-id="dc4ce-131">Click **Test OAuth** in the upper-right corner of the page.</span></span>

9. <span data-ttu-id="dc4ce-132">Anote a **chave do consumidor**, o **Segredo do consumidor**, o **Token de acesso** e o **Segredo do token de acesso**.</span><span class="sxs-lookup"><span data-stu-id="dc4ce-132">Write down **consumer key**, **Consumer secret**, **Access token**, and **Access token secret**.</span></span>

### <a name="download-tweets"></a><span data-ttu-id="dc4ce-133">Baixar tweets</span><span class="sxs-lookup"><span data-stu-id="dc4ce-133">Download tweets</span></span>

<span data-ttu-id="dc4ce-134">O código Python a seguir baixa 10.000 tweets do Twitter e os salva em um arquivo chamado **tweets.txt**.</span><span class="sxs-lookup"><span data-stu-id="dc4ce-134">The following Python code downloads 10,000 tweets from Twitter and save them to a file named **tweets.txt**.</span></span>

> [!NOTE]
> <span data-ttu-id="dc4ce-135">As etapas a seguir são executadas no cluster HDInsight, já que o Python já está instalado.</span><span class="sxs-lookup"><span data-stu-id="dc4ce-135">The following steps are performed on the HDInsight cluster, since Python is already installed.</span></span>

1. <span data-ttu-id="dc4ce-136">Conecte-se ao cluster HDInsight usando SSH:</span><span class="sxs-lookup"><span data-stu-id="dc4ce-136">Connect to the HDInsight cluster using SSH:</span></span>

    ```bash
    ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
    ```

    <span data-ttu-id="dc4ce-137">Para obter mais informações, confira [Usar SSH com HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="dc4ce-137">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

3. <span data-ttu-id="dc4ce-138">Use os comandos a seguir para instalar [Tweepy](http://www.tweepy.org/), [Progressbar](https://pypi.python.org/pypi/progressbar/2.2) e outros pacotes necessários:</span><span class="sxs-lookup"><span data-stu-id="dc4ce-138">Use the following commands to install [Tweepy](http://www.tweepy.org/), [Progressbar](https://pypi.python.org/pypi/progressbar/2.2), and other required packages:</span></span>

   ```bash
   sudo apt install python-dev libffi-dev libssl-dev
   sudo apt remove python-openssl
   pip install virtualenv
   mkdir gettweets
   cd gettweets
   virtualenv gettweets
   source gettweets/bin/activate
   pip install tweepy progressbar pyOpenSSL requests[security]
   ```

4. <span data-ttu-id="dc4ce-139">Use o comando a seguir para criar um arquivo chamado **gettweets.py**:</span><span class="sxs-lookup"><span data-stu-id="dc4ce-139">Use the following command to create a file named **gettweets.py**:</span></span>

   ```bash
   nano gettweets.py
   ```

5. <span data-ttu-id="dc4ce-140">Use o texto a seguir como o conteúdo do arquivo **gettweets.py**:</span><span class="sxs-lookup"><span data-stu-id="dc4ce-140">Use the following text as the contents of the **gettweets.py** file:</span></span>

   ```python
   #!/usr/bin/python

   from tweepy import Stream, OAuthHandler
   from tweepy.streaming import StreamListener
   from progressbar import ProgressBar, Percentage, Bar
   import json
   import sys

   #Twitter app information
   consumer_secret='Your consumer secret'
   consumer_key='Your consumer key'
   access_token='Your access token'
   access_token_secret='Your access token secret'

   #The number of tweets we want to get
   max_tweets=10000

   #Create the listener class that receives and saves tweets
   class listener(StreamListener):
       #On init, set the counter to zero and create a progress bar
       def __init__(self, api=None):
           self.num_tweets = 0
           self.pbar = ProgressBar(widgets=[Percentage(), Bar()], maxval=max_tweets).start()

       #When data is received, do this
       def on_data(self, data):
           #Append the tweet to the 'tweets.txt' file
           with open('tweets.txt', 'a') as tweet_file:
               tweet_file.write(data)
               #Increment the number of tweets
               self.num_tweets += 1
               #Check to see if we have hit max_tweets and exit if so
               if self.num_tweets >= max_tweets:
                   self.pbar.finish()
                   sys.exit(0)
               else:
                   #increment the progress bar
                   self.pbar.update(self.num_tweets)
           return True

       #Handle any errors that may occur
       def on_error(self, status):
           print status

   #Get the OAuth token
   auth = OAuthHandler(consumer_key, consumer_secret)
   auth.set_access_token(access_token, access_token_secret)
   #Use the listener class for stream processing
   twitterStream = Stream(auth, listener())
   #Filter for these topics
   twitterStream.filter(track=["azure","cloud","hdinsight"])
   ```

    > [!IMPORTANT]
    > <span data-ttu-id="dc4ce-141">Substitua o texto de espaço reservado para os seguintes itens com as informações do seu aplicativo do twitter:</span><span class="sxs-lookup"><span data-stu-id="dc4ce-141">Replace the placeholder text for the following items with the information from your twitter application:</span></span>
    >
    > * `consumer_secret`
    > * `consumer_key`
    > * `access_token`
    > * `access_token_secret`

6. <span data-ttu-id="dc4ce-142">Use **Ctrl + X** e **Y** para salvar o arquivo.</span><span class="sxs-lookup"><span data-stu-id="dc4ce-142">Use **Ctrl + X**, then **Y** to save the file.</span></span>

7. <span data-ttu-id="dc4ce-143">Use o comando a seguir para executar o arquivo e baixar os tweets:</span><span class="sxs-lookup"><span data-stu-id="dc4ce-143">Use the following command to run the file and download tweets:</span></span>

    ```bash
    python gettweets.py
    ```

    <span data-ttu-id="dc4ce-144">Aparece um indicador de progresso.</span><span class="sxs-lookup"><span data-stu-id="dc4ce-144">A progress indicator appears.</span></span> <span data-ttu-id="dc4ce-145">Ele conta até 100%, conforme os tweets são baixados.</span><span class="sxs-lookup"><span data-stu-id="dc4ce-145">It counts up to 100% as the tweets are downloaded.</span></span>

   > [!NOTE]
   > <span data-ttu-id="dc4ce-146">Se estiver demorando muito tempo para a barra de progresso Avançar, você deverá alterar o filtro para rastrear os tópicos mais populares.</span><span class="sxs-lookup"><span data-stu-id="dc4ce-146">If it is taking a long time for the progress bar to advance, you should change the filter to track trending topics.</span></span> <span data-ttu-id="dc4ce-147">Quando há muitos tweets sobre o tópico no filtro, você pode obter rapidamente os 10.000 tweets necessários.</span><span class="sxs-lookup"><span data-stu-id="dc4ce-147">When there are many tweets about the topic in your filter, you can quickly get the 10000 tweets needed.</span></span>

### <a name="upload-the-data"></a><span data-ttu-id="dc4ce-148">Carregar os dados</span><span class="sxs-lookup"><span data-stu-id="dc4ce-148">Upload the data</span></span>

<span data-ttu-id="dc4ce-149">Para carregar os dados no armazenamento do HDInsight, use os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="dc4ce-149">To upload the data to HDInsight storage, use the following commands:</span></span>

   ```bash
   hdfs dfs -mkdir -p /tutorials/twitter/data
   hdfs dfs -put tweets.txt /tutorials/twitter/data/tweets.txt
```

<span data-ttu-id="dc4ce-150">Esses comandos armazenam os dados em um local que todos os nós no cluster podem acessar.</span><span class="sxs-lookup"><span data-stu-id="dc4ce-150">These commands store the data in a location that all nodes in the cluster can access.</span></span>

## <a name="run-the-hiveql-job"></a><span data-ttu-id="dc4ce-151">Executar o trabalho HiveQL</span><span class="sxs-lookup"><span data-stu-id="dc4ce-151">Run the HiveQL job</span></span>

1. <span data-ttu-id="dc4ce-152">Use o comando a seguir para criar um arquivo com instruções HiveQL:</span><span class="sxs-lookup"><span data-stu-id="dc4ce-152">Use the following command to create a file containing HiveQL statements:</span></span>

   ```bash
   nano twitter.hql
   ```

    <span data-ttu-id="dc4ce-153">Use o texto a seguir como o conteúdo do arquivo:</span><span class="sxs-lookup"><span data-stu-id="dc4ce-153">Use the following text as the contents of the file:</span></span>

   ```hiveql
   set hive.exec.dynamic.partition = true;
   set hive.exec.dynamic.partition.mode = nonstrict;
   -- Drop table, if it exists
   DROP TABLE tweets_raw;
   -- Create it, pointing toward the tweets logged from Twitter
   CREATE EXTERNAL TABLE tweets_raw (
       json_response STRING
   )
   STORED AS TEXTFILE LOCATION '/tutorials/twitter/data';
   -- Drop and recreate the destination table
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
   -- Select tweets from the imported data, parse the JSON,
   -- and insert into the tweets table
   FROM tweets_raw
   INSERT OVERWRITE TABLE tweets
   SELECT
       cast(get_json_object(json_response, '$.id_str') as BIGINT),
       get_json_object(json_response, '$.created_at'),
       concat(substr (get_json_object(json_response, '$.created_at'),1,10),' ',
       substr (get_json_object(json_response, '$.created_at'),27,4)),
       substr (get_json_object(json_response, '$.created_at'),27,4),
       case substr (get_json_object(json_response,    '$.created_at'),5,3)
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
   ```

2. <span data-ttu-id="dc4ce-154">Pressione **Ctrl + X** e pressione **Y** para salvar o arquivo.</span><span class="sxs-lookup"><span data-stu-id="dc4ce-154">Press **Ctrl + X**, then press **Y** to save the file.</span></span>
3. <span data-ttu-id="dc4ce-155">Use o comando a seguir para executar o HiveQL contido no arquivo:</span><span class="sxs-lookup"><span data-stu-id="dc4ce-155">Use the following command to run the HiveQL contained in the file:</span></span>

   ```bash
   beeline -u 'jdbc:hive2://headnodehost:10001/;transportMode=http' -i twitter.hql
   ```

    <span data-ttu-id="dc4ce-156">Esse comando executa o arquivo **twitter.hql**.</span><span class="sxs-lookup"><span data-stu-id="dc4ce-156">This command runs the the **twitter.hql** file.</span></span> <span data-ttu-id="dc4ce-157">Quando a consulta for concluída, você verá um prompt `jdbc:hive2//localhost:10001/>`.</span><span class="sxs-lookup"><span data-stu-id="dc4ce-157">Once the query completes, you see a `jdbc:hive2//localhost:10001/>` prompt.</span></span>

4. <span data-ttu-id="dc4ce-158">No prompt de beeline, use a consulta a seguir para verificar se os dados foram importados:</span><span class="sxs-lookup"><span data-stu-id="dc4ce-158">From the beeline prompt, use the following query to verify that data was imported:</span></span>

   ```hiveql
   SELECT name, screen_name, count(1) as cc
       FROM tweets
       WHERE text like "%Azure%"
       GROUP BY name,screen_name
       ORDER BY cc DESC LIMIT 10;
   ```

    <span data-ttu-id="dc4ce-159">Essa consulta retornará no máximo 10 tweets com a palavra **Azure** no texto da mensagem.</span><span class="sxs-lookup"><span data-stu-id="dc4ce-159">This query returns a maximum of 10 tweets that contain the word **Azure** in the message text.</span></span>

## <a name="next-steps"></a><span data-ttu-id="dc4ce-160">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="dc4ce-160">Next steps</span></span>

<span data-ttu-id="dc4ce-161">Você aprendeu como transformar um conjunto de dados JSON não estruturado uma em tabela estruturada do Hive.</span><span class="sxs-lookup"><span data-stu-id="dc4ce-161">You have learned how to transform an unstructured JSON dataset into a structured Hive table.</span></span> <span data-ttu-id="dc4ce-162">Para saber mais sobre o Hive no HDInsight, consulte os documentos a seguir:</span><span class="sxs-lookup"><span data-stu-id="dc4ce-162">To learn more about Hive on HDInsight, see the following documents:</span></span>

* [<span data-ttu-id="dc4ce-163">Introdução ao HDInsight</span><span class="sxs-lookup"><span data-stu-id="dc4ce-163">Get started with HDInsight</span></span>](hdinsight-hadoop-linux-tutorial-get-started.md)
* [<span data-ttu-id="dc4ce-164">Analisar dados de atraso de voo usando o HDInsight</span><span class="sxs-lookup"><span data-stu-id="dc4ce-164">Analyze flight delay data using HDInsight</span></span>](hdinsight-analyze-flight-delay-data-linux.md)

[curl]: http://curl.haxx.se
[curl-download]: http://curl.haxx.se/download.html

[apache-hive-tutorial]: https://cwiki.apache.org/confluence/display/Hive/Tutorial

[twitter-streaming-api]: https://dev.twitter.com/docs/streaming-apis
[twitter-statuses-filter]: https://dev.twitter.com/docs/api/1.1/post/statuses/filter
