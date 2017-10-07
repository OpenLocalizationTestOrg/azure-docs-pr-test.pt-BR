---
title: aaaAzure Kit de ferramentas para IntelliJ - depurar aplicativos remotamente no HDInsight Spark | Microsoft Docs
description: Saiba como usar as ferramentas do HDInsight no Kit de ferramentas do Azure para IntelliJ tooremotely depurar aplicativos executados em clusters de HDInsight Spark por meio de vpn.
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 55fb454f-c7dc-46de-a978-e242e9a94f4c
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: ad67d23bf609d0a7afb38b2acb110062f8b27b39
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-toolkit-for-intellij-toodebug-applications-remotely-on-hdinsight-spark-through-vpn"></a>Use o Kit de ferramentas do Azure para aplicativos de toodebug IntelliJ remotamente no HDInsight Spark por meio de VPN

Recomendamos a forma de saudação de depuração remotamente por meio de applicaltion spark ssh. Para obter instruções, consulte [Depurar aplicativos Spark remotamente em um cluster HDInsight com o kit de ferramentas do Azure para IntelliJ por meio do SSH](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-apache-spark-intellij-tool-debug-remotely-through-ssh).

Este artigo fornece orientações passo a passo sobre como toouse hello ferramentas HDInsight no Kit de ferramentas do Azure para IntelliJ toosubmit um trabalho Spark no cluster HDInsight Spark e depurá-lo remotamente de um computador desktop. toodo, portanto, você deve executar Olá seguindo as etapas de alto nível:

1. Crie uma Rede Virtual do Azure site a site ou ponto a site. etapas de saudação neste documento pressupõem que você use uma rede site a site.
2. Crie um cluster Spark no HDInsight do Azure que faz parte da saudação-to-site rede Virtual do Azure.
3. Verifique a conectividade de saudação entre o nó principal do cluster hello e sua área de trabalho.
4. Crie um aplicativo Scala no IntelliJ IDEA e configure-o para a depuração remota.
5. Executar e depurar o aplicativo hello.

