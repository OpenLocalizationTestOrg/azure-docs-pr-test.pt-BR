---
title: clusters de Hadoop aaaCreate usando um navegador da web - HDInsight do Azure | Microsoft Docs
description: "Saiba como toocreate Hadoop, HBase, tempestade ou Spark clusters no Linux para HDInsight usando um navegador da web e Olá portal de visualização do Azure."
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 697278cf-0032-4f7c-b9b2-a84c4347659e
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: 63027e35e2d66dd76218aff3e0c085fc811736ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-linux-based-clusters-in-hdinsight-using-hello-azure-portal"></a>Criar clusters baseados em Linux em HDInsight usando Olá portal do Azure
[!INCLUDE [selector](../../includes/hdinsight-create-linux-cluster-selector.md)]

Olá portal do Azure é uma ferramenta de gerenciamento baseado na web para serviços e recursos hospedados na nuvem do Microsoft Azure hello. Neste artigo, você aprenderá como toocreate HDInsight baseados em Linux clusters usando o portal de saudação.

## <a name="prerequisites"></a>Pré-requisitos
[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

* **Uma assinatura do Azure**. Consulte [Obter avaliação gratuita do Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).
* **Um navegador da Web**. Olá portal do Azure usa HTML5 e Javascript e pode não funcionar corretamente em navegadores da web mais antigos.

## <a name="create-clusters"></a>Criar clusters
Olá portal do Azure expõe a maioria das propriedades de cluster hello. Usando um modelo do Azure Resource Manager, é possível ocultar muitos detalhes. Para obter mais informações, veja [Criar clusters Hadoop baseados em Linux no HDInsight usando modelos do Azure Resource Manager](hdinsight-hadoop-create-linux-clusters-arm-templates.md).

[!INCLUDE [secure-transfer-enabled-storage-account](../../includes/hdinsight-secure-transfer.md)]


1. Entrar toohello [portal do Azure](https://portal.azure.com).
2. Clique em **+**, em **Inteligência + Análise** e clique em **HDInsight**.
   
    ![Criar um novo cluster no portal do Azure de saudação](./media/hdinsight-hadoop-create-linux-cluster-portal/hdinsight-create-cluster.png "criar um novo cluster no hello portal do Azure")

3. Em Olá **HDInsight** folha, clique em **personalizado (tamanho, configurações, aplicativos)**, clique em **Noções básicas de**e, em seguida, digite Olá informações a seguir.

    ![Criar um novo cluster no portal do Azure de saudação](./media/hdinsight-hadoop-create-linux-cluster-portal/hdinsight-create-cluster-basics.png "criar um novo cluster no hello portal do Azure")

    * Insira o **Nome do Cluster**: esse nome deve ser globalmente exclusivo.

    * De saudação **assinatura** Olá lista suspensa, selecione uma assinatura do Azure que será usada para o cluster de saudação.

    * Clique em **Tipo de cluster** e, em seguida, selecione:
   
        * **Tipo de cluster**: se você não souber quais toochoose, selecione **Hadoop**. É do tipo de cluster mais popular hello.
     
            > [!IMPORTANT]
            > HDInsight clusters entram em uma variedade de tipos, que correspondem a carga de trabalho toohello ou tecnologia que Olá cluster é ajustada para. Não há nenhum método com suporte toocreate um cluster que combina vários tipos, como Storm e HBase em um cluster. 
            > 
            > 
        
        * **Sistema Operacional**: selecione **Linux**.
        
        * **Versão**: usar a versão padrão de saudação se você não souber quais toochoose. Para obter mais informações, consulte [Versões de cluster do HDInsight](hdinsight-component-versioning.md).
        * **Nível de cluster**: HDInsight do Azure fornece ofertas de nuvem Olá grandes dados em duas categorias: camadas Standard e Premium. Para obter mais informações, consulte [Camadas de cluster](hdinsight-hadoop-provision-linux-clusters.md#cluster-tiers).

    * Para **nome de usuário de logon de Cluster** e **senha de logon de Cluster**, fornecer Olá nome de usuário e senha de usuário de administrador hello.

    * Insira um **nome de usuário SSH** e se desejar que a senha SSH Olá toohave igual Olá senha de administrador que você especificou anteriormente, selecione Olá **usar a mesma senha de logon de cluster** caixa de seleção. Se não, fornecer um **senha** ou **chave pública**, que será o usuário SSH Olá tooauthenticate usado. Usar uma chave pública é hello abordagem recomendada. Clique em **selecione** em configuração de credenciais de Olá Olá inferior toosave.
   
        Para obter informações, consulte [Usar SSH com HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

    * Para **grupo de recursos**, especifique se deseja toocreate um novo grupo de recursos ou use uma existente.

    * Especifique um centro de dados **local** onde Olá cluster será criado.

    * Clique em **Avançar**.

4. Em Olá **armazenamento** folha, especifique se deseja o armazenamento do Azure (WASB) ou repositório Data Lake como o armazenamento padrão. Examinar a tabela de saudação abaixo para obter mais informações.

    ![Criar um novo cluster no portal do Azure de saudação](./media/hdinsight-hadoop-create-linux-cluster-portal/hdinsight-create-cluster-storage.png "criar um novo cluster no hello portal do Azure")

    | Armazenamento                                      | Descrição |
    |----------------------------------------------|-------------|
    | **Blobs de armazenamento do Azure como armazenamento padrão**   | <ul><li>Para o **tipo de armazenamento primário**, selecione **Armazenamento do Azure**. Depois disso, para **método de seleção**, você pode escolher **Minhas assinaturas** se você quiser toospecify uma conta de armazenamento que faz parte de sua assinatura do Azure e a conta de armazenamento, em seguida, selecione hello. Caso contrário, clique em **chave de acesso** e fornecer informações de Olá Olá conta de armazenamento que você deseja toochoose de fora da sua assinatura do Azure.</li><li>Para **contêiner padrão**, você pode escolher toogo com o nome do contêiner padrão Olá sugerida pelo portal de saudação ou especificar sua própria.</li><li>Se você estiver usando WASB como armazenamento padrão, você pode clicar em (opcionalmente) **contas de armazenamento adicionais** contas de armazenamento adicional toospecify tooassociate com cluster hello. Em Olá **as chaves de armazenamento do Azure** folha, clique em **adicionar uma chave de armazenamento**, e, em seguida, você pode fornecer uma conta de armazenamento de suas assinaturas do Azure ou de outras assinaturas (fornecendo conta de armazenamento Olá chave de acesso).</li><li>Se você estiver usando WASB como armazenamento padrão, você pode clicar em (opcionalmente) **acesso de repositório Data Lake** toospecify repositório Azure Data Lake como armazenamento adicional. Para obter mais informações, consulte [Criar um cluster HDInsight com o Data Lake Store usando o Portal do Azure](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</li></ul> |
    | **Azure Data Lake Store como armazenamento padrão** | Para **tipo de armazenamento primário**, selecione **repositório Data Lake** e, em seguida, consulte o artigo toohello [criar um cluster HDInsight com repositório Data Lake usando o Portal do Azure](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md) para instruções. |
    | **Metastores externas**                      | Opcionalmente, você pode especificar um SQL database toosave Hive e Oozie metadados associados com cluster hello. Para **selecionar um banco de dados SQL para o Hive** selecionar um banco de dados SQL e forneça Olá nome de usuário e senha para o banco de dados de saudação. Repita essas etapas para metadados do Oozie.<br><br>Há algumas considerações ao usar o Banco de Dados SQL do Azure para metastores. <ul><li>banco de dados do SQL Azure Olá usado para metastore Olá deve permitir a conectividade tooother serviços do Azure, incluindo o Azure HDInsight. No painel de banco de dados do SQL Azure hello, direita Olá, clique no nome do servidor de saudação. Este é o servidor de saudação no qual Olá SQL instância de banco de dados está em execução. Quando estiver no modo de servidor de saudação, clique em **configurar**e, em seguida, para **serviços do Azure**, clique em **Sim**e, em seguida, clique em **salvar**.</li><li>Ao criar um metastore, não use um nome de banco de dados que contenha traços ou hifens, pois isso pode causar Olá toofail de processo de criação de cluster.</li></ul>                                                                                                                                                                       |

    Clique em **Avançar**. 

    > [!WARNING]
    > Não há suporte para usando uma conta de armazenamento adicional no cluster do HDInsight Olá um local diferente.

5. Opcionalmente, clique em **aplicativos** tooinstall aplicativos que funcionam com clusters HDInsight. Esses aplicativos podem ser desenvolvidos pela Microsoft, por ISVs (fornecedores independentes de software) ou por conta própria. Para saber mais, veja [HDInsight instalar aplicativos](hdinsight-apps-install-applications.md#install-applications-during-cluster-creation).


6. Clique em **tamanho do Cluster** toodisplay informações sobre nós Olá que será criado para esse cluster. Definir o número de saudação de nós de trabalho que você precisa para cluster hello. Olá estimativa de custo de cluster Olá será mostrado na folha de saudação.
   
    ![Nó folha de camadas de preços](./media/hdinsight-hadoop-create-linux-cluster-portal/hdinsight-create-cluster-nodes.png "especificar o número de nós de cluster")
   
   > [!IMPORTANT]
   > Se você planeja mais de 32 nós de trabalho, ou na criação do cluster, dimensionando cluster Olá após a criação, você deve selecionar um tamanho de nó principal com pelo menos 8 núcleos e 14GB ram.
   > 
   > Para saber mais sobre tamanhos de nós e custos associados, consulte [Preços do HDInsight](https://azure.microsoft.com/pricing/details/hdinsight/).
   > 
   > 
   
   Clique em **próximo** toosave nó de saudação preços de configuração.

7. Clique em **configurações avançadas** tooconfigure outras configurações opcionais, como o uso de **ações de Script** toocustomize tooinstall um cluster componentes personalizados ou ingressar em um **deredeVirtual**. Examinar a tabela de saudação abaixo para obter mais informações.

    ![Nó folha de camadas de preços](./media/hdinsight-hadoop-create-linux-cluster-portal/hdinsight-create-cluster-advanced.png "especificar o número de nós de cluster")

    | Opção | Descrição |
    |--------|-------------|
    | **Ações de Script** | Use esta opção se você quiser toouse toocustomize um script personalizado um cluster, como cluster hello está sendo criado. Para obter mais informações sobre ações de script, consulte [Personalizar clusters HDInsight usando a Ação de Script](hdinsight-hadoop-customize-cluster-linux.md). |
    | **Rede Virtual** | Se você quiser que o cluster de saudação tooplace em uma rede virtual, selecione uma sub-rede de rede e hello virtual do Azure. Para obter informações sobre como usar o HDInsight com uma rede Virtual, incluindo requisitos de configuração específicos para Olá rede Virtual, consulte [HDInsight estender recursos usando uma rede Virtual do Azure](hdinsight-extend-hadoop-virtual-network.md). |

    Clique em **Avançar**.

8. Em Olá **resumo** folha, verifique as informações de saudação inserido anteriormente e, em seguida, clique em **criar**.

    ![Nó folha de camadas de preços](./media/hdinsight-hadoop-create-linux-cluster-portal/hdinsight-create-cluster-summary.png "especificar o número de nós de cluster")
    
    > [!NOTE]
    > Levará algum tempo para Olá cluster toobe criado, normalmente em torno de 15 minutos. Use o bloco Olá Olá quadro inicial ou Olá **notificações** entrada hello à esquerda do hello página toocheck no processo de provisionamento de saudação.
    > 
    > 
12. Após a conclusão do processo de criação de saudação, clique em lado a lado para cluster de saudação da folha de cluster Olá quadro inicial toolaunch Olá Olá. folha de cluster Olá fornece Olá informações a seguir.
    
    ![Folha de cluster](./media/hdinsight-hadoop-create-linux-cluster-portal/hdinsight-create-cluster-completed.png "propriedades do Cluster")
    
    Use Olá toounderstand Olá ícones na parte superior da saudação desta folha a seguir.
    
    * **Visão geral** guia fornece informações essenciais de todos os Olá sobre cluster hello como o nome de Olá, grupo de recursos de saudação ele pertence ao local de hello, sistema de operacional hello, URL para o painel do cluster hello, etc.
    * **Painel** direciona toohello Ambari portal associado Olá cluster.
    * **Secure Shell**: informações necessárias de cluster de saudação tooaccess usando o SSH.
    * **Cluster de escala** permite que você aumenta o número de saudação de nós de trabalho associada Olá cluster.
    * **Excluir**: cluster de HDInsight Olá exclusões.
    

## <a name="customize-clusters"></a>Personalizar clusters
* Consulte [Personalizar clusters do HDInsight usando a Inicialização](hdinsight-hadoop-customize-cluster-bootstrap.md).
* Consulte [Personalizar os clusters HDInsight usando a Ação de Script](hdinsight-hadoop-customize-cluster-linux.md).

## <a name="delete-hello-cluster"></a>Excluir o cluster Olá
[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="troubleshoot"></a>Solucionar problemas

Se você tiver problemas com a criação de clusters HDInsight, confira os [requisitos de controle de acesso](hdinsight-administer-use-portal-linux.md#create-clusters).

## <a name="next-steps"></a>Próximas etapas
Agora que você criou com êxito um cluster HDInsight, usar Olá toolearn a seguir como toowork com o cluster:

### <a name="hadoop-clusters"></a>Clusters do Hadoop
* [Usar o Hive com o HDInsight](hdinsight-use-hive.md)
* [Usar o Pig com o HDInsight](hdinsight-use-pig.md)
* [Usar o MapReduce com o HDInsight](hdinsight-use-mapreduce.md)

### <a name="hbase-clusters"></a>Clusters do HBase
* [Introdução ao HBase no HDInsight](hdinsight-hbase-tutorial-get-started-linux.md)
* [Desenvolvimento de aplicativos Java para HBase no HDInsight](hdinsight-hbase-build-java-maven-linux.md)

### <a name="storm-clusters"></a>Clusters Storm
* [Desenvolver topologias Java para Storm no HDInsight](hdinsight-storm-develop-java-topology.md)
* [Usar componentes de Python no Storm no HDInsight](hdinsight-storm-develop-python-topology.md)
* [Implantar e monitorar topologias com o Storm no HDInsight](hdinsight-storm-deploy-monitor-topology-linux.md)

### <a name="spark-clusters"></a>Clusters do Spark
* [Criar um aplicativo autônomo usando Scala](hdinsight-apache-spark-create-standalone-application.md)
* [Executar trabalhos remotamente em um cluster do Spark usando Livy](hdinsight-apache-spark-livy-rest-interface.md)
* [Spark com BI: executar análise de dados interativa usando o Spark no HDInsight com ferramentas de BI](hdinsight-apache-spark-use-bi-tools.md)
* [Spark com o aprendizado de máquina: Use Spark nos resultados de inspeção de alimentos HDInsight toopredict](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [Streaming Spark: usar o Spark no HDInsight para a criação de aplicativos de streaming em tempo real](hdinsight-apache-spark-eventhub-streaming.md)

