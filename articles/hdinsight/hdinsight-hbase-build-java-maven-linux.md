---
title: "Cliente HBase Java – Azure HDInsight | Microsoft Docs"
description: "Saiba como usar o Apache Maven para compilar um aplicativo do Apache HBase baseado em Java e depois implantá-lo no HBase no HDInsight do Azure."
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
ms.openlocfilehash: 03c88397e36c0fc7f19410e49f6b6f1a607659f8
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="build-java-applications-for-apache-hbase"></a><span data-ttu-id="22a18-103">Compilar aplicativos Java para Apache HBase</span><span class="sxs-lookup"><span data-stu-id="22a18-103">Build Java applications for Apache HBase</span></span>

<span data-ttu-id="22a18-104">Saiba como criar um aplicativo [Apache HBase](http://hbase.apache.org/) em Java.</span><span class="sxs-lookup"><span data-stu-id="22a18-104">Learn how to create an [Apache HBase](http://hbase.apache.org/) application in Java.</span></span> <span data-ttu-id="22a18-105">Depois, use o aplicativo com o HBase no Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="22a18-105">Then use the application with HBase on Azure HDInsight.</span></span>

<span data-ttu-id="22a18-106">As etapas deste documentam usam [Maven](http://maven.apache.org/) para criar e compilar o projeto.</span><span class="sxs-lookup"><span data-stu-id="22a18-106">The steps in this document use [Maven](http://maven.apache.org/) to create and build the project.</span></span> <span data-ttu-id="22a18-107">Maven é uma ferramenta de software para compreensão e gerenciamento de projetos que permite a você compilar software, documentação e relatórios para projetos Java.</span><span class="sxs-lookup"><span data-stu-id="22a18-107">Maven is a software project management and comprehension tool that allows you to build software, documentation, and reports for Java projects.</span></span>

> [!NOTE]
> <span data-ttu-id="22a18-108">As etapas neste documento foram testadas mais recentemente com o HDInsight 3.6.</span><span class="sxs-lookup"><span data-stu-id="22a18-108">The steps in this document were most recently tested with HDInsight 3.6.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="22a18-109">As etapas deste documento exigem um cluster HDInsight que usa Linux.</span><span class="sxs-lookup"><span data-stu-id="22a18-109">The steps in this document require an HDInsight cluster that uses Linux.</span></span> <span data-ttu-id="22a18-110">O Linux é o único sistema operacional usado no HDInsight versão 3.4 ou superior.</span><span class="sxs-lookup"><span data-stu-id="22a18-110">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="22a18-111">Para obter mais informações, confira [baixa do HDInsight no Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="22a18-111">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <a name="requirements"></a><span data-ttu-id="22a18-112">Requisitos</span><span class="sxs-lookup"><span data-stu-id="22a18-112">Requirements</span></span>

* <span data-ttu-id="22a18-113">[Plataforma Java JDK](http://www.oracle.com/technetwork/java/javase/downloads/index.html) 8 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="22a18-113">[Java platform JDK](http://www.oracle.com/technetwork/java/javase/downloads/index.html) 8 or later.</span></span>

    > [!NOTE]
    > <span data-ttu-id="22a18-114">O HDInsight 3.5 e posterior usa Java 8.</span><span class="sxs-lookup"><span data-stu-id="22a18-114">HDInsight 3.5 and greater requires Java 8.</span></span> <span data-ttu-id="22a18-115">Versões anteriores do HDInsight requerem Java 7.</span><span class="sxs-lookup"><span data-stu-id="22a18-115">Earlier versions of HDInsight require Java 7.</span></span>

* [<span data-ttu-id="22a18-116">Maven</span><span class="sxs-lookup"><span data-stu-id="22a18-116">Maven</span></span>](http://maven.apache.org/)

* [<span data-ttu-id="22a18-117">Um cluster HDInsight do Azure baseado em Linux com HBase</span><span class="sxs-lookup"><span data-stu-id="22a18-117">A Linux-based Azure HDInsight cluster with HBase</span></span>](hdinsight-hbase-tutorial-get-started-linux.md#create-hbase-cluster)

  > [!NOTE]
  > <span data-ttu-id="22a18-118">As etapas neste documento foram testadas com as versões 3.4 e 3.5 do cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="22a18-118">The steps in this document have been tested with HDInsight cluster versions 3.4 and 3.5.</span></span> <span data-ttu-id="22a18-119">Os valores padrão fornecidos nos exemplos destinam-se um cluster HDInsight 3.5.</span><span class="sxs-lookup"><span data-stu-id="22a18-119">The default values provided in examples are for a HDInsight 3.5 cluster.</span></span>

## <a name="create-the-project"></a><span data-ttu-id="22a18-120">Criar o projeto</span><span class="sxs-lookup"><span data-stu-id="22a18-120">Create the project</span></span>

1. <span data-ttu-id="22a18-121">Por meio da linha de comando em seu ambiente de desenvolvimento, mude os diretórios para o local em que você deseja criar o projeto, por exemplo, `cd code\hbase`.</span><span class="sxs-lookup"><span data-stu-id="22a18-121">From the command line in your development environment, change directories to the location where you want to create the project, for example, `cd code\hbase`.</span></span>

2. <span data-ttu-id="22a18-122">Use o comando **mvn** , que é instalado com o Maven, para gerar o scaffolding para o projeto.</span><span class="sxs-lookup"><span data-stu-id="22a18-122">Use the **mvn** command, which is installed with Maven, to generate the scaffolding for the project.</span></span>

    ```bash
    mvn archetype:generate -DgroupId=com.microsoft.examples -DartifactId=hbaseapp -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
    ```

    > [!NOTE]
    > <span data-ttu-id="22a18-123">Se você estiver usando o PowerShell, coloque os parâmetros `-D` entre aspas duplas.</span><span class="sxs-lookup"><span data-stu-id="22a18-123">If you are using PowerShell, you must enclose the `-D` parameters in double quotes.</span></span>
    >
    > `mvn archetype:generate "-DgroupId=com.microsoft.examples" "-DartifactId=hbaseapp" "-DarchetypeArtifactId=maven-archetype-quickstart" "-DinteractiveMode=false"`

    <span data-ttu-id="22a18-124">Esse comando cria um novo diretório com o mesmo nome que o parâmetro **artifactID** (**hbaseapp** neste exemplo). Esse diretório contém os seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="22a18-124">This command creates a directory with the same name as the **artifactID** parameter (**hbaseapp** in this example.) This directory contains the following items:</span></span>

   * <span data-ttu-id="22a18-125">**pom.xml**: o[POM](http://maven.apache.org/guides/introduction/introduction-to-the-pom.html)(Modelo de Objeto de Projeto) contém informações e detalhes de configuração usados para compilar o projeto.</span><span class="sxs-lookup"><span data-stu-id="22a18-125">**pom.xml**:  The Project Object Model ([POM](http://maven.apache.org/guides/introduction/introduction-to-the-pom.html)) contains information and configuration details used to build the project.</span></span>
   * <span data-ttu-id="22a18-126">**src**: o diretório que contém **main\java\com\microsoft\examples**, no qual você criará seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="22a18-126">**src**: The directory that contains the **main/java/com/microsoft/examples** directory, where you author the application.</span></span>

3. <span data-ttu-id="22a18-127">Exclua o arquivo `src/test/java/com/microsoft/examples/apptest.java`.</span><span class="sxs-lookup"><span data-stu-id="22a18-127">Delete the `src/test/java/com/microsoft/examples/apptest.java` file.</span></span> <span data-ttu-id="22a18-128">Ele não será usado neste exemplo.</span><span class="sxs-lookup"><span data-stu-id="22a18-128">It is not be used in this example.</span></span>

## <a name="update-the-project-object-model"></a><span data-ttu-id="22a18-129">Atualize o modelo do objeto do projeto</span><span class="sxs-lookup"><span data-stu-id="22a18-129">Update the Project Object Model</span></span>

1. <span data-ttu-id="22a18-130">Edite o arquivo `pom.xml` e adicione o seguinte código dentro da seção `<dependencies>`:</span><span class="sxs-lookup"><span data-stu-id="22a18-130">Edit the `pom.xml` file and add the following code inside the `<dependencies>` section:</span></span>

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

    <span data-ttu-id="22a18-131">Esta seção indica que o projeto precisa dos componentes **hbase-client** e **phoenix-core**.</span><span class="sxs-lookup"><span data-stu-id="22a18-131">This section indicates that the project needs **hbase-client** and **phoenix-core** components.</span></span> <span data-ttu-id="22a18-132">Em tempo de compilação, essa dependência será baixada do repositório padrão do Maven.</span><span class="sxs-lookup"><span data-stu-id="22a18-132">At compile time, these dependencies are downloaded from the default Maven repository.</span></span> <span data-ttu-id="22a18-133">Você pode usar a [Pesquisa de repositório central do Maven](http://search.maven.org/#artifactdetails%7Corg.apache.hbase%7Chbase-client%7C0.98.4-hadoop2%7Cjar) para saber mais sobre essa dependência.</span><span class="sxs-lookup"><span data-stu-id="22a18-133">You can use the [Maven Central Repository Search](http://search.maven.org/#artifactdetails%7Corg.apache.hbase%7Chbase-client%7C0.98.4-hadoop2%7Cjar) to learn more about this dependency.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="22a18-134">O número da versão do cliente hbase deve corresponder à versão do HBase fornecida com o cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="22a18-134">The version number of the hbase-client must match the version of HBase that is provided with your HDInsight cluster.</span></span> <span data-ttu-id="22a18-135">Use a tabela a seguir para localizar o número da versão correta.</span><span class="sxs-lookup"><span data-stu-id="22a18-135">Use the following table to find the correct version number.</span></span>

   | <span data-ttu-id="22a18-136">Versão do cluster HDInsight</span><span class="sxs-lookup"><span data-stu-id="22a18-136">HDInsight cluster version</span></span> | <span data-ttu-id="22a18-137">Versão do HBase a ser usada</span><span class="sxs-lookup"><span data-stu-id="22a18-137">HBase version to use</span></span> |
   | --- | --- |
   | <span data-ttu-id="22a18-138">3.2</span><span class="sxs-lookup"><span data-stu-id="22a18-138">3.2</span></span> |<span data-ttu-id="22a18-139">0.98.4-hadoop2</span><span class="sxs-lookup"><span data-stu-id="22a18-139">0.98.4-hadoop2</span></span> |
   | <span data-ttu-id="22a18-140">3.3, 3.4, 3.5 e 3.6</span><span class="sxs-lookup"><span data-stu-id="22a18-140">3.3, 3.4, 3.5, and 3.6</span></span> |<span data-ttu-id="22a18-141">1.1.2</span><span class="sxs-lookup"><span data-stu-id="22a18-141">1.1.2</span></span> |

    <span data-ttu-id="22a18-142">Para saber mais sobre as versões e os componentes do HDInsight, confira [Quais são os diferentes componentes do Hadoop disponíveis com o HDInsight?](hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="22a18-142">For more information on HDInsight versions and components, see [What are the different Hadoop components available with HDInsight](hdinsight-component-versioning.md).</span></span>

3. <span data-ttu-id="22a18-143">Adicione o código a seguir ao arquivo **pom.xml**.</span><span class="sxs-lookup"><span data-stu-id="22a18-143">Add the following code to the **pom.xml** file.</span></span> <span data-ttu-id="22a18-144">Esse texto deve estar dentro das marcas `<project>...</project>` no arquivo, por exemplo, entre `</dependencies>` e `</project>`.</span><span class="sxs-lookup"><span data-stu-id="22a18-144">This text must be inside the `<project>...</project>` tags in the file, for example, between `</dependencies>` and `</project>`.</span></span>

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

    <span data-ttu-id="22a18-145">Esta seção configura um recurso (`conf/hbase-site.xml`), que contém informações de configuração para o HBase.</span><span class="sxs-lookup"><span data-stu-id="22a18-145">This section configures a resource (`conf/hbase-site.xml`) that contains configuration information for HBase.</span></span>

   > [!NOTE]
   > <span data-ttu-id="22a18-146">Você também pode definir valores de configuração via código.</span><span class="sxs-lookup"><span data-stu-id="22a18-146">You can also set configuration values via code.</span></span> <span data-ttu-id="22a18-147">Veja os comentários no exemplo `CreateTable`.</span><span class="sxs-lookup"><span data-stu-id="22a18-147">See the comments in the `CreateTable` example.</span></span>

    <span data-ttu-id="22a18-148">Esta seção também configura os plug-ins [Maven Compiler](http://maven.apache.org/plugins/maven-compiler-plugin/) e [Maven Shade](http://maven.apache.org/plugins/maven-shade-plugin/).</span><span class="sxs-lookup"><span data-stu-id="22a18-148">This section also configures the [Maven Compiler Plugin](http://maven.apache.org/plugins/maven-compiler-plugin/) and [Maven Shade Plugin](http://maven.apache.org/plugins/maven-shade-plugin/).</span></span> <span data-ttu-id="22a18-149">O plug-in compilador é usado para compilar a topologia.</span><span class="sxs-lookup"><span data-stu-id="22a18-149">The compiler plug-in is used to compile the topology.</span></span> <span data-ttu-id="22a18-150">O plug-in de tonalidade é usado para evitar a duplicação de licenças no pacote JAR que é criado pelo Maven.</span><span class="sxs-lookup"><span data-stu-id="22a18-150">The shade plug-in is used to prevent license duplication in the JAR package that is built by Maven.</span></span> <span data-ttu-id="22a18-151">O plug-in serve para evitar o erro de arquivos de licença duplicados no momento da execução no cluster do HDInsight.</span><span class="sxs-lookup"><span data-stu-id="22a18-151">This plugin is used to prevent a "duplicate license files" error at run time on the HDInsight cluster.</span></span> <span data-ttu-id="22a18-152">Utilize o plug-in de tonalidade do Maven com a implementação `ApacheLicenseResourceTransformer` para isso.</span><span class="sxs-lookup"><span data-stu-id="22a18-152">Using maven-shade-plugin with the `ApacheLicenseResourceTransformer` implementation prevents the error.</span></span>

    <span data-ttu-id="22a18-153">O plug-in de tonalidade do Maven também produzirá um uber jar, que contém todas as dependências exigidas pelo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="22a18-153">The maven-shade-plugin also produces an uber jar that contains all the dependencies required by the application.</span></span>

4. <span data-ttu-id="22a18-154">Salve o arquivo `pom.xml`.</span><span class="sxs-lookup"><span data-stu-id="22a18-154">Save the `pom.xml` file.</span></span>

5. <span data-ttu-id="22a18-155">Crie um diretório chamado `conf` no diretório `hbaseapp`.</span><span class="sxs-lookup"><span data-stu-id="22a18-155">Create a directory named `conf` in the `hbaseapp` directory.</span></span> <span data-ttu-id="22a18-156">Esse diretório será usado para armazenar informações de configuração para se conectar ao HBase.</span><span class="sxs-lookup"><span data-stu-id="22a18-156">This directory is used to hold configuration information for connecting to HBase.</span></span>

6. <span data-ttu-id="22a18-157">Use o seguinte comando para copiar a configuração HBase do cluster HBase para o diretório `conf`.</span><span class="sxs-lookup"><span data-stu-id="22a18-157">Use the following command to copy the HBase configuration from the HBase cluster to the `conf` directory.</span></span> <span data-ttu-id="22a18-158">Substitua `USERNAME` pelo nome de seu logon SSH.</span><span class="sxs-lookup"><span data-stu-id="22a18-158">Replace `USERNAME` with the name of your SSH login.</span></span> <span data-ttu-id="22a18-159">Substitua o `CLUSTERNAME` pelo nome do seu cluster HDInsight:</span><span class="sxs-lookup"><span data-stu-id="22a18-159">Replace `CLUSTERNAME` with your HDInsight cluster name:</span></span>

    ```bash
    scp USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:/etc/hbase/conf/hbase-site.xml ./conf/hbase-site.xml
    ```

   <span data-ttu-id="22a18-160">Para saber mais sobre como usar `ssh` e `scp`, confira [Usar SSH com HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="22a18-160">For more information on using `ssh` and `scp`, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

## <a name="create-the-application"></a><span data-ttu-id="22a18-161">Criar o aplicativo</span><span class="sxs-lookup"><span data-stu-id="22a18-161">Create the application</span></span>

1. <span data-ttu-id="22a18-162">Acesse o diretório `hbaseapp/src/main/java/com/microsoft/examples` e renomeie o arquivo app.java como `CreateTable.java`.</span><span class="sxs-lookup"><span data-stu-id="22a18-162">Go to the `hbaseapp/src/main/java/com/microsoft/examples` directory and rename the app.java file to `CreateTable.java`.</span></span>

2. <span data-ttu-id="22a18-163">Abra o arquivo `CreateTable.java` e substitua o conteúdo existente pelo texto exibido a seguir:</span><span class="sxs-lookup"><span data-stu-id="22a18-163">Open the `CreateTable.java` file and replace the existing contents with the following text:</span></span>

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

        //Linux-based HDInsight clusters use /hbase-unsecure as the znode parent
        config.set("zookeeper.znode.parent","/hbase-unsecure");

        // create an admin object using the config
        HBaseAdmin admin = new HBaseAdmin(config);

        // create the table...
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

        // Add each person to the table
        //   Use the `name` column family for the name
        //   Use the `contactinfo` column family for the email
        for (int i = 0; i< people.length; i++) {
            Put person = new Put(Bytes.toBytes(people[i][0]));
            person.add(Bytes.toBytes("name"), Bytes.toBytes("first"), Bytes.toBytes(people[i][1]));
            person.add(Bytes.toBytes("name"), Bytes.toBytes("last"), Bytes.toBytes(people[i][2]));
            person.add(Bytes.toBytes("contactinfo"), Bytes.toBytes("email"), Bytes.toBytes(people[i][3]));
            table.put(person);
        }
        // flush commits and close the table
        table.flushCommits();
        table.close();
        }
    }
   ```

    <span data-ttu-id="22a18-164">Esse código é a classe **CreateTable**, que cria uma tabela chamada **pessoas** e a preenche com alguns usuários predefinidos.</span><span class="sxs-lookup"><span data-stu-id="22a18-164">This code is the **CreateTable** class, which creates a table named **people** and populate it with some predefined users.</span></span>

3. <span data-ttu-id="22a18-165">Salve o arquivo `CreateTable.java`.</span><span class="sxs-lookup"><span data-stu-id="22a18-165">Save the `CreateTable.java` file.</span></span>

4. <span data-ttu-id="22a18-166">No diretório `hbaseapp/src/main/java/com/microsoft/examples`, crie um novo arquivo chamado `SearchByEmail.java`.</span><span class="sxs-lookup"><span data-stu-id="22a18-166">In the `hbaseapp/src/main/java/com/microsoft/examples` directory, create a file named `SearchByEmail.java`.</span></span> <span data-ttu-id="22a18-167">Use o seguinte texto como o conteúdo deste arquivo:</span><span class="sxs-lookup"><span data-stu-id="22a18-167">Use the following text as the contents of this file:</span></span>

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

        // Use GenericOptionsParser to get only the parameters to the class
        // and not all the parameters passed (when using WebHCat for example)
        String[] otherArgs = new GenericOptionsParser(config, args).getRemainingArgs();
        if (otherArgs.length != 1) {
            System.out.println("usage: [regular expression]");
            System.exit(-1);
        }

        // Open the table
        HTable table = new HTable(config, "people");

        // Define the family and qualifiers to be used
        byte[] contactFamily = Bytes.toBytes("contactinfo");
        byte[] emailQualifier = Bytes.toBytes("email");
        byte[] nameFamily = Bytes.toBytes("name");
        byte[] firstNameQualifier = Bytes.toBytes("first");
        byte[] lastNameQualifier = Bytes.toBytes("last");

        // Create a regex filter
        RegexStringComparator emailFilter = new RegexStringComparator(otherArgs[0]);
        // Attach the regex filter to a filter
        //   for the email column
        SingleColumnValueFilter filter = new SingleColumnValueFilter(
            contactFamily,
            emailQualifier,
            CompareOp.EQUAL,
            emailFilter
        );

        // Create a scan and set the filter
        Scan scan = new Scan();
        scan.setFilter(filter);

        // Get the results
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

    <span data-ttu-id="22a18-168">A classe **SearchByEmail** pode ser usada para consultar por linhas, por endereço de email.</span><span class="sxs-lookup"><span data-stu-id="22a18-168">The **SearchByEmail** class can be used to query for rows by email address.</span></span> <span data-ttu-id="22a18-169">Já que ele utiliza um filtro de expressão comum, você pode fornecer uma cadeia de caracteres ou então uma expressão comum ao utilizar a classe.</span><span class="sxs-lookup"><span data-stu-id="22a18-169">Because it uses a regular expression filter, you can provide either a string or a regular expression when using the class.</span></span>

5. <span data-ttu-id="22a18-170">Salve o arquivo `SearchByEmail.java`.</span><span class="sxs-lookup"><span data-stu-id="22a18-170">Save the `SearchByEmail.java` file.</span></span>

6. <span data-ttu-id="22a18-171">No diretório `hbaseapp/src/main/hava/com/microsoft/examples`, crie um novo arquivo chamado `DeleteTable.java`.</span><span class="sxs-lookup"><span data-stu-id="22a18-171">In the `hbaseapp/src/main/hava/com/microsoft/examples` directory, create a file named `DeleteTable.java`.</span></span> <span data-ttu-id="22a18-172">Use o seguinte texto como o conteúdo deste arquivo:</span><span class="sxs-lookup"><span data-stu-id="22a18-172">Use the following text as the contents of this file:</span></span>

   ```java
    package com.microsoft.examples;
    import java.io.IOException;

    import org.apache.hadoop.conf.Configuration;
    import org.apache.hadoop.hbase.HBaseConfiguration;
    import org.apache.hadoop.hbase.client.HBaseAdmin;

    public class DeleteTable {
        public static void main(String[] args) throws IOException {
        Configuration config = HBaseConfiguration.create();

        // Create an admin object using the config
        HBaseAdmin admin = new HBaseAdmin(config);

        // Disable, and then delete the table
        admin.disableTable("people");
        admin.deleteTable("people");
        }
    }
   ```

    <span data-ttu-id="22a18-173">Essa classe limpa as tabelas HBase criadas nesse exemplo desabilitando e eliminando a tabela criada pela classe `CreateTable`.</span><span class="sxs-lookup"><span data-stu-id="22a18-173">This class cleans up the HBase tables created in this example by disabling and dropping the table created by the `CreateTable` class.</span></span>

7. <span data-ttu-id="22a18-174">Salve o arquivo `DeleteTable.java`.</span><span class="sxs-lookup"><span data-stu-id="22a18-174">Save the `DeleteTable.java` file.</span></span>

## <a name="build-and-package-the-application"></a><span data-ttu-id="22a18-175">Compilar e criar o pacote do aplicativo</span><span class="sxs-lookup"><span data-stu-id="22a18-175">Build and package the application</span></span>

1. <span data-ttu-id="22a18-176">Use o diretório `hbaseapp`, use o comando a seguir para compilar um arquivo JAR que contém o aplicativo:</span><span class="sxs-lookup"><span data-stu-id="22a18-176">From the `hbaseapp` directory, use the following command to build a JAR file that contains the application:</span></span>

    ```bash
    mvn clean package
    ```

    <span data-ttu-id="22a18-177">Este comando compila e empacota o aplicativo em um arquivo .jar.</span><span class="sxs-lookup"><span data-stu-id="22a18-177">This command builds and packages the application into a .jar file.</span></span>

2. <span data-ttu-id="22a18-178">Após a conclusão do comando, o diretório `hbaseapp/target` conterá um arquivo chamado `hbaseapp-1.0-SNAPSHOT.jar`.</span><span class="sxs-lookup"><span data-stu-id="22a18-178">When the command completes, the `hbaseapp/target` directory contains a file named `hbaseapp-1.0-SNAPSHOT.jar`.</span></span>

   > [!NOTE]
   > <span data-ttu-id="22a18-179">O arquivo `hbaseapp-1.0-SNAPSHOT.jar` é um uber jar.</span><span class="sxs-lookup"><span data-stu-id="22a18-179">The `hbaseapp-1.0-SNAPSHOT.jar` file is an uber jar.</span></span> <span data-ttu-id="22a18-180">Ele contém todas as dependências exigidas para executar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="22a18-180">It contains all the dependencies required to run the application.</span></span>


## <a name="upload-the-jar-and-run-jobs-ssh"></a><span data-ttu-id="22a18-181">Carregue o arquivo JAR e execute trabalhos (SSH)</span><span class="sxs-lookup"><span data-stu-id="22a18-181">Upload the JAR and run jobs (SSH)</span></span>

<span data-ttu-id="22a18-182">As etapas a seguir usam `scp` para copiar o arquivo JAR no nó principal de seu HBase no cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="22a18-182">The following steps use `scp` to copy the JAR to the primary head node of your HBase on HDInsight cluster.</span></span> <span data-ttu-id="22a18-183">Então, o comando `ssh` será utilizado para se conectar ao cluster e executar o exemplo diretamente no nó principal.</span><span class="sxs-lookup"><span data-stu-id="22a18-183">The `ssh` command is then used to connect to the cluster and run the example directly on the head node.</span></span>

1. <span data-ttu-id="22a18-184">Use o comando a seguir para carregar o jar no cluster:</span><span class="sxs-lookup"><span data-stu-id="22a18-184">To upload the jar to the cluster, use the following command:</span></span>

    ```bash
    scp ./target/hbaseapp-1.0-SNAPSHOT.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:hbaseapp-1.0-SNAPSHOT.jar
    ```

    <span data-ttu-id="22a18-185">Substitua `USERNAME` pelo nome de seu logon SSH.</span><span class="sxs-lookup"><span data-stu-id="22a18-185">Replace `USERNAME` with the name of your SSH login.</span></span> <span data-ttu-id="22a18-186">Substitua o `CLUSTERNAME` pelo nome do seu cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="22a18-186">Replace `CLUSTERNAME` with your HDInsight cluster name.</span></span>

2. <span data-ttu-id="22a18-187">Use o comando a seguir para se conectar ao cluster HBase:</span><span class="sxs-lookup"><span data-stu-id="22a18-187">To connect to the HBase cluster, use the following command:</span></span>

    ```bash
    ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
    ```

    <span data-ttu-id="22a18-188">Substitua `USERNAME` pelo nome de seu logon SSH.</span><span class="sxs-lookup"><span data-stu-id="22a18-188">Replace `USERNAME` the name of your SSH login.</span></span> <span data-ttu-id="22a18-189">Substitua o `CLUSTERNAME` pelo nome do seu cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="22a18-189">Replace `CLUSTERNAME` with your HDInsight cluster name.</span></span>

3. <span data-ttu-id="22a18-190">Use o seguinte comando para criar uma tabela do HBase usando o aplicativo Java:</span><span class="sxs-lookup"><span data-stu-id="22a18-190">To create an HBase table using the Java application, use the following command:</span></span>

    ```bash
    yarn jar hbaseapp-1.0-SNAPSHOT.jar com.microsoft.examples.CreateTable
    ```

    <span data-ttu-id="22a18-191">Esse comando cria uma nova tabela do HBase chamada **people** e a preenche com dados.</span><span class="sxs-lookup"><span data-stu-id="22a18-191">This command creates a HBase table named **people**, and populates it with data.</span></span>

4. <span data-ttu-id="22a18-192">Use o seguinte comando para procurar endereços de email armazenados na tabela:</span><span class="sxs-lookup"><span data-stu-id="22a18-192">To search for email addresses stored in the table, use the following command:</span></span>

    ```bash
    yarn jar hbaseapp-1.0-SNAPSHOT.jar com.microsoft.examples.SearchByEmail contoso.com
    ```

    <span data-ttu-id="22a18-193">Você receberá as resultados a seguir:</span><span class="sxs-lookup"><span data-stu-id="22a18-193">You receive the following results:</span></span>

        Franklin Holtz - ID: 2
        Franklin Holtz - franklin@contoso.com - ID: 2
        Rae Schroeder - ID: 4
        Rae Schroeder - rae@contoso.com - ID: 4
        Gabriela Ingram - ID: 6
        Gabriela Ingram - gabriela@contoso.com - ID: 6

5. <span data-ttu-id="22a18-194">Para excluir a tabela, use o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="22a18-194">To delete the table, use the following command:</span></span>

    

## <a name="upload-the-jar-and-run-jobs-powershell"></a><span data-ttu-id="22a18-195">Carregue o arquivo JAR e execute trabalhos (PowerShell)</span><span class="sxs-lookup"><span data-stu-id="22a18-195">Upload the JAR and run jobs (PowerShell)</span></span>

<span data-ttu-id="22a18-196">As etapas a seguir usam o Azure PowerShell para carregar o arquivo JAR para o armazenamento padrão do cluster HBase.</span><span class="sxs-lookup"><span data-stu-id="22a18-196">The following steps use Azure PowerShell to upload the JAR to the default storage for your HBase cluster.</span></span> <span data-ttu-id="22a18-197">Os cmdlets do HDInsight serão usados para executar os exemplos remotamente.</span><span class="sxs-lookup"><span data-stu-id="22a18-197">HDInsight cmdlets are then used to run the examples remotely.</span></span>

1. <span data-ttu-id="22a18-198">Após instalar e configurar o Azure PowerShell, crie um arquivo chamado `hbase-runner.psm1`.</span><span class="sxs-lookup"><span data-stu-id="22a18-198">After installing and configuring Azure PowerShell, create a file named `hbase-runner.psm1`.</span></span> <span data-ttu-id="22a18-199">Use o seguinte texto como o conteúdo deste arquivo:</span><span class="sxs-lookup"><span data-stu-id="22a18-199">Use the following text as the contents of this file:</span></span>

   ```powershell
    <#
    .SYNOPSIS
    Copies a file to the primary storage of an HDInsight cluster.
    .DESCRIPTION
    Copies a file from a local directory to the blob container for
    the HDInsight cluster.
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
    #The class to run
    [Parameter(Mandatory = $true)]
    [String]$className,

    #The name of the HDInsight cluster
    [Parameter(Mandatory = $true)]
    [String]$clusterName,

    #Only used when using SearchByEmail
    [Parameter(Mandatory = $false)]
    [String]$emailRegex,

    #Use if you want to see stderr output
    [Parameter(Mandatory = $false)]
    [Switch]$showErr
    )

    Set-StrictMode -Version 3

    # Is the Azure module installed?
    FindAzure

    # Get the login for the HDInsight cluster
    $creds=Get-Credential -Message "Enter the login for the cluster" -UserName "admin"

    # The JAR
    $jarFile = "wasb:///example/jars/hbaseapp-1.0-SNAPSHOT.jar"

    # The job definition
    $jobDefinition = New-AzureRmHDInsightMapReduceJobDefinition `
        -JarFile $jarFile `
        -ClassName $className `
        -Arguments $emailRegex

    # Get the job output
    $job = Start-AzureRmHDInsightJob `
        -ClusterName $clusterName `
        -JobDefinition $jobDefinition `
        -HttpCredential $creds
    Write-Host "Wait for the job to complete ..." -ForegroundColor Green
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
    Write-Host "Display the standard output ..." -ForegroundColor Green
    Get-AzureRmHDInsightJobOutput `
                -Clustername $clusterName `
                -JobId $job.JobId `
                -HttpCredential $creds
    }

    <#
    .SYNOPSIS
    Copies a file to the primary storage of an HDInsight cluster.
    .DESCRIPTION
    Copies a file from a local directory to the blob container for
    the HDInsight cluster.
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
            #The path to the local file.
            [Parameter(Mandatory = $true)]
            [String]$localPath,

            #The destination path and file name, relative to the root of the container.
            [Parameter(Mandatory = $true)]
            [String]$destinationPath,

            #The name of the HDInsight cluster
            [Parameter(Mandatory = $true)]
            [String]$clusterName,

            #If specified, overwrites existing files without prompting
            [Parameter(Mandatory = $false)]
            [Switch]$force
        )

        Set-StrictMode -Version 3

        # Is the Azure module installed?
        FindAzure

        # Get authentication for the cluster
        $creds=Get-Credential

        # Does the local path exist?
        if (-not (Test-Path $localPath))
        {
            throw "Source path '$localPath' does not exist."
        }

        # Get the primary storage container
        $storage = GetStorage -clusterName $clusterName

        # Upload file to storage, overwriting existing files if -force was used.
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
            throw "No active Azure subscription found! If you have a subscription, use the Login-AzureRmAccount cmdlet to login to your subscription."
        }
    }

    function GetStorage {
        param(
            [Parameter(Mandatory = $true)]
            [String]$clusterName
        )
        $hdi = Get-AzureRmHDInsightCluster -ClusterName $clusterName
        # Does the cluster exist?
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
        # Get the resource group, in case we need that
        $return.resourceGroup = $resourceGroup
        # Get the storage context, as we can't depend
        # on using the default storage context
        $return.context = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey
        # Get the container, so we know where to
        # find/store blobs
        $return.container = $container
        # Return storage accounts to support finding all accounts for
        # a cluster
        $return.storageAccount = $storageAccountName
        $return.storageAccountKey = $storageAccountKey

        return $return
    }
    # Only export the verb-phrase things
    export-modulemember *-*
   ```

    <span data-ttu-id="22a18-200">Esse arquivo contém dois módulos:</span><span class="sxs-lookup"><span data-stu-id="22a18-200">This file contains two modules:</span></span>

   * <span data-ttu-id="22a18-201">**Add-HDInsightFile** – utilizado para carregar arquivos no cluster</span><span class="sxs-lookup"><span data-stu-id="22a18-201">**Add-HDInsightFile** - used to upload files to the cluster</span></span>
   * <span data-ttu-id="22a18-202">**Start-HBaseExample** - utilizado para executar as classes criadas anteriormente</span><span class="sxs-lookup"><span data-stu-id="22a18-202">**Start-HBaseExample** - used to run the classes created earlier</span></span>

2. <span data-ttu-id="22a18-203">Salve o arquivo `hbase-runner.psm1`.</span><span class="sxs-lookup"><span data-stu-id="22a18-203">Save the `hbase-runner.psm1` file.</span></span>

3. <span data-ttu-id="22a18-204">Abra uma nova janela do Azure PowerShell, altere os diretórios para o diretório `hbaseapp` e execute o comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="22a18-204">Open a new Azure PowerShell window, change directories to the `hbaseapp` directory, and then run the following command:</span></span>

    ```powershell
    PS C:\ Import-Module c:\path\to\hbase-runner.psm1
    ```

    <span data-ttu-id="22a18-205">Altere o caminho até o local do arquivo `hbase-runner.psm1` criado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="22a18-205">Change the path to the location of the `hbase-runner.psm1` file created earlier.</span></span> <span data-ttu-id="22a18-206">Esse comando registra o módulo com o Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="22a18-206">This command registers the module with Azure PowerShell.</span></span>

4. <span data-ttu-id="22a18-207">Use o comando a seguir para carregar o `hbaseapp-1.0-SNAPSHOT.jar` em seu cluster.</span><span class="sxs-lookup"><span data-stu-id="22a18-207">Use the following command to upload the `hbaseapp-1.0-SNAPSHOT.jar` to your cluster.</span></span>

    ```powershell
    Add-HDInsightFile -localPath target\hbaseapp-1.0-SNAPSHOT.jar -destinationPath example/jars/hbaseapp-1.0-SNAPSHOT.jar -clusterName hdinsightclustername
    ```

    <span data-ttu-id="22a18-208">Substitua `hdinsightclustername` pelo nome do cluster.</span><span class="sxs-lookup"><span data-stu-id="22a18-208">Replace `hdinsightclustername` with the name of your cluster.</span></span> <span data-ttu-id="22a18-209">O comando carrega o `hbaseapp-1.0-SNAPSHOT.jar` no local `example/jars` no armazenamento primário do cluster.</span><span class="sxs-lookup"><span data-stu-id="22a18-209">The command uploads the `hbaseapp-1.0-SNAPSHOT.jar` to the `example/jars` location in the primary storage for your cluster.</span></span>

5. <span data-ttu-id="22a18-210">Para criar uma tabela usando `hbaseapp`, use o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="22a18-210">To create a table using the `hbaseapp`, use the following command:</span></span>

    ```powershell
    Start-HBaseExample -className com.microsoft.examples.CreateTable -clusterName hdinsightclustername
    ```

    <span data-ttu-id="22a18-211">Substitua `hdinsightclustername` pelo nome do cluster.</span><span class="sxs-lookup"><span data-stu-id="22a18-211">Replace `hdinsightclustername` with the name of your cluster.</span></span>

    <span data-ttu-id="22a18-212">Esse comando cria uma tabela chamada **people** no HBase em seu cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="22a18-212">This command creates a table named **people** in HBase on your HDInsight cluster.</span></span> <span data-ttu-id="22a18-213">Esse comando não mostra nenhuma saída na janela do console.</span><span class="sxs-lookup"><span data-stu-id="22a18-213">This command does not show any output in the console window.</span></span>

6. <span data-ttu-id="22a18-214">Para procurar por entradas na tabela, use o comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="22a18-214">To search for entries in the table, use the following command:</span></span>

    ```powershell
    Start-HBaseExample -className com.microsoft.examples.SearchByEmail -clusterName hdinsightclustername -emailRegex contoso.com
    ```

    <span data-ttu-id="22a18-215">Substitua `hdinsightclustername` pelo nome do cluster.</span><span class="sxs-lookup"><span data-stu-id="22a18-215">Replace `hdinsightclustername` with the name of your cluster.</span></span>

    <span data-ttu-id="22a18-216">Esse comando usa a classe `SearchByEmail` para procurar por quaisquer linhas nas quais a família de colunas `contactinformation` e a coluna `email` contenham a cadeia de caracteres `contoso.com`.</span><span class="sxs-lookup"><span data-stu-id="22a18-216">This command uses the `SearchByEmail` class to search for any rows where the `contactinformation` column family and the `email` column, contains the string `contoso.com`.</span></span> <span data-ttu-id="22a18-217">Você deve receber os seguintes resultados:</span><span class="sxs-lookup"><span data-stu-id="22a18-217">You should receive the following results:</span></span>

          Franklin Holtz - ID: 2
          Franklin Holtz - franklin@contoso.com - ID: 2
          Rae Schroeder - ID: 4
          Rae Schroeder - rae@contoso.com - ID: 4
          Gabriela Ingram - ID: 6
          Gabriela Ingram - gabriela@contoso.com - ID: 6

    <span data-ttu-id="22a18-218">Usar **fabrikam.com** como o valor de `-emailRegex` retornará os usuários que tenham **fabrikam.com** no campo de email.</span><span class="sxs-lookup"><span data-stu-id="22a18-218">Using **fabrikam.com** for the `-emailRegex` value returns the users that have **fabrikam.com** in the email field.</span></span> <span data-ttu-id="22a18-219">Você também pode usar expressões regulares como o termo de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="22a18-219">You can also use regular expressions as the search term.</span></span> <span data-ttu-id="22a18-220">Por exemplo, **^ r** retorna endereços que começam com a letra 'r'.</span><span class="sxs-lookup"><span data-stu-id="22a18-220">For example, **^r** returns email addresses that begin with the letter 'r'.</span></span>

### <a name="no-results-or-unexpected-results-when-using-start-hbaseexample"></a><span data-ttu-id="22a18-221">Nenhum resultado ou resultados inesperados ao usar o Start-HBaseExample</span><span class="sxs-lookup"><span data-stu-id="22a18-221">No results or unexpected results when using Start-HBaseExample</span></span>

<span data-ttu-id="22a18-222">Utilize o parâmetro `-showErr` para exibir o erro padrão (STDERR) produzido durante a execução do trabalho.</span><span class="sxs-lookup"><span data-stu-id="22a18-222">Use the `-showErr` parameter to view the standard error (STDERR) that is produced while running the job.</span></span>

## <a name="delete-the-table"></a><span data-ttu-id="22a18-223">Excluir a tabela</span><span class="sxs-lookup"><span data-stu-id="22a18-223">Delete the table</span></span>

<span data-ttu-id="22a18-224">Após ter terminado o exemplo, use o seguinte para excluir a tabela **pessoas** utilizada neste exemplo:</span><span class="sxs-lookup"><span data-stu-id="22a18-224">When you are done with the example, use the following to delete the **people** table used in this example:</span></span>

<span data-ttu-id="22a18-225">__De uma sessão `ssh`__:</span><span class="sxs-lookup"><span data-stu-id="22a18-225">__From an `ssh` session__:</span></span>

`yarn jar hbaseapp-1.0-SNAPSHOT.jar com.microsoft.examples.DeleteTable`

<span data-ttu-id="22a18-226">__Do Azure PowerShell__:</span><span class="sxs-lookup"><span data-stu-id="22a18-226">__From Azure PowerShell__:</span></span>

`Start-HBaseExample -className com.microsoft.examples.DeleteTable -clusterName hdinsightclustername`

## <a name="next-steps"></a><span data-ttu-id="22a18-227">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="22a18-227">Next steps</span></span>

[<span data-ttu-id="22a18-228">Saiba como usar o SQuirreL SQL com o HBase</span><span class="sxs-lookup"><span data-stu-id="22a18-228">Learn how to use SQuirreL SQL with HBase</span></span>](hdinsight-hbase-phoenix-squirrel-linux.md)
