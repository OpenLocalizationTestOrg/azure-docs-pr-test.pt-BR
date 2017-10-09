---
title: "Ação de Script de aaaUse tooinstall Solr no HDInsight baseados em Linux - Azure | Microsoft Docs"
description: "Saiba como tooinstall Solr no Hadoop de HDInsight baseados em Linux clusters usando ações de Script."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: cc93ed5c-a358-456a-91a4-f179185c0e98
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/07/2017
ms.author: larryfr
ms.openlocfilehash: 4c179032b95ae187f1830d8927f8796372fa8ebe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="install-and-use-solr-on-hdinsight-hadoop-clusters"></a>Instalar e usar o Solr em clusters HDInsight do Hadoop

Saiba como tooinstall Solr no Azure HDInsight usando a ação de Script. O Solr é uma plataforma de pesquisa poderosa e oferece recursos de pesquisa em nível corporativo para os dados gerenciados pelo Hadoop.

> [!IMPORTANT]
    > etapas de saudação neste documento exigem um cluster HDInsight que usa o Linux. Linux é Olá sistema operacional somente de usado no HDInsight versão 3.4 ou posterior. Para obter mais informações, confira [baixa do HDInsight no Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).

> [!IMPORTANT]
> script de exemplo Hello usado neste documento instala 4.9 Solr com uma configuração específica. Se desejar que o cluster de Solr tooconfigure Olá com diferentes coleções, fragmentos, esquemas, réplicas, etc., você deve modificar o script hello e binários do Solr.

## <a name="whatis"></a>O que é Solr

