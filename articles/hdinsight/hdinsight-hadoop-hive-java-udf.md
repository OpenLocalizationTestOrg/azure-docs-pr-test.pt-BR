---
title: "função definida pelo usuário de aaaJava (UDF) com Hive no HDInsight - Azure | Microsoft Docs"
description: "Saiba como toocreate um baseados em Java definida pelo usuário UDF (função) que funciona com Hive. Este exemplo UDF converte uma tabela de toolowercase de cadeias de caracteres de texto."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 8d4f8efe-2f01-4a61-8619-651e873c7982
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/26/2017
ms.author: larryfr
ms.openlocfilehash: 392b4cfb73299d2f6c1e8e825a4201b48d501388
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-a-java-udf-with-hive-in-hdinsight"></a><span data-ttu-id="1da62-104">Usar um Java UDF com o Hive no HDInsight</span><span class="sxs-lookup"><span data-stu-id="1da62-104">Use a Java UDF with Hive in HDInsight</span></span>

<span data-ttu-id="1da62-105">Saiba como toocreate um baseados em Java definida pelo usuário UDF (função) que funciona com Hive.</span><span class="sxs-lookup"><span data-stu-id="1da62-105">Learn how toocreate a Java-based user-defined function (UDF) that works with Hive.</span></span> <span data-ttu-id="1da62-106">Olá Java UDF neste exemplo converte uma tabela de cadeias de caracteres em minúsculas tooall de caracteres de texto.</span><span class="sxs-lookup"><span data-stu-id="1da62-106">hello Java UDF in this example converts a table of text strings tooall-lowercase characters.</span></span>

## <a name="requirements"></a><span data-ttu-id="1da62-107">Requisitos</span><span class="sxs-lookup"><span data-stu-id="1da62-107">Requirements</span></span>

