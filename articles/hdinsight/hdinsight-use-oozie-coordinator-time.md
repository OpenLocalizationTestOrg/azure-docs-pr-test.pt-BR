---
title: coordenador de Hadoop Oozie aaaUse baseadas no HDInsight | Microsoft Docs
description: "Usar o Coordenador do Oozie com o Hadoop baseado no tempo no HDInsight, um serviço de big data. Saiba como toodefine Oozie coordenadores e fluxos de trabalho e enviar trabalhos."
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 00c3a395-d51a-44ff-af2d-1f116c4b1c83
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ms.openlocfilehash: aecbb5ee94a4234d1a7768bdb6de2a33508b1e4c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-time-based-oozie-coordinator-with-hadoop-in-hdinsight-toodefine-workflows-and-coordinate-jobs"></a>Usar o coordenador de Oozie baseada em tempo com Hadoop no HDInsight toodefine os fluxos de trabalho e coordenar trabalhos
Neste artigo, você aprenderá como fluxos de trabalho toodefine e coordenadores e como tootrigger Olá trabalhos do coordenador, com base no tempo. É útil toogo por meio de [Oozie de uso com o HDInsight] [ hdinsight-use-oozie] antes de ler este artigo. Além disso tooOozie, também é possível agendar trabalhos usando o Azure Data Factory. toolearn do Azure Data Factory, consulte [usar o Pig e Hive com a fábrica de dados](../data-factory/data-factory-data-transformation-activities.md).

> [!NOTE]
> Este artigo requer um cluster HDInsight baseado no Windows. Para obter informações sobre como usar Oozie, incluindo trabalhos baseados em tempo, em um cluster baseado em Linux, consulte [Oozie Use com toodefine Hadoop e executar um fluxo de trabalho no HDInsight baseados em Linux](hdinsight-use-oozie-linux-mac.md)

## <a name="what-is-oozie"></a>O que é o Oozie
O Apache Oozie é um sistema de fluxo de trabalho/coordenação que gerencia trabalhos do Hadoop. Ele é integrado com pilha de Hadoop hello e dá suporte à trabalhos de Hadoop MapReduce Apache, Pig do Apache, Apache Hive e Apache Sqoop. Ele também pode ser tooschedule usado trabalhos que são tooa específicas do sistema, como programas de Java ou scripts de shell.

Olá, imagem a seguir mostra Olá de fluxo de trabalho que você implementará:

![Diagrama de fluxo de trabalho][img-workflow-diagram]

fluxo de trabalho Olá contém duas ações:

1. Uma ação de Hive executa uma saudação de toocount script HiveQL ocorrências de cada tipo de nível de log em um arquivo de log log4j. Cada log log4j consiste em uma linha de campos que contém um [nível de LOG] campo tooshow Olá tipo e hello gravidade, por exemplo:

        2012-02-03 18:35:34 SampleClass6 [INFO] everything normal for id 577725851
        2012-02-03 18:35:34 SampleClass4 [FATAL] system problem at id 1991281254
        2012-02-03 18:35:34 SampleClass3 [DEBUG] detail for id 1304807656
        ...

    saudação de saída do script de Hive é semelhante a:

        [DEBUG] 434
        [ERROR] 3
        [FATAL] 1
        [INFO]  96
        [TRACE] 816
        [WARN]  4

    Para obter mais informações sobre o Hive, consulte [Usar o Hive com o HDInsight][hdinsight-use-hive].
2. Uma ação de Sqoop exporta a tabela de tooa de saída Olá HiveQL ação em um banco de dados do SQL Azure. Para saber mais sobre o Sqoop, confira [Usar o Sqoop com o HDInsight][hdinsight-use-sqoop].

> [!NOTE]
> Para versões com suporte do Oozie em clusters de HDInsight, consulte [Novidades nas versões de cluster Olá fornecidas pelo HDInsight?] [hdinsight-versions].
>
>

## <a name="prerequisites"></a>Pré-requisitos
Antes de começar este tutorial, você deve ter o seguinte hello:

* **Uma estação de trabalho com o PowerShell do Azure**.

    > [!IMPORTANT]
    > O suporte do Azure PowerShell para gerenciar os recursos do HDInsight usando o Gerenciador de Serviços do Azure está **preterido** e será removido em 1º de janeiro de 2017. Olá etapas para esse documento use Olá novos cmdlets do HDInsight que funcionam com o Gerenciador de recursos do Azure.
    >
    > Siga as etapas de saudação em [instalar e configurar o Azure PowerShell](/powershell/azureps-cmdlets-docs) tooinstall Olá última versão do PowerShell do Azure. Se você tiver scripts que toobe necessidade modificado toouse Olá novos cmdlets que funcionam com o Gerenciador de recursos do Azure, consulte [tooAzure migrando desenvolvimento baseado no Gerenciador de recursos de ferramentas para clusters de HDInsight](hdinsight-hadoop-development-using-azure-resource-manager.md) para obter mais informações.

