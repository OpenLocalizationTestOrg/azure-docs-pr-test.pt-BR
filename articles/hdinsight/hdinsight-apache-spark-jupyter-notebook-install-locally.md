---
title: aaaInstall Jupyter localmente & conectar-se o cluster do Spark no HDInsight tooan | Microsoft Docs
description: "Saiba como anotações do Jupyter tooinstall localmente no seu computador e conecte-o cluster do tooan Apache Spark no HDInsight do Azure."
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 48593bdf-4122-4f2e-a8ec-fdc009e47c16
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: 95c052110b84b677fd23048597af9511365cacfc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="install-jupyter-notebook-on-your-computer-and-connect-tooapache-spark-on-hdinsight"></a>Instalar o bloco de anotações do Jupyter em seu computador e conecte-se tooApache Spark no HDInsight

Neste artigo, você aprenderá como anotações do Jupyter tooinstall, com hello PySpark personalizado (para Python) e kernels Spark (para Scala) com despertar magic e conecte-se o cluster do HDInsight Olá notebook tooan. Pode haver um número de motivos tooinstall Jupyter no computador local, e pode haver alguns desafios também. Para obter mais informações sobre isso, consulte a seção de saudação [por que devo instalar Jupyter no meu computador](#why-should-i-install-jupyter-on-my-computer) final Olá deste artigo.

Há três etapas principais envolvidas na instalação Jupyter e hello magic Spark no seu computador.

* Instalar bloco de notas Jupyter
* Instalar hello PySpark e kernels Spark com hello magic Spark
* Configurar Spark magic tooaccess cluster Spark no HDInsight

Para obter mais informações sobre kernels personalizado hello e mágico de Spark Olá disponível para blocos de anotações do Jupyter com o cluster HDInsight, consulte [clusters Kernels disponíveis para blocos de anotações do Jupyter com Linux do Apache Spark no HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md).

## <a name="prerequisites"></a>Pré-requisitos
pré-requisitos de saudação listados aqui não são para a instalação do Jupyter. Esses são para cluster de HDInsight do conexão Olá Jupyter notebook tooan quando notebook hello está instalado.

* Uma assinatura do Azure. Consulte [Obter avaliação gratuita do Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).
* Um cluster do Apache Spark no HDInsight. Para obter instruções, consulte o artigo sobre como [Criar clusters do Apache Spark no Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).

## <a name="install-jupyter-notebook-on-your-computer"></a>Instalar bloco de notas Jupyter em seu computador

Você deve instalar o Python antes de instalar notebooks do Jupyter. Python e Jupyter estão disponíveis como parte da saudação [distribuição Anaconda](https://www.continuum.io/downloads). Quando instala o Anaconda, você instala uma distribuição do Python. Quando Anaconda estiver instalado, você adiciona instalação de Jupyter Olá executando comandos apropriados.

1. Baixar Olá [instalador Anaconda](https://www.continuum.io/downloads) para sua plataforma e a configuração de execução hello. Ao Assistente de instalação de saudação em execução, verifique se que você selecionar a variável de caminho Olá opção tooadd Anaconda tooyour.
2. Execute Olá comando tooinstall Jupyter a seguir.

        conda install jupyter

    Para obter mais informações sobre a instalação do Jupyter, confira [Installing Jupyter using Anaconda](http://jupyter.readthedocs.io/en/latest/install.html)(Instalando o Jupyter usando o Anaconda).

## <a name="install-hello-kernels-and-spark-magic"></a>Instalar kernels hello e magic Spark

Para obter instruções sobre como mágica do tooinstall Olá Spark, Olá PySpark e kernels Spark, siga instruções de instalação de saudação em Olá [sparkmagic documentação](https://github.com/jupyter-incubator/sparkmagic#installation) no GitHub. Olá primeira etapa na documentação do hello Spark magic solicitará que você tooinstall mágico de Spark. Substitua essa primeira etapa no link Olá Olá comandos, dependendo da versão de saudação do cluster do HDInsight Olá que você se conectará a seguir. Depois disso, siga Olá restantes etapas descritas na documentação mágica do hello Spark. Se você quiser kernels diferentes do tooinstall Olá, você deve executar a etapa 3 no hello seção de instruções de instalação magic Spark.

* Para clusters v3.4, instale sparkmagic 0.2.3 executando `pip install sparkmagic==0.2.3`

* Para clusters v3.5 e v3.6, instale sparkmagic 0.11.2 executando `pip install sparkmagic==0.11.2`

## <a name="configure-spark-magic-tooconnect-toohdinsight-spark-cluster"></a>Configurar o cluster do Spark tooconnect magic tooHDInsight Spark

Nesta seção você configurar mágico do Spark Olá que você instalou o cluster do Apache Spark de tooan tooconnect anterior você já deve ter criado no Azure HDInsight.

1. Olá Jupyter informações de configuração é normalmente armazenado no diretório base de usuários de saudação. toolocate comandos de seu diretório base em qualquer plataforma de sistema operacional, Olá tipo a seguir.

    Inicie o shell de Python hello. Em uma janela de comando, digite o seguinte hello:

        python

    Na Olá shell Python, digite Olá toofind comando diretório base Olá a seguir.

        import os
        print(os.path.expanduser('~'))

2. Navegue diretório base toohello e crie uma pasta chamada **.sparkmagic** se ele ainda não existir.
3. Na pasta hello, crie um arquivo chamado **config. JSON** e adicione Olá seguindo o trecho JSON dentro dele.

        {
          "kernel_python_credentials" : {
            "username": "{USERNAME}",
            "base64_password": "{BASE64ENCODEDPASSWORD}",
            "url": "https://{CLUSTERDNSNAME}.azurehdinsight.net/livy"
          },
          "kernel_scala_credentials" : {
            "username": "{USERNAME}",
            "base64_password": "{BASE64ENCODEDPASSWORD}",
            "url": "https://{CLUSTERDNSNAME}.azurehdinsight.net/livy"
          }
        }

4. Substitua **{USERNAME}**, **{CLUSTERDNSNAME}** e **{BASE64ENCODEDPASSWORD}** pelos valores apropriados. Você pode usar um número de utilitários em sua linguagem de programação favorita ou senha codificada em base64 de toogenerate online para sua senha real.

5. Definir configurações de pulsação direita Olá no `config.json`. Você deve adicionar essas configurações em Olá mesmo nível como Olá `kernel_python_credentials` e `kernel_scala_credentials` trechos seu adicionado anteriormente. Para obter um exemplo sobre como e onde tooadd Olá configurações de pulsação, consulte [config. JSON de exemplo](https://github.com/jupyter-incubator/sparkmagic/blob/master/sparkmagic/example_config.json).

    * Para `sparkmagic 0.2.3` (clusters v3.4), incluem:

            "should_heartbeat": true,
            "heartbeat_refresh_seconds": 5,
            "heartbeat_retry_seconds": 1

    * Para `sparkmagic 0.11.2` (clusters v3.5 e v3.6), inclua:

            "heartbeat_refresh_seconds": 5,
            "livy_server_heartbeat_timeout_seconds": 60,
            "heartbeat_retry_seconds": 1

    >[!TIP]
    >As pulsações são enviadas tooensure que não vazam sessões. Quando um computador fica toosleep ou está desligado, pulsação Olá não for enviada, resultando em Olá sessão sendo limpo. Para clusters v3.4, se desejar toodisable esse comportamento, você pode definir Olá Livy config `livy.server.interactive.heartbeat.timeout` muito`0` de saudação Ambari UI. Para v 3.5 de clusters, se você não definir a configuração de saudação 3.5 acima, sessão de saudação não será excluído.

6. Inicie o Jupyter. Use Olá comando a seguir no prompt de comando hello.

        jupyter notebook

7. Verifique se você pode se conectar a cluster toohello usando anotações do Jupyter hello e que você pode usar mágico de Spark Olá disponível com kernels hello. Execute Olá etapas a seguir.

    a. Crie um novo bloco de anotações. No canto superior direito da saudação, clique em **novo**. Você deve ver o kernel do padrão de saudação **Python2** e Olá dois kernels nova instalação, **PySpark** e **Spark**. Clique em **PySpark**.

    ![Kernels no bloco de anotações do Jupyter](./media/hdinsight-apache-spark-jupyter-notebook-install-locally/jupyter-kernels.png "Kernels no bloco de anotações do Jupyter")

    b. Execute Olá trecho de código a seguir.

        %%sql
        SELECT * FROM hivesampletable LIMIT 5

    Se você pode recuperar com êxito saída hello, seu cluster de HDInsight toohello conexão é testada.

    >[!TIP]
    >Se você quiser tooupdate Olá notebook configuração tooconnect tooa cluster diferente, atualize Olá config. JSON com o novo conjunto de saudação de valores, conforme mostrado na etapa 3 acima.

## <a name="why-should-i-install-jupyter-on-my-computer"></a>Por que devo instalar o Jupyter no meu computador?
Pode haver um número de motivos pelos quais você pode desejar tooinstall Jupyter em seu computador e, em seguida, conecte-se de cluster tooa Spark no HDInsight.

* Embora os blocos de anotações do Jupyter já estão disponíveis no cluster do hello Spark no HDInsight do Azure, instalando Jupyter no seu computador fornece Olá opção toocreate seus blocos de anotações localmente, testar o aplicativo em um cluster em execução e, em seguida, carregar Olá cluster de toohello blocos de anotações. cluster de toohello blocos de anotações do hello tooupload, você pode carregá-los usando anotações do Jupyter Olá que está em execução ou saudação do cluster ou salvá-las toohello /HdiNotebooks pasta na conta de armazenamento Olá associada Olá cluster. Para obter mais informações sobre como os blocos de anotações são armazenados no cluster hello, consulte [blocos de anotações do Jupyter armazenamento](hdinsight-apache-spark-jupyter-notebook-kernels.md#where-are-the-notebooks-stored)?
* Com blocos de anotações Olá disponíveis localmente, você pode conectar clusters do Spark toodifferent com base em suas necessidades de aplicativo.
* Você pode usar GitHub tooimplement um sistema de controle de origem e ter controle de versão para notebooks hello. Você também pode ter um ambiente de colaboração em que vários usuários podem trabalhar com hello mesmo bloco de anotações.
* Você pode trabalhar com blocos de notas localmente sem sequer ter um cluster em operação. Você só precisa de um cluster tootest seus blocos de anotações em, não toomanually gerenciar seus blocos de anotações ou em um ambiente de desenvolvimento.
* Ele pode ser mais fácil tooconfigure seu próprio ambiente de desenvolvimento local que a instalação de Jupyter tooconfigure Olá no cluster hello.  Você pode tirar proveito de todos os softwares de saudação instalado localmente sem configurar um ou mais clusters remotos.

> [!WARNING]
> Com Jupyter instalado no computador local, vários usuários podem executar Olá mesmo bloco de anotações Olá Spark mesmo cluster em Olá simultaneamente. Nessa situação, várias sessões Livy são criadas. Se você tiver um problema e deseja toodebug que, ele será um tootrack tarefa complexa que sessão Livy pertence toowhich usuário.
>
>

## <a name="seealso"></a>Consulte também
* [Visão geral: Apache Spark no Azure HDInsight](hdinsight-apache-spark-overview.md)

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
* [Usar o plug-in de ferramentas de HDInsight para toocreate IntelliJ IDEIA e enviar Spark Scala aplicativos](hdinsight-apache-spark-intellij-tool-plugin.md)
* [Usar o plug-in de ferramentas de HDInsight para aplicativos de Spark toodebug IntelliJ IDEIA remotamente](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [Usar blocos de anotações do Zeppelin com um cluster Spark no HDInsight](hdinsight-apache-spark-zeppelin-notebook.md)
* [Kernels disponíveis para o bloco de anotações Jupyter no cluster do Spark para HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [Usar pacotes externos com blocos de notas Jupyter](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)

### <a name="manage-resources"></a>Gerenciar recursos
* [Gerenciar os recursos de cluster do hello Apache Spark no HDInsight do Azure](hdinsight-apache-spark-resource-manager.md)
* [Rastrear e depurar trabalhos em execução em um cluster do Apache Spark no HDInsight](hdinsight-apache-spark-job-debugging.md)
