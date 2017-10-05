---
title: "UDF (função definida pelo usuário) do Java com o Hive no HDInsight – Azure | Microsoft Docs"
description: "Saiba como criar um UDF (função definida pelo usuário) baseado em Java que funcione com o Hive. Este UDF de exemplo converte uma tabela de cadeias de caracteres de texto em minúsculas."
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
ms.openlocfilehash: 481d234eaf88bdb210821084ee4154159470eda0
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="use-a-java-udf-with-hive-in-hdinsight"></a><span data-ttu-id="37229-104">Usar um Java UDF com o Hive no HDInsight</span><span class="sxs-lookup"><span data-stu-id="37229-104">Use a Java UDF with Hive in HDInsight</span></span>

<span data-ttu-id="37229-105">Saiba como criar um UDF (função definida pelo usuário) baseado em Java que funcione com o Hive.</span><span class="sxs-lookup"><span data-stu-id="37229-105">Learn how to create a Java-based user-defined function (UDF) that works with Hive.</span></span> <span data-ttu-id="37229-106">O UDF Java neste exemplo converte uma tabela de cadeias de caracteres de texto em caracteres minúsculos.</span><span class="sxs-lookup"><span data-stu-id="37229-106">The Java UDF in this example converts a table of text strings to all-lowercase characters.</span></span>

## <a name="requirements"></a><span data-ttu-id="37229-107">Requisitos</span><span class="sxs-lookup"><span data-stu-id="37229-107">Requirements</span></span>

