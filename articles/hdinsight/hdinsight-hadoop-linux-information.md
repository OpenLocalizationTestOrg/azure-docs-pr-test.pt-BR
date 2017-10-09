---
title: aaaTips para usar Hadoop em HDInsight baseados em Linux - Azure | Microsoft Docs
description: "Obtenha dicas de implementação para usar clusters HDInsight baseados em Linux (Hadoop) em um ambiente familiar do Linux em execução no hello nuvem do Azure."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: c41c611c-5798-4c14-81cc-bed1e26b5609
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/12/2017
ms.author: larryfr
ms.openlocfilehash: a555622605079c9beae88ece872042e36d540c7d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="information-about-using-hdinsight-on-linux"></a>Informações sobre o uso do HDInsight no Linux

Clusters de HDInsight do Azure fornecem Hadoop em um ambiente familiar do Linux, em execução no hello nuvem do Azure. Para a maioria da coisas, ele deve funcionar exatamente como qualquer outra instalação do Hadoop no Linux. Este documento indica diferenças específicas que você deve estar atento.

> [!IMPORTANT]
> Linux é Olá sistema operacional somente de usado no HDInsight versão 3.4 ou posterior. Para obter mais informações, confira [baixa do HDInsight no Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).

## <a name="prerequisites"></a>Pré-requisitos

Muitas das etapas neste documento hello usam Olá utilitários, que podem ser necessário toobe instalado no seu sistema a seguir.

