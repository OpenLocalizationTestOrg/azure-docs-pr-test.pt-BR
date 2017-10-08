---
title: aaaUse Kit de ferramentas do Azure para IntelliJ com Hortonworks Sandbox | Microsoft Docs
description: Saiba como toouse HDInsight ferramentas no Kit de ferramentas do Azure para IntelliJ com Hortonworks seguro.
keywords: "ferramentas do hadoop,consulta do hive,intellij,área restrita do hortonworks,kit de ferramentas do azure para intellij"
services: HDInsight
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: b587cc9b-a41a-49ac-998f-b54d6c0bdfe0
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/25/2017
ms.author: jgao
ms.openlocfilehash: 2bf97068a9cec99fcc7b4ff9469b91d8cbe2a8d8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hdinsight-tools-for-intellij-with-hortonworks-sandbox"></a>Usar ferramentas de HDInsight para IntelliJ com a área restrita do Hortonworks

Saiba como toouse ferramentas do HDInsight para IntelliJ toodevelop Apache Scala aplicativos e, então, testar Olá aplicativos em [Hortonworks Sandbox](http://hortonworks.com/products/sandbox/) em execução em sua estação de trabalho. 

[IntelliJ IDEA](https://www.jetbrains.com/idea/) é um ambiente de desenvolvimento integrado Java (IDE) para o desenvolvimento de software de computador. Depois de ter desenvolvido e testar seus aplicativos na área restrita do Hortonworks, você pode movê-los muito[HDInsight do Azure](hdinsight-hadoop-introduction.md).

## <a name="prerequisites"></a>Pré-requisitos

Antes de começar este tutorial, você deverá ter o seguinte:

- HDP (Plataforma de Dados do Hortonworks) 2.4 na Área Restrita do Hortonworks em execução no seu ambiente local. tooconfigure HDP, consulte [começar no ecossistema do Hadoop Olá com um sandbox Hadoop em uma máquina virtual](hdinsight-hadoop-emulator-get-started.md). 
    >[!NOTE]
    >As Ferramentas do HDInsight para IntelliJ foram testadas somente com HDP 2.4. tooget HDP 2.4, expanda **Hortonworks Sandbox arquivamento** em Olá [Hortonworks Sandbox downloads site](http://hortonworks.com/downloads/#sandbox).

- [Java Developer Kit (JDK) versão 1.8 ou posterior](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html). JDK é exigida pelo Olá Kit de ferramentas do Azure para IntelliJ.

- [Edição de comunidade IDEIA IntelliJ](https://www.jetbrains.com/idea/download) com hello [Scala](https://plugins.jetbrains.com/idea/plugin/1347-scala) plug-in e hello [Kit de ferramentas do Azure para IntelliJ](../azure-toolkit-for-intellij.md) plug-in. Ferramentas de HDInsight para IntelliJ está disponível como parte do Kit de ferramentas do Azure para IntelliJ de saudação. 

  tooinstall Olá plug-ins, Olá a seguir:

  1. Abra o IntelliJ IDEA.
  2. Em Olá **bem-vindo** tela, selecione **configurar**e, em seguida, selecione **plug-ins**.
  3. Selecione **JetBrains instalar plug-in** no canto inferior esquerdo de saudação.
  4. Use Olá toosearch de função de pesquisa para **Scala**e, em seguida, selecione **instalar**.
  5. Selecione **reiniciar IntelliJ IDEIA** toocomplete instalação de saudação.
  6. Saudação de tooinstall Repita a etapa 4 e 5 **Kit de ferramentas do Azure para IntelliJ**. Para obter mais informações, consulte [Olá instalar o Kit de ferramentas do Azure para IntelliJ](../azure-toolkit-for-intellij-installation.md).

## <a name="create-a-spark-scala-application"></a>Criar um aplicativo Spark Scala

Nesta seção, você cria um projeto de exemplo do Scala usando o IntelliJ IDEA. Na próxima seção, Olá, você vincular IDEIA IntelliJ toohello Hortonworks área restrita (emulador) antes de enviar o projeto de saudação.

1. Abra IntelliJ IDEA de sua estação de trabalho. Em Olá **novo projeto** caixa de diálogo caixa, Olá a seguir:

   a. Selecione **HDInsight** > **Spark no HDInsight (Scala)**.

   b. Em Olá **ferramenta de compilação** , selecione qualquer uma das Olá a seguir, de acordo com a necessidade de tooyour:

    * **Maven**, para obter suporte ao assistente de criação de projetos Scala
    * **SBT**, para gerenciar dependências hello e criação de projeto de Scala Olá

   ![caixa de diálogo Novo projeto Olá](./media/hdinsight-tools-for-intellij-with-hortonworks-sandbox/intellij-create-scala-project.png)

2. Selecione **Avançar**.

3. Em Olá próximo **novo projeto** caixa de diálogo caixa, Olá a seguir:

    ![Criar IntelliJ Scala propriedades do projeto](./media/hdinsight-tools-for-intellij-with-hortonworks-sandbox/intellij-create-scala-project-properties.png)

    a. Em Olá **nome do projeto** , digite um nome de projeto.

    b. Em Olá **local do projeto** caixa, digite o local do projeto.

    c. Próxima toohello **projeto SDK** lista suspensa, selecione **novo**, selecione **JDK**, e, em seguida, especifique a pasta de saudação do JDK Java versão 1.7 ou posterior. Selecione **Java 1.8** para cluster de 2. x Spark hello, ou selecione **Java 1.7** para cluster 1. x do hello Spark. local do saudação padrão é C:\Program Files\Java\jdk1.8.x_xxx.

    d. Em Olá **versão Spark** lista suspensa, o Assistente de criação de projeto Scala se integra a versão correta do Olá para Spark SDK e Scala SDK. Se a versão do cluster Spark Olá for anterior à 2.0, selecione **despertar 1. x**. Caso contrário, selecione **Spark 2.x**. Esse exemplo usa o Spark 1.6.2 (Scala 2.10.5). Certifique-se de que você está usando o repositório de saudação marcado Scala 2.10.x. Não use o repositório Olá marcado Scala 2.11.x.

4. Selecione **Concluir**.

5. Se hello **projeto** exibição não ainda estiver aberta, pressione **Alt + 1** tooopen-lo.

6. Em **Explorador de projeto**, expanda o projeto hello e, em seguida, selecione **src**.

7. Clique com botão direito **src**, ponto muito**novo**e, em seguida, selecione **Scala classe**.

8. Em Olá **nome** , digite um nome em Olá **tipo** selecione **objeto**e, em seguida, selecione **Okey**.

    ![janela de criar uma nova classe de Scala Olá](./media/hdinsight-tools-for-intellij-with-hortonworks-sandbox/intellij-create-new-scala-class.png)

9. No arquivo de .scala hello, cole Olá código a seguir:

        import java.util.Random
        import org.apache.spark.{SparkConf, SparkContext}
        import org.apache.spark.SparkContext._

        /**
        * Usage: GroupByTest [numMappers] [numKVPairs] [valSize] [numReducers]
        */
        object GroupByTest {
            def main(args: Array[String]) {
                val sparkConf = new SparkConf().setAppName("GroupBy Test")
                var numMappers = 3
                var numKVPairs = 10
                var valSize = 10
                var numReducers = 2

                val sc = new SparkContext(sparkConf)

                val pairs1 = sc.parallelize(0 until numMappers, numMappers).flatMap { p =>
                val ranGen = new Random
                var arr1 = new Array[(Int, Array[Byte])](numKVPairs)
                for (i <- 0 until numKVPairs) {
                    val byteArr = new Array[Byte](valSize)
                    ranGen.nextBytes(byteArr)
                    arr1(i) = (ranGen.nextInt(Int.MaxValue), byteArr)
                }
                arr1
                }.cache
                // Enforce that everything has been calculated and in cache
                pairs1.count

                println(pairs1.groupByKey(numReducers).count)
            }
        }

10. Em Olá **criar** menu, selecione **projeto de compilação**. Certifique-se de que compilação Olá foi concluída com êxito.


## <a name="link-toohello-hortonworks-sandbox"></a>Vincular toohello Hortonworks seguro

Antes de poder vincular tooa Hortonworks área restrita (emulador), você deve ter um aplicativo IntelliJ existente.

emulador de tooan toolink, Olá a seguir:

1. Projeto de saudação aberto no IntelliJ.

2. Em Olá **exibição** menu, selecione **ferramentas Windows**e, em seguida, selecione **Azure Explorer**.

3. Expanda **Azure**, clique com o botão direito do mouse em **HDInsight** e, em seguida, selecione **Vincular um Emulador**.

4. Em Olá **Link um novo emulador** janela, digite a senha de saudação configurou para a conta raiz de saudação do hello Hortonworks Sandbox, digite toothose de valores semelhantes no hello captura de tela a seguir e, em seguida, selecione **Okey** . 

   ![janela de "Vincular um novo emulador" Hello](./media/hdinsight-tools-for-intellij-with-hortonworks-sandbox/intellij-link-an-emulator.png)

5. emulador de saudação tooconfigure, selecione **Sim**.

Quando emulador Olá estiver conectado com êxito, emulador hello (Hortonworks área restrita) é listado no nó de HDInsight hello.

## <a name="submit-hello-spark-scala-application-toohello-hortonworks-sandbox"></a>Enviar Olá Spark Scala aplicativo toohello Hortonworks seguro

Depois de vincular o emulador de toohello IntelliJ IDEIA, você poderá enviar seu projeto.

toosubmit um emulador de tooan de projeto, Olá a seguir:

1. Em **Explorador de projeto**, clique com botão direito hello e, em seguida, selecione **tooHDInsight do aplicativo de envio Spark**.

2. Olá a seguir:

    a. Em Olá **cluster Spark (Linux)** lista suspensa, selecione o local seguro de Hortonworks.

    b. Em Olá **nome da classe principal** caixa, escolha ou insira o nome da classe principal de saudação. Para este tutorial, o nome de saudação é **GroupByTest**.

3. Selecione **Enviar**. Olá logs de envio de trabalho são mostrados na janela de ferramenta de envio Olá Spark.

## <a name="next-steps"></a>Próximas etapas

- toolearn como toocreate aplicativos de Spark para HDInsight usando ferramentas de HDInsight para IntelliJ, ir muito[usar ferramentas de HDInsight no Kit de ferramentas do Azure para aplicativos do IntelliJ toocreate Spark para HDInsight Spark Linux cluster](hdinsight-apache-spark-intellij-tool-plugin.md).

- toowatch um vídeo de ferramentas de HDInsight para IntelliJ, ir muito[introduzir ferramentas de HDInsight para IntelliJ para desenvolvimento Spark](https://www.youtube.com/watch?v=YTZzYVgut6c).

- toolearn como aplicativos de Spark toodebug usando Olá toolkit remotamente no HDInsight por meio do SSH, ir muito[depurar remotamente aplicativos Spark em um cluster de HDInsight com o Kit de ferramentas do Azure para IntelliJ por meio do SSH](hdinsight-apache-spark-intellij-tool-debug-remotely-through-ssh.md).

- toolearn como aplicativos de Spark toodebug usando Olá toolkit remotamente no HDInsight por meio de VPN, vá muito[usar ferramentas de HDInsight no Kit de ferramentas do Azure para aplicativos de Spark toodebug IntelliJ remotamente no cluster HDInsight Spark Linux](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md).

- toolearn como toouse ferramentas HDInsight para Eclipse toocreate um aplicativo Spark, ir muito[usar ferramentas de HDInsight no Kit de ferramentas do Azure para aplicativos do Eclipse toocreate Spark](hdinsight-apache-spark-eclipse-tool-plugin.md).

- toowatch um vídeo de ferramentas HDInsight para o Eclipse, vá muito[usar a ferramenta de HDInsight para aplicativos do Eclipse toocreate Spark](https://mix.office.com/watch/1rau2mopb6fha).