* **Um cluster HDInsight**. Para saber mais sobre como criar um cluster HDInsight, confira [Criar cluster HDInsight][hdinsight-provision] ou [Introdução ao HDInsight][hdinsight-get-started]. Você precisará Olá toogo dados tutorial Olá a seguir:

    <table border = "1">
    <tr><th>Propriedade do cluster</th><th>Nome de variável do Windows PowerShell</th><th>Valor</th><th>Descrição</th></tr>
    <tr><td>Nome do cluster HDInsight</td><td>$clusterName</td><td></td><td>cluster de HDInsight Olá no qual você executará este tutorial.</td></tr>
    <tr><td>Nome de usuário do cluster HDInsight</td><td>$clusterUsername</td><td></td><td>nome de usuário do cluster do HDInsight Hello. </td></tr>
    <tr><td>Senha de usuário do cluster HDInsight </td><td>$clusterPassword</td><td></td><td>senha de usuário do cluster do HDInsight Hello.</td></tr>
    <tr><td>Nome da conta de armazenamento do Azure</td><td>$storageAccountName</td><td></td><td>Um cluster de HDInsight de toohello disponíveis de conta de armazenamento do Azure. Para este tutorial, use a conta de armazenamento de padrão de Olá que você especificou durante o processo de provisionamento de cluster hello.</td></tr>
    <tr><td>Nome do contêiner de blob do Azure</td><td>$containerName</td><td></td><td>Neste exemplo, use o contêiner de armazenamento de BLOBs do Azure Olá que é usado para o sistema de arquivos de cluster de HDInsight do saudação padrão. Por padrão, ele tem Olá mesmo nome do cluster do HDInsight hello.</td></tr>
    </table>
* **Um banco de dados SQL do Azure**. Você deve configurar uma regra de firewall para Olá tooallow acesso ao servidor de banco de dados SQL de sua estação de trabalho. Para obter instruções sobre como criar um banco de dados do SQL Azure e configurando o firewall do hello, consulte [se familiarizar com o banco de dados do SQL Azure] [sqldatabase-get-iniciado]. Este artigo fornece um script do Windows PowerShell para criar a tabela de banco de dados do SQL Azure Olá é necessário para este tutorial.

    <table border = "1">
    <tr><th>Propriedade de banco de dados SQL</th><th>Nome de variável do Windows PowerShell</th><th>Valor</th><th>Descrição</th></tr>
    <tr><td>Nome do servidor de banco de dados SQL</td><td>$sqlDatabaseServer</td><td></td><td>Olá SQL database server toowhich Sqoop exportará dados. </td></tr>
    <tr><td>Nome de logon do banco de dados SQL</td><td>$sqlDatabaseLogin</td><td></td><td>Nome de logon do banco de dados SQL.</td></tr>
    <tr><td>Senha de logon do banco de dados SQL</td><td>$sqlDatabaseLoginPassword</td><td></td><td>Senha de logon do banco de dados SQL.</td></tr>
    <tr><td>Nome do banco de dados SQL</td><td>$sqlDatabaseName</td><td></td><td>toowhich de banco de dados SQL do Azure de saudação Sqoop exportará dados. </td></tr>
    </table>

  > [!NOTE]
  > Por padrão, um banco de dados SQL do Azure permite conexões de serviços do Azure, como o Azure HDInsight. Se essa configuração de firewall estiver desabilitada, você deve habilitá-lo da saudação Portal do Azure. Para saber mais sobre como criar um Banco de Dados SQL e configurar regras de firewall, confira [Criar e configurar o Banco de Dados SQL][sqldatabase-get-started].

> [!NOTE]
> Valores de saudação de preenchimento em tabelas de saudação. Isso poderá ser útil para percorrer este tutorial.

## <a name="define-oozie-workflow-and-hello-related-hiveql-script"></a>Definir o fluxo de trabalho do Oozie e Olá script HiveQL relacionados
As definições de fluxos de trabalho do Oozie são escritas em hPDL (uma Linguagem de Definição de Processo XML). nome de arquivo de fluxo de trabalho saudação padrão *. XML*.  Você salvar o arquivo de fluxo de trabalho Olá localmente e, em seguida, implantá-lo cluster do HDInsight toohello por usar PowerShell do Azure, mais adiante neste tutorial.

Olá ação de Hive no fluxo de trabalho Olá chama um arquivo de script HiveQL. Esse arquivo de script contém três instruções HiveQL:

1. **Olá instrução DROP TABLE** exclusões Olá log4j Hive tabela se ela existir.
2. **Olá instrução CREATE TABLE** cria uma log4j Hive tabela externa, que aponta toohello local do arquivo de log do hello log4j;
3. **Olá local do arquivo de log do hello log4j**. é o delimitador de campo Hello ",". delimitador de linha Hello padrão é "\n". Uma tabela externa Hive é o arquivo de dados de saudação de tooavoid usado que está sendo removido do local original do hello, caso você deseje fluxo de trabalho toorun Olá Oozie várias vezes.
4. **Olá instrução inserir substituir** contagens de ocorrências de saudação de cada tipo de nível de log do hello log4j tabela de Hive e salva o local de armazenamento de BLOBs do Azure do hello saída tooan.

> [!NOTE]
> Há um erro conhecido do caminho do Hive. Você encontrará esse problema ao enviar um trabalho do Oozie. Olá instruções para corrigir o problema de saudação pode ser encontrada no hello Wiki do TechNet: [Hive do HDInsight erro: não é possível toorename][technetwiki-hive-error].

**toobe toodefine Olá HiveQL script arquivo chamado pelo fluxo de trabalho Olá**

1. Crie um arquivo de texto com hello seguinte conteúdo:

        DROP TABLE ${hiveTableName};
        CREATE EXTERNAL TABLE ${hiveTableName}(t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string) ROW FORMAT DELIMITED FIELDS TERMINATED BY ' ' STORED AS TEXTFILE LOCATION '${hiveDataFolder}';
        INSERT OVERWRITE DIRECTORY '${hiveOutputFolder}' SELECT t4 AS sev, COUNT(*) AS cnt FROM ${hiveTableName} WHERE t4 LIKE '[%' GROUP BY t4;

    Há três variáveis usadas em script hello:

   * ${hiveTableName}
   * ${hiveDataFolder}
   * ${hiveOutputFolder}

     arquivo de definição de fluxo de trabalho (. XML neste tutorial) Olá passará toothis esses valores script HiveQL em tempo de execução.