* <span data-ttu-id="37229-108">Um cluster HDInsight</span><span class="sxs-lookup"><span data-stu-id="37229-108">An HDInsight cluster</span></span> 

    > [!IMPORTANT]
    > <span data-ttu-id="37229-109">O Linux é o único sistema operacional usado no HDInsight versão 3.4 ou superior.</span><span class="sxs-lookup"><span data-stu-id="37229-109">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="37229-110">Para obter mais informações, confira [baixa do HDInsight no Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="37229-110">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

    <span data-ttu-id="37229-111">A maioria das etapas neste documento funciona tanto em clusters baseados em Windows quanto nos baseados em Linux.</span><span class="sxs-lookup"><span data-stu-id="37229-111">Most steps in this document work on both Windows- and Linux-based clusters.</span></span> <span data-ttu-id="37229-112">No entanto, as etapas usadas para carregar o UDF compilado ao cluster e executá-lo são específicas para clusters baseados em Linux.</span><span class="sxs-lookup"><span data-stu-id="37229-112">However, the steps used to upload the compiled UDF to the cluster and run it are specific to Linux-based clusters.</span></span> <span data-ttu-id="37229-113">São fornecidos links para informações que podem ser usados com clusters baseados em Windows.</span><span class="sxs-lookup"><span data-stu-id="37229-113">Links are provided to information that can be used with Windows-based clusters.</span></span>

* <span data-ttu-id="37229-114">[Java JDK](http://www.oracle.com/technetwork/java/javase/downloads/) 8 ou posterior (ou um equivalente, como OpenJDK)</span><span class="sxs-lookup"><span data-stu-id="37229-114">[Java JDK](http://www.oracle.com/technetwork/java/javase/downloads/) 8 or later (or an equivalent, such as OpenJDK)</span></span>

* [<span data-ttu-id="37229-115">Apache Maven</span><span class="sxs-lookup"><span data-stu-id="37229-115">Apache Maven</span></span>](http://maven.apache.org/)

* <span data-ttu-id="37229-116">Um editor de texto ou Java IDE</span><span class="sxs-lookup"><span data-stu-id="37229-116">A text editor or Java IDE</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="37229-117">Se você criar os arquivos de Python em um cliente Windows, você deverá usar um editor que usa LF como uma terminação de linha.</span><span class="sxs-lookup"><span data-stu-id="37229-117">If you create the Python files on a Windows client, you must use an editor that uses LF as a line ending.</span></span> <span data-ttu-id="37229-118">Se você não tem certeza se o seu editor usa LF ou CRLF, veja a seção de [Solução de problemas](#troubleshooting) para ver as etapas para remover o caractere CR.</span><span class="sxs-lookup"><span data-stu-id="37229-118">If you are not sure whether your editor uses LF or CRLF, see the [Troubleshooting](#troubleshooting) section for steps on removing the CR character.</span></span>

## <a name="create-an-example-java-udf"></a><span data-ttu-id="37229-119">Criar UDF Java de exemplo</span><span class="sxs-lookup"><span data-stu-id="37229-119">Create an example Java UDF</span></span> 

1. <span data-ttu-id="37229-120">Na linha de comando, use o seguinte para criar um novo projeto Maven:</span><span class="sxs-lookup"><span data-stu-id="37229-120">From a command line, use the following to create a new Maven project:</span></span>

    ```bash
    mvn archetype:generate -DgroupId=com.microsoft.examples -DartifactId=ExampleUDF -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
    ```

   > [!NOTE]
   > <span data-ttu-id="37229-121">Se você estiver usando o PowerShell, deverá inserir os parâmetros entre aspas.</span><span class="sxs-lookup"><span data-stu-id="37229-121">If you are using PowerShell, you must put quotes around the parameters.</span></span> <span data-ttu-id="37229-122">Por exemplo: `mvn archetype:generate "-DgroupId=com.microsoft.examples" "-DartifactId=ExampleUDF" "-DarchetypeArtifactId=maven-archetype-quickstart" "-DinteractiveMode=false"`.</span><span class="sxs-lookup"><span data-stu-id="37229-122">For example, `mvn archetype:generate "-DgroupId=com.microsoft.examples" "-DartifactId=ExampleUDF" "-DarchetypeArtifactId=maven-archetype-quickstart" "-DinteractiveMode=false"`.</span></span>

    <span data-ttu-id="37229-123">Esse comando cria um diretório chamado **exampleudf**, que contém o projeto Maven.</span><span class="sxs-lookup"><span data-stu-id="37229-123">This command creates a directory named **exampleudf**, which contains the Maven project.</span></span>

2. <span data-ttu-id="37229-124">Quando o projeto tiver sido criado, exclua o diretório **exampleudf/src/teste** que foi criado como parte do projeto.</span><span class="sxs-lookup"><span data-stu-id="37229-124">Once the project has been created, delete the **exampleudf/src/test** directory that was created as part of the project.</span></span>

3. <span data-ttu-id="37229-125">Abra o **exampleudf/pom.xml** e substitua a entrada `<dependencies>` existente pelo seguinte XML:</span><span class="sxs-lookup"><span data-stu-id="37229-125">Open the **exampleudf/pom.xml**, and replace the existing `<dependencies>` entry with the following XML:</span></span>

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

    <span data-ttu-id="37229-126">Essas entradas especificam a versão do Hadoop e do Hive incluídas com o HDInsight 3.5.</span><span class="sxs-lookup"><span data-stu-id="37229-126">These entries specify the version of Hadoop and Hive included with HDInsight 3.5.</span></span> <span data-ttu-id="37229-127">Você pode encontrar informações sobre as versões do Hadoop e do Hive fornecidas com o HDInsight no documento [Controle de versão de componente do HDInsight](hdinsight-component-versioning.md) .</span><span class="sxs-lookup"><span data-stu-id="37229-127">You can find information on the versions of Hadoop and Hive provided with HDInsight from the [HDInsight component versioning](hdinsight-component-versioning.md) document.</span></span>

    <span data-ttu-id="37229-128">Adicione uma seção `<build>` antes da linha `</project>` no final do arquivo.</span><span class="sxs-lookup"><span data-stu-id="37229-128">Add a `<build>` section before the `</project>` line at the end of the file.</span></span> <span data-ttu-id="37229-129">Esta seção deve conter o XML a seguir:</span><span class="sxs-lookup"><span data-stu-id="37229-129">This section should contain the following XML:</span></span>

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

    <span data-ttu-id="37229-130">Essas entradas definem como compilar o projeto.</span><span class="sxs-lookup"><span data-stu-id="37229-130">These entries define how to build the project.</span></span> <span data-ttu-id="37229-131">Especificamente, a versão do Java que o projeto usa e como criar um uberjar para implantação no cluster.</span><span class="sxs-lookup"><span data-stu-id="37229-131">Specifically, the version of Java that the project uses and how to build an uberjar for deployment to the cluster.</span></span>

    <span data-ttu-id="37229-132">Salve o arquivo depois que as alterações forem feitas.</span><span class="sxs-lookup"><span data-stu-id="37229-132">Save the file once the changes have been made.</span></span>

4. <span data-ttu-id="37229-133">Renomeie **exampleudf/src/main/java/com/microsoft/examples/App.java** para **ExampleUDF.java** e abra o arquivo no editor.</span><span class="sxs-lookup"><span data-stu-id="37229-133">Rename **exampleudf/src/main/java/com/microsoft/examples/App.java** to **ExampleUDF.java**, and then open the file in your editor.</span></span>

5. <span data-ttu-id="37229-134">Substitua o conteúdo do arquivo **ExampleUDF.java** pelo seguinte e, em seguida, salve o arquivo.</span><span class="sxs-lookup"><span data-stu-id="37229-134">Replace the contents of the **ExampleUDF.java** file with the following, then save the file.</span></span>

    ```java
    package com.microsoft.examples;

    import org.apache.hadoop.hive.ql.exec.Description;
    import org.apache.hadoop.hive.ql.exec.UDF;
    import org.apache.hadoop.io.*;

    // Description of the UDF
    @Description(
        name="ExampleUDF",
        value="returns a lower case version of the input string.",
        extended="select ExampleUDF(deviceplatform) from hivesampletable limit 10;"
    )
    public class ExampleUDF extends UDF {
        // Accept a string input
        public String evaluate(String input) {
            // If the value is null, return a null
            if(input == null)
                return null;
            // Lowercase the input string and return it
            return input.toLowerCase();
        }
    }
    ```

    <span data-ttu-id="37229-135">Este código implementa um UDF que aceita um valor de cadeia de caracteres e retorna uma versão da cadeia de caracteres em minúsculas.</span><span class="sxs-lookup"><span data-stu-id="37229-135">This code implements a UDF that accepts a string value, and returns a lowercase version of the string.</span></span>

## <a name="build-and-install-the-udf"></a><span data-ttu-id="37229-136">Compilar e instalar o UDF</span><span class="sxs-lookup"><span data-stu-id="37229-136">Build and install the UDF</span></span>

1. <span data-ttu-id="37229-137">Use o seguinte comando para compilar e empacotar o UDF:</span><span class="sxs-lookup"><span data-stu-id="37229-137">Use the following command to compile and package the UDF:</span></span>

    ```bash
    mvn compile package
    ```

    <span data-ttu-id="37229-138">Este comando cria e empacota o UDF no arquivo `exampleudf/target/ExampleUDF-1.0-SNAPSHOT.jar`.</span><span class="sxs-lookup"><span data-stu-id="37229-138">This command builds and packages the UDF into the `exampleudf/target/ExampleUDF-1.0-SNAPSHOT.jar` file.</span></span>

2. <span data-ttu-id="37229-139">Use o comando `scp` para copiar o arquivo para o cluster do HDInsight.</span><span class="sxs-lookup"><span data-stu-id="37229-139">Use the `scp` command to copy the file to the HDInsight cluster.</span></span>

    ```bash
    scp ./target/ExampleUDF-1.0-SNAPSHOT.jar myuser@mycluster-ssh.azurehdinsight
    ```

    <span data-ttu-id="37229-140">Substitua `myuser` pela conta de usuário SSH para o cluster.</span><span class="sxs-lookup"><span data-stu-id="37229-140">Replace `myuser` with the SSH user account for your cluster.</span></span> <span data-ttu-id="37229-141">Substitua `mycluster` pelo nome do cluster.</span><span class="sxs-lookup"><span data-stu-id="37229-141">Replace `mycluster` with the cluster name.</span></span> <span data-ttu-id="37229-142">Se você tiver usado uma senha para proteger a conta SSH, você precisará digitá-la.</span><span class="sxs-lookup"><span data-stu-id="37229-142">If you used a password to secure the SSH account, you are prompted to enter the password.</span></span> <span data-ttu-id="37229-143">Se você tiver usado um certificado, talvez precise usar o parâmetro `-i` para especificar o arquivo da chave privada.</span><span class="sxs-lookup"><span data-stu-id="37229-143">If you used a certificate, you may need to use the `-i` parameter to specify the private key file.</span></span>

3. <span data-ttu-id="37229-144">Conecte-se ao cluster usando o SSH.</span><span class="sxs-lookup"><span data-stu-id="37229-144">Connect to the cluster using SSH.</span></span>

    ```bash
    ssh myuser@mycluster-ssh.azurehdinsight.net
    ```

    <span data-ttu-id="37229-145">Para obter mais informações, confira [Usar SSH com HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="37229-145">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

4. <span data-ttu-id="37229-146">Na sessão de SSH, copie o arquivo jar para o armazenamento do HDInsight.</span><span class="sxs-lookup"><span data-stu-id="37229-146">From the SSH session, copy the jar file to HDInsight storage.</span></span>

    ```bash
    hdfs dfs -put ExampleUDF-1.0-SNAPSHOT.jar /example/jars
    ```

## <a name="use-the-udf-from-hive"></a><span data-ttu-id="37229-147">Usar o UDF do Hive</span><span class="sxs-lookup"><span data-stu-id="37229-147">Use the UDF from Hive</span></span>

1. <span data-ttu-id="37229-148">Use o seguinte para iniciar o cliente Beeline na sessão de SSH.</span><span class="sxs-lookup"><span data-stu-id="37229-148">Use the following to start the Beeline client from the SSH session.</span></span>

    ```bash
    beeline -u 'jdbc:hive2://localhost:10001/;transportMode=http' -n admin
    ```

    <span data-ttu-id="37229-149">Esse comando presume que você usou o padrão de **admin** para a conta de logon para o cluster.</span><span class="sxs-lookup"><span data-stu-id="37229-149">This command assumes that you used the default of **admin** for the login account for your cluster.</span></span>

2. <span data-ttu-id="37229-150">Quando você chegar ao prompt `jdbc:hive2://localhost:10001/>` , digite o seguinte para adicionar o UDF no Hive e expô-lo como uma função.</span><span class="sxs-lookup"><span data-stu-id="37229-150">Once you arrive at the `jdbc:hive2://localhost:10001/>` prompt, enter the following to add the UDF to Hive and expose it as a function.</span></span>

    ```hiveql
    ADD JAR wasb:///example/jars/ExampleUDF-1.0-SNAPSHOT.jar;
    CREATE TEMPORARY FUNCTION tolower as 'com.microsoft.examples.ExampleUDF';
    ```

    > [!NOTE]
    > <span data-ttu-id="37229-151">Este exemplo assume que o Armazenamento do Azure é o armazenamento padrão do cluster.</span><span class="sxs-lookup"><span data-stu-id="37229-151">This example assumes that Azure Storage is default storage for the cluster.</span></span> <span data-ttu-id="37229-152">Se o cluster usar o Data Lake Store em vez disso, altere o valor `wasb:///` para `adl:///`.</span><span class="sxs-lookup"><span data-stu-id="37229-152">If your cluster uses Data Lake Store instead, change the `wasb:///` value to `adl:///`.</span></span>

3. <span data-ttu-id="37229-153">Use o UDF para converter valores recuperados de uma tabela em cadeias de caracteres de letras minúsculas.</span><span class="sxs-lookup"><span data-stu-id="37229-153">Use the UDF to convert values retrieved from a table to lower case strings.</span></span>

    ```hiveql
    SELECT tolower(deviceplatform) FROM hivesampletable LIMIT 10;
    ```

    <span data-ttu-id="37229-154">Essa consulta seleciona a plataforma do dispositivo (Android, Windows, iOS etc.) na tabela, converte a cadeia de caracteres em letras minúsculas e as exibe.</span><span class="sxs-lookup"><span data-stu-id="37229-154">This query selects the device platform (Android, Windows, iOS, etc.) from the table, convert the string to lower case, and then display them.</span></span> <span data-ttu-id="37229-155">A saída é semelhante ao texto a seguir:</span><span class="sxs-lookup"><span data-stu-id="37229-155">The output appears similar to the following text:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="37229-156">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="37229-156">Next steps</span></span>

<span data-ttu-id="37229-157">Para ver outras maneiras de trabalhar com o Hive, consulte [Usar o Hive com o HDInsight](hdinsight-use-hive.md).</span><span class="sxs-lookup"><span data-stu-id="37229-157">For other ways to work with Hive, see [Use Hive with HDInsight](hdinsight-use-hive.md).</span></span>

<span data-ttu-id="37229-158">Para obter mais informações sobre funções definidas pelo usuário do Hive, consulte a seção [Operadores e funções definidas pelo usuário do Hive](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF) do wiki Hive em apache.org.</span><span class="sxs-lookup"><span data-stu-id="37229-158">For more information on Hive User-Defined Functions, see [Hive Operators and User-Defined Functions](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF) section of the Hive wiki at apache.org.</span></span>
