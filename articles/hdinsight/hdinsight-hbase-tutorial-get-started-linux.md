---
title: aaaGet iniciada com um exemplo de HBase em HDInsight - Azure | Microsoft Docs
description: "Siga este toostart de exemplo Apache HBase com hadoop no HDInsight. Criar tabelas de saudação shell do HBase e consultá-los usando o Hive."
keywords: exemplo hbasecommand,hbase
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 4d6a2658-6b19-4268-95ee-822890f5a33a
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/17/2017
ms.author: jgao
ms.openlocfilehash: 43419780142b320b16180a2b1f25020dee2f7a11
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-an-apache-hbase-example-in-hdinsight"></a>Introdução a um exemplo do Apache HBase no HDInsight

Saiba como toocreate um cluster HBase em HDInsight, criar tabelas HBase e consultar tabelas usando o Hive. Para obter informações gerais do HBase, confira [Visão geral do HBase do HDInsight][hdinsight-hbase-overview].

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="prerequisites"></a>Pré-requisitos
Antes de tentar Este exemplo HBase, você deve ter Olá itens a seguir:

* **Uma assinatura do Azure**. Consulte [Obter avaliação gratuita do Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).
* [Secure Shell(SSH)](hdinsight-hadoop-linux-use-ssh-unix.md). 
* [curl](http://curl.haxx.se/download.html).

## <a name="create-hbase-cluster"></a>Nome do cluster HBase
Olá procedimento a seguir usa um toocreate de modelo do Gerenciador de recursos do Azure um versão 3.4 baseados em Linux HBase cluster e hello dependentes armazenamento do Azure conta padrão. parâmetros de saudação toounderstand usados no procedimento de saudação e outros métodos de criação de cluster, consulte [Hadoop baseado em Linux criar clusters de HDInsight](hdinsight-hadoop-provision-linux-clusters.md).

1. Clique em Olá seguindo o modelo de saudação tooopen imagem em Olá portal do Azure. Olá modelo está localizado em um contêiner de blob público. 
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-hbase-linux%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-hbase-tutorial-get-started-linux/deploy-to-azure.png" alt="Deploy tooAzure"></a>
2. De saudação **implantação personalizada** folha, digite Olá valores a seguir:
   
   * **Assinatura**: selecione sua assinatura do Azure que é usado toocreate Olá cluster.
   * **Grupo de recursos**: Crie um grupo de Gerenciamento de Recursos do Azure ou use um existente.
   * **Local**: especificar local de Olá Olá do grupo de recursos. 
   * **ClusterName**: insira um nome para o cluster do HBase hello.
   * **Nome de logon e senha do cluster**: nome de logon padrão Olá é **admin**.
   * **SSH username e password**: nome de usuário saudação padrão é **sshuser**.  Você pode renomeá-lo.
     
     Outros parâmetros são opcionais.  
     
     Cada cluster tem uma dependência de conta de Armazenamento do Azure. Depois de excluir um cluster, dados saudação retém na conta de armazenamento hello. nome da conta de armazenamento para o cluster padrão de saudação é o nome de cluster de saudação com "store" acrescentada. Ele é codificado na seção de variáveis de modelo de saudação.
3. Selecione **concordo toohello termos e condições declaradas acima**e, em seguida, clique em **compra**. Demora cerca de 20 minutos toocreate um cluster.

> [!NOTE]
> Depois que um cluster HBase for excluído, você pode criar outro cluster HBase usando Olá mesmo contêiner de blob padrão. cluster novo Olá seleciona tabelas de HBase Olá criado no cluster original hello. tooavoid inconsistências, recomendamos que você desabilite a tabelas do hello HBase antes de excluir o cluster de saudação.
> 
> 

## <a name="create-tables-and-insert-data"></a>Criar tabelas e inserir dados
Você pode usar SSH tooconnect tooHBase clusters e, em seguida, usar tabelas do Shell do HBase toocreate HBase, inserir dados e consultar dados. Para obter mais informações, confira [Usar SSH com HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

Para a maioria das pessoas, os dados aparecem em um formato tabular hello:

![dados tabulares do HBase HDInsight][img-hbase-sample-data-tabular]

No HBase (uma implementação de BigTable), hello mesmo dados parece com:

![Dados BigTable do HBase HDInsight][img-hbase-sample-data-bigtable]


**Olá toouse shell do HBase**

1. SSH, execute Olá HBase comando a seguir:
   
    ```bash
    hbase shell
    ```

2. Crie um HBase com famílias de duas colunas:

    ```hbaseshell   
    create 'Contacts', 'Personal', 'Office'
    list
    ```
3. Insira alguns dados:
    
    ```hbaseshell   
    put 'Contacts', '1000', 'Personal:Name', 'John Dole'
    put 'Contacts', '1000', 'Personal:Phone', '1-425-000-0001'
    put 'Contacts', '1000', 'Office:Phone', '1-425-000-0002'
    put 'Contacts', '1000', 'Office:Address', '1111 San Gabriel Dr.'
    scan 'Contacts'
    ```
   
    ![Shell do HBase do Hadoop HDInsight][img-hbase-shell]
4. Obter uma única linha
   
    ```hbaseshell
    get 'Contacts', '1000'
    ```
   
    Você deverá ver Olá mesmos resultados usando o comando de verificação de saudação porque há apenas uma linha.
   
    Para obter mais informações sobre o esquema de tabela do HBase hello, consulte [tooHBase Introdução Design de esquema][hbase-schema]. Para obter mais comandos HBase, confira [Guia de referência do Apache HBase][hbase-quick-start].
5. Saída Olá shell
   
    ```hbaseshell
    exit
    ```

**toobulk carregar dados em tabela do HBase Olá contatos**

O HBase inclui vários métodos de carregamento de dados em tabelas.  Para obter mais informações, consulte [Carregamento em massa](http://hbase.apache.org/book.html#arch.bulk.load).

Um arquivo de dados de exemplo pode ser encontrado em um contêiner de blobs público, *wasb://hbasecontacts@hditutorialdata.blob.core.windows.net/contacts.txt*.  conteúdo Olá Olá do arquivo de dados é:

    8396    Calvin Raji      230-555-0191    230-555-0191    5415 San Gabriel Dr.
    16600   Karen Wu         646-555-0113    230-555-0192    9265 La Paz
    4324    Karl Xie         508-555-0163    230-555-0193    4912 La Vuelta
    16891   Jonn Jackson     674-555-0110    230-555-0194    40 Ellis St.
    3273    Miguel Miller    397-555-0155    230-555-0195    6696 Anchor Drive
    3588    Osa Agbonile     592-555-0152    230-555-0196    1873 Lion Circle
    10272   Julia Lee        870-555-0110    230-555-0197    3148 Rose Street
    4868    Jose Hayes       599-555-0171    230-555-0198    793 Crawford Street
    4761    Caleb Alexander  670-555-0141    230-555-0199    4775 Kentucky Dr.
    16443   Terry Chander    998-555-0171    230-555-0200    771 Northridge Drive

Opcionalmente, você pode criar um arquivo de texto e carregar a conta de armazenamento do próprio hello arquivos tooyour. Para obter instruções hello, consulte [carregar dados para trabalhos de Hadoop no HDInsight][hdinsight-upload-data].

> [!NOTE]
> Esse procedimento usa a tabela do HBase contatos Olá que você criou no procedimento última Olá.
> 

1. SSH, execute Olá Olá de tootransform comando tooStoreFiles de arquivo de dados e armazenam em um caminho relativo especificado pelo Dimporttsv.bulk.output a seguir.  Se você estiver no Shell do HBase, use Olá tooexit de comando de saída.

    ```bash   
    hbase org.apache.hadoop.hbase.mapreduce.ImportTsv -Dimporttsv.columns="HBASE_ROW_KEY,Personal:Name,Personal:Phone,Office:Phone,Office:Address" -Dimporttsv.bulk.output="/example/data/storeDataFileOutput" Contacts wasb://hbasecontacts@hditutorialdata.blob.core.windows.net/contacts.txt
    ```

2. Execute Olá seguindo os dados de saudação do comando tooupload da tabela do HBase toohello /example/data/storeDataFileOutput:
   
    ```bash
    hbase org.apache.hadoop.hbase.mapreduce.LoadIncrementalHFiles /example/data/storeDataFileOutput Contacts
    ```

3. Você pode abrir Olá shell do HBase e usar o conteúdo da tabela Olá verificação comando toolist hello.

## <a name="use-hive-tooquery-hbase"></a>Use a seção tooquery HBase

Você pode consultar os dados nas tabelas HBase usando o Hive. Nesta seção, você cria uma tabela Hive que mapeia a tabela do HBase toohello e usa dados de saudação tooquery em sua tabela do HBase.

1. Abra **PuTTY**e conecte-se o cluster toohello.  Consulte as instruções de saudação no procedimento anterior hello.
2. Da sessão SSH hello, use Olá comando toostart Beeline a seguir:

    ```bash
    beeline -u 'jdbc:hive2://localhost:10001/;transportMode=http' -n admin
    ```

    Para saber mais sobre o Beeline, consulte [Usar o Hive com Hadoop no HDInsight com Beeline](hdinsight-hadoop-use-hive-beeline.md).
       
3. Execute Olá HiveQL toocreate de script a seguir em uma tabela de Hive que vincula a tabela do HBase toohello. Certifique-se de que você criou a tabela de exemplo hello citada anteriormente neste tutorial, usando o shell do HBase Olá antes de executar essa instrução.

    ```hiveql   
    CREATE EXTERNAL TABLE hbasecontacts(rowkey STRING, name STRING, homephone STRING, officephone STRING, officeaddress STRING)
    STORED BY 'org.apache.hadoop.hive.hbase.HBaseStorageHandler'
    WITH SERDEPROPERTIES ('hbase.columns.mapping' = ':key,Personal:Name,Personal:Phone,Office:Phone,Office:Address')
    TBLPROPERTIES ('hbase.table.name' = 'Contacts');
    ```

4. Execute Olá HiveQL script tooquery Olá dados Olá HBase tabela a seguir:

    ```hiveql   
    SELECT count(rowkey) FROM hbasecontacts;
    ```

## <a name="use-hbase-rest-apis-using-curl"></a>Usar APIs de REST do HBase usando Curl

Olá API REST é protegida por meio de [autenticação básica](http://en.wikipedia.org/wiki/Basic_access_authentication). Você sempre deve fazer solicitações usando Secure HTTP (HTTPS) toohelp Certifique-se de que suas credenciais são enviadas com segurança toohello server.

2. Use Olá comando toolist Olá HBase as tabelas existentes a seguir:

    ```bash
    curl -u <UserName>:<Password> \
    -G https://<ClusterName>.azurehdinsight.net/hbaserest/
    ```

3. Use Olá comando toocreate uma nova tabela do HBase com as famílias de duas colunas a seguir:

    ```bash   
    curl -u <UserName>:<Password> \
    -X PUT "https://<ClusterName>.azurehdinsight.net/hbaserest/Contacts1/schema" \
    -H "Accept: application/json" \
    -H "Content-Type: application/json" \
    -d "{\"@name\":\"Contact1\",\"ColumnSchema\":[{\"name\":\"Personal\"},{\"name\":\"Office\"}]}" \
    -v
    ```

    esquema de saudação é fornecida no formato JSon de saudação.
4. Use Olá tooinsert de comando a seguir alguns dados:

    ```bash   
    curl -u <UserName>:<Password> \
    -X PUT "https://<ClusterName>.azurehdinsight.net/hbaserest/Contacts1/false-row-key" \
    -H "Accept: application/json" \
    -H "Content-Type: application/json" \
    -d "{\"Row\":[{\"key\":\"MTAwMA==\",\"Cell\": [{\"column\":\"UGVyc29uYWw6TmFtZQ==\", \"$\":\"Sm9obiBEb2xl\"}]}]}" \
    -v
    ```
   
    Você deve base64 codificar valores hello especificados na opção -d hello. No exemplo hello:
   
   * MTAwMA==: 1000
   * UGVyc29uYWw6TmFtZQ==: Personal:Name
   * Sm9obiBEb2xl: John Dole
     
     [chave de linha False](https://hbase.apache.org/apidocs/org/apache/hadoop/hbase/rest/package-summary.html#operation_cell_store_single) tooinsert permite vários valores (em lotes).
5. Use Olá comando tooget uma linha a seguir:
   
    ```bash 
    curl -u <UserName>:<Password> \
    -X GET "https://<ClusterName>.azurehdinsight.net/hbaserest/Contacts1/1000" \
    -H "Accept: application/json" \
    -v
    ```

Para saber mais sobre o Rest HBase, veja [Guia de referência do Apache HBase](https://hbase.apache.org/book.html#_rest).

> [!NOTE]
> Não há suporte para thrift pelo HBase no HDInsight.
>
> Ondulação ou com qualquer outra comunicação REST WebHCat, você deve autenticar solicitações de saudação fornecendo Olá nome e a senha de administrador de cluster do HDInsight hello. Você também deve usar o nome do cluster hello como parte do identificador de recurso uniforme (URI) do hello usado server de toohello toosend Olá solicitações:
> 
>   
>        curl -u <UserName>:<Password> \
>        -G https://<ClusterName>.azurehdinsight.net/templeton/v1/status
>   
>    Você deve receber um toohello semelhante resposta resposta a seguir:
>   
>        {"status":"ok","version":"v1"}
   


## <a name="check-cluster-status"></a>Verificar o status do cluster
O HBase em HDInsight é fornecido com uma interface do usuário da Web para monitorar clusters. Olá IU da Web pode solicitar informações sobre regiões ou estatísticas.

**Olá tooaccess HBase mestre UI**

1. O logon no Olá Olá Ambari Web UI no https://&lt;Clustername >. n e t.
2. Clique em **HBase** no menu esquerdo hello.
3. Clique em **links rápidos** Olá superior da página hello, o link de nó ativo em Zookeeper toohello ponto e, em seguida, clique em **HBase mestre UI**.  Saudação da interface do usuário é aberta em outra guia do navegador:

  ![Interface do Usuário HDInsight HBase HMaster](./media/hdinsight-hbase-tutorial-get-started-linux/hdinsight-hbase-hmaster-ui.png)

  Olá UI HBase mestre contém Olá seções a seguir:

  - servidores de região
  - mestres de backup
  - tables
  - tarefas
  - atributos de software

## <a name="delete-hello-cluster"></a>Excluir o cluster Olá
tooavoid inconsistências, recomendamos que você desabilite a tabelas do hello HBase antes de excluir o cluster de saudação.

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="troubleshoot"></a>Solucionar problemas

Se você tiver problemas com a criação de clusters HDInsight, confira os [requisitos de controle de acesso](hdinsight-administer-use-portal-linux.md#create-clusters).

## <a name="next-steps"></a>Próximas etapas
Neste artigo, você aprendeu como toocreate um cluster HBase e como o modo de exibição e tabelas toocreate Olá dados nessas tabelas de Olá shell do HBase. Você também aprendeu como toouse uma seção de consulta em dados em HBase tabelas e como toouse Olá APIs de REST do HBase c# toocreate uma tabela do HBase e recuperar dados da tabela de saudação.

toolearn mais, consulte:

* [Visão geral do HBase do HDInsight][hdinsight-hbase-overview]: o HBase é um banco de dados NoSQL de software livre Apache baseado no Hadoop que fornece acesso aleatório e uma sólida consistência para grandes quantidades de dados não estruturados e semiestruturados.

[hdinsight-manage-portal]: hdinsight-administer-use-management-portal.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hbase-reference]: http://hbase.apache.org/book.html#importtsv
[hbase-schema]: http://0b4af6cdc2f0c5998459-c0245c5c937c5dedcca3f1764ecc9b2f.r43.cf2.rackcdn.com/9353-login1210_khurana.pdf
[hbase-quick-start]: http://hbase.apache.org/book.html#quickstart





[hdinsight-hbase-overview]: hdinsight-hbase-overview.md
[hdinsight-hbase-provision-vnet]: hdinsight-hbase-provision-vnet.md
[hdinsight-versions]: hdinsight-component-versioning.md
[hbase-twitter-sentiment]: hdinsight-hbase-analyze-twitter-sentiment.md
[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[azure-portal]: https://portal.azure.com/
[azure-create-storageaccount]: http://azure.microsoft.com/documentation/articles/storage-create-storage-account/

[img-hdinsight-hbase-cluster-quick-create]: ./media/hdinsight-hbase-tutorial-get-started-linux/hdinsight-hbase-quick-create.png
[img-hdinsight-hbase-hive-editor]: ./media/hdinsight-hbase-tutorial-get-started-linux/hdinsight-hbase-hive-editor.png
[img-hdinsight-hbase-file-browser]: ./media/hdinsight-hbase-tutorial-get-started-linux/hdinsight-hbase-file-browser.png
[img-hbase-shell]: ./media/hdinsight-hbase-tutorial-get-started-linux/hdinsight-hbase-shell.png
[img-hbase-sample-data-tabular]: ./media/hdinsight-hbase-tutorial-get-started-linux/hdinsight-hbase-contacts-tabular.png
[img-hbase-sample-data-bigtable]: ./media/hdinsight-hbase-tutorial-get-started-linux/hdinsight-hbase-contacts-bigtable.png