## <a name="prerequisites"></a>Pré-requisitos
* Uma assinatura do Azure. Consulte [Obter avaliação gratuita do Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).
* Um cluster do Apache Spark no HDInsight. Para obter instruções, consulte o artigo sobre como [Criar clusters do Apache Spark no Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).
* Kit de desenvolvimento Oracle Java. Você pode instalá-lo clicando [aqui](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).
* IntelliJ IDEA. Este artigo usa a versão 2017.1. Você pode instalá-lo clicando [aqui](https://www.jetbrains.com/idea/download/).
* Ferramentas do HDInsight no Kit de Ferramentas do Azure para IntelliJ. Ferramentas de HDInsight para IntelliJ estão disponíveis como parte do Kit de ferramentas do Azure para IntelliJ de saudação. Para obter instruções sobre como tooinstall Olá Kit de ferramentas do Azure, consulte [Olá instalando o Kit de ferramentas do Azure para IntelliJ](../azure-toolkit-for-intellij-installation.md).
* Faça logon em sua assinatura do Azure no IntelliJ IDEA. Siga as instruções de saudação [aqui](hdinsight-apache-spark-intellij-tool-plugin.md).
* Ao executar o aplicativo Scala Spark para depuração remota em um computador Windows, você pode obter uma exceção conforme explicado em [SPARK 2356](https://issues.apache.org/jira/browse/SPARK-2356) que ocorre devido a falta de tooa WinUtils.exe no Windows. toowork alternativa para esse erro, você deve [baixar Olá executável aqui](http://public-repo-1.hortonworks.com/hdp-win-alpha/winutils.exe) tooa local como **C:\WinUtils\bin**. Em seguida, você deve adicionar uma variável de ambiente **HADOOP_HOME** e defina o valor de saudação da variável de saudação muito**C\WinUtils**.

## <a name="step-1-create-an-azure-virtual-network"></a>Etapa 1: Criar uma rede virtual do Azure
Siga as instruções de saudação do hello abaixo links toocreate uma rede Virtual do Azure e, em seguida, verifique a conectividade de saudação entre desktop saudação e rede Virtual do Azure.

* [Criar uma Rede Virtual com uma conexão VPN site a site usando o Portal do Azure](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md)
* [Criar uma Rede Virtual com uma conexão VPN site a site usando o PowerShell](../vpn-gateway/vpn-gateway-create-site-to-site-rm-powershell.md)
* [Configurar uma rede virtual do tooa conexão ponto a site usando o PowerShell](../vpn-gateway/vpn-gateway-howto-point-to-site-rm-ps.md)

## <a name="step-2-create-an-hdinsight-spark-cluster"></a>Etapa 2: Criar um cluster HDInsight Spark
Você também deve criar um cluster do Apache Spark no HDInsight do Azure que faz parte da saudação rede Virtual do Azure que você criou. Use as informações de saudação disponíveis no [baseados em Linux criar clusters de HDInsight](hdinsight-hadoop-provision-linux-clusters.md). Como parte da configuração opcional, selecione Olá rede Virtual do Azure que você criou na etapa anterior hello.

## <a name="step-3-verify-hello-connectivity-between-hello-cluster-headnode-and-your-desktop"></a>Etapa 3: Verificar a conectividade de saudação entre o nó principal do cluster hello e sua área de trabalho
1. Obter endereço IP Olá Olá um nó principal. Abra o Ambari UI cluster hello. Na folha de cluster hello, clique em **painel**.

    ![Localizar o IP do nó de cabeçalho](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/launch-ambari-ui.png)
2. De Olá Ambari UI, do canto superior direito de saudação, clique em **Hosts**.

    ![Localizar o IP do nó de cabeçalho](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/ambari-hosts.png)
3. Você deve ver uma lista de nós de cabeçalho, os nós de trabalho e os nós do zookeeper. Olá headnodes ter Olá **hn*** prefixo. Clique em um nó principal do hello primeiro.

    ![Localizar o IP do nó de cabeçalho](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/cluster-headnodes.png)
4. Final Olá Olá página aberta, de saudação **resumo** caixa de endereço IP hello cópia do nó principal do hello e nome de host de saudação.

    ![Localizar o IP do nó de cabeçalho](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/headnode-ip-address.png)
5. Incluir endereço IP de saudação e nome de host de saudação do Olá um nó principal toohello **hosts** arquivo em computador Olá onde você deseja toorun e depurar remotamente trabalhos do Spark hello. Isso permite que você toocommunicate com hello um nó principal usando endereço IP hello, bem como Olá hostname.

   1. Abra um bloco de notas com permissões elevadas. No menu de arquivo hello, clique em **abrir** e, em seguida, navegue toohello local do arquivo de hosts de saudação. Em um computador com o Windows, é `C:\Windows\System32\Drivers\etc\hosts`.
   2. Adicionar Olá após toohello **hosts** arquivo.

           # For headnode0
           192.xxx.xx.xx hn0-nitinp
           192.xxx.xx.xx hn0-nitinp.lhwwghjkpqejawpqbwcdyp3.gx.internal.cloudapp.net

           # For headnode1
           192.xxx.xx.xx hn1-nitinp
           192.xxx.xx.xx hn1-nitinp.lhwwghjkpqejawpqbwcdyp3.gx.internal.cloudapp.net
6. Em computador Olá conectado toohello rede Virtual do Azure que é usado pelo cluster do HDInsight Olá, verifique se você pode executar o ping ambos headnodes hello usando endereço IP hello, bem como Olá hostname.
7. SSH em Olá nó principal do cluster usando instruções Olá em [cluster do HDInsight tooan conectar usando o SSH](hdinsight-hadoop-linux-use-ssh-unix.md). Do nó principal do cluster hello, ping endereço IP de saudação do computador desktop saudação. Você deve testar conectividade tooboth Olá endereços atribuídos toohello computador, um para a conexão de rede de saudação e Olá para Olá rede Virtual do Azure que Olá computador está conectado.
8. Repita as etapas de Olá Olá também outros um nó principal.

## <a name="step-4-create-a-spark-scala-application-using-hello-hdinsight-tools-in-azure-toolkit-for-intellij-and-configure-it-for-remote-debugging"></a>Etapa 4: Criar um aplicativo de Scala Spark usando ferramentas do HDInsight Olá no Kit de ferramentas do Azure para IntelliJ e configurá-lo para depuração remota
1. Inicie o IntelliJ IDEA e crie um novo projeto. Na caixa de diálogo projeto novo hello, fazer Olá opções a seguir e, em seguida, clique em **próximo**.

    ![Criar um aplicativo Spark Scala](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/create-hdi-scala-app.png)

   * No painel esquerdo do hello, selecione **HDInsight**.
   * No painel direito da saudação, selecione **Spark no HDInsight (Scala)**.
   * Clique em **Avançar**.
2. Na próxima janela de hello, forneça Olá detalhes de projeto a seguir e, em seguida, clique em **concluir**.  
   - Forneça um nome de projeto e o local do projeto.
   - Para o **SDK de projeto**, use o Java 1.8 para o cluster do Spark 2.x e o Java 1.7 para o cluster do Spark 1.x.
   - Para a **versão do Spark**, o assistente de criação de projetos Scala integra a versão apropriada do SDK do Spark e do SDK do Scala. Se a versão do cluster spark Olá for inferior 2.0, escolha despertar 1. x. Caso contrário, você deve selecionar o spark2.x. Este exemplo usa o Spark 2.0.2 (Scala 2.11.8).
       ![Criar um aplicativo Spark Scala](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/hdi-scala-project-details.png)
  
3. projeto do Spark Olá criará automaticamente um artefato para você. artefato de saudação toosee, siga estas etapas.

   1. De saudação **arquivo** menu, clique em **estrutura do projeto**.
   2. Em Olá **estrutura do projeto** caixa de diálogo, clique em **artefatos** toosee artefato de padrão de saudação que é criado.
   ![Criar JAR](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/default-artifact.png)

      Você também pode criar seu próprios artefato bly clicando em Olá  **+**  ícone, realçado na imagem de saudação acima.

4. Adicione projeto de tooyour de bibliotecas. tooadd uma biblioteca, clique no nome do projeto Olá na árvore de projeto Olá e clique **abrir configurações de módulo**. Em Olá **estrutura do projeto** caixa de diálogo, no painel esquerdo do hello, clique em **bibliotecas**, clique o símbolo de saudação (+) e, em seguida, clique em **do Maven**.

    ![Adicionar biblioteca](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/add-library.png)

    Em Olá **baixar a biblioteca do repositório Maven** caixa de diálogo caixa, pesquisar e adicionar Olá bibliotecas a seguir.

   * `org.scalatest:scalatest_2.10:2.2.1`
   * `org.apache.hadoop:hadoop-azure:2.7.1`
5. Cópia `yarn-site.xml` e `core-site.xml` de saudação um nó principal do cluster e adicioná-lo toohello projeto. Use Olá seguintes comandos toocopy Olá arquivos. Você pode usar [Cygwin](https://cygwin.com/install.html) a seguir Olá toorun `scp` comandos toocopy arquivos Olá Olá headnodes de cluster.

        scp <ssh user name>@<headnode IP address or host name>://etc/hadoop/conf/core-site.xml .

    Porque estamos já adicionado Olá cluster um nó principal IP endereços e nomes de host fo Olá arquivo hosts na área de trabalho hello, podemos usar Olá **scp** comandos Olá maneira a seguir.

        scp sshuser@hn0-nitinp:/etc/hadoop/conf/core-site.xml .
        scp sshuser@hn0-nitinp:/etc/hadoop/conf/yarn-site.xml .

    Adicionar esses arquivos de projeto tooyour copiando-os em Olá **/src** pasta na árvore do projeto, por exemplo `<your project directory>\src`.
6. Saudação de atualização `core-site.xml` toomake Olá alterações a seguir.

   1. `core-site.xml`inclui a conta de armazenamento de chave toohello Olá criptografado associada Olá cluster. Em Olá `core-site.xml` que você adicionou o projeto toohello, Olá de substituir chave criptografada com a chave de armazenamento real Olá associada à conta de armazenamento padrão hello. Confira [Gerenciar as chaves de acesso de armazenamento](../storage/common/storage-create-storage-account.md#manage-your-storage-account).

           <property>
                 <name>fs.azure.account.key.hdistoragecentral.blob.core.windows.net</name>
                 <value>access-key-associated-with-the-account</value>
           </property>
   2. Remover Olá seguindo as entradas da saudação `core-site.xml`.

           <property>
                 <name>fs.azure.account.keyprovider.hdistoragecentral.blob.core.windows.net</name>
                 <value>org.apache.hadoop.fs.azure.ShellDecryptionKeyProvider</value>
           </property>

           <property>
                 <name>fs.azure.shellkeyprovider.script</name>
                 <value>/usr/lib/python2.7/dist-packages/hdinsight_common/decrypt.sh</value>
           </property>

           <property>
                 <name>net.topology.script.file.name</name>
                 <value>/etc/hadoop/conf/topology_script.py</value>
           </property>
   3. Salve o arquivo hello.
7. Adicione classe principal de saudação para seu aplicativo. De saudação **Explorador de projeto**, clique com botão direito **src**, ponto muito**novo**e, em seguida, clique em **Scala classe**.

    ![Adicionar código-fonte](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/hdi-spark-scala-code.png)
8. Em Olá **criar nova classe Scala** caixa de diálogo caixa, forneça um nome para **tipo** selecione **objeto**e, em seguida, clique em **Okey**.

    ![Adicionar código-fonte](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/hdi-spark-scala-code-object.png)
9. Em Olá `MyClusterAppMain.scala` de arquivo, cole Olá código a seguir. Esse código cria um contexto de Spark hello e inicia um `executeJob` método da saudação `SparkSample` objeto.

        import org.apache.spark.{SparkConf, SparkContext}

        object SparkSampleMain {
          def main (arg: Array[String]): Unit = {
            val conf = new SparkConf().setAppName("SparkSample")
                                      .set("spark.hadoop.validateOutputSpecs", "false")
            val sc = new SparkContext(conf)

            SparkSample.executeJob(sc,
                                   "wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv",
                                   "wasb:///HVACOut")
          }
        }

10. Repita as etapas 8 e 9 acima tooadd um novo objeto Scala chamado `SparkSample`. classe toothis adicionar Olá código a seguir. Esse código lê dados de saudação de saudação HVAC.csv (disponível em todos os clusters de HDInsight Spark), recupera linhas de saudação que têm apenas um dígito na coluna sétima Olá Olá CSV e grava a saída de hello muito**/HVACOut** em padrão Olá contêiner de armazenamento de cluster hello.

        import org.apache.spark.SparkContext

        object SparkSample {
         def executeJob (sc: SparkContext, input: String, output: String): Unit = {
           val rdd = sc.textFile(input)

           //find hello rows which have only one digit in hello 7th column in hello CSV
           val rdd1 =  rdd.filter(s => s.split(",")(6).length() == 1)

           val s = sc.parallelize(rdd.take(5)).cartesian(rdd).count()
           println(s)

           rdd1.saveAsTextFile(output)
           //rdd1.collect().foreach(println)
         }
        }
11. Repita as etapas 8 e 9 acima tooadd uma nova classe chamada `RemoteClusterDebugging`. Essa classe implementa uma estrutura de teste do Spark Olá é usada para depurar aplicativos. Adicionar Olá toohello de código a seguir `RemoteClusterDebugging` classe.

        import org.apache.spark.{SparkConf, SparkContext}
        import org.scalatest.FunSuite

        class RemoteClusterDebugging extends FunSuite {

         test("Remote run") {
           val conf = new SparkConf().setAppName("SparkSample")
                                     .setMaster("yarn-client")
                                     .set("spark.yarn.am.extraJavaOptions", "-Dhdp.version=2.4")
                                     .set("spark.yarn.jar", "wasb:///hdp/apps/2.4.2.0-258/spark-assembly-1.6.1.2.4.2.0-258-hadoop2.7.1.2.4.2.0-258.jar")
                                     .setJars(Seq("""C:\workspace\IdeaProjects\MyClusterApp\out\artifacts\MyClusterApp_DefaultArtifact\default_artifact.jar"""))
                                     .set("spark.hadoop.validateOutputSpecs", "false")
           val sc = new SparkContext(conf)

           SparkSample.executeJob(sc,
             "wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv",
             "wasb:///HVACOut")
         }
        }

     Algumas coisas importantes toonote aqui:

   * Para `.set("spark.yarn.jar", "wasb:///hdp/apps/2.4.2.0-258/spark-assembly-1.6.1.2.4.2.0-258-hadoop2.7.1.2.4.2.0-258.jar")`, certifique-se de saudação assembly Spark JAR está disponível no armazenamento de cluster Olá no caminho especificado hello.
   * Para `setJars`, especifique Olá local onde jar do artefato Olá será criado. Geralmente, é `<Your IntelliJ project directory>\out\<project name>_DefaultArtifact\default_artifact.jar`.
12. Em Olá `RemoteClusterDebugging` da classe, clique com botão direito Olá `test` palavra-chave e selecione **criar RemoteClusterDebugging configuração**.

    ![Criar configuração remota](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/create-remote-config.png)

13. Na caixa de diálogo hello, forneça um nome para a configuração de saudação e selecione Olá **teste tipo** como **nome do teste**. Deixe todos os outros valores como padrão, clique em **Aplicar** e clique em **OK**.

    ![Criar configuração remota](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/provide-config-value.png)
14. Agora você deve ver uma **remoto executar** configuração suspensa na barra de menus do hello.

    ![Criar configuração remota](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/config-run.png)

## <a name="step-5-run-hello-application-in-debug-mode"></a>Etapa 5: Executar aplicativo hello no modo de depuração
1. No seu projeto IntelliJ IDEIA, abra `SparkSample.scala` e criar um rdd1 de too'val próximo ponto de interrupção '. No menu pop-up de saudação para a criação de um ponto de interrupção, selecione **linha na função executeJob**.

    ![Adicionar um ponto de interrupção](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/create-breakpoint.png)
2. Clique em Olá **depurar executar** toohello próximo botão **remoto executar** toostart de lista suspensa de configuração executando o aplicativo hello.

    ![Execute o programa de saudação no modo de depuração](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/debug-run-mode.png)
3. Quando a execução do programa hello atinge o ponto de interrupção hello, você verá um **depurador** guia no painel inferior de saudação.

    ![Execute o programa de saudação no modo de depuração](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/debug-add-watch.png)
4. Clique em hello (**+**) ícone tooadd uma inspeção conforme mostrado na imagem de saudação abaixo.

    ![Execute o programa de saudação no modo de depuração](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/debug-add-watch-variable.png)

    Aqui, porque o aplicativo hello rompeu antes de variável Olá `rdd1` foi criado com essa inspeção podemos ver quais são Olá primeiras 5 linhas na variável de saudação `rdd`. Pressione **ENTER**.

    ![Execute o programa de saudação no modo de depuração](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/debug-add-watch-variable-value.png)

    O que você vê na imagem de saudação acima é que, em tempo de execução, você poderia consultar terabytes de dados e de depuração como seu aplicativo avança. Por exemplo, na saída de hello mostrada na imagem de saudação acima, você pode ver que Olá primeira linha da saída de hello é um cabeçalho. Com base nisso, você pode modificar a linha de cabeçalho do aplicativo código tooskip Olá se necessário.
5. Agora você pode clicar Olá **retomar programa** ícone tooproceed com seu aplicativo seja executado.

    ![Execute o programa de saudação no modo de depuração](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/debug-continue-run.png)
6. Se o aplicativo hello for concluído com êxito, você verá uma saída semelhante Olá seguinte.

    ![Execute o programa de saudação no modo de depuração](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/debug-complete.png)

## <a name="seealso"></a>Consulte também
* [Visão geral: Apache Spark no Azure HDInsight](hdinsight-apache-spark-overview.md)

### <a name="demo"></a>Demonstração
* Criar projeto do Scala (vídeo): [Criar aplicativos Spark Scala](https://channel9.msdn.com/Series/AzureDataLake/Create-Spark-Applications-with-the-Azure-Toolkit-for-IntelliJ)
* Depuração remota (vídeo): [Kit de ferramentas do uso do Azure para aplicativos de Spark toodebug IntelliJ remotamente no HDInsight Cluster](https://channel9.msdn.com/Series/AzureDataLake/Debug-HDInsight-Spark-Applications-with-Azure-Toolkit-for-IntelliJ)

### <a name="scenarios"></a>Cenários
* [Spark com BI: executar análise de dados interativa usando o Spark no HDInsight com ferramentas de BI](hdinsight-apache-spark-use-bi-tools.md)
* [Spark com Aprendizado de Máquina: usar o Spark no HDInsight para analisar a temperatura de prédios usando dados do sistema HVAC](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [Spark com o aprendizado de máquina: Use Spark nos resultados de inspeção de alimentos HDInsight toopredict](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [Streaming Spark: usar o Spark no HDInsight para a criação de aplicativos de streaming em tempo real](hdinsight-apache-spark-eventhub-streaming.md)
* [Análise de log do site usando o Spark no HDInsight](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a>Criar e executar aplicativos
* [Criar um aplicativo autônomo usando Scala](hdinsight-apache-spark-create-standalone-application.md)
* [Executar trabalhos remotamente em um cluster do Spark usando Livy](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a>Ferramentas e extensões
* [Usar as ferramentas do HDInsight no Kit de ferramentas do Azure para IntelliJ toocreate e enviar maiores Spark Scala aplicativos](hdinsight-apache-spark-intellij-tool-plugin.md)
* [Use o Kit de ferramentas do Azure para aplicativos de Spark toodebug IntelliJ remotamente por meio do SSH](hdinsight-apache-spark-intellij-tool-debug-remotely-through-ssh.md)
* [Usar ferramentas do HDInsight para IntelliJ com a área restrita do Hortonworks](hdinsight-tools-for-intellij-with-hortonworks-sandbox.md)
* [Use as ferramentas do HDInsight no Kit de ferramentas do Azure para aplicativos do Eclipse toocreate Spark](hdinsight-apache-spark-eclipse-tool-plugin.md)
* [Usar blocos de anotações do Zeppelin com um cluster Spark no HDInsight](hdinsight-apache-spark-zeppelin-notebook.md)
* [Kernels disponíveis para o bloco de anotações Jupyter no cluster do Spark para HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [Usar pacotes externos com blocos de notas Jupyter](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [Instalar Jupyter em seu computador e conecte-se tooan cluster HDInsight Spark](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a>Gerenciar recursos
* [Gerenciar os recursos de cluster do hello Apache Spark no HDInsight do Azure](hdinsight-apache-spark-resource-manager.md)
* [Rastrear e depurar trabalhos em execução em um cluster do Apache Spark no HDInsight](hdinsight-apache-spark-job-debugging.md)
