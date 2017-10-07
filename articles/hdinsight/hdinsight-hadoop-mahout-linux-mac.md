---
title: "recomendações de aaaGenerate usando Mahout e HDInsight (SSH) - Azure | Microsoft Docs"
description: "Saiba como toouse Olá Apache Mahout recomendações de filme toogenerate biblioteca com HDInsight (Hadoop) de aprendizado de máquina."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: c78ec37c-9a8c-4bb6-9e38-0bdb9e89fbd7
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: larryfr
ms.openlocfilehash: fedac9ceb4268f8421bce4623a5ad271041b8b3d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="generate-movie-recommendations-by-using-apache-mahout-with-linux-based-hadoop-in-hdinsight-ssh"></a>Gerar recomendações de filmes usando o Apache Mahout com o Hadoop para Linux no HDInsight (SSH)

[!INCLUDE [mahout-selector](../../includes/hdinsight-selector-mahout.md)]

Saiba como Olá toouse [Mahout Apache](http://mahout.apache.org) biblioteca de aprendizado de máquina com recomendações de filme toogenerate HDInsight do Azure.

O Mahout é uma biblioteca de [machine learning][ml] para o Apache Hadoop. O Mahout contém algoritmos para processamento de dados, como filtragem, classificação e clustering. Neste artigo, você deve usar uma recomendação mecanismo toogenerate filme as recomendações se baseiam em filmes viu seus amigos.

## <a name="prerequisites"></a>Pré-requisitos

* Criar um cluster HDInsight baseado em Linux. Para saber mais sobre como criar um, confira [Introdução ao uso do Hadoop baseado em Linux no HDInsight][getstarted].

> [!IMPORTANT]
> Linux é Olá sistema operacional somente de usado no HDInsight versão 3.4 ou posterior. Para obter mais informações, confira [baixa do HDInsight no Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).

* Um cliente SSH. Para obter mais informações, consulte Olá [usar SSH com HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) documento.

## <a name="mahout-versioning"></a>Versões do Mahout

Para obter mais informações sobre a versão de saudação do Mahout no HDInsight, consulte [HDInsight versões e componentes do Hadoop](hdinsight-component-versioning.md).

## <a name="recommendations"></a>Entendendo as recomendações

Uma das funções de saudação que é fornecido por Mahout é um mecanismo de recomendação. Esse mecanismo aceita dados em formato de saudação do `userID`, `itemId`, e `prefValue` (Olá preferência para o item de saudação). Mahout pode executar a ocorrência colegas analysis toodetermine: *os usuários com a preferência de um item também têm uma preferência para esses outros itens*. Mahout determina, em seguida, os usuários com as preferências de tipo de item, que podem ser usado toomake recomendações.

Olá seguinte fluxo de trabalho é um exemplo simplificado que usa dados do filme:

* **Ocorrência colegas**: Joe, Alice e Bob vinculadas todos os *estrela guerras*, *Olá Empire greves volta*, e *retorno de saudação Jedi*. Mahout determina que os usuários que também como qualquer um desses filmes Olá outras duas.

* **Ocorrência colegas**: Bob e Alice também gostaram *Olá fantasma ameaça*, *ataque de Clones Olá*, e *Vingança de saudação Sith*. Mahout determina que os usuários que gostaram filmes de três anterior Olá também como esses três filmes.

* **Recomendação de similaridade**: Joe porque gostou Olá três primeiros filmes, Mahout examina filmes que outras pessoas com as preferências semelhantes gostou, mas Joe não tem observados (gostou/classificado). Nesse caso, recomenda Mahout *Olá fantasma ameaça*, *ataque de Clones Olá*, e *Vingança de saudação Sith*.

### <a name="understanding-hello-data"></a>Noções básicas sobre dados saudação

Convenientemente, a [GroupLens Research][movielens] oferece dados de classificação para filmes em um formato compatível com o Mahout. Esses dados estão disponíveis no armazenamento padrão do cluster em `/HdiSamples/HdiSamples/MahoutMovieData`.

Existem dois arquivos, `moviedb.txt` e `user-ratings.txt`. arquivo de usuário ratings.txt Olá é usado durante a análise, enquanto moviedb.txt é uma informação de texto amigável tooprovide usado ao exibir os resultados de saudação da análise de saudação.

dados contidos no usuário ratings.txt Hello tem uma estrutura de `userID`, `movieID`, `userRating`, e `timestamp`, que informa como altamente cada usuário classificado como um filme. Aqui está um exemplo de dados de saudação:

    196    242    3    881250949
    186    302    3    891717742
    22    377    1    878887116
    244    51    2    880606923
    166    346    1    886397596

## <a name="run-hello-analysis"></a>Executar a análise de saudação

De um cluster de toohello de conexão SSH, use Olá trabalho de recomendação de saudação do comando toorun a seguir:

```bash
mahout recommenditembased -s SIMILARITY_COOCCURRENCE -i /HdiSamples/HdiSamples/MahoutMovieData/user-ratings.txt -o /example/data/mahoutout --tempDir /temp/mahouttemp
```

> [!NOTE]
> Olá trabalho pode levar vários toocomplete de minutos e pode executar vários trabalhos de MapReduce.

## <a name="view-hello-output"></a>Exibir saída de hello

1. Após a conclusão do trabalho hello, use Olá após a saída do comando tooview Olá gerado:

    ```bash
    hdfs dfs -text /example/data/mahoutout/part-r-00000
    ```

    saída de Hello aparece da seguinte maneira:

        1    [234:5.0,347:5.0,237:5.0,47:5.0,282:5.0,275:5.0,88:5.0,515:5.0,514:5.0,121:5.0]
        2    [282:5.0,210:5.0,237:5.0,234:5.0,347:5.0,121:5.0,258:5.0,515:5.0,462:5.0,79:5.0]
        3    [284:5.0,285:4.828125,508:4.7543354,845:4.75,319:4.705128,124:4.7045455,150:4.6938777,311:4.6769233,248:4.65625,272:4.649266]
        4    [690:5.0,12:5.0,234:5.0,275:5.0,121:5.0,255:5.0,237:5.0,895:5.0,282:5.0,117:5.0]

    Olá primeira coluna é Olá `userID`. Olá valores contidos em ' [' e ']' são `movieId`:`recommendationScore`.

2. Você pode usar a saída de hello, juntamente com hello moviedb.txt, tooprovide obter mais informações sobre recomendações de saudação. Primeiro, precisamos de arquivos de saudação toocopy localmente usando Olá comandos a seguir:

    ```bash
    hdfs dfs -get /example/data/mahoutout/part-r-00000 recommendations.txt
    hdfs dfs -get /HdiSamples/HdiSamples/MahoutMovieData/* .
    ```

    Este comando copia Olá arquivo de tooa de dados de saída denominado **recommendations.txt** no diretório atual hello, juntamente com os arquivos de dados do filme hello.

3. Use Olá comando toocreate um script de Python procura nomes de filme para dados de saudação na saída do hello recomendações a seguir:

    ```bash
    nano show_recommendations.py
    ```

    Quando abre o editor de hello, use Olá depois do texto como conteúdo de saudação do arquivo hello:

   ```python
   #!/usr/bin/env python

   import sys

   if len(sys.argv) != 5:
        print "Arguments: userId userDataFilename movieFilename recommendationFilename"
        sys.exit(1)

   userId, userDataFilename, movieFilename, recommendationFilename = sys.argv[1:]

   print "Reading Movies Descriptions"
   movieFile = open(movieFilename)
   movieById = {}
   for line in movieFile:
       tokens = line.split("|")
       movieById[tokens[0]] = tokens[1:]
   movieFile.close()

   print "Reading Rated Movies"
   userDataFile = open(userDataFilename)
   ratedMovieIds = []
   for line in userDataFile:
       tokens = line.split("\t")
       if tokens[0] == userId:
           ratedMovieIds.append((tokens[1],tokens[2]))
   userDataFile.close()

   print "Reading Recommendations"
   recommendationFile = open(recommendationFilename)
   recommendations = []
   for line in recommendationFile:
       tokens = line.split("\t")
       if tokens[0] == userId:
           movieIdAndScores = tokens[1].strip("[]\n").split(",")
           recommendations = [ movieIdAndScore.split(":") for movieIdAndScore in movieIdAndScores ]
           break
   recommendationFile.close()

   print "Rated Movies"
   print "------------------------"
   for movieId, rating in ratedMovieIds:
       print "%s, rating=%s" % (movieById[movieId][0], rating)
   print "------------------------"

   print "Recommended Movies"
   print "------------------------"
   for movieId, score in recommendations:
       print "%s, score=%s" % (movieById[movieId][0], score)
   print "------------------------"
   ```

    Pressione **Ctrl-X**, **Y**e, finalmente, **Enter** toosave dados de saudação.

4. Execute o script de Python hello. Olá comando a seguir supõe que você está no diretório Olá onde todos os arquivos de saudação foram baixados:

    ```bash
    python show_recommendations.py 4 user-ratings.txt moviedb.txt recommendations.txt
    ```

    Esse comando examina recomendações Olá geradas para 4 ID de usuário.

    * Olá **ratings.txt usuário** arquivo é usado tooretrieve filmes que tenham sido classificados.

    * Olá **moviedb.txt** arquivo é usado tooretrieve Olá nomes de filmes hello.

    * Olá **recommendations.txt** é usado tooretrieve recomendações de filme Olá para este usuário.

     saudação de saída desse comando é semelhante toohello seguinte texto:

        Pontuação de sete anos no Tibete (1997) = 5.0 Indiana Jones e hello última campanha (1989), pontuação = 5.0 Jaws (1975), pontuação = 5.0 sentido e Sensibility (1995), pontuação = 5.0 independência (ID4) (1996), pontuação = 5.0 meu melhor amigo casamento (1997), pontuação = 5.0 Jerry Maguire (1996 ), pontuação = 5.0 Scream 2 (1997), pontuação = 5.0 tooKill de tempo, (1996), pontuação = 5.0

## <a name="delete-temporary-data"></a>Excluir dados temporários

Trabalhos mahout não remova os dados temporários que são criados durante o processamento de trabalho hello. Olá `--tempDir` parâmetro é especificado em Olá exemplo trabalho tooisolate Olá os arquivos temporários em um caminho específico para exclusão fácil. arquivos temporários do tooremove hello, use Olá comando a seguir:

```bash
hdfs dfs -rm -f -r /temp/mahouttemp
```

> [!WARNING]
> Se você quiser novamente o comando de saudação toorun, você também deve excluir o diretório de saída hello. Use Olá toodelete a seguir neste diretório:
>
> `hdfs dfs -rm -f -r /example/data/mahoutout`


## <a name="next-steps"></a>Próximas etapas

Agora que você aprendeu como toouse Mahout, descubra outras maneiras de trabalhar com dados no HDInsight:

* [Hive com o HDInsight](hdinsight-use-hive.md)
* [Pig com o HDInsight](hdinsight-use-pig.md)
* [MapReduce com o HDInsight](hdinsight-use-mapreduce.md)

[build]: http://mahout.apache.org/developers/buildingmahout.html
[movielens]: http://grouplens.org/datasets/movielens/
[100k]: http://files.grouplens.org/datasets/movielens/ml-100k.zip
[getstarted]: hdinsight-hadoop-linux-tutorial-get-started.md
[upload]: hdinsight-upload-data.md
[ml]: http://en.wikipedia.org/wiki/Machine_learning
[forest]: http://en.wikipedia.org/wiki/Random_forest
[enableremote]: ./media/hdinsight-mahout/enableremote.png
[connect]: ./media/hdinsight-mahout/connect.png
[hadoopcli]: ./media/hdinsight-mahout/hadoopcli.png
[tools]: https://github.com/Blackmist/hdinsight-tools
