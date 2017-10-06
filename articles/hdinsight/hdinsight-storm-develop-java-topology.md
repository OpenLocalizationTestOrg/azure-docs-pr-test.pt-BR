---
title: aaaApache Storm exemplo de topologia de Java - HDInsight do Azure | Microsoft Docs
description: Saiba como topologias do Apache Storm toocreate em Java, criando uma palavra de exemplo contagem de topologia.
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
ms.openlocfilehash: 54fa9dc3c93ddad83ac861f3101f50f80117d804
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-apache-storm-topology-in-java"></a><span data-ttu-id="ff678-104">Criar uma topologia Apache Storm em Java</span><span class="sxs-lookup"><span data-stu-id="ff678-104">Create an Apache Storm topology in Java</span></span>

<span data-ttu-id="ff678-105">Saiba como toocreate uma topologia em Java para o Apache Storm.</span><span class="sxs-lookup"><span data-stu-id="ff678-105">Learn how toocreate a Java-based topology for Apache Storm.</span></span> <span data-ttu-id="ff678-106">Crie uma topologia Storm que implementa um aplicativo de contagem de palavras.</span><span class="sxs-lookup"><span data-stu-id="ff678-106">You create a Storm topology that implements a word-count application.</span></span> <span data-ttu-id="ff678-107">Use o Maven toobuild e pacote de saudação do projeto.</span><span class="sxs-lookup"><span data-stu-id="ff678-107">You use Maven toobuild and package hello project.</span></span> <span data-ttu-id="ff678-108">Em seguida, você aprenderá como toodefine Olá topologia usando Olá framework de fluxo.</span><span class="sxs-lookup"><span data-stu-id="ff678-108">Then, you learn how toodefine hello topology using hello Flux framework.</span></span>

> [!NOTE]
> <span data-ttu-id="ff678-109">estrutura do fluxo de saudação está disponível no Storm 0.10.0 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="ff678-109">hello Flux framework is available in Storm 0.10.0 or later.</span></span> <span data-ttu-id="ff678-110">O Storm 0.10.0 está disponível com o HDInsight 3.3 e 3.4.</span><span class="sxs-lookup"><span data-stu-id="ff678-110">Storm 0.10.0 is available with HDInsight 3.3 and 3.4.</span></span>

<span data-ttu-id="ff678-111">Depois de concluir as etapas de saudação neste documento, você pode implantar Olá topologia tooApache Storm no HDInsight.</span><span class="sxs-lookup"><span data-stu-id="ff678-111">After completing hello steps in this document, you can deploy hello topology tooApache Storm on HDInsight.</span></span>

