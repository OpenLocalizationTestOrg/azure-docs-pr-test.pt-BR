---
title: "Olá aaaUse toocreate portal do Azure HDInsight do Azure clusters com repositório Data Lake | Microsoft Docs"
description: "Usar Olá toocreate portal do Azure e usar clusters de HDInsight com repositório Azure Data Lake"
services: data-lake-store,hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: a8c45a83-a8e3-4227-8b02-1bc1e1de6767
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/14/2017
ms.author: nitinme
ms.openlocfilehash: f23113d444a3c5a01894dba29f75f3621b2d16bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-hdinsight-clusters-with-data-lake-store-by-using-hello-azure-portal"></a>Criar clusters de HDInsight com repositório Data Lake usando Olá portal do Azure
> [!div class="op_single_selector"]
> * [Use Olá portal do Azure](data-lake-store-hdinsight-hadoop-use-portal.md)
> * [Usar o PowerShell (para armazenamento padrão)](data-lake-store-hdinsight-hadoop-use-powershell-for-default-storage.md)
> * [Usar o PowerShell (para armazenamento adicional)](data-lake-store-hdinsight-hadoop-use-powershell.md)
> * [Usar o Resource Manager](data-lake-store-hdinsight-hadoop-use-resource-manager-template.md)
>
>

Saiba como toouse Olá toocreate portal do Azure um cluster HDInsight com uma conta do repositório Azure Data Lake como um armazenamento adicional ou de armazenamento padrão da saudação. Embora o armazenamento adicional é opcional para um cluster HDInsight, é recomendável toostore seus dados comerciais em hello mais contas de armazenamento.

## <a name="prerequisites"></a>Pré-requisitos
Antes de começar este tutorial, certifique-se de que você cumpriu Olá requisitos a seguir:

* **Uma assinatura do Azure**. Vá muito[avaliação gratuita do Azure obter](https://azure.microsoft.com/pricing/free-trial/).
* **Uma conta do repositório Azure Data Lake**. Siga as instruções de saudação do [Introdução ao repositório Azure Data Lake usando o portal do Azure de saudação](data-lake-store-get-started-portal.md). Você também deve criar uma pasta raiz na conta de saudação.  Neste tutorial, uma pasta raiz chamada __/clusters__ é usada.
* **Uma entidade de serviço do Azure Active Directory**. Este tutorial fornece instruções sobre como toocreate uma entidade de serviço no Azure Active Directory (AD do Azure). No entanto, toocreate uma entidade de serviço, você deve ser um administrador do AD do Azure. Se você for um administrador, você pode ignorar esse pré-requisito e continuar com o tutorial hello.

    >[!NOTE]
    >Você poderá criar uma entidade de serviço somente se for um administrador do Azure AD. O administrador do Azure AD deverá criar uma entidade de serviço antes que você possa criar um cluster HDInsight com o Data Lake Store. Além disso, entidade de serviço Olá deve ser criada com um certificado, conforme descrito em [criar uma entidade de serviço com certificado](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-self-signed-certificate).
    >

## <a name="create-an-hdinsight-cluster"></a>Crie um cluster HDInsight

Nesta seção, você pode criar um cluster HDInsight com contas do repositório Data Lake como padrão de saudação ou armazenamento adicional da saudação. Este artigo se concentra somente a parte de saudação da configuração de contas do repositório Data Lake.  Para informações de criação de cluster geral hello e procedimentos, consulte [Hadoop criar clusters de HDInsight](../hdinsight/hdinsight-hadoop-provision-linux-clusters.md).

### <a name="create-a-cluster-with-data-lake-store-as-default-storage"></a>Criar um cluster com o Data Lake Store como armazenamento padrão

**toocreate um HDInsight cluster com um repositório Data Lake como conta de armazenamento saudação padrão**

1. Entrar toohello [portal do Azure](https://portal.azure.com).
2. Execute [criar clusters](../hdinsight/hdinsight-hadoop-create-linux-clusters-portal.md#create-clusters) para obter informações gerais sobre a criação de clusters HDInsight hello.
3. Em Olá **armazenamento** folha, em **tipo de armazenamento primário**, selecione **repositório Data Lake**e, em seguida, digite Olá informações a seguir:

    ![Cluster de tooHDInsight principal de serviço Add](./media/data-lake-store-hdinsight-hadoop-use-portal/hdi.adl.1.adls.storage.png "adicionar cluster de tooHDInsight principal de serviço")

    - **Selecionar conta do Data Lake Store**: selecione uma conta existente do Data Lake Store. Uma conta existente do Data Lake Store é necessária.  Consulte [Pré-requisitos](#prereuisites).
    - **Caminho raiz**: insira um caminho onde os arquivos de cluster específicos de saudação estão toobe armazenado. Na captura de tela hello, é __/clusters myhdiadlcluster/__, no qual Olá __/clusters__ pasta deve existir e hello Portal cria *myhdicluster* pasta.  Olá *myhdicluster* é o nome do cluster hello.
    - **Acesso de repositório data Lake**: configurar o acesso entre a conta do repositório Data Lake hello e o cluster HDInsight. Para obter instruções, consulte [Configurar acesso ao Data Lake Store](#configure-data-lake-store-access).
    - **Contas de armazenamento adicionais**: contas de adicionar contas de armazenamento do Azure como armazenamento adicional para o cluster hello. tooadd adicionais Data Lake armazenamentos é feito dando permissões de cluster Olá nos dados mais contas do repositório Data Lake ao configurar uma conta do repositório Data Lake como tipo de armazenamento primário hello. Consulte [Configurar acesso ao Data Lake Store](#configure-data-lake-store-access).

4. Em Olá **acesso de repositório Data Lake**, clique em **selecione**e, em seguida, continue com a criação do cluster, conforme descrito em [Hadoop criar clusters de HDInsight](../hdinsight/hdinsight-hadoop-create-linux-clusters-portal.md).


### <a name="create-a-cluster-with-data-lake-store-as-additional-storage"></a>Criar um cluster com o Data Lake Store como armazenamento adicional

Olá instruções a seguir cria um cluster HDInsight com uma conta de armazenamento do Azure como armazenamento de padrão de saudação e uma conta de repositório Data Lake como um armazenamento adicional.
**toocreate um HDInsight cluster com um repositório Data Lake como conta de armazenamento saudação padrão**

1. Entrar toohello [portal do Azure](https://portal.azure.com).
2. Execute [criar clusters](../hdinsight/hdinsight-hadoop-create-linux-clusters-portal.md#create-clusters) para obter informações gerais sobre a criação de clusters HDInsight hello.
3. Em Olá **armazenamento** folha, em **tipo de armazenamento primário**, selecione **armazenamento do Azure**e, em seguida, digite Olá informações a seguir:

    ![Cluster de tooHDInsight principal de serviço Add](./media/data-lake-store-hdinsight-hadoop-use-portal/hdi.adl.1.png "adicionar cluster de tooHDInsight principal de serviço")

    - **Método de seleção**: use uma saudação as opções a seguir:

        * toospecify uma conta de armazenamento que faz parte de sua assinatura do Azure, selecione **Minhas assinaturas**e, em seguida, selecione conta de armazenamento hello.
        * toospecify uma conta de armazenamento que está fora de sua assinatura do Azure, selecione **chave de acesso**e, em seguida, fornecer informações Olá Olá fora da conta de armazenamento.

    - **Contêiner padrão**: Usar valor saudação padrão ou especificar seu próprio nome.

    - Contas de armazenamento adicionais: adicionar mais contas de armazenamento do Azure como armazenamento adicional da saudação.
    - Acesso de repositório data Lake: configurar o acesso entre a conta do repositório Data Lake hello e o cluster HDInsight. Para obter instruções, consulte [Configurar acesso ao Data Lake Store](#configure-data-lake-store-access).

## <a name="configure-data-lake-store-access"></a>Configurar acesso ao Data Lake Store 

Nesta seção, você configura o acesso ao Data Lake Store de clusters do HDInsight usando uma entidade de serviço do Azure Active Directory. 

### <a name="specify-a-service-principal"></a>Especificar uma entidade de serviço

De Olá portal do Azure, você pode usar uma entidade de serviço existente ou criar um novo.

**toocreate uma entidade de serviço de saudação portal do Azure**

1. Clique em **acesso de repositório Data Lake** da folha de repositório de saudação.
2. Em Olá **acesso de repositório Data Lake** folha, clique em **criar novo**.
3. Clique em **entidade de serviço**e siga as instruções de saudação toocreate uma entidade de serviço.
4. Baixar o certificado de saudação se você decidir toouse-lo novamente no futuro de saudação. Baixando certificado de saudação é útil que se você quiser toouse Olá mesmo serviço principal, quando você criar clusters de HDInsight adicionais.

    ![Cluster de tooHDInsight principal de serviço Add](./media/data-lake-store-hdinsight-hadoop-use-portal/hdi.adl.2.png "adicionar cluster de tooHDInsight principal de serviço")

4. Clique em **acesso** tooconfigure acesso à pasta de saudação.  Consulte [Configurar permissões de arquivo](#configure-file-permissions).


**toouse uma entidade de saudação do Azure portal de serviço existente**

1. Clique em **Acesso ao Data Lake Store**.
1. Em Olá **acesso de repositório Data Lake** folha, clique em **usar existente**.
2. Clique em **Entidade de Serviço** e, em seguida, selecione uma entidade de serviço. 
3. Carregar certificado de hello (arquivo. pfx) que é associado com a entidade de serviço selecionado e, em seguida, digite a senha do certificado hello.

    ![Cluster de tooHDInsight principal de serviço Add](./media/data-lake-store-hdinsight-hadoop-use-portal/hdi.adl.5.png "adicionar cluster de tooHDInsight principal de serviço")

4. Clique em **acesso** tooconfigure acesso à pasta de saudação.  Consulte [Configurar permissões de arquivo](#configure-file-permissions).


### <a name="configure-file-permissions"></a>Configurar permissões de arquivo

Olá configura são diferentes dependendo se a conta de saudação é usada como uma conta de armazenamento adicional ou de armazenamento padrão da saudação:

- Usado como o armazenamento padrão

    - permissão no nível de raiz de saudação do hello conta do repositório Data Lake
    - permissão no nível de raiz de saudação do hello armazenamento de cluster HDInsight. Por exemplo, Olá __/clusters__ pasta usada anteriormente no tutorial de saudação.
- Usar como um armazenamento adicional

    - Permissão em pastas de saudação onde você acesso necessário ao arquivo.

**permissão de tooassign a saudação de nível de raiz de conta do repositório Data Lake**

1. Em Olá **acesso de repositório Data Lake** folha, clique em **acesso**. Olá **selecionar permissões de arquivo** folha é aberta. Ele lista todas as contas do repositório Data Lake Olá em sua assinatura.
2. Passe o mouse (não clique) mouse Olá sobre nome de saudação do hello toomake Olá caixa de seleção visível, em seguida, selecione Olá a caixa de seleção de conta de repositório Data Lake.

    ![Cluster de tooHDInsight principal de serviço Add](./media/data-lake-store-hdinsight-hadoop-use-portal/hdi.adl.3.png "adicionar cluster de tooHDInsight principal de serviço")

  Por padrão, as opções __LER__, __GRAVAR__ E __EXECUTAR__ estão selecionadas.

3. Clique em **selecione** na parte inferior da saudação da página de saudação.
4. Clique em **executar** tooassign permissão.
5. Clique em **Concluído**.

**permissão de tooassign a saudação de nível de raiz de cluster do HDInsight**

1. Em Olá **acesso de repositório Data Lake** folha, clique em **acesso**. Olá **selecionar permissões de arquivo** folha é aberta. Ele lista todas as contas do repositório Data Lake Olá em sua assinatura.
1. De saudação **selecionar permissões de arquivo** folha, clique em tooshow de nome de repositório Data Lake Olá seu conteúdo.
2. Selecione raiz de armazenamento de cluster de HDInsight Olá de caixa de seleção Olá esquerda saudação da pasta hello. De acordo com captura de tela de toohello anteriormente, é de raiz de armazenamento de cluster Olá __/clusters__ pasta que você especificou ao selecionar repositório Olá Data Lake como armazenamento padrão.
3. Definir permissões de saudação na pasta de saudação.  Por padrão, as opções ler, gravar e executar estão selecionadas.
4. Clique em **selecione** na parte inferior da saudação da página de saudação.
5. Clique em **Executar**.
6. Clique em **Concluído**.

Se você estiver usando o repositório Data Lake como armazenamento adicional, você deve atribuir permissão somente para pastas de saudação que você deseja tooaccess do cluster do HDInsight hello. Por exemplo, abaixo da captura de tela hello, você fornecer acesso apenas muito**hdiaddonstorage** pasta em uma conta do repositório Data Lake.

![Atribuir o cluster HDInsight do serviço principal permissões toohello](./media/data-lake-store-hdinsight-hadoop-use-portal/hdi.adl.3-1.png "cluster de HDInsight atribuir serviço principal permissões toohello")


## <a name="verify-cluster-set-up"></a>Verificar a configuração do cluster

Após a conclusão da instalação do cluster Olá, na folha de cluster Olá, verifique os resultados, fazendo uma ou ambas Olá etapas a seguir:

* tooverify Olá armazenamento associado para cluster Olá é a conta do repositório Data Lake Olá que você especificou, clique em **contas de armazenamento** no painel esquerdo da saudação.

    ![Cluster de tooHDInsight principal de serviço Add](./media/data-lake-store-hdinsight-hadoop-use-portal/hdi.adl.6-1.png "adicionar cluster de tooHDInsight principal de serviço")

* tooverify que Olá entidade de serviço está corretamente associado ao cluster do HDInsight hello, clique em **acesso de repositório Data Lake** no painel esquerdo da saudação.

    ![Cluster de tooHDInsight principal de serviço Add](./media/data-lake-store-hdinsight-hadoop-use-portal/hdi.adl.6.png "adicionar cluster de tooHDInsight principal de serviço")


## <a name="examples"></a>Exemplos

Depois que você configurou o cluster Olá com repositório Data Lake como seu armazenamento, consulte exemplos toothese como toouse HDInsight cluster dados saudação tooanalyze que são armazenados no repositório Data Lake.

### <a name="run-a-hive-query-against-data-in-a-data-lake-store-as-primary-storage"></a>Executar uma consulta do Hive nos dados de um Data Lake Store (como armazenamento primário)

toorun uma consulta de Hive, use a interface de modos de exibição de Hive de Olá no portal do Ambari hello. Para obter instruções sobre como toouse Ambari Hive exibições, consulte [Olá Use exibição de Hive com Hadoop no HDInsight](../hdinsight/hdinsight-hadoop-use-hive-ambari-view.md).

Quando você trabalha com dados em um repositório Data Lake, há alguns toochange de cadeias de caracteres.

Se você usar, por exemplo, Olá cluster que você criou com o repositório Data Lake como armazenamento primário, dados de toohello saudação caminho serão: *publicitário: / / < data_lake_store_account_name > /azuredatalakestore.net/path/to/file*. Um toocreate de consulta de Hive uma tabela de dados de exemplo que são armazenados na conta do repositório Data Lake do hello aparência Olá instrução a seguir:

    CREATE EXTERNAL TABLE websitelog (str string) LOCATION 'adl://hdiadlsstorage.azuredatalakestore.net/clusters/myhdiadlcluster/HdiSamples/HdiSamples/WebsiteLogSampleData/SampleLog/'

Descrições:
* `adl://hdiadlstorage.azuredatalakestore.net/`é a raiz de saudação da saudação conta do repositório Data Lake.
* `/clusters/myhdiadlcluster`é a raiz de saudação de dados de cluster Olá que você especificou ao criar o cluster de saudação.
* `/HdiSamples/HdiSamples/WebsiteLogSampleData/SampleLog/`é o local de saudação do arquivo de exemplo hello usado na consulta de saudação.

### <a name="run-a-hive-query-against-data-in-a-data-lake-store-as-additional-storage"></a>Executar uma consulta do Hive nos dados de um Data Lake Store (como armazenamento adicional)

Se o cluster Olá que você criou usa o armazenamento de Blob como armazenamento padrão, os dados de exemplo hello não está no hello conta do repositório Azure Data Lake que é usada como armazenamento adicional. Nesse caso, primeiro transferir dados de saudação do armazenamento de Blob toohello repositório Data Lake e, em seguida, execute consultas hello, conforme mostrado no hello anterior de exemplo.

Para obter informações sobre como toocopy do armazenamento de Blob tooa Data Lake do repositório de dados, consulte Olá artigos a seguir:

* [Usar dados de toocopy Distcp entre blobs de armazenamento do Azure e o repositório Data Lake](data-lake-store-copy-data-wasb-distcp.md)
* [Usar AdlCopy toocopy dados de armazenamento do Azure tooData Lake armazenamento de blobs](data-lake-store-copy-data-azure-storage-blob.md)

### <a name="use-data-lake-store-with-a-spark-cluster"></a>Usar o Data Lake Store com o cluster Spark
Você pode usar um trabalhos do Spark cluster toorun Spark nos dados armazenados em um repositório Data Lake. Para obter mais informações, consulte [dados de tooanalyze cluster Use HDInsight Spark no repositório Data Lake](../hdinsight/hdinsight-apache-spark-use-with-data-lake-store.md).


### <a name="use-data-lake-store-in-a-storm-topology"></a>Usar o Repositório Data Lake em uma topologia do Storm
Você pode usar dados de toowrite do repositório Data Lake saudação de uma topologia Storm. Para obter instruções sobre como tooachieve neste cenário, consulte [repositório Azure Data Lake Use com Apache Storm com HDInsight](../hdinsight/hdinsight-storm-write-data-lake-store.md).

## <a name="see-also"></a>Consulte também
* [PowerShell: Criar um cluster de HDInsight toouse repositório Data Lake](data-lake-store-hdinsight-hadoop-use-powershell.md)

[makecert]: https://msdn.microsoft.com/library/windows/desktop/ff548309(v=vs.85).aspx
[pvk2pfx]: https://msdn.microsoft.com/library/windows/desktop/ff550672(v=vs.85).aspx