* <span data-ttu-id="1da62-108">Um cluster HDInsight</span><span class="sxs-lookup"><span data-stu-id="1da62-108">An HDInsight cluster</span></span> 

    > [!IMPORTANT]
    > <span data-ttu-id="1da62-109">Linux é Olá sistema operacional somente de usado no HDInsight versão 3.4 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="1da62-109">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="1da62-110">Para obter mais informações, confira [baixa do HDInsight no Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="1da62-110">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

    <span data-ttu-id="1da62-111">A maioria das etapas neste documento funciona tanto em clusters baseados em Windows quanto nos baseados em Linux.</span><span class="sxs-lookup"><span data-stu-id="1da62-111">Most steps in this document work on both Windows- and Linux-based clusters.</span></span> <span data-ttu-id="1da62-112">No entanto, Olá etapas usadas tooupload Olá compilados cluster do UDF toohello e execute-são clusters específicos com base em tooLinux.</span><span class="sxs-lookup"><span data-stu-id="1da62-112">However, hello steps used tooupload hello compiled UDF toohello cluster and run it are specific tooLinux-based clusters.</span></span> <span data-ttu-id="1da62-113">Links são fornecidos tooinformation que pode ser usado com clusters baseados no Windows.</span><span class="sxs-lookup"><span data-stu-id="1da62-113">Links are provided tooinformation that can be used with Windows-based clusters.</span></span>

* <span data-ttu-id="1da62-114">[Java JDK](http://www.oracle.com/technetwork/java/javase/downloads/) 8 ou posterior (ou um equivalente, como OpenJDK)</span><span class="sxs-lookup"><span data-stu-id="1da62-114">[Java JDK](http://www.oracle.com/technetwork/java/javase/downloads/) 8 or later (or an equivalent, such as OpenJDK)</span></span>

* [<span data-ttu-id="1da62-115">Apache Maven</span><span class="sxs-lookup"><span data-stu-id="1da62-115">Apache Maven</span></span>](http://maven.apache.org/)

* <span data-ttu-id="1da62-116">Um editor de texto ou Java IDE</span><span class="sxs-lookup"><span data-stu-id="1da62-116">A text editor or Java IDE</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="1da62-117">Se você criar hello arquivos Python em um cliente Windows, você deve usar um editor que usa LF como um final de linha.</span><span class="sxs-lookup"><span data-stu-id="1da62-117">If you create hello Python files on a Windows client, you must use an editor that uses LF as a line ending.</span></span> <span data-ttu-id="1da62-118">Se você não tiver certeza se seu editor usa LF ou CRLF, consulte Olá [solução de problemas](#troubleshooting) seção etapas sobre como remover Olá caracteres CR.</span><span class="sxs-lookup"><span data-stu-id="1da62-118">If you are not sure whether your editor uses LF or CRLF, see hello [Troubleshooting](#troubleshooting) section for steps on removing hello CR character.</span></span>

## <a name="create-an-example-java-udf"></a><span data-ttu-id="1da62-119">Criar UDF Java de exemplo</span><span class="sxs-lookup"><span data-stu-id="1da62-119">Create an example Java UDF</span></span> 

1. <span data-ttu-id="1da62-120">De uma linha de comando, use Olá toocreate um novo projeto Maven a seguir:</span><span class="sxs-lookup"><span data-stu-id="1da62-120">From a command line, use hello following toocreate a new Maven project:</span></span>

    ```bash
    mvn archetype:generate -DgroupId=com.microsoft.examples -DartifactId=ExampleUDF -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
    ```

   > [!NOTE]
   > <span data-ttu-id="1da62-121">Se você estiver usando o PowerShell, você deve colocar entre aspas, parâmetros de saudação.</span><span class="sxs-lookup"><span data-stu-id="1da62-121">If you are using PowerShell, you must put quotes around hello parameters.</span></span> <span data-ttu-id="1da62-122">Por exemplo: `mvn archetype:generate "-DgroupId=com.microsoft.examples" "-DartifactId=ExampleUDF" "-DarchetypeArtifactId=maven-archetype-quickstart" "-DinteractiveMode=false"`.</span><span class="sxs-lookup"><span data-stu-id="1da62-122">For example, `mvn archetype:generate "-DgroupId=com.microsoft.examples" "-DartifactId=ExampleUDF" "-DarchetypeArtifactId=maven-archetype-quickstart" "-DinteractiveMode=false"`.</span></span>

    <span data-ttu-id="1da62-123">Este comando cria um diretório chamado **exampleudf**, que contém o projeto Maven hello.</span><span class="sxs-lookup"><span data-stu-id="1da62-123">This command creates a directory named **exampleudf**, which contains hello Maven project.</span></span>

2. <span data-ttu-id="1da62-124">Depois que o projeto de saudação foi criado, excluir Olá **src/exampleudf/teste** diretório que foi criado como parte do projeto de saudação.</span><span class="sxs-lookup"><span data-stu-id="1da62-124">Once hello project has been created, delete hello **exampleudf/src/test** directory that was created as part of hello project.</span></span>

3. <span data-ttu-id="1da62-125">Olá abrir **exampleudf/pom.xml**e substituir Olá `<dependencies>` entrada hello XML a seguir:</span><span class="sxs-lookup"><span data-stu-id="1da62-125">Open hello **exampleudf/pom.xml**, and replace hello existing `<dependencies>` entry with hello following XML:</span></span>

    ```xml
    <dependencies>
        <dependency>
            <groupId>org.apache.hadoop</groupId>
            <artifactId>hadoop-client</artifactId>
            <version>2.7.3</version>
            <scope>provided</scope>
        </dependency>
        <dependency>
            <groupId>org.apache.hive</groupId>
            <artifactId>hive-exec</artifactId>
            <version>1.2.1</version>
            <scope>provided</scope>
        </dependency>
    </dependencies>
    ```

    <span data-ttu-id="1da62-126">Essas entradas de especificar a versão de saudação do Hadoop e Hive incluído com o HDInsight 3.5.</span><span class="sxs-lookup"><span data-stu-id="1da62-126">These entries specify hello version of Hadoop and Hive included with HDInsight 3.5.</span></span> <span data-ttu-id="1da62-127">Você pode encontrar informações sobre versões de saudação do Hadoop e Hive fornecido com o HDInsight da saudação [o controle de versão do HDInsight componente](hdinsight-component-versioning.md) documento.</span><span class="sxs-lookup"><span data-stu-id="1da62-127">You can find information on hello versions of Hadoop and Hive provided with HDInsight from hello [HDInsight component versioning](hdinsight-component-versioning.md) document.</span></span>

    <span data-ttu-id="1da62-128">Adicionar um `<build>` seção antes Olá `</project>` linha no final de saudação do arquivo hello.</span><span class="sxs-lookup"><span data-stu-id="1da62-128">Add a `<build>` section before hello `</project>` line at hello end of hello file.</span></span> <span data-ttu-id="1da62-129">Esta seção deve conter Olá XML a seguir:</span><span class="sxs-lookup"><span data-stu-id="1da62-129">This section should contain hello following XML:</span></span>

    ```xml
    <build>
        <plugins>
            <!-- build for Java 1.8. This is required by HDInsight 3.5  -->
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-compiler-plugin</artifactId>
                <version>3.3</version>
                <configuration>
                    <source>1.8</source>
                    <target>1.8</target>
                </configuration>
            </plugin>
            <!-- build an uber jar -->
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-shade-plugin</artifactId>
                <version>2.3</version>
                <configuration>
                    <!-- Keep us from getting a can't overwrite file error -->
                    <transformers>
                        <transformer
                                implementation="org.apache.maven.plugins.shade.resource.ApacheLicenseResourceTransformer">
                        </transformer>
                        <transformer implementation="org.apache.maven.plugins.shade.resource.ServicesResourceTransformer">
                        </transformer>
                    </transformers>
                    <!-- Keep us from getting a bad signature error -->
                    <filters>
                        <filter>
                            <artifact>*:*</artifact>
                            <excludes>
                                <exclude>META-INF/*.SF</exclude>
                                <exclude>META-INF/*.DSA</exclude>
                                <exclude>META-INF/*.RSA</exclude>
                            </excludes>
                        </filter>
                    </filters>
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

    <span data-ttu-id="1da62-130">Essas entradas definem como toobuild Olá projeto.</span><span class="sxs-lookup"><span data-stu-id="1da62-130">These entries define how toobuild hello project.</span></span> <span data-ttu-id="1da62-131">Especificamente, versão de saudação do Java que Olá projeto usa e como toobuild uma uberjar para cluster de toohello de implantação.</span><span class="sxs-lookup"><span data-stu-id="1da62-131">Specifically, hello version of Java that hello project uses and how toobuild an uberjar for deployment toohello cluster.</span></span>

    <span data-ttu-id="1da62-132">Salve o arquivo de saudação quando Olá foi alterado.</span><span class="sxs-lookup"><span data-stu-id="1da62-132">Save hello file once hello changes have been made.</span></span>

4. <span data-ttu-id="1da62-133">Renomear **exampleudf/src/main/java/com/microsoft/examples/App.java** muito**ExampleUDF.java**e, em seguida, abra o arquivo de saudação em seu editor.</span><span class="sxs-lookup"><span data-stu-id="1da62-133">Rename **exampleudf/src/main/java/com/microsoft/examples/App.java** too**ExampleUDF.java**, and then open hello file in your editor.</span></span>

5. <span data-ttu-id="1da62-134">Substitua o conteúdo de saudação do hello **ExampleUDF.java** de arquivos com os seguintes hello e salve o arquivo de saudação.</span><span class="sxs-lookup"><span data-stu-id="1da62-134">Replace hello contents of hello **ExampleUDF.java** file with hello following, then save hello file.</span></span>

    ```java
    package com.microsoft.examples;

    import org.apache.hadoop.hive.ql.exec.Description;
    import org.apache.hadoop.hive.ql.exec.UDF;
    import org.apache.hadoop.io.*;

    // Description of hello UDF
    @Description(
        name="ExampleUDF",
        value="returns a lower case version of hello input string.",
        extended="select ExampleUDF(deviceplatform) from hivesampletable limit 10;"
    )
    public class ExampleUDF extends UDF {
        // Accept a string input
        public String evaluate(String input) {
            // If hello value is null, return a null
            if(input == null)
                return null;
            // Lowercase hello input string and return it
            return input.toLowerCase();
        }
    }
    ```

    <span data-ttu-id="1da62-135">Esse código implementa um UDF que aceita um valor de cadeia de caracteres e retorna uma versão minúscula de cadeia de caracteres de saudação.</span><span class="sxs-lookup"><span data-stu-id="1da62-135">This code implements a UDF that accepts a string value, and returns a lowercase version of hello string.</span></span>

## <a name="build-and-install-hello-udf"></a><span data-ttu-id="1da62-136">Crie e instale Olá UDF</span><span class="sxs-lookup"><span data-stu-id="1da62-136">Build and install hello UDF</span></span>

1. <span data-ttu-id="1da62-137">Use Olá toocompile de comando a seguir e Olá UDF do pacote:</span><span class="sxs-lookup"><span data-stu-id="1da62-137">Use hello following command toocompile and package hello UDF:</span></span>

    ```bash
    mvn compile package
    ```

    <span data-ttu-id="1da62-138">Este comando cria e pacotes Olá UDF em Olá `exampleudf/target/ExampleUDF-1.0-SNAPSHOT.jar` arquivo.</span><span class="sxs-lookup"><span data-stu-id="1da62-138">This command builds and packages hello UDF into hello `exampleudf/target/ExampleUDF-1.0-SNAPSHOT.jar` file.</span></span>

2. <span data-ttu-id="1da62-139">Saudação de uso `scp` cluster HDInsight toohello de arquivos do comando toocopy hello.</span><span class="sxs-lookup"><span data-stu-id="1da62-139">Use hello `scp` command toocopy hello file toohello HDInsight cluster.</span></span>

    ```bash
    scp ./target/ExampleUDF-1.0-SNAPSHOT.jar myuser@mycluster-ssh.azurehdinsight
    ```

    <span data-ttu-id="1da62-140">Substituir `myuser` com hello SSH a conta de usuário para seu cluster.</span><span class="sxs-lookup"><span data-stu-id="1da62-140">Replace `myuser` with hello SSH user account for your cluster.</span></span> <span data-ttu-id="1da62-141">Substituir `mycluster` com o nome do cluster hello.</span><span class="sxs-lookup"><span data-stu-id="1da62-141">Replace `mycluster` with hello cluster name.</span></span> <span data-ttu-id="1da62-142">Se você usou uma saudação de toosecure de senha SSH conta, você é solicitadas tooenter Olá por senha.</span><span class="sxs-lookup"><span data-stu-id="1da62-142">If you used a password toosecure hello SSH account, you are prompted tooenter hello password.</span></span> <span data-ttu-id="1da62-143">Se você usou um certificado, talvez seja necessário Olá toouse `-i` parâmetro toospecify Olá arquivo de chave privada.</span><span class="sxs-lookup"><span data-stu-id="1da62-143">If you used a certificate, you may need toouse hello `-i` parameter toospecify hello private key file.</span></span>

3. <span data-ttu-id="1da62-144">Conecte-se toohello cluster usando o SSH.</span><span class="sxs-lookup"><span data-stu-id="1da62-144">Connect toohello cluster using SSH.</span></span>

    ```bash
    ssh myuser@mycluster-ssh.azurehdinsight.net
    ```

    <span data-ttu-id="1da62-145">Para obter mais informações, confira [Usar SSH com HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="1da62-145">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

4. <span data-ttu-id="1da62-146">Da sessão SSH Olá, copie o armazenamento de tooHDInsight de arquivos jar hello.</span><span class="sxs-lookup"><span data-stu-id="1da62-146">From hello SSH session, copy hello jar file tooHDInsight storage.</span></span>

    ```bash
    hdfs dfs -put ExampleUDF-1.0-SNAPSHOT.jar /example/jars
    ```

## <a name="use-hello-udf-from-hive"></a><span data-ttu-id="1da62-147">Usar Olá UDF de Hive</span><span class="sxs-lookup"><span data-stu-id="1da62-147">Use hello UDF from Hive</span></span>

1. <span data-ttu-id="1da62-148">Use Olá cliente de Beeline toostart Olá da sessão SSH Olá a seguir.</span><span class="sxs-lookup"><span data-stu-id="1da62-148">Use hello following toostart hello Beeline client from hello SSH session.</span></span>

    ```bash
    beeline -u 'jdbc:hive2://localhost:10001/;transportMode=http' -n admin
    ```

    <span data-ttu-id="1da62-149">Esse comando assume que você usou padrão Olá **admin** Olá conta de logon para o cluster.</span><span class="sxs-lookup"><span data-stu-id="1da62-149">This command assumes that you used hello default of **admin** for hello login account for your cluster.</span></span>

2. <span data-ttu-id="1da62-150">Quando chegar à saudação `jdbc:hive2://localhost:10001/>` prompt, digite Olá tooadd Olá UDF tooHive a seguir e expô-lo como uma função.</span><span class="sxs-lookup"><span data-stu-id="1da62-150">Once you arrive at hello `jdbc:hive2://localhost:10001/>` prompt, enter hello following tooadd hello UDF tooHive and expose it as a function.</span></span>

    ```hiveql
    ADD JAR wasb:///example/jars/ExampleUDF-1.0-SNAPSHOT.jar;
    CREATE TEMPORARY FUNCTION tolower as 'com.microsoft.examples.ExampleUDF';
    ```

    > [!NOTE]
    > <span data-ttu-id="1da62-151">Este exemplo presume que o armazenamento do Azure é o armazenamento padrão para cluster hello.</span><span class="sxs-lookup"><span data-stu-id="1da62-151">This example assumes that Azure Storage is default storage for hello cluster.</span></span> <span data-ttu-id="1da62-152">Se o cluster usa o repositório Data Lake em vez disso, alterar Olá `wasb:///` valor muito`adl:///`.</span><span class="sxs-lookup"><span data-stu-id="1da62-152">If your cluster uses Data Lake Store instead, change hello `wasb:///` value too`adl:///`.</span></span>

3. <span data-ttu-id="1da62-153">Use Olá UDF tooconvert valores recuperados de uma cadeias de caracteres tabela toolower maiusculas.</span><span class="sxs-lookup"><span data-stu-id="1da62-153">Use hello UDF tooconvert values retrieved from a table toolower case strings.</span></span>

    ```hiveql
    SELECT tolower(deviceplatform) FROM hivesampletable LIMIT 10;
    ```

    <span data-ttu-id="1da62-154">Esta consulta selecionará Olá plataforma de dispositivo (Android, Windows, iOS, etc.) da tabela Olá, converta o caso de toolower de cadeia de caracteres de saudação e exibi-los.</span><span class="sxs-lookup"><span data-stu-id="1da62-154">This query selects hello device platform (Android, Windows, iOS, etc.) from hello table, convert hello string toolower case, and then display them.</span></span> <span data-ttu-id="1da62-155">saída de Hello aparece semelhante toohello texto a seguir:</span><span class="sxs-lookup"><span data-stu-id="1da62-155">hello output appears similar toohello following text:</span></span>

        +----------+--+
        |   _c0    |
        +----------+--+
        | android  |
        | android  |
        | android  |
        | android  |
        | android  |
        | android  |
        | android  |
        | android  |
        | android  |
        | android  |
        +----------+--+

## <a name="next-steps"></a><span data-ttu-id="1da62-156">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="1da62-156">Next steps</span></span>

<span data-ttu-id="1da62-157">Para outros toowork maneiras com Hive, consulte [uso de Hive do HDInsight](hdinsight-use-hive.md).</span><span class="sxs-lookup"><span data-stu-id="1da62-157">For other ways toowork with Hive, see [Use Hive with HDInsight](hdinsight-use-hive.md).</span></span>

<span data-ttu-id="1da62-158">Para obter mais informações sobre as funções de Hive User-Defined, consulte [Hive operadores e funções definidas pelo usuário](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF) seção Olá Hive wiki em apache.org.</span><span class="sxs-lookup"><span data-stu-id="1da62-158">For more information on Hive User-Defined Functions, see [Hive Operators and User-Defined Functions](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF) section of hello Hive wiki at apache.org.</span></span>
