---
title: "Exemplo de topologia Java do Apache Storm – Azure HDInsight | Microsoft Docs"
description: Aprenda a criar topologias Apache Storm em Java criando um exemplo de topologia de contagem de palavras.
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
keywords: apache storm, exemplo de apache storm, storm java, exemplo de topologia storm
ms.assetid: a8838f29-9c08-4fd9-99ef-26655d1bf6d7
ms.service: hdinsight
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/07/2017
ms.author: larryfr
ms.custom: H1Hack27Feb2017,hdinsightactive,hdiseo17may2017
ms.openlocfilehash: 36285fbaf1da3c566d338bd5612eebad327eaf50
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="create-an-apache-storm-topology-in-java"></a><span data-ttu-id="f5429-104">Criar uma topologia Apache Storm em Java</span><span class="sxs-lookup"><span data-stu-id="f5429-104">Create an Apache Storm topology in Java</span></span>

<span data-ttu-id="f5429-105">Aprenda a criar uma topologia baseada em Java para o Apache Storm.</span><span class="sxs-lookup"><span data-stu-id="f5429-105">Learn how to create a Java-based topology for Apache Storm.</span></span> <span data-ttu-id="f5429-106">Crie uma topologia Storm que implementa um aplicativo de contagem de palavras.</span><span class="sxs-lookup"><span data-stu-id="f5429-106">You create a Storm topology that implements a word-count application.</span></span> <span data-ttu-id="f5429-107">Use o Maven para compilar e empacotar o projeto.</span><span class="sxs-lookup"><span data-stu-id="f5429-107">You use Maven to build and package the project.</span></span> <span data-ttu-id="f5429-108">Em seguida, você aprenderá como definir a topologia usando a estrutura Flux.</span><span class="sxs-lookup"><span data-stu-id="f5429-108">Then, you learn how to define the topology using the Flux framework.</span></span>

> [!NOTE]
> <span data-ttu-id="f5429-109">A estrutura Flux está disponível no Storm 0.10.0 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="f5429-109">The Flux framework is available in Storm 0.10.0 or later.</span></span> <span data-ttu-id="f5429-110">O Storm 0.10.0 está disponível com o HDInsight 3.3 e 3.4.</span><span class="sxs-lookup"><span data-stu-id="f5429-110">Storm 0.10.0 is available with HDInsight 3.3 and 3.4.</span></span>

<span data-ttu-id="f5429-111">Depois de concluir as etapas neste documento, você pode implantar a topologia para o Apache Storm no HDInsight.</span><span class="sxs-lookup"><span data-stu-id="f5429-111">After completing the steps in this document, you can deploy the topology to Apache Storm on HDInsight.</span></span>