> [!NOTE]
> <span data-ttu-id="ff678-112">Uma versão completa do exemplos de topologia Storm Olá criado neste documento está disponível em [https://github.com/Azure-Samples/hdinsight-java-storm-wordcount](https://github.com/Azure-Samples/hdinsight-java-storm-wordcount).</span><span class="sxs-lookup"><span data-stu-id="ff678-112">A completed version of hello Storm topology examples created in this document is available at [https://github.com/Azure-Samples/hdinsight-java-storm-wordcount](https://github.com/Azure-Samples/hdinsight-java-storm-wordcount).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ff678-113">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="ff678-113">Prerequisites</span></span>

* [<span data-ttu-id="ff678-114">Java Developer Kit (JDK) versão 7</span><span class="sxs-lookup"><span data-stu-id="ff678-114">Java Developer Kit (JDK) version 7</span></span>](https://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html)

* <span data-ttu-id="ff678-115">[Maven (https://maven.apache.org/download.cgi)](https://maven.apache.org/download.cgi): Maven é um sistema de compilação do projeto para projetos Java.</span><span class="sxs-lookup"><span data-stu-id="ff678-115">[Maven (https://maven.apache.org/download.cgi)](https://maven.apache.org/download.cgi): Maven is a project build system for Java projects.</span></span>

* <span data-ttu-id="ff678-116">Um editor de texto ou IDE.</span><span class="sxs-lookup"><span data-stu-id="ff678-116">A text editor or IDE.</span></span>

## <a name="configure-environment-variables"></a><span data-ttu-id="ff678-117">Configurar variáveis de ambiente</span><span class="sxs-lookup"><span data-stu-id="ff678-117">Configure environment variables</span></span>

<span data-ttu-id="ff678-118">Olá seguintes variáveis de ambiente podem ser definidas quando você instala o Java e hello JDK.</span><span class="sxs-lookup"><span data-stu-id="ff678-118">hello following environment variables may be set when you install Java and hello JDK.</span></span> <span data-ttu-id="ff678-119">No entanto, você deve verificar se eles existem e que eles contêm valores de saudação corretos para seu sistema.</span><span class="sxs-lookup"><span data-stu-id="ff678-119">However, you should check that they exist and that they contain hello correct values for your system.</span></span>

* <span data-ttu-id="ff678-120">**JAVA_HOME** -deve apontar toohello diretório onde Olá o Java runtime environment (JRE) está instalado.</span><span class="sxs-lookup"><span data-stu-id="ff678-120">**JAVA_HOME** - should point toohello directory where hello Java runtime environment (JRE) is installed.</span></span> <span data-ttu-id="ff678-121">Por exemplo, em uma distribuição Unix ou Linux, ele deve ter um valor semelhante muito`/usr/lib/jvm/java-7-oracle`.</span><span class="sxs-lookup"><span data-stu-id="ff678-121">For example, in a Unix or Linux distribution, it should have a value similar too`/usr/lib/jvm/java-7-oracle`.</span></span> <span data-ttu-id="ff678-122">No Windows, ele deve ter um valor semelhante muito`c:\Program Files (x86)\Java\jre1.7`</span><span class="sxs-lookup"><span data-stu-id="ff678-122">In Windows, it would have a value similar too`c:\Program Files (x86)\Java\jre1.7`</span></span>

* <span data-ttu-id="ff678-123">**CAMINHO** -deve conter Olá caminhos a seguir:</span><span class="sxs-lookup"><span data-stu-id="ff678-123">**PATH** - should contain hello following paths:</span></span>

  * <span data-ttu-id="ff678-124">**JAVA_HOME** (ou caminho equivalente Olá)</span><span class="sxs-lookup"><span data-stu-id="ff678-124">**JAVA_HOME** (or hello equivalent path)</span></span>

  * <span data-ttu-id="ff678-125">**JAVA_HOME\bin** (ou caminho equivalente Olá)</span><span class="sxs-lookup"><span data-stu-id="ff678-125">**JAVA_HOME\bin** (or hello equivalent path)</span></span>

  * <span data-ttu-id="ff678-126">diretório de saudação onde Maven está instalado</span><span class="sxs-lookup"><span data-stu-id="ff678-126">hello directory where Maven is installed</span></span>

## <a name="create-a-maven-project"></a><span data-ttu-id="ff678-127">Criar um projeto Maven</span><span class="sxs-lookup"><span data-stu-id="ff678-127">Create a Maven project</span></span>

<span data-ttu-id="ff678-128">Na linha de comando hello, use Olá comando a seguir toocreate um projeto Maven chamado **WordCount**:</span><span class="sxs-lookup"><span data-stu-id="ff678-128">From hello command line, use hello following command toocreate a Maven project named **WordCount**:</span></span>

```bash
mvn archetype:generate -DarchetypeArtifactId=maven-archetype-quickstart -DgroupId=com.microsoft.example -DartifactId=WordCount -DinteractiveMode=false
```

> [!NOTE]
> <span data-ttu-id="ff678-129">Se você estiver usando o PowerShell, coloque os parâmetros `-D` com aspas duplas.</span><span class="sxs-lookup"><span data-stu-id="ff678-129">If you are using PowerShell, you must surround the`-D` parameters with double quotes.</span></span>
>
> `mvn archetype:generate "-DarchetypeArtifactId=maven-archetype-quickstart" "-DgroupId=com.microsoft.example" "-DartifactId=WordCount" "-DinteractiveMode=false"`

<span data-ttu-id="ff678-130">Este comando cria um diretório chamado `WordCount` no local atual do hello, que contém um projeto Maven básico.</span><span class="sxs-lookup"><span data-stu-id="ff678-130">This command creates a directory named `WordCount` at hello current location, which contains a basic Maven project.</span></span> <span data-ttu-id="ff678-131">Olá `WordCount` diretório contém Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="ff678-131">hello `WordCount` directory contains hello following items:</span></span>

* <span data-ttu-id="ff678-132">`pom.xml`: Contém configurações para o projeto Maven hello.</span><span class="sxs-lookup"><span data-stu-id="ff678-132">`pom.xml`: Contains settings for hello Maven project.</span></span>
* <span data-ttu-id="ff678-133">`src\main\java\com\microsoft\example`: contém o código do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="ff678-133">`src\main\java\com\microsoft\example`: Contains your application code.</span></span>
* <span data-ttu-id="ff678-134">`src\test\java\com\microsoft\example`: contém testes para o seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="ff678-134">`src\test\java\com\microsoft\example`: Contains tests for your application.</span></span> 

### <a name="remove-hello-generated-example-code"></a><span data-ttu-id="ff678-135">Remover o código de exemplo hello gerado</span><span class="sxs-lookup"><span data-stu-id="ff678-135">Remove hello generated example code</span></span>

<span data-ttu-id="ff678-136">Exclua arquivos de aplicativo de hello e teste Olá gerado:</span><span class="sxs-lookup"><span data-stu-id="ff678-136">Delete hello generated test and hello application files:</span></span>

* <span data-ttu-id="ff678-137">**src\test\java\com\microsoft\example\AppTest.java**</span><span class="sxs-lookup"><span data-stu-id="ff678-137">**src\test\java\com\microsoft\example\AppTest.java**</span></span>
* <span data-ttu-id="ff678-138">**src\main\java\com\microsoft\example\App.java**</span><span class="sxs-lookup"><span data-stu-id="ff678-138">**src\main\java\com\microsoft\example\App.java**</span></span>

## <a name="add-maven-repositories"></a><span data-ttu-id="ff678-139">Adicionar repositórios Maven</span><span class="sxs-lookup"><span data-stu-id="ff678-139">Add Maven repositories</span></span>

<span data-ttu-id="ff678-140">HDInsight é baseado nos Olá HDP Hortonworks Data Platform (), portanto, é recomendável usar as dependências do hello Hortonworks repositório toodownload para seus projetos do Apache Storm.</span><span class="sxs-lookup"><span data-stu-id="ff678-140">HDInsight is based on hello Hortonworks Data Platform (HDP), so we recommend using hello Hortonworks repository toodownload dependencies for your Apache Storm projects.</span></span> <span data-ttu-id="ff678-141">Em Olá __pom.xml__ de arquivo, adicione Olá XML a seguir após Olá `<url>http://maven.apache.org</url>` linha:</span><span class="sxs-lookup"><span data-stu-id="ff678-141">In hello __pom.xml__ file, add hello following XML after hello `<url>http://maven.apache.org</url>` line:</span></span>

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

## <a name="add-properties"></a><span data-ttu-id="ff678-142">Adicionar propriedades</span><span class="sxs-lookup"><span data-stu-id="ff678-142">Add properties</span></span>

<span data-ttu-id="ff678-143">Maven permite valores de nível de projeto toodefine chamados de propriedades.</span><span class="sxs-lookup"><span data-stu-id="ff678-143">Maven allows you toodefine project-level values called properties.</span></span> <span data-ttu-id="ff678-144">Em Olá __pom.xml__, adicionar Olá após o texto após Olá `</repositories>` linha:</span><span class="sxs-lookup"><span data-stu-id="ff678-144">In hello __pom.xml__, add hello following text after hello `</repositories>` line:</span></span>

```xml
<properties>
    <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
    <!--
    This is a version of Storm from hello Hortonworks repository that is compatible with HDInsight.
    -->
    <storm.version>1.0.1.2.5.3.0-37</storm.version>
</properties>
```

<span data-ttu-id="ff678-145">Agora você pode usar esse valor em outras seções Olá `pom.xml`.</span><span class="sxs-lookup"><span data-stu-id="ff678-145">You can now use this value in other sections of hello `pom.xml`.</span></span> <span data-ttu-id="ff678-146">Por exemplo, ao especificar versão Olá componentes Storm, você pode usar `${storm.version}` em vez de um valor de codificação.</span><span class="sxs-lookup"><span data-stu-id="ff678-146">For example, when specifying hello version of Storm components, you can use `${storm.version}` instead of hard coding a value.</span></span>

## <a name="add-dependencies"></a><span data-ttu-id="ff678-147">Adicionar dependências</span><span class="sxs-lookup"><span data-stu-id="ff678-147">Add dependencies</span></span>

<span data-ttu-id="ff678-148">Adicione uma dependência para componentes do Storm.</span><span class="sxs-lookup"><span data-stu-id="ff678-148">Add a dependency for Storm components.</span></span> <span data-ttu-id="ff678-149">Olá abrir `pom.xml` de arquivos e adicionar Olá Olá código a seguir `<dependencies>` seção:</span><span class="sxs-lookup"><span data-stu-id="ff678-149">Open hello `pom.xml` file and add hello following code in hello `<dependencies>` section:</span></span>

```xml
<dependency>
    <groupId>org.apache.storm</groupId>
    <artifactId>storm-core</artifactId>
    <version>${storm.version}</version>
    <!-- keep storm out of hello jar-with-dependencies -->
    <scope>provided</scope>
</dependency>
```

<span data-ttu-id="ff678-150">Em tempo de compilação, Maven usa esse toolook informações `storm-core` no repositório de Maven hello.</span><span class="sxs-lookup"><span data-stu-id="ff678-150">At compile time, Maven uses this information toolook up `storm-core` in hello Maven repository.</span></span> <span data-ttu-id="ff678-151">Parece primeiro repositório Olá no computador local.</span><span class="sxs-lookup"><span data-stu-id="ff678-151">It first looks in hello repository on your local computer.</span></span> <span data-ttu-id="ff678-152">Se os arquivos de saudação não existe, Maven baixa os arquivos de Repositório Maven público de saudação e os armazena no repositório local hello.</span><span class="sxs-lookup"><span data-stu-id="ff678-152">If hello files aren't there, Maven downloads them from hello public Maven repository and stores them in hello local repository.</span></span>

> [!NOTE]
> <span data-ttu-id="ff678-153">Saudação de aviso `<scope>provided</scope>` linha nesta seção.</span><span class="sxs-lookup"><span data-stu-id="ff678-153">Notice hello `<scope>provided</scope>` line in this section.</span></span> <span data-ttu-id="ff678-154">Essa configuração informa Maven tooexclude **storm core** de todos os arquivos JAR que são criados, porque ele é fornecido pelo sistema hello.</span><span class="sxs-lookup"><span data-stu-id="ff678-154">This setting tells Maven tooexclude **storm-core** from any JAR files that are created, because it is provided by hello system.</span></span>

## <a name="build-configuration"></a><span data-ttu-id="ff678-155">Configuração de compilação</span><span class="sxs-lookup"><span data-stu-id="ff678-155">Build configuration</span></span>

<span data-ttu-id="ff678-156">Maven plug-ins permitem fases de compilação Olá toocustomize do projeto de saudação.</span><span class="sxs-lookup"><span data-stu-id="ff678-156">Maven plug-ins allow you toocustomize hello build stages of hello project.</span></span> <span data-ttu-id="ff678-157">Por exemplo, como o projeto de saudação é compilado ou como toopackage-lo em um arquivo JAR.</span><span class="sxs-lookup"><span data-stu-id="ff678-157">For example, how hello project is compiled or how toopackage it into a JAR file.</span></span> <span data-ttu-id="ff678-158">Olá abrir `pom.xml` de arquivos e adicionar Olá seguindo o código diretamente acima Olá `</project>` linha.</span><span class="sxs-lookup"><span data-stu-id="ff678-158">Open hello `pom.xml` file and add hello following code directly above hello `</project>` line.</span></span>

```xml
<build>
    <plugins>
    </plugins>
    <resources>
    </resources>
</build>
```

<span data-ttu-id="ff678-159">Esta seção é usado tooadd plug-ins, recursos e outras opções de configuração de compilação.</span><span class="sxs-lookup"><span data-stu-id="ff678-159">This section is used tooadd plug-ins, resources, and other build configuration options.</span></span> <span data-ttu-id="ff678-160">Para obter uma referência completa de saudação **pom.xml** de arquivos, consulte [http://maven.apache.org/pom.html](http://maven.apache.org/pom.html).</span><span class="sxs-lookup"><span data-stu-id="ff678-160">For a full reference of hello **pom.xml** file, see [http://maven.apache.org/pom.html](http://maven.apache.org/pom.html).</span></span>

### <a name="add-plug-ins"></a><span data-ttu-id="ff678-161">Adicionar plug-ins</span><span class="sxs-lookup"><span data-stu-id="ff678-161">Add plug-ins</span></span>

<span data-ttu-id="ff678-162">Para obter topologias Apache Storm implementadas em Java, Olá [plug-in do Exec Maven](http://www.mojohaus.org/exec-maven-plugin/) é útil porque permite tooeasily executar topologia Olá localmente no seu ambiente de desenvolvimento.</span><span class="sxs-lookup"><span data-stu-id="ff678-162">For Apache Storm topologies implemented in Java, hello [Exec Maven Plugin](http://www.mojohaus.org/exec-maven-plugin/) is useful because it allows you tooeasily run hello topology locally in your development environment.</span></span> <span data-ttu-id="ff678-163">Adicionar Olá após toohello `<plugins>` seção Olá `pom.xml` tooinclude Olá Exec Maven plugin do arquivo:</span><span class="sxs-lookup"><span data-stu-id="ff678-163">Add hello following toohello `<plugins>` section of hello `pom.xml` file tooinclude hello Exec Maven plugin:</span></span>

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

<span data-ttu-id="ff678-164">Útil outro plug-in é hello [plug-in do Apache Maven compilador](http://maven.apache.org/plugins/maven-compiler-plugin/), que é usado toochange opções de compilação.</span><span class="sxs-lookup"><span data-stu-id="ff678-164">Another useful plug-in is hello [Apache Maven Compiler Plugin](http://maven.apache.org/plugins/maven-compiler-plugin/), which is used toochange compilation options.</span></span> <span data-ttu-id="ff678-165">alterações de Olá Olá versão do Java que usa Maven para origem de saudação e de destino para o seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="ff678-165">hello changes hello Java version that Maven uses for hello source and target for your application.</span></span>

* <span data-ttu-id="ff678-166">Para HDInsight __3.4 ou anteriores__, definir a origem da saudação e too__1.7__ de versão do Java de destino.</span><span class="sxs-lookup"><span data-stu-id="ff678-166">For HDInsight __3.4 or earlier__, set hello source and target Java version too__1.7__.</span></span>

* <span data-ttu-id="ff678-167">Para HDInsight __3.5__, definir a origem da saudação e too__1.8__ de versão do Java de destino.</span><span class="sxs-lookup"><span data-stu-id="ff678-167">For HDInsight __3.5__, set hello source and target Java version too__1.8__.</span></span>

<span data-ttu-id="ff678-168">Adicionar Olá depois do texto de saudação `<plugins>` seção Olá `pom.xml` tooinclude Olá Apache Maven compilador plugin do arquivo.</span><span class="sxs-lookup"><span data-stu-id="ff678-168">Add hello following text in hello `<plugins>` section of hello `pom.xml` file tooinclude hello Apache Maven Compiler plugin.</span></span> <span data-ttu-id="ff678-169">Este exemplo especifica 1.8, para a versão do HDInsight de destino Olá é 3.5.</span><span class="sxs-lookup"><span data-stu-id="ff678-169">This example specifies 1.8, so hello target HDInsight version is 3.5.</span></span>

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

### <a name="configure-resources"></a><span data-ttu-id="ff678-170">Configurar recursos</span><span class="sxs-lookup"><span data-stu-id="ff678-170">Configure resources</span></span>

<span data-ttu-id="ff678-171">Olá seção de recursos permite que você tooinclude recursos de código não como arquivos de configuração necessários pelos componentes na topologia de saudação.</span><span class="sxs-lookup"><span data-stu-id="ff678-171">hello resources section allows you tooinclude non-code resources such as configuration files needed by components in hello topology.</span></span> <span data-ttu-id="ff678-172">Neste exemplo, adicionar Olá depois do texto de saudação `<resources>` seção Olá ' pom.xml arquivo.</span><span class="sxs-lookup"><span data-stu-id="ff678-172">For this example, add hello following text in hello `<resources>` section of hello \`pom.xml file.</span></span>

```xml
<resource>
    <directory>${basedir}/resources</directory>
    <filtering>false</filtering>
    <includes>
        <include>log4j2.xml</include>
    </includes>
</resource>
```

<span data-ttu-id="ff678-173">Este exemplo adiciona o diretório de recursos de saudação na raiz de saudação do projeto da saudação (`${basedir}`) como um local que contém recursos e inclui o arquivo hello chamado `log4j2.xml`.</span><span class="sxs-lookup"><span data-stu-id="ff678-173">This example adds hello resources directory in hello root of hello project (`${basedir}`) as a location that contains resources, and includes hello file named `log4j2.xml`.</span></span> <span data-ttu-id="ff678-174">Esse arquivo é usado tooconfigure quais informações são registradas pelo topologia hello.</span><span class="sxs-lookup"><span data-stu-id="ff678-174">This file is used tooconfigure what information is logged by hello topology.</span></span>

## <a name="create-hello-topology"></a><span data-ttu-id="ff678-175">Criar topologia Olá</span><span class="sxs-lookup"><span data-stu-id="ff678-175">Create hello topology</span></span>

<span data-ttu-id="ff678-176">Uma topologia Apache Storm baseada em Java consiste em três componentes que você deve criar (ou referenciar) como uma dependência.</span><span class="sxs-lookup"><span data-stu-id="ff678-176">A Java-based Apache Storm topology consists of three components that you must author (or reference) as a dependency.</span></span>

* <span data-ttu-id="ff678-177">**Spouts**: Leituras de fontes de dados externos e emite os fluxos de dados na topologia de saudação.</span><span class="sxs-lookup"><span data-stu-id="ff678-177">**Spouts**: Reads data from external sources and emits streams of data into hello topology.</span></span>

* <span data-ttu-id="ff678-178">**Bolts**: executa processamento em fluxos emitidos por spouts ou outros bolts e emite um ou mais fluxos.</span><span class="sxs-lookup"><span data-stu-id="ff678-178">**Bolts**: Performs processing on streams emitted by spouts or other bolts, and emits one or more streams.</span></span>

* <span data-ttu-id="ff678-179">**Topologia**: define como Olá spouts e parafusos são organizados e fornece o ponto de entrada hello para a topologia de saudação.</span><span class="sxs-lookup"><span data-stu-id="ff678-179">**Topology**: Defines how hello spouts and bolts are arranged, and provides hello entry point for hello topology.</span></span>

### <a name="create-hello-spout"></a><span data-ttu-id="ff678-180">Criar spout Olá</span><span class="sxs-lookup"><span data-stu-id="ff678-180">Create hello spout</span></span>

<span data-ttu-id="ff678-181">requisitos de tooreduce para configurar fontes de dados externas, Olá após spout simplesmente emite sentenças aleatórias.</span><span class="sxs-lookup"><span data-stu-id="ff678-181">tooreduce requirements for setting up external data sources, hello following spout simply emits random sentences.</span></span> <span data-ttu-id="ff678-182">É uma versão modificada de um spout que é fornecido com hello [exemplos Storm Starter](https://github.com/apache/storm/blob/0.10.x-branch/examples/storm-starter/src/jvm/storm/starter).</span><span class="sxs-lookup"><span data-stu-id="ff678-182">It is a modified version of a spout that is provided with hello [Storm-Starter examples](https://github.com/apache/storm/blob/0.10.x-branch/examples/storm-starter/src/jvm/storm/starter).</span></span>

> [!NOTE]
> <span data-ttu-id="ff678-183">Para obter um exemplo de um spout que lê a partir de uma fonte de dados externa, consulte um dos Olá exemplos a seguir:</span><span class="sxs-lookup"><span data-stu-id="ff678-183">For an example of a spout that reads from an external data source, see one of hello following examples:</span></span>
>
> * <span data-ttu-id="ff678-184">[TwitterSampleSPout](https://github.com/apache/storm/blob/0.10.x-branch/examples/storm-starter/src/jvm/storm/starter/spout/TwitterSampleSpout.java): um spout de exemplo que lê do Twitter</span><span class="sxs-lookup"><span data-stu-id="ff678-184">[TwitterSampleSPout](https://github.com/apache/storm/blob/0.10.x-branch/examples/storm-starter/src/jvm/storm/starter/spout/TwitterSampleSpout.java): An example spout that reads from Twitter</span></span>
> * <span data-ttu-id="ff678-185">[Storm-Kafka](https://github.com/apache/storm/tree/0.10.x-branch/external/storm-kafka): um spout que lê do Kafka</span><span class="sxs-lookup"><span data-stu-id="ff678-185">[Storm-Kafka](https://github.com/apache/storm/tree/0.10.x-branch/external/storm-kafka): A spout that reads from Kafka</span></span>

<span data-ttu-id="ff678-186">Para spout hello, crie um arquivo chamado `RandomSentenceSpout.java` em Olá `src\main\java\com\microsoft\example` Olá diretório e usar código Java a seguir como conteúdo hello:</span><span class="sxs-lookup"><span data-stu-id="ff678-186">For hello spout, create a file named `RandomSentenceSpout.java` in hello `src\main\java\com\microsoft\example` directory and use hello following Java code as hello contents:</span></span>

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
  //Collector used tooemit output
  SpoutOutputCollector _collector;
  //Used toogenerate a random number
  Random _rand;

  //Open is called when an instance of hello class is created
  @Override
  public void open(Map conf, TopologyContext context, SpoutOutputCollector collector) {
  //Set hello instance collector toohello one passed in
    _collector = collector;
    //For randomness
    _rand = new Random();
  }

  //Emit data toohello stream
  @Override
  public void nextTuple() {
  //Sleep for a bit
    Utils.sleep(100);
    //hello sentences that are randomly emitted
    String[] sentences = new String[]{ "hello cow jumped over hello moon", "an apple a day keeps hello doctor away",
        "four score and seven years ago", "snow white and hello seven dwarfs", "i am at two with nature" };
    //Randomly pick a sentence
    String sentence = sentences[_rand.nextInt(sentences.length)];
    //Emit hello sentence
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

  //Declare hello output fields. In this case, an sentence
  @Override
  public void declareOutputFields(OutputFieldsDeclarer declarer) {
    declarer.declare(new Fields("sentence"));
  }
}
```

> [!NOTE]
> <span data-ttu-id="ff678-187">Embora essa topologia usa apenas um spout, outros podem ter vários que feed de dados de origens diferentes em topologia hello.</span><span class="sxs-lookup"><span data-stu-id="ff678-187">Although this topology uses only one spout, others may have several that feed data from different sources into hello topology.</span></span>

### <a name="create-hello-bolts"></a><span data-ttu-id="ff678-188">Criar hello parafusos</span><span class="sxs-lookup"><span data-stu-id="ff678-188">Create hello bolts</span></span>

<span data-ttu-id="ff678-189">Parafusos tratar Olá processamento de dados.</span><span class="sxs-lookup"><span data-stu-id="ff678-189">Bolts handle hello data processing.</span></span> <span data-ttu-id="ff678-190">Essa topologia usa dois bolts:</span><span class="sxs-lookup"><span data-stu-id="ff678-190">This topology uses two bolts:</span></span>

* <span data-ttu-id="ff678-191">**SplitSentence**: divide sentenças Olá emitidas pelo **RandomSentenceSpout** em palavras individuais.</span><span class="sxs-lookup"><span data-stu-id="ff678-191">**SplitSentence**: Splits hello sentences emitted by **RandomSentenceSpout** into individual words.</span></span>

* <span data-ttu-id="ff678-192">**WordCount**: conta quantas vezes cada palavra ocorreu.</span><span class="sxs-lookup"><span data-stu-id="ff678-192">**WordCount**: Counts how many times each word has occurred.</span></span>

> [!NOTE]
> <span data-ttu-id="ff678-193">Parafusos podem fazer qualquer coisa, por exemplo, computação, persistência ou falando tooexternal componentes.</span><span class="sxs-lookup"><span data-stu-id="ff678-193">Bolts can do anything, for example, computation, persistence, or talking tooexternal components.</span></span>

<span data-ttu-id="ff678-194">Crie dois novos arquivos, `SplitSentence.java` e `WordCount.java` em Olá `src\main\java\com\microsoft\example` directory.</span><span class="sxs-lookup"><span data-stu-id="ff678-194">Create two new files, `SplitSentence.java` and `WordCount.java` in hello `src\main\java\com\microsoft\example` directory.</span></span> <span data-ttu-id="ff678-195">Use Olá depois do texto como conteúdo Olá para arquivos de saudação:</span><span class="sxs-lookup"><span data-stu-id="ff678-195">Use hello following text as hello contents for hello files:</span></span>

#### <a name="splitsentence"></a><span data-ttu-id="ff678-196">SplitSentence</span><span class="sxs-lookup"><span data-stu-id="ff678-196">SplitSentence</span></span>

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

  //Execute is called tooprocess tuples
  @Override
  public void execute(Tuple tuple, BasicOutputCollector collector) {
    //Get hello sentence content from hello tuple
    String sentence = tuple.getString(0);
    //An iterator tooget each word
    BreakIterator boundary=BreakIterator.getWordInstance();
    //Give hello iterator hello sentence
    boundary.setText(sentence);
    //Find hello beginning first word
    int start=boundary.first();
    //Iterate over each word and emit it toohello output stream
    for (int end=boundary.next(); end != BreakIterator.DONE; start=end, end=boundary.next()) {
      //get hello word
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

#### <a name="wordcount"></a><span data-ttu-id="ff678-197">WordCount</span><span class="sxs-lookup"><span data-stu-id="ff678-197">WordCount</span></span>

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
  //How often tooemit a count of words
  private Integer emitFrequency;

  // Default constructor
  public WordCount() {
      emitFrequency=5; // Default too60 seconds
  }

  // Constructor that sets emit frequency
  public WordCount(Integer frequency) {
      emitFrequency=frequency;
  }

  //Configure frequency of tick tuples for this bolt
  //This delivers a 'tick' tuple on a specific interval,
  //which is used tootrigger certain actions
  @Override
  public Map<String, Object> getComponentConfiguration() {
      Config conf = new Config();
      conf.put(Config.TOPOLOGY_TICK_TUPLE_FREQ_SECS, emitFrequency);
      return conf;
  }

  //execute is called tooprocess tuples
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
      //Get hello word contents from hello tuple
      String word = tuple.getString(0);
      //Have we counted any already?
      Integer count = counts.get(word);
      if (count == null)
        count = 0;
      //Increment hello count and store it
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

### <a name="define-hello-topology"></a><span data-ttu-id="ff678-198">Definir a topologia de saudação</span><span class="sxs-lookup"><span data-stu-id="ff678-198">Define hello topology</span></span>

<span data-ttu-id="ff678-199">topologia de saudação vincula Olá spouts e bolts juntos em um gráfico, que define como os dados fluem entre os componentes de saudação.</span><span class="sxs-lookup"><span data-stu-id="ff678-199">hello topology ties hello spouts and bolts together into a graph, which defines how data flows between hello components.</span></span> <span data-ttu-id="ff678-200">Ele também fornece dicas de paralelismo Storm usa ao criar instâncias de componentes de saudação no cluster hello.</span><span class="sxs-lookup"><span data-stu-id="ff678-200">It also provides parallelism hints that Storm uses when creating instances of hello components within hello cluster.</span></span>

<span data-ttu-id="ff678-201">Olá imagem a seguir é um diagrama básico do gráfico de saudação de componentes para esta topologia.</span><span class="sxs-lookup"><span data-stu-id="ff678-201">hello following image is a basic diagram of hello graph of components for this topology.</span></span>

![saudação de exibição de diagrama spouts e bolts organização](./media/hdinsight-storm-develop-java-topology/wordcount-topology.png)

<span data-ttu-id="ff678-203">tooimplement Olá topologia, crie um arquivo chamado `WordCountTopology.java` em Olá `src\main\java\com\microsoft\example` directory.</span><span class="sxs-lookup"><span data-stu-id="ff678-203">tooimplement hello topology, create a file named `WordCountTopology.java` in hello `src\main\java\com\microsoft\example` directory.</span></span> <span data-ttu-id="ff678-204">Saudação de usar código Java a seguir como conteúdo de saudação do arquivo hello:</span><span class="sxs-lookup"><span data-stu-id="ff678-204">Use hello following Java code as hello contents of hello file:</span></span>

```java
package com.microsoft.example;

import org.apache.storm.Config;
import org.apache.storm.LocalCluster;
import org.apache.storm.StormSubmitter;
import org.apache.storm.topology.TopologyBuilder;
import org.apache.storm.tuple.Fields;

import com.microsoft.example.RandomSentenceSpout;

public class WordCountTopology {

  //Entry point for hello topology
  public static void main(String[] args) throws Exception {
  //Used toobuild hello topology
    TopologyBuilder builder = new TopologyBuilder();
    //Add hello spout, with a name of 'spout'
    //and parallelism hint of 5 executors
    builder.setSpout("spout", new RandomSentenceSpout(), 5);
    //Add hello SplitSentence bolt, with a name of 'split'
    //and parallelism hint of 8 executors
    //shufflegrouping subscribes toohello spout, and equally distributes
    //tuples (sentences) across instances of hello SplitSentence bolt
    builder.setBolt("split", new SplitSentence(), 8).shuffleGrouping("spout");
    //Add hello counter, with a name of 'count'
    //and parallelism hint of 12 executors
    //fieldsgrouping subscribes toohello split bolt, and
    //ensures that hello same word is sent toohello same instance (group by field 'word')
    builder.setBolt("count", new WordCount(), 12).fieldsGrouping("split", new Fields("word"));

    //new configuration
    Config conf = new Config();
    //Set toofalse toodisable debug information when
    // running in production on a cluster
    conf.setDebug(false);

    //If there are arguments, we are running on a cluster
    if (args != null && args.length > 0) {
      //parallelism hint tooset hello number of workers
      conf.setNumWorkers(3);
      //submit hello topology
      StormSubmitter.submitTopology(args[0], conf, builder.createTopology());
    }
    //Otherwise, we are running locally
    else {
      //Cap hello maximum number of executors that can be spawned
      //for a component too3
      conf.setMaxTaskParallelism(3);
      //LocalCluster is used toorun locally
      LocalCluster cluster = new LocalCluster();
      //submit hello topology
      cluster.submitTopology("word-count", conf, builder.createTopology());
      //sleep
      Thread.sleep(10000);
      //shut down hello cluster
      cluster.shutdown();
    }
  }
}
```

### <a name="configure-logging"></a><span data-ttu-id="ff678-205">Configurar o registro em log</span><span class="sxs-lookup"><span data-stu-id="ff678-205">Configure logging</span></span>

<span data-ttu-id="ff678-206">Tempestade usa Apache Log4j toolog informações.</span><span class="sxs-lookup"><span data-stu-id="ff678-206">Storm uses Apache Log4j toolog information.</span></span> <span data-ttu-id="ff678-207">Se você não configurar o registro em log, a topologia de saudação emite informações de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="ff678-207">If you do not configure logging, hello topology emits diagnostic information.</span></span> <span data-ttu-id="ff678-208">toocontrol que é registrado em log, crie um arquivo chamado `log4j2.xml` em Olá `resources` directory.</span><span class="sxs-lookup"><span data-stu-id="ff678-208">toocontrol what is logged, create a file named `log4j2.xml` in hello `resources` directory.</span></span> <span data-ttu-id="ff678-209">Use Olá XML a seguir como conteúdo de saudação do arquivo hello.</span><span class="sxs-lookup"><span data-stu-id="ff678-209">Use hello following XML as hello contents of hello file.</span></span>

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

<span data-ttu-id="ff678-210">Esse XML configura um novo agente para Olá `com.microsoft.example` classe, que inclui componentes de saudação nessa topologia de exemplo.</span><span class="sxs-lookup"><span data-stu-id="ff678-210">This XML configures a new logger for hello `com.microsoft.example` class, which includes hello components in this example topology.</span></span> <span data-ttu-id="ff678-211">nível de saudação é definido tootrace para esse agente, que captura qualquer informação de registro em log emitida pelos componentes nesta topologia.</span><span class="sxs-lookup"><span data-stu-id="ff678-211">hello level is set tootrace for this logger, which captures any logging information emitted by components in this topology.</span></span>

<span data-ttu-id="ff678-212">Olá `<Root level="error">` seção configura o nível de raiz de saudação do log (tudo o que não está em `com.microsoft.example`) tooonly informações de erro de log.</span><span class="sxs-lookup"><span data-stu-id="ff678-212">hello `<Root level="error">` section configures hello root level of logging (everything not in `com.microsoft.example`) tooonly log error information.</span></span>

<span data-ttu-id="ff678-213">Para saber mais sobre como configurar o registro em log para Log4j, confira [http://logging.apache.org/log4j/2.x/manual/configuration.html](http://logging.apache.org/log4j/2.x/manual/configuration.html).</span><span class="sxs-lookup"><span data-stu-id="ff678-213">For more information on configuring logging for Log4j, see [http://logging.apache.org/log4j/2.x/manual/configuration.html](http://logging.apache.org/log4j/2.x/manual/configuration.html).</span></span>

> [!NOTE]
> <span data-ttu-id="ff678-214">Storm versão 0.10.0 e superior usa Log4j 2.x.</span><span class="sxs-lookup"><span data-stu-id="ff678-214">Storm version 0.10.0 and higher use Log4j 2.x.</span></span> <span data-ttu-id="ff678-215">Versões mais antigas do storm usavam Log4j 1.x, que usava um formato diferente para a configuração de log.</span><span class="sxs-lookup"><span data-stu-id="ff678-215">Older versions of storm used Log4j 1.x, which used a different format for log configuration.</span></span> <span data-ttu-id="ff678-216">Para obter informações sobre a configuração anterior hello, consulte [http://wiki.apache.org/logging-log4j/Log4jXmlFormat](http://wiki.apache.org/logging-log4j/Log4jXmlFormat).</span><span class="sxs-lookup"><span data-stu-id="ff678-216">For information on hello older configuration, see [http://wiki.apache.org/logging-log4j/Log4jXmlFormat](http://wiki.apache.org/logging-log4j/Log4jXmlFormat).</span></span>

## <a name="test-hello-topology-locally"></a><span data-ttu-id="ff678-217">Topologia de saudação do teste localmente</span><span class="sxs-lookup"><span data-stu-id="ff678-217">Test hello topology locally</span></span>

<span data-ttu-id="ff678-218">Depois de salvar arquivos hello, use Olá comando tootest Olá topologia do local a seguir.</span><span class="sxs-lookup"><span data-stu-id="ff678-218">After you save hello files, use hello following command tootest hello topology locally.</span></span>

```bash
mvn compile exec:java -Dstorm.topology=com.microsoft.example.WordCountTopology
```

<span data-ttu-id="ff678-219">Como ele é executado, topologia Olá exibe informações de inicialização.</span><span class="sxs-lookup"><span data-stu-id="ff678-219">As it runs, hello topology displays startup information.</span></span> <span data-ttu-id="ff678-220">Olá, texto a seguir é um exemplo de saída de contagem de palavras hello:</span><span class="sxs-lookup"><span data-stu-id="ff678-220">hello following text is an example of hello word count output:</span></span>

    17:33:27 [Thread-12-count] INFO  com.microsoft.example.WordCount - Emitting a count of 56 for word snow
    17:33:27 [Thread-12-count] INFO  com.microsoft.example.WordCount - Emitting a count of 56 for word white
    17:33:27 [Thread-12-count] INFO  com.microsoft.example.WordCount - Emitting a count of 112 for word seven
    17:33:27 [Thread-16-count] INFO  com.microsoft.example.WordCount - Emitting a count of 195 for word the
    17:33:27 [Thread-30-count] INFO  com.microsoft.example.WordCount - Emitting a count of 113 for word and
    17:33:27 [Thread-30-count] INFO  com.microsoft.example.WordCount - Emitting a count of 57 for word dwarfs
    17:33:27 [Thread-12-count] INFO  com.microsoft.example.WordCount - Emitting a count of 57 for word snow

<span data-ttu-id="ff678-221">Esse log de exemplo indica que o word Olá ' e ' 113 vezes foi emitido.</span><span class="sxs-lookup"><span data-stu-id="ff678-221">This example log indicates that hello word 'and' has been emitted 113 times.</span></span> <span data-ttu-id="ff678-222">Olá contagem continuar toogo backup como topologia Olá executa porque spout Olá continuamente emite Olá mesmo sentenças.</span><span class="sxs-lookup"><span data-stu-id="ff678-222">hello count continues toogo up as long as hello topology runs because hello spout continuously emits hello same sentences.</span></span>

<span data-ttu-id="ff678-223">Há um intervalo de cinco segundos entre a emissão de palavras e as contagens.</span><span class="sxs-lookup"><span data-stu-id="ff678-223">There is a 5-second interval between emission of words and counts.</span></span> <span data-ttu-id="ff678-224">Olá **WordCount** componente está configurado tooonly emitir informações quando chega uma tupla de escala.</span><span class="sxs-lookup"><span data-stu-id="ff678-224">hello **WordCount** component is configured tooonly emit information when a tick tuple arrives.</span></span> <span data-ttu-id="ff678-225">Ele solicita que as tuplas de escala sejam entregues somente a cada cinco segundos.</span><span class="sxs-lookup"><span data-stu-id="ff678-225">It requests that tick tuples are only delivered every five seconds.</span></span>

## <a name="convert-hello-topology-tooflux"></a><span data-ttu-id="ff678-226">Converter Olá topologia tooFlux</span><span class="sxs-lookup"><span data-stu-id="ff678-226">Convert hello topology tooFlux</span></span>

<span data-ttu-id="ff678-227">Fluxo é uma nova estrutura disponível com Storm 0.10.0 e superior, que permite a configuração tooseparate da implementação.</span><span class="sxs-lookup"><span data-stu-id="ff678-227">Flux is a new framework available with Storm 0.10.0 and higher, which allows you tooseparate configuration from implementation.</span></span> <span data-ttu-id="ff678-228">Os componentes ainda são definidos em Java, mas a topologia de saudação é definida usando um arquivo YAML.</span><span class="sxs-lookup"><span data-stu-id="ff678-228">Your components are still defined in Java, but hello topology is defined using a YAML file.</span></span> <span data-ttu-id="ff678-229">Você pode empacotar uma definição de topologia padrão com o seu projeto, ou usar um arquivo autônomo ao enviar a topologia de saudação.</span><span class="sxs-lookup"><span data-stu-id="ff678-229">You can package a default topology definition with your project, or use a standalone file when submitting hello topology.</span></span> <span data-ttu-id="ff678-230">Ao enviar Olá topologia tooStorm, você pode usar variáveis de ambiente ou valores de toopopulate de arquivos de configuração Olá definição de topologia YAML.</span><span class="sxs-lookup"><span data-stu-id="ff678-230">When submitting hello topology tooStorm, you can use environment variables or configuration files toopopulate values in hello YAML topology definition.</span></span>

<span data-ttu-id="ff678-231">arquivo YAML de saudação define Olá componentes toouse topologia hello e saudação de fluxo de dados entre eles.</span><span class="sxs-lookup"><span data-stu-id="ff678-231">hello YAML file defines hello components toouse for hello topology and hello data flow between them.</span></span> <span data-ttu-id="ff678-232">Você pode incluir um arquivo YAML como parte do arquivo jar do hello, ou você pode usar um arquivo YAML externo.</span><span class="sxs-lookup"><span data-stu-id="ff678-232">You can include a YAML file as part of hello jar file or you can use an external YAML file.</span></span>

<span data-ttu-id="ff678-233">Para saber mais sobre o Flux, veja [Estrutura do Flux (https://storm.apache.org/releases/0.10.0/flux.html)](https://storm.apache.org/releases/0.10.0/flux.html).</span><span class="sxs-lookup"><span data-stu-id="ff678-233">For more information on Flux, see [Flux framework (https://storm.apache.org/releases/0.10.0/flux.html)](https://storm.apache.org/releases/0.10.0/flux.html).</span></span>

> [!WARNING]
> <span data-ttu-id="ff678-234">Vencimento tooa [bug (https://issues.apache.org/jira/browse/STORM-2055)](https://issues.apache.org/jira/browse/STORM-2055) com Storm 1.0.1, talvez seja necessário tooinstall um [ambiente de desenvolvimento Storm](https://storm.apache.org/releases/1.0.1/Setting-up-development-environment.html) toorun localmente topologias de fluxo.</span><span class="sxs-lookup"><span data-stu-id="ff678-234">Due tooa [bug (https://issues.apache.org/jira/browse/STORM-2055)](https://issues.apache.org/jira/browse/STORM-2055) with Storm 1.0.1, you may need tooinstall a [Storm development environment](https://storm.apache.org/releases/1.0.1/Setting-up-development-environment.html) toorun Flux topologies locally.</span></span>

1. <span data-ttu-id="ff678-235">Mover Olá `WordCountTopology.java` arquivo fora do projeto de saudação.</span><span class="sxs-lookup"><span data-stu-id="ff678-235">Move hello `WordCountTopology.java` file out of hello project.</span></span> <span data-ttu-id="ff678-236">Anteriormente, esse arquivo definido topologia hello, mas não é necessária com o fluxo.</span><span class="sxs-lookup"><span data-stu-id="ff678-236">Previously, this file defined hello topology, but isn't needed with Flux.</span></span>

2. <span data-ttu-id="ff678-237">Em Olá `resources` diretório, crie um arquivo chamado `topology.yaml`.</span><span class="sxs-lookup"><span data-stu-id="ff678-237">In hello `resources` directory, create a file named `topology.yaml`.</span></span> <span data-ttu-id="ff678-238">Use Olá depois do texto como o conteúdo deste arquivo hello.</span><span class="sxs-lookup"><span data-stu-id="ff678-238">Use hello following text as hello contents of this file.</span></span>

        name: "wordcount"       # friendly name for hello topology
        
        config:                 # Topology configuration
        topology.workers: 1     # Hint for hello number of workers toocreate
        
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
            from: "sentence-spout"       # hello stream emitter
            to: "splitter-bolt"          # hello stream consumer
            grouping:                    # Grouping type
                type: SHUFFLE
          
            - name: "Splitter -> Counter"
            from: "splitter-bolt"
            to: "counter-bolt"
            grouping:
            type: FIELDS
                args: ["word"]           # field(s) toogroup on

3. <span data-ttu-id="ff678-239">Verifique Olá toohello alterações a seguir `pom.xml` arquivo.</span><span class="sxs-lookup"><span data-stu-id="ff678-239">Make hello following changes toohello `pom.xml` file.</span></span>
   
   * <span data-ttu-id="ff678-240">Adicionar Olá após nova dependência no hello `<dependencies>` seção:</span><span class="sxs-lookup"><span data-stu-id="ff678-240">Add hello following new dependency in hello `<dependencies>` section:</span></span>
     
        ```xml
        <!-- Add a dependency on hello Flux framework -->
        <dependency>
            <groupId>org.apache.storm</groupId>
            <artifactId>flux-core</artifactId>
            <version>${storm.version}</version>
        </dependency>
        ```
   * <span data-ttu-id="ff678-241">Adicionar Olá seguindo o plug-in toohello `<plugins>` seção.</span><span class="sxs-lookup"><span data-stu-id="ff678-241">Add hello following plugin toohello `<plugins>` section.</span></span> <span data-ttu-id="ff678-242">Este plug-in lida com a criação de um pacote (arquivo jar) Olá para projeto de saudação e aplica alguns tooFlux de transformações específicas ao criar o pacote de saudação.</span><span class="sxs-lookup"><span data-stu-id="ff678-242">This plugin handles hello creation of a package (jar file) for hello project, and applies some transformations specific tooFlux when creating hello package.</span></span>
     
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
                    <!-- We're using Flux, so refer tooit as main -->
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

   * <span data-ttu-id="ff678-243">Em Olá **exec de plugin maven** `<configuration>` seção, altere o valor de saudação para `<mainClass>` muito`org.apache.storm.flux.Flux`.</span><span class="sxs-lookup"><span data-stu-id="ff678-243">In hello **exec-maven-plugin** `<configuration>` section, change hello value for `<mainClass>` too`org.apache.storm.flux.Flux`.</span></span> <span data-ttu-id="ff678-244">Essa configuração permite que o fluxo toohandle executando topologia Olá localmente em desenvolvimento.</span><span class="sxs-lookup"><span data-stu-id="ff678-244">This setting allows Flux toohandle running hello topology locally in development.</span></span>

   * <span data-ttu-id="ff678-245">Em Olá `<resources>` seção, adicione Olá após toohello `<includes>`.</span><span class="sxs-lookup"><span data-stu-id="ff678-245">In hello `<resources>` section, add hello following toohello `<includes>`.</span></span> <span data-ttu-id="ff678-246">Esse XML inclui arquivo YAML Olá que define a topologia de saudação como parte do projeto de saudação.</span><span class="sxs-lookup"><span data-stu-id="ff678-246">This XML includes hello YAML file that defines hello topology as part of hello project.</span></span>

        ```xml
        <include>topology.yaml</include>
        ```

## <a name="test-hello-flux-topology-locally"></a><span data-ttu-id="ff678-247">Topologia de fluxo de saudação teste localmente</span><span class="sxs-lookup"><span data-stu-id="ff678-247">Test hello flux topology locally</span></span>

1. <span data-ttu-id="ff678-248">Use Olá toocompile a seguir e execute a topologia de fluxo hello usando Maven:</span><span class="sxs-lookup"><span data-stu-id="ff678-248">Use hello following toocompile and execute hello Flux topology using Maven:</span></span>

    ```bash
    mvn compile exec:java -Dexec.args="--local -R /topology.yaml"
    ```

    <span data-ttu-id="ff678-249">Se você estiver usando o PowerShell, use Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="ff678-249">If you are using PowerShell, use hello following command:</span></span>

    ```bash
    mvn compile exec:java "-Dexec.args=--local -R /topology.yaml"
    ```

    > [!WARNING]
    > <span data-ttu-id="ff678-250">Se a topologia usar bits do Storm 1.0.1, esse comando falhará.</span><span class="sxs-lookup"><span data-stu-id="ff678-250">If your topology uses Storm 1.0.1 bits, this command fails.</span></span> <span data-ttu-id="ff678-251">Essa falha é causada por [https://issues.apache.org/jira/browse/STORM-2055](https://issues.apache.org/jira/browse/STORM-2055).</span><span class="sxs-lookup"><span data-stu-id="ff678-251">This failure is caused by [https://issues.apache.org/jira/browse/STORM-2055](https://issues.apache.org/jira/browse/STORM-2055).</span></span> <span data-ttu-id="ff678-252">Em vez disso, [instalar Storm em seu ambiente de desenvolvimento](http://storm.apache.org/releases/0.10.0/Setting-up-development-environment.html) e use Olá informações a seguir.</span><span class="sxs-lookup"><span data-stu-id="ff678-252">Instead, [install Storm in your development environment](http://storm.apache.org/releases/0.10.0/Setting-up-development-environment.html) and use hello following information.</span></span>

    <span data-ttu-id="ff678-253">Se você tiver [instalado Storm em seu ambiente de desenvolvimento](http://storm.apache.org/releases/0.10.0/Setting-up-development-environment.html), você pode usar o hello comandos a seguir em vez disso:</span><span class="sxs-lookup"><span data-stu-id="ff678-253">If you have [installed Storm in your development environment](http://storm.apache.org/releases/0.10.0/Setting-up-development-environment.html), you can use hello following commands instead:</span></span>

    ```bash
    mvn compile package
    storm jar target/WordCount-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --local -R /topology.yaml
    ```

    <span data-ttu-id="ff678-254">Olá `--local` parâmetro executa topologia Olá em modo local no seu ambiente de desenvolvimento.</span><span class="sxs-lookup"><span data-stu-id="ff678-254">hello `--local` parameter runs hello topology in local mode on your development environment.</span></span> <span data-ttu-id="ff678-255">Olá `-R /topology.yaml` usa o parâmetro hello `topology.yaml` recursos de arquivo de topologia de Olá Olá jar arquivo toodefine.</span><span class="sxs-lookup"><span data-stu-id="ff678-255">hello `-R /topology.yaml` parameter uses hello `topology.yaml` file resource from hello jar file toodefine hello topology.</span></span>

    <span data-ttu-id="ff678-256">Como ele é executado, topologia Olá exibe informações de inicialização.</span><span class="sxs-lookup"><span data-stu-id="ff678-256">As it runs, hello topology displays startup information.</span></span> <span data-ttu-id="ff678-257">Olá texto a seguir é um exemplo de saída de hello:</span><span class="sxs-lookup"><span data-stu-id="ff678-257">hello following text is an example of hello output:</span></span>

        17:33:27 [Thread-12-count] INFO  com.microsoft.example.WordCount - Emitting a count of 56 for word snow
        17:33:27 [Thread-12-count] INFO  com.microsoft.example.WordCount - Emitting a count of 56 for word white
        17:33:27 [Thread-12-count] INFO  com.microsoft.example.WordCount - Emitting a count of 112 for word seven
        17:33:27 [Thread-16-count] INFO  com.microsoft.example.WordCount - Emitting a count of 195 for word the
        17:33:27 [Thread-30-count] INFO  com.microsoft.example.WordCount - Emitting a count of 113 for word and
        17:33:27 [Thread-30-count] INFO  com.microsoft.example.WordCount - Emitting a count of 57 for word dwarfs

    <span data-ttu-id="ff678-258">Há um atraso de 10 segundos entre os lotes das informações registradas em log.</span><span class="sxs-lookup"><span data-stu-id="ff678-258">There is a 10-second delay between batches of logged information.</span></span>

2. <span data-ttu-id="ff678-259">Faça uma cópia do hello `topology.yaml` arquivo de projeto do hello.</span><span class="sxs-lookup"><span data-stu-id="ff678-259">Make a copy of hello `topology.yaml` file from hello project.</span></span> <span data-ttu-id="ff678-260">Novo arquivo de saudação nome `newtopology.yaml`.</span><span class="sxs-lookup"><span data-stu-id="ff678-260">Name hello new file `newtopology.yaml`.</span></span> <span data-ttu-id="ff678-261">Em Olá `newtopology.yaml` de arquivo, localize a seguinte Olá seção e altera o valor de saudação do `10` muito`5`.</span><span class="sxs-lookup"><span data-stu-id="ff678-261">In hello `newtopology.yaml` file, find hello following section and change hello value of `10` too`5`.</span></span> <span data-ttu-id="ff678-262">Esse intervalo de saudação modificação alterações entre a emissão de lotes de palavra contagens de too5 de 10 segundos.</span><span class="sxs-lookup"><span data-stu-id="ff678-262">This modification changes hello interval between emitting batches of word counts from 10 seconds too5.</span></span>

    ```yaml
    - id: "counter-bolt"
    className: "com.microsoft.example.WordCount"
    constructorArgs:
    - 5
    parallelism: 1
    ```yaml

3. toorun hello topology, use hello following command:

    ```bash
    mvn exec:java -Dexec.args="--local /path/to/newtopology.yaml"
    ```

    <span data-ttu-id="ff678-263">Se preferir, se você tiver o Storm no ambiente de desenvolvimento:</span><span class="sxs-lookup"><span data-stu-id="ff678-263">Or, if you have Storm on your development environment:</span></span>

    ```bash
    storm jar target/WordCount-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --local /path/to/newtopology.yaml
    ```

    <span data-ttu-id="ff678-264">Saudação de alteração `/path/to/newtopology.yaml` toohello caminho toohello newtopology.yaml arquivo criado na etapa anterior hello.</span><span class="sxs-lookup"><span data-stu-id="ff678-264">Change hello `/path/to/newtopology.yaml` toohello path toohello newtopology.yaml file you created in hello previous step.</span></span> <span data-ttu-id="ff678-265">Esse comando usa Olá newtopology.yaml como definição de topologia de saudação.</span><span class="sxs-lookup"><span data-stu-id="ff678-265">This command uses hello newtopology.yaml as hello topology definition.</span></span> <span data-ttu-id="ff678-266">Como não incluímos Olá `compile` parâmetro, Maven usa a versão de saudação do projeto de saudação criado nas etapas anteriores.</span><span class="sxs-lookup"><span data-stu-id="ff678-266">Since we didn't include hello `compile` parameter, Maven uses hello version of hello project built in previous steps.</span></span>

    <span data-ttu-id="ff678-267">Uma vez Olá topologia é iniciado, você deve observar que o tempo de saudação entre os lotes emitidos alterou o valor de saudação de tooreflect em newtopology.yaml.</span><span class="sxs-lookup"><span data-stu-id="ff678-267">Once hello topology starts, you should notice that hello time between emitted batches has changed tooreflect hello value in newtopology.yaml.</span></span> <span data-ttu-id="ff678-268">Como você pode ver que você pode alterar sua configuração por meio de um arquivo YAML sem a necessidade de topologia de saudação toorecompile.</span><span class="sxs-lookup"><span data-stu-id="ff678-268">So you can see that you can change your configuration through a YAML file without having toorecompile hello topology.</span></span>

<span data-ttu-id="ff678-269">Para obter mais informações sobre esses e outros recursos da estrutura do fluxo de hello, consulte [fluxo (https://storm.apache.org/releases/0.10.0/flux.html)](https://storm.apache.org/releases/0.10.0/flux.html).</span><span class="sxs-lookup"><span data-stu-id="ff678-269">For more information on these and other features of hello Flux framework, see [Flux (https://storm.apache.org/releases/0.10.0/flux.html)](https://storm.apache.org/releases/0.10.0/flux.html).</span></span>

## <a name="trident"></a><span data-ttu-id="ff678-270">Trident</span><span class="sxs-lookup"><span data-stu-id="ff678-270">Trident</span></span>

<span data-ttu-id="ff678-271">O Trident é uma abstração de alto nível fornecida pelo Storm.</span><span class="sxs-lookup"><span data-stu-id="ff678-271">Trident is a high-level abstraction that is provided by Storm.</span></span> <span data-ttu-id="ff678-272">Ele dá suporte ao processamento com monitoramento de estado.</span><span class="sxs-lookup"><span data-stu-id="ff678-272">It supports stateful processing.</span></span> <span data-ttu-id="ff678-273">Olá principal vantagem do Trident é que possa garantir que cada mensagem que entra em topologia Olá é processada apenas uma vez.</span><span class="sxs-lookup"><span data-stu-id="ff678-273">hello primary advantage of Trident is that it can guarantee that every message that enters hello topology is processed only once.</span></span> <span data-ttu-id="ff678-274">Sem usar o Trident, sua topologia só pode garantir que as mensagens sejam processadas pelo menos uma vez.</span><span class="sxs-lookup"><span data-stu-id="ff678-274">Without using Trident, your topology can only guarantee that messages are processed at least once.</span></span> <span data-ttu-id="ff678-275">Também existem outras diferenças, como componentes internos que podem ser usados em vez da criação de bolts.</span><span class="sxs-lookup"><span data-stu-id="ff678-275">There are also other differences, such as built-in components that can be used instead of creating bolts.</span></span> <span data-ttu-id="ff678-276">Na verdade, os bolts são substituídos por componentes menos genéricos, como filtros, projeções e funções.</span><span class="sxs-lookup"><span data-stu-id="ff678-276">In fact, bolts are replaced by less-generic components, such as filters, projections, and functions.</span></span>

<span data-ttu-id="ff678-277">Os aplicativos Trident podem ser criados usando projetos Maven.</span><span class="sxs-lookup"><span data-stu-id="ff678-277">Trident applications can be created by using Maven projects.</span></span> <span data-ttu-id="ff678-278">Use Olá basic mesmo etapas, conforme apresentado anteriormente neste artigo — somente código Olá é diferente.</span><span class="sxs-lookup"><span data-stu-id="ff678-278">You use hello same basic steps as presented earlier in this article—only hello code is different.</span></span> <span data-ttu-id="ff678-279">Trident também (atualmente) não pode ser usado com o framework de fluxo de saudação.</span><span class="sxs-lookup"><span data-stu-id="ff678-279">Trident also cannot (currently) be used with hello Flux framework.</span></span>

<span data-ttu-id="ff678-280">Para obter mais informações sobre Trident, consulte Olá [visão geral da API Trident](http://storm.apache.org/documentation/Trident-API-Overview.html).</span><span class="sxs-lookup"><span data-stu-id="ff678-280">For more information about Trident, see hello [Trident API Overview](http://storm.apache.org/documentation/Trident-API-Overview.html).</span></span>

<span data-ttu-id="ff678-281">Para obter um exemplo de um aplicativo Trident, consulte [Trending topics do Twitter com Apache Storm no HDInsight](hdinsight-storm-twitter-trending.md).</span><span class="sxs-lookup"><span data-stu-id="ff678-281">For an example of a Trident application, see [Twitter trending topics with Apache Storm on HDInsight](hdinsight-storm-twitter-trending.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="ff678-282">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="ff678-282">Next Steps</span></span>

<span data-ttu-id="ff678-283">Você aprendeu como toocreate uma topologia Storm usando Java.</span><span class="sxs-lookup"><span data-stu-id="ff678-283">You have learned how toocreate a Storm topology by using Java.</span></span> <span data-ttu-id="ff678-284">Agora saiba como:</span><span class="sxs-lookup"><span data-stu-id="ff678-284">Now learn how to:</span></span>

* [<span data-ttu-id="ff678-285">Implantar e gerenciar topologias Apache Storm no HDInsight</span><span class="sxs-lookup"><span data-stu-id="ff678-285">Deploy and manage Apache Storm topologies on HDInsight</span></span>](hdinsight-storm-deploy-monitor-topology.md)

* [<span data-ttu-id="ff678-286">Desenvolver topologias C# para o Apache Storm no HDInsight usando o Visual Studio</span><span class="sxs-lookup"><span data-stu-id="ff678-286">Develop C# topologies for Apache Storm on HDInsight using Visual Studio</span></span>](hdinsight-storm-develop-csharp-visual-studio-topology.md)

<span data-ttu-id="ff678-287">Para obter mais topologias Storm, consulte [Topologias de exemplo para o Storm no HDInsight](hdinsight-storm-example-topology.md).</span><span class="sxs-lookup"><span data-stu-id="ff678-287">You can find more example Storm topologies by visiting [Example topologies for Storm on HDInsight](hdinsight-storm-example-topology.md).</span></span>

