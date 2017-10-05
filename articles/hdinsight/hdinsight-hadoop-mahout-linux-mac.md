---
title: "Gerar recomendações usando o Mahout e o HDInsight (SSH) – Azure | Microsoft Docs"
description: "Saiba como usar a biblioteca de aprendizado de máquina do Apache Mahout para gerar recomendações de vídeos com o HDInsight (Hadoop)."
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
ms.openlocfilehash: 28450d72f19a5467d88bc787d11f6c37c5afbf9a
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="generate-movie-recommendations-by-using-apache-mahout-with-linux-based-hadoop-in-hdinsight-ssh"></a><span data-ttu-id="0f75a-103">Gerar recomendações de filmes usando o Apache Mahout com o Hadoop para Linux no HDInsight (SSH)</span><span class="sxs-lookup"><span data-stu-id="0f75a-103">Generate movie recommendations by using Apache Mahout with Linux-based Hadoop in HDInsight (SSH)</span></span>

[!INCLUDE [mahout-selector](../../includes/hdinsight-selector-mahout.md)]

<span data-ttu-id="0f75a-104">Saiba como usar a biblioteca de aprendizado de máquina do [Apache Mahout](http://mahout.apache.org) com o Azure HDInsight para gerar recomendações de vídeos.</span><span class="sxs-lookup"><span data-stu-id="0f75a-104">Learn how to use the [Apache Mahout](http://mahout.apache.org) machine learning library with Azure HDInsight to generate movie recommendations.</span></span>

<span data-ttu-id="0f75a-105">O Mahout é uma biblioteca de [machine learning][ml] para o Apache Hadoop.</span><span class="sxs-lookup"><span data-stu-id="0f75a-105">Mahout is a [machine learning][ml] library for Apache Hadoop.</span></span> <span data-ttu-id="0f75a-106">O Mahout contém algoritmos para processamento de dados, como filtragem, classificação e clustering.</span><span class="sxs-lookup"><span data-stu-id="0f75a-106">Mahout contains algorithms for processing data, such as filtering, classification, and clustering.</span></span> <span data-ttu-id="0f75a-107">Neste artigo, você utiliza um mecanismo de recomendação para gerar recomendações de filmes baseadas nos vídeos que seus amigos assistiram.</span><span class="sxs-lookup"><span data-stu-id="0f75a-107">In this article, you use a recommendation engine to generate movie recommendations that are based on movies your friends have seen.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0f75a-108">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="0f75a-108">Prerequisites</span></span>

* <span data-ttu-id="0f75a-109">Criar um cluster HDInsight baseado em Linux.</span><span class="sxs-lookup"><span data-stu-id="0f75a-109">A Linux-based HDInsight cluster.</span></span> <span data-ttu-id="0f75a-110">Para saber mais sobre como criar um, confira [Introdução ao uso do Hadoop baseado em Linux no HDInsight][getstarted].</span><span class="sxs-lookup"><span data-stu-id="0f75a-110">For information about creating one, see [Get started using Linux-based Hadoop in HDInsight][getstarted].</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0f75a-111">O Linux é o único sistema operacional usado no HDInsight versão 3.4 ou superior.</span><span class="sxs-lookup"><span data-stu-id="0f75a-111">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="0f75a-112">Para obter mais informações, confira [baixa do HDInsight no Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="0f75a-112">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="0f75a-113">Um cliente SSH.</span><span class="sxs-lookup"><span data-stu-id="0f75a-113">An SSH client.</span></span> <span data-ttu-id="0f75a-114">Para saber mais, consulte o documento [Usar SSH com HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="0f75a-114">For more information, see the [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) document.</span></span>

## <a name="mahout-versioning"></a><span data-ttu-id="0f75a-115">Versões do Mahout</span><span class="sxs-lookup"><span data-stu-id="0f75a-115">Mahout versioning</span></span>

<span data-ttu-id="0f75a-116">Para obter mais informações sobre a versão do Mahout incluída com o cluster HDInsight, consulte [Versões do HDInsight e componentes do Hadoop](hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="0f75a-116">For more information about the version of Mahout in HDInsight, see [HDInsight versions and Hadoop components](hdinsight-component-versioning.md).</span></span>

## <span data-ttu-id="0f75a-117"><a name="recommendations"></a>Entendendo as recomendações</span><span class="sxs-lookup"><span data-stu-id="0f75a-117"><a name="recommendations"></a>Understanding recommendations</span></span>

<span data-ttu-id="0f75a-118">Uma das funções oferecidas pelo Mahout é um mecanismo de recomendação.</span><span class="sxs-lookup"><span data-stu-id="0f75a-118">One of the functions that is provided by Mahout is a recommendation engine.</span></span> <span data-ttu-id="0f75a-119">Esse mecanismo aceita dados no formato de `userID`, `itemId` e `prefValue` (o usuário escolhe o item de sua preferência).</span><span class="sxs-lookup"><span data-stu-id="0f75a-119">This engine accepts data in the format of `userID`, `itemId`, and `prefValue` (the preference for the item).</span></span> <span data-ttu-id="0f75a-120">O Mahout, então, pode realizar análises de coocorrência, para determinar que *usuários que têm preferência por um item também têm preferência por esses outros itens*.</span><span class="sxs-lookup"><span data-stu-id="0f75a-120">Mahout can then perform co-occurance analysis to determine: *users who have a preference for an item also have a preference for these other items*.</span></span> <span data-ttu-id="0f75a-121">O Mahout determinará, então, usuários com preferências de item similares, que podem ser utilizadas para fazer recomendações.</span><span class="sxs-lookup"><span data-stu-id="0f75a-121">Mahout then determines users with like-item preferences, which can be used to make recommendations.</span></span>

<span data-ttu-id="0f75a-122">O fluxo de trabalho a seguir é um exemplo simplificado que usa dados de filmes:</span><span class="sxs-lookup"><span data-stu-id="0f75a-122">The following workflow is a simplified example that uses movie data:</span></span>

* <span data-ttu-id="0f75a-123">**Co-ocorrência**: Joe, Alice e Bob, todos gostaram de *Guerra nas Estrelas*, *O Império Contra-ataca* e *O Retorno de Jedi*.</span><span class="sxs-lookup"><span data-stu-id="0f75a-123">**Co-occurance**: Joe, Alice, and Bob all liked *Star Wars*, *The Empire Strikes Back*, and *Return of the Jedi*.</span></span> <span data-ttu-id="0f75a-124">O Mahout determina que usuários que gostam de qualquer um desses filmes também gostam dos outros dois.</span><span class="sxs-lookup"><span data-stu-id="0f75a-124">Mahout determines that users who like any one of these movies also like the other two.</span></span>

* <span data-ttu-id="0f75a-125">**Co-ocorrência**: Bob e Alice também gostaram de *A Ameaça Fantasma*, *A Guerra dos Clones* e *A Vingança dos Sith*.</span><span class="sxs-lookup"><span data-stu-id="0f75a-125">**Co-occurance**: Bob and Alice also liked *The Phantom Menace*, *Attack of the Clones*, and *Revenge of the Sith*.</span></span> <span data-ttu-id="0f75a-126">O Mahout determina que usuários que gostam de qualquer um dos três filmes citados anteriormente também gostam destes últimos três filmes.</span><span class="sxs-lookup"><span data-stu-id="0f75a-126">Mahout determines that users who liked the previous three movies also like these three movies.</span></span>

* <span data-ttu-id="0f75a-127">**Recomendação por similaridade**: já que Joe gostou dos primeiros três, o Mahout pesquisará os filmes que outros com preferências similares gostaram, mas que Joe não assistiu (curtiu/classificou).</span><span class="sxs-lookup"><span data-stu-id="0f75a-127">**Similarity recommendation**: Because Joe liked the first three movies, Mahout looks at movies that others with similar preferences liked, but Joe has not watched (liked/rated).</span></span> <span data-ttu-id="0f75a-128">Nesse caso, o Mahout recomendaria *A Ameaça Fantasma*, *A Guerra dos Clones* e *A Vingança dos Sith*.</span><span class="sxs-lookup"><span data-stu-id="0f75a-128">In this case, Mahout recommends *The Phantom Menace*, *Attack of the Clones*, and *Revenge of the Sith*.</span></span>

### <a name="understanding-the-data"></a><span data-ttu-id="0f75a-129">Compreendendo os dados</span><span class="sxs-lookup"><span data-stu-id="0f75a-129">Understanding the data</span></span>

<span data-ttu-id="0f75a-130">Convenientemente, a [GroupLens Research][movielens] oferece dados de classificação para filmes em um formato compatível com o Mahout.</span><span class="sxs-lookup"><span data-stu-id="0f75a-130">Conveniently, [GroupLens Research][movielens] provides rating data for movies in a format that is compatible with Mahout.</span></span> <span data-ttu-id="0f75a-131">Esses dados estão disponíveis no armazenamento padrão do cluster em `/HdiSamples/HdiSamples/MahoutMovieData`.</span><span class="sxs-lookup"><span data-stu-id="0f75a-131">This data is available on your cluster's default storage at `/HdiSamples/HdiSamples/MahoutMovieData`.</span></span>

<span data-ttu-id="0f75a-132">Existem dois arquivos, `moviedb.txt` e `user-ratings.txt`.</span><span class="sxs-lookup"><span data-stu-id="0f75a-132">There are two files, `moviedb.txt` and `user-ratings.txt`.</span></span> <span data-ttu-id="0f75a-133">O arquivo ratings.txt do usuário é usado durante a análise, enquanto moviedb.txt é usado para fornecer informações de texto amigável ao exibir os resultados da análise.</span><span class="sxs-lookup"><span data-stu-id="0f75a-133">The user-ratings.txt file is used during analysis, while moviedb.txt is used to provide user-friendly text information when displaying the results of the analysis.</span></span>

<span data-ttu-id="0f75a-134">Os dados contidos em user-ratings.txt têm uma estrutura de `userID`, `movieID`, `userRating` e `timestamp`, que informa a classificação que cada usuário deu a um filme.</span><span class="sxs-lookup"><span data-stu-id="0f75a-134">The data contained in user-ratings.txt has a structure of `userID`, `movieID`, `userRating`, and `timestamp`, which tells us how highly each user rated a movie.</span></span> <span data-ttu-id="0f75a-135">Aqui está um exemplo dos dados:</span><span class="sxs-lookup"><span data-stu-id="0f75a-135">Here is an example of the data:</span></span>

    196    242    3    881250949
    186    302    3    891717742
    22    377    1    878887116
    244    51    2    880606923
    166    346    1    886397596

## <a name="run-the-analysis"></a><span data-ttu-id="0f75a-136">Executar a análise</span><span class="sxs-lookup"><span data-stu-id="0f75a-136">Run the analysis</span></span>

<span data-ttu-id="0f75a-137">Em uma conexão SSH ao cluster, use o comando a seguir para executar o trabalho de recomendação:</span><span class="sxs-lookup"><span data-stu-id="0f75a-137">From an SSH connection to the cluster, use the following command to run the recommendation job:</span></span>

```bash
mahout recommenditembased -s SIMILARITY_COOCCURRENCE -i /HdiSamples/HdiSamples/MahoutMovieData/user-ratings.txt -o /example/data/mahoutout --tempDir /temp/mahouttemp
```

> [!NOTE]
> <span data-ttu-id="0f75a-138">O trabalho pode levar vários minutos para ser concluído e pode executar vários trabalhos do MapReduce.</span><span class="sxs-lookup"><span data-stu-id="0f75a-138">The job may take several minutes to complete, and may run multiple MapReduce jobs.</span></span>

## <a name="view-the-output"></a><span data-ttu-id="0f75a-139">Exibir a saída</span><span class="sxs-lookup"><span data-stu-id="0f75a-139">View the output</span></span>

1. <span data-ttu-id="0f75a-140">Quando o trabalho for concluído, use o seguinte comando para exibir a saída gerada:</span><span class="sxs-lookup"><span data-stu-id="0f75a-140">Once the job completes, use the following command to view the generated output:</span></span>

    ```bash
    hdfs dfs -text /example/data/mahoutout/part-r-00000
    ```

    <span data-ttu-id="0f75a-141">A saída é exibida da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="0f75a-141">The output appears as follows:</span></span>

        1    [234:5.0,347:5.0,237:5.0,47:5.0,282:5.0,275:5.0,88:5.0,515:5.0,514:5.0,121:5.0]
        2    [282:5.0,210:5.0,237:5.0,234:5.0,347:5.0,121:5.0,258:5.0,515:5.0,462:5.0,79:5.0]
        3    [284:5.0,285:4.828125,508:4.7543354,845:4.75,319:4.705128,124:4.7045455,150:4.6938777,311:4.6769233,248:4.65625,272:4.649266]
        4    [690:5.0,12:5.0,234:5.0,275:5.0,121:5.0,255:5.0,237:5.0,895:5.0,282:5.0,117:5.0]

    <span data-ttu-id="0f75a-142">A primeira coluna é a `userID`.</span><span class="sxs-lookup"><span data-stu-id="0f75a-142">The first column is the `userID`.</span></span> <span data-ttu-id="0f75a-143">Os valores contidos em '[' and ']' são `movieId`:`recommendationScore`.</span><span class="sxs-lookup"><span data-stu-id="0f75a-143">The values contained in '[' and ']' are `movieId`:`recommendationScore`.</span></span>

2. <span data-ttu-id="0f75a-144">Você pode usar a saída juntamente com o moviedb.txt para fornecer mais informações sobre as recomendações.</span><span class="sxs-lookup"><span data-stu-id="0f75a-144">You can use the output, along with the moviedb.txt, to provide more information on the recommendations.</span></span> <span data-ttu-id="0f75a-145">Primeiro, é necessário copiar os arquivos localmente usando os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="0f75a-145">First, we need to copy the files locally using the following commands:</span></span>

    ```bash
    hdfs dfs -get /example/data/mahoutout/part-r-00000 recommendations.txt
    hdfs dfs -get /HdiSamples/HdiSamples/MahoutMovieData/* .
    ```

    <span data-ttu-id="0f75a-146">Esse comando copiará os dados de saída em um arquivo chamado **recommendations.txt** no diretório atual, juntamente com os arquivos de dados de filme.</span><span class="sxs-lookup"><span data-stu-id="0f75a-146">This command copies the output data to a file named **recommendations.txt** in the current directory, along with the movie data files.</span></span>

3. <span data-ttu-id="0f75a-147">Use o comando a seguir para criar um script Python que pesquise nomes de filmes para os dados na saída de recomendações:</span><span class="sxs-lookup"><span data-stu-id="0f75a-147">Use the following command to create a Python script that looks up movie names for the data in the recommendations output:</span></span>

    ```bash
    nano show_recommendations.py
    ```

    <span data-ttu-id="0f75a-148">Quando o editor for aberto, use o texto a seguir como conteúdo do arquivo:</span><span class="sxs-lookup"><span data-stu-id="0f75a-148">When the editor opens, use the following text as the contents of the file:</span></span>

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

    <span data-ttu-id="0f75a-149">Pressione **Ctrl-X**, **Y** e finalmente **Enter** para salvar os dados.</span><span class="sxs-lookup"><span data-stu-id="0f75a-149">Press **Ctrl-X**, **Y**, and finally **Enter** to save the data.</span></span>

4. <span data-ttu-id="0f75a-150">Execute o script Python.</span><span class="sxs-lookup"><span data-stu-id="0f75a-150">Run the Python script.</span></span> <span data-ttu-id="0f75a-151">O comando a seguir pressupõe que você esteja no diretório em que todos os arquivos foram baixados:</span><span class="sxs-lookup"><span data-stu-id="0f75a-151">The following command assumes you are in the directory where all the files were downloaded:</span></span>

    ```bash
    python show_recommendations.py 4 user-ratings.txt moviedb.txt recommendations.txt
    ```

    <span data-ttu-id="0f75a-152">Esse comando examina as recomendações geradas para o usuário ID 4.</span><span class="sxs-lookup"><span data-stu-id="0f75a-152">This command looks at the recommendations generated for user ID 4.</span></span>

    * <span data-ttu-id="0f75a-153">O arquivo **user-ratings.txt** é usado para recuperar filmes que foram classificados.</span><span class="sxs-lookup"><span data-stu-id="0f75a-153">The **user-ratings.txt** file is used to retrieve movies that have been rated.</span></span>

    * <span data-ttu-id="0f75a-154">O arquivo **user-ratings.txt** é usado para recuperar os nomes dos filmes.</span><span class="sxs-lookup"><span data-stu-id="0f75a-154">The **moviedb.txt** file is used to retrieve the names of the movies.</span></span>

    * <span data-ttu-id="0f75a-155">O arquivo **recommendations.txt** é usado para recuperar as recomendações de filmes deste usuário.</span><span class="sxs-lookup"><span data-stu-id="0f75a-155">The **recommendations.txt** is used to retrieve the movie recommendations for this user.</span></span>

     <span data-ttu-id="0f75a-156">A saída desse comando deve ser semelhante a este texto:</span><span class="sxs-lookup"><span data-stu-id="0f75a-156">The output from this command is similar to the following text:</span></span>

        <span data-ttu-id="0f75a-157">Seven Years in Tibet (1997), score=5.0   Indiana Jones and the Last Crusade (1989), score=5.0   Jaws (1975), score=5.0   Sense and Sensibility (1995), score=5.0   Independence Day (ID4) (1996), score=5.0   My Best Friend's Wedding (1997), score=5.0   Jerry Maguire (1996), score=5.0   Scream 2 (1997), score=5.0   Time to Kill, A (1996), score=5.0</span><span class="sxs-lookup"><span data-stu-id="0f75a-157">Seven Years in Tibet (1997), score=5.0   Indiana Jones and the Last Crusade (1989), score=5.0   Jaws (1975), score=5.0   Sense and Sensibility (1995), score=5.0   Independence Day (ID4) (1996), score=5.0   My Best Friend's Wedding (1997), score=5.0   Jerry Maguire (1996), score=5.0   Scream 2 (1997), score=5.0   Time to Kill, A (1996), score=5.0</span></span>

## <a name="delete-temporary-data"></a><span data-ttu-id="0f75a-158">Excluir dados temporários</span><span class="sxs-lookup"><span data-stu-id="0f75a-158">Delete temporary data</span></span>

<span data-ttu-id="0f75a-159">Os trabalhos do Mahout não removem dados temporários criados durante o processamento do trabalho.</span><span class="sxs-lookup"><span data-stu-id="0f75a-159">Mahout jobs do not remove temporary data that is created while processing the job.</span></span> <span data-ttu-id="0f75a-160">O parâmetro `--tempDir` é especificado no trabalho de exemplo para isolar os arquivos temporários em um caminho específico para fácil exclusão.</span><span class="sxs-lookup"><span data-stu-id="0f75a-160">The `--tempDir` parameter is specified in the example job to isolate the temporary files into a specific path for easy deletion.</span></span> <span data-ttu-id="0f75a-161">Para remover os arquivos temporários, use o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="0f75a-161">To remove the temp files, use the following command:</span></span>

```bash
hdfs dfs -rm -f -r /temp/mahouttemp
```

> [!WARNING]
> <span data-ttu-id="0f75a-162">Se você quiser executar o comando novamente, você também deve excluir o diretório de saída.</span><span class="sxs-lookup"><span data-stu-id="0f75a-162">If you want to run the command again, you must also delete the output directory.</span></span> <span data-ttu-id="0f75a-163">Use o seguinte para excluir esse diretório:</span><span class="sxs-lookup"><span data-stu-id="0f75a-163">Use the following to delete this directory:</span></span>
>
> `hdfs dfs -rm -f -r /example/data/mahoutout`


## <a name="next-steps"></a><span data-ttu-id="0f75a-164">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="0f75a-164">Next steps</span></span>

<span data-ttu-id="0f75a-165">Agora que você aprendeu como usar o Mahout, descubra outras maneiras de trabalhar com dados no HDInsight:</span><span class="sxs-lookup"><span data-stu-id="0f75a-165">Now that you have learned how to use Mahout, discover other ways of working with data on HDInsight:</span></span>

* [<span data-ttu-id="0f75a-166">Hive com o HDInsight</span><span class="sxs-lookup"><span data-stu-id="0f75a-166">Hive with HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="0f75a-167">Pig com o HDInsight</span><span class="sxs-lookup"><span data-stu-id="0f75a-167">Pig with HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="0f75a-168">MapReduce com o HDInsight</span><span class="sxs-lookup"><span data-stu-id="0f75a-168">MapReduce with HDInsight</span></span>](hdinsight-use-mapreduce.md)

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
