---
title: aaaHue com Hadoop em clusters baseados em HDInsight Linux - Azure | Microsoft Docs
description: "Saiba como clusters de matiz tooinstall no HDInsight e use túnel tooroute Olá solicitações tooHue. Usar o armazenamento de toobrowse matiz e execute o Hive ou Pig."
keywords: hue hadoop
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 9e57fcca-e26c-479d-a745-7b80a9290447
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: f086cbad2a90cc6903fbfccbf4a6be44f8999d07
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="install-and-use-hue-on-hdinsight-hadoop-clusters"></a>Instalar e usar o Hue em clusters de Hadoop do HDInsight

Saiba como clusters de matiz tooinstall no HDInsight e use túnel tooroute Olá solicitações tooHue.

> [!IMPORTANT]
> etapas de saudação neste documento exigem um cluster HDInsight que usa o Linux. Linux é Olá sistema operacional somente de usado no HDInsight versão 3.4 ou posterior. Para obter mais informações, confira [baixa do HDInsight no Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).

## <a name="what-is-hue"></a>O que é o Hue?
O matiz é que um conjunto de aplicativos da Web usado toointeract com um cluster Hadoop. Você pode usar o matiz toobrowse Olá armazenamento associado a um cluster de Hadoop (no caso de saudação de clusters de HDInsight, WASB), executar os scripts de Pig e Hive trabalhos e assim por diante. Olá a componentes a seguir estão disponíveis com instalações de matiz em um cluster HDInsight Hadoop.

* Editor de Hive Beeswax
* Pig
* Gerenciador do Metastore
* Oozie
* FileBrowser (que fala contêiner padrão de tooWASB)
* Navegador de Trabalhos

