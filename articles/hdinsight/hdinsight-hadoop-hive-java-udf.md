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
# <a name="use-a-java-udf-with-hive-in-hdinsight"></a>Usar um Java UDF com o Hive no HDInsight

Saiba como toocreate um baseados em Java definida pelo usuário UDF (função) que funciona com Hive. Olá Java UDF neste exemplo converte uma tabela de cadeias de caracteres em minúsculas tooall de caracteres de texto.

## <a name="requirements"></a>Requisitos

* Um cluster HDInsight 

    > [!IMPORTANT]
    > Linux é Olá sistema operacional somente de usado no HDInsight versão 3.4 ou posterior. Para obter mais informações, confira [baixa do HDInsight no Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).

    A maioria das etapas neste documento funciona tanto em clusters baseados em Windows quanto nos baseados em Linux. No entanto, Olá etapas usadas tooupload Olá compilados cluster do UDF toohello e execute-são clusters específicos com base em tooLinux. Links são fornecidos tooinformation que pode ser usado com clusters baseados no Windows.

* [Java JDK](http://www.oracle.com/technetwork/java/javase/downloads/) 8 ou posterior (ou um equivalente, como OpenJDK)

* [Apache Maven](http://maven.apache.org/)

* Um editor de texto ou Java IDE

    > [!IMPORTANT]
    > Se você criar hello arquivos Python em um cliente Windows, você deve usar um editor que usa LF como um final de linha. Se você não tiver certeza se seu editor usa LF ou CRLF, consulte Olá [solução de problemas](#troubleshooting) seção etapas sobre como remover Olá caracteres CR.

## <a name="create-an-example-java-udf"></a>Criar UDF Java de exemplo 

1. De uma linha de comando, use Olá toocreate um novo projeto Maven a seguir:

    ```bash
    mvn archetype:generate -DgroupId=com.microsoft.examples -DartifactId=ExampleUDF -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
    ```

   > [!NOTE]
   > Se você estiver usando o PowerShell, você deve colocar entre aspas, parâmetros de saudação. Por exemplo: `mvn archetype:generate "-DgroupId=com.microsoft.examples" "-DartifactId=ExampleUDF" "-DarchetypeArtifactId=maven-archetype-quickstart" "-DinteractiveMode=false"`.

    Este comando cria um diretório chamado **exampleudf**, que contém o projeto Maven hello.

2. Depois que o projeto de saudação foi criado, excluir Olá **src/exampleudf/teste** diretório que foi criado como parte do projeto de saudação.

3. Olá abrir **exampleudf/pom.xml**e substituir Olá `<dependencies>` entrada hello XML a seguir:

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

    Essas entradas de especificar a versão de saudação do Hadoop e Hive incluído com o HDInsight 3.5. Você pode encontrar informações sobre versões de saudação do Hadoop e Hive fornecido com o HDInsight da saudação [o controle de versão do HDInsight componente](hdinsight-component-versioning.md) documento.

    Adicionar um `<build>` seção antes Olá `</project>` linha no final de saudação do arquivo hello. Esta seção deve conter Olá XML a seguir:

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

    Essas entradas definem como toobuild Olá projeto. Especificamente, versão de saudação do Java que Olá projeto usa e como toobuild uma uberjar para cluster de toohello de implantação.

    Salve o arquivo de saudação quando Olá foi alterado.

4. Renomear **exampleudf/src/main/java/com/microsoft/examples/App.java** muito**ExampleUDF.java**e, em seguida, abra o arquivo de saudação em seu editor.

5. Substitua o conteúdo de saudação do hello **ExampleUDF.java** de arquivos com os seguintes hello e salve o arquivo de saudação.

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

    Esse código implementa um UDF que aceita um valor de cadeia de caracteres e retorna uma versão minúscula de cadeia de caracteres de saudação.

## <a name="build-and-install-hello-udf"></a>Crie e instale Olá UDF

1. Use Olá toocompile de comando a seguir e Olá UDF do pacote:

    ```bash
    mvn compile package
    ```

    Este comando cria e pacotes Olá UDF em Olá `exampleudf/target/ExampleUDF-1.0-SNAPSHOT.jar` arquivo.

2. Saudação de uso `scp` cluster HDInsight toohello de arquivos do comando toocopy hello.

    ```bash
    scp ./target/ExampleUDF-1.0-SNAPSHOT.jar myuser@mycluster-ssh.azurehdinsight
    ```

    Substituir `myuser` com hello SSH a conta de usuário para seu cluster. Substituir `mycluster` com o nome do cluster hello. Se você usou uma saudação de toosecure de senha SSH conta, você é solicitadas tooenter Olá por senha. Se você usou um certificado, talvez seja necessário Olá toouse `-i` parâmetro toospecify Olá arquivo de chave privada.

3. Conecte-se toohello cluster usando o SSH.

    ```bash
    ssh myuser@mycluster-ssh.azurehdinsight.net
    ```

    Para obter mais informações, confira [Usar SSH com HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

4. Da sessão SSH Olá, copie o armazenamento de tooHDInsight de arquivos jar hello.

    ```bash
    hdfs dfs -put ExampleUDF-1.0-SNAPSHOT.jar /example/jars
    ```

## <a name="use-hello-udf-from-hive"></a>Usar Olá UDF de Hive

1. Use Olá cliente de Beeline toostart Olá da sessão SSH Olá a seguir.

    ```bash
    beeline -u 'jdbc:hive2://localhost:10001/;transportMode=http' -n admin
    ```

    Esse comando assume que você usou padrão Olá **admin** Olá conta de logon para o cluster.

2. Quando chegar à saudação `jdbc:hive2://localhost:10001/>` prompt, digite Olá tooadd Olá UDF tooHive a seguir e expô-lo como uma função.

    ```hiveql
    ADD JAR wasb:///example/jars/ExampleUDF-1.0-SNAPSHOT.jar;
    CREATE TEMPORARY FUNCTION tolower as 'com.microsoft.examples.ExampleUDF';
    ```

    > [!NOTE]
    > Este exemplo presume que o armazenamento do Azure é o armazenamento padrão para cluster hello. Se o cluster usa o repositório Data Lake em vez disso, alterar Olá `wasb:///` valor muito`adl:///`.

3. Use Olá UDF tooconvert valores recuperados de uma cadeias de caracteres tabela toolower maiusculas.

    ```hiveql
    SELECT tolower(deviceplatform) FROM hivesampletable LIMIT 10;
    ```

    Esta consulta selecionará Olá plataforma de dispositivo (Android, Windows, iOS, etc.) da tabela Olá, converta o caso de toolower de cadeia de caracteres de saudação e exibi-los. saída de Hello aparece semelhante toohello texto a seguir:

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

## <a name="next-steps"></a>Próximas etapas

Para outros toowork maneiras com Hive, consulte [uso de Hive do HDInsight](hdinsight-use-hive.md).

Para obter mais informações sobre as funções de Hive User-Defined, consulte [Hive operadores e funções definidas pelo usuário](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF) seção Olá Hive wiki em apache.org.
