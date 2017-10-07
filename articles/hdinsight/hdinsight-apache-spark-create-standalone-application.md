---
title: aaaCreate Scala aplicativo toorun em clusters Spark - HDInsight do Azure | Microsoft Docs
description: "Crie um aplicativo Spark escrito em Scala com Apache Maven Olá build do sistema e um arquétipo Maven existente para Scala fornecido pelo IntelliJ IDEIA."
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: b2467a40-a340-4b80-bb00-f2c3339db57b
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/25/2017
ms.author: nitinme
ms.openlocfilehash: b25291b60921021486f55d78b4832a070a54d163
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-scala-maven-application-toorun-on-apache-spark-cluster-on-hdinsight"></a>Criar um toorun de aplicativo Scala Maven no cluster do Apache Spark no HDInsight

Saiba como toocreate um aplicativo Spark escrito em Scala usando Maven IntelliJ ideia. artigo Olá usa Apache Maven hello sistema de compilação e começa com um arquétipo Maven existente para Scala fornecido pelo IntelliJ IDEIA.  Criando um aplicativo Scala no IntelliJ IDEIA envolve Olá etapas a seguir:

* Use Maven como sistema de compilação de saudação.
* Atualize as dependências do módulo Spark de tooresolve de arquivo de modelo de objeto do projeto (POM).
* Escreva seu aplicativo em Scala.
* Gere um arquivo jar que pode ser enviado tooHDInsight Spark clusters.
* Execute o aplicativo hello no cluster do Spark usando Livy.

> [!NOTE]
> HDInsight também fornece um processo IntelliJ IDEIA plug-in ferramenta tooease Olá de criar e enviar aplicativos tooan cluster HDInsight Spark no Linux. Para obter mais informações, consulte [Use HDInsight ferramentas de plug-in para toocreate IntelliJ IDEIA e enviar aplicativos Spark](hdinsight-apache-spark-intellij-tool-plugin.md).
> 
> 

## <a name="prerequisites"></a>Pré-requisitos