2. Salve o arquivo hello como **C:\Tutorials\UseOozie\useooziewf.hql** usando a codificação ANSI (ASCII). (Use o Bloco de Notas se o seu editor de texto não fornecer essa opção.) Esse arquivo de script será implantado toohello HDInsight cluster posteriormente no tutorial de saudação.

**toodefine um fluxo de trabalho**

1. Crie um arquivo de texto com hello seguinte conteúdo:

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
                <param>hiveOutputFolder=${hiveOutputFolder}</param>
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
            <arg>${hiveOutputFolder}</arg>
            <arg>-m</arg>
            <arg>1</arg>
            <arg>--input-fields-terminated-by</arg>
            <arg>"\001"</arg>
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

    Há duas ações definidas no fluxo de trabalho de saudação. Olá start-tooaction é *RunHiveScript*. Se a ação de saudação executa *Okey*, ação Avançar Olá é *RunSqoopExport*.

    Olá RunHiveScript tem diversas variáveis. Passa valores hello quando você enviar o trabalho de Oozie de saudação de sua estação de trabalho usando o PowerShell do Azure.

    Variáveis de fluxo de trabalho

    <table border = "1">
    <tr><th>Variáveis de fluxo de trabalho</th><th>Descrição</th></tr>
    <tr><td>${jobTracker}</td><td>Especifique a URL de saudação do rastreador de trabalho do Hadoop hello. Use <strong>jobtrackerhost:9010</strong> no cluster HDInsight versões 3.0 e 2.0.</td></tr>
    <tr><td>${nameNode}</td><td>Especifica URL de saudação do nó do nome de Hadoop hello. Usar saudação padrão arquivo sistema wasb: / / endereço, por exemplo, <i>wasb: / /&lt;containerName&gt;@&lt;storageAccountName&gt;. >.blob.Core.Windows.NET</i>.</td></tr>
    <tr><td>${queueName}</td><td>Especifica o nome de fila Olá Olá trabalho será enviado para. Use <strong>padrão</strong>.</td></tr>
    </table>

    Variáveis de ação do Hive

    <table border = "1">
    <tr><th>Variável de ação do Hive</th><th>Descrição</th></tr>
    <tr><td>${hiveDataFolder}</td><td>diretório de origem Olá para Olá comando Hive Create Table.</td></tr>
    <tr><td>${hiveOutputFolder}</td><td>pasta de saída Olá para Olá instrução inserir substituir.</td></tr>
    <tr><td>${hiveTableName}</td><td>nome de saudação da tabela de Hive Olá que faz referência a arquivos de dados de log4j hello.</td></tr>
    </table>

    Variáveis de ação do Sqoop

    <table border = "1">
    <tr><th>Variável de ação do Sqoop</th><th>Descrição</th></tr>
    <tr><td>${sqlDatabaseConnectionString}</td><td>Cadeia de conexão do Banco de Dados SQL.</td></tr>
    <tr><td>${sqlDatabaseTableName}</td><td>saudação de dados do SQL Azure banco de dados tabela toowhere saudação será exportada.</td></tr>
    <tr><td>${hiveOutputFolder}</td><td>pasta de saída Olá para Olá instrução Hive inserir substituir. Isso é hello mesma pasta para exportação de Sqoop hello (export-dir).</td></tr>
    </table>

    Para obter mais informações sobre o fluxo de trabalho do Oozie e usando as ações de fluxo de trabalho de saudação, consulte [documentação do Apache Oozie 4.0] [ apache-oozie-400] (para a versão 3.0 do cluster HDInsight) ou [Oozie Apache 3.3.2 documentação] [ apache-oozie-332] (para a versão 2.1 do cluster HDInsight).

1. Salve o arquivo hello como **C:\Tutorials\UseOozie\workflow.xml** usando a codificação ANSI (ASCII). (Use o Bloco de Notas se o seu editor de texto não fornecer essa opção.)

**coordenador de toodefine**

1. Crie um arquivo de texto com hello seguinte conteúdo:

    ```xml
    <coordinator-app name="my_coord_app" frequency="${coordFrequency}" start="${coordStart}" end="${coordEnd}" timezone="${coordTimezone}" xmlns="uri:oozie:coordinator:0.4">
        <action>
            <workflow>
                <app-path>${wfPath}</app-path>
            </workflow>
        </action>
    </coordinator-app>
    ```

    Há cinco variáveis usadas no arquivo de definição de saudação:

   | Variável | Descrição |
   | --- | --- |
   | ${coordFrequency} |Tempo de pausa do trabalho. A frequência sempre é expressa em minutos. |
   | ${coordStart} |Hora de início do trabalho. |
   | ${coordEnd} |Hora de término do trabalho. |
   | ${coordTimezone} |O Oozie processa trabalhos do coordenador em um fuso horário fixo sem horário de verão (geralmente representado pelo UTC). Este fuso horário é conhecido como hello "Oozie processamento de fuso horário." |
   | ${wfPath} |caminho Hello. Olá XML.  Se o nome de arquivo de fluxo de trabalho de saudação não é um nome de arquivo padrão de saudação (. xml), você deve especificar isto. |
