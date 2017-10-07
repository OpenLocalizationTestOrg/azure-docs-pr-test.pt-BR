---
title: aaaBuild um aplicativo de Java HBase baseados no Windows Azure HDInsight | Microsoft Docs
description: "Saiba como toouse aplicativo de Apache HBase do Apache Maven toobuild um baseados em Java, em seguida, implantá-lo tooa baseados no Windows Azure HDInsight cluster."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 7f4a4e02-45ab-40dd-842b-3ec034f256c9
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/05/2017
ms.author: larryfr
ROBOTS: NOINDEX
ms.openlocfilehash: 33c2f3d12cb6a17b5406817e8bcd3accff239517
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-maven-toobuild-java-applications-that-use-hbase-with-windows-based-hdinsight-hadoop"></a>Usar Maven toobuild Java aplicativos que usam HBase com HDInsight baseados em Windows (Hadoop)
Saiba como toocreate e criar um [HBase Apache](http://hbase.apache.org/) aplicativo em Java usando o Apache Maven. Em seguida, use o aplicativo hello com Azure HDInsight (Hadoop).

[Maven](http://maven.apache.org/) é um projeto management e compreender ferramenta de software que permite que você toobuild software, documentação e relatórios para projetos Java. Neste artigo, você aprenderá como toouse-toocreate um aplicativo Java básico que cria, consulta e exclui um HBase de tabela em um cluster HDInsight do Azure.

> [!IMPORTANT]
> etapas de saudação neste documento exigem um cluster HDInsight que usa o Windows. Linux é Olá sistema operacional somente de usado no HDInsight versão 3.4 ou posterior. Para obter mais informações, confira [baixa do HDInsight no Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).

## <a name="requirements"></a>Requisitos
* [Plataforma Java JDK](http://www.oracle.com/technetwork/java/javase/downloads/index.html) 7 ou superior
* [Maven](http://maven.apache.org/)
* Um cluster HDInsight baseado no Windows com HBase

    > [!NOTE]
    > Olá etapas neste documento foram testadas com as versões 3.2 e 3.3 do HDInsight cluster. valores padrão de saudação fornecidos nos exemplos são para um cluster HDInsight 3.3.

## <a name="create-hello-project"></a>Criar projeto Olá
1. Na linha de comando de saudação em seu ambiente de desenvolvimento, alterar o local de toohello de diretórios em que você deseja toocreate Olá projeto, por exemplo, `cd code\hdinsight`.
2. Saudação de uso **mvn** comando, que é instalado com o Maven, Olá toogenerate estrutura do projeto de saudação.

        mvn archetype:generate -DgroupId=com.microsoft.examples -DartifactId=hbaseapp -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false

    Este comando cria um diretório no local atual do hello, com o nome de saudação especificado pelo Olá **artifactID** parâmetro (**hbaseapp** neste exemplo.) Este diretório contém Olá itens a seguir:

   * **POM.XML**: Olá o modelo de objeto do projeto ([POM](http://maven.apache.org/guides/introduction/introduction-to-the-pom.html)) contém informações e configuração detalhes usados toobuild Olá projeto.
   * **src**: diretório de saudação que contém a saudação **main\java\com\microsoft\examples** directory, onde você irá criar aplicativo hello.
3. Excluir Olá **src\test\java\com\microsoft\examples\apptest.java** arquivo porque ele não é usado neste exemplo.

## <a name="update-hello-project-object-model"></a>Saudação de atualizar o modelo de objeto de projeto
1. Editar saudação **pom.xml** de arquivos e adicionar Olá seguindo o código dentro de saudação `<dependencies>` seção:

        <dependency>
          <groupId>org.apache.hbase</groupId>
          <artifactId>hbase-client</artifactId>
          <version>1.1.2</version>
        </dependency>

    Esta seção informa Maven que Olá projeto requer **hbase cliente** versão **1.1.2**. Em tempo de compilação, a dependência é baixada do repositório de Maven saudação padrão. Você pode usar o hello [pesquisa de repositório Central Maven](http://search.maven.org/#artifactdetails%7Corg.apache.hbase%7Chbase-client%7C0.98.4-hadoop2%7Cjar) toolearn mais sobre essa dependência.

   > [!IMPORTANT]
   > número de versão de Hello deve corresponder a versão de saudação do HBase que é fornecido com o seu cluster HDInsight. Use Olá número de versão correta de saudação de toofind tabela a seguir.
   >
   >

   | Versão do cluster HDInsight | Toouse de versão do HBase |
   | --- | --- |
   | 3.2 |0.98.4-hadoop2 |
   | 3.3 |1.1.2 |

    Para obter mais informações sobre as versões de HDInsight e componentes, consulte [quais são Olá Hadoop componentes diferentes disponíveis com o HDInsight](hdinsight-component-versioning.md).
2. Se você estiver usando um cluster HDInsight 3.3, você também deverá adicionar Olá após toohello `<dependencies>` seção:

        <dependency>
            <groupId>org.apache.phoenix</groupId>
            <artifactId>phoenix-core</artifactId>
            <version>4.4.0-HBase-1.1</version>
        </dependency>

    Essa dependência carregará componentes de phoenix core hello, que são usados pelo Hbase versão 1.1.
3. Adicionar Olá toohello de código a seguir **pom.xml** arquivo. Esta seção deve estar dentro de saudação `<project>...</project>` marcas de saudação do arquivo, por exemplo, entre `</dependencies>` e `</project>`.

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
                    <source>1.7</source>
                    <target>1.7</target>
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

    Olá `<resources>` seção configura um recurso (**conf\hbase Storm-site.XML**) que contém informações de configuração para HBase.

   > [!NOTE]
   > Você também pode definir valores de configuração via código. Consulte comentários Olá Olá **CreateTable** exemplo a seguir para saber como toodo isso.
   >
   >

    Isso `<plugins>` seção configura Olá [plug-in de compilador Maven](http://maven.apache.org/plugins/maven-compiler-plugin/) e [plug-in de sombra Maven](http://maven.apache.org/plugins/maven-shade-plugin/). compilador de saudação plug-in é usado toocompile Olá topologia. Sombreamento de saudação plug-in é usado tooprevent eliminação de duplicação de licença no pacote JAR Olá que é criada pelo Maven. motivo de saudação que é usado é que os arquivos de licença duplicadas de saudação causam um erro em tempo de execução no cluster do HDInsight hello. Usando o plugin do maven sombreamento com hello `ApacheLicenseResourceTransformer` implementação impede que esse erro.

    Olá maven-tonalidade-plug-in também produz uma grande jar (ou jar fat) que contém todas as dependências de Olá exigidas pelo aplicativo hello.
4. Salvar Olá **pom.xml** arquivo.
5. Crie um novo diretório chamado **conf** em Olá **hbaseapp** directory. Em Olá **conf** diretório, crie um arquivo chamado **hbase-site.XML**. Use o seguinte hello como conteúdo de saudação do arquivo hello:

        <?xml version="1.0"?>
        <?xml-stylesheet type="text/xsl" href="configuration.xsl"?>
        <!--
        /**
          * Copyright 2010 hello Apache Software Foundation
          *
          * Licensed toohello Apache Software Foundation (ASF) under one
          * or more contributor license agreements.  See hello NOTICE file
          * distributed with this work for additional information
          * regarding copyright ownership.  hello ASF licenses this file
          * tooyou under hello Apache License, Version 2.0 (the
          * "License"); you may not use this file except in compliance
          * with hello License.  You may obtain a copy of hello License at
          *
          *     http://www.apache.org/licenses/LICENSE-2.0
          *
          * Unless required by applicable law or agreed tooin writing, software
          * distributed under hello License is distributed on an "AS IS" BASIS,
          * WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
          * See hello License for hello specific language governing permissions and
          * limitations under hello License.
          */
        -->
        <configuration>
          <property>
            <name>hbase.cluster.distributed</name>
            <value>true</value>
          </property>
          <property>
            <name>hbase.zookeeper.quorum</name>
            <value>zookeeper0,zookeeper1,zookeeper2</value>
          </property>
          <property>
            <name>hbase.zookeeper.property.clientPort</name>
            <value>2181</value>
          </property>
        </configuration>

    Esse arquivo será a configuração de HBase Olá tooload usado para um cluster HDInsight.

   > [!NOTE]
   > Este é um arquivo hbase-site.XML mínima e contém as configurações mínimas de bare da saudação de cluster do HDInsight hello.

6. Salvar Olá **hbase-site.XML** arquivo.

## <a name="create-hello-application"></a>Criar um aplicativo hello
1. Vá toohello **hbaseapp\src\main\java\com\microsoft\examples** diretório e renomear Olá arquivo app.java muito**CreateTable.java**.
2. Olá abrir **CreateTable.java** de arquivo e substitua conteúdo existente Olá Olá código a seguir:

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
            // hello following sets hello znode root for Linux-based HDInsight
            //config.set("zookeeper.znode.parent","/hbase-unsecure");

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

    Isso é hello **CreateTable** classe, que criará uma tabela denominada **pessoas** e preenchê-la com alguns usuários predefinidos.
3. Salvar Olá **CreateTable.java** arquivo.
4. Em Olá **hbaseapp\src\main\java\com\microsoft\examples** diretório, crie um novo arquivo chamado **SearchByEmail.java**. Use Olá código a seguir como o conteúdo deste arquivo hello:

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

            // Create a new regex filter
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

    Olá **SearchByEmail** classe pode ser usado tooquery para linhas por endereço de email. Porque ele usa um filtro de expressão regular, você pode fornecer uma cadeia de caracteres ou uma expressão regular ao usar a classe de saudação.
5. Salvar Olá **SearchByEmail.java** arquivo.
6. Em Olá **hbaseapp\src\main\hava\com\microsoft\examples** diretório, crie um novo arquivo chamado **DeleteTable.java**. Use Olá código a seguir como o conteúdo deste arquivo hello:

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

    Essa classe é para limpar esse exemplo desabilitando e descartando Olá tabela criados por Olá **CreateTable** classe.
7. Salvar Olá **DeleteTable.java** arquivo.

## <a name="build-and-package-hello-application"></a>Aplicativo hello de compilação e pacote
1. Abra um prompt de comando e altere os diretórios toohello **hbaseapp** directory.
2. Use Olá comando toobuild um arquivo JAR que contém o aplicativo hello a seguir:

        mvn clean package

    Isso limpa qualquer artefatos de compilação anterior, baixa todas as dependências que ainda não tiver sido instaladas, em seguida, cria e pacotes aplicativo hello.
3. Quando Olá comando for concluído, hello **hbaseapp\target** diretório contém um arquivo chamado **hbaseapp-1.0-SNAPSHOT.jar**.

   > [!NOTE]
   > Olá **hbaseapp-1.0-SNAPSHOT.jar** arquivo é uma grande jar (às vezes chamado de um jar fat,) que contém todas as dependências de saudação necessário toorun aplicativo de hello.

## <a name="upload-hello-jar-file-and-start-a-job"></a>Carregue o arquivo JAR de saudação e iniciar um trabalho
Há muitos tooupload de maneiras um cluster do HDInsight de tooyour arquivos, conforme descrito em [carregar dados para trabalhos de Hadoop no HDInsight](hdinsight-upload-data.md). Olá, etapas a seguir usam PowerShell do Azure.

[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]

1. Após instalar e configurar o Azure PowerShell, crie um novo arquivo chamado **hbase-runner.psm1**. Use o seguinte de hello como o conteúdo deste arquivo hello:

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

    Esse arquivo contém dois módulos:

   * **Adicionar HDInsightFile** -usado tooupload arquivos tooHDInsight
   * **Iniciar HBaseExample** -toorun Olá classes criadas anteriormente usadas
2. Salvar Olá **hbase runner.psm1** arquivo.
3. Abra uma nova janela do PowerShell do Azure, altere os diretórios toohello **hbaseapp** directory, e, em seguida, Olá executar comando a seguir.

        PS C:\ Import-Module c:\path\to\hbase-runner.psm1

    Alterar Olá caminho toohello local de saudação **hbase runner.psm1** arquivo criado anteriormente. Isso registra o módulo Olá para esta sessão do PowerShell do Azure.
4. Comando a seguir de saudação do uso Olá tooupload **hbaseapp-1.0-SNAPSHOT.jar** tooyour HDInsight cluster.

        Add-HDInsightFile -localPath target\hbaseapp-1.0-SNAPSHOT.jar -destinationPath example/jars/hbaseapp-1.0-SNAPSHOT.jar -clusterName hdinsightclustername

    Substituir **hdinsightclustername** com nome de saudação do cluster HDInsight. comando Olá carrega Olá **hbaseapp-1.0-SNAPSHOT.jar** toohello **exemplo/jars** local no armazenamento primário Olá seu cluster HDInsight.
5. Depois que forem carregados arquivos Olá, use Olá de código a seguir toocreate uma tabela usando Olá **hbaseapp**:

        Start-HBaseExample -className com.microsoft.examples.CreateTable -clusterName hdinsightclustername

    Substituir **hdinsightclustername** com nome de saudação do cluster HDInsight.

    Esse comando cria uma nova tabela chamada **pessoas** em seu cluster HDInsight. Este comando não mostra nenhuma saída na janela do console de saudação.
6. toosearch de entradas na tabela de hello, use Olá comando a seguir:

        Start-HBaseExample -className com.microsoft.examples.SearchByEmail -clusterName hdinsightclustername -emailRegex contoso.com

    Substituir **hdinsightclustername** com nome de saudação do cluster HDInsight.

    Esse comando usa Olá **SearchByEmail** classe toosearch para todas as linhas onde hello **contactinformation** família de coluna e hello **email** coluna contém a cadeia de caracteres de saudação **contoso.com**. Você deve receber Olá resultados a seguir:

          Franklin Holtz - ID: 2
          Franklin Holtz - franklin@contoso.com - ID: 2
          Rae Schroeder - ID: 4
          Rae Schroeder - rae@contoso.com - ID: 4
          Gabriela Ingram - ID: 6
          Gabriela Ingram - gabriela@contoso.com - ID: 6

    Usando **fabrikam.com** para Olá `-emailRegex` valor retorna usuários Olá que têm **fabrikam.com** no campo de email hello. Desde que esta pesquisa é implementada usando um filtro de baseadas em expressão regular, você também pode inserir expressões regulares, como **^ r**, quais entradas retorna onde o email Olá começa com hello letra 'r'.

## <a name="delete-hello-table"></a>Excluir tabela Olá
Quando tiver terminado com o exemplo hello, comando a seguir do uso Olá de saudação do hello Azure PowerShell sessão toodelete **pessoas** tabela usada neste exemplo:

    Start-HBaseExample -className com.microsoft.examples.DeleteTable -clusterName hdinsightclustername

Substituir **hdinsightclustername** com nome de saudação do cluster HDInsight.

## <a name="troubleshooting"></a>Solucionar problemas
### <a name="no-results-or-unexpected-results-when-using-start-hbaseexample"></a>Nenhum resultado ou resultados inesperados ao usar o Start-HBaseExample
Saudação de uso `-showErr` parâmetro tooview saudação padrão erro (STDERR) que é gerado durante o trabalho de saudação em execução.
