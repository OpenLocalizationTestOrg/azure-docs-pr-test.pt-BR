---
title: fluxos de trabalho do aaaUse Oozie Hadoop em HDInsight baseados em Linux | Microsoft Docs
description: Usar o Oozie do Hadoop no HDInsight baseado em Linux. Saiba como toodefine um fluxo de trabalho do Oozie e enviar um trabalho de Oozie.
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: d7603471-5076-43d1-8b9a-dbc4e366ce5d
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/04/2017
ms.author: larryfr
ms.openlocfilehash: cb5682837543312621e3424b7a9341b5d2a00bf8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-oozie-with-hadoop-toodefine-and-run-a-workflow-on-linux-based-hdinsight"></a>Usar Oozie com toodefine Hadoop e executar um fluxo de trabalho no HDInsight baseados em Linux

[!INCLUDE [oozie-selector](../../includes/hdinsight-oozie-selector.md)]

Saiba como toouse Apache Oozie com Hadoop no HDInsight. O Apache Oozie é um sistema de fluxo de trabalho/coordenação que gerencia trabalhos do Hadoop. Oozie é integrado com pilha de Hadoop hello e dá suporte a saudação trabalhos a seguir:

* Apache MapReduce
* Apache Pig
* Apache Hive
* Apache Sqoop

Oozie também pode ser tooschedule usado trabalhos que são tooa específicas do sistema, como programas de Java ou scripts de shell

> [!NOTE]
> Outra opção para definir fluxos de trabalho com o HDInsight é uma Azure Data Factory. toolearn mais sobre o Azure Data Factory, consulte [usar o Pig e Hive com a fábrica de dados][azure-data-factory-pig-hive].

> [!IMPORTANT]
> O Oozie não está habilitado no HDInsight ingressado no domínio.

## <a name="prerequisites"></a>Pré-requisitos

* **Um cluster hdinsight**: consulte [Introdução ao HDInsight no Linux](hdinsight-hadoop-linux-tutorial-get-started.md)

  > [!IMPORTANT]
  > etapas de saudação neste documento exigem um cluster HDInsight que usa o Linux. Linux é Olá sistema operacional somente de usado no HDInsight versão 3.4 ou posterior. Para obter mais informações, confira [baixa do HDInsight no Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).

## <a name="example-workflow"></a>Fluxo de trabalho de exemplo

fluxo de trabalho de saudação usado neste documento contém duas ações. Ações são definições de tarefas, como Sqoop, Hive, MapReduce ou outro processo de execução:

![Diagrama de fluxo de trabalho][img-workflow-diagram]

1. Uma ação de Hive executa um script HiveQL tooextract registros de saudação **hivesampletable** incluído no HDInsight. Cada linha de dados descreve uma visita de um dispositivo móvel específico. formato de registro de saudação aparece semelhante toohello texto a seguir:

        8       18:54:20        en-US   Android Samsung SCH-i500        California     United States    13.9204007      0       0
        23      19:19:44        en-US   Android HTC     Incredible      Pennsylvania   United States    NULL    0       0
        23      19:19:46        en-US   Android HTC     Incredible      Pennsylvania   United States    1.4757422       0       1

    Olá usado neste documento de script do Hive contagens de visitas a saudação total para cada plataforma (como Android ou iPhone) e armazena Olá contagens tooa nova seção tabela.

    Para obter mais informações sobre o Hive, consulte [Usar o Hive com o HDInsight][hdinsight-use-hive].

2. Uma ação de Sqoop exporta conteúdo Olá Olá nova tabela tooa tabela Hive em um banco de dados do SQL Azure. Para saber mais sobre o Sqoop, confira [Usar o Hadoop Sqoop com o HDInsight][hdinsight-use-sqoop].

> [!NOTE]
> Para versões com suporte do Oozie em clusters de HDInsight, consulte [Novidades nas versões de cluster de Hadoop Olá fornecidas pelo HDInsight][hdinsight-versions].

## <a name="create-hello-working-directory"></a>Criar o diretório de trabalho Olá

Oozie espera os recursos necessários para um trabalho toobe armazenada no hello mesmo diretório. Este exemplo usa **wasb:///tutorials/useoozie**. Nesse diretório e o diretório de dados de saudação que mantém Olá Hive tabela criada por este fluxo de trabalho, use Olá toocreate de comando a seguir:

```
hdfs dfs -mkdir -p /tutorials/useoozie/data
```

> [!NOTE]
> Olá `-p` parâmetro faz com que todos os diretórios no hello caminho toobe criado. Olá **dados** diretório é toohold usado dados usados por Olá **useooziewf.hql** script.

Também execute Olá comando, o que garante que Oozie pode representar a conta de usuário ao executar trabalhos de Hive e Sqoop a seguir. Substitua **NOME DE USUÁRIO** pelo seu nome de logon:

```
sudo adduser USERNAME users
```