* [cURL](https://curl.haxx.se/) -usado toocommunicate com serviços baseados na web
* [jq](https://stedolan.github.io/jq/) -usado tooparse documentos JSON
* [2.0 do CLI do Azure](https://docs.microsoft.com/cli/azure/install-az-cli2) (visualização) - tooremotely usado gerenciar serviços do Azure

## <a name="users"></a>Usuários

A menos que tenha [ingressado no domínio](hdinsight-domain-joined-introduction.md), o HDInsight deve ser considerado como um sistema de **usuário único**. Uma conta de usuário SSH é criada com o cluster hello, com permissões de nível de administrador. Contas SSH adicionais podem ser criadas, mas eles também têm o cluster de toohello de acesso de administrador.

O domínio HDInsight dá suporte para vários usuários e configurações de função e de permissão mais granulares. Para obter mais informações, consulte [Gerenciar clusters HDInsight ingressados em domínio](hdinsight-domain-joined-manage.md).

## <a name="domain-names"></a>Nomes de domínio

Olá totalmente qualificado toouse de nome (FQDN) do domínio ao se conectar a cluster toohello de saudação internet é  **&lt;clustername >. cluster>.azurehdinsight.NET** ou (SSH)  **&lt;clustername-ssh >. cluster>.azurehdinsight.NET**.

Internamente, cada nó no cluster Olá tem um nome que é atribuído durante a configuração do cluster. nomes de cluster Olá toofind, consulte Olá **Hosts** página Olá da interface do usuário do Ambari Web. Você também pode usar o hello tooreturn uma lista de hosts de saudação Ambari API de REST a seguir:

    curl -u admin:PASSWORD -G "https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/hosts" | jq '.items[].Hosts.host_name'

Substituir **senha** com senha de saudação da conta de administrador Olá, e **CLUSTERNAME** com nome de saudação do cluster. Esse comando retorna um documento JSON que contém uma lista de hosts de saudação em cluster hello. Jq é usado tooextract Olá `host_name` valor do elemento para cada host.

Se você precisar toofind nome de saudação do nó de saudação para um serviço específico, você pode consultar Ambari para esse componente. Por exemplo, hosts de saudação toofind para o nó do nome HDFS hello, use Olá comando a seguir:

    curl -u admin:PASSWORD -G "https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/services/HDFS/components/NAMENODE" | jq '.host_components[].HostRoles.host_name'

Esse comando retorna um documento JSON que descreve o serviço hello e, em seguida, efetua pull de jq out só Olá `host_name` valor para os hosts de saudação.

## <a name="remote-access-tooservices"></a>Tooservices de acesso remoto

* **Ambari (web)** - https://&lt;nomedocluster>.azurehdinsight.net

    Autenticar usando a senha e o usuário de administrador de cluster hello e, em seguida, faça logon no tooAmbari.

    A autenticação é texto sem formatação - sempre use HTTPS toohelp Certifique-se de que a conexão de saudação é segura.

    > [!IMPORTANT]
    > Alguns dos Olá web interfaces do usuário disponíveis por meio de nós de acesso do Ambari usando um nome de domínio interno. Nomes não forem publicamente acessíveis através de domínio interno Olá da internet. Você pode receber erros de "servidor não encontrado" quando você tentar tooaccess alguns recursos sobre Olá da Internet.
    >
    > toouse Olá toda a funcionalidade do Olá Ambari web da interface do usuário, use um SSH túnel tooproxy web tráfego toohello nó principal do cluster. Consulte [Use SSH túnel tooaccess Ambari web da interface do usuário, ResourceManager, JobHistory, NameNode, Oozie e outras interfaces do usuário da web](hdinsight-linux-ambari-ssh-tunnel.md)

* **Ambari (REST)** - https://&lt;nomedocluster>.azurehdinsight.net/ambari

    > [!NOTE]
    > Autentica usando a senha e o usuário de administrador de cluster de saudação.
    >
    > A autenticação é texto sem formatação - sempre use HTTPS toohelp Certifique-se de que a conexão de saudação é segura.

* **WebHCat (Templeton)** - https://&lt;nomedocluster>.azurehdinsight.net/templeton

    > [!NOTE]
    > Autentica usando a senha e o usuário de administrador de cluster de saudação.
    >
    > A autenticação é texto sem formatação - sempre use HTTPS toohelp Certifique-se de que a conexão de saudação é segura.

* **SSH** - &lt;nomedocluster>-ssh.azurehdinsight.net na porta 22 ou 23. Porta 22 é um nó principal primário de toohello de tooconnect usadas, enquanto 23 é usado tooconnect toohello secundário. Para obter mais informações sobre nós de cabeçalho hello, consulte [clusters de disponibilidade e confiabilidade do Hadoop no HDInsight](hdinsight-high-availability-linux.md).

    > [!NOTE]
    > Você pode acessar somente nós de cluster de saudação principal por meio do SSH de um computador cliente. Uma vez conectado, você pode acessar, em seguida, nós de trabalho hello usando SSH de um nó principal.

## <a name="file-locations"></a>Locais de arquivos

Arquivos relacionados ao Hadoop podem ser encontrado em nós de cluster Olá no `/usr/hdp`. Este diretório contém Olá seguintes subpastas:

* **2.2.4.9-1**: nome do diretório Olá é a versão de saudação do hello Hortonworks Data Platform usado pelo HDInsight. número de saudação no cluster pode ser diferente de saudação listados aqui.
* **atual**: este diretório contém links toosubdirectories em Olá **2.2.4.9-1** directory. Esse diretório existe para que você não tem o número de versão tooremember hello.

Dados de exemplo e arquivos JAR encontram-se no Sistema de Arquivos Distribuído Hadoop em `/example` e `/HdiSamples`

## <a name="hdfs-azure-storage-and-data-lake-store"></a>HDFS, Armazenamento do Azure e Data Lake Store

Na maioria das distribuições do Hadoop, HDFS é apoiado pelo armazenamento local nas máquinas Olá cluster hello. Utilizar armazenamento local pode ser dispendioso para uma solução baseada em nuvem onde você é cobrado por hora ou minuto por recursos cibernéticos.

HDInsight usa o blobs no armazenamento do Azure ou repositório Azure Data Lake como repositório de saudação. Esses serviços oferecem Olá benefícios a seguir:

* Armazenamento de longo prazo econômico
* Acessibilidade por meio de serviços externos, como sites, utilitários de upload/download de arquivos, SDKs para vários idiomas e navegadores da Web

> [!WARNING]
> O HDInsight suporta apenas contas do Azure Storage de __Uso geral__. Ele não oferece suporte a saudação __armazenamento de Blob__ tipo de conta.

Uma conta de armazenamento do Azure pode conter backup too4.75 TB, embora os blobs individuais (ou arquivos de uma perspectiva de HDInsight) só podem chegar a too195 GB. Repositório Azure Data Lake pode crescer dinamicamente toohold trilhões de arquivos, com mais de um petabyte de arquivos individuais. Para saber mais, confira [Noções básicas sobre blobs](https://docs.microsoft.com/rest/api/storageservices/understanding-block-blobs--append-blobs--and-page-blobs) e [Data Lake Store](https://azure.microsoft.com/services/data-lake-store/).

Ao usar o armazenamento do Azure ou repositório Data Lake, você não tem toodo nada especial de dados de saudação do HDInsight tooaccess. Por exemplo, Olá comando a seguir lista os arquivos no hello `/example/data` pasta independentemente de ele é armazenado no armazenamento do Azure ou repositório Data Lake:

    hdfs dfs -ls /example/data

### <a name="uri-and-scheme"></a>URI e esquema

Alguns comandos podem exigir esquema de saudação toospecify como parte do URI de saudação ao acessar um arquivo. Por exemplo, Olá componente Storm HDFS requer esquema de saudação toospecify. Ao usar o armazenamento não padrão (armazenamento adicionado como armazenamento "adicional" toohello cluster), você sempre deve usar o esquema de saudação como parte do URI de saudação.

Ao usar __armazenamento do Azure__, use um dos Olá esquemas URI a seguir:

* `wasb:///`: acessar o armazenamento padrão usando comunicação não criptografada.

* `wasbs:///`: acessar o armazenamento padrão usando comunicação criptografada.  esquema de wasbs Olá tem suporte somente a partir de HDInsight versão 3.6 em diante.

* `wasb://<container-name>@<account-name>.blob.core.windows.net/`: usado ao se comunicar com uma conta de armazenamento não padrão. Por exemplo, se você tiver uma conta de armazenamento adicional ou ao acessar dados armazenados em uma conta de armazenamento com acesso público.

Ao usar __repositório Data Lake__, use um dos Olá esquemas URI a seguir:

* `adl:///`: Acesso Olá Lake armazenamento de dados padrão para o cluster de saudação.

* `adl://<storage-name>.azuredatalakestore.net/`: utilizado ao se comunicar com uma conta de armazenamento Data Lake não padrão. Também usado tooaccess dados fora do diretório raiz de saudação do seu cluster HDInsight.

> [!IMPORTANT]
> Ao usar o repositório Data Lake como saudação de armazenamento padrão para HDInsight, você deve especificar um caminho dentro Olá repositório toouse como raiz de saudação do armazenamento de HDInsight. caminho padrão de saudação é `/clusters/<cluster-name>/`.
>
> Ao usar `/` ou `adl:///` tooaccess dados, você pode acessar somente os dados armazenados na raiz da saudação (por exemplo, `/clusters/<cluster-name>/`) do cluster hello. tooaccess dados em qualquer lugar no repositório de hello, use Olá `adl://<storage-name>.azuredatalakestore.net/` formato.

### <a name="what-storage-is-hello-cluster-using"></a>O armazenamento é usando o cluster Olá

Você pode usar a configuração de armazenamento do Ambari tooretrieve saudação padrão para o cluster de saudação. Use Olá seguinte comando informações de configuração do HDFS tooretrieve usando ondulação e filtrá-los usando [jq](https://stedolan.github.io/jq/):

```curl -u admin:PASSWORD -G "https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/configurations/service_config_versions?service_name=HDFS&service_config_version=1" | jq '.items[].configurations[].properties["fs.defaultFS"] | select(. != null)'```

> [!NOTE]
> Isso retorna o primeiro servidor de toohello configuração aplicada hello (`service_config_version=1`), que contém essas informações. Talvez seja necessário toolist todas as versões de configuração toofind hello mais recente.

Este comando retorna um toohello semelhante valor URIs a seguir:

* `wasb://<container-name>@<account-name>.blob.core.windows.net`, se estiver usando uma conta de armazenamento do Azure.

    Hello, nome da conta é Olá nome da conta de armazenamento do Azure hello, enquanto o nome do contêiner de saudação é o contêiner de blob de saudação que é a raiz de Olá Olá de armazenamento de cluster.

* `adl://home`, se estiver usando o Azure Data Lake Store. nome do repositório Data Lake tooget hello, use Olá chamada REST a seguir:

    ```curl -u admin:PASSWORD -G "https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/configurations/service_config_versions?service_name=HDFS&service_config_version=1" | jq '.items[].configurations[].properties["dfs.adls.home.hostname"] | select(. != null)'```

    Esse comando retorna Olá após o nome do host: `<data-lake-store-account-name>.azuredatalakestore.net`.

    diretório de saudação tooget no repositório de saudação que é a raiz Olá para HDInsight, use Olá chamada REST a seguir:

    ```curl -u admin:PASSWORD -G "https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/configurations/service_config_versions?service_name=HDFS&service_config_version=1" | jq '.items[].configurations[].properties["dfs.adls.home.mountpoint"] | select(. != null)'```

    Esse comando retorna um toohello semelhante caminho caminho a seguir: `/clusters/<hdinsight-cluster-name>/`.

Você também pode encontrar informações de armazenamento hello usando Olá portal do Azure usando Olá etapas a seguir:

1. Em Olá [portal do Azure](https://portal.azure.com/), selecione o cluster HDInsight.

2. De saudação **propriedades** seção, selecione **contas de armazenamento**. Olá informações de armazenamento de cluster Olá são exibidas.

### <a name="how-do-i-access-files-from-outside-hdinsight"></a>Como acessar arquivos fora do HDInsight

Há uma várias maneiras tooaccess dados do cluster do HDInsight Olá externa. Olá seguem alguns links tooutilities e SDKs que podem ser usado toowork com seus dados:

Se usar __armazenamento do Azure__, consulte Olá links para que você pode acessar seus dados de maneiras a seguir:

* [CLI do Azure 2.0](https://docs.microsoft.com/cli/azure/install-az-cli2): comandos de interface de linha de comando para trabalhar com o Azure. Depois de instalar, usar Olá `az storage` comando para obter ajuda sobre o uso de armazenamento, ou `az storage blob` para comandos específicos do blob.
* [blobxfer.py](https://github.com/Azure/azure-batch-samples/tree/master/Python/Storage): um script Python para trabalhar com blobs no Armazenamento do Azure.
* Vários SDKs:

    * [Java](https://github.com/Azure/azure-sdk-for-java)
    * [Node.js](https://github.com/Azure/azure-sdk-for-node)
    * [PHP](https://github.com/Azure/azure-sdk-for-php)
    * [Python](https://github.com/Azure/azure-sdk-for-python)
    * [Ruby](https://github.com/Azure/azure-sdk-for-ruby)
    * [.NET](https://github.com/Azure/azure-sdk-for-net)
    * [API REST de armazenamento](https://msdn.microsoft.com/library/azure/dd135733.aspx)

Se usar __repositório Azure Data Lake__, consulte Olá links para que você pode acessar seus dados de maneiras a seguir:

* [Navegador da Web](../data-lake-store/data-lake-store-get-started-portal.md)
* [PowerShell](../data-lake-store/data-lake-store-get-started-powershell.md)
* [CLI 2.0 do Azure](../data-lake-store/data-lake-store-get-started-cli-2.0.md)
* [API de REST WebHDFS](../data-lake-store/data-lake-store-get-started-rest-api.md)
* [Ferramentas do Data Lake para Visual Studio](https://www.microsoft.com/download/details.aspx?id=49504)
* [.NET](../data-lake-store/data-lake-store-get-started-net-sdk.md)
* [Java](../data-lake-store/data-lake-store-get-started-java-sdk.md)
* [Python](../data-lake-store/data-lake-store-get-started-python.md)

## <a name="scaling"></a>Dimensionar o cluster

dimensionando o recurso de cluster de saudação permite toodynamically alterar o número de saudação de nós de dados usado por um cluster. Você pode executar operações de dimensionamento enquanto outros trabalhos ou processos estão sendo executados em um cluster.

tipos de cluster diferente de saudação são afetados por dimensionamento da seguinte maneira:

* **Hadoop**: na redução do número de saudação de nós em um cluster, alguns dos serviços de saudação em cluster Olá são reiniciados. Operações de dimensionamento pode causar trabalhos em execução ou pendente toofail na conclusão de saudação do hello a operação de dimensionamento. Você pode enviar novamente os trabalhos de saudação após a conclusão da operação de saudação.
* **HBase**: servidores regionais são balanceados automaticamente dentro de alguns minutos após a conclusão da operação de dimensionamento de saudação. servidores regionais de saldo de toomanually, use Olá etapas a seguir:

    1. Conecte-se o cluster do HDInsight toohello usando o SSH. Para obter mais informações, confira [Usar SSH com HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

    2. Use Olá shell do HBase Olá toostart a seguir:

            hbase shell

    3. Depois de saudação shell do HBase estiver carregado, use Olá servidores regionais de saudação do toomanually saldo a seguir:

            balancer

* **Storm**: você deve rebalancear qualquer topologia do Storm em execução após uma operação de dimensionamento. Rebalanceamento permite que as definições de paralelismo tooreadjust topologia Olá com base no número de novos Olá de nós do cluster de saudação. topologias de toorebalance em execução, use um dos Olá as opções a seguir:

    * **SSH**: conectar servidor toohello e comando de uso a seguir de saudação toorebalance uma topologia:

            storm rebalance TOPOLOGYNAME

        Você também pode especificar dicas de paralelismo parâmetros toooverride Olá originalmente fornecidas pelo topologia hello. Por exemplo, `storm rebalance mytopology -n 5 -e blue-spout=3 -e yellow-bolt=10` configura Olá processos de trabalho de too5 topologia, 3 executores de componente do hello spout azul e 10 executores de componente de amarelo brilhante hello.

    * **Profusão de interface do usuário**: etapas a seguir do uso Olá toorebalance uma topologia usando Olá profusão de interface do usuário.

        1. Abra **https://CLUSTERNAME.azurehdinsight.net/stormui** no navegador da web, onde CLUSTERNAME é o nome de saudação do cluster Storm. Se solicitado, insira o nome de administrador (admin) do cluster de HDInsight hello e senha que você especificou ao criar o cluster de saudação.
        2. Selecione Olá topologia desejar toorebalance, e selecione Olá **reequilibrar** botão. Inserir o intervalo de saudação antes Olá rebalanceie operação seja executada.

Para obter informações específicas sobre como dimensionar o cluster HDInsight, consulte:

* [Gerenciar clusters Hadoop em HDInsight usando Olá portal do Azure](hdinsight-administer-use-portal-linux.md#scale-clusters)
* [Gerenciar clusters Hadoop no HDInsight Usando o Azure PowerShell](hdinsight-administer-use-command-line.md#scale-clusters)

## <a name="how-do-i-install-hue-or-other-hadoop-component"></a>Como instalo o Hue (ou outro componente do Hadoop)?

O HDInsight é um serviço gerenciado. Se o Azure detectar um problema com o cluster hello, pode excluir Olá falha de nó e criar um nó tooreplace-lo. Se você instalar manualmente as coisas em cluster hello, eles não são mantidos quando a operação ocorre. Em vez disso, use as [Ações de Script HDInsight](hdinsight-hadoop-customize-cluster.md). Uma ação de script pode ser usado toomake Olá as seguintes alterações:

* Instalar e configurar um serviço ou um site da Web, como Spark ou Hue.
* Instale e configure um componente que requer alterações de configuração em vários nós de cluster de saudação. Por exemplo, uma variável de ambiente necessária, a criação de um diretório de log ou a criação de um arquivo de configuração.

Ações de script são scripts Bash. scripts de saudação executar durante o provisionamento de cluster e podem ser tooinstall usado e configurar componentes adicionais no cluster de saudação. Scripts de exemplo são fornecidos para a instalação Olá componentes a seguir:

* [Hue](hdinsight-hadoop-hue-linux.md)
* [Giraph](hdinsight-hadoop-giraph-install-linux.md)
* [Solr](hdinsight-hadoop-solr-install-linux.md)

Para saber mais sobre como desenvolver suas próprias ações de script, consulte [Desenvolvimento de ação de script com o HDInsight](hdinsight-hadoop-script-actions-linux.md).

### <a name="jar-files"></a>Arquivos Jar

Algumas tecnologias do Hadoop são fornecidas em arquivos jar independentes que contêm funções usadas como parte de um trabalho do MapReduce ou de dentro de Pig ou Hive. Enquanto eles podem ser instalados usando as ações de Script, eles geralmente não exigem nenhuma configuração e podem ser carregado toohello cluster após a configuração e usados diretamente. Se você quiser toomake-se de componente de saudação sobrevive refazer a imagem do cluster hello, você pode armazenar arquivos jar de saudação no armazenamento padrão da saudação para seu cluster (WASB ou publicitário).

Por exemplo, se você quiser toouse hello mais recente versão do [DataFu](http://datafu.incubator.apache.org/), você pode baixar um jar que contém o projeto hello e carregue-o cluster do HDInsight toohello. Siga a documentação de DataFu Olá sobre como toouse de Pig ou Hive.

> [!IMPORTANT]
> Alguns componentes que são arquivos jar de autônomos são fornecidos com o HDInsight, mas não estão no caminho de saudação. Se você estiver procurando por um componente específico, você pode usar o hello siga toosearch para ele no cluster:
>
> ```find / -name *componentname*.jar 2>/dev/null```
>
> Esse comando retorna o caminho de saudação de todos os arquivos jar correspondentes.

toouse uma versão diferente de um componente, carregamento Olá versão precisa e usá-lo em seus trabalhos.

> [!WARNING]
> Componentes fornecidos com o cluster do HDInsight Olá são totalmente suportados e Microsoft Support ajuda tooisolate e resolver problemas relacionados toothese componentes.
>
> Componentes personalizados recebem suporte comercialmente razoável toohelp toofurther você solucionar o problema de saudação. Isso pode resultar em resolver o problema de saudação ou solicitando que tooengage de canais disponíveis para Olá abrir tecnologias de origem onde profundo conhecimento para que a tecnologia é encontrado. Por exemplo, há muitos sites de comunidades que podem ser usados, como o [Fórum do MSDN para o HDInsight](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=hdinsight), [http://stackoverflow.com](http://stackoverflow.com). E mais, os projetos Apache têm sites de projeto em [http://apache.org](http://apache.org), por exemplo: [Hadoop](http://hadoop.apache.org/), [Spark](http://spark.apache.org/).

## <a name="next-steps"></a>Próximas etapas

* [Migrar do HDInsight baseados em Windows com base em tooLinux](hdinsight-migrate-from-windows-to-linux.md)
* [Usar o Hive com o HDInsight](hdinsight-use-hive.md)
* [Usar o Pig com o HDInsight](hdinsight-use-pig.md)
* [Usar trabalhos do MapReduce com o HDInsight](hdinsight-use-mapreduce.md)