* Uma assinatura do Azure. Consulte [Obter avaliação gratuita do Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).
* Um cluster do Apache Spark no HDInsight. Para obter instruções, consulte o artigo sobre como [Criar clusters do Apache Spark no Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).
* Kit de desenvolvimento Oracle Java. Você pode instalá-lo clicando [aqui](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).
* Um Java IDE. Este artigo usa IntelliJ IDEA 15.0.1. Você pode instalá-lo clicando [aqui](https://www.jetbrains.com/idea/download/).

## <a name="install-scala-plugin-for-intellij-idea"></a>Instalar o plug-in Scala para IntelliJ IDEA
Se instalação de IDEIA IntelliJ não não solicitar para habilitar o plug-in de Scala, inicie o IntelliJ IDEIA e percorrer Olá plug-in de saudação de tooinstall as etapas a seguir:

1. Inicie o IntelliJ IDEA e, na tela de boas-vindas, clique em **Configurar** e, em seguida, clique em **Plug-ins**.
   
    ![Habilitar plug-in do scala](./media/hdinsight-apache-spark-create-standalone-application/enable-scala-plugin.png)
2. Na próxima tela de saudação, clique em **JetBrains instalar plug-in** do canto inferior esquerdo da saudação. Em Olá **Procurar plug-ins de JetBrains** caixa de diálogo que é aberta, procure Scala e, em seguida, clique em **instalar**.
   
    ![Instalar o plug-in do scala](./media/hdinsight-apache-spark-create-standalone-application/install-scala-plugin.png)
3. Depois de saudação plug-in foi instalado com êxito, clique em Olá **botão reiniciar IntelliJ IDEIA** toorestart Olá IDE.

## <a name="create-a-standalone-scala-project"></a>Criar um projeto de Scala autônomo
1. Inicie o IntelliJ IDEA e crie um novo projeto. Na caixa de diálogo projeto novo hello, fazer Olá opções a seguir e, em seguida, clique em **próximo**.
   
    ![Criar projeto Maven](./media/hdinsight-apache-spark-create-standalone-application/create-maven-project.png)
   
   * Selecione **Maven** como o tipo de projeto hello.
   * Especifique um **SDK do projeto**. Clique em novo e navegar o diretório de instalação do Java toohello, normalmente `C:\Program Files\Java\jdk1.8.0_66`.
   * Selecione Olá **criar do arquétipo** opção.
   * Na lista de saudação do arquétipos, selecione **org.scala tools.archetypes:scala-arquétipo simples**. Isso criará estrutura de diretório hello e baixar Olá necessário padrão dependências toowrite Scala programa.
2. Forneça os valores relevantes para **GroupId**, **ArtifactId** e **versão**. Clique em **Avançar**.
3. Na próxima caixa de diálogo hello, em que você especificar o diretório base Maven e outras configurações do usuário, aceite os padrões de saudação e clique em **próximo**.
4. Na caixa de diálogo última hello, especifique um nome de projeto e o local e, em seguida, clique em **concluir**.
5. Excluir Olá **MySpec.Scala** de arquivos no **src\test\scala\com\microsoft\spark\example**. Você não precisa isso para o aplicativo hello.
6. Se necessário, renomeie os arquivos de origem e de teste de padrão de saudação. No painel esquerdo de saudação no hello IntelliJ IDEIA, navegue muito**src\main\scala\com.microsoft.spark.example**. Clique com botão direito **App.scala**, clique em **refatorar**, clique em Renomear o arquivo e na caixa de diálogo hello, forneça Olá novo nome para o aplicativo hello e, em seguida, clique em **refatorar**.
   
    ![Renomear arquivos](./media/hdinsight-apache-spark-create-standalone-application/rename-scala-files.png)  
7. As etapas subsequentes hello, você atualizará Olá pom.xml toodefine Olá dependências Olá Spark Scala aplicativo. Para essas dependências toobe baixado e resolvidos automaticamente, que você deve configurar Maven adequadamente.
   
    ![Configurar Maven para downloads automáticos](./media/hdinsight-apache-spark-create-standalone-application/configure-maven.png)
   
   1. De saudação **arquivo** menu, clique em **configurações**.
   2. Em Olá **configurações** caixa de diálogo, navegue muito**implantação da compilação, execução,** > **ferramentas de compilação** > **Maven**  >  **Importando**.
   3. Selecione a opção de saudação muito**Maven importar projetos automaticamente**.
   4. Clique em **Aplicar** e, em seguida, clique em **OK**.
8. Atualize Olá Scala origem arquivo tooinclude seu código de aplicativo. Abrir e substitua Olá código de exemplo existente com hello código a seguir e salve as alterações de saudação. Esse código lê dados de saudação de Olá HVAC.csv (disponível em todos os clusters de HDInsight Spark), recupera linhas de saudação que têm apenas um dígito na coluna sexto hello e grava a saída de hello muito**/HVACOut** em armazenamento padrão da saudação contêiner de cluster hello.
   
        package com.microsoft.spark.example
   
        import org.apache.spark.SparkConf
        import org.apache.spark.SparkContext
   
        /**
          * Test IO toowasb
          */
        object WasbIOTest {
          def main (arg: Array[String]): Unit = {
            val conf = new SparkConf().setAppName("WASBIOTest")
            val sc = new SparkContext(conf)
   
            val rdd = sc.textFile("wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")
   
            //find hello rows which have only one digit in hello 7th column in hello CSV
            val rdd1 = rdd.filter(s => s.split(",")(6).length() == 1)
   
            rdd1.saveAsTextFile("wasb:///HVACout")
          }
        }
9. Atualize pom.xml hello.
   
   1. Dentro de `<project>\<properties>` adicione Olá seguinte:
      
          <scala.version>2.10.4</scala.version>
          <scala.compat.version>2.10.4</scala.compat.version>
          <scala.binary.version>2.10</scala.binary.version>
   2. Dentro de `<project>\<dependencies>` adicione Olá seguinte:
      
           <dependency>
             <groupId>org.apache.spark</groupId>
             <artifactId>spark-core_${scala.binary.version}</artifactId>
             <version>1.4.1</version>
           </dependency>
      
      Salve alterações toopom.xml.
10. Crie o arquivo hello. jar. O IntelliJ IDEA permite a criação de JAR como um artefato de um projeto. Execute Olá etapas a seguir.
    
    1. De saudação **arquivo** menu, clique em **estrutura do projeto**.
    2. Em Olá **estrutura do projeto** caixa de diálogo, clique em **artefatos** e, em seguida, clique em hello mais símbolo. Na caixa de diálogo pop-up de saudação, clique em **JAR**e, em seguida, clique em **de módulos com dependências**.
       
        ![Criar JAR](./media/hdinsight-apache-spark-create-standalone-application/create-jar-1.png)
    3. Em Olá **criar JAR de módulos** caixa de diálogo, clique nas reticências da saudação (![reticências](./media/hdinsight-apache-spark-create-standalone-application/ellipsis.png) ) em relação a saudação **classe principal**.
    4. Em Olá **selecionar principal classe** caixa de diálogo, a classe Olá select que é exibido por padrão e, em seguida, clique em **Okey**.
       
        ![Criar JAR](./media/hdinsight-apache-spark-create-standalone-application/create-jar-2.png)
    5. Em Olá **criar JAR de módulos** caixa de diálogo caixa, certifique-se de que a opção Olá muito**extrair toohello destino JAR** está selecionado e, em seguida, clique em **Okey**. Isso cria um JAR único com todas as dependências.
       
        ![Criar JAR](./media/hdinsight-apache-spark-create-standalone-application/create-jar-3.png)
    6. Guia de layout de saída Olá lista todos os jars Olá que estão incluídos como parte do projeto de Maven hello. Você pode selecionar e excluir Olá aqueles nos quais Olá Scala aplicativo não tem nenhuma dependência direta. Para o aplicativo hello, estamos criando aqui, você pode remover Olá tudo, exceto o último (**SparkSimpleApp saída de compilação**). Selecione Olá jars toodelete e clique em Olá **excluir** ícone.
       
        ![Criar JAR](./media/hdinsight-apache-spark-create-standalone-application/delete-output-jars.png)
       
        Certifique-se de **compilar no Verifique** caixa é selecionada, o que garante que jar Olá é criado sempre que o projeto Olá for criado ou atualizado. Clique em **Aplicar** e em **OK**.
    7. Olá barra de menus, clique em **criar**e, em seguida, clique em **projeto Make**. Você também pode clicar em **criar artefatos** toocreate jar de saudação. Olá jar de saída é criado sob **\out\artifacts**.
       
        ![Criar JAR](./media/hdinsight-apache-spark-create-standalone-application/output.png)

## <a name="run-hello-application-on-hello-spark-cluster"></a>Executar o aplicativo hello no cluster do Spark Olá
aplicativo de hello toorun no cluster hello, você deve fazer a seguir hello:

* **Blob de armazenamento do Azure cópia Olá aplicativo jar toohello** associada Olá cluster. Você pode usar [ **AzCopy**](../storage/common/storage-use-azcopy.md), um comando de linha utilitário, toodo assim. Há muitos outros clientes assim que você pode usar dados tooupload. É possível saber mais sobre eles em [Carregar dados para trabalhos do Hadoop no HDInsight](hdinsight-upload-data.md).
* **Use Livy toosubmit um trabalho de aplicativo remotamente** toohello cluster do Spark. Clusters Spark no HDInsight inclui Livy que expõe os demais pontos de extremidade tooremotely enviar trabalhos Spark. Para obter mais informações, consulte [Enviar trabalhos do Spark remotamente usando Livy com clusters Spark no HDInsight](hdinsight-apache-spark-livy-rest-interface.md).

## <a name="next-step"></a>Próxima etapa

Neste artigo, você aprendeu como toocreate um aplicativo de scala Spark. Adiantamento toohello próximo artigo toolearn como toorun este aplicativo em um HDInsight Spark cluster usando Livy.

> [!div class="nextstepaction"]
>[Executar trabalhos remotamente em um cluster do Spark usando Livy](hdinsight-apache-spark-livy-rest-interface.md)

