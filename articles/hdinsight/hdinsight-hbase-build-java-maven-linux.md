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
# <a name="build-java-applications-for-apache-hbase"></a><span data-ttu-id="408cb-103">Compilar aplicativos Java para Apache HBase</span><span class="sxs-lookup"><span data-stu-id="408cb-103">Build Java applications for Apache HBase</span></span>

<span data-ttu-id="408cb-104">Saiba como toocreate uma [HBase Apache](http://hbase.apache.org/) aplicativo em Java.</span><span class="sxs-lookup"><span data-stu-id="408cb-104">Learn how toocreate an [Apache HBase](http://hbase.apache.org/) application in Java.</span></span> <span data-ttu-id="408cb-105">Em seguida, use o aplicativo hello com HBase em HDInsight do Azure.</span><span class="sxs-lookup"><span data-stu-id="408cb-105">Then use hello application with HBase on Azure HDInsight.</span></span>

<span data-ttu-id="408cb-106">Olá as etapas deste documento usam [Maven](http://maven.apache.org/) toocreate e compilação do projeto de saudação.</span><span class="sxs-lookup"><span data-stu-id="408cb-106">hello steps in this document use [Maven](http://maven.apache.org/) toocreate and build hello project.</span></span> <span data-ttu-id="408cb-107">Maven é uma ferramenta de compreensão que permite que você toobuild software, documentação e relatórios para projetos Java e o gerenciamento de projeto de software.</span><span class="sxs-lookup"><span data-stu-id="408cb-107">Maven is a software project management and comprehension tool that allows you toobuild software, documentation, and reports for Java projects.</span></span>

> [!NOTE]
> <span data-ttu-id="408cb-108">Olá etapas neste documento foram recentemente testadas com HDInsight 3.6.</span><span class="sxs-lookup"><span data-stu-id="408cb-108">hello steps in this document were most recently tested with HDInsight 3.6.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="408cb-109">etapas de saudação neste documento exigem um cluster HDInsight que usa o Linux.</span><span class="sxs-lookup"><span data-stu-id="408cb-109">hello steps in this document require an HDInsight cluster that uses Linux.</span></span> <span data-ttu-id="408cb-110">Linux é Olá sistema operacional somente de usado no HDInsight versão 3.4 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="408cb-110">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="408cb-111">Para obter mais informações, confira [baixa do HDInsight no Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="408cb-111">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <a name="requirements"></a><span data-ttu-id="408cb-112">Requisitos</span><span class="sxs-lookup"><span data-stu-id="408cb-112">Requirements</span></span>

* <span data-ttu-id="408cb-113">[Plataforma Java JDK](http://www.oracle.com/technetwork/java/javase/downloads/index.html) 8 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="408cb-113">[Java platform JDK](http://www.oracle.com/technetwork/java/javase/downloads/index.html) 8 or later.</span></span>

    > [!NOTE]
    > <span data-ttu-id="408cb-114">O HDInsight 3.5 e posterior usa Java 8.</span><span class="sxs-lookup"><span data-stu-id="408cb-114">HDInsight 3.5 and greater requires Java 8.</span></span> <span data-ttu-id="408cb-115">Versões anteriores do HDInsight requerem Java 7.</span><span class="sxs-lookup"><span data-stu-id="408cb-115">Earlier versions of HDInsight require Java 7.</span></span>

* [<span data-ttu-id="408cb-116">Maven</span><span class="sxs-lookup"><span data-stu-id="408cb-116">Maven</span></span>](http://maven.apache.org/)

* [<span data-ttu-id="408cb-117">Um cluster HDInsight do Azure baseado em Linux com HBase</span><span class="sxs-lookup"><span data-stu-id="408cb-117">A Linux-based Azure HDInsight cluster with HBase</span></span>](hdinsight-hbase-tutorial-get-started-linux.md#create-hbase-cluster)

  > [!NOTE]
  > <span data-ttu-id="408cb-118">Olá etapas neste documento foram testadas com as versões de cluster HDInsight 3.4 e 3.5.</span><span class="sxs-lookup"><span data-stu-id="408cb-118">hello steps in this document have been tested with HDInsight cluster versions 3.4 and 3.5.</span></span> <span data-ttu-id="408cb-119">valores padrão de saudação fornecidos nos exemplos são para um cluster HDInsight 3.5.</span><span class="sxs-lookup"><span data-stu-id="408cb-119">hello default values provided in examples are for a HDInsight 3.5 cluster.</span></span>

## <a name="create-hello-project"></a><span data-ttu-id="408cb-120">Criar projeto Olá</span><span class="sxs-lookup"><span data-stu-id="408cb-120">Create hello project</span></span>

1. <span data-ttu-id="408cb-121">Na linha de comando de saudação em seu ambiente de desenvolvimento, alterar o local de toohello de diretórios em que você deseja toocreate Olá projeto, por exemplo, `cd code\hbase`.</span><span class="sxs-lookup"><span data-stu-id="408cb-121">From hello command line in your development environment, change directories toohello location where you want toocreate hello project, for example, `cd code\hbase`.</span></span>

2. <span data-ttu-id="408cb-122">Saudação de uso **mvn** comando, que é instalado com o Maven, Olá toogenerate estrutura do projeto de saudação.</span><span class="sxs-lookup"><span data-stu-id="408cb-122">Use hello **mvn** command, which is installed with Maven, toogenerate hello scaffolding for hello project.</span></span>

    ```bash
    mvn archetype:generate -DgroupId=com.microsoft.examples -DartifactId=hbaseapp -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
    ```

    > [!NOTE]
    > <span data-ttu-id="408cb-123">Se você estiver usando o PowerShell, você deverá colocar Olá `-D` parâmetros entre aspas duplas.</span><span class="sxs-lookup"><span data-stu-id="408cb-123">If you are using PowerShell, you must enclose hello `-D` parameters in double quotes.</span></span>
    >
    > `mvn archetype:generate "-DgroupId=com.microsoft.examples" "-DartifactId=hbaseapp" "-DarchetypeArtifactId=maven-archetype-quickstart" "-DinteractiveMode=false"`

    <span data-ttu-id="408cb-124">Este comando cria um diretório com hello mesmo nome como Olá **artifactID** parâmetro (**hbaseapp** neste exemplo.) Este diretório contém Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="408cb-124">This command creates a directory with hello same name as hello **artifactID** parameter (**hbaseapp** in this example.) This directory contains hello following items:</span></span>

   * <span data-ttu-id="408cb-125">**POM.XML**: Olá o modelo de objeto do projeto ([POM](http://maven.apache.org/guides/introduction/introduction-to-the-pom.html)) contém informações e configuração detalhes usados toobuild Olá projeto.</span><span class="sxs-lookup"><span data-stu-id="408cb-125">**pom.xml**:  hello Project Object Model ([POM](http://maven.apache.org/guides/introduction/introduction-to-the-pom.html)) contains information and configuration details used toobuild hello project.</span></span>
   * <span data-ttu-id="408cb-126">**src**: diretório de saudação que contém a saudação **principal/java/com/microsoft/exemplos** directory, onde você cria o aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="408cb-126">**src**: hello directory that contains hello **main/java/com/microsoft/examples** directory, where you author hello application.</span></span>

3. <span data-ttu-id="408cb-127">Excluir Olá `src/test/java/com/microsoft/examples/apptest.java` arquivo.</span><span class="sxs-lookup"><span data-stu-id="408cb-127">Delete hello `src/test/java/com/microsoft/examples/apptest.java` file.</span></span> <span data-ttu-id="408cb-128">Ele não será usado neste exemplo.</span><span class="sxs-lookup"><span data-stu-id="408cb-128">It is not be used in this example.</span></span>

## <a name="update-hello-project-object-model"></a><span data-ttu-id="408cb-129">Saudação de atualizar o modelo de objeto de projeto</span><span class="sxs-lookup"><span data-stu-id="408cb-129">Update hello Project Object Model</span></span>

1. <span data-ttu-id="408cb-130">Editar saudação `pom.xml` de arquivos e adicionar Olá seguindo o código dentro de saudação `<dependencies>` seção:</span><span class="sxs-lookup"><span data-stu-id="408cb-130">Edit hello `pom.xml` file and add hello following code inside hello `<dependencies>` section:</span></span>

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

    <span data-ttu-id="408cb-131">Esta seção indica que o projeto Olá deve **hbase cliente** e **phoenix core** componentes.</span><span class="sxs-lookup"><span data-stu-id="408cb-131">This section indicates that hello project needs **hbase-client** and **phoenix-core** components.</span></span> <span data-ttu-id="408cb-132">Em tempo de compilação, essas dependências são baixadas do repositório de Maven saudação padrão.</span><span class="sxs-lookup"><span data-stu-id="408cb-132">At compile time, these dependencies are downloaded from hello default Maven repository.</span></span> <span data-ttu-id="408cb-133">Você pode usar o hello [pesquisa de repositório Central Maven](http://search.maven.org/#artifactdetails%7Corg.apache.hbase%7Chbase-client%7C0.98.4-hadoop2%7Cjar) toolearn mais sobre essa dependência.</span><span class="sxs-lookup"><span data-stu-id="408cb-133">You can use hello [Maven Central Repository Search](http://search.maven.org/#artifactdetails%7Corg.apache.hbase%7Chbase-client%7C0.98.4-hadoop2%7Cjar) toolearn more about this dependency.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="408cb-134">número de versão de saudação do hbase Olá-cliente deve corresponder a versão de saudação do HBase que é fornecido com o seu cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="408cb-134">hello version number of hello hbase-client must match hello version of HBase that is provided with your HDInsight cluster.</span></span> <span data-ttu-id="408cb-135">Use Olá número de versão correta de saudação de toofind tabela a seguir.</span><span class="sxs-lookup"><span data-stu-id="408cb-135">Use hello following table toofind hello correct version number.</span></span>

   | <span data-ttu-id="408cb-136">Versão do cluster HDInsight</span><span class="sxs-lookup"><span data-stu-id="408cb-136">HDInsight cluster version</span></span> | <span data-ttu-id="408cb-137">Toouse de versão do HBase</span><span class="sxs-lookup"><span data-stu-id="408cb-137">HBase version toouse</span></span> |
   | --- | --- |
   | <span data-ttu-id="408cb-138">3.2</span><span class="sxs-lookup"><span data-stu-id="408cb-138">3.2</span></span> |<span data-ttu-id="408cb-139">0.98.4-hadoop2</span><span class="sxs-lookup"><span data-stu-id="408cb-139">0.98.4-hadoop2</span></span> |
   | <span data-ttu-id="408cb-140">3.3, 3.4, 3.5 e 3.6</span><span class="sxs-lookup"><span data-stu-id="408cb-140">3.3, 3.4, 3.5, and 3.6</span></span> |<span data-ttu-id="408cb-141">1.1.2</span><span class="sxs-lookup"><span data-stu-id="408cb-141">1.1.2</span></span> |

    <span data-ttu-id="408cb-142">Para obter mais informações sobre as versões de HDInsight e componentes, consulte [quais são Olá Hadoop componentes diferentes disponíveis com o HDInsight](hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="408cb-142">For more information on HDInsight versions and components, see [What are hello different Hadoop components available with HDInsight](hdinsight-component-versioning.md).</span></span>

3. <span data-ttu-id="408cb-143">Adicionar Olá toohello de código a seguir **pom.xml** arquivo.</span><span class="sxs-lookup"><span data-stu-id="408cb-143">Add hello following code toohello **pom.xml** file.</span></span> <span data-ttu-id="408cb-144">Esse texto deve estar dentro de saudação `<project>...</project>` marcas de saudação do arquivo, por exemplo, entre `</dependencies>` e `</project>`.</span><span class="sxs-lookup"><span data-stu-id="408cb-144">This text must be inside hello `<project>...</project>` tags in hello file, for example, between `</dependencies>` and `</project>`.</span></span>

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

    <span data-ttu-id="408cb-145">Esta seção configura um recurso (`conf/hbase-site.xml`), que contém informações de configuração para o HBase.</span><span class="sxs-lookup"><span data-stu-id="408cb-145">This section configures a resource (`conf/hbase-site.xml`) that contains configuration information for HBase.</span></span>

   > [!NOTE]
   > <span data-ttu-id="408cb-146">Você também pode definir valores de configuração via código.</span><span class="sxs-lookup"><span data-stu-id="408cb-146">You can also set configuration values via code.</span></span> <span data-ttu-id="408cb-147">Consulte comentários Olá Olá `CreateTable` exemplo.</span><span class="sxs-lookup"><span data-stu-id="408cb-147">See hello comments in hello `CreateTable` example.</span></span>

    <span data-ttu-id="408cb-148">Esta seção também configura Olá [plug-in de compilador Maven](http://maven.apache.org/plugins/maven-compiler-plugin/) e [plug-in de sombra Maven](http://maven.apache.org/plugins/maven-shade-plugin/).</span><span class="sxs-lookup"><span data-stu-id="408cb-148">This section also configures hello [Maven Compiler Plugin](http://maven.apache.org/plugins/maven-compiler-plugin/) and [Maven Shade Plugin](http://maven.apache.org/plugins/maven-shade-plugin/).</span></span> <span data-ttu-id="408cb-149">compilador de saudação plug-in é usado toocompile Olá topologia.</span><span class="sxs-lookup"><span data-stu-id="408cb-149">hello compiler plug-in is used toocompile hello topology.</span></span> <span data-ttu-id="408cb-150">Sombreamento de saudação plug-in é usado tooprevent eliminação de duplicação de licença no pacote JAR Olá que é criada pelo Maven.</span><span class="sxs-lookup"><span data-stu-id="408cb-150">hello shade plug-in is used tooprevent license duplication in hello JAR package that is built by Maven.</span></span> <span data-ttu-id="408cb-151">Este plug-in é usado tooprevent um erro "a duplicação de arquivos de licença" em tempo de execução no cluster do HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="408cb-151">This plugin is used tooprevent a "duplicate license files" error at run time on hello HDInsight cluster.</span></span> <span data-ttu-id="408cb-152">Usando o plugin do maven sombreamento com hello `ApacheLicenseResourceTransformer` implementação impede que o erro de saudação.</span><span class="sxs-lookup"><span data-stu-id="408cb-152">Using maven-shade-plugin with hello `ApacheLicenseResourceTransformer` implementation prevents hello error.</span></span>

    <span data-ttu-id="408cb-153">Olá maven tonalidade plugin também produz um jar grande que contém todas as dependências de Olá exigidas pelo aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="408cb-153">hello maven-shade-plugin also produces an uber jar that contains all hello dependencies required by hello application.</span></span>

4. <span data-ttu-id="408cb-154">Salvar Olá `pom.xml` arquivo.</span><span class="sxs-lookup"><span data-stu-id="408cb-154">Save hello `pom.xml` file.</span></span>

5. <span data-ttu-id="408cb-155">Crie um diretório chamado `conf` em Olá `hbaseapp` directory.</span><span class="sxs-lookup"><span data-stu-id="408cb-155">Create a directory named `conf` in hello `hbaseapp` directory.</span></span> <span data-ttu-id="408cb-156">Este diretório é usado toohold informações de configuração para conectar-se tooHBase.</span><span class="sxs-lookup"><span data-stu-id="408cb-156">This directory is used toohold configuration information for connecting tooHBase.</span></span>

6. <span data-ttu-id="408cb-157">Comando a seguir de saudação de uso HBase configuração Olá toocopy Olá HBase cluster toohello `conf` directory.</span><span class="sxs-lookup"><span data-stu-id="408cb-157">Use hello following command toocopy hello HBase configuration from hello HBase cluster toohello `conf` directory.</span></span> <span data-ttu-id="408cb-158">Substituir `USERNAME` com o nome de saudação do seu logon SSH.</span><span class="sxs-lookup"><span data-stu-id="408cb-158">Replace `USERNAME` with hello name of your SSH login.</span></span> <span data-ttu-id="408cb-159">Substitua o `CLUSTERNAME` pelo nome do seu cluster HDInsight:</span><span class="sxs-lookup"><span data-stu-id="408cb-159">Replace `CLUSTERNAME` with your HDInsight cluster name:</span></span>

    ```bash
    scp USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:/etc/hbase/conf/hbase-site.xml ./conf/hbase-site.xml
    ```

   <span data-ttu-id="408cb-160">Para saber mais sobre como usar `ssh` e `scp`, confira [Usar SSH com HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="408cb-160">For more information on using `ssh` and `scp`, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

## <a name="create-hello-application"></a><span data-ttu-id="408cb-161">Criar um aplicativo hello</span><span class="sxs-lookup"><span data-stu-id="408cb-161">Create hello application</span></span>

1. <span data-ttu-id="408cb-162">Vá toohello `hbaseapp/src/main/java/com/microsoft/examples` diretório e renomear Olá app.java arquivo muito`CreateTable.java`.</span><span class="sxs-lookup"><span data-stu-id="408cb-162">Go toohello `hbaseapp/src/main/java/com/microsoft/examples` directory and rename hello app.java file too`CreateTable.java`.</span></span>

2. <span data-ttu-id="408cb-163">Olá abrir `CreateTable.java` de arquivo e substitua conteúdo existente Olá Olá texto a seguir:</span><span class="sxs-lookup"><span data-stu-id="408cb-163">Open hello `CreateTable.java` file and replace hello existing contents with hello following text:</span></span>

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

    <span data-ttu-id="408cb-164">Esse código é hello **CreateTable** classe, que cria uma tabela denominada **pessoas** e preenchê-la com alguns usuários predefinidos.</span><span class="sxs-lookup"><span data-stu-id="408cb-164">This code is hello **CreateTable** class, which creates a table named **people** and populate it with some predefined users.</span></span>

3. <span data-ttu-id="408cb-165">Salvar Olá `CreateTable.java` arquivo.</span><span class="sxs-lookup"><span data-stu-id="408cb-165">Save hello `CreateTable.java` file.</span></span>

4. <span data-ttu-id="408cb-166">Em Olá `hbaseapp/src/main/java/com/microsoft/examples` diretório, crie um arquivo chamado `SearchByEmail.java`.</span><span class="sxs-lookup"><span data-stu-id="408cb-166">In hello `hbaseapp/src/main/java/com/microsoft/examples` directory, create a file named `SearchByEmail.java`.</span></span> <span data-ttu-id="408cb-167">Use Olá depois do texto como o conteúdo deste arquivo hello:</span><span class="sxs-lookup"><span data-stu-id="408cb-167">Use hello following text as hello contents of this file:</span></span>

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

    <span data-ttu-id="408cb-168">Olá **SearchByEmail** classe pode ser usado tooquery para linhas por endereço de email.</span><span class="sxs-lookup"><span data-stu-id="408cb-168">hello **SearchByEmail** class can be used tooquery for rows by email address.</span></span> <span data-ttu-id="408cb-169">Porque ele usa um filtro de expressão regular, você pode fornecer uma cadeia de caracteres ou uma expressão regular ao usar a classe de saudação.</span><span class="sxs-lookup"><span data-stu-id="408cb-169">Because it uses a regular expression filter, you can provide either a string or a regular expression when using hello class.</span></span>

5. <span data-ttu-id="408cb-170">Salvar Olá `SearchByEmail.java` arquivo.</span><span class="sxs-lookup"><span data-stu-id="408cb-170">Save hello `SearchByEmail.java` file.</span></span>

6. <span data-ttu-id="408cb-171">Em Olá `hbaseapp/src/main/hava/com/microsoft/examples` diretório, crie um arquivo chamado `DeleteTable.java`.</span><span class="sxs-lookup"><span data-stu-id="408cb-171">In hello `hbaseapp/src/main/hava/com/microsoft/examples` directory, create a file named `DeleteTable.java`.</span></span> <span data-ttu-id="408cb-172">Use Olá depois do texto como o conteúdo deste arquivo hello:</span><span class="sxs-lookup"><span data-stu-id="408cb-172">Use hello following text as hello contents of this file:</span></span>

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

    <span data-ttu-id="408cb-173">Essa classe limpa Olá HBase tabelas criadas neste exemplo, desabilitando e descartando Olá tabela criadas pelo Olá `CreateTable` classe.</span><span class="sxs-lookup"><span data-stu-id="408cb-173">This class cleans up hello HBase tables created in this example by disabling and dropping hello table created by hello `CreateTable` class.</span></span>

7. <span data-ttu-id="408cb-174">Salvar Olá `DeleteTable.java` arquivo.</span><span class="sxs-lookup"><span data-stu-id="408cb-174">Save hello `DeleteTable.java` file.</span></span>

## <a name="build-and-package-hello-application"></a><span data-ttu-id="408cb-175">Aplicativo hello de compilação e pacote</span><span class="sxs-lookup"><span data-stu-id="408cb-175">Build and package hello application</span></span>

1. <span data-ttu-id="408cb-176">De saudação `hbaseapp` diretório, o comando a seguir do uso Olá toobuild um arquivo JAR que contém o aplicativo hello:</span><span class="sxs-lookup"><span data-stu-id="408cb-176">From hello `hbaseapp` directory, use hello following command toobuild a JAR file that contains hello application:</span></span>

    ```bash
    mvn clean package
    ```

    <span data-ttu-id="408cb-177">Este comando cria e pacotes Olá aplicativo em um arquivo. jar.</span><span class="sxs-lookup"><span data-stu-id="408cb-177">This command builds and packages hello application into a .jar file.</span></span>

2. <span data-ttu-id="408cb-178">Quando Olá comando for concluído, hello `hbaseapp/target` diretório contém um arquivo chamado `hbaseapp-1.0-SNAPSHOT.jar`.</span><span class="sxs-lookup"><span data-stu-id="408cb-178">When hello command completes, hello `hbaseapp/target` directory contains a file named `hbaseapp-1.0-SNAPSHOT.jar`.</span></span>

   > [!NOTE]
   > <span data-ttu-id="408cb-179">Olá `hbaseapp-1.0-SNAPSHOT.jar` arquivo é um jar grande.</span><span class="sxs-lookup"><span data-stu-id="408cb-179">hello `hbaseapp-1.0-SNAPSHOT.jar` file is an uber jar.</span></span> <span data-ttu-id="408cb-180">Ele contém todos os aplicativos de Olá Olá dependências toorun necessária.</span><span class="sxs-lookup"><span data-stu-id="408cb-180">It contains all hello dependencies required toorun hello application.</span></span>


## <a name="upload-hello-jar-and-run-jobs-ssh"></a><span data-ttu-id="408cb-181">Olá JAR de carregar e executar trabalhos (SSH)</span><span class="sxs-lookup"><span data-stu-id="408cb-181">Upload hello JAR and run jobs (SSH)</span></span>

<span data-ttu-id="408cb-182">Olá use as etapas a seguir `scp` toocopy Olá JAR toohello primário nó principal do seu HBase no cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="408cb-182">hello following steps use `scp` toocopy hello JAR toohello primary head node of your HBase on HDInsight cluster.</span></span> <span data-ttu-id="408cb-183">Olá `ssh` comando é usada tooconnect toohello cluster e execute o exemplo hello diretamente no nó principal hello.</span><span class="sxs-lookup"><span data-stu-id="408cb-183">hello `ssh` command is then used tooconnect toohello cluster and run hello example directly on hello head node.</span></span>

1. <span data-ttu-id="408cb-184">tooupload Olá jar toohello cluster use Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="408cb-184">tooupload hello jar toohello cluster, use hello following command:</span></span>

    ```bash
    scp ./target/hbaseapp-1.0-SNAPSHOT.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:hbaseapp-1.0-SNAPSHOT.jar
    ```

    <span data-ttu-id="408cb-185">Substituir `USERNAME` com o nome de saudação do seu logon SSH.</span><span class="sxs-lookup"><span data-stu-id="408cb-185">Replace `USERNAME` with hello name of your SSH login.</span></span> <span data-ttu-id="408cb-186">Substitua o `CLUSTERNAME` pelo nome do seu cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="408cb-186">Replace `CLUSTERNAME` with your HDInsight cluster name.</span></span>

2. <span data-ttu-id="408cb-187">tooconnect toohello HBase cluster, use Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="408cb-187">tooconnect toohello HBase cluster, use hello following command:</span></span>

    ```bash
    ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
    ```

    <span data-ttu-id="408cb-188">Substituir `USERNAME` nome de saudação do seu logon SSH.</span><span class="sxs-lookup"><span data-stu-id="408cb-188">Replace `USERNAME` hello name of your SSH login.</span></span> <span data-ttu-id="408cb-189">Substitua o `CLUSTERNAME` pelo nome do seu cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="408cb-189">Replace `CLUSTERNAME` with your HDInsight cluster name.</span></span>

3. <span data-ttu-id="408cb-190">toocreate uma tabela do HBase usando Olá aplicativo Java, use Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="408cb-190">toocreate an HBase table using hello Java application, use hello following command:</span></span>

    ```bash
    yarn jar hbaseapp-1.0-SNAPSHOT.jar com.microsoft.examples.CreateTable
    ```

    <span data-ttu-id="408cb-191">Esse comando cria uma nova tabela do HBase chamada **people** e a preenche com dados.</span><span class="sxs-lookup"><span data-stu-id="408cb-191">This command creates a HBase table named **people**, and populates it with data.</span></span>

4. <span data-ttu-id="408cb-192">toosearch para endereços de email armazenados na tabela hello, use Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="408cb-192">toosearch for email addresses stored in hello table, use hello following command:</span></span>

    ```bash
    yarn jar hbaseapp-1.0-SNAPSHOT.jar com.microsoft.examples.SearchByEmail contoso.com
    ```

    <span data-ttu-id="408cb-193">Você receberá Olá resultados a seguir:</span><span class="sxs-lookup"><span data-stu-id="408cb-193">You receive hello following results:</span></span>

        Franklin Holtz - ID: 2
        Franklin Holtz - franklin@contoso.com - ID: 2
        Rae Schroeder - ID: 4
        Rae Schroeder - rae@contoso.com - ID: 4
        Gabriela Ingram - ID: 6
        Gabriela Ingram - gabriela@contoso.com - ID: 6

5. <span data-ttu-id="408cb-194">tabela de saudação toodelete, use Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="408cb-194">toodelete hello table, use hello following command:</span></span>

    

## <a name="upload-hello-jar-and-run-jobs-powershell"></a><span data-ttu-id="408cb-195">Olá JAR de carregar e executar trabalhos (PowerShell)</span><span class="sxs-lookup"><span data-stu-id="408cb-195">Upload hello JAR and run jobs (PowerShell)</span></span>

<span data-ttu-id="408cb-196">Olá etapas a seguir usa armazenamento do Azure PowerShell tooupload Olá JAR toohello padrão para o cluster HBase.</span><span class="sxs-lookup"><span data-stu-id="408cb-196">hello following steps use Azure PowerShell tooupload hello JAR toohello default storage for your HBase cluster.</span></span> <span data-ttu-id="408cb-197">Cmdlets do HDInsight forem usado toorun Olá exemplos remotamente.</span><span class="sxs-lookup"><span data-stu-id="408cb-197">HDInsight cmdlets are then used toorun hello examples remotely.</span></span>

1. <span data-ttu-id="408cb-198">Após instalar e configurar o Azure PowerShell, crie um arquivo chamado `hbase-runner.psm1`.</span><span class="sxs-lookup"><span data-stu-id="408cb-198">After installing and configuring Azure PowerShell, create a file named `hbase-runner.psm1`.</span></span> <span data-ttu-id="408cb-199">Use Olá depois do texto como o conteúdo deste arquivo hello:</span><span class="sxs-lookup"><span data-stu-id="408cb-199">Use hello following text as hello contents of this file:</span></span>

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

    <span data-ttu-id="408cb-200">Esse arquivo contém dois módulos:</span><span class="sxs-lookup"><span data-stu-id="408cb-200">This file contains two modules:</span></span>

   * <span data-ttu-id="408cb-201">**Adicionar HDInsightFile** - usadas cluster de toohello arquivos tooupload</span><span class="sxs-lookup"><span data-stu-id="408cb-201">**Add-HDInsightFile** - used tooupload files toohello cluster</span></span>
   * <span data-ttu-id="408cb-202">**Iniciar HBaseExample** -toorun Olá classes criadas anteriormente usadas</span><span class="sxs-lookup"><span data-stu-id="408cb-202">**Start-HBaseExample** - used toorun hello classes created earlier</span></span>

2. <span data-ttu-id="408cb-203">Salvar Olá `hbase-runner.psm1` arquivo.</span><span class="sxs-lookup"><span data-stu-id="408cb-203">Save hello `hbase-runner.psm1` file.</span></span>

3. <span data-ttu-id="408cb-204">Abra uma nova janela do PowerShell do Azure, altere os diretórios toohello `hbaseapp` directory, e, em seguida, Olá executar comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="408cb-204">Open a new Azure PowerShell window, change directories toohello `hbaseapp` directory, and then run hello following command:</span></span>

    ```powershell
    PS C:\ Import-Module c:\path\to\hbase-runner.psm1
    ```

    <span data-ttu-id="408cb-205">Alterar Olá caminho toohello local de saudação `hbase-runner.psm1` arquivo criado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="408cb-205">Change hello path toohello location of hello `hbase-runner.psm1` file created earlier.</span></span> <span data-ttu-id="408cb-206">Esse comando registra o módulo de saudação com o Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="408cb-206">This command registers hello module with Azure PowerShell.</span></span>

4. <span data-ttu-id="408cb-207">Comando a seguir de saudação do uso Olá tooupload `hbaseapp-1.0-SNAPSHOT.jar` tooyour cluster.</span><span class="sxs-lookup"><span data-stu-id="408cb-207">Use hello following command tooupload hello `hbaseapp-1.0-SNAPSHOT.jar` tooyour cluster.</span></span>

    ```powershell
    Add-HDInsightFile -localPath target\hbaseapp-1.0-SNAPSHOT.jar -destinationPath example/jars/hbaseapp-1.0-SNAPSHOT.jar -clusterName hdinsightclustername
    ```

    <span data-ttu-id="408cb-208">Substituir `hdinsightclustername` com nome de saudação do cluster.</span><span class="sxs-lookup"><span data-stu-id="408cb-208">Replace `hdinsightclustername` with hello name of your cluster.</span></span> <span data-ttu-id="408cb-209">comando Olá carrega Olá `hbaseapp-1.0-SNAPSHOT.jar` toohello `example/jars` local no armazenamento primário de saudação para seu cluster.</span><span class="sxs-lookup"><span data-stu-id="408cb-209">hello command uploads hello `hbaseapp-1.0-SNAPSHOT.jar` toohello `example/jars` location in hello primary storage for your cluster.</span></span>

5. <span data-ttu-id="408cb-210">Olá toocreate uma tabela usando `hbaseapp`, use Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="408cb-210">toocreate a table using hello `hbaseapp`, use hello following command:</span></span>

    ```powershell
    Start-HBaseExample -className com.microsoft.examples.CreateTable -clusterName hdinsightclustername
    ```

    <span data-ttu-id="408cb-211">Substituir `hdinsightclustername` com nome de saudação do cluster.</span><span class="sxs-lookup"><span data-stu-id="408cb-211">Replace `hdinsightclustername` with hello name of your cluster.</span></span>

    <span data-ttu-id="408cb-212">Esse comando cria uma tabela chamada **people** no HBase em seu cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="408cb-212">This command creates a table named **people** in HBase on your HDInsight cluster.</span></span> <span data-ttu-id="408cb-213">Este comando não mostra nenhuma saída na janela do console de saudação.</span><span class="sxs-lookup"><span data-stu-id="408cb-213">This command does not show any output in hello console window.</span></span>

6. <span data-ttu-id="408cb-214">toosearch de entradas na tabela de hello, use Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="408cb-214">toosearch for entries in hello table, use hello following command:</span></span>

    ```powershell
    Start-HBaseExample -className com.microsoft.examples.SearchByEmail -clusterName hdinsightclustername -emailRegex contoso.com
    ```

    <span data-ttu-id="408cb-215">Substituir `hdinsightclustername` com nome de saudação do cluster.</span><span class="sxs-lookup"><span data-stu-id="408cb-215">Replace `hdinsightclustername` with hello name of your cluster.</span></span>

    <span data-ttu-id="408cb-216">Esse comando usa Olá `SearchByEmail` classe toosearch para todas as linhas onde hello `contactinformation` família de coluna e hello `email` coluna contém a cadeia de caracteres de saudação `contoso.com`.</span><span class="sxs-lookup"><span data-stu-id="408cb-216">This command uses hello `SearchByEmail` class toosearch for any rows where hello `contactinformation` column family and hello `email` column, contains hello string `contoso.com`.</span></span> <span data-ttu-id="408cb-217">Você deve receber Olá resultados a seguir:</span><span class="sxs-lookup"><span data-stu-id="408cb-217">You should receive hello following results:</span></span>

          Franklin Holtz - ID: 2
          Franklin Holtz - franklin@contoso.com - ID: 2
          Rae Schroeder - ID: 4
          Rae Schroeder - rae@contoso.com - ID: 4
          Gabriela Ingram - ID: 6
          Gabriela Ingram - gabriela@contoso.com - ID: 6

    <span data-ttu-id="408cb-218">Usando **fabrikam.com** para Olá `-emailRegex` valor retorna usuários Olá que têm **fabrikam.com** no campo de email hello.</span><span class="sxs-lookup"><span data-stu-id="408cb-218">Using **fabrikam.com** for hello `-emailRegex` value returns hello users that have **fabrikam.com** in hello email field.</span></span> <span data-ttu-id="408cb-219">Você também pode usar expressões regulares, como o termo de pesquisa hello.</span><span class="sxs-lookup"><span data-stu-id="408cb-219">You can also use regular expressions as hello search term.</span></span> <span data-ttu-id="408cb-220">Por exemplo, **^ r** retorna endereços que começam com hello letra 'r'.</span><span class="sxs-lookup"><span data-stu-id="408cb-220">For example, **^r** returns email addresses that begin with hello letter 'r'.</span></span>

### <a name="no-results-or-unexpected-results-when-using-start-hbaseexample"></a><span data-ttu-id="408cb-221">Nenhum resultado ou resultados inesperados ao usar o Start-HBaseExample</span><span class="sxs-lookup"><span data-stu-id="408cb-221">No results or unexpected results when using Start-HBaseExample</span></span>

<span data-ttu-id="408cb-222">Saudação de uso `-showErr` parâmetro tooview saudação padrão erro (STDERR) que é gerado durante o trabalho de saudação em execução.</span><span class="sxs-lookup"><span data-stu-id="408cb-222">Use hello `-showErr` parameter tooview hello standard error (STDERR) that is produced while running hello job.</span></span>

## <a name="delete-hello-table"></a><span data-ttu-id="408cb-223">Excluir tabela Olá</span><span class="sxs-lookup"><span data-stu-id="408cb-223">Delete hello table</span></span>

<span data-ttu-id="408cb-224">Quando tiver terminado com o exemplo hello, use Olá Olá toodelete a seguir **pessoas** tabela usada neste exemplo:</span><span class="sxs-lookup"><span data-stu-id="408cb-224">When you are done with hello example, use hello following toodelete hello **people** table used in this example:</span></span>

<span data-ttu-id="408cb-225">__De uma sessão `ssh`__:</span><span class="sxs-lookup"><span data-stu-id="408cb-225">__From an `ssh` session__:</span></span>

`yarn jar hbaseapp-1.0-SNAPSHOT.jar com.microsoft.examples.DeleteTable`

<span data-ttu-id="408cb-226">__Do Azure PowerShell__:</span><span class="sxs-lookup"><span data-stu-id="408cb-226">__From Azure PowerShell__:</span></span>

`Start-HBaseExample -className com.microsoft.examples.DeleteTable -clusterName hdinsightclustername`

## <a name="next-steps"></a><span data-ttu-id="408cb-227">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="408cb-227">Next steps</span></span>

[<span data-ttu-id="408cb-228">Saiba como toouse SQL esquilo com HBase</span><span class="sxs-lookup"><span data-stu-id="408cb-228">Learn how toouse SQuirreL SQL with HBase</span></span>](hdinsight-hbase-phoenix-squirrel-linux.md)