2. Salve o arquivo hello como **C:\Tutorials\UseOozie\coordinator.xml** usando a codificação do hello ANSI (ASCII). (Use o Bloco de Notas se o seu editor de texto não fornecer essa opção.)

## <a name="deploy-hello-oozie-project-and-prepare-hello-tutorial"></a>Implantar projeto do Oozie hello e preparar o tutorial Olá
Você executará uma Azure PowerShell a seguir Olá script tooperform:

* Saudação de copiar o armazenamento de Blob tooAzure HiveQL script (useoozie.hql), wasb:///tutorials/useoozie/useoozie.hql.
* Copie toowasb:///tutorials/useoozie/workflow.xml. XML.
* Copie coordinator.xml toowasb:///tutorials/useoozie/coordinator.xml.
* Copiar arquivo de dados de saudação (/ example/data/sample.log) toowasb:///tutorials/useoozie/data/sample.log.
* Criar uma tabela do Banco de Dados SQL para armazenar os dados de exportação do Sqoop. nome da tabela Olá é *log4jLogCount*.

**Compreender o armazenamento do HDInsight**

O HDInsight usa o armazenamento de blob do Azure para o armazenamento de dados. wasb: / / é a implementação da Microsoft do sistema de arquivo hello distribuído de Hadoop (HDFS) no armazenamento de BLOBs do Azure. Para obter mais informações, consulte [Usar o Armazenamento de Blobs do Azure com o HDInsight][hdinsight-storage].

Quando você provisiona um cluster HDInsight, uma conta de armazenamento de BLOBs do Azure e um contêiner específico dessa conta é designado como o sistema de arquivos padrão hello, como no HDFS. Além disso toothis conta de armazenamento, você pode adicionar contas de armazenamento adicional da saudação mesmo assinatura do Azure ou de assinaturas do Azure diferentes durante o processo de provisionamento de saudação. Para saber mais sobre como adicionar mais contas de armazenamento, confira [Provisionar clusters HDInsight][hdinsight-provision]. script do toosimplify hello Azure PowerShell usado neste tutorial, todos os Olá arquivos são armazenados no contêiner do sistema de arquivos saudação padrão localizados no *tutoriais/useoozie*. Por padrão, esse contêiner tiver Olá mesmo nome como o nome do cluster HDInsight hello.
Olá sintaxe é:

    wasb[s]://<ContainerName>@<StorageAccountName>.blob.core.windows.net/<path>/<filename>