> [!NOTE]
> <span data-ttu-id="f5429-112">Uma versão completa do exemplo de topologia Storm criado neste documento está disponível em [https://github.com/Azure-Samples/hdinsight-java-storm-wordcount](https://github.com/Azure-Samples/hdinsight-java-storm-wordcount).</span><span class="sxs-lookup"><span data-stu-id="f5429-112">A completed version of the Storm topology examples created in this document is available at [https://github.com/Azure-Samples/hdinsight-java-storm-wordcount](https://github.com/Azure-Samples/hdinsight-java-storm-wordcount).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f5429-113">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="f5429-113">Prerequisites</span></span>

* [<span data-ttu-id="f5429-114">Java Developer Kit (JDK) versão 7</span><span class="sxs-lookup"><span data-stu-id="f5429-114">Java Developer Kit (JDK) version 7</span></span>](https://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html)

* <span data-ttu-id="f5429-115">[Maven (https://maven.apache.org/download.cgi)](https://maven.apache.org/download.cgi): Maven é um sistema de compilação do projeto para projetos Java.</span><span class="sxs-lookup"><span data-stu-id="f5429-115">[Maven (https://maven.apache.org/download.cgi)](https://maven.apache.org/download.cgi): Maven is a project build system for Java projects.</span></span>

* <span data-ttu-id="f5429-116">Um editor de texto ou IDE.</span><span class="sxs-lookup"><span data-stu-id="f5429-116">A text editor or IDE.</span></span>

## <a name="configure-environment-variables"></a><span data-ttu-id="f5429-117">Configurar variáveis de ambiente</span><span class="sxs-lookup"><span data-stu-id="f5429-117">Configure environment variables</span></span>

<span data-ttu-id="f5429-118">As seguintes variáveis de ambiente podem ser definidas quando você instala o Java e o JDK.</span><span class="sxs-lookup"><span data-stu-id="f5429-118">The following environment variables may be set when you install Java and the JDK.</span></span> <span data-ttu-id="f5429-119">No entanto, você deve verificar se elas existem e se contêm os valores corretos para o seu sistema.</span><span class="sxs-lookup"><span data-stu-id="f5429-119">However, you should check that they exist and that they contain the correct values for your system.</span></span>

* <span data-ttu-id="f5429-120">**JAVA_HOME** - deve apontar para o diretório onde o JRE (Java runtime environment) está instalado.</span><span class="sxs-lookup"><span data-stu-id="f5429-120">**JAVA_HOME** - should point to the directory where the Java runtime environment (JRE) is installed.</span></span> <span data-ttu-id="f5429-121">Por exemplo, em uma distribuição Unix ou Linux, ele deve ter um valor semelhante a `/usr/lib/jvm/java-7-oracle`.</span><span class="sxs-lookup"><span data-stu-id="f5429-121">For example, in a Unix or Linux distribution, it should have a value similar to `/usr/lib/jvm/java-7-oracle`.</span></span> <span data-ttu-id="f5429-122">No Windows, ele teria um valor semelhante a `c:\Program Files (x86)\Java\jre1.7`</span><span class="sxs-lookup"><span data-stu-id="f5429-122">In Windows, it would have a value similar to `c:\Program Files (x86)\Java\jre1.7`</span></span>

* <span data-ttu-id="f5429-123">**PATH** - deve conter os seguintes caminhos:</span><span class="sxs-lookup"><span data-stu-id="f5429-123">**PATH** - should contain the following paths:</span></span>

  * <span data-ttu-id="f5429-124">**JAVA_HOME** (ou o caminho equivalente)</span><span class="sxs-lookup"><span data-stu-id="f5429-124">**JAVA_HOME** (or the equivalent path)</span></span>

  * <span data-ttu-id="f5429-125">**JAVA_HOME\bin** (ou o caminho equivalente)</span><span class="sxs-lookup"><span data-stu-id="f5429-125">**JAVA_HOME\bin** (or the equivalent path)</span></span>

  * <span data-ttu-id="f5429-126">O diretório onde o Maven está instalado</span><span class="sxs-lookup"><span data-stu-id="f5429-126">The directory where Maven is installed</span></span>

## <a name="create-a-maven-project"></a><span data-ttu-id="f5429-127">Criar um projeto do Maven</span><span class="sxs-lookup"><span data-stu-id="f5429-127">Create a Maven project</span></span>

<span data-ttu-id="f5429-128">Na linha de comando, use o seguinte comando para criar um novo projeto do Maven chamado **WordCount**:</span><span class="sxs-lookup"><span data-stu-id="f5429-128">From the command line, use the following command to create a Maven project named **WordCount**:</span></span>

```bash
mvn archetype:generate -DarchetypeArtifactId=maven-archetype-quickstart -DgroupId=com.microsoft.example -DartifactId=WordCount -DinteractiveMode=false
```

> [!NOTE]
> <span data-ttu-id="f5429-129">Se você estiver usando o PowerShell, coloque os parâmetros `-D` com aspas duplas.</span><span class="sxs-lookup"><span data-stu-id="f5429-129">If you are using PowerShell, you must surround the`-D` parameters with double quotes.</span></span>
>
> `mvn archetype:generate "-DarchetypeArtifactId=maven-archetype-quickstart" "-DgroupId=com.microsoft.example" "-DartifactId=WordCount" "-DinteractiveMode=false"`

<span data-ttu-id="f5429-130">Esse comando cria um diretório chamado `WordCount` no local atual, que contém um projeto básico do Maven.</span><span class="sxs-lookup"><span data-stu-id="f5429-130">This command creates a directory named `WordCount` at the current location, which contains a basic Maven project.</span></span> <span data-ttu-id="f5429-131">O diretório `WordCount` contém os seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="f5429-131">The `WordCount` directory contains the following items:</span></span>

* <span data-ttu-id="f5429-132">`pom.xml`: contém configurações para o projeto Maven.</span><span class="sxs-lookup"><span data-stu-id="f5429-132">`pom.xml`: Contains settings for the Maven project.</span></span>
* <span data-ttu-id="f5429-133">`src\main\java\com\microsoft\example`: contém o código do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="f5429-133">`src\main\java\com\microsoft\example`: Contains your application code.</span></span>
* <span data-ttu-id="f5429-134">`src\test\java\com\microsoft\example`: contém testes para o seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="f5429-134">`src\test\java\com\microsoft\example`: Contains tests for your application.</span></span> 

### <a name="remove-the-generated-example-code"></a><span data-ttu-id="f5429-135">Remover o exemplo de código gerado</span><span class="sxs-lookup"><span data-stu-id="f5429-135">Remove the generated example code</span></span>

<span data-ttu-id="f5429-136">Exclua o teste gerado e os arquivos do aplicativo:</span><span class="sxs-lookup"><span data-stu-id="f5429-136">Delete the generated test and the application files:</span></span>

* <span data-ttu-id="f5429-137">**src\test\java\com\microsoft\example\AppTest.java**</span><span class="sxs-lookup"><span data-stu-id="f5429-137">**src\test\java\com\microsoft\example\AppTest.java**</span></span>
* <span data-ttu-id="f5429-138">**src\main\java\com\microsoft\example\App.java**</span><span class="sxs-lookup"><span data-stu-id="f5429-138">**src\main\java\com\microsoft\example\App.java**</span></span>

## <a name="add-maven-repositories"></a><span data-ttu-id="f5429-139">Adicionar repositórios Maven</span><span class="sxs-lookup"><span data-stu-id="f5429-139">Add Maven repositories</span></span>

<span data-ttu-id="f5429-140">Como o HDInsight tem base no HDP (Hortonworks Data Platform), recomendamos o uso do repositório Hortonworks para baixar dependências de seus projetos do Apache Storm.</span><span class="sxs-lookup"><span data-stu-id="f5429-140">HDInsight is based on the Hortonworks Data Platform (HDP), so we recommend using the Hortonworks repository to download dependencies for your Apache Storm projects.</span></span> <span data-ttu-id="f5429-141">No arquivo __pom.xml__, adicione o seguinte XML após a linha `<url>http://maven.apache.org</url>`:</span><span class="sxs-lookup"><span data-stu-id="f5429-141">In the __pom.xml__ file, add the following XML after the `<url>http://maven.apache.org</url>` line:</span></span>

```xml
<repositories>
    <repository>
        <releases>
            <enabled>true</enabled>
            <updatePolicy>always</updatePolicy>
            <checksumPolicy>warn</checksumPolicy>
        </releases>
        <snapshots>
            <enabled>false</enabled>
            <updatePolicy>never</updatePolicy>
            <checksumPolicy>fail</checksumPolicy>
        </snapshots>
        <id>HDPReleases</id>
        <name>HDP Releases</name>
        <url>http://repo.hortonworks.com/content/repositories/releases/</url>
        <layout>default</layout>
    </repository>
    <repository>
        <releases>
            <enabled>true</enabled>
            <updatePolicy>always</updatePolicy>
            <checksumPolicy>warn</checksumPolicy>
        </releases>
        <snapshots>
            <enabled>false</enabled>
            <updatePolicy>never</updatePolicy>
            <checksumPolicy>fail</checksumPolicy>
        </snapshots>
        <id>HDPJetty</id>
        <name>Hadoop Jetty</name>
        <url>http://repo.hortonworks.com/content/repositories/jetty-hadoop/</url>
        <layout>default</layout>
    </repository>
</repositories>
```

## <a name="add-properties"></a><span data-ttu-id="f5429-142">Adicionar propriedades</span><span class="sxs-lookup"><span data-stu-id="f5429-142">Add properties</span></span>

<span data-ttu-id="f5429-143">O Maven permite que você defina valores de nível de projeto chamados propriedades.</span><span class="sxs-lookup"><span data-stu-id="f5429-143">Maven allows you to define project-level values called properties.</span></span> <span data-ttu-id="f5429-144">No __pom.xml__, adicione o texto a seguir após a linha `</repositories>`:</span><span class="sxs-lookup"><span data-stu-id="f5429-144">In the __pom.xml__, add the following text after the `</repositories>` line:</span></span>

```xml
<properties>
    <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
    <!--
    This is a version of Storm from the Hortonworks repository that is compatible with HDInsight.
    -->
    <storm.version>1.0.1.2.5.3.0-37</storm.version>
</properties>
```

<span data-ttu-id="f5429-145">Agora você pode usar esse valor em outras seções do `pom.xml`.</span><span class="sxs-lookup"><span data-stu-id="f5429-145">You can now use this value in other sections of the `pom.xml`.</span></span> <span data-ttu-id="f5429-146">Por exemplo, ao especificar a versão dos componentes do Storm, podemos usar `${storm.version}` em vez de fazer hard-coding de um valor.</span><span class="sxs-lookup"><span data-stu-id="f5429-146">For example, when specifying the version of Storm components, you can use `${storm.version}` instead of hard coding a value.</span></span>

## <a name="add-dependencies"></a><span data-ttu-id="f5429-147">Adicionar dependências</span><span class="sxs-lookup"><span data-stu-id="f5429-147">Add dependencies</span></span>

<span data-ttu-id="f5429-148">Adicione uma dependência para componentes do Storm.</span><span class="sxs-lookup"><span data-stu-id="f5429-148">Add a dependency for Storm components.</span></span> <span data-ttu-id="f5429-149">Abra o arquivo `pom.xml` e adicione o seguinte código na seção `<dependencies>`:</span><span class="sxs-lookup"><span data-stu-id="f5429-149">Open the `pom.xml` file and add the following code in the `<dependencies>` section:</span></span>

```xml
<dependency>
    <groupId>org.apache.storm</groupId>
    <artifactId>storm-core</artifactId>
    <version>${storm.version}</version>
    <!-- keep storm out of the jar-with-dependencies -->
    <scope>provided</scope>
</dependency>
```

<span data-ttu-id="f5429-150">No momento da compilação, o Maven usa essas informações para pesquisar `storm-core` no repositório Maven.</span><span class="sxs-lookup"><span data-stu-id="f5429-150">At compile time, Maven uses this information to look up `storm-core` in the Maven repository.</span></span> <span data-ttu-id="f5429-151">Ele primeiro procura no repositório em seu computador local.</span><span class="sxs-lookup"><span data-stu-id="f5429-151">It first looks in the repository on your local computer.</span></span> <span data-ttu-id="f5429-152">Se os arquivos não estiverem lá, o Maven os baixará do repositório Maven público e os armazenará no repositório local.</span><span class="sxs-lookup"><span data-stu-id="f5429-152">If the files aren't there, Maven downloads them from the public Maven repository and stores them in the local repository.</span></span>

> [!NOTE]
> <span data-ttu-id="f5429-153">Observe a linha `<scope>provided</scope>` nesta seção.</span><span class="sxs-lookup"><span data-stu-id="f5429-153">Notice the `<scope>provided</scope>` line in this section.</span></span> <span data-ttu-id="f5429-154">Essa configuração informa ao Maven para excluir o **storm-core** de qualquer arquivo JAR criado, pois ele será fornecido pelo sistema.</span><span class="sxs-lookup"><span data-stu-id="f5429-154">This setting tells Maven to exclude **storm-core** from any JAR files that are created, because it is provided by the system.</span></span>

## <a name="build-configuration"></a><span data-ttu-id="f5429-155">Configuração de compilação</span><span class="sxs-lookup"><span data-stu-id="f5429-155">Build configuration</span></span>

<span data-ttu-id="f5429-156">Plug-ins do Maven permitem que você personalize os estágios de compilação do projeto.</span><span class="sxs-lookup"><span data-stu-id="f5429-156">Maven plug-ins allow you to customize the build stages of the project.</span></span> <span data-ttu-id="f5429-157">Por exemplo, como o projeto é compilado ou como compactá-lo em um arquivo JAR.</span><span class="sxs-lookup"><span data-stu-id="f5429-157">For example, how the project is compiled or how to package it into a JAR file.</span></span> <span data-ttu-id="f5429-158">Abra o arquivo `pom.xml` e adicione o seguinte código na seção diretamente acima da linha `</project>`.</span><span class="sxs-lookup"><span data-stu-id="f5429-158">Open the `pom.xml` file and add the following code directly above the `</project>` line.</span></span>

```xml
<build>
    <plugins>
    </plugins>
    <resources>
    </resources>
</build>
```

<span data-ttu-id="f5429-159">Esta seção será usada para adicionar plug-ins, recursos e outras opções de configuração de compilação.</span><span class="sxs-lookup"><span data-stu-id="f5429-159">This section is used to add plug-ins, resources, and other build configuration options.</span></span> <span data-ttu-id="f5429-160">Para obter uma referência completa do arquivo **pom.xml**, consulte [http://maven.apache.org/pom.html](http://maven.apache.org/pom.html).</span><span class="sxs-lookup"><span data-stu-id="f5429-160">For a full reference of the **pom.xml** file, see [http://maven.apache.org/pom.html](http://maven.apache.org/pom.html).</span></span>

### <a name="add-plug-ins"></a><span data-ttu-id="f5429-161">Adicionar plug-ins</span><span class="sxs-lookup"><span data-stu-id="f5429-161">Add plug-ins</span></span>

<span data-ttu-id="f5429-162">Para topologias Apache Storm implementadas em Java, o [plug-in Maven Exec](http://www.mojohaus.org/exec-maven-plugin/) é útil porque permite que você execute com facilidade a topologia localmente em seu ambiente de desenvolvimento.</span><span class="sxs-lookup"><span data-stu-id="f5429-162">For Apache Storm topologies implemented in Java, the [Exec Maven Plugin](http://www.mojohaus.org/exec-maven-plugin/) is useful because it allows you to easily run the topology locally in your development environment.</span></span> <span data-ttu-id="f5429-163">Adicione o seguinte à seção `<plugins>` do arquivo `pom.xml` para incluir o plug-in Exec Maven:</span><span class="sxs-lookup"><span data-stu-id="f5429-163">Add the following to the `<plugins>` section of the `pom.xml` file to include the Exec Maven plugin:</span></span>

```xml
<plugin>
    <groupId>org.codehaus.mojo</groupId>
    <artifactId>exec-maven-plugin</artifactId>
    <version>1.4.0</version>
    <executions>
    <execution>
    <goals>
        <goal>exec</goal>
    </goals>
    </execution>
    </executions>
    <configuration>
    <executable>java</executable>
    <includeProjectDependencies>true</includeProjectDependencies>
    <includePluginDependencies>false</includePluginDependencies>
    <classpathScope>compile</classpathScope>
    <mainClass>${storm.topology}</mainClass>
    <cleanupDaemonThreads>false</cleanupDaemonThreads> 
    </configuration>
</plugin>
```

<span data-ttu-id="f5429-164">Outro plug-in útil é o [Plug-in do compilador Apache Maven](http://maven.apache.org/plugins/maven-compiler-plugin/), que é usado para alterar opções de compilação.</span><span class="sxs-lookup"><span data-stu-id="f5429-164">Another useful plug-in is the [Apache Maven Compiler Plugin](http://maven.apache.org/plugins/maven-compiler-plugin/), which is used to change compilation options.</span></span> <span data-ttu-id="f5429-165">Ele muda a versão do Java que o Maven usa para a origem e o destino de seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="f5429-165">The changes the Java version that Maven uses for the source and target for your application.</span></span>

* <span data-ttu-id="f5429-166">Para HDInsight __3.4 ou anterior__, defina a versão Java de origem e de destino como __1.7__.</span><span class="sxs-lookup"><span data-stu-id="f5429-166">For HDInsight __3.4 or earlier__, set the source and target Java version to __1.7__.</span></span>

* <span data-ttu-id="f5429-167">Para HDInsight __3.5__, defina a versão Java de origem e de destino como __1.8__.</span><span class="sxs-lookup"><span data-stu-id="f5429-167">For HDInsight __3.5__, set the source and target Java version to __1.8__.</span></span>

<span data-ttu-id="f5429-168">Adicione o seguinte texto à seção `<plugins>` do arquivo `pom.xml` para incluir o plug-in Compilador do Apache Maven.</span><span class="sxs-lookup"><span data-stu-id="f5429-168">Add the following text in the `<plugins>` section of the `pom.xml` file to include the Apache Maven Compiler plugin.</span></span> <span data-ttu-id="f5429-169">Este exemplo especifica a versão 1.8. Portanto, a versão do HDInsight de destino será a 3.5.</span><span class="sxs-lookup"><span data-stu-id="f5429-169">This example specifies 1.8, so the target HDInsight version is 3.5.</span></span>

```xml
<plugin>
    <groupId>org.apache.maven.plugins</groupId>
    <artifactId>maven-compiler-plugin</artifactId>
    <version>3.3</version>
    <configuration>
    <source>1.8</source>
    <target>1.8</target>
    </configuration>
</plugin>
```

### <a name="configure-resources"></a><span data-ttu-id="f5429-170">Configurar recursos</span><span class="sxs-lookup"><span data-stu-id="f5429-170">Configure resources</span></span>

<span data-ttu-id="f5429-171">A seção de recursos permite que você inclua recursos que não são código, por exemplo, arquivos de configuração necessários aos componentes na topologia.</span><span class="sxs-lookup"><span data-stu-id="f5429-171">The resources section allows you to include non-code resources such as configuration files needed by components in the topology.</span></span> <span data-ttu-id="f5429-172">Para este exemplo, adicione o texto a seguir na seção `<resources>` do arquivo pom.xml.</span><span class="sxs-lookup"><span data-stu-id="f5429-172">For this example, add the following text in the `<resources>` section of the \`pom.xml file.</span></span>

```xml
<resource>
    <directory>${basedir}/resources</directory>
    <filtering>false</filtering>
    <includes>
        <include>log4j2.xml</include>
    </includes>
</resource>
```

<span data-ttu-id="f5429-173">Esse exemplo adiciona o diretório de recursos na raiz do projeto (`${basedir}`) como um local que contém os recursos e inclui o arquivo `log4j2.xml`.</span><span class="sxs-lookup"><span data-stu-id="f5429-173">This example adds the resources directory in the root of the project (`${basedir}`) as a location that contains resources, and includes the file named `log4j2.xml`.</span></span> <span data-ttu-id="f5429-174">Esse arquivo é usado para configurar quais informações são registradas pela topologia.</span><span class="sxs-lookup"><span data-stu-id="f5429-174">This file is used to configure what information is logged by the topology.</span></span>

## <a name="create-the-topology"></a><span data-ttu-id="f5429-175">Criar a topologia</span><span class="sxs-lookup"><span data-stu-id="f5429-175">Create the topology</span></span>

<span data-ttu-id="f5429-176">Uma topologia Apache Storm baseada em Java consiste em três componentes que você deve criar (ou referenciar) como uma dependência.</span><span class="sxs-lookup"><span data-stu-id="f5429-176">A Java-based Apache Storm topology consists of three components that you must author (or reference) as a dependency.</span></span>

* <span data-ttu-id="f5429-177">**Spouts**: lê dados de fontes externas e a emite fluxos de dados para a topologia.</span><span class="sxs-lookup"><span data-stu-id="f5429-177">**Spouts**: Reads data from external sources and emits streams of data into the topology.</span></span>

* <span data-ttu-id="f5429-178">**Bolts**: executa processamento em fluxos emitidos por spouts ou outros bolts e emite um ou mais fluxos.</span><span class="sxs-lookup"><span data-stu-id="f5429-178">**Bolts**: Performs processing on streams emitted by spouts or other bolts, and emits one or more streams.</span></span>

* <span data-ttu-id="f5429-179">**Topologia**: define como os spouts e bolts são organizados e fornece o ponto de entrada para a topologia.</span><span class="sxs-lookup"><span data-stu-id="f5429-179">**Topology**: Defines how the spouts and bolts are arranged, and provides the entry point for the topology.</span></span>

### <a name="create-the-spout"></a><span data-ttu-id="f5429-180">Criar o spout</span><span class="sxs-lookup"><span data-stu-id="f5429-180">Create the spout</span></span>

<span data-ttu-id="f5429-181">Para reduzir os requisitos para configurar fontes de dados externas, o seguinte spout simplesmente emite sentenças aleatórias.</span><span class="sxs-lookup"><span data-stu-id="f5429-181">To reduce requirements for setting up external data sources, the following spout simply emits random sentences.</span></span> <span data-ttu-id="f5429-182">É uma versão modificada de um spout fornecido com os [exemplos Storm-Starter](https://github.com/apache/storm/blob/0.10.x-branch/examples/storm-starter/src/jvm/storm/starter).</span><span class="sxs-lookup"><span data-stu-id="f5429-182">It is a modified version of a spout that is provided with the [Storm-Starter examples](https://github.com/apache/storm/blob/0.10.x-branch/examples/storm-starter/src/jvm/storm/starter).</span></span>

> [!NOTE]
> <span data-ttu-id="f5429-183">Para obter um exemplo de um spout que lê de uma fonte de dados externa, consulte um dos exemplos a seguir:</span><span class="sxs-lookup"><span data-stu-id="f5429-183">For an example of a spout that reads from an external data source, see one of the following examples:</span></span>
>
> * <span data-ttu-id="f5429-184">[TwitterSampleSPout](https://github.com/apache/storm/blob/0.10.x-branch/examples/storm-starter/src/jvm/storm/starter/spout/TwitterSampleSpout.java): um spout de exemplo que lê do Twitter</span><span class="sxs-lookup"><span data-stu-id="f5429-184">[TwitterSampleSPout](https://github.com/apache/storm/blob/0.10.x-branch/examples/storm-starter/src/jvm/storm/starter/spout/TwitterSampleSpout.java): An example spout that reads from Twitter</span></span>
> * <span data-ttu-id="f5429-185">[Storm-Kafka](https://github.com/apache/storm/tree/0.10.x-branch/external/storm-kafka): um spout que lê do Kafka</span><span class="sxs-lookup"><span data-stu-id="f5429-185">[Storm-Kafka](https://github.com/apache/storm/tree/0.10.x-branch/external/storm-kafka): A spout that reads from Kafka</span></span>

<span data-ttu-id="f5429-186">Para o spout, crie um arquivo chamado `RandomSentenceSpout.java` no diretório `src\main\java\com\microsoft\example` e use o código Java a seguir como conteúdo:</span><span class="sxs-lookup"><span data-stu-id="f5429-186">For the spout, create a file named `RandomSentenceSpout.java` in the `src\main\java\com\microsoft\example` directory and use the following Java code as the contents:</span></span>

```java
package com.microsoft.example;

import org.apache.storm.spout.SpoutOutputCollector;
import org.apache.storm.task.TopologyContext;
import org.apache.storm.topology.OutputFieldsDeclarer;
import org.apache.storm.topology.base.BaseRichSpout;
import org.apache.storm.tuple.Fields;
import org.apache.storm.tuple.Values;
import org.apache.storm.utils.Utils;

import java.util.Map;
import java.util.Random;

//This spout randomly emits sentences
public class RandomSentenceSpout extends BaseRichSpout {
  //Collector used to emit output
  SpoutOutputCollector _collector;
  //Used to generate a random number
  Random _rand;

  //Open is called when an instance of the class is created
  @Override
  public void open(Map conf, TopologyContext context, SpoutOutputCollector collector) {
  //Set the instance collector to the one passed in
    _collector = collector;
    //For randomness
    _rand = new Random();
  }

  //Emit data to the stream
  @Override
  public void nextTuple() {
  //Sleep for a bit
    Utils.sleep(100);
    //The sentences that are randomly emitted
    String[] sentences = new String[]{ "the cow jumped over the moon", "an apple a day keeps the doctor away",
        "four score and seven years ago", "snow white and the seven dwarfs", "i am at two with nature" };
    //Randomly pick a sentence
    String sentence = sentences[_rand.nextInt(sentences.length)];
    //Emit the sentence
    _collector.emit(new Values(sentence));
  }

  //Ack is not implemented since this is a basic example
  @Override
  public void ack(Object id) {
  }

  //Fail is not implemented since this is a basic example
  @Override
  public void fail(Object id) {
  }

  //Declare the output fields. In this case, an sentence
  @Override
  public void declareOutputFields(OutputFieldsDeclarer declarer) {
    declarer.declare(new Fields("sentence"));
  }
}
```

> [!NOTE]
> <span data-ttu-id="f5429-187">Embora essa topologia use apenas um spout, outras pessoas poderão ter vários que alimentam dados de origens diferentes na topologia.</span><span class="sxs-lookup"><span data-stu-id="f5429-187">Although this topology uses only one spout, others may have several that feed data from different sources into the topology.</span></span>

### <a name="create-the-bolts"></a><span data-ttu-id="f5429-188">Criar os bolts</span><span class="sxs-lookup"><span data-stu-id="f5429-188">Create the bolts</span></span>

<span data-ttu-id="f5429-189">Bolts manipulam o processamento de dados.</span><span class="sxs-lookup"><span data-stu-id="f5429-189">Bolts handle the data processing.</span></span> <span data-ttu-id="f5429-190">Essa topologia usa dois bolts:</span><span class="sxs-lookup"><span data-stu-id="f5429-190">This topology uses two bolts:</span></span>

* <span data-ttu-id="f5429-191">**SplitSentence**: divide as sentenças emitidas por **RandomSentenceSpout** em palavras individuais.</span><span class="sxs-lookup"><span data-stu-id="f5429-191">**SplitSentence**: Splits the sentences emitted by **RandomSentenceSpout** into individual words.</span></span>

* <span data-ttu-id="f5429-192">**WordCount**: conta quantas vezes cada palavra ocorreu.</span><span class="sxs-lookup"><span data-stu-id="f5429-192">**WordCount**: Counts how many times each word has occurred.</span></span>

> [!NOTE]
> <span data-ttu-id="f5429-193">Os bolts podem fazer qualquer coisa, por exemplo, computação, persistência ou conversar com componentes externos.</span><span class="sxs-lookup"><span data-stu-id="f5429-193">Bolts can do anything, for example, computation, persistence, or talking to external components.</span></span>

<span data-ttu-id="f5429-194">Crie dois novos arquivos, `SplitSentence.java` e `WordCount.java`, no diretório `src\main\java\com\microsoft\example`.</span><span class="sxs-lookup"><span data-stu-id="f5429-194">Create two new files, `SplitSentence.java` and `WordCount.java` in the `src\main\java\com\microsoft\example` directory.</span></span> <span data-ttu-id="f5429-195">Use o texto a seguir como conteúdo dos arquivos:</span><span class="sxs-lookup"><span data-stu-id="f5429-195">Use the following text as the contents for the files:</span></span>

#### <a name="splitsentence"></a><span data-ttu-id="f5429-196">SplitSentence</span><span class="sxs-lookup"><span data-stu-id="f5429-196">SplitSentence</span></span>

```java
package com.microsoft.example;

import java.text.BreakIterator;

import org.apache.storm.topology.BasicOutputCollector;
import org.apache.storm.topology.OutputFieldsDeclarer;
import org.apache.storm.topology.base.BaseBasicBolt;
import org.apache.storm.tuple.Fields;
import org.apache.storm.tuple.Tuple;
import org.apache.storm.tuple.Values;

//There are a variety of bolt types. In this case, use BaseBasicBolt
public class SplitSentence extends BaseBasicBolt {

  //Execute is called to process tuples
  @Override
  public void execute(Tuple tuple, BasicOutputCollector collector) {
    //Get the sentence content from the tuple
    String sentence = tuple.getString(0);
    //An iterator to get each word
    BreakIterator boundary=BreakIterator.getWordInstance();
    //Give the iterator the sentence
    boundary.setText(sentence);
    //Find the beginning first word
    int start=boundary.first();
    //Iterate over each word and emit it to the output stream
    for (int end=boundary.next(); end != BreakIterator.DONE; start=end, end=boundary.next()) {
      //get the word
      String word=sentence.substring(start,end);
      //If a word is whitespace characters, replace it with empty
      word=word.replaceAll("\\s+","");
      //if it's an actual word, emit it
      if (!word.equals("")) {
        collector.emit(new Values(word));
      }
    }
  }

  //Declare that emitted tuples contain a word field
  @Override
  public void declareOutputFields(OutputFieldsDeclarer declarer) {
    declarer.declare(new Fields("word"));
  }
}
```

#### <a name="wordcount"></a><span data-ttu-id="f5429-197">WordCount</span><span class="sxs-lookup"><span data-stu-id="f5429-197">WordCount</span></span>

```java
package com.microsoft.example;

import java.util.HashMap;
import java.util.Map;
import java.util.Iterator;

import org.apache.storm.Constants;
import org.apache.storm.topology.BasicOutputCollector;
import org.apache.storm.topology.OutputFieldsDeclarer;
import org.apache.storm.topology.base.BaseBasicBolt;
import org.apache.storm.tuple.Fields;
import org.apache.storm.tuple.Tuple;
import org.apache.storm.tuple.Values;
import org.apache.storm.Config;

// For logging
import org.apache.logging.log4j.Logger;
import org.apache.logging.log4j.LogManager;

//There are a variety of bolt types. In this case, use BaseBasicBolt
public class WordCount extends BaseBasicBolt {
  //Create logger for this class
  private static final Logger logger = LogManager.getLogger(WordCount.class);
  //For holding words and counts
  Map<String, Integer> counts = new HashMap<String, Integer>();
  //How often to emit a count of words
  private Integer emitFrequency;

  // Default constructor
  public WordCount() {
      emitFrequency=5; // Default to 60 seconds
  }

  // Constructor that sets emit frequency
  public WordCount(Integer frequency) {
      emitFrequency=frequency;
  }

  //Configure frequency of tick tuples for this bolt
  //This delivers a 'tick' tuple on a specific interval,
  //which is used to trigger certain actions
  @Override
  public Map<String, Object> getComponentConfiguration() {
      Config conf = new Config();
      conf.put(Config.TOPOLOGY_TICK_TUPLE_FREQ_SECS, emitFrequency);
      return conf;
  }

  //execute is called to process tuples
  @Override
  public void execute(Tuple tuple, BasicOutputCollector collector) {
    //If it's a tick tuple, emit all words and counts
    if(tuple.getSourceComponent().equals(Constants.SYSTEM_COMPONENT_ID)
            && tuple.getSourceStreamId().equals(Constants.SYSTEM_TICK_STREAM_ID)) {
      for(String word : counts.keySet()) {
        Integer count = counts.get(word);
        collector.emit(new Values(word, count));
        logger.info("Emitting a count of " + count + " for word " + word);
      }
    } else {
      //Get the word contents from the tuple
      String word = tuple.getString(0);
      //Have we counted any already?
      Integer count = counts.get(word);
      if (count == null)
        count = 0;
      //Increment the count and store it
      count++;
      counts.put(word, count);
    }
  }

  //Declare that this emits a tuple containing two fields; word and count
  @Override
  public void declareOutputFields(OutputFieldsDeclarer declarer) {
    declarer.declare(new Fields("word", "count"));
  }
}
```

### <a name="define-the-topology"></a><span data-ttu-id="f5429-198">Definir a topologia</span><span class="sxs-lookup"><span data-stu-id="f5429-198">Define the topology</span></span>

<span data-ttu-id="f5429-199">A topologia vincula os spouts e bolts em um gráfico, que define como os dados fluem entre os componentes.</span><span class="sxs-lookup"><span data-stu-id="f5429-199">The topology ties the spouts and bolts together into a graph, which defines how data flows between the components.</span></span> <span data-ttu-id="f5429-200">Ele também fornece dicas de paralelismo que o Storm usará ao criar instâncias dos componentes de dentro do cluster.</span><span class="sxs-lookup"><span data-stu-id="f5429-200">It also provides parallelism hints that Storm uses when creating instances of the components within the cluster.</span></span>

<span data-ttu-id="f5429-201">A imagem a seguir é um diagrama básico do gráfico de componentes para esta topologia.</span><span class="sxs-lookup"><span data-stu-id="f5429-201">The following image is a basic diagram of the graph of components for this topology.</span></span>

![diagrama mostrando a organização de spouts e bolts](./media/hdinsight-storm-develop-java-topology/wordcount-topology.png)

<span data-ttu-id="f5429-203">Para implementar a topologia, crie um arquivo chamado `WordCountTopology.java` no diretório `src\main\java\com\microsoft\example`.</span><span class="sxs-lookup"><span data-stu-id="f5429-203">To implement the topology, create a file named `WordCountTopology.java` in the `src\main\java\com\microsoft\example` directory.</span></span> <span data-ttu-id="f5429-204">Use o seguinte código Java como o conteúdo do arquivo:</span><span class="sxs-lookup"><span data-stu-id="f5429-204">Use the following Java code as the contents of the file:</span></span>

```java
package com.microsoft.example;

import org.apache.storm.Config;
import org.apache.storm.LocalCluster;
import org.apache.storm.StormSubmitter;
import org.apache.storm.topology.TopologyBuilder;
import org.apache.storm.tuple.Fields;

import com.microsoft.example.RandomSentenceSpout;

public class WordCountTopology {

  //Entry point for the topology
  public static void main(String[] args) throws Exception {
  //Used to build the topology
    TopologyBuilder builder = new TopologyBuilder();
    //Add the spout, with a name of 'spout'
    //and parallelism hint of 5 executors
    builder.setSpout("spout", new RandomSentenceSpout(), 5);
    //Add the SplitSentence bolt, with a name of 'split'
    //and parallelism hint of 8 executors
    //shufflegrouping subscribes to the spout, and equally distributes
    //tuples (sentences) across instances of the SplitSentence bolt
    builder.setBolt("split", new SplitSentence(), 8).shuffleGrouping("spout");
    //Add the counter, with a name of 'count'
    //and parallelism hint of 12 executors
    //fieldsgrouping subscribes to the split bolt, and
    //ensures that the same word is sent to the same instance (group by field 'word')
    builder.setBolt("count", new WordCount(), 12).fieldsGrouping("split", new Fields("word"));

    //new configuration
    Config conf = new Config();
    //Set to false to disable debug information when
    // running in production on a cluster
    conf.setDebug(false);

    //If there are arguments, we are running on a cluster
    if (args != null && args.length > 0) {
      //parallelism hint to set the number of workers
      conf.setNumWorkers(3);
      //submit the topology
      StormSubmitter.submitTopology(args[0], conf, builder.createTopology());
    }
    //Otherwise, we are running locally
    else {
      //Cap the maximum number of executors that can be spawned
      //for a component to 3
      conf.setMaxTaskParallelism(3);
      //LocalCluster is used to run locally
      LocalCluster cluster = new LocalCluster();
      //submit the topology
      cluster.submitTopology("word-count", conf, builder.createTopology());
      //sleep
      Thread.sleep(10000);
      //shut down the cluster
      cluster.shutdown();
    }
  }
}
```

### <a name="configure-logging"></a><span data-ttu-id="f5429-205">Configurar o registro em log</span><span class="sxs-lookup"><span data-stu-id="f5429-205">Configure logging</span></span>

<span data-ttu-id="f5429-206">O Storm usa o Apache Log4j para registrar informações em log.</span><span class="sxs-lookup"><span data-stu-id="f5429-206">Storm uses Apache Log4j to log information.</span></span> <span data-ttu-id="f5429-207">Se você não configurar o log, a topologia emitirá informações de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="f5429-207">If you do not configure logging, the topology emits diagnostic information.</span></span> <span data-ttu-id="f5429-208">Para controlar o que é registrado, crie um arquivo chamado `log4j2.xml` no diretório `resources`.</span><span class="sxs-lookup"><span data-stu-id="f5429-208">To control what is logged, create a file named `log4j2.xml` in the `resources` directory.</span></span> <span data-ttu-id="f5429-209">Use o seguinte XML como o conteúdo do arquivo.</span><span class="sxs-lookup"><span data-stu-id="f5429-209">Use the following XML as the contents of the file.</span></span>

```xml
<?xml version="1.0" encoding="UTF-8"?>
<Configuration>
<Appenders>
    <Console name="STDOUT" target="SYSTEM_OUT">
        <PatternLayout pattern="%d{HH:mm:ss} [%t] %-5level %logger{36} - %msg%n"/>
    </Console>
</Appenders>
<Loggers>
    <Logger name="com.microsoft.example" level="trace" additivity="false">
        <AppenderRef ref="STDOUT"/>
    </Logger>
    <Root level="error">
        <Appender-Ref ref="STDOUT"/>
    </Root>
</Loggers>
</Configuration>
```

<span data-ttu-id="f5429-210">Esse XML configura um novo agente de log para a classe `com.microsoft.example`, que inclui os componentes nesta topologia de exemplo.</span><span class="sxs-lookup"><span data-stu-id="f5429-210">This XML configures a new logger for the `com.microsoft.example` class, which includes the components in this example topology.</span></span> <span data-ttu-id="f5429-211">O nível é definido como rastreamento para esse agente, que captura as informações de registro em log emitidas pelos componentes nessa topologia.</span><span class="sxs-lookup"><span data-stu-id="f5429-211">The level is set to trace for this logger, which captures any logging information emitted by components in this topology.</span></span>

<span data-ttu-id="f5429-212">A seção `<Root level="error">` configura o nível raiz do registro em log (tudo que não está em `com.microsoft.example`) para registrar apenas as informações de erro.</span><span class="sxs-lookup"><span data-stu-id="f5429-212">The `<Root level="error">` section configures the root level of logging (everything not in `com.microsoft.example`) to only log error information.</span></span>

<span data-ttu-id="f5429-213">Para saber mais sobre como configurar o registro em log para Log4j, confira [http://logging.apache.org/log4j/2.x/manual/configuration.html](http://logging.apache.org/log4j/2.x/manual/configuration.html).</span><span class="sxs-lookup"><span data-stu-id="f5429-213">For more information on configuring logging for Log4j, see [http://logging.apache.org/log4j/2.x/manual/configuration.html](http://logging.apache.org/log4j/2.x/manual/configuration.html).</span></span>

> [!NOTE]
> <span data-ttu-id="f5429-214">Storm versão 0.10.0 e superior usa Log4j 2.x.</span><span class="sxs-lookup"><span data-stu-id="f5429-214">Storm version 0.10.0 and higher use Log4j 2.x.</span></span> <span data-ttu-id="f5429-215">Versões mais antigas do storm usavam Log4j 1.x, que usava um formato diferente para a configuração de log.</span><span class="sxs-lookup"><span data-stu-id="f5429-215">Older versions of storm used Log4j 1.x, which used a different format for log configuration.</span></span> <span data-ttu-id="f5429-216">Para saber mais sobre a configuração mais antiga, confira [http://wiki.apache.org/logging-log4j/Log4jXmlFormat](http://wiki.apache.org/logging-log4j/Log4jXmlFormat).</span><span class="sxs-lookup"><span data-stu-id="f5429-216">For information on the older configuration, see [http://wiki.apache.org/logging-log4j/Log4jXmlFormat](http://wiki.apache.org/logging-log4j/Log4jXmlFormat).</span></span>

## <a name="test-the-topology-locally"></a><span data-ttu-id="f5429-217">Testar a topologia localmente</span><span class="sxs-lookup"><span data-stu-id="f5429-217">Test the topology locally</span></span>

<span data-ttu-id="f5429-218">Depois de salvar os arquivos, use o comando a seguir para testar a topologia localmente.</span><span class="sxs-lookup"><span data-stu-id="f5429-218">After you save the files, use the following command to test the topology locally.</span></span>

```bash
mvn compile exec:java -Dstorm.topology=com.microsoft.example.WordCountTopology
```

<span data-ttu-id="f5429-219">À medida que for executada, a topologia exibirá informações de inicialização.</span><span class="sxs-lookup"><span data-stu-id="f5429-219">As it runs, the topology displays startup information.</span></span> <span data-ttu-id="f5429-220">O texto a seguir é um exemplo da saída de contagem de palavras:</span><span class="sxs-lookup"><span data-stu-id="f5429-220">The following text is an example of the word count output:</span></span>

    17:33:27 [Thread-12-count] INFO  com.microsoft.example.WordCount - Emitting a count of 56 for word snow
    17:33:27 [Thread-12-count] INFO  com.microsoft.example.WordCount - Emitting a count of 56 for word white
    17:33:27 [Thread-12-count] INFO  com.microsoft.example.WordCount - Emitting a count of 112 for word seven
    17:33:27 [Thread-16-count] INFO  com.microsoft.example.WordCount - Emitting a count of 195 for word the
    17:33:27 [Thread-30-count] INFO  com.microsoft.example.WordCount - Emitting a count of 113 for word and
    17:33:27 [Thread-30-count] INFO  com.microsoft.example.WordCount - Emitting a count of 57 for word dwarfs
    17:33:27 [Thread-12-count] INFO  com.microsoft.example.WordCount - Emitting a count of 57 for word snow

<span data-ttu-id="f5429-221">Esse log de exemplo indica que a palavra 'and' foi emitida 113 vezes.</span><span class="sxs-lookup"><span data-stu-id="f5429-221">This example log indicates that the word 'and' has been emitted 113 times.</span></span> <span data-ttu-id="f5429-222">A contagem continuará a crescer enquanto a topologia for executada, uma vez que o spout emite continuamente as mesmas sentenças.</span><span class="sxs-lookup"><span data-stu-id="f5429-222">The count continues to go up as long as the topology runs because the spout continuously emits the same sentences.</span></span>

<span data-ttu-id="f5429-223">Há um intervalo de cinco segundos entre a emissão de palavras e as contagens.</span><span class="sxs-lookup"><span data-stu-id="f5429-223">There is a 5-second interval between emission of words and counts.</span></span> <span data-ttu-id="f5429-224">O componente **WordCount** está configurado para emitir informações somente quando chega uma tupla de escala.</span><span class="sxs-lookup"><span data-stu-id="f5429-224">The **WordCount** component is configured to only emit information when a tick tuple arrives.</span></span> <span data-ttu-id="f5429-225">Ele solicita que as tuplas de escala sejam entregues somente a cada cinco segundos.</span><span class="sxs-lookup"><span data-stu-id="f5429-225">It requests that tick tuples are only delivered every five seconds.</span></span>

## <a name="convert-the-topology-to-flux"></a><span data-ttu-id="f5429-226">Converter a topologia para Flux</span><span class="sxs-lookup"><span data-stu-id="f5429-226">Convert the topology to Flux</span></span>

<span data-ttu-id="f5429-227">Flux é uma nova estrutura disponível com o Storm 0.10.0 e superior, que permite que você separe a configuração da implementação.</span><span class="sxs-lookup"><span data-stu-id="f5429-227">Flux is a new framework available with Storm 0.10.0 and higher, which allows you to separate configuration from implementation.</span></span> <span data-ttu-id="f5429-228">Os componentes ainda são definidos em Java, mas a topologia é definida usando um arquivo YAML.</span><span class="sxs-lookup"><span data-stu-id="f5429-228">Your components are still defined in Java, but the topology is defined using a YAML file.</span></span> <span data-ttu-id="f5429-229">Você pode empacotar uma definição de topologia padrão com seu projeto, ou usar um arquivo autônomo ao enviar a topologia.</span><span class="sxs-lookup"><span data-stu-id="f5429-229">You can package a default topology definition with your project, or use a standalone file when submitting the topology.</span></span> <span data-ttu-id="f5429-230">Ao enviar a topologia para o Storm, você pode usar variáveis de ambiente ou arquivos de configuração para preencher os valores na definição de topologia YAML.</span><span class="sxs-lookup"><span data-stu-id="f5429-230">When submitting the topology to Storm, you can use environment variables or configuration files to populate values in the YAML topology definition.</span></span>

<span data-ttu-id="f5429-231">O arquivo YAML define os componentes a serem usados para a topologia, e o fluxo de os dados entre eles.</span><span class="sxs-lookup"><span data-stu-id="f5429-231">The YAML file defines the components to use for the topology and the data flow between them.</span></span> <span data-ttu-id="f5429-232">Você pode incluir um arquivo YAML como parte do arquivo jar ou usar um arquivo YAML externo.</span><span class="sxs-lookup"><span data-stu-id="f5429-232">You can include a YAML file as part of the jar file or you can use an external YAML file.</span></span>

<span data-ttu-id="f5429-233">Para saber mais sobre o Flux, veja [Estrutura do Flux (https://storm.apache.org/releases/0.10.0/flux.html)](https://storm.apache.org/releases/0.10.0/flux.html).</span><span class="sxs-lookup"><span data-stu-id="f5429-233">For more information on Flux, see [Flux framework (https://storm.apache.org/releases/0.10.0/flux.html)](https://storm.apache.org/releases/0.10.0/flux.html).</span></span>

> [!WARNING]
> <span data-ttu-id="f5429-234">Devido a um [bug (https://issues.apache.org/jira/browse/STORM-2055)](https://issues.apache.org/jira/browse/STORM-2055) no Storm 1.0.1, talvez você precise instalar um [ambiente de desenvolvimento do Storm](https://storm.apache.org/releases/1.0.1/Setting-up-development-environment.html) para executar topologias do Flux localmente.</span><span class="sxs-lookup"><span data-stu-id="f5429-234">Due to a [bug (https://issues.apache.org/jira/browse/STORM-2055)](https://issues.apache.org/jira/browse/STORM-2055) with Storm 1.0.1, you may need to install a [Storm development environment](https://storm.apache.org/releases/1.0.1/Setting-up-development-environment.html) to run Flux topologies locally.</span></span>

1. <span data-ttu-id="f5429-235">Mova o arquivo `WordCountTopology.java` para fora do projeto.</span><span class="sxs-lookup"><span data-stu-id="f5429-235">Move the `WordCountTopology.java` file out of the project.</span></span> <span data-ttu-id="f5429-236">Anteriormente, este arquivo definia a topologia, mas isso não é necessário com o Flux.</span><span class="sxs-lookup"><span data-stu-id="f5429-236">Previously, this file defined the topology, but isn't needed with Flux.</span></span>

2. <span data-ttu-id="f5429-237">No diretório `resources`, crie um novo arquivo chamado `topology.yaml`.</span><span class="sxs-lookup"><span data-stu-id="f5429-237">In the `resources` directory, create a file named `topology.yaml`.</span></span> <span data-ttu-id="f5429-238">Use o seguinte texto como o conteúdo desse arquivo.</span><span class="sxs-lookup"><span data-stu-id="f5429-238">Use the following text as the contents of this file.</span></span>

        name: "wordcount"       # friendly name for the topology
        
        config:                 # Topology configuration
        topology.workers: 1     # Hint for the number of workers to create
        
        spouts:                 # Spout definitions
        - id: "sentence-spout"
            className: "com.microsoft.example.RandomSentenceSpout"
            parallelism: 1      # parallelism hint
        
        bolts:                  # Bolt definitions
        - id: "splitter-bolt"
            className: "com.microsoft.example.SplitSentence"
            parallelism: 1
         
        - id: "counter-bolt"
            className: "com.microsoft.example.WordCount"
            constructorArgs:
                - 10
            parallelism: 1
        
        streams:                # Stream definitions
            - name: "Spout --> Splitter" # name isn't used (placeholder for logging, UI, etc.)
            from: "sentence-spout"       # The stream emitter
            to: "splitter-bolt"          # The stream consumer
            grouping:                    # Grouping type
                type: SHUFFLE
          
            - name: "Splitter -> Counter"
            from: "splitter-bolt"
            to: "counter-bolt"
            grouping:
            type: FIELDS
                args: ["word"]           # field(s) to group on

3. <span data-ttu-id="f5429-239">Faça as alterações a seguir no arquivo `pom.xml`.</span><span class="sxs-lookup"><span data-stu-id="f5429-239">Make the following changes to the `pom.xml` file.</span></span>
   
   * <span data-ttu-id="f5429-240">Adicione a nova dependência a seguir à seção `<dependencies>` :</span><span class="sxs-lookup"><span data-stu-id="f5429-240">Add the following new dependency in the `<dependencies>` section:</span></span>
     
        ```xml
        <!-- Add a dependency on the Flux framework -->
        <dependency>
            <groupId>org.apache.storm</groupId>
            <artifactId>flux-core</artifactId>
            <version>${storm.version}</version>
        </dependency>
        ```
   * <span data-ttu-id="f5429-241">Adicione o plug-in a seguir à seção `<plugins>` .</span><span class="sxs-lookup"><span data-stu-id="f5429-241">Add the following plugin to the `<plugins>` section.</span></span> <span data-ttu-id="f5429-242">Este plug-in cuida da criação de um pacote (arquivo jar) para o projeto e aplica algumas transformações específicas ao Flux durante a criação do pacote.</span><span class="sxs-lookup"><span data-stu-id="f5429-242">This plugin handles the creation of a package (jar file) for the project, and applies some transformations specific to Flux when creating the package.</span></span>
     
        ```xml
        <!-- build an uber jar -->
        <plugin>
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-shade-plugin</artifactId>
            <version>2.3</version>
            <configuration>
                <transformers>
                    <!-- Keep us from getting a "can't overwrite file error" -->
                    <transformer implementation="org.apache.maven.plugins.shade.resource.ApacheLicenseResourceTransformer" />
                    <transformer implementation="org.apache.maven.plugins.shade.resource.ServicesResourceTransformer" />
                    <!-- We're using Flux, so refer to it as main -->
                    <transformer implementation="org.apache.maven.plugins.shade.resource.ManifestResourceTransformer">
                        <mainClass>org.apache.storm.flux.Flux</mainClass>
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
        ```

   * <span data-ttu-id="f5429-243">Na seção **exec-maven-plugin** `<configuration>`, altere o valor de `<mainClass>` para `org.apache.storm.flux.Flux`.</span><span class="sxs-lookup"><span data-stu-id="f5429-243">In the **exec-maven-plugin** `<configuration>` section, change the value for `<mainClass>` to `org.apache.storm.flux.Flux`.</span></span> <span data-ttu-id="f5429-244">Essa configuração permite que o Flux cuide da execução da topologia localmente no desenvolvimento.</span><span class="sxs-lookup"><span data-stu-id="f5429-244">This setting allows Flux to handle running the topology locally in development.</span></span>

   * <span data-ttu-id="f5429-245">Na seção `<resources>`, adicione o seguinte a `<includes>`.</span><span class="sxs-lookup"><span data-stu-id="f5429-245">In the `<resources>` section, add the following to the `<includes>`.</span></span> <span data-ttu-id="f5429-246">Esse XML inclui o arquivo YAML que define a topologia como parte do projeto.</span><span class="sxs-lookup"><span data-stu-id="f5429-246">This XML includes the YAML file that defines the topology as part of the project.</span></span>

        ```xml
        <include>topology.yaml</include>
        ```

## <a name="test-the-flux-topology-locally"></a><span data-ttu-id="f5429-247">Testar a topologia do Flux localmente</span><span class="sxs-lookup"><span data-stu-id="f5429-247">Test the flux topology locally</span></span>

1. <span data-ttu-id="f5429-248">Use o seguinte para compilar e executar a topologia do Flux usando o Maven:</span><span class="sxs-lookup"><span data-stu-id="f5429-248">Use the following to compile and execute the Flux topology using Maven:</span></span>

    ```bash
    mvn compile exec:java -Dexec.args="--local -R /topology.yaml"
    ```

    <span data-ttu-id="f5429-249">Se você estiver usando o PowerShell, use o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="f5429-249">If you are using PowerShell, use the following command:</span></span>

    ```bash
    mvn compile exec:java "-Dexec.args=--local -R /topology.yaml"
    ```

    > [!WARNING]
    > <span data-ttu-id="f5429-250">Se a topologia usar bits do Storm 1.0.1, esse comando falhará.</span><span class="sxs-lookup"><span data-stu-id="f5429-250">If your topology uses Storm 1.0.1 bits, this command fails.</span></span> <span data-ttu-id="f5429-251">Essa falha é causada por [https://issues.apache.org/jira/browse/STORM-2055](https://issues.apache.org/jira/browse/STORM-2055).</span><span class="sxs-lookup"><span data-stu-id="f5429-251">This failure is caused by [https://issues.apache.org/jira/browse/STORM-2055](https://issues.apache.org/jira/browse/STORM-2055).</span></span> <span data-ttu-id="f5429-252">Em vez disso, [instale o Storm no ambiente de desenvolvimento](http://storm.apache.org/releases/0.10.0/Setting-up-development-environment.html) e use as informações a seguir.</span><span class="sxs-lookup"><span data-stu-id="f5429-252">Instead, [install Storm in your development environment](http://storm.apache.org/releases/0.10.0/Setting-up-development-environment.html) and use the following information.</span></span>

    <span data-ttu-id="f5429-253">Se você tiver [instalado o Storm no ambiente de desenvolvimento](http://storm.apache.org/releases/0.10.0/Setting-up-development-environment.html), poderá usar os seguintes comandos em vez disso:</span><span class="sxs-lookup"><span data-stu-id="f5429-253">If you have [installed Storm in your development environment](http://storm.apache.org/releases/0.10.0/Setting-up-development-environment.html), you can use the following commands instead:</span></span>

    ```bash
    mvn compile package
    storm jar target/WordCount-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --local -R /topology.yaml
    ```

    <span data-ttu-id="f5429-254">O parâmetro `--local` executa a topologia no modo local no ambiente de desenvolvimento.</span><span class="sxs-lookup"><span data-stu-id="f5429-254">The `--local` parameter runs the topology in local mode on your development environment.</span></span> <span data-ttu-id="f5429-255">O parâmetro `-R /topology.yaml` usa o recurso de arquivo `topology.yaml` do arquivo jar para definir a topologia.</span><span class="sxs-lookup"><span data-stu-id="f5429-255">The `-R /topology.yaml` parameter uses the `topology.yaml` file resource from the jar file to define the topology.</span></span>

    <span data-ttu-id="f5429-256">À medida que for executada, a topologia exibirá informações de inicialização.</span><span class="sxs-lookup"><span data-stu-id="f5429-256">As it runs, the topology displays startup information.</span></span> <span data-ttu-id="f5429-257">O texto a seguir é um exemplo de saída:</span><span class="sxs-lookup"><span data-stu-id="f5429-257">The following text is an example of the output:</span></span>

        17:33:27 [Thread-12-count] INFO  com.microsoft.example.WordCount - Emitting a count of 56 for word snow
        17:33:27 [Thread-12-count] INFO  com.microsoft.example.WordCount - Emitting a count of 56 for word white
        17:33:27 [Thread-12-count] INFO  com.microsoft.example.WordCount - Emitting a count of 112 for word seven
        17:33:27 [Thread-16-count] INFO  com.microsoft.example.WordCount - Emitting a count of 195 for word the
        17:33:27 [Thread-30-count] INFO  com.microsoft.example.WordCount - Emitting a count of 113 for word and
        17:33:27 [Thread-30-count] INFO  com.microsoft.example.WordCount - Emitting a count of 57 for word dwarfs

    <span data-ttu-id="f5429-258">Há um atraso de 10 segundos entre os lotes das informações registradas em log.</span><span class="sxs-lookup"><span data-stu-id="f5429-258">There is a 10-second delay between batches of logged information.</span></span>

2. <span data-ttu-id="f5429-259">Faça uma cópia do arquivo `topology.yaml` do projeto.</span><span class="sxs-lookup"><span data-stu-id="f5429-259">Make a copy of the `topology.yaml` file from the project.</span></span> <span data-ttu-id="f5429-260">Nomeie o novo arquivo `newtopology.yaml`.</span><span class="sxs-lookup"><span data-stu-id="f5429-260">Name the new file `newtopology.yaml`.</span></span> <span data-ttu-id="f5429-261">No arquivo `newtopology.yaml`, localize a seção a seguir e altere o valor de `10` para `5`.</span><span class="sxs-lookup"><span data-stu-id="f5429-261">In the `newtopology.yaml` file, find the following section and change the value of `10` to `5`.</span></span> <span data-ttu-id="f5429-262">Essa modificação altera o intervalo entre as emissões de lotes de contagens de palavras de 10 segundos para 5.</span><span class="sxs-lookup"><span data-stu-id="f5429-262">This modification changes the interval between emitting batches of word counts from 10 seconds to 5.</span></span>

    ```yaml
    - id: "counter-bolt"
    className: "com.microsoft.example.WordCount"
    constructorArgs:
    - 5
    parallelism: 1
    ```yaml

3. To run the topology, use the following command:

    ```bash
    mvn exec:java -Dexec.args="--local /path/to/newtopology.yaml"
    ```

    <span data-ttu-id="f5429-263">Se preferir, se você tiver o Storm no ambiente de desenvolvimento:</span><span class="sxs-lookup"><span data-stu-id="f5429-263">Or, if you have Storm on your development environment:</span></span>

    ```bash
    storm jar target/WordCount-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --local /path/to/newtopology.yaml
    ```

    <span data-ttu-id="f5429-264">Altere o `/path/to/newtopology.yaml` para o caminho para o arquivo newtopology.yaml criado por você na etapa anterior.</span><span class="sxs-lookup"><span data-stu-id="f5429-264">Change the `/path/to/newtopology.yaml` to the path to the newtopology.yaml file you created in the previous step.</span></span> <span data-ttu-id="f5429-265">Esse comando usa o newtopology.yaml como a definição da topologia.</span><span class="sxs-lookup"><span data-stu-id="f5429-265">This command uses the newtopology.yaml as the topology definition.</span></span> <span data-ttu-id="f5429-266">Como não incluímos o parâmetro `compile`, o Maven usará a versão do projeto criado nas etapas anteriores.</span><span class="sxs-lookup"><span data-stu-id="f5429-266">Since we didn't include the `compile` parameter, Maven uses the version of the project built in previous steps.</span></span>

    <span data-ttu-id="f5429-267">Depois que a topologia começar, você deverá observar uma alteração no tempo entre os lotes emitidos refletindo o valor em newtopology.yaml.</span><span class="sxs-lookup"><span data-stu-id="f5429-267">Once the topology starts, you should notice that the time between emitted batches has changed to reflect the value in newtopology.yaml.</span></span> <span data-ttu-id="f5429-268">Veja então que você pode alterar sua configuração por meio de um arquivo YAML sem ter que recompilar a topologia.</span><span class="sxs-lookup"><span data-stu-id="f5429-268">So you can see that you can change your configuration through a YAML file without having to recompile the topology.</span></span>

<span data-ttu-id="f5429-269">Para obter mais informações sobre esses e outros recursos da estrutura do Flux, consulte [Flux (https://storm.apache.org/releases/0.10.0/flux.html)](https://storm.apache.org/releases/0.10.0/flux.html).</span><span class="sxs-lookup"><span data-stu-id="f5429-269">For more information on these and other features of the Flux framework, see [Flux (https://storm.apache.org/releases/0.10.0/flux.html)](https://storm.apache.org/releases/0.10.0/flux.html).</span></span>

## <a name="trident"></a><span data-ttu-id="f5429-270">Trident</span><span class="sxs-lookup"><span data-stu-id="f5429-270">Trident</span></span>

<span data-ttu-id="f5429-271">O Trident é uma abstração de alto nível fornecida pelo Storm.</span><span class="sxs-lookup"><span data-stu-id="f5429-271">Trident is a high-level abstraction that is provided by Storm.</span></span> <span data-ttu-id="f5429-272">Ele dá suporte ao processamento com monitoramento de estado.</span><span class="sxs-lookup"><span data-stu-id="f5429-272">It supports stateful processing.</span></span> <span data-ttu-id="f5429-273">A principal vantagem do Trident é que ele pode garantir que todas as mensagens que entrarem na topologia sejam processadas somente uma vez.</span><span class="sxs-lookup"><span data-stu-id="f5429-273">The primary advantage of Trident is that it can guarantee that every message that enters the topology is processed only once.</span></span> <span data-ttu-id="f5429-274">Sem usar o Trident, sua topologia só pode garantir que as mensagens sejam processadas pelo menos uma vez.</span><span class="sxs-lookup"><span data-stu-id="f5429-274">Without using Trident, your topology can only guarantee that messages are processed at least once.</span></span> <span data-ttu-id="f5429-275">Também existem outras diferenças, como componentes internos que podem ser usados em vez da criação de bolts.</span><span class="sxs-lookup"><span data-stu-id="f5429-275">There are also other differences, such as built-in components that can be used instead of creating bolts.</span></span> <span data-ttu-id="f5429-276">Na verdade, os bolts são substituídos por componentes menos genéricos, como filtros, projeções e funções.</span><span class="sxs-lookup"><span data-stu-id="f5429-276">In fact, bolts are replaced by less-generic components, such as filters, projections, and functions.</span></span>

<span data-ttu-id="f5429-277">Os aplicativos Trident podem ser criados usando projetos Maven.</span><span class="sxs-lookup"><span data-stu-id="f5429-277">Trident applications can be created by using Maven projects.</span></span> <span data-ttu-id="f5429-278">Use as mesmas etapas básicas como apresentado anteriormente neste artigo — somente o código é diferente.</span><span class="sxs-lookup"><span data-stu-id="f5429-278">You use the same basic steps as presented earlier in this article—only the code is different.</span></span> <span data-ttu-id="f5429-279">O Trident também (atualmente) não pode ser usado com a estrutura do Flux.</span><span class="sxs-lookup"><span data-stu-id="f5429-279">Trident also cannot (currently) be used with the Flux framework.</span></span>

<span data-ttu-id="f5429-280">Para obter mais informações sobre o Trident, consulte a [Visão geral da API do Trident](http://storm.apache.org/documentation/Trident-API-Overview.html).</span><span class="sxs-lookup"><span data-stu-id="f5429-280">For more information about Trident, see the [Trident API Overview](http://storm.apache.org/documentation/Trident-API-Overview.html).</span></span>

<span data-ttu-id="f5429-281">Para obter um exemplo de um aplicativo Trident, consulte [Trending topics do Twitter com Apache Storm no HDInsight](hdinsight-storm-twitter-trending.md).</span><span class="sxs-lookup"><span data-stu-id="f5429-281">For an example of a Trident application, see [Twitter trending topics with Apache Storm on HDInsight](hdinsight-storm-twitter-trending.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="f5429-282">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="f5429-282">Next Steps</span></span>

<span data-ttu-id="f5429-283">Você aprendeu a criar uma topologia do Storm usando Java.</span><span class="sxs-lookup"><span data-stu-id="f5429-283">You have learned how to create a Storm topology by using Java.</span></span> <span data-ttu-id="f5429-284">Agora saiba como:</span><span class="sxs-lookup"><span data-stu-id="f5429-284">Now learn how to:</span></span>

* [<span data-ttu-id="f5429-285">Implantar e gerenciar topologias Apache Storm no HDInsight</span><span class="sxs-lookup"><span data-stu-id="f5429-285">Deploy and manage Apache Storm topologies on HDInsight</span></span>](hdinsight-storm-deploy-monitor-topology.md)

* [<span data-ttu-id="f5429-286">Desenvolver topologias C# para o Apache Storm no HDInsight usando o Visual Studio</span><span class="sxs-lookup"><span data-stu-id="f5429-286">Develop C# topologies for Apache Storm on HDInsight using Visual Studio</span></span>](hdinsight-storm-develop-csharp-visual-studio-topology.md)

<span data-ttu-id="f5429-287">Para obter mais topologias Storm, consulte [Topologias de exemplo para o Storm no HDInsight](hdinsight-storm-example-topology.md).</span><span class="sxs-lookup"><span data-stu-id="f5429-287">You can find more example Storm topologies by visiting [Example topologies for Storm on HDInsight](hdinsight-storm-example-topology.md).</span></span>

