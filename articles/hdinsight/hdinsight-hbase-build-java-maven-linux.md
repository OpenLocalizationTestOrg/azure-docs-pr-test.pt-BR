---
title: cliente de HBase aaaJava - HDInsight do Azure | Microsoft Docs
description: "Saiba como toouse aplicativo de Apache HBase do Apache Maven toobuild um baseados em Java, em seguida, implantá-lo tooHBase no Azure HDInsight."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: 
ms.assetid: 1d1ed180-e0f4-4d1c-b5ea-72e0eda643bc
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/07/2017
ms.author: larryfr
ms.openlocfilehash: 41ef92b2900280dd59089c4fa40686c44133b337
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="build-java-applications-for-apache-hbase"></a>Compilar aplicativos Java para Apache HBase

Saiba como toocreate uma [HBase Apache](http://hbase.apache.org/) aplicativo em Java. Em seguida, use o aplicativo hello com HBase em HDInsight do Azure.

Olá as etapas deste documento usam [Maven](http://maven.apache.org/) toocreate e compilação do projeto de saudação. Maven é uma ferramenta de compreensão que permite que você toobuild software, documentação e relatórios para projetos Java e o gerenciamento de projeto de software.

> [!NOTE]
> Olá etapas neste documento foram recentemente testadas com HDInsight 3.6.

> [!IMPORTANT]
> etapas de saudação neste documento exigem um cluster HDInsight que usa o Linux. Linux é Olá sistema operacional somente de usado no HDInsight versão 3.4 ou posterior. Para obter mais informações, confira [baixa do HDInsight no Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).

## <a name="requirements"></a>Requisitos

* [Plataforma Java JDK](http://www.oracle.com/technetwork/java/javase/downloads/index.html) 8 ou posterior.

    > [!NOTE]
    > O HDInsight 3.5 e posterior usa Java 8. Versões anteriores do HDInsight requerem Java 7.

* [Maven](http://maven.apache.org/)

* [Um cluster HDInsight do Azure baseado em Linux com HBase](hdinsight-hbase-tutorial-get-started-linux.md#create-hbase-cluster)

  > [!NOTE]
  > Olá etapas neste documento foram testadas com as versões de cluster HDInsight 3.4 e 3.5. valores padrão de saudação fornecidos nos exemplos são para um cluster HDInsight 3.5.

## <a name="create-hello-project"></a>Criar projeto Olá

1. Na linha de comando de saudação em seu ambiente de desenvolvimento, alterar o local de toohello de diretórios em que você deseja toocreate Olá projeto, por exemplo, `cd code\hbase`.

2. Saudação de uso **mvn** comando, que é instalado com o Maven, Olá toogenerate estrutura do projeto de saudação.

    ```bash
    mvn archetype:generate -DgroupId=com.microsoft.examples -DartifactId=hbaseapp -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
    ```

    > [!NOTE]
    > Se você estiver usando o PowerShell, você deverá colocar Olá `-D` parâmetros entre aspas duplas.
    >
    > `mvn archetype:generate "-DgroupId=com.microsoft.examples" "-DartifactId=hbaseapp" "-DarchetypeArtifactId=maven-archetype-quickstart" "-DinteractiveMode=false"`

    Este comando cria um diretório com hello mesmo nome como Olá **artifactID** parâmetro (**hbaseapp** neste exemplo.) Este diretório contém Olá itens a seguir:

   * **POM.XML**: Olá o modelo de objeto do projeto ([POM](http://maven.apache.org/guides/introduction/introduction-to-the-pom.html)) contém informações e configuração detalhes usados toobuild Olá projeto.
   * **src**: diretório de saudação que contém a saudação **principal/java/com/microsoft/exemplos** directory, onde você cria o aplicativo hello.

3. Excluir Olá `src/test/java/com/microsoft/examples/apptest.java` arquivo. Ele não será usado neste exemplo.

## <a name="update-hello-project-object-model"></a>Saudação de atualizar o modelo de objeto de projeto

1. Editar saudação `pom.xml` de arquivos e adicionar Olá seguindo o código dentro de saudação `<dependencies>` seção:

   ```xml
    <dependency>
        <groupId>org.apache.hbase</groupId>
        <artifactId>hbase-client</artifactId>
        <version>1.1.2</version>
    </dependency>
    <dependency>
        <groupId>org.apache.phoenix</groupId>
        <artifactId>phoenix-core</artifactId>
        <version>4.4.0-HBase-1.1</version>
    </dependency>
   ```

    Esta seção indica que o projeto Olá deve **hbase cliente** e **phoenix core** componentes. Em tempo de compilação, essas dependências são baixadas do repositório de Maven saudação padrão. Você pode usar o hello [pesquisa de repositório Central Maven](http://search.maven.org/#artifactdetails%7Corg.apache.hbase%7Chbase-client%7C0.98.4-hadoop2%7Cjar) toolearn mais sobre essa dependência.

   > [!IMPORTANT]
   > número de versão de saudação do hbase Olá-cliente deve corresponder a versão de saudação do HBase que é fornecido com o seu cluster HDInsight. Use Olá número de versão correta de saudação de toofind tabela a seguir.

   | Versão do cluster HDInsight | Toouse de versão do HBase |
   | --- | --- |
   | 3.2 |0.98.4-hadoop2 |
   | 3.3, 3.4, 3.5 e 3.6 |1.1.2 |

    Para obter mais informações sobre as versões de HDInsight e componentes, consulte [quais são Olá Hadoop componentes diferentes disponíveis com o HDInsight](hdinsight-component-versioning.md).

3. Adicionar Olá toohello de código a seguir **pom.xml** arquivo. Esse texto deve estar dentro de saudação `<project>...</project>` marcas de saudação do arquivo, por exemplo, entre `</dependencies>` e `</project>`.

   ```xml
    <build>
        <sourceDirectory>src</sourceDirectory>
        <resources>
        <resource>
            <directory>${basedir}/conf</directory>
            <filtering>false</filtering>
            <includes>
            <include>hbase-site.xml</include>
            </includes>
        </resource>
        </resources>
        <plugins>
        <plugin>
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-compiler-plugin</artifactId>
                    <version>3.3</version>
            <configuration>
                <source>1.8</source>
                <target>1.8</target>
            </configuration>
            </plugin>
        <plugin>
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-shade-plugin</artifactId>
            <version>2.3</version>
            <configuration>
            <transformers>
                <transformer implementation="org.apache.maven.plugins.shade.resource.ApacheLicenseResourceTransformer">
                </transformer>
            </transformers>
            </configuration>
            <executions>
            <execution>
                <phase>package</phase>
                <goals>
                <goal>shade</goal>
                </goals>
            </execution>
            </executions>
        </plugin>
        </plugins>
    </build>
   ```

    Esta seção configura um recurso (`conf/hbase-site.xml`), que contém informações de configuração para o HBase.

   > [!NOTE]
   > Você também pode definir valores de configuração via código. Consulte comentários Olá Olá `CreateTable` exemplo.

    Esta seção também configura Olá [plug-in de compilador Maven](http://maven.apache.org/plugins/maven-compiler-plugin/) e [plug-in de sombra Maven](http://maven.apache.org/plugins/maven-shade-plugin/). compilador de saudação plug-in é usado toocompile Olá topologia. Sombreamento de saudação plug-in é usado tooprevent eliminação de duplicação de licença no pacote JAR Olá que é criada pelo Maven. Este plug-in é usado tooprevent um erro "a duplicação de arquivos de licença" em tempo de execução no cluster do HDInsight hello. Usando o plugin do maven sombreamento com hello `ApacheLicenseResourceTransformer` implementação impede que o erro de saudação.

    Olá maven tonalidade plugin também produz um jar grande que contém todas as dependências de Olá exigidas pelo aplicativo hello.

4. Salvar Olá `pom.xml` arquivo.

5. Crie um diretório chamado `conf` em Olá `hbaseapp` directory. Este diretório é usado toohold informações de configuração para conectar-se tooHBase.

6. Comando a seguir de saudação de uso HBase configuração Olá toocopy Olá HBase cluster toohello `conf` directory. Substituir `USERNAME` com o nome de saudação do seu logon SSH. Substitua o `CLUSTERNAME` pelo nome do seu cluster HDInsight:

    ```bash
    scp USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:/etc/hbase/conf/hbase-site.xml ./conf/hbase-site.xml
    ```

   Para saber mais sobre como usar `ssh` e `scp`, confira [Usar SSH com HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

## <a name="create-hello-application"></a>Criar um aplicativo hello

1. Vá toohello `hbaseapp/src/main/java/com/microsoft/examples` diretório e renomear Olá app.java arquivo muito`CreateTable.java`.

2. Olá abrir `CreateTable.java` de arquivo e substitua conteúdo existente Olá Olá texto a seguir:

   ```java
    package com.microsoft.examples;
    import java.io.IOException;

    import org.apache.hadoop.conf.Configuration;
    import org.apache.hadoop.hbase.HBaseConfiguration;
    import org.apache.hadoop.hbase.client.HBaseAdmin;
    import org.apache.hadoop.hbase.HTableDescriptor;
    import org.apache.hadoop.hbase.TableName;
    import org.apache.hadoop.hbase.HColumnDescriptor;
    import org.apache.hadoop.hbase.client.HTable;
    import org.apache.hadoop.hbase.client.Put;
    import org.apache.hadoop.hbase.util.Bytes;

    public class CreateTable {
        public static void main(String[] args) throws IOException {
        Configuration config = HBaseConfiguration.create();

        // Example of setting zookeeper values for HDInsight
        // in code instead of an hbase-site.xml file
        //
        // config.set("hbase.zookeeper.quorum",
        //            "zookeepernode0,zookeepernode1,zookeepernode2");
        //config.set("hbase.zookeeper.property.clientPort", "2181");
        //config.set("hbase.cluster.distributed", "true");
        //
        //NOTE: Actual zookeeper host names can be found using Ambari:
        //curl -u admin:PASSWORD -G "https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/hosts"

        //Linux-based HDInsight clusters use /hbase-unsecure as hello znode parent
        config.set("zookeeper.znode.parent","/hbase-unsecure");

        // create an admin object using hello config
        HBaseAdmin admin = new HBaseAdmin(config);

        // create hello table...
        HTableDescriptor tableDescriptor = new HTableDescriptor(TableName.valueOf("people"));
        // ... with two column families
        tableDescriptor.addFamily(new HColumnDescriptor("name"));
        tableDescriptor.addFamily(new HColumnDescriptor("contactinfo"));
        admin.createTable(tableDescriptor);

        // define some people
        String[][] people = {
            { "1", "Marcel", "Haddad", "marcel@fabrikam.com"},
            { "2", "Franklin", "Holtz", "franklin@contoso.com" },
            { "3", "Dwayne", "McKee", "dwayne@fabrikam.com" },
            { "4", "Rae", "Schroeder", "rae@contoso.com" },
            { "5", "Rosalie", "burton", "rosalie@fabrikam.com"},
            { "6", "Gabriela", "Ingram", "gabriela@contoso.com"} };

        HTable table = new HTable(config, "people");

        // Add each person toohello table
        //   Use hello `name` column family for hello name
        //   Use hello `contactinfo` column family for hello email
        for (int i = 0; i< people.length; i++) {
            Put person = new Put(Bytes.toBytes(people[i][0]));
            person.add(Bytes.toBytes("name"), Bytes.toBytes("first"), Bytes.toBytes(people[i][1]));
            person.add(Bytes.toBytes("name"), Bytes.toBytes("last"), Bytes.toBytes(people[i][2]));
            person.add(Bytes.toBytes("contactinfo"), Bytes.toBytes("email"), Bytes.toBytes(people[i][3]));
            table.put(person);
        }
        // flush commits and close hello table
        table.flushCommits();
        table.close();
        }
    }
   ```

    Esse código é hello **CreateTable** classe, que cria uma tabela denominada **pessoas** e preenchê-la com alguns usuários predefinidos.

3. Salvar Olá `CreateTable.java` arquivo.

4. Em Olá `hbaseapp/src/main/java/com/microsoft/examples` diretório, crie um arquivo chamado `SearchByEmail.java`. Use Olá depois do texto como o conteúdo deste arquivo hello:

   ```java
    package com.microsoft.examples;
    import java.io.IOException;

    import org.apache.hadoop.conf.Configuration;
    import org.apache.hadoop.hbase.HBaseConfiguration;
    import org.apache.hadoop.hbase.client.HTable;
    import org.apache.hadoop.hbase.client.Scan;
    import org.apache.hadoop.hbase.client.ResultScanner;
    import org.apache.hadoop.hbase.client.Result;
    import org.apache.hadoop.hbase.filter.RegexStringComparator;
    import org.apache.hadoop.hbase.filter.SingleColumnValueFilter;
    import org.apache.hadoop.hbase.filter.CompareFilter.CompareOp;
    import org.apache.hadoop.hbase.util.Bytes;
    import org.apache.hadoop.util.GenericOptionsParser;

    public class SearchByEmail {
        public static void main(String[] args) throws IOException {
        Configuration config = HBaseConfiguration.create();

        // Use GenericOptionsParser tooget only hello parameters toohello class
        // and not all hello parameters passed (when using WebHCat for example)
        String[] otherArgs = new GenericOptionsParser(config, args).getRemainingArgs();
        if (otherArgs.length != 1) {
            System.out.println("usage: [regular expression]");
            System.exit(-1);
        }

        // Open hello table
        HTable table = new HTable(config, "people");

        // Define hello family and qualifiers toobe used
        byte[] contactFamily = Bytes.toBytes("contactinfo");
        byte[] emailQualifier = Bytes.toBytes("email");
        byte[] nameFamily = Bytes.toBytes("name");
        byte[] firstNameQualifier = Bytes.toBytes("first");
        byte[] lastNameQualifier = Bytes.toBytes("last");

        // Create a regex filter
        RegexStringComparator emailFilter = new RegexStringComparator(otherArgs[0]);
        // Attach hello regex filter tooa filter
        //   for hello email column
        SingleColumnValueFilter filter = new SingleColumnValueFilter(
            contactFamily,
            emailQualifier,
            CompareOp.EQUAL,
            emailFilter
        );

        // Create a scan and set hello filter
        Scan scan = new Scan();
        scan.setFilter(filter);

        // Get hello results
        ResultScanner results = table.getScanner(scan);
        // Iterate over results and print  values
        for (Result result : results ) {
            String id = new String(result.getRow());
            byte[] firstNameObj = result.getValue(nameFamily, firstNameQualifier);
            String firstName = new String(firstNameObj);
            byte[] lastNameObj = result.getValue(nameFamily, lastNameQualifier);
            String lastName = new String(lastNameObj);
            System.out.println(firstName + " " + lastName + " - ID: " + id);
            byte[] emailObj = result.getValue(contactFamily, emailQualifier);
            String email = new String(emailObj);
            System.out.println(firstName + " " + lastName + " - " + email + " - ID: " + id);
        }
        results.close();
        table.close();
        }
    }
   ```

    Olá **SearchByEmail** classe pode ser usado tooquery para linhas por endereço de email. Porque ele usa um filtro de expressão regular, você pode fornecer uma cadeia de caracteres ou uma expressão regular ao usar a classe de saudação.

5. Salvar Olá `SearchByEmail.java` arquivo.

6. Em Olá `hbaseapp/src/main/hava/com/microsoft/examples` diretório, crie um arquivo chamado `DeleteTable.java`. Use Olá depois do texto como o conteúdo deste arquivo hello:

   ```java
    package com.microsoft.examples;
    import java.io.IOException;

    import org.apache.hadoop.conf.Configuration;
    import org.apache.hadoop.hbase.HBaseConfiguration;
    import org.apache.hadoop.hbase.client.HBaseAdmin;

    public class DeleteTable {
        public static void main(String[] args) throws IOException {
        Configuration config = HBaseConfiguration.create();

        // Create an admin object using hello config
        HBaseAdmin admin = new HBaseAdmin(config);

        // Disable, and then delete hello table
        admin.disableTable("people");
        admin.deleteTable("people");
        }
    }
   ```

    Essa classe limpa Olá HBase tabelas criadas neste exemplo, desabilitando e descartando Olá tabela criadas pelo Olá `CreateTable` classe.

7. Salvar Olá `DeleteTable.java` arquivo.

## <a name="build-and-package-hello-application"></a>Aplicativo hello de compilação e pacote

1. De saudação `hbaseapp` diretório, o comando a seguir do uso Olá toobuild um arquivo JAR que contém o aplicativo hello:

    ```bash
    mvn clean package
    ```

    Este comando cria e pacotes Olá aplicativo em um arquivo. jar.

2. Quando Olá comando for concluído, hello `hbaseapp/target` diretório contém um arquivo chamado `hbaseapp-1.0-SNAPSHOT.jar`.

   > [!NOTE]
   > Olá `hbaseapp-1.0-SNAPSHOT.jar` arquivo é um jar grande. Ele contém todos os aplicativos de Olá Olá dependências toorun necessária.


## <a name="upload-hello-jar-and-run-jobs-ssh"></a>Olá JAR de carregar e executar trabalhos (SSH)

Olá use as etapas a seguir `scp` toocopy Olá JAR toohello primário nó principal do seu HBase no cluster HDInsight. Olá `ssh` comando é usada tooconnect toohello cluster e execute o exemplo hello diretamente no nó principal hello.

1. tooupload Olá jar toohello cluster use Olá comando a seguir:

    ```bash
    scp ./target/hbaseapp-1.0-SNAPSHOT.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:hbaseapp-1.0-SNAPSHOT.jar
    ```

    Substituir `USERNAME` com o nome de saudação do seu logon SSH. Substitua o `CLUSTERNAME` pelo nome do seu cluster HDInsight.

2. tooconnect toohello HBase cluster, use Olá comando a seguir:

    ```bash
    ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
    ```

    Substituir `USERNAME` nome de saudação do seu logon SSH. Substitua o `CLUSTERNAME` pelo nome do seu cluster HDInsight.

3. toocreate uma tabela do HBase usando Olá aplicativo Java, use Olá comando a seguir:

    ```bash
    yarn jar hbaseapp-1.0-SNAPSHOT.jar com.microsoft.examples.CreateTable
    ```

    Esse comando cria uma nova tabela do HBase chamada **people** e a preenche com dados.

4. toosearch para endereços de email armazenados na tabela hello, use Olá comando a seguir:

    ```bash
    yarn jar hbaseapp-1.0-SNAPSHOT.jar com.microsoft.examples.SearchByEmail contoso.com
    ```

    Você receberá Olá resultados a seguir:

        Franklin Holtz - ID: 2
        Franklin Holtz - franklin@contoso.com - ID: 2
        Rae Schroeder - ID: 4
        Rae Schroeder - rae@contoso.com - ID: 4
        Gabriela Ingram - ID: 6
        Gabriela Ingram - gabriela@contoso.com - ID: 6

5. tabela de saudação toodelete, use Olá comando a seguir:

    

## <a name="upload-hello-jar-and-run-jobs-powershell"></a>Olá JAR de carregar e executar trabalhos (PowerShell)

Olá etapas a seguir usa armazenamento do Azure PowerShell tooupload Olá JAR toohello padrão para o cluster HBase. Cmdlets do HDInsight forem usado toorun Olá exemplos remotamente.

1. Após instalar e configurar o Azure PowerShell, crie um arquivo chamado `hbase-runner.psm1`. Use Olá depois do texto como o conteúdo deste arquivo hello:

   ```powershell
    <#
    .SYNOPSIS
    Copies a file toohello primary storage of an HDInsight cluster.
    .DESCRIPTION
    Copies a file from a local directory toohello blob container for
    hello HDInsight cluster.
    .EXAMPLE
    Start-HBaseExample -className "com.microsoft.examples.CreateTable"
    -clusterName "MyHDInsightCluster"

    .EXAMPLE
    Start-HBaseExample -className "com.microsoft.examples.SearchByEmail"
    -clusterName "MyHDInsightCluster"
    -emailRegex "contoso.com"

    .EXAMPLE
    Start-HBaseExample -className "com.microsoft.examples.SearchByEmail"
    -clusterName "MyHDInsightCluster"
    -emailRegex "^r" -showErr
    #>

    function Start-HBaseExample {
    [CmdletBinding(SupportsShouldProcess = $true)]
    param(
    #hello class toorun
    [Parameter(Mandatory = $true)]
    [String]$className,

    #hello name of hello HDInsight cluster
    [Parameter(Mandatory = $true)]
    [String]$clusterName,

    #Only used when using SearchByEmail
    [Parameter(Mandatory = $false)]
    [String]$emailRegex,

    #Use if you want toosee stderr output
    [Parameter(Mandatory = $false)]
    [Switch]$showErr
    )

    Set-StrictMode -Version 3

    # Is hello Azure module installed?
    FindAzure

    # Get hello login for hello HDInsight cluster
    $creds=Get-Credential -Message "Enter hello login for hello cluster" -UserName "admin"

    # hello JAR
    $jarFile = "wasb:///example/jars/hbaseapp-1.0-SNAPSHOT.jar"

    # hello job definition
    $jobDefinition = New-AzureRmHDInsightMapReduceJobDefinition `
        -JarFile $jarFile `
        -ClassName $className `
        -Arguments $emailRegex

    # Get hello job output
    $job = Start-AzureRmHDInsightJob `
        -ClusterName $clusterName `
        -JobDefinition $jobDefinition `
        -HttpCredential $creds
    Write-Host "Wait for hello job toocomplete ..." -ForegroundColor Green
    Wait-AzureRmHDInsightJob `
        -ClusterName $clusterName `
        -JobId $job.JobId `
        -HttpCredential $creds
    if($showErr)
    {
    Write-Host "STDERR"
    Get-AzureRmHDInsightJobOutput `
                -Clustername $clusterName `
                -JobId $job.JobId `
                -HttpCredential $creds `
                -DisplayOutputType StandardError
    }
    Write-Host "Display hello standard output ..." -ForegroundColor Green
    Get-AzureRmHDInsightJobOutput `
                -Clustername $clusterName `
                -JobId $job.JobId `
                -HttpCredential $creds
    }

    <#
    .SYNOPSIS
    Copies a file toohello primary storage of an HDInsight cluster.
    .DESCRIPTION
    Copies a file from a local directory toohello blob container for
    hello HDInsight cluster.
    .EXAMPLE
    Add-HDInsightFile -localPath "C:\temp\data.txt"
    -destinationPath "example/data/data.txt"
    -ClusterName "MyHDInsightCluster"
    .EXAMPLE
    Add-HDInsightFile -localPath "C:\temp\data.txt"
    -destinationPath "example/data/data.txt"
    -ClusterName "MyHDInsightCluster"
    -Container "MyContainer"
    #>

    function Add-HDInsightFile {
        [CmdletBinding(SupportsShouldProcess = $true)]
        param(
            #hello path toohello local file.
            [Parameter(Mandatory = $true)]
            [String]$localPath,

            #hello destination path and file name, relative toohello root of hello container.
            [Parameter(Mandatory = $true)]
            [String]$destinationPath,

            #hello name of hello HDInsight cluster
            [Parameter(Mandatory = $true)]
            [String]$clusterName,

            #If specified, overwrites existing files without prompting
            [Parameter(Mandatory = $false)]
            [Switch]$force
        )

        Set-StrictMode -Version 3

        # Is hello Azure module installed?
        FindAzure

        # Get authentication for hello cluster
        $creds=Get-Credential

        # Does hello local path exist?
        if (-not (Test-Path $localPath))
        {
            throw "Source path '$localPath' does not exist."
        }

        # Get hello primary storage container
        $storage = GetStorage -clusterName $clusterName

        # Upload file toostorage, overwriting existing files if -force was used.
        Set-AzureStorageBlobContent -File $localPath `
            -Blob $destinationPath `
            -force:$force `
            -Container $storage.container `
            -Context $storage.context
    }

    function FindAzure {
        # Is there an active Azure subscription?
        $sub = Get-AzureRmSubscription -ErrorAction SilentlyContinue
        if(-not($sub))
        {
            throw "No active Azure subscription found! If you have a subscription, use hello Login-AzureRmAccount cmdlet toologin tooyour subscription."
        }
    }

    function GetStorage {
        param(
            [Parameter(Mandatory = $true)]
            [String]$clusterName
        )
        $hdi = Get-AzureRmHDInsightCluster -ClusterName $clusterName
        # Does hello cluster exist?
        if (!$hdi)
        {
            throw "HDInsight cluster '$clusterName' does not exist."
        }
        # Create a return object for context & container
        $return = @{}
        $storageAccounts = @{}

        # Get storage information
        $resourceGroup = $hdi.ResourceGroup
        $storageAccountName=$hdi.DefaultStorageAccount.split('.')[0]
        $container=$hdi.DefaultStorageContainer
        $storageAccountKey=(Get-AzureRmStorageAccountKey `
            -Name $storageAccountName `
        -ResourceGroupName $resourceGroup)[0].Value
        # Get hello resource group, in case we need that
        $return.resourceGroup = $resourceGroup
        # Get hello storage context, as we can't depend
        # on using hello default storage context
        $return.context = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey
        # Get hello container, so we know where to
        # find/store blobs
        $return.container = $container
        # Return storage accounts toosupport finding all accounts for
        # a cluster
        $return.storageAccount = $storageAccountName
        $return.storageAccountKey = $storageAccountKey

        return $return
    }
    # Only export hello verb-phrase things
    export-modulemember *-*
   ```

    Esse arquivo contém dois módulos:

   * **Adicionar HDInsightFile** - usadas cluster de toohello arquivos tooupload
   * **Iniciar HBaseExample** -toorun Olá classes criadas anteriormente usadas

2. Salvar Olá `hbase-runner.psm1` arquivo.

3. Abra uma nova janela do PowerShell do Azure, altere os diretórios toohello `hbaseapp` directory, e, em seguida, Olá executar comando a seguir:

    ```powershell
    PS C:\ Import-Module c:\path\to\hbase-runner.psm1
    ```

    Alterar Olá caminho toohello local de saudação `hbase-runner.psm1` arquivo criado anteriormente. Esse comando registra o módulo de saudação com o Azure PowerShell.

4. Comando a seguir de saudação do uso Olá tooupload `hbaseapp-1.0-SNAPSHOT.jar` tooyour cluster.

    ```powershell
    Add-HDInsightFile -localPath target\hbaseapp-1.0-SNAPSHOT.jar -destinationPath example/jars/hbaseapp-1.0-SNAPSHOT.jar -clusterName hdinsightclustername
    ```

    Substituir `hdinsightclustername` com nome de saudação do cluster. comando Olá carrega Olá `hbaseapp-1.0-SNAPSHOT.jar` toohello `example/jars` local no armazenamento primário de saudação para seu cluster.

5. Olá toocreate uma tabela usando `hbaseapp`, use Olá comando a seguir:

    ```powershell
    Start-HBaseExample -className com.microsoft.examples.CreateTable -clusterName hdinsightclustername
    ```

    Substituir `hdinsightclustername` com nome de saudação do cluster.

    Esse comando cria uma tabela chamada **people** no HBase em seu cluster HDInsight. Este comando não mostra nenhuma saída na janela do console de saudação.

6. toosearch de entradas na tabela de hello, use Olá comando a seguir:

    ```powershell
    Start-HBaseExample -className com.microsoft.examples.SearchByEmail -clusterName hdinsightclustername -emailRegex contoso.com
    ```

    Substituir `hdinsightclustername` com nome de saudação do cluster.

    Esse comando usa Olá `SearchByEmail` classe toosearch para todas as linhas onde hello `contactinformation` família de coluna e hello `email` coluna contém a cadeia de caracteres de saudação `contoso.com`. Você deve receber Olá resultados a seguir:

          Franklin Holtz - ID: 2
          Franklin Holtz - franklin@contoso.com - ID: 2
          Rae Schroeder - ID: 4
          Rae Schroeder - rae@contoso.com - ID: 4
          Gabriela Ingram - ID: 6
          Gabriela Ingram - gabriela@contoso.com - ID: 6

    Usando **fabrikam.com** para Olá `-emailRegex` valor retorna usuários Olá que têm **fabrikam.com** no campo de email hello. Você também pode usar expressões regulares, como o termo de pesquisa hello. Por exemplo, **^ r** retorna endereços que começam com hello letra 'r'.

### <a name="no-results-or-unexpected-results-when-using-start-hbaseexample"></a>Nenhum resultado ou resultados inesperados ao usar o Start-HBaseExample

Saudação de uso `-showErr` parâmetro tooview saudação padrão erro (STDERR) que é gerado durante o trabalho de saudação em execução.

## <a name="delete-hello-table"></a>Excluir tabela Olá

Quando tiver terminado com o exemplo hello, use Olá Olá toodelete a seguir **pessoas** tabela usada neste exemplo:

__De uma sessão `ssh`__:

`yarn jar hbaseapp-1.0-SNAPSHOT.jar com.microsoft.examples.DeleteTable`

__Do Azure PowerShell__:

`Start-HBaseExample -className com.microsoft.examples.DeleteTable -clusterName hdinsightclustername`

## <a name="next-steps"></a>Próximas etapas

[Saiba como toouse SQL esquilo com HBase](hdinsight-hbase-phoenix-squirrel-linux.md)