> [!NOTE]
> Olá somente *wasb: / /* sintaxe tem suporte na versão 3.0 do cluster HDInsight. Olá antigo *asv: / /* sintaxe tem suporte no HDInsight 2.1 e 1.6 clusters, mas não há suporte em clusters de HDInsight 3.0.
>
> Olá wasb: / / caminho é um caminho virtual. Para obter mais informações, consulte [Usar o Armazenamento de Blobs do Azure com o HDInsight][hdinsight-storage].

Um arquivo que é armazenado no contêiner do sistema de arquivos saudação padrão pode ser acessado do HDInsight usando qualquer Olá URIs (estou usando. XML como um exemplo) a seguir:

    wasb://mycontainer@mystorageaccount.blob.core.windows.net/tutorials/useoozie/workflow.xml
    wasb:///tutorials/useoozie/workflow.xml
    /tutorials/useoozie/workflow.xml

Se desejar que o arquivo de saudação do tooaccess diretamente da conta de armazenamento Olá, nome do blob Olá para o arquivo hello é:

    tutorials/useoozie/workflow.xml

**Compreender a tabela interna e a tabela externa do Hive**

Há algumas coisas que você precisa tooknow sobre tabelas internas e externas de Hive:

* Olá comando CREATE TABLE cria uma tabela interna, também conhecido como uma tabela gerenciada. arquivo de dados Olá deve estar localizado no contêiner de padrão de saudação.
* Olá comando CREATE TABLE move dados saudação arquivotoohello/hive/warehouse/<TableName> pasta no contêiner de padrão de saudação.
* Olá comando CREATE EXTERNAL TABLE cria uma tabela externa. arquivo de dados Olá pode estar localizado fora da saudação padrão contêiner.
* Olá comando CREATE EXTERNAL TABLE não mover o arquivo de dados de saudação.
* Olá comando CREATE EXTERNAL TABLE não permite que todas as subpastas na pasta Olá especificado na cláusula de local de saudação. Essa é Olá razão por que o tutorial Olá faz uma cópia do arquivo de sample.log hello.

Para obter mais informações, consulte [HDInsight: introdução às tabelas internas e externas do Hive][cindygross-hive-tables].

**tutorial de saudação tooprepare**

1. Saudação de abrir o Windows PowerShell ISE (na tela inicial do Windows 8 hello, digite **PowerShell_ISE**e, em seguida, clique em **o Windows PowerShell ISE**. Para obter mais informações, confira [Iniciar o Windows PowerShell no Windows 8 e no Windows][powershell-start]).
2. No painel inferior do hello, execute Olá comando tooconnect tooyour assinatura do Azure a seguir:

    ```powershell
    Add-AzureAccount
    ```

    Você será solicitado tooenter suas credenciais de conta do Azure. Esse método de adição de uma conexão de assinatura expira e depois de 12 horas, você terá toorun Olá cmdlet novamente.

   > [!NOTE]
   > Se você tiver várias assinaturas do Azure e assinatura do saudação padrão não é Olá aquele que você deseja toouse, use Olá <strong>Select-AzureSubscription</strong> tooselect cmdlet uma assinatura.

3. Copie Olá script a seguir no painel de script hello e então definir variáveis de seis primeiras hello:

    ```powershell
    # WASB variables
    $storageAccountName = "<StorageAccountName>"
    $containerName = "<BlobStorageContainerName>"

    # SQL database variables
    $sqlDatabaseServer = "<SQLDatabaseServerName>"
    $sqlDatabaseLogin = "<SQLDatabaseLoginName>"
    $sqlDatabaseLoginPassword = "SQLDatabaseLoginPassword>"
    $sqlDatabaseName = "<SQLDatabaseName>"
    $sqlDatabaseTableName = "log4jLogsCount"

    # Oozie files for hello tutorial
    $hiveQLScript = "C:\Tutorials\UseOozie\useooziewf.hql"
    $workflowDefinition = "C:\Tutorials\UseOozie\workflow.xml"
    $coordDefinition =  "C:\Tutorials\UseOozie\coordinator.xml"

    # WASB folder for storing hello Oozie tutorial files.
    $destFolder = "tutorials/useoozie"  # Do NOT use hello long path here
    ```

    Para obter mais descrições de variáveis de hello, consulte Olá [pré-requisitos](#prerequisites) seção neste tutorial.

4. Acrescente Olá toohello script no painel de script hello a seguir:

    ```powershell
    # Create a storage context object
    $storageaccountkey = get-azurestoragekey $storageAccountName | %{$_.Primary}
    $destContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageaccountkey

    function uploadOozieFiles()
    {
        Write-Host "Copy HiveQL script, workflow definition and coordinator definition ..." -ForegroundColor Green
        Set-AzureStorageBlobContent -File $hiveQLScript -Container $containerName -Blob "$destFolder/useooziewf.hql" -Context $destContext
        Set-AzureStorageBlobContent -File $workflowDefinition -Container $containerName -Blob "$destFolder/workflow.xml" -Context $destContext
        Set-AzureStorageBlobContent -File $coordDefinition -Container $containerName -Blob "$destFolder/coordinator.xml" -Context $destContext
    }

    function prepareHiveDataFile()
    {
        Write-Host "Make a copy of hello sample.log file ... " -ForegroundColor Green
        Start-CopyAzureStorageBlob -SrcContainer $containerName -SrcBlob "example/data/sample.log" -Context $destContext -DestContainer $containerName -destBlob "$destFolder/data/sample.log" -DestContext $destContext
    }

    function prepareSQLDatabase()
    {
        # SQL query string for creating log4jLogsCount table
        $cmdCreateLog4jCountTable = " CREATE TABLE [dbo].[$sqlDatabaseTableName](
                [Level] [nvarchar](10) NOT NULL,
                [Total] float,
            CONSTRAINT [PK_$sqlDatabaseTableName] PRIMARY KEY CLUSTERED
            (
            [Level] ASC
            )
            )"

        #Create hello log4jLogsCount table
        Write-Host "Create Log4jLogsCount table ..." -ForegroundColor Green
        $conn = New-Object System.Data.SqlClient.SqlConnection
        $conn.ConnectionString = "Data Source=$sqlDatabaseServer.database.windows.net;Initial Catalog=$sqlDatabaseName;User ID=$sqlDatabaseLogin;Password=$sqlDatabaseLoginPassword;Encrypt=true;Trusted_Connection=false;"
        $conn.open()
        $cmd = New-Object System.Data.SqlClient.SqlCommand
        $cmd.connection = $conn
        $cmd.commandtext = $cmdCreateLog4jCountTable
        $cmd.executenonquery()

        $conn.close()
    }

    # upload workflow.xml, coordinator.xml, and ooziewf.hql
    uploadOozieFiles;

    # make a copy of example/data/sample.log tooexample/data/log4j/sample.log
    prepareHiveDataFile;

    # create log4jlogsCount table on SQL database
    prepareSQLDatabase;
    ```

5. Clique em **Executar Script** ou pressione **F5** toorun script de saudação. saída de Hello será semelhante a:

    ![Saída de preparação do tutorial][img-preparation-output]

## <a name="run-hello-oozie-project"></a>Executar Olá Oozie projeto
Atualmente, o PowerShell do Azure não fornece nenhum cmdlet para definir trabalhos do Oozie. Você pode usar o hello **Invoke-RestMethod** tooinvoke cmdlet Oozie os serviços da web. API de serviços web de Oozie Olá é uma API de JSON de REST de HTTP. Para obter mais informações sobre a API de serviços web de Oozie hello, consulte [documentação do Apache Oozie 4.0] [ apache-oozie-400] (para a versão 3.0 do cluster HDInsight) ou [documentação do Apache Oozie 3.3.2] [ apache-oozie-332] (para a versão 2.1 do cluster HDInsight).

**toosubmit um trabalho Oozie**

1. Saudação de abrir o Windows PowerShell ISE (na tela inicial do Windows 8, digite **PowerShell_ISE**e, em seguida, clique em **o Windows PowerShell ISE**. Para obter mais informações, confira [Iniciar o Windows PowerShell no Windows 8 e no Windows][powershell-start]).
2. Script a seguir de saudação de cópia no painel de script hello e, em seguida, o conjunto Olá variáveis primeiro quatorze (no entanto, ignorar **$storageUri**).

    ```powershell
    #HDInsight cluster variables
    $clusterName = "<HDInsightClusterName>"
    $clusterUsername = "<HDInsightClusterUsername>"
    $clusterPassword = "<HDInsightClusterUserPassword>"

    #Azure Blob storage (WASB) variables
    $storageAccountName = "<StorageAccountName>"
    $storageContainerName = "<BlobContainerName>"
    $storageUri="wasb://$storageContainerName@$storageAccountName.blob.core.windows.net"

    #Azure SQL database variables
    $sqlDatabaseServer = "<SQLDatabaseServerName>"
    $sqlDatabaseLogin = "<SQLDatabaseLoginName>"
    $sqlDatabaseLoginPassword = "<SQLDatabaseloginPassword>"
    $sqlDatabaseName = "<SQLDatabaseName>"

    #Oozie WF/coordinator variables
    $coordStart = "2014-03-21T13:45Z"
    $coordEnd = "2014-03-21T13:45Z"
    $coordFrequency = "1440"    # in minutes, 24h x 60m = 1440m
    $coordTimezone = "UTC"    #UTC/GMT

    $oozieWFPath="$storageUri/tutorials/useoozie"  # hello default name is workflow.xml. And you don't need toospecify hello file name.
    $waitTimeBetweenOozieJobStatusCheck=10

    #Hive action variables
    $hiveScript = "$storageUri/tutorials/useoozie/useooziewf.hql"
    $hiveTableName = "log4jlogs"
    $hiveDataFolder = "$storageUri/tutorials/useoozie/data"
    $hiveOutputFolder = "$storageUri/tutorials/useoozie/output"

    #Sqoop action variables
    $sqlDatabaseConnectionString = "jdbc:sqlserver://$sqlDatabaseServer.database.windows.net;user=$sqlDatabaseLogin@$sqlDatabaseServer;password=$sqlDatabaseLoginPassword;database=$sqlDatabaseName"
    $sqlDatabaseTableName = "log4jLogsCount"

    $passwd = ConvertTo-SecureString $clusterPassword -AsPlainText -Force
    $creds = New-Object System.Management.Automation.PSCredential ($clusterUsername, $passwd)
    ```

    Para obter mais descrições de variáveis de hello, consulte Olá [pré-requisitos](#prerequisites) seção neste tutorial.

    $coordstart e $coordend são Olá início de fluxo de trabalho e a hora de término. toofind horário de UTC/GMT hello, pesquise "hora do utc" em bing.com. Olá $coordFrequency é a frequência em minutos que o fluxo de trabalho do toorun hello.
3. Acrescente Olá toohello script a seguir. Esta parte define a carga do Oozie hello:

    ```powershell
    #OoziePayload used for Oozie web service submission
    $OoziePayload =  @"
    <?xml version="1.0" encoding="UTF-8"?>
    <configuration>

        <property>
            <name>nameNode</name>
            <value>$storageUrI</value>
        </property>

        <property>
            <name>jobTracker</name>
            <value>jobtrackerhost:9010</value>
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
            <name>oozie.coord.application.path</name>
            <value>$oozieWFPath</value>
        </property>

        <property>
            <name>wfPath</name>
            <value>$oozieWFPath</value>
        </property>

        <property>
            <name>coordStart</name>
            <value>$coordStart</value>
        </property>

        <property>
            <name>coordEnd</name>
            <value>$coordEnd</value>
        </property>

        <property>
            <name>coordFrequency</name>
            <value>$coordFrequency</value>
        </property>

        <property>
            <name>coordTimezone</name>
            <value>$coordTimezone</value>
        </property>

        <property>
            <name>hiveScript</name>
            <value>$hiveScript</value>
        </property>

        <property>
            <name>hiveTableName</name>
            <value>$hiveTableName</value>
        </property>

        <property>
            <name>hiveDataFolder</name>
            <value>$hiveDataFolder</value>
        </property>

        <property>
            <name>hiveOutputFolder</name>
            <value>$hiveOutputFolder</value>
        </property>

        <property>
            <name>sqlDatabaseConnectionString</name>
            <value>&quot;$sqlDatabaseConnectionString&quot;</value>
        </property>

        <property>
            <name>sqlDatabaseTableName</name>
            <value>$SQLDatabaseTableName</value>
        </property>

        <property>
            <name>user.name</name>
            <value>admin</value>
        </property>

    </configuration>
    "@
    ```

   > [!NOTE]
   > Olá, o arquivo de carga de envio do principal diferença em comparação comparada toohello fluxo de trabalho é variável Olá **oozie.coord.application.path**. Ao enviar um trabalho de fluxo de trabalho, use **oozie.wf.application.path** em vez disso.

4. Acrescente Olá toohello script a seguir. Esta parte verifica o status do serviço Olá Oozie web:

    ```powershell
    function checkOozieServerStatus()
    {
        Write-Host "Checking Oozie server status..." -ForegroundColor Green
        $clusterUriStatus = "https://$clusterName.azurehdinsight.net:443/oozie/v2/admin/status"
        $response = Invoke-RestMethod -Method Get -Uri $clusterUriStatus -Credential $creds -OutVariable $OozieServerStatus

        $jsonResponse = ConvertFrom-Json (ConvertTo-Json -InputObject $response)
        $oozieServerSatus = $jsonResponse[0].("systemMode")
        Write-Host "Oozie server status is $oozieServerSatus..."

        if($oozieServerSatus -notmatch "NORMAL")
        {
            Write-Host "Oozie server status is $oozieServerSatus...cannot submit Oozie jobs. Check hello server status and re-run hello job."
            exit 1
        }
    }
    ```

5. Acrescente Olá toohello script a seguir. Esta parte cria um trabalho Oozie:

    ```powershell
    function createOozieJob()
    {
        # create Oozie job
        Write-Host "Sending hello following Payload toohello cluster:" -ForegroundColor Green
        Write-Host "`n--------`n$OoziePayload`n--------"
        $clusterUriCreateJob = "https://$clusterName.azurehdinsight.net:443/oozie/v2/jobs"
        $response = Invoke-RestMethod -Method Post -Uri $clusterUriCreateJob -Credential $creds -Body $OoziePayload -ContentType "application/xml" -OutVariable $OozieJobName -debug -Verbose

        $jsonResponse = ConvertFrom-Json (ConvertTo-Json -InputObject $response)
        $oozieJobId = $jsonResponse[0].("id")
        Write-Host "Oozie job id is $oozieJobId..."

        return $oozieJobId
    }
    ```

   > [!NOTE]
   > Quando você envia um fluxo de trabalho, você deve fazer outro web serviço chamada toostart Olá trabalho depois que o trabalho de saudação é criado. Nesse caso, o trabalho de coordenador de saudação é disparado por vez. trabalho de saudação será iniciado automaticamente.

6. Acrescente Olá toohello script a seguir. Esta parte verifica o status do trabalho Oozie hello:

    ```powershell
    function checkOozieJobStatus($oozieJobId)
    {
        # get job status
        Write-Host "Sleeping for $waitTimeBetweenOozieJobStatusCheck seconds until hello job metadata is populated in hello Oozie metastore..." -ForegroundColor Green
        Start-Sleep -Seconds $waitTimeBetweenOozieJobStatusCheck

        Write-Host "Getting job status and waiting for hello job toocomplete..." -ForegroundColor Green
        $clusterUriGetJobStatus = "https://$clusterName.azurehdinsight.net:443/oozie/v2/job/" + $oozieJobId + "?show=info"
        $response = Invoke-RestMethod -Method Get -Uri $clusterUriGetJobStatus -Credential $creds
        $jsonResponse = ConvertFrom-Json (ConvertTo-Json -InputObject $response)
        $JobStatus = $jsonResponse[0].("status")

        while($JobStatus -notmatch "SUCCEEDED|KILLED")
        {
            Write-Host "$(Get-Date -format 'G'): $oozieJobId is in $JobStatus state...waiting $waitTimeBetweenOozieJobStatusCheck seconds for hello job toocomplete..."
            Start-Sleep -Seconds $waitTimeBetweenOozieJobStatusCheck
            $response = Invoke-RestMethod -Method Get -Uri $clusterUriGetJobStatus -Credential $creds
            $jsonResponse = ConvertFrom-Json (ConvertTo-Json -InputObject $response)
            $JobStatus = $jsonResponse[0].("status")
        }

        Write-Host "$(Get-Date -format 'G'): $oozieJobId is in $JobStatus state!"
        if($JobStatus -notmatch "SUCCEEDED")
        {
            Write-Host "Check logs at http://headnode0:9014/cluster for detais."
            exit -1
        }
    }
    ```

7. (Opcional) Acrescente Olá toohello script a seguir.

    ```powershell
    function listOozieJobs()
    {
        Write-Host "Listing Oozie jobs..." -ForegroundColor Green
        $clusterUriStatus = "https://$clusterName.azurehdinsight.net:443/oozie/v2/jobs"
        $response = Invoke-RestMethod -Method Get -Uri $clusterUriStatus -Credential $creds

        write-host "Job ID                                   App Name        Status      Started                         Ended"
        write-host "----------------------------------------------------------------------------------------------------------------------------------"
        foreach($job in $response.workflows)
        {
            Write-Host $job.id "`t" $job.appName "`t" $job.status "`t" $job.startTime "`t" $job.endTime
        }
    }

    function ShowOozieJobLog($oozieJobId)
    {
        Write-Host "Showing Oozie job info..." -ForegroundColor Green
        $clusterUriStatus = "https://$clusterName.azurehdinsight.net:443/oozie/v2/job/$oozieJobId" + "?show=log"
        $response = Invoke-RestMethod -Method Get -Uri $clusterUriStatus -Credential $creds
        write-host $response
    }

    function killOozieJob($oozieJobId)
    {
        Write-Host "Killing hello Oozie job $oozieJobId..." -ForegroundColor Green
        $clusterUriStartJob = "https://$clusterName.azurehdinsight.net:443/oozie/v2/job/" + $oozieJobId + "?action=kill" #Valid values for hello 'action' parameter are 'start', 'suspend', 'resume', 'kill', 'dryrun', 'rerun', and 'change'.
        $response = Invoke-RestMethod -Method Put -Uri $clusterUriStartJob -Credential $creds | Format-Table -HideTableHeaders -debug
    }
    ```

8. Acrescente Olá toohello script a seguir:

    ```powershell
    checkOozieServerStatus
    # listOozieJobs
    $oozieJobId = createOozieJob($oozieJobId)
    checkOozieJobStatus($oozieJobId)
    # ShowOozieJobLog($oozieJobId)
    # killOozieJob($oozieJobId)
    ```

    Remova sinais de # Olá funções adicionais do toorun hello.
9. Se seu cluster HDinsight for versão 2.1, substitua "https://$clusterName.azurehdinsight.net:443/oozie/v2/" por "https://$clusterName.azurehdinsight.net:443/oozie/v1/". Versão 2.1 do cluster HDInsight não não dá suporte à versão 2 Olá serviços da web.
10. Clique em **Executar Script** ou pressione **F5** toorun script de saudação. saída de Hello será semelhante a:

     ![Saída do fluxo de trabalho da execução do tutorial][img-runworkflow-output]
11. Conecte-se tooyour dados do banco de dados SQL toosee hello exportada.

**log de erros de trabalho toocheck Olá**

tootroubleshoot um fluxo de trabalho, arquivo de log do Oozie Olá pode ser encontrado em C:\apps\dist\oozie-3.3.2.1.3.2.0-05\oozie-win-distro\logs\Oozie.log do nó principal do cluster Olá. Para obter informações sobre o RDP, consulte [Olá de clusters HDInsight administrando usando o portal do Azure][hdinsight-admin-portal].

**tutorial de saudação toorerun**

fluxo de trabalho toorerun hello, você deve executar Olá tarefas a seguir:

* Exclua o arquivo de saída do script de Hive de saudação.
* Exclua dados de saudação na tabela de log4jLogsCount hello.

Este é um exemplo de script do Windows PowerShell que você pode usar:

```powershell
$storageAccountName = "<AzureStorageAccountName>"
$containerName = "<ContainerName>"

#SQL database variables
$sqlDatabaseServer = "<SQLDatabaseServerName>"
$sqlDatabaseLogin = "<SQLDatabaseLoginName>"
$sqlDatabaseLoginPassword = "<SQLDatabaseLoginPassword>"
$sqlDatabaseName = "<SQLDatabaseName>"
$sqlDatabaseTableName = "log4jLogsCount"

Write-host "Delete hello Hive script output file ..." -ForegroundColor Green
$storageaccountkey = get-azurestoragekey $storageAccountName | %{$_.Primary}
$destContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageaccountkey
Remove-AzureStorageBlob -Context $destContext -Blob "tutorials/useoozie/output/000000_0" -Container $containerName

Write-host "Delete all hello records from hello log4jLogsCount table ..." -ForegroundColor Green
$conn = New-Object System.Data.SqlClient.SqlConnection
$conn.ConnectionString = "Data Source=$sqlDatabaseServer.database.windows.net;Initial Catalog=$sqlDatabaseName;User ID=$sqlDatabaseLogin;Password=$sqlDatabaseLoginPassword;Encrypt=true;Trusted_Connection=false;"
$conn.open()
$cmd = New-Object System.Data.SqlClient.SqlCommand
$cmd.connection = $conn
$cmd.commandtext = "delete from $sqlDatabaseTableName"
$cmd.executenonquery()

$conn.close()
```

## <a name="next-steps"></a>Próximas etapas
Neste tutorial, você aprendeu como toodefine um fluxo de trabalho do Oozie e um coordenador Oozie e como toorun um coordenador Oozie de trabalho usando o PowerShell do Azure. toolearn mais, consulte Olá artigos a seguir:

* [Introdução ao HDInsight][hdinsight-get-started]
* [Usar o armazenamento de Blobs do Azure com o HDInsight][hdinsight-storage]
* [Administrar clusters HDInsight usando o Azure PowerShell][hdinsight-admin-powershell]
* [Carregar dados tooHDInsight][hdinsight-upload-data]
* [Use o Sqoop com o HDInsight][hdinsight-use-sqoop]
* [Usar o Hive com o HDInsight][hdinsight-use-hive]
* [Usar o Pig com o HDInsight][hdinsight-use-pig]
* [Desenvolver programas Java MapReduce para HDInsight][hdinsight-develop-java-mapreduce]

[hdinsight-cmdlets-download]: http://go.microsoft.com/fwlink/?LinkID=325563

[hdinsight-versions]:  hdinsight-component-versioning.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-admin-portal]: hdinsight-administer-use-management-portal.md

[hdinsight-use-sqoop]: hdinsight-use-sqoop.md
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-admin-powershell]: hdinsight-administer-use-powershell.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-pig]: hdinsight-use-pig.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md
[hdinsight-develop-java-mapreduce]: hdinsight-develop-deploy-java-mapreduce-linux.md
[hdinsight-use-oozie]: hdinsight-use-oozie.md

[sqldatabase-get-started]: ../sql-database/sql-database-get-started.md

[azure-management-portal]: https://portal.azure.com/
[azure-create-storageaccount]:../storage/common/storage-create-storage-account.md

[apache-hadoop]: http://hadoop.apache.org/
[apache-oozie-400]: http://oozie.apache.org/docs/4.0.0/
[apache-oozie-332]: http://oozie.apache.org/docs/3.3.2/

[powershell-download]: http://azure.microsoft.com/downloads/
[powershell-about-profiles]: http://go.microsoft.com/fwlink/?LinkID=113729
[powershell-install-configure]: /powershell/azureps-cmdlets-docs
[powershell-start]: http://technet.microsoft.com/library/hh847889.aspx
[powershell-script]: http://technet.microsoft.com/library/ee176949.aspx

[cindygross-hive-tables]: http://blogs.msdn.com/b/cindygross/archive/2013/02/06/hdinsight-hive-internal-and-external-tables-intro.aspx

[img-workflow-diagram]: ./media/hdinsight-use-oozie-coordinator-time/HDI.UseOozie.Workflow.Diagram.png
[img-preparation-output]: ./media/hdinsight-use-oozie-coordinator-time/HDI.UseOozie.Preparation.Output1.png
[img-runworkflow-output]: ./media/hdinsight-use-oozie-coordinator-time/HDI.UseOozie.RunCoord.Output.png

[technetwiki-hive-error]: http://social.technet.microsoft.com/wiki/contents/articles/23047.hdinsight-hive-error-unable-to-rename.aspx
