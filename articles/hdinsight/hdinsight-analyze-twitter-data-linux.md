---
title: aaaAnalyze Twitter dados com o Apache Hive - HDInsight do Azure | Microsoft Docs
description: "Saiba como toouse usar Hive e Hadoop em HDInsight tootransform bruto TWitter dados em uma tabela de Hive pesquisável."
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
ms.openlocfilehash: 02c4d027c7bbf390ac1c3724c14f8d549ea5195e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-twitter-data-using-hive-and-hadoop-on-hdinsight"></a>Analisar dados do Twitter usando o Hive e Hadoop no HDInsight

Saiba como toouse tooprocess Apache Hive dados do Twitter. resultado de saudação é uma lista de usuários do Twitter que enviou Olá tweets mais que contêm uma palavra específica.

> [!IMPORTANT]
> etapas de saudação neste documento foram testadas em HDInsight 3.6.
>
> Linux é Olá sistema operacional somente de usado no HDInsight versão 3.4 ou posterior. Para obter mais informações, confira [baixa do HDInsight no Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).

## <a name="get-hello-data"></a>Obter dados de saudação

Twitter permite Olá tooretrieve [dados para cada tweet](https://dev.twitter.com/docs/platform-objects/tweets) como um documento JSON JavaScript Object Notation () por meio de uma API REST. [OAuth](http://oauth.net) é necessário para autenticação toohello API.

### <a name="create-a-twitter-application"></a>Criar um aplicativo do Twitter

1. Em um navegador da web, entrar muito[https://apps.twitter.com/](https://apps.twitter.com/). Clique em Olá **inscrição agora** link se você não tiver uma conta do Twitter.

2. Clique em **Criar Novo Aplicativo**.

3. Digite o **Nome**, a **Descrição** e o **Site**. Você pode fazer backup de uma URL para Olá **site** campo. Olá, a tabela a seguir mostra algumas toouse de valores de exemplo:

   | Campo | Valor |
   |:--- |:--- |
   | Nome |MyHDInsightApp |
   | Descrição |MyHDInsightApp |
   | Site |http://www.myhdinsightapp.com |

4. Marque **Sim, eu concordo** e, em seguida, clique em **Criar seu aplicativo do Twitter**.

5. Clique em Olá **permissões** guia saudação padrão permissão é **somente leitura**.

6. Clique em Olá **chaves e Tokens de acesso** guia.

7. Clique em **Criar meu token de acesso**.

8. Clique em **teste OAuth** no canto superior direito de saudação da página de saudação.

9. Anote a **chave do consumidor**, o **Segredo do consumidor**, o **Token de acesso** e o **Segredo do token de acesso**.

### <a name="download-tweets"></a>Baixar tweets

Olá código Python a seguir baixa 10.000 tweets do Twitter e salvá-los arquivo tooa chamado **tweets.txt**.

> [!NOTE]
> Olá etapas a seguir é executada no cluster do HDInsight hello, como Python já está instalado.

1. Conecte o cluster do HDInsight toohello usando SSH:

    ```bash
    ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
    ```

    Para obter mais informações, confira [Usar SSH com HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

3. A seguir Olá use comandos tooinstall [Tweepy](http://www.tweepy.org/), [Progressbar](https://pypi.python.org/pypi/progressbar/2.2)e outros pacotes necessários:

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

4. Comando de uso a seguir de saudação toocreate um arquivo chamado **gettweets.py**:

   ```bash
   nano gettweets.py
   ```

5. Saudação de uso após o texto como conteúdo de saudação do hello **gettweets.py** arquivo:

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

   #hello number of tweets we want tooget
   max_tweets=10000

   #Create hello listener class that receives and saves tweets
   class listener(StreamListener):
       #On init, set hello counter toozero and create a progress bar
       def __init__(self, api=None):
           self.num_tweets = 0
           self.pbar = ProgressBar(widgets=[Percentage(), Bar()], maxval=max_tweets).start()

       #When data is received, do this
       def on_data(self, data):
           #Append hello tweet toohello 'tweets.txt' file
           with open('tweets.txt', 'a') as tweet_file:
               tweet_file.write(data)
               #Increment hello number of tweets
               self.num_tweets += 1
               #Check toosee if we have hit max_tweets and exit if so
               if self.num_tweets >= max_tweets:
                   self.pbar.finish()
                   sys.exit(0)
               else:
                   #increment hello progress bar
                   self.pbar.update(self.num_tweets)
           return True

       #Handle any errors that may occur
       def on_error(self, status):
           print status

   #Get hello OAuth token
   auth = OAuthHandler(consumer_key, consumer_secret)
   auth.set_access_token(access_token, access_token_secret)
   #Use hello listener class for stream processing
   twitterStream = Stream(auth, listener())
   #Filter for these topics
   twitterStream.filter(track=["azure","cloud","hdinsight"])
   ```

    > [!IMPORTANT]
    > Substitua o texto do espaço reservado Olá para Olá seguir itens com informações de saudação de seu aplicativo twitter:
    >
    > * `consumer_secret`
    > * `consumer_key`
    > * `access_token`
    > * `access_token_secret`

6. Use **Ctrl + X**, em seguida, **Y** toosave arquivo de saudação.

7. Use Olá após o arquivo de saudação do comando toorun e baixar tweets:

    ```bash
    python gettweets.py
    ```

    Aparece um indicador de progresso. Ele conta % too100 como Olá tweets são baixadas.

   > [!NOTE]
   > Se estiver demorando muito tempo para Olá tooadvance de barra de progresso, você deve alterar tópicos de tendência Olá filtro tootrack. Quando há muitos tweets sobre o tópico Olá no filtro, você pode chegar facilmente Olá 10000 tweets necessário.

### <a name="upload-hello-data"></a>Carregar dados de saudação

armazenamento de tooHDInsight de dados de saudação do tooupload, Olá use comandos a seguir:

   ```bash
   hdfs dfs -mkdir -p /tutorials/twitter/data
   hdfs dfs -put tweets.txt /tutorials/twitter/data/tweets.txt
```

Esses comandos armazenam dados de saudação em um local que podem acessar todos os nós no cluster de saudação.

## <a name="run-hello-hiveql-job"></a>Executar trabalho de estilo de saudação

1. Use Olá um arquivo que contém instruções de HiveQL toocreate de comando a seguir:

   ```bash
   nano twitter.hql
   ```

    Use Olá depois do texto como conteúdo de saudação do arquivo hello:

   ```hiveql
   set hive.exec.dynamic.partition = true;
   set hive.exec.dynamic.partition.mode = nonstrict;
   -- Drop table, if it exists
   DROP TABLE tweets_raw;
   -- Create it, pointing toward hello tweets logged from Twitter
   CREATE EXTERNAL TABLE tweets_raw (
       json_response STRING
   )
   STORED AS TEXTFILE LOCATION '/tutorials/twitter/data';
   -- Drop and recreate hello destination table
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
   -- Select tweets from hello imported data, parse hello JSON,
   -- and insert into hello tweets table
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

2. Pressione **Ctrl + X**, em seguida, pressione **Y** toosave arquivo de saudação.
3. Use Olá Olá do comando toorun que hiveql contido no arquivo hello a seguir:

   ```bash
   beeline -u 'jdbc:hive2://headnodehost:10001/;transportMode=http' -i twitter.hql
   ```

    Esse comando executa Olá Olá **twitter.hql** arquivo. Depois que a consulta de saudação é concluída, você verá um `jdbc:hive2//localhost:10001/>` prompt.

4. No prompt de beeline de saudação, use Olá que os dados foram importados de tooverify de consulta a seguir:

   ```hiveql
   SELECT name, screen_name, count(1) as cc
       FROM tweets
       WHERE text like "%Azure%"
       GROUP BY name,screen_name
       ORDER BY cc DESC LIMIT 10;
   ```

    Esta consulta retorna um máximo de 10 tweets que contêm a palavra hello **Azure** no texto da mensagem de saudação.

## <a name="next-steps"></a>Próximas etapas

Você aprendeu como tootransform um conjunto de dados não estruturado JSON em uma tabela de Hive estruturado. toolearn mais sobre o Hive no HDInsight, consulte Olá documentos a seguir:

* [Introdução ao HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md)
* [Analisar dados de atraso de voo usando o HDInsight](hdinsight-analyze-flight-delay-data-linux.md)

[curl]: http://curl.haxx.se
[curl-download]: http://curl.haxx.se/download.html

[apache-hive-tutorial]: https://cwiki.apache.org/confluence/display/Hive/Tutorial

[twitter-streaming-api]: https://dev.twitter.com/docs/streaming-apis
[twitter-statuses-filter]: https://dev.twitter.com/docs/api/1.1/post/statuses/filter