> [!WARNING]
> Componentes fornecidos com o cluster do HDInsight Olá são totalmente suportados e ajudarão tooisolate e resolver problemas relacionados toothese componentes Microsoft Support.
>
> Componentes personalizados recebem suporte comercialmente razoável toohelp toofurther você solucionar o problema de saudação. Isso pode resultar em resolver o problema de saudação ou solicitando que tooengage de canais disponíveis para Olá abrir tecnologias de origem onde profundo conhecimento para que a tecnologia é encontrado. Por exemplo, há muitos sites de comunidades que podem ser usados, como o [Fórum do MSDN para o HDInsight](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=hdinsight), [http://stackoverflow.com](http://stackoverflow.com). Além disso, os projetos do Apache têm sites do projeto em [http://apache.org](http://apache.org), por exemplo: [Hadoop](http://hadoop.apache.org/).
>
>

## <a name="install-hue-using-script-actions"></a>Instalar o Hue usando Ações de Script

Olá script tooinstall matiz em um cluster HDInsight baseados em Linux está disponível em https://hdiconfigactions.blob.core.windows.net/linuxhueconfigactionv02/install-hue-uber-v02.sh. Você pode usar este script tooinstall matiz em clusters com Blobs de armazenamento do Azure (WASB) ou repositório Azure Data Lake como armazenamento padrão.

Esta seção fornece instruções sobre como toouse Olá script durante o provisionamento de cluster hello usando Olá portal do Azure.

> [!NOTE]
> PowerShell do Azure, Olá CLI do Azure, Olá HDInsight .NET SDK ou modelos do Azure Resource Manager também podem ser usado tooapply ações de script. Você também pode aplicar o script ações tooalready clusters em execução. Para saber mais, veja [Personalizar clusters HDInsight com as Ações de Script](hdinsight-hadoop-customize-cluster-linux.md).
>
>

1. Iniciar o provisionamento de um cluster usando as etapas de saudação em [HDInsight provisionar clusters no Linux](hdinsight-hadoop-provision-linux-clusters.md), mas não conclua o provisionamento.

   > [!NOTE]
   > clusters de matiz tooinstall no HDInsight, hello tamanho recomendado de um nó principal é pelo menos A4 (8 núcleos, 14 GB de memória).
   >
   >
2. Em Olá **configuração opcional** folha, selecione **ações de Script**e fornecer informações de hello, conforme mostrado abaixo:

    ![Fornecer parâmetros de ação de script para Matiz](./media/hdinsight-hadoop-hue-linux/hue-script-action.png "Fornecer parâmetros de ação de script para Matiz")

   * **NOME**: insira um nome amigável para a ação de script hello.
   * **URI DO SCRIPT**: https://hdiconfigactions.blob.core.windows.net/linuxhueconfigactionv02/install-hue-uber-v02.sh
   * **CABEÇALHO**: marque esta opção
   * **TRABALHO**: deixe essa opção em branco.
   * **ZOOKEEPER**: deixe essa opção em branco.
   * **PARÂMETROS**: deixe essa opção em branco.
3. Na parte inferior de saudação do hello **ações de Script**, use Olá **selecione** configuração de saudação do botão toosave. Por fim, use Olá **selecione** botão na parte inferior de saudação do hello **configuração opcional** informações de configuração opcional de saudação de toosave de folha.
4. Continuar o provisionamento de cluster Olá conforme descrito em [HDInsight provisionar clusters no Linux](hdinsight-hadoop-provision-linux-clusters.md).

## <a name="use-hue-with-hdinsight-clusters"></a>Usar o Hue com clusters do HDInsight

Túnel SSH é tooaccess de maneira única matiz Olá no cluster hello quando ele estiver em execução. Túnel SSH permite Olá tráfego toogo diretamente de um nó principal toohello de saudação do cluster onde matiz está em execução. Após cluster Olá provisionamento, use Olá matiz de toouse as etapas a seguir em um cluster HDInsight Linux.

> [!NOTE]
> É recomendável usar o Firefox web navegador toofollow Olá instruções a seguir.
>
>

1. Use as informações de saudação em [tooaccess Use SSH túnel Ambari web da interface do usuário, ResourceManager, JobHistory, NameNode, Oozie e outra interface de usuário de web](hdinsight-linux-ambari-ssh-tunnel.md) toocreate um SSH de túnel do seu cluster HDInsight de toohello de sistema de cliente e, em seguida, configurar o Web navegador toouse Olá túnel SSH como um proxy.

2. Depois que você criou um túnel SSH e configurou o tráfego de tooproxy de navegador por ele, você deve encontrar nome de host de saudação do nó de cabeçalho principal hello. Você pode fazer isso por meio da conexão toohello cluster usando o SSH na porta 22. Por exemplo, `ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net` onde **USERNAME** é o nome de usuário SSH e **CLUSTERNAME** é o nome de saudação do cluster.

    Para obter mais informações, confira [Usar SSH com HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

3. Uma vez conectado, use Olá após o nome de domínio totalmente qualificado do comando tooobtain Olá de um nó principal do hello primário:

        hostname -f

    Isso retornará uma nome semelhante toohello a seguir:

        hn0-myhdi-nfebtpfdv1nubcidphpap2eq2b.ex.internal.cloudapp.net

    Isso é Olá hostname de um nó principal do hello primário onde o site de matiz hello está localizado.
4. Use o hello navegador tooopen Olá matiz portal em http://HOSTNAME:8888. Substitua o nome de host pelo nome de Olá obtida na etapa anterior hello.

   > [!NOTE]
   > Quando você efetuar login para Olá primeira vez, será solicitado toocreate toolog uma conta no portal de matiz toohello. as credenciais de saudação especificado aqui serão limitado toohello portal e não são relacionadas toohello admin ou SSH especificado ao cluster de saudação provisionar as credenciais do usuário.
   >
   >

    ![Portal de matiz logon toohello](./media/hdinsight-hadoop-hue-linux/hdinsight-hue-portal-login.png "especificar credenciais para o portal de matiz")

### <a name="run-a-hive-query"></a>Executar um trabalho do Hive
1. No portal de matiz hello, clique em **editores de consulta**e, em seguida, clique em **Hive** editor do tooopen Olá Hive.

    ![Usar o Hive](./media/hdinsight-hadoop-hue-linux/hdinsight-hue-portal-use-hive.png "Usar o Hive")
2. Em Olá **auxiliar** guia em **banco de dados**, você deve ver **hivesampletable**. Essa é uma tabela de exemplo que é enviada juntamente com todos os clusters de Hadoop no HDInsight. Insira uma consulta de exemplo no painel direito da saudação e ver o resultado de saudação em Olá **resultados** guia no painel de saudação abaixo, conforme mostrado na captura de tela de saudação.

    ![Executar consulta de Hive](./media/hdinsight-hadoop-hue-linux/hdinsight-hue-portal-hive-query.png "Executar consulta de Hive")

    Você também pode usar o hello **gráfico** guia toosee uma representação visual dos resultados de saudação.

### <a name="browse-hello-cluster-storage"></a>Procurar armazenamento de cluster Olá
1. No portal de matiz hello, clique em **navegador de arquivo** no canto superior direito de saudação da barra de menus do hello.
2. Por padrão, o navegador de arquivo hello abre no hello **/usuário/myuser** directory. Clique em barra Olá antes de diretório de usuário Olá na raiz do hello caminho toogo toohello do contêiner de armazenamento do Azure Olá associada Olá cluster.

    ![Use o navegador de arquivos](./media/hdinsight-hadoop-hue-linux/hdinsight-hue-portal-file-browser.png "Use o navegador de arquivos")
3. Clique duas vezes em um arquivo ou pasta toosee Olá disponível operações. Saudação de uso **carregar** botão no hello direita tooupload toohello atual diretório. Saudação de uso **novo** botão toocreate novos arquivos ou diretórios.

> [!NOTE]
> navegador de arquivo Hello matiz só pode mostrar conteúdo Olá Olá padrão do contêiner de associado cluster do HDInsight hello. Qualquer contas/contêineres de armazenamento adicional que pode associado ao cluster Olá não será acessíveis usando o navegador de arquivo hello. No entanto, recipientes adicionais de saudação associadas Olá cluster sempre será acessíveis para trabalhos de Hive hello. Por exemplo, se você inserir o comando Olá `dfs -ls wasb://newcontainer@mystore.blob.core.windows.net` no editor de Hive hello, você pode ver o conteúdo de saudação de recipientes adicionais também. Neste comando, **newcontainer** não for saudação padrão contêiner associado a um cluster.
>
>

## <a name="important-considerations"></a>Considerações importantes
1. Olá script usado tooinstall matiz instala apenas em Olá um nó principal primário do cluster hello.

2. Durante a instalação, vários serviços de Hadoop (HDFS, YARN, MR2, Oozie) são reiniciados para atualizar a configuração de saudação. Depois que o script hello termina de instalar o matiz, ele pode levar algum tempo para que outros toostart de serviços Hadoop até. Isso pode, inicialmente, afetar o desempenho do Hue. Depois que todos os serviços tiverem sido iniciados, o Hue estará totalmente funcional.
3. Matiz não compreende Tez trabalhos, que é o padrão atual para o Hive do hello. Se você quiser toouse MapReduce como Olá Hive do mecanismo de execução, atualize Olá Olá de toouse script comando no script a seguir:

        set hive.execution.engine=mr;

4. Com clusters do Linux, você pode ter um cenário onde os serviços estão em execução no nó primário principal de saudação enquanto Olá Gerenciador de recursos pode estar em execução no hello secundário. Esse cenário pode resultar em erros (mostrados abaixo) ao usar detalhes de tooview matiz de trabalhos em execução no cluster de saudação. No entanto, você pode exibir detalhes do trabalho hello quando Olá trabalho foi concluído.

   ![Erro no portal de matiz](./media/hdinsight-hadoop-hue-linux/hdinsight-hue-portal-error.png "Erro no portal de matiz")

   Isso é devido tooa problema conhecido. Como alternativa, modifique Ambari para que hello active Gerenciador de recursos também é executado em um nó principal do hello primário.
5. O Hue entende o WebHDFS, enquanto os clusters HDInsight utilizam o Armazenamento do Azure com o `wasb://`. Portanto, o script de personalizado Olá utilizado com a ação de script instala WebWasb, que é um serviço compatível com WebHDFS para conversar tooWASB. Portanto, embora o portal de matiz Olá diz HDFS em locais (como quando você move o mouse sobre Olá **navegador de arquivo**), ele deve ser interpretado como WASB.

## <a name="next-steps"></a>Próximas etapas
* [Instalar o Giraph em clusters HDInsight](hdinsight-hadoop-giraph-install-linux.md). Use cluster personalização tooinstall que giraph no Hadoop de HDInsight clusters. Giraph permite tooperform gráfico usando Hadoop de processamento e pode ser usado com o Azure HDInsight.
* [Instalar o Solr em clusters HDInsight](hdinsight-hadoop-solr-install-linux.md). Use cluster personalização tooinstall que solr no Hadoop de HDInsight clusters. Solr permite operações de pesquisa poderoso tooperform nos dados armazenados.
* [Instalar o R em clusters HDInsight](hdinsight-hadoop-r-scripts-linux.md). Use cluster personalização tooinstall R em clusters de HDInsight Hadoop. R é uma linguagem e ambiente de software livre para computação estatística. Ele fornece centenas de funções estatísticas internas e sua própria linguagem de programação, que combina aspectos de programação funcional e de programação orientada a objetos. Ele também fornece recursos abrangentes de gráficos.

[powershell-install-configure]: install-configure-powershell-linux.md
[hdinsight-provision]: hdinsight-provision-clusters-linux.md
[hdinsight-cluster-customize]: hdinsight-hadoop-customize-cluster-linux.md
