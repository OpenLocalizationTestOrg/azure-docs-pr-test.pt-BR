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
# <a name="generate-movie-recommendations-by-using-apache-mahout-with-linux-based-hadoop-in-hdinsight-ssh"></a><span data-ttu-id="9a5a8-103">Gerar recomendações de filmes usando o Apache Mahout com o Hadoop para Linux no HDInsight (SSH)</span><span class="sxs-lookup"><span data-stu-id="9a5a8-103">Generate movie recommendations by using Apache Mahout with Linux-based Hadoop in HDInsight (SSH)</span></span>

[!INCLUDE [mahout-selector](../../includes/hdinsight-selector-mahout.md)]

<span data-ttu-id="9a5a8-104">Saiba como Olá toouse [Mahout Apache](http://mahout.apache.org) biblioteca de aprendizado de máquina com recomendações de filme toogenerate HDInsight do Azure.</span><span class="sxs-lookup"><span data-stu-id="9a5a8-104">Learn how toouse hello [Apache Mahout](http://mahout.apache.org) machine learning library with Azure HDInsight toogenerate movie recommendations.</span></span>

<span data-ttu-id="9a5a8-105">O Mahout é uma biblioteca de [machine learning][ml] para o Apache Hadoop.</span><span class="sxs-lookup"><span data-stu-id="9a5a8-105">Mahout is a [machine learning][ml] library for Apache Hadoop.</span></span> <span data-ttu-id="9a5a8-106">O Mahout contém algoritmos para processamento de dados, como filtragem, classificação e clustering.</span><span class="sxs-lookup"><span data-stu-id="9a5a8-106">Mahout contains algorithms for processing data, such as filtering, classification, and clustering.</span></span> <span data-ttu-id="9a5a8-107">Neste artigo, você deve usar uma recomendação mecanismo toogenerate filme as recomendações se baseiam em filmes viu seus amigos.</span><span class="sxs-lookup"><span data-stu-id="9a5a8-107">In this article, you use a recommendation engine toogenerate movie recommendations that are based on movies your friends have seen.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9a5a8-108">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="9a5a8-108">Prerequisites</span></span>

* <span data-ttu-id="9a5a8-109">Criar um cluster HDInsight baseado em Linux.</span><span class="sxs-lookup"><span data-stu-id="9a5a8-109">A Linux-based HDInsight cluster.</span></span> <span data-ttu-id="9a5a8-110">Para saber mais sobre como criar um, confira [Introdução ao uso do Hadoop baseado em Linux no HDInsight][getstarted].</span><span class="sxs-lookup"><span data-stu-id="9a5a8-110">For information about creating one, see [Get started using Linux-based Hadoop in HDInsight][getstarted].</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9a5a8-111">Linux é Olá sistema operacional somente de usado no HDInsight versão 3.4 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="9a5a8-111">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="9a5a8-112">Para obter mais informações, confira [baixa do HDInsight no Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="9a5a8-112">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="9a5a8-113">Um cliente SSH.</span><span class="sxs-lookup"><span data-stu-id="9a5a8-113">An SSH client.</span></span> <span data-ttu-id="9a5a8-114">Para obter mais informações, consulte Olá [usar SSH com HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) documento.</span><span class="sxs-lookup"><span data-stu-id="9a5a8-114">For more information, see hello [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) document.</span></span>

## <a name="mahout-versioning"></a><span data-ttu-id="9a5a8-115">Versões do Mahout</span><span class="sxs-lookup"><span data-stu-id="9a5a8-115">Mahout versioning</span></span>

<span data-ttu-id="9a5a8-116">Para obter mais informações sobre a versão de saudação do Mahout no HDInsight, consulte [HDInsight versões e componentes do Hadoop](hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="9a5a8-116">For more information about hello version of Mahout in HDInsight, see [HDInsight versions and Hadoop components](hdinsight-component-versioning.md).</span></span>

## <span data-ttu-id="9a5a8-117"><a name="recommendations"></a>Entendendo as recomendações</span><span class="sxs-lookup"><span data-stu-id="9a5a8-117"><a name="recommendations"></a>Understanding recommendations</span></span>

<span data-ttu-id="9a5a8-118">Uma das funções de saudação que é fornecido por Mahout é um mecanismo de recomendação.</span><span class="sxs-lookup"><span data-stu-id="9a5a8-118">One of hello functions that is provided by Mahout is a recommendation engine.</span></span> <span data-ttu-id="9a5a8-119">Esse mecanismo aceita dados em formato de saudação do `userID`, `itemId`, e `prefValue` (Olá preferência para o item de saudação).</span><span class="sxs-lookup"><span data-stu-id="9a5a8-119">This engine accepts data in hello format of `userID`, `itemId`, and `prefValue` (hello preference for hello item).</span></span> <span data-ttu-id="9a5a8-120">Mahout pode executar a ocorrência colegas analysis toodetermine: *os usuários com a preferência de um item também têm uma preferência para esses outros itens*.</span><span class="sxs-lookup"><span data-stu-id="9a5a8-120">Mahout can then perform co-occurance analysis toodetermine: *users who have a preference for an item also have a preference for these other items*.</span></span> <span data-ttu-id="9a5a8-121">Mahout determina, em seguida, os usuários com as preferências de tipo de item, que podem ser usado toomake recomendações.</span><span class="sxs-lookup"><span data-stu-id="9a5a8-121">Mahout then determines users with like-item preferences, which can be used toomake recommendations.</span></span>

<span data-ttu-id="9a5a8-122">Olá seguinte fluxo de trabalho é um exemplo simplificado que usa dados do filme:</span><span class="sxs-lookup"><span data-stu-id="9a5a8-122">hello following workflow is a simplified example that uses movie data:</span></span>

* <span data-ttu-id="9a5a8-123">**Ocorrência colegas**: Joe, Alice e Bob vinculadas todos os *estrela guerras*, *Olá Empire greves volta*, e *retorno de saudação Jedi*.</span><span class="sxs-lookup"><span data-stu-id="9a5a8-123">**Co-occurance**: Joe, Alice, and Bob all liked *Star Wars*, *hello Empire Strikes Back*, and *Return of hello Jedi*.</span></span> <span data-ttu-id="9a5a8-124">Mahout determina que os usuários que também como qualquer um desses filmes Olá outras duas.</span><span class="sxs-lookup"><span data-stu-id="9a5a8-124">Mahout determines that users who like any one of these movies also like hello other two.</span></span>

* <span data-ttu-id="9a5a8-125">**Ocorrência colegas**: Bob e Alice também gostaram *Olá fantasma ameaça*, *ataque de Clones Olá*, e *Vingança de saudação Sith*.</span><span class="sxs-lookup"><span data-stu-id="9a5a8-125">**Co-occurance**: Bob and Alice also liked *hello Phantom Menace*, *Attack of hello Clones*, and *Revenge of hello Sith*.</span></span> <span data-ttu-id="9a5a8-126">Mahout determina que os usuários que gostaram filmes de três anterior Olá também como esses três filmes.</span><span class="sxs-lookup"><span data-stu-id="9a5a8-126">Mahout determines that users who liked hello previous three movies also like these three movies.</span></span>

* <span data-ttu-id="9a5a8-127">**Recomendação de similaridade**: Joe porque gostou Olá três primeiros filmes, Mahout examina filmes que outras pessoas com as preferências semelhantes gostou, mas Joe não tem observados (gostou/classificado).</span><span class="sxs-lookup"><span data-stu-id="9a5a8-127">**Similarity recommendation**: Because Joe liked hello first three movies, Mahout looks at movies that others with similar preferences liked, but Joe has not watched (liked/rated).</span></span> <span data-ttu-id="9a5a8-128">Nesse caso, recomenda Mahout *Olá fantasma ameaça*, *ataque de Clones Olá*, e *Vingança de saudação Sith*.</span><span class="sxs-lookup"><span data-stu-id="9a5a8-128">In this case, Mahout recommends *hello Phantom Menace*, *Attack of hello Clones*, and *Revenge of hello Sith*.</span></span>

### <a name="understanding-hello-data"></a><span data-ttu-id="9a5a8-129">Noções básicas sobre dados saudação</span><span class="sxs-lookup"><span data-stu-id="9a5a8-129">Understanding hello data</span></span>

<span data-ttu-id="9a5a8-130">Convenientemente, a [GroupLens Research][movielens] oferece dados de classificação para filmes em um formato compatível com o Mahout.</span><span class="sxs-lookup"><span data-stu-id="9a5a8-130">Conveniently, [GroupLens Research][movielens] provides rating data for movies in a format that is compatible with Mahout.</span></span> <span data-ttu-id="9a5a8-131">Esses dados estão disponíveis no armazenamento padrão do cluster em `/HdiSamples/HdiSamples/MahoutMovieData`.</span><span class="sxs-lookup"><span data-stu-id="9a5a8-131">This data is available on your cluster's default storage at `/HdiSamples/HdiSamples/MahoutMovieData`.</span></span>

<span data-ttu-id="9a5a8-132">Existem dois arquivos, `moviedb.txt` e `user-ratings.txt`.</span><span class="sxs-lookup"><span data-stu-id="9a5a8-132">There are two files, `moviedb.txt` and `user-ratings.txt`.</span></span> <span data-ttu-id="9a5a8-133">arquivo de usuário ratings.txt Olá é usado durante a análise, enquanto moviedb.txt é uma informação de texto amigável tooprovide usado ao exibir os resultados de saudação da análise de saudação.</span><span class="sxs-lookup"><span data-stu-id="9a5a8-133">hello user-ratings.txt file is used during analysis, while moviedb.txt is used tooprovide user-friendly text information when displaying hello results of hello analysis.</span></span>

<span data-ttu-id="9a5a8-134">dados contidos no usuário ratings.txt Hello tem uma estrutura de `userID`, `movieID`, `userRating`, e `timestamp`, que informa como altamente cada usuário classificado como um filme.</span><span class="sxs-lookup"><span data-stu-id="9a5a8-134">hello data contained in user-ratings.txt has a structure of `userID`, `movieID`, `userRating`, and `timestamp`, which tells us how highly each user rated a movie.</span></span> <span data-ttu-id="9a5a8-135">Aqui está um exemplo de dados de saudação:</span><span class="sxs-lookup"><span data-stu-id="9a5a8-135">Here is an example of hello data:</span></span>

    196    242    3    881250949
    186    302    3    891717742
    22    377    1    878887116
    244    51    2    880606923
    166    346    1    886397596

## <a name="run-hello-analysis"></a><span data-ttu-id="9a5a8-136">Executar a análise de saudação</span><span class="sxs-lookup"><span data-stu-id="9a5a8-136">Run hello analysis</span></span>

<span data-ttu-id="9a5a8-137">De um cluster de toohello de conexão SSH, use Olá trabalho de recomendação de saudação do comando toorun a seguir:</span><span class="sxs-lookup"><span data-stu-id="9a5a8-137">From an SSH connection toohello cluster, use hello following command toorun hello recommendation job:</span></span>

```bash
mahout recommenditembased -s SIMILARITY_COOCCURRENCE -i /HdiSamples/HdiSamples/MahoutMovieData/user-ratings.txt -o /example/data/mahoutout --tempDir /temp/mahouttemp
```

> [!NOTE]
> <span data-ttu-id="9a5a8-138">Olá trabalho pode levar vários toocomplete de minutos e pode executar vários trabalhos de MapReduce.</span><span class="sxs-lookup"><span data-stu-id="9a5a8-138">hello job may take several minutes toocomplete, and may run multiple MapReduce jobs.</span></span>

## <a name="view-hello-output"></a><span data-ttu-id="9a5a8-139">Exibir saída de hello</span><span class="sxs-lookup"><span data-stu-id="9a5a8-139">View hello output</span></span>

1. <span data-ttu-id="9a5a8-140">Após a conclusão do trabalho hello, use Olá após a saída do comando tooview Olá gerado:</span><span class="sxs-lookup"><span data-stu-id="9a5a8-140">Once hello job completes, use hello following command tooview hello generated output:</span></span>

    ```bash
    hdfs dfs -text /example/data/mahoutout/part-r-00000
    ```

    <span data-ttu-id="9a5a8-141">saída de Hello aparece da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="9a5a8-141">hello output appears as follows:</span></span>

        1    [234:5.0,347:5.0,237:5.0,47:5.0,282:5.0,275:5.0,88:5.0,515:5.0,514:5.0,121:5.0]
        2    [282:5.0,210:5.0,237:5.0,234:5.0,347:5.0,121:5.0,258:5.0,515:5.0,462:5.0,79:5.0]
        3    [284:5.0,285:4.828125,508:4.7543354,845:4.75,319:4.705128,124:4.7045455,150:4.6938777,311:4.6769233,248:4.65625,272:4.649266]
        4    [690:5.0,12:5.0,234:5.0,275:5.0,121:5.0,255:5.0,237:5.0,895:5.0,282:5.0,117:5.0]

    <span data-ttu-id="9a5a8-142">Olá primeira coluna é Olá `userID`.</span><span class="sxs-lookup"><span data-stu-id="9a5a8-142">hello first column is hello `userID`.</span></span> <span data-ttu-id="9a5a8-143">Olá valores contidos em ' [' e ']' são `movieId`:`recommendationScore`.</span><span class="sxs-lookup"><span data-stu-id="9a5a8-143">hello values contained in '[' and ']' are `movieId`:`recommendationScore`.</span></span>

2. <span data-ttu-id="9a5a8-144">Você pode usar a saída de hello, juntamente com hello moviedb.txt, tooprovide obter mais informações sobre recomendações de saudação.</span><span class="sxs-lookup"><span data-stu-id="9a5a8-144">You can use hello output, along with hello moviedb.txt, tooprovide more information on hello recommendations.</span></span> <span data-ttu-id="9a5a8-145">Primeiro, precisamos de arquivos de saudação toocopy localmente usando Olá comandos a seguir:</span><span class="sxs-lookup"><span data-stu-id="9a5a8-145">First, we need toocopy hello files locally using hello following commands:</span></span>

    ```bash
    hdfs dfs -get /example/data/mahoutout/part-r-00000 recommendations.txt
    hdfs dfs -get /HdiSamples/HdiSamples/MahoutMovieData/* .
    ```

    <span data-ttu-id="9a5a8-146">Este comando copia Olá arquivo de tooa de dados de saída denominado **recommendations.txt** no diretório atual hello, juntamente com os arquivos de dados do filme hello.</span><span class="sxs-lookup"><span data-stu-id="9a5a8-146">This command copies hello output data tooa file named **recommendations.txt** in hello current directory, along with hello movie data files.</span></span>

3. <span data-ttu-id="9a5a8-147">Use Olá comando toocreate um script de Python procura nomes de filme para dados de saudação na saída do hello recomendações a seguir:</span><span class="sxs-lookup"><span data-stu-id="9a5a8-147">Use hello following command toocreate a Python script that looks up movie names for hello data in hello recommendations output:</span></span>

    ```bash
    nano show_recommendations.py
    ```

    <span data-ttu-id="9a5a8-148">Quando abre o editor de hello, use Olá depois do texto como conteúdo de saudação do arquivo hello:</span><span class="sxs-lookup"><span data-stu-id="9a5a8-148">When hello editor opens, use hello following text as hello contents of hello file:</span></span>

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

    <span data-ttu-id="9a5a8-149">Pressione **Ctrl-X**, **Y**e, finalmente, **Enter** toosave dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="9a5a8-149">Press **Ctrl-X**, **Y**, and finally **Enter** toosave hello data.</span></span>

4. <span data-ttu-id="9a5a8-150">Execute o script de Python hello.</span><span class="sxs-lookup"><span data-stu-id="9a5a8-150">Run hello Python script.</span></span> <span data-ttu-id="9a5a8-151">Olá comando a seguir supõe que você está no diretório Olá onde todos os arquivos de saudação foram baixados:</span><span class="sxs-lookup"><span data-stu-id="9a5a8-151">hello following command assumes you are in hello directory where all hello files were downloaded:</span></span>

    ```bash
    python show_recommendations.py 4 user-ratings.txt moviedb.txt recommendations.txt
    ```

    <span data-ttu-id="9a5a8-152">Esse comando examina recomendações Olá geradas para 4 ID de usuário.</span><span class="sxs-lookup"><span data-stu-id="9a5a8-152">This command looks at hello recommendations generated for user ID 4.</span></span>

    * <span data-ttu-id="9a5a8-153">Olá **ratings.txt usuário** arquivo é usado tooretrieve filmes que tenham sido classificados.</span><span class="sxs-lookup"><span data-stu-id="9a5a8-153">hello **user-ratings.txt** file is used tooretrieve movies that have been rated.</span></span>

    * <span data-ttu-id="9a5a8-154">Olá **moviedb.txt** arquivo é usado tooretrieve Olá nomes de filmes hello.</span><span class="sxs-lookup"><span data-stu-id="9a5a8-154">hello **moviedb.txt** file is used tooretrieve hello names of hello movies.</span></span>

    * <span data-ttu-id="9a5a8-155">Olá **recommendations.txt** é usado tooretrieve recomendações de filme Olá para este usuário.</span><span class="sxs-lookup"><span data-stu-id="9a5a8-155">hello **recommendations.txt** is used tooretrieve hello movie recommendations for this user.</span></span>

     <span data-ttu-id="9a5a8-156">saudação de saída desse comando é semelhante toohello seguinte texto:</span><span class="sxs-lookup"><span data-stu-id="9a5a8-156">hello output from this command is similar toohello following text:</span></span>

        <span data-ttu-id="9a5a8-157">Pontuação de sete anos no Tibete (1997) = 5.0 Indiana Jones e hello última campanha (1989), pontuação = 5.0 Jaws (1975), pontuação = 5.0 sentido e Sensibility (1995), pontuação = 5.0 independência (ID4) (1996), pontuação = 5.0 meu melhor amigo casamento (1997), pontuação = 5.0 Jerry Maguire (1996 ), pontuação = 5.0 Scream 2 (1997), pontuação = 5.0 tooKill de tempo, (1996), pontuação = 5.0</span><span class="sxs-lookup"><span data-stu-id="9a5a8-157">Seven Years in Tibet (1997), score=5.0   Indiana Jones and hello Last Crusade (1989), score=5.0   Jaws (1975), score=5.0   Sense and Sensibility (1995), score=5.0   Independence Day (ID4) (1996), score=5.0   My Best Friend's Wedding (1997), score=5.0   Jerry Maguire (1996), score=5.0   Scream 2 (1997), score=5.0   Time tooKill, A (1996), score=5.0</span></span>

## <a name="delete-temporary-data"></a><span data-ttu-id="9a5a8-158">Excluir dados temporários</span><span class="sxs-lookup"><span data-stu-id="9a5a8-158">Delete temporary data</span></span>

<span data-ttu-id="9a5a8-159">Trabalhos mahout não remova os dados temporários que são criados durante o processamento de trabalho hello.</span><span class="sxs-lookup"><span data-stu-id="9a5a8-159">Mahout jobs do not remove temporary data that is created while processing hello job.</span></span> <span data-ttu-id="9a5a8-160">Olá `--tempDir` parâmetro é especificado em Olá exemplo trabalho tooisolate Olá os arquivos temporários em um caminho específico para exclusão fácil.</span><span class="sxs-lookup"><span data-stu-id="9a5a8-160">hello `--tempDir` parameter is specified in hello example job tooisolate hello temporary files into a specific path for easy deletion.</span></span> <span data-ttu-id="9a5a8-161">arquivos temporários do tooremove hello, use Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="9a5a8-161">tooremove hello temp files, use hello following command:</span></span>

```bash
hdfs dfs -rm -f -r /temp/mahouttemp
```

> [!WARNING]
> <span data-ttu-id="9a5a8-162">Se você quiser novamente o comando de saudação toorun, você também deve excluir o diretório de saída hello.</span><span class="sxs-lookup"><span data-stu-id="9a5a8-162">If you want toorun hello command again, you must also delete hello output directory.</span></span> <span data-ttu-id="9a5a8-163">Use Olá toodelete a seguir neste diretório:</span><span class="sxs-lookup"><span data-stu-id="9a5a8-163">Use hello following toodelete this directory:</span></span>
>
> `hdfs dfs -rm -f -r /example/data/mahoutout`


## <a name="next-steps"></a><span data-ttu-id="9a5a8-164">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="9a5a8-164">Next steps</span></span>

<span data-ttu-id="9a5a8-165">Agora que você aprendeu como toouse Mahout, descubra outras maneiras de trabalhar com dados no HDInsight:</span><span class="sxs-lookup"><span data-stu-id="9a5a8-165">Now that you have learned how toouse Mahout, discover other ways of working with data on HDInsight:</span></span>

* [<span data-ttu-id="9a5a8-166">Hive com o HDInsight</span><span class="sxs-lookup"><span data-stu-id="9a5a8-166">Hive with HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="9a5a8-167">Pig com o HDInsight</span><span class="sxs-lookup"><span data-stu-id="9a5a8-167">Pig with HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="9a5a8-168">MapReduce com o HDInsight</span><span class="sxs-lookup"><span data-stu-id="9a5a8-168">MapReduce with HDInsight</span></span>](hdinsight-use-mapreduce.md)

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