> [!NOTE]
> Você pode ignorar erros que o usuário Olá já é um membro de saudação `users` grupo.

## <a name="add-a-database-driver"></a>Adicionar um driver de banco de dados

Como esse fluxo de trabalho usa Sqoop tooexport dados tooSQL banco de dados, você deve fornecer que uma cópia do driver JDBC Olá usado tootalk tooSQL banco de dados. Use Olá após o comando toocopy-toohello diretório de trabalho:

```
hdfs dfs -put /usr/share/java/sqljdbc_4.1/enu/sqljdbc*.jar /tutorials/useoozie/
```

Se o fluxo de trabalho usados outros recursos, como um jar que contém um aplicativo de MapReduce, você precisaria tooadd esses recursos também.

## <a name="define-hello-hive-query"></a>Definir a consulta de Hive Olá

Use Olá seguindo as etapas toocreate um script de estilo que define uma consulta, que é usada em um fluxo de trabalho do Oozie neste documento.

1. Conecte-se toohello cluster usando o SSH. Olá, comando a seguir é um exemplo de como usar o hello `ssh` comando. Substituir __nome de usuário__ com usuário SSH Olá cluster hello. Substituir __CLUSTERNAME__ com o nome de saudação do cluster do HDInsight hello.

    ```
    ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
    ```

    Para obter mais informações, confira [Usar SSH com HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

2. De Olá conexão SSH, use Olá comando toocreate um arquivo a seguir:

    ```
    nano useooziewf.hql
    ```

3. Depois de saudação nano editor é aberto, use Olá consulta a seguir como conteúdo de saudação do arquivo hello:

    ```hiveql
    DROP TABLE ${hiveTableName};
    CREATE EXTERNAL TABLE ${hiveTableName}(deviceplatform string, count string) ROW FORMAT DELIMITED
    FIELDS TERMINATED BY '\t' STORED AS TEXTFILE LOCATION '${hiveDataFolder}';
    INSERT OVERWRITE TABLE ${hiveTableName} SELECT deviceplatform, COUNT(*) as count FROM hivesampletable GROUP BY deviceplatform;
    ```

    Há duas variáveis usadas em script hello:

    * **${hiveTableName}**: contém nome de saudação do hello tabela toobe criado

    * **${hiveDataFolder}**: contém arquivos de dados de Olá Olá local toostore para tabela Olá

    arquivo de definição de fluxo de trabalho (. XML neste tutorial) Olá passa esses valores toothis script HiveQL em tempo de execução

4. editor de saudação tooexit, pressione Ctrl-X. Quando solicitado, selecione **Y** toosave Olá arquivo, em seguida, usar **Enter** toouse Olá **useooziewf.hql** nome de arquivo.

5. A seguir Olá use comandos toocopy **useooziewf.hql** muito**wasb:///tutorials/useoozie/useooziewf.hql**:

    ```
    hdfs dfs -put useooziewf.hql /tutorials/useoozie/useooziewf.hql
    ```

    Esses comandos armazenam Olá **useooziewf.hql** no arquivo em armazenamento Olá HDFS compatível com cluster hello.

## <a name="define-hello-workflow"></a>Definir o fluxo de trabalho Olá

As definições de fluxos de trabalho do Oozie são escritas em hPDL (uma Linguagem de Definição de Processo XML). Use Olá fluxo de trabalho de saudação de toodefine as etapas a seguir:

1. Use Olá toocreate instrução a seguir e editar um arquivo novo:

    ```
    nano workflow.xml
    ```

2. Uma vez Olá nano editor é aberta, digite Olá XML a seguir como o conteúdo do arquivo hello:

    ```xml
    <workflow-app name="useooziewf" xmlns="uri:oozie:workflow:0.2">
        <start too= "RunHiveScript"/>
        <action name="RunHiveScript">
        <hive xmlns="uri:oozie:hive-action:0.2">
            <job-tracker>${jobTracker}</job-tracker>
            <name-node>${nameNode}</name-node>
            <configuration>
            <property>
                <name>mapred.job.queue.name</name>
                <value>${queueName}</value>
            </property>
            </configuration>
            <script>${hiveScript}</script>
            <param>hiveTableName=${hiveTableName}</param>
            <param>hiveDataFolder=${hiveDataFolder}</param>
        </hive>
        <ok to="RunSqoopExport"/>
        <error to="fail"/>
        </action>
        <action name="RunSqoopExport">
        <sqoop xmlns="uri:oozie:sqoop-action:0.2">
            <job-tracker>${jobTracker}</job-tracker>
            <name-node>${nameNode}</name-node>
            <configuration>
            <property>
                <name>mapred.compress.map.output</name>
                <value>true</value>
            </property>
            </configuration>
            <arg>export</arg>
            <arg>--connect</arg>
            <arg>${sqlDatabaseConnectionString}</arg>
            <arg>--table</arg>
            <arg>${sqlDatabaseTableName}</arg>
            <arg>--export-dir</arg>
            <arg>${hiveDataFolder}</arg>
            <arg>-m</arg>
            <arg>1</arg>
            <arg>--input-fields-terminated-by</arg>
            <arg>"\t"</arg>
            <archive>sqljdbc41.jar</archive>
            </sqoop>
        <ok to="end"/>
        <error to="fail"/>
        </action>
        <kill name="fail">
        <message>Job failed, error message[${wf:errorMessage(wf:lastErrorNode())}] </message>
        </kill>
        <end name="end"/>
    </workflow-app>
    ```

    Há duas ações definidas no fluxo de trabalho hello:

   * **RunHiveScript**: essa ação é Olá iniciar ação e executa Olá **useooziewf.hql** script de Hive

   * **RunSqoopExport**: essa ação exporta dados de saudação criados a partir de tooSQL de script de Hive hello usando Sqoop de banco de dados. Esta ação é executada somente se hello **RunHiveScript** ação foi bem-sucedida.

     fluxo de trabalho Olá tem várias entradas, como `${jobTracker}`. Essas entradas são substituídas por valores usados na definição de trabalho hello. definição de trabalho Olá é criada neste documento.

     Saudação de Observação também `<archive>sqljdbc4.jar</arcive>` entrada hello Sqoop seção. Essa entrada instrui Oozie toomake neste arquivo disponível para Sqoop quando esta ação é executada.

3. Use Ctrl-X, em seguida, **Y** e **Enter** toosave arquivo de saudação.

4. Olá toocopy do comando de uso a seguir de saudação **. XML** arquivo muito**/tutorials/useoozie/workflow.xml**:

    ```
    hdfs dfs -put workflow.xml /tutorials/useoozie/workflow.xml
    ```

## <a name="create-hello-database"></a>Criar banco de dados de saudação

toocreate um banco de dados SQL do Azure, siga as etapas de Olá Olá [criar um banco de dados SQL](../sql-database/sql-database-get-started.md) documento. Ao criar o banco de dados hello, use `oozietest` como nome do banco de dados de saudação. Também faça uma anotação de nome de saudação do servidor de banco de dados de saudação.

### <a name="create-hello-table"></a>Criar tabela Olá

> [!NOTE]
> Há muitas maneiras tooconnect tooSQL banco de dados toocreate uma tabela. Olá use as etapas a seguir [FreeTDS](http://www.freetds.org/) do cluster do HDInsight hello.


1. Use Olá após o comando tooinstall FreeTDS no cluster do HDInsight hello:

    ```
    sudo apt-get --assume-yes install freetds-dev freetds-bin
    ```

2. Depois de FreeTDS tiver sido instalado, use Olá após o servidor de banco de dados SQL do comando tooconnect toohello criado anteriormente:

    ```
    TDSVER=8.0 tsql -H <serverName>.database.windows.net -U <sqlLogin> -P <sqlPassword> -p 1433 -D oozietest
    ```

    Você receberá a saída toohello semelhante texto a seguir:

        locale is "en_US.UTF-8"
        locale charset is "UTF-8"
        using default charset "UTF-8"
        Default database being set toooozietest
        1>

3. Em Olá `1>` prompt, digite Olá linhas seguintes:

    ```
    CREATE TABLE [dbo].[mobiledata](
    [deviceplatform] [nvarchar](50),
    [count] [bigint])
    GO
    CREATE CLUSTERED INDEX mobiledata_clustered_index on mobiledata(deviceplatform)
    GO
    ```

    Olá quando `GO` instrução for inserida, instruções de saudação anterior são avaliadas. Essas instruções criam uma tabela chamada **mobiledata** que é usada pelo fluxo de trabalho de saudação.

    Saudação de uso tooverify que Olá a tabela a seguir foi criada:

    ```
    SELECT * FROM information_schema.tables
    GO
    ```

    Você verá a saída toohello semelhante texto a seguir:

    ```
    TABLE_CATALOG   TABLE_SCHEMA    TABLE_NAME      TABLE_TYPE
    oozietest       dbo     mobiledata      BASE TABLE
    ```

4. Digite `exit` em Olá `1>` tooexit Olá tsql utilitário do prompt.

## <a name="create-hello-job-definition"></a>Criar definição de trabalho Olá

definição de trabalho Olá descreve onde toofind hello. XML. Ele também descreve onde toofind outros arquivos usados pelo fluxo de trabalho de saudação (como useooziewf.hql). Ele também define os valores de saudação para as propriedades usadas em fluxo de trabalho hello e os arquivos associados.

1. Use Olá endereço completo do comando tooget Olá de armazenamento padrão da saudação a seguir. Este endereço é usado no arquivo de configuração de saudação em breve:

    ```
    sed -n '/<name>fs.default/,/<\/value>/p' /etc/hadoop/conf/core-site.xml
    ```

    Esse comando retorna informações toohello semelhante XML a seguir:

    ```xml
    <name>fs.defaultFS</name>
    <value>wasb://mycontainer@mystorageaccount.blob.core.windows.net</value>
    ```

    > [!NOTE]
    > Se o cluster do HDInsight Olá usa o armazenamento do Azure como armazenamento padrão da saudação, Olá `<value>` conteúdo de elemento começa com `wasb://`. Se o Azure Data Lake Store é usado, ele começa com `adl://`.

    Salvar o conteúdo de saudação do hello `<value>` elemento, como ele é usado em providências hello.

2. Use Olá comando tooget FQDN do nó principal do cluster Olá a seguir. Essas informações são usadas para Olá endereço JobTracker para cluster hello:

    ```
    hostname -f
    ```

    Isso retorna informações toohello semelhante texto a seguir:

    ```hn0-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net```

    Olá porta usada para Olá JobTracker está 8050, Olá endereço completo toouse para Olá JobTracker `hn0-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net:8050`.

3. Use Olá configuração de definição de trabalho toocreate Olá Oozie a seguir:

    ```
    nano job.xml
    ```

4. Depois de saudação nano editor é aberto, use Olá XML a seguir como conteúdo de saudação do arquivo hello:

    ```xml
    <?xml version="1.0" encoding="UTF-8"?>
    <configuration>

        <property>
        <name>nameNode</name>
        <value>wasb://mycontainer@mystorageaccount.blob.core.windows.net</value>
        </property>

        <property>
        <name>jobTracker</name>
        <value>JOBTRACKERADDRESS</value>
        </property>

        <property>
        <name>queueName</name>
        <value>default</value>
        </property>

        <property>
        <name>oozie.use.system.libpath</name>
        <value>true</value>
        </property>

        <property>
        <name>hiveScript</name>
        <value>wasb://mycontainer@mystorageaccount.blob.core.windows.net/tutorials/useoozie/useooziewf.hql</value>
        </property>

        <property>
        <name>hiveTableName</name>
        <value>mobilecount</value>
        </property>

        <property>
        <name>hiveDataFolder</name>
        <value>wasb://mycontainer@mystorageaccount.blob.core.windows.net/tutorials/useoozie/data</value>
        </property>

        <property>
        <name>sqlDatabaseConnectionString</name>
        <value>"jdbc:sqlserver://serverName.database.windows.net;user=adminLogin;password=adminPassword;database=oozietest"</value>
        </property>

        <property>
        <name>sqlDatabaseTableName</name>
        <value>mobiledata</value>
        </property>

        <property>
        <name>user.name</name>
        <value>YourName</value>
        </property>

        <property>
        <name>oozie.wf.application.path</name>
        <value>wasb://mycontainer@mystorageaccount.blob.core.windows.net/tutorials/useoozie</value>
        </property>
    </configuration>
    ```

   * Substitua todas as instâncias de  **wasb://mycontainer@mystorageaccount.blob.core.windows.net**  com valor de saudação recebidas anteriormente para armazenamento padrão.

     > [!WARNING]
     > Se o caminho de saudação é um `wasb` caminho, você deve usar o caminho completo da saudação. Não reduzi-lo toojust `wasb:///`.

   * Substituir **JOBTRACKERADDRESS** com hello endereço JobTracker/ResourceManager recebidas anteriormente.
   * Substituir **YourName** com seu nome de logon para o cluster do HDInsight hello.
   * Substituir **serverName**, **adminLogin**, e **adminPassword** com informações de saudação para seu banco de dados do SQL Azure.

     A maioria das informações neste arquivo hello é toopopulate usados valores de saudação usados nos arquivos. XML ou ooziewf.hql de saudação (por exemplo, ${nameNode}.)

     > [!NOTE]
     > Olá **oozie.wf.application.path** entrada define onde toofind hello. XML arquivo que contém o fluxo de trabalho Olá foi executado por esse trabalho.

5. Use Ctrl-X, em seguida, **Y** e **Enter** toosave arquivo de saudação.

## <a name="submit-and-manage-hello-job"></a>Enviar e gerenciar o trabalho de saudação

Hello etapas a seguir usam Olá Oozie comando toosubmit e gerenciar fluxos de trabalho do Oozie no cluster hello. Olá Oozie comando é uma interface amigável sobre Olá [Oozie REST API](https://oozie.apache.org/docs/4.1.0/WebServicesAPI.html).

> [!IMPORTANT]
> Ao usar o comando do hello Oozie, você deve usar Olá FQDN para um nó principal do hello HDInsight. Esse FQDN só está acessível no cluster hello ou se hello cluster estiver em uma rede Virtual do Azure, de outras máquinas Olá mesma rede.


1. Use Olá após tooobtain Olá URL toohello Oozie serviço:

    ```
    sed -n '/<name>oozie.base.url/,/<\/value>/p' /etc/oozie/conf/oozie-site.xml
    ```

    Isso retorna informações toohello semelhante XML a seguir:

    ```xml
    <name>oozie.base.url</name>
    <value>http://hn0-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net:11000/oozie</value>
    ```

    Olá `http://hn0-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net:11000/oozie` parte é Olá URL toouse com hello Oozie comando.

2. Olá Use toocreate uma variável de ambiente a seguir para URL hello, para que você não tenha tootype para cada comando:

    ```
    export OOZIE_URL=http://HOSTNAMEt:11000/oozie
    ```

    Substitua URL Olá Olá um recebidas anteriormente.
3. Use Olá trabalho de saudação toosubmit a seguir:

    ```
    oozie job -config job.xml -submit
    ```

    Esse comando carrega informações de trabalho de saudação do **job.xml** e envia tooOozie, mas não não executá-lo.

    Após a conclusão do comando hello, ele deverá retornar Olá ID do trabalho de saudação. Por exemplo: `0000005-150622124850154-oozie-oozi-W`. Essa ID é um trabalho de saudação toomanage usado.

4. Exibir o status de saudação do trabalho hello usando Olá comando a seguir:

    ```
    oozie job -info <JOBID>
    ```

    > [!NOTE]
    > Substituir `<JOBID>` com hello ID retornado na etapa anterior hello.

    Isso retorna informações toohello semelhante texto a seguir:

    ```
    Job ID : 0000005-150622124850154-oozie-oozi-W
    ------------------------------------------------------------------------------------------------------------------------------------
    Workflow Name : useooziewf
    App Path      : wasb:///tutorials/useoozie
    Status        : PREP
    Run           : 0
    User          : USERNAME
    Group         : -
    Created       : 2015-06-22 15:06 GMT
    Started       : -
    Last Modified : 2015-06-22 15:06 GMT
    Ended         : -
    CoordAction ID: -
    ------------------------------------------------------------------------------------------------------------------------------------
    ```

    Este trabalho tem o status `PREP`. Este status indica que esse trabalho Olá foi criado, mas não foi iniciado.

5. Use Olá trabalho de saudação do toostart de comando a seguir:

    ```
    oozie job -start JOBID
    ```

    > [!NOTE]
    > Substituir `<JOBID>` com hello ID retornado anteriormente.

    Se você verificar o status de saudação após esse comando, ele está em um estado de execução e informações serão retornadas para ações de saudação do trabalho de saudação.

6. Depois de concluir a tarefa de saudação com êxito, você pode verificar se os dados saudação foi gerados e exportado toohello tabela de banco de dados SQL usando Olá comandos a seguir:

    ```
    TDSVER=8.0 tsql -H <serverName>.database.windows.net -U <adminLogin> -P <adminPassword> -p 1433 -D oozietest
    ```

    Em Olá `1>` prompt, digite Olá consulta a seguir:

    ```
    SELECT * FROM mobiledata
    GO
    ```

    informações de Hello retornadas são semelhante toohello texto a seguir:

        deviceplatform  count
        Android 31591
        iPhone OS       22731
        proprietary development 3
        RIM OS  3464
        Unknown 213
        Windows Phone   1791
        (6 rows affected)

Para obter mais informações sobre Olá comando Oozie, consulte [ferramenta de linha de comando do Oozie](https://oozie.apache.org/docs/4.1.0/DG_CommandLineTool.html).

## <a name="oozie-rest-api"></a>API REST do Oozie

Olá Oozie REST API permite que você toobuild suas próprias ferramentas que funcionam com Oozie. Olá seguem HDInsight de informações específicas sobre como usar o hello Oozie REST API:

* **URI**: Olá API REST podem ser acessada de fora cluster Olá em`https://CLUSTERNAME.azurehdinsight.net/oozie`

* **Autenticação**: autenticar toohello API usando a conta de cluster HTTP hello (administrador) e a senha. Por exemplo:

    ```
    curl -u admin:PASSWORD https://CLUSTERNAME.azurehdinsight.net/oozie/versions
    ```

Para obter mais informações sobre como usar o hello Oozie REST API, consulte [API de serviços Web Oozie](https://oozie.apache.org/docs/4.1.0/WebServicesAPI.html).

## <a name="oozie-web-ui"></a>Interface da Web do Oozie

Saudação da interface do usuário do Oozie Web fornece uma visão baseado na web status de saudação do Oozie trabalhos no cluster hello. Interface da web Hello permite Olá tooview informações a seguir:

* Status do trabalho
* Definição de trabalho
* Configuração
* Um gráfico de ações de saudação em trabalho Olá
* Logs para o trabalho de saudação

Você também pode exibir detalhes de ações dentro de um trabalho.

tooaccess Olá a interface do usuário da Web do Oozie, use Olá etapas a seguir:

1. Crie um cluster de HDInsight de toohello de túnel SSH. Para obter informações, consulte Olá [usar SSH de encapsulamento HDInsight](hdinsight-linux-ambari-ssh-tunnel.md) documento.

2. Quando tiver sido criado um túnel, abra Olá Ambari web da interface do usuário no seu navegador da web. Olá URI para o site do Ambari Olá é **https://CLUSTERNAME.azurehdinsight.net**. Substituir **CLUSTERNAME** com nome de saudação do cluster HDInsight baseados em Linux.

3. Olá lado esquerdo da página hello, selecione **Oozie**, em seguida, **Links rápidos**e, finalmente, **Oozie Web UI**.

    ![imagem de menus Olá](./media/hdinsight-use-oozie-linux-mac/ooziewebuisteps.png)

4. Olá padrões de interface do usuário da Web do Oozie toodisplaying trabalhos de fluxo de trabalho em execução. toosee todos os trabalhos de fluxo de trabalho, selecione **todos os trabalhos**.

    ![Todos os trabalhos exibidos](./media/hdinsight-use-oozie-linux-mac/ooziejobs.png)

5. Selecione um trabalho tooview obter mais informações sobre o trabalho de saudação.

    ![Informações do Trabalho](./media/hdinsight-use-oozie-linux-mac/jobinfo.png)

6. Na guia de informações sobre o trabalho Olá, você pode ver informações de trabalho básico e ações individuais de saudação do trabalho de saudação. Usando guias de saudação na parte superior de saudação que você pode exibir Olá definição de trabalho, configuração de trabalho, Olá acesso Log do trabalho ou exibir um direcionado acíclico Graph (DAG) do trabalho de saudação.

   * **Trabalho de Log**: selecione Olá **GetLogs** botão tooget todos os logs de trabalho hello, ou use Olá **inserir o filtro de pesquisa** campo toofilter logs

       ![Log de trabalhos](./media/hdinsight-use-oozie-linux-mac/joblog.png)

   * **JobDAG**: Olá DAG é uma representação gráfica dos caminhos de dados Olá feito por meio do fluxo de trabalho Olá

       ![DAG de trabalho](./media/hdinsight-use-oozie-linux-mac/jobdag.png)

7. Selecionando uma das ações de saudação do hello **informações sobre o trabalho** guia exibe informações de ação de saudação. Por exemplo, selecione Olá **RunHiveScript** ação.

    ![Informações da ação](./media/hdinsight-use-oozie-linux-mac/action.png)

8. Você pode ver detalhes de ação de saudação, como um link toohello **URL do Console**. Esse link pode ser usado tooview JobTracker informações para o trabalho de saudação.

## <a name="scheduling-jobs"></a>Agendamento de trabalhos

coordenador de saudação permite que você toospecify uma frequência de início, fim e ocorrência para trabalhos. toodefine uma agenda para o fluxo de trabalho hello, Olá use as etapas a seguir:

1. Saudação de uso a seguir toocreate um arquivo chamado **coordinator.xml**:

    ```
    nano coordinator.xml
    ```

    Use Olá XML a seguir como conteúdo de saudação do arquivo hello:

    ```xml
    <coordinator-app name="my_coord_app" frequency="${coordFrequency}" start="${coordStart}" end="${coordEnd}" timezone="${coordTimezone}" xmlns="uri:oozie:coordinator:0.4">
        <action>
        <workflow>
            <app-path>${workflowPath}</app-path>
        </workflow>
        </action>
    </coordinator-app>
    ```

    > [!NOTE]
    > Olá `${...}` variáveis são substituídas pelos valores na definição do trabalho de saudação em tempo de execução. Olá variáveis são:
    >
    > * `${coordFrequency}`: Hora entre instâncias do trabalho de saudação de execução.
    > ** `${coordStart}`: hora de início do trabalho de saudação.
    > * `${coordEnd}`: hora de término de trabalho hello.
    > * `${coordTimezone}`: os trabalhos do coordenador estão em um fuso horário fixo sem horário de verão (geralmente representado com o uso do UTC). Este fuso horário é conhecido como hello "Oozie processamento de fuso horário."
    > * `${wfPath}`: Olá. XML toohello de caminho.

2. Olá toosave de arquivo, use Ctrl-X, **Y**, e **Enter**.

3. Use Olá comando toocopy Olá arquivo toohello diretório de trabalho para esse trabalho a seguir:

    ```
    hadoop fs -put coordinator.xml /tutorials/useoozie/coordinator.xml
    ```

4. Olá Use toomodify Olá a seguir **job.xml** arquivo:

    ```
    nano job.xml
    ```

    Verifique Olá as seguintes alterações:

   * arquivo de coordenador de saudação tooinstruct oozie toorun em vez de fluxo de trabalho hello, alteração `<name>oozie.wf.application.path</name>` muito`<name>oozie.coord.application.path</name>`.

   * Olá tooset `workflowPath` variável usada pelo coordenador hello, adicionar Olá XML a seguir:

        ```xml
        <property>
            <name>workflowPath</name>
            <value>wasb://mycontainer@mystorageaccount.blob.core.windows.net/tutorials/useoozie</value>
        </property>
        ```

       Substituir saudação `wasb://mycontainer@mystorageaccount.blob.core.windows` texto com valor de saudação usado em outras entradas no arquivo de job.xml hello.

   * início de saudação toodefine, fim e frequência de coordenador hello, adicionam Olá XML a seguir:

        ```xml
        <property>
            <name>coordStart</name>
            <value>2017-05-10T12:00Z</value>
        </property>

        <property>
            <name>coordEnd</name>
            <value>2017-05-12T12:00Z</value>
        </property>

        <property>
            <name>coordFrequency</name>
            <value>1440</value>
        </property>

        <property>
            <name>coordTimezone</name>
            <value>UTC</value>
        </property>
        ```

       Os valores definidos Olá too12 de hora de início: 00 PM em 10 de maio de 2017, Olá tooMay de hora de término 12, 2017. intervalo de saudação para executar este trabalho diariamente. frequência de saudação é em minutos, até 24 horas x 60 minutos = 1440 minutos. Por fim, o fuso horário de saudação é definido tooUTC.

5. Use Ctrl-X, em seguida, **Y** e **Enter** toosave arquivo de saudação.

6. trabalho de saudação toorun, use Olá comando a seguir:

    ```
    oozie job -config job.xml -run
    ```

    Esse comando envia e inicia o trabalho de saudação.

7. Se você visitar Olá Oozie Web UI e selecionar Olá **trabalhos do coordenador** guia, você verá informações toohello semelhante imagem a seguir:

    ![guia de trabalhos do coordenador](./media/hdinsight-use-oozie-linux-mac/coordinatorjob.png)

    Olá **materialização próxima** entrada contém Olá próxima vez que Olá execuções de trabalho.

8. Toohello semelhante anterior fluxo de trabalho, selecionando a entrada de trabalho Olá na interface da web hello exibe informações sobre o trabalho de saudação:

    ![Informações de trabalho do coordenador](./media/hdinsight-use-oozie-linux-mac/coordinatorjobinfo.png)

    > [!NOTE]
    > Esta imagem mostra apenas bem-sucedida execuções do trabalho hello, ações não individuais de fluxo de trabalho Olá agendado. toosee que, selecione uma saudação **ação** entradas.

    ![Informações da ação](./media/hdinsight-use-oozie-linux-mac/coordinatoractionjob.png)

## <a name="troubleshooting"></a>Solucionar problemas

Olá Oozie UI permite tooview Oozie logs. Ele também contém logs de tooJobTracker links para tarefas de MapReduce iniciadas pelo fluxo de trabalho de saudação. saudação padrão para solução de problemas deve ser:

1. Exibir o trabalho de saudação na interface do usuário da Web do Oozie.

2. Se houver um erro ou falha de uma ação específica, selecione Olá toosee ação se hello **mensagem de erro** campo fornece mais informações sobre a falha de saudação.

3. Se estiver disponível, use a URL de saudação da saudação ação tooview mais detalhes (como logs de JobTracker) para a ação de saudação.

Olá, estes são erros específicos que você pode encontrar, e como tooresolve-los.

### <a name="ja009-cannot-initialize-cluster"></a>JA009: não é possível inicializar o cluster

**Sintomas**: Olá alterações de status de trabalho muito**suspenso**. Detalhes do trabalho Olá mostram o status de RunHiveScript hello como **START_MANUAL**. Selecionando a ação de saudação exibe Olá a seguinte mensagem de erro:

    JA009: Cannot initialize Cluster. Please check your configuration for map

**Causa**: Olá endereços WASB usados em Olá **job.xml** arquivo não contém o contêiner de armazenamento hello ou nome de conta de armazenamento. formato de endereço Olá WASB deve ser `wasb://containername@storageaccountname.blob.core.windows.net`.

**Resolução**: alterar Olá WASB endereços usados pelo trabalho de saudação.

### <a name="ja002-oozie-is-not-allowed-tooimpersonate-ltuser"></a>JA002: Oozie não é permitido tooimpersonate &lt;usuário >

**Sintomas**: Olá alterações de status de trabalho muito**suspenso**. Detalhes do trabalho Olá mostram o status de RunHiveScript hello como **START_MANUAL**. Selecionando a ação de saudação mostra Olá a seguinte mensagem de erro:

    JA002: User: oozie is not allowed tooimpersonate <USER>

**Causa**: configurações de permissão atuais não permitem Oozie tooimpersonate Olá especificar conta de usuário.

**Resolução**: Oozie é permitido tooimpersonate usuários Olá **usuários** grupo. Saudação de uso `groups USERNAME` toosee grupos de Olá Olá a conta de usuário é membro. Se o usuário Olá não é um membro da saudação **usuários** de grupo, use Olá grupo toohello do comando tooadd Olá usuário a seguir:

    sudo adduser USERNAME users

> [!NOTE]
> Pode levar vários minutos antes de HDInsight reconhece que o usuário Olá foi adicionado toohello grupo.

### <a name="launcher-error-sqoop"></a>ERRO do Iniciador (Sqoop)

**Sintomas**: Olá alterações de status de trabalho muito**KILLED**. Detalhes do trabalho Olá mostram o status de RunSqoopExport hello como **erro**. Selecionando a ação de saudação mostra Olá a seguinte mensagem de erro:

    Launcher ERROR, reason: Main class [org.apache.oozie.action.hadoop.SqoopMain], exit code [1]

**Causa**: Sqoop é tooload não é possível Olá banco de dados driver necessário tooaccess Olá banco de dados.

**Resolução**: ao usar o Sqoop de um trabalho de Oozie, você deve incluir driver do banco de dados de saudação com hello outros recursos (como. XML Olá) usados pelo trabalho de saudação. Também fazer referência a arquivo hello que contém o driver de banco de dados de saudação do hello `<sqoop>...</sqoop>` seção. Olá XML.

Por exemplo, para o trabalho de saudação neste documento, você usaria Olá etapas a seguir:

1. Copie o diretório do hello sqljdbc4.1.jar arquivo toohello /tutorials/useoozie:

    ```
    hdfs dfs -put /usr/share/java/sqljdbc_4.1/enu/sqljdbc41.jar /tutorials/useoozie/sqljdbc41.jar
    ```

2. Modificar Olá. XML tooadd Olá XML a seguir em uma nova linha acima `</sqoop>`:

    ```xml
    <archive>sqljdbc41.jar</archive>
    ```

## <a name="next-steps"></a>Próximas etapas

Neste tutorial, você aprendeu como toodefine um fluxo de trabalho do Oozie e como toorun um trabalho Oozie. toolearn mais sobre como trabalhar com HDInsight, consulte Olá artigos a seguir:

* [Usar o Coordenador do Oozie baseado em tempo com o HDInsight][hdinsight-oozie-coordinator-time]
* [Carregar dados para trabalhos do Hadoop no HDInsight][hdinsight-upload-data]
* [Usar Sqoop com o Hadoop no HDInsight][hdinsight-use-sqoop]
* [Usar o Hive com Hadoop no HDInsight][hdinsight-use-hive]
* [Usar o Pig com Hadoop no HDInsight][hdinsight-use-pig]
* [Desenvolver programas Java MapReduce para HDInsight][hdinsight-develop-mapreduce]

[hdinsight-cmdlets-download]: http://go.microsoft.com/fwlink/?LinkID=325563
[azure-data-factory-pig-hive]: ../data-factory/data-factory-data-transformation-activities.md
[hdinsight-oozie-coordinator-time]: hdinsight-use-oozie-coordinator-time.md
[hdinsight-versions]:  hdinsight-component-versioning.md
[hdinsight-storage]: hdinsight-use-blob-storage.md
[hdinsight-get-started]: hdinsight-get-started.md
[hdinsight-use-sqoop]: hdinsight-use-sqoop-mac-linux.md
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-use-mapreduce]: hdinsight-use-mapreduce.md
[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-pig]: hdinsight-use-pig.md
[hdinsight-storage]: hdinsight-use-blob-storage.md
[hdinsight-get-started-emulator]: hdinsight-get-started-emulator.md
[hdinsight-develop-mapreduce]: hdinsight-develop-deploy-java-mapreduce-linux.md

[sqldatabase-create-configue]: sql-database-create-configure.md
[sqldatabase-get-started]: sql-database-get-started.md

[azure-create-storageaccount]:../storage/common/storage-create-storage-account.md

[apache-hadoop]: http://hadoop.apache.org/
[apache-oozie-400]: http://oozie.apache.org/docs/4.0.0/
[apache-oozie-332]: http://oozie.apache.org/docs/3.3.2/

[powershell-download]: http://azure.microsoft.com/downloads/
[powershell-about-profiles]: http://go.microsoft.com/fwlink/?LinkID=113729
[powershell-install-configure]: /powershell/azureps-cmdlets-docs
[powershell-start]: http://technet.microsoft.com/library/hh847889.aspx
[powershell-script]: https://technet.microsoft.com/en-us/library/ee176961.aspx

[cindygross-hive-tables]: http://blogs.msdn.com/b/cindygross/archive/2013/02/06/hdinsight-hive-internal-and-external-tables-intro.aspx

[img-workflow-diagram]: ./media/hdinsight-use-oozie/HDI.UseOozie.Workflow.Diagram.png
[img-preparation-output]: ./media/hdinsight-use-oozie/HDI.UseOozie.Preparation.Output1.png
[img-runworkflow-output]: ./media/hdinsight-use-oozie/HDI.UseOozie.RunWF.Output.png

[technetwiki-hive-error]: http://social.technet.microsoft.com/wiki/contents/articles/23047.hdinsight-hive-error-unable-to-rename.aspx