O [Apache Solr](http://lucene.apache.org/solr/features.html) é uma plataforma de pesquisa empresarial que habilita operações poderosas de pesquisa de texto completo nos dados. Enquanto o Hadoop permite armazenar e gerenciar grandes quantidades de dados, o Apache Solr fornece recursos de pesquisa de saudação tooquickly recupera dados de saudação.

> [!WARNING]
> Componentes fornecidos com o cluster do HDInsight Olá são totalmente suportados pela Microsoft.
>
> Componentes personalizados, como Solr, recebem suporte comercialmente razoável toohelp toofurther você solucionar o problema de saudação. O suporte da Microsoft pode não ser capaz de tooresolve problemas com componentes personalizados. Talvez seja necessário comunidades de código-fonte aberto Olá tooengage para obter assistência. Por exemplo, há muitos sites de comunidades que podem ser usados, como o [Fórum do MSDN para o HDInsight](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=hdinsight), [http://stackoverflow.com](http://stackoverflow.com). Além disso, os projetos do Apache têm sites do projeto em [http://apache.org](http://apache.org), por exemplo: [Hadoop](http://hadoop.apache.org/).

## <a name="what-hello-script-does"></a>O script hello faz

Esse script faz Olá cluster do HDInsight toohello alterações a seguir:

* Instala o Solr 4.9 em `/usr/hdp/current/solr`
* Cria um usuário, **solrusr**, que é usado toorun Olá Solr serviço
* Conjuntos de **solruser** como proprietário de saudação do`/usr/hdp/current/solr`
* Adiciona uma configuração [Upstart](http://upstart.ubuntu.com/) que inicia automaticamente o Solr.

## <a name="install"></a>Instalar o Solr usando ações de script

Tooinstall um script de exemplo Solr em um cluster HDInsight está disponível em Olá local a seguir:

    https://hdiconfigactions.blob.core.windows.net/linuxsolrconfigactionv01/solr-installer-v01.sh

toocreate um cluster que tem Solr instalado, use Olá etapas Olá [HDInsight criar clusters](hdinsight-hadoop-create-linux-clusters-portal.md) documento. Durante o processo de criação de hello, use Olá etapas tooinstall Solr a seguir:

1. De saudação __resumo do Cluster__ folha, select__Advanced settings__, em seguida, __ações de Script__. Use Olá formulário de saudação toopopulate informações a seguir:

   * **NOME**: insira um nome amigável para a ação de script hello.
   * **URI do SCRIPT**: https://hdiconfigactions.blob.core.windows.net/linuxsolrconfigactionv01/solr-installer-v01.sh
   * **CABEÇALHO**: marque esta opção
   * **TRABALHO**: marque esta opção
   * **ZOOKEEPER**: verificar tooinstall essa opção no nó de Zookeeper Olá
   * **PARÂMETROS**: deixe este campo em branco

2. Na parte inferior de saudação do hello **ações de Script** folha, use Olá **selecione** configuração de saudação do botão toosave. Por fim, use Olá **próximo** botão tooreturn toohello __resumo do Cluster__

3. De saudação __resumo do Cluster__ página, selecione __criar__ toocreate cluster de saudação.

## <a name="usesolr"></a>Como usar o Solr no HDInsight

> [!IMPORTANT]
> etapas de Olá nesta seção demonstram a funcionalidade básica do Solr. Para obter mais informações sobre como usar Solr, consulte Olá [Solr Apache site](http://lucene.apache.org/solr/).

### <a name="index-data"></a>Dados de índice

Use Olá tooSolr de dados de exemplo de tooadd as etapas a seguir e, em seguida, consultá-los:

1. Conecte o cluster do HDInsight toohello usando SSH:

    ```bash
    ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
    ```

    Para obter mais informações, confira [Usar SSH com HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

     > [!IMPORTANT]
     > As etapas neste documento usam SSL túnel tooconnect toohello Solr da web da interface do usuário. toouse essas etapas, você deve estabelecer um SSL de túnel e, em seguida, configure seu navegador toouse-lo.
     >
     > Para obter mais informações, consulte Olá [usar SSH de encapsulamento HDInsight](hdinsight-linux-ambari-ssh-tunnel.md) documento.

2. Use Olá dados de exemplo do comandos toohave Solr índice a seguir:

    ```bash
    cd /usr/hdp/current/solr/example/exampledocs
    java -jar post.jar solr.xml monitor.xml
    ```

    Olá saída a seguir será retornada toohello console:

        POSTing file solr.xml
        POSTing file monitor.xml
        2 files indexed.
        COMMITting Solr index changes toohttp://localhost:8983/solr/update..
        Time spent: 0:00:01.624

    Olá `post.jar` utilitário adiciona Olá **solr.xml** e **monitor.xml** índice de toohello de documentos.
  
3. Use Olá Olá do comando tooquery Solr API de REST a seguir:

    ```bash
    curl "http://localhost:8983/solr/collection1/select?q=*%3A*&wt=json&indent=true"
    ```

    Este comando localiza **collection1** para documentos que correspondam a  **\*:\***  (codificado como \*% 3A\* na cadeia de caracteres de consulta de saudação). Olá documento JSON a seguir está um exemplo de resposta de saudação:

            "response": {
                "numFound": 2,
                "start": 0,
                "maxScore": 1,
                "docs": [
                  {
                    "id": "SOLR1000",
                    "name": "Solr, hello Enterprise Search Server",
                    "manu": "Apache Software Foundation",
                    "cat": [
                      "software",
                      "search"
                    ],
                    "features": [
                      "Advanced Full-Text Search Capabilities using Lucene",
                      "Optimized for High Volume Web Traffic",
                      "Standards Based Open Interfaces - XML and HTTP",
                      "Comprehensive HTML Administration Interfaces",
                      "Scalability - Efficient Replication tooother Solr Search Servers",
                      "Flexible and Adaptable with XML configuration and Schema",
                      "Good unicode support: héllo (hello with an accent over hello e)"
                    ],
                    "price": 0,
                    "price_c": "0,USD",
                    "popularity": 10,
                    "inStock": true,
                    "incubationdate_dt": "2006-01-17T00:00:00Z",
                    "_version_": 1486960636996878300
                  },
                  {
                    "id": "3007WFP",
                    "name": "Dell Widescreen UltraSharp 3007WFP",
                    "manu": "Dell, Inc.",
                    "manu_id_s": "dell",
                    "cat": [
                      "electronics and computer1"
                    ],
                    "features": [
                      "30\" TFT active matrix LCD, 2560 x 1600, .25mm dot pitch, 700:1 contrast"
                    ],
                    "includes": "USB cable",
                    "weight": 401.6,
                    "price": 2199,
                    "price_c": "2199,USD",
                    "popularity": 6,
                    "inStock": true,
                    "store": "43.17614,-90.57341",
                    "_version_": 1486960637584081000
                  }
                ]
              }

### <a name="using-hello-solr-dashboard"></a>Usando o painel de Solr Olá

Painel de Solr Olá é uma interface que permite que você toowork com Solr através do seu navegador da web. Painel de Solr Olá não seja exposto diretamente no Olá da Internet do seu cluster HDInsight. Você pode usar um tooaccess de túnel SSH-lo. Para obter mais informações sobre o uso de um túnel SSH, consulte Olá [usar SSH de encapsulamento HDInsight](hdinsight-linux-ambari-ssh-tunnel.md) documento.

Depois de estabelecer um túnel SSH, use Olá painel de Solr de saudação de toouse etapas a seguir:

1. Determine o nome do host de saudação para um nó principal do hello primário:

   1. Use o nó principal do cluster SSH tooconnect toohello. Por exemplo: `ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net`.

       Para obter mais informações sobre como usar SSH, consulte Olá [usar SSH com HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

   2. Use Olá tooget Olá nome de host totalmente qualificado do comando a seguir:

        ```bash
        hostname -f
        ```

        Este comando retorna um toohello semelhante valor após o nome do host:

            hn0-myhdi-nfebtpfdv1nubcidphpap2eq2b.ex.internal.cloudapp.net

        Salve o valor de saudação retornado, pois ele é usado mais tarde.

2. No seu navegador, conecte-se muito**solr/http://HOSTNAME:8983 / #/**, onde **HOSTNAME** é Olá nome determinado nas etapas anteriores hello.

    Olá solicitação é encaminhada por meio de saudação SSH túnel toohello Solr interface da web em seu cluster. Olá aparecerá semelhante toohello imagem a seguir:

    ![Imagem do painel do Solr](./media/hdinsight-hadoop-solr-install-linux/solrdashboard.png)

3. No painel esquerdo do hello, use Olá **Core seletor** suspensa tooselect **collection1**. Várias entradas deverão aparecer abaixo de **collection1**.

4. Entradas de saudação abaixo **collection1**, selecione **consulta**. Use Olá página de pesquisa de saudação de toopopulate valores a seguir:

   * Em Olá **p** texto, digite  **\*:**\*. Essa consulta retorna todos os documentos de saudação que são indexados em Solr. Se você quiser toosearch para uma cadeia de caracteres específica dentro de documentos hello, você pode inserir essa cadeia de caracteres aqui.
   * Em Olá **wt** caixa de texto, selecione Olá formato de saída. O padrão é **json**.

     Por fim, selecione Olá **executar consulta** botão na parte inferior de saudação do e de pesquisa de saudação.

     ![Use a ação de Script toocustomize um cluster](./media/hdinsight-hadoop-solr-install-linux/hdi-solr-dashboard-query.png)

     saída de Hello retorna Olá dois documentos que você adicionou toohello índice anteriormente. saudação de saída é similar toohello documento JSON a seguir:

           "response": {
               "numFound": 2,
               "start": 0,
               "maxScore": 1,
               "docs": [
                 {
                   "id": "SOLR1000",
                   "name": "Solr, hello Enterprise Search Server",
                   "manu": "Apache Software Foundation",
                   "cat": [
                     "software",
                     "search"
                   ],
                   "features": [
                     "Advanced Full-Text Search Capabilities using Lucene",
                     "Optimized for High Volume Web Traffic",
                     "Standards Based Open Interfaces - XML and HTTP",
                     "Comprehensive HTML Administration Interfaces",
                     "Scalability - Efficient Replication tooother Solr Search Servers",
                     "Flexible and Adaptable with XML configuration and Schema",
                     "Good unicode support: héllo (hello with an accent over hello e)"
                   ],
                   "price": 0,
                   "price_c": "0,USD",
                   "popularity": 10,
                   "inStock": true,
                   "incubationdate_dt": "2006-01-17T00:00:00Z",
                   "_version_": 1486960636996878300
                 },
                 {
                   "id": "3007WFP",
                   "name": "Dell Widescreen UltraSharp 3007WFP",
                   "manu": "Dell, Inc.",
                   "manu_id_s": "dell",
                   "cat": [
                     "electronics and computer1"
                   ],
                   "features": [
                     "30\" TFT active matrix LCD, 2560 x 1600, .25mm dot pitch, 700:1 contrast"
                   ],
                   "includes": "USB cable",
                   "weight": 401.6,
                   "price": 2199,
                   "price_c": "2199,USD",
                   "popularity": 6,
                   "inStock": true,
                   "store": "43.17614,-90.57341",
                   "_version_": 1486960637584081000
                 }
               ]
             }

### <a name="starting-and-stopping-solr"></a>Iniciando e parando o Solr

Use Olá toomanually parar e iniciar Solr de comandos a seguir:

```bash
sudo stop solr
sudo start solr
```

## <a name="backup-indexed-data"></a>Backup de dados indexados

Use Olá etapas tooback o armazenamento do Solr dados toohello padrão para o cluster a seguir:

1. Conectar-se o cluster toohello usando SSH, use Olá após o nome de host do comando tooget Olá para o nó principal hello:

    ```bash
    hostname -f
    ```

2. Use Olá comando toocreate um instantâneo dos dados indexado de saudação a seguir. Substituir **HOSTNAME** com nome hello retornado pelo comando anterior hello:

    ```bash
    curl http://HOSTNAME:8983/solr/replication?command=backup
    ```

    resposta de saudação é semelhante toohello XML a seguir:

        <?xml version="1.0" encoding="UTF-8"?>
        <response>
          <lst name="responseHeader">
            <int name="status">0</int>
            <int name="QTime">9</int>
          </lst>
          <str name="status">OK</str>
        </response>

3. Altere os diretórios muito`/usr/hdp/current/solr/example/solr`. Há um subdiretório aqui para cada coleção. O diretório de cada coleção contém um `data` diretório que contém o instantâneo Olá para coleção hello.

4. toocreate um arquivo compactado de pasta de instantâneo de Olá Olá use comandos a seguir:

    ```bash
    tar -zcf snapshot.20150806185338855.tgz snapshot.20150806185338855
    ```

    Substituir saudação `snapshot.20150806185338855` valores com o nome de saudação do instantâneo Olá para sua coleção.

    Este comando cria um arquivo chamado **snapshot.20150806185338855.tgz**, que contém o conteúdo de saudação do hello **snapshot.20150806185338855** directory.

5. Em seguida, você pode armazenar o armazenamento primário do cluster de toohello arquivo hello, usando o comando a seguir de saudação:

    ```bash
    hdfs dfs -put snapshot.20150806185338855.tgz /example/data
    ```

Para obter mais informações sobre como trabalhar com backups e restaurações do Solr, consulte [https://cwiki.apache.org/confluence/display/solr/Making+and+Restoring+Backups](https://cwiki.apache.org/confluence/display/solr/Making+and+Restoring+Backups).

## <a name="next-steps"></a>Próximas etapas

* [Instalar o Giraph em clusters HDInsight](hdinsight-hadoop-giraph-install-linux.md). Use cluster personalização tooinstall que giraph no Hadoop de HDInsight clusters. Giraph permite gráfico tooperform processamento usando Hadoop e pode ser usado com o Azure HDInsight.

* [Instalar matiz em clusters HDInsight](hdinsight-hadoop-hue-linux.md). Use o matiz de tooinstall de personalização de cluster em clusters de HDInsight Hadoop. O matiz é que um conjunto de aplicativos da Web usado toointeract com um cluster Hadoop.

[hdinsight-cluster-customize]: hdinsight-hadoop-customize-cluster-linux.md
