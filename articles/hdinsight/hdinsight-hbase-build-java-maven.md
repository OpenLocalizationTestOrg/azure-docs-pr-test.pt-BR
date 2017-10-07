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
# <a name="use-maven-toobuild-java-applications-that-use-hbase-with-windows-based-hdinsight-hadoop"></a><span data-ttu-id="b274c-103">Usar Maven toobuild Java aplicativos que usam HBase com HDInsight baseados em Windows (Hadoop)</span><span class="sxs-lookup"><span data-stu-id="b274c-103">Use Maven toobuild Java applications that use HBase with Windows-based HDInsight (Hadoop)</span></span>
<span data-ttu-id="b274c-104">Saiba como toocreate e criar um [HBase Apache](http://hbase.apache.org/) aplicativo em Java usando o Apache Maven.</span><span class="sxs-lookup"><span data-stu-id="b274c-104">Learn how toocreate and build an [Apache HBase](http://hbase.apache.org/) application in Java by using Apache Maven.</span></span> <span data-ttu-id="b274c-105">Em seguida, use o aplicativo hello com Azure HDInsight (Hadoop).</span><span class="sxs-lookup"><span data-stu-id="b274c-105">Then use hello application with Azure HDInsight (Hadoop).</span></span>

<span data-ttu-id="b274c-106">[Maven](http://maven.apache.org/) é um projeto management e compreender ferramenta de software que permite que você toobuild software, documentação e relatórios para projetos Java.</span><span class="sxs-lookup"><span data-stu-id="b274c-106">[Maven](http://maven.apache.org/) is a software project management and comprehension tool that allows you toobuild software, documentation, and reports for Java projects.</span></span> <span data-ttu-id="b274c-107">Neste artigo, você aprenderá como toouse-toocreate um aplicativo Java básico que cria, consulta e exclui um HBase de tabela em um cluster HDInsight do Azure.</span><span class="sxs-lookup"><span data-stu-id="b274c-107">In this article, you learn how toouse it toocreate a basic Java application that that creates, queries, and deletes an HBase table on an Azure HDInsight cluster.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b274c-108">etapas de saudação neste documento exigem um cluster HDInsight que usa o Windows.</span><span class="sxs-lookup"><span data-stu-id="b274c-108">hello steps in this document require an HDInsight cluster that uses Windows.</span></span> <span data-ttu-id="b274c-109">Linux é Olá sistema operacional somente de usado no HDInsight versão 3.4 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="b274c-109">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="b274c-110">Para obter mais informações, confira [baixa do HDInsight no Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="b274c-110">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <a name="requirements"></a><span data-ttu-id="b274c-111">Requisitos</span><span class="sxs-lookup"><span data-stu-id="b274c-111">Requirements</span></span>
* <span data-ttu-id="b274c-112">[Plataforma Java JDK](http://www.oracle.com/technetwork/java/javase/downloads/index.html) 7 ou superior</span><span class="sxs-lookup"><span data-stu-id="b274c-112">[Java platform JDK](http://www.oracle.com/technetwork/java/javase/downloads/index.html) 7 or later</span></span>
* [<span data-ttu-id="b274c-113">Maven</span><span class="sxs-lookup"><span data-stu-id="b274c-113">Maven</span></span>](http://maven.apache.org/)
* <span data-ttu-id="b274c-114">Um cluster HDInsight baseado no Windows com HBase</span><span class="sxs-lookup"><span data-stu-id="b274c-114">A Windows-based HDInsight cluster with HBase</span></span>

    > [!NOTE]
    > <span data-ttu-id="b274c-115">Olá etapas neste documento foram testadas com as versões 3.2 e 3.3 do HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="b274c-115">hello steps in this document have been tested with HDInsight cluster versions 3.2 and 3.3.</span></span> <span data-ttu-id="b274c-116">valores padrão de saudação fornecidos nos exemplos são para um cluster HDInsight 3.3.</span><span class="sxs-lookup"><span data-stu-id="b274c-116">hello default values provided in examples are for a HDInsight 3.3 cluster.</span></span>

## <a name="create-hello-project"></a><span data-ttu-id="b274c-117">Criar projeto Olá</span><span class="sxs-lookup"><span data-stu-id="b274c-117">Create hello project</span></span>
1. <span data-ttu-id="b274c-118">Na linha de comando de saudação em seu ambiente de desenvolvimento, alterar o local de toohello de diretórios em que você deseja toocreate Olá projeto, por exemplo, `cd code\hdinsight`.</span><span class="sxs-lookup"><span data-stu-id="b274c-118">From hello command line in your development environment, change directories toohello location where you want toocreate hello project, for example, `cd code\hdinsight`.</span></span>
2. <span data-ttu-id="b274c-119">Saudação de uso **mvn** comando, que é instalado com o Maven, Olá toogenerate estrutura do projeto de saudação.</span><span class="sxs-lookup"><span data-stu-id="b274c-119">Use hello **mvn** command, which is installed with Maven, toogenerate hello scaffolding for hello project.</span></span>

        mvn archetype:generate -DgroupId=com.microsoft.examples -DartifactId=hbaseapp -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false

    <span data-ttu-id="b274c-120">Este comando cria um diretório no local atual do hello, com o nome de saudação especificado pelo Olá **artifactID** parâmetro (**hbaseapp** neste exemplo.) Este diretório contém Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="b274c-120">This command creates a directory in hello current location, with hello name specified by hello **artifactID** parameter (**hbaseapp** in this example.) This directory contains hello following items:</span></span>

   * <span data-ttu-id="b274c-121">**POM.XML**: Olá o modelo de objeto do projeto ([POM](http://maven.apache.org/guides/introduction/introduction-to-the-pom.html)) contém informações e configuração detalhes usados toobuild Olá projeto.</span><span class="sxs-lookup"><span data-stu-id="b274c-121">**pom.xml**:  hello Project Object Model ([POM](http://maven.apache.org/guides/introduction/introduction-to-the-pom.html)) contains information and configuration details used toobuild hello project.</span></span>
   * <span data-ttu-id="b274c-122">**src**: diretório de saudação que contém a saudação **main\java\com\microsoft\examples** directory, onde você irá criar aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="b274c-122">**src**: hello directory that contains hello **main\java\com\microsoft\examples** directory, where you will author hello application.</span></span>
3. <span data-ttu-id="b274c-123">Excluir Olá **src\test\java\com\microsoft\examples\apptest.java** arquivo porque ele não é usado neste exemplo.</span><span class="sxs-lookup"><span data-stu-id="b274c-123">Delete hello **src\test\java\com\microsoft\examples\apptest.java** file because it is not used in this example.</span></span>

## <a name="update-hello-project-object-model"></a><span data-ttu-id="b274c-124">Saudação de atualizar o modelo de objeto de projeto</span><span class="sxs-lookup"><span data-stu-id="b274c-124">Update hello Project Object Model</span></span>
1. <span data-ttu-id="b274c-125">Editar saudação **pom.xml** de arquivos e adicionar Olá seguindo o código dentro de saudação `<dependencies>` seção:</span><span class="sxs-lookup"><span data-stu-id="b274c-125">Edit hello **pom.xml** file and add hello following code inside hello `<dependencies>` section:</span></span>

        <dependency>
          <groupId>org.apache.hbase</groupId>
          <artifactId>hbase-client</artifactId>
          <version>1.1.2</version>
        </dependency>

    <span data-ttu-id="b274c-126">Esta seção informa Maven que Olá projeto requer **hbase cliente** versão **1.1.2**.</span><span class="sxs-lookup"><span data-stu-id="b274c-126">This section tells Maven that hello project requires **hbase-client** version **1.1.2**.</span></span> <span data-ttu-id="b274c-127">Em tempo de compilação, a dependência é baixada do repositório de Maven saudação padrão.</span><span class="sxs-lookup"><span data-stu-id="b274c-127">At compile time, this dependency is downloaded from hello default Maven repository.</span></span> <span data-ttu-id="b274c-128">Você pode usar o hello [pesquisa de repositório Central Maven](http://search.maven.org/#artifactdetails%7Corg.apache.hbase%7Chbase-client%7C0.98.4-hadoop2%7Cjar) toolearn mais sobre essa dependência.</span><span class="sxs-lookup"><span data-stu-id="b274c-128">You can use hello [Maven Central Repository Search](http://search.maven.org/#artifactdetails%7Corg.apache.hbase%7Chbase-client%7C0.98.4-hadoop2%7Cjar) toolearn more about this dependency.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="b274c-129">número de versão de Hello deve corresponder a versão de saudação do HBase que é fornecido com o seu cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="b274c-129">hello version number must match hello version of HBase that is provided with your HDInsight cluster.</span></span> <span data-ttu-id="b274c-130">Use Olá número de versão correta de saudação de toofind tabela a seguir.</span><span class="sxs-lookup"><span data-stu-id="b274c-130">Use hello following table toofind hello correct version number.</span></span>
   >
   >

   | <span data-ttu-id="b274c-131">Versão do cluster HDInsight</span><span class="sxs-lookup"><span data-stu-id="b274c-131">HDInsight cluster version</span></span> | <span data-ttu-id="b274c-132">Toouse de versão do HBase</span><span class="sxs-lookup"><span data-stu-id="b274c-132">HBase version toouse</span></span> |
   | --- | --- |
   | <span data-ttu-id="b274c-133">3.2</span><span class="sxs-lookup"><span data-stu-id="b274c-133">3.2</span></span> |<span data-ttu-id="b274c-134">0.98.4-hadoop2</span><span class="sxs-lookup"><span data-stu-id="b274c-134">0.98.4-hadoop2</span></span> |
   | <span data-ttu-id="b274c-135">3.3</span><span class="sxs-lookup"><span data-stu-id="b274c-135">3.3</span></span> |<span data-ttu-id="b274c-136">1.1.2</span><span class="sxs-lookup"><span data-stu-id="b274c-136">1.1.2</span></span> |

    <span data-ttu-id="b274c-137">Para obter mais informações sobre as versões de HDInsight e componentes, consulte [quais são Olá Hadoop componentes diferentes disponíveis com o HDInsight](hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="b274c-137">For more information on HDInsight versions and components, see [What are hello different Hadoop components available with HDInsight](hdinsight-component-versioning.md).</span></span>
2. <span data-ttu-id="b274c-138">Se você estiver usando um cluster HDInsight 3.3, você também deverá adicionar Olá após toohello `<dependencies>` seção:</span><span class="sxs-lookup"><span data-stu-id="b274c-138">If you are using an HDInsight 3.3 cluster, you must also add hello following toohello `<dependencies>` section:</span></span>

        <dependency>
            <groupId>org.apache.phoenix</groupId>
            <artifactId>phoenix-core</artifactId>
            <version>4.4.0-HBase-1.1</version>
        </dependency>

    <span data-ttu-id="b274c-139">Essa dependência carregará componentes de phoenix core hello, que são usados pelo Hbase versão 1.1.</span><span class="sxs-lookup"><span data-stu-id="b274c-139">This dependency will load hello phoenix-core components, which are used by Hbase version 1.1.x.</span></span>
3. <span data-ttu-id="b274c-140">Adicionar Olá toohello de código a seguir **pom.xml** arquivo.</span><span class="sxs-lookup"><span data-stu-id="b274c-140">Add hello following code toohello **pom.xml** file.</span></span> <span data-ttu-id="b274c-141">Esta seção deve estar dentro de saudação `<project>...</project>` marcas de saudação do arquivo, por exemplo, entre `</dependencies>` e `</project>`.</span><span class="sxs-lookup"><span data-stu-id="b274c-141">This section must be inside hello `<project>...</project>` tags in hello file, for example, between `</dependencies>` and `</project>`.</span></span>

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

    <span data-ttu-id="b274c-142">Olá `<resources>` seção configura um recurso (**conf\hbase Storm-site.XML**) que contém informações de configuração para HBase.</span><span class="sxs-lookup"><span data-stu-id="b274c-142">hello `<resources>` section configures a resource (**conf\hbase-site.xml**) that contains configuration information for HBase.</span></span>

   > [!NOTE]
   > <span data-ttu-id="b274c-143">Você também pode definir valores de configuração via código.</span><span class="sxs-lookup"><span data-stu-id="b274c-143">You can also set configuration values via code.</span></span> <span data-ttu-id="b274c-144">Consulte comentários Olá Olá **CreateTable** exemplo a seguir para saber como toodo isso.</span><span class="sxs-lookup"><span data-stu-id="b274c-144">See hello comments in hello **CreateTable** example that follows for how toodo this.</span></span>
   >
   >

    <span data-ttu-id="b274c-145">Isso `<plugins>` seção configura Olá [plug-in de compilador Maven](http://maven.apache.org/plugins/maven-compiler-plugin/) e [plug-in de sombra Maven](http://maven.apache.org/plugins/maven-shade-plugin/).</span><span class="sxs-lookup"><span data-stu-id="b274c-145">This `<plugins>` section configures hello [Maven Compiler Plugin](http://maven.apache.org/plugins/maven-compiler-plugin/) and [Maven Shade Plugin](http://maven.apache.org/plugins/maven-shade-plugin/).</span></span> <span data-ttu-id="b274c-146">compilador de saudação plug-in é usado toocompile Olá topologia.</span><span class="sxs-lookup"><span data-stu-id="b274c-146">hello compiler plug-in is used toocompile hello topology.</span></span> <span data-ttu-id="b274c-147">Sombreamento de saudação plug-in é usado tooprevent eliminação de duplicação de licença no pacote JAR Olá que é criada pelo Maven.</span><span class="sxs-lookup"><span data-stu-id="b274c-147">hello shade plug-in is used tooprevent license duplication in hello JAR package that is built by Maven.</span></span> <span data-ttu-id="b274c-148">motivo de saudação que é usado é que os arquivos de licença duplicadas de saudação causam um erro em tempo de execução no cluster do HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="b274c-148">hello reason this is used is that hello duplicate license files cause an error at run time on hello HDInsight cluster.</span></span> <span data-ttu-id="b274c-149">Usando o plugin do maven sombreamento com hello `ApacheLicenseResourceTransformer` implementação impede que esse erro.</span><span class="sxs-lookup"><span data-stu-id="b274c-149">Using maven-shade-plugin with hello `ApacheLicenseResourceTransformer` implementation prevents this error.</span></span>

    <span data-ttu-id="b274c-150">Olá maven-tonalidade-plug-in também produz uma grande jar (ou jar fat) que contém todas as dependências de Olá exigidas pelo aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="b274c-150">hello maven-shade-plugin also produces an uber jar (or fat jar) that contains all hello dependencies required by hello application.</span></span>
4. <span data-ttu-id="b274c-151">Salvar Olá **pom.xml** arquivo.</span><span class="sxs-lookup"><span data-stu-id="b274c-151">Save hello **pom.xml** file.</span></span>
5. <span data-ttu-id="b274c-152">Crie um novo diretório chamado **conf** em Olá **hbaseapp** directory.</span><span class="sxs-lookup"><span data-stu-id="b274c-152">Create a new directory named **conf** in hello **hbaseapp** directory.</span></span> <span data-ttu-id="b274c-153">Em Olá **conf** diretório, crie um arquivo chamado **hbase-site.XML**.</span><span class="sxs-lookup"><span data-stu-id="b274c-153">In hello **conf** directory, create a file named **hbase-site.xml**.</span></span> <span data-ttu-id="b274c-154">Use o seguinte hello como conteúdo de saudação do arquivo hello:</span><span class="sxs-lookup"><span data-stu-id="b274c-154">Use hello following as hello contents of hello file:</span></span>

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

    <span data-ttu-id="b274c-155">Esse arquivo será a configuração de HBase Olá tooload usado para um cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="b274c-155">This file will be used tooload hello HBase configuration for an HDInsight cluster.</span></span>

   > [!NOTE]
   > <span data-ttu-id="b274c-156">Este é um arquivo hbase-site.XML mínima e contém as configurações mínimas de bare da saudação de cluster do HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="b274c-156">This is a minimal hbase-site.xml file, and it contains hello bare minimum settings for hello HDInsight cluster.</span></span>

6. <span data-ttu-id="b274c-157">Salvar Olá **hbase-site.XML** arquivo.</span><span class="sxs-lookup"><span data-stu-id="b274c-157">Save hello **hbase-site.xml** file.</span></span>

## <a name="create-hello-application"></a><span data-ttu-id="b274c-158">Criar um aplicativo hello</span><span class="sxs-lookup"><span data-stu-id="b274c-158">Create hello application</span></span>
1. <span data-ttu-id="b274c-159">Vá toohello **hbaseapp\src\main\java\com\microsoft\examples** diretório e renomear Olá arquivo app.java muito**CreateTable.java**.</span><span class="sxs-lookup"><span data-stu-id="b274c-159">Go toohello **hbaseapp\src\main\java\com\microsoft\examples** directory and rename hello app.java file too**CreateTable.java**.</span></span>
2. <span data-ttu-id="b274c-160">Olá abrir **CreateTable.java** de arquivo e substitua conteúdo existente Olá Olá código a seguir:</span><span class="sxs-lookup"><span data-stu-id="b274c-160">Open hello **CreateTable.java** file and replace hello existing contents with hello following code:</span></span>

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

    <span data-ttu-id="b274c-161">Isso é hello **CreateTable** classe, que criará uma tabela denominada **pessoas** e preenchê-la com alguns usuários predefinidos.</span><span class="sxs-lookup"><span data-stu-id="b274c-161">This is hello **CreateTable** class, which will create a table named **people** and populate it with some predefined users.</span></span>
3. <span data-ttu-id="b274c-162">Salvar Olá **CreateTable.java** arquivo.</span><span class="sxs-lookup"><span data-stu-id="b274c-162">Save hello **CreateTable.java** file.</span></span>
4. <span data-ttu-id="b274c-163">Em Olá **hbaseapp\src\main\java\com\microsoft\examples** diretório, crie um novo arquivo chamado **SearchByEmail.java**.</span><span class="sxs-lookup"><span data-stu-id="b274c-163">In hello **hbaseapp\src\main\java\com\microsoft\examples** directory, create a new file named **SearchByEmail.java**.</span></span> <span data-ttu-id="b274c-164">Use Olá código a seguir como o conteúdo deste arquivo hello:</span><span class="sxs-lookup"><span data-stu-id="b274c-164">Use hello following code as hello contents of this file:</span></span>

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

    <span data-ttu-id="b274c-165">Olá **SearchByEmail** classe pode ser usado tooquery para linhas por endereço de email.</span><span class="sxs-lookup"><span data-stu-id="b274c-165">hello **SearchByEmail** class can be used tooquery for rows by email address.</span></span> <span data-ttu-id="b274c-166">Porque ele usa um filtro de expressão regular, você pode fornecer uma cadeia de caracteres ou uma expressão regular ao usar a classe de saudação.</span><span class="sxs-lookup"><span data-stu-id="b274c-166">Because it uses a regular expression filter, you can provide either a string or a regular expression when using hello class.</span></span>
5. <span data-ttu-id="b274c-167">Salvar Olá **SearchByEmail.java** arquivo.</span><span class="sxs-lookup"><span data-stu-id="b274c-167">Save hello **SearchByEmail.java** file.</span></span>
6. <span data-ttu-id="b274c-168">Em Olá **hbaseapp\src\main\hava\com\microsoft\examples** diretório, crie um novo arquivo chamado **DeleteTable.java**.</span><span class="sxs-lookup"><span data-stu-id="b274c-168">In hello **hbaseapp\src\main\hava\com\microsoft\examples** directory, create a new file named **DeleteTable.java**.</span></span> <span data-ttu-id="b274c-169">Use Olá código a seguir como o conteúdo deste arquivo hello:</span><span class="sxs-lookup"><span data-stu-id="b274c-169">Use hello following code as hello contents of this file:</span></span>

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

    <span data-ttu-id="b274c-170">Essa classe é para limpar esse exemplo desabilitando e descartando Olá tabela criados por Olá **CreateTable** classe.</span><span class="sxs-lookup"><span data-stu-id="b274c-170">This class is for cleaning up this example by disabling and dropping hello table created by hello **CreateTable** class.</span></span>
7. <span data-ttu-id="b274c-171">Salvar Olá **DeleteTable.java** arquivo.</span><span class="sxs-lookup"><span data-stu-id="b274c-171">Save hello **DeleteTable.java** file.</span></span>

## <a name="build-and-package-hello-application"></a><span data-ttu-id="b274c-172">Aplicativo hello de compilação e pacote</span><span class="sxs-lookup"><span data-stu-id="b274c-172">Build and package hello application</span></span>
1. <span data-ttu-id="b274c-173">Abra um prompt de comando e altere os diretórios toohello **hbaseapp** directory.</span><span class="sxs-lookup"><span data-stu-id="b274c-173">Open a command prompt and change directories toohello **hbaseapp** directory.</span></span>
2. <span data-ttu-id="b274c-174">Use Olá comando toobuild um arquivo JAR que contém o aplicativo hello a seguir:</span><span class="sxs-lookup"><span data-stu-id="b274c-174">Use hello following command toobuild a JAR file that contains hello application:</span></span>

        mvn clean package

    <span data-ttu-id="b274c-175">Isso limpa qualquer artefatos de compilação anterior, baixa todas as dependências que ainda não tiver sido instaladas, em seguida, cria e pacotes aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="b274c-175">This cleans any previous build artifacts, downloads any dependencies that have not already been installed, then builds and packages hello application.</span></span>
3. <span data-ttu-id="b274c-176">Quando Olá comando for concluído, hello **hbaseapp\target** diretório contém um arquivo chamado **hbaseapp-1.0-SNAPSHOT.jar**.</span><span class="sxs-lookup"><span data-stu-id="b274c-176">When hello command completes, hello **hbaseapp\target** directory contains a file named **hbaseapp-1.0-SNAPSHOT.jar**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="b274c-177">Olá **hbaseapp-1.0-SNAPSHOT.jar** arquivo é uma grande jar (às vezes chamado de um jar fat,) que contém todas as dependências de saudação necessário toorun aplicativo de hello.</span><span class="sxs-lookup"><span data-stu-id="b274c-177">hello **hbaseapp-1.0-SNAPSHOT.jar** file is an uber jar (sometimes called a fat jar,) which contains all hello dependencies required toorun hello application.</span></span>

## <a name="upload-hello-jar-file-and-start-a-job"></a><span data-ttu-id="b274c-178">Carregue o arquivo JAR de saudação e iniciar um trabalho</span><span class="sxs-lookup"><span data-stu-id="b274c-178">Upload hello JAR file and start a job</span></span>
<span data-ttu-id="b274c-179">Há muitos tooupload de maneiras um cluster do HDInsight de tooyour arquivos, conforme descrito em [carregar dados para trabalhos de Hadoop no HDInsight](hdinsight-upload-data.md).</span><span class="sxs-lookup"><span data-stu-id="b274c-179">There are many ways tooupload a file tooyour HDInsight cluster, as described in [Upload data for Hadoop jobs in HDInsight](hdinsight-upload-data.md).</span></span> <span data-ttu-id="b274c-180">Olá, etapas a seguir usam PowerShell do Azure.</span><span class="sxs-lookup"><span data-stu-id="b274c-180">hello following steps use Azure PowerShell.</span></span>

[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]

1. <span data-ttu-id="b274c-181">Após instalar e configurar o Azure PowerShell, crie um novo arquivo chamado **hbase-runner.psm1**.</span><span class="sxs-lookup"><span data-stu-id="b274c-181">After installing and configuring Azure PowerShell, create a new file named **hbase-runner.psm1**.</span></span> <span data-ttu-id="b274c-182">Use o seguinte de hello como o conteúdo deste arquivo hello:</span><span class="sxs-lookup"><span data-stu-id="b274c-182">Use hello following as hello contents of this file:</span></span>

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

    <span data-ttu-id="b274c-183">Esse arquivo contém dois módulos:</span><span class="sxs-lookup"><span data-stu-id="b274c-183">This file contains two modules:</span></span>

   * <span data-ttu-id="b274c-184">**Adicionar HDInsightFile** -usado tooupload arquivos tooHDInsight</span><span class="sxs-lookup"><span data-stu-id="b274c-184">**Add-HDInsightFile** - used tooupload files tooHDInsight</span></span>
   * <span data-ttu-id="b274c-185">**Iniciar HBaseExample** -toorun Olá classes criadas anteriormente usadas</span><span class="sxs-lookup"><span data-stu-id="b274c-185">**Start-HBaseExample** - used toorun hello classes created earlier</span></span>
2. <span data-ttu-id="b274c-186">Salvar Olá **hbase runner.psm1** arquivo.</span><span class="sxs-lookup"><span data-stu-id="b274c-186">Save hello **hbase-runner.psm1** file.</span></span>
3. <span data-ttu-id="b274c-187">Abra uma nova janela do PowerShell do Azure, altere os diretórios toohello **hbaseapp** directory, e, em seguida, Olá executar comando a seguir.</span><span class="sxs-lookup"><span data-stu-id="b274c-187">Open a new Azure PowerShell window, change directories toohello **hbaseapp** directory, and then run hello following command.</span></span>

        PS C:\ Import-Module c:\path\to\hbase-runner.psm1

    <span data-ttu-id="b274c-188">Alterar Olá caminho toohello local de saudação **hbase runner.psm1** arquivo criado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="b274c-188">Change hello path toohello location of hello **hbase-runner.psm1** file created earlier.</span></span> <span data-ttu-id="b274c-189">Isso registra o módulo Olá para esta sessão do PowerShell do Azure.</span><span class="sxs-lookup"><span data-stu-id="b274c-189">This registers hello module for this Azure PowerShell session.</span></span>
4. <span data-ttu-id="b274c-190">Comando a seguir de saudação do uso Olá tooupload **hbaseapp-1.0-SNAPSHOT.jar** tooyour HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="b274c-190">Use hello following command tooupload hello **hbaseapp-1.0-SNAPSHOT.jar** tooyour HDInsight cluster.</span></span>

        Add-HDInsightFile -localPath target\hbaseapp-1.0-SNAPSHOT.jar -destinationPath example/jars/hbaseapp-1.0-SNAPSHOT.jar -clusterName hdinsightclustername

    <span data-ttu-id="b274c-191">Substituir **hdinsightclustername** com nome de saudação do cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="b274c-191">Replace **hdinsightclustername** with hello name of your HDInsight cluster.</span></span> <span data-ttu-id="b274c-192">comando Olá carrega Olá **hbaseapp-1.0-SNAPSHOT.jar** toohello **exemplo/jars** local no armazenamento primário Olá seu cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="b274c-192">hello command uploads hello **hbaseapp-1.0-SNAPSHOT.jar** toohello **example/jars** location in hello primary storage for your HDInsight cluster.</span></span>
5. <span data-ttu-id="b274c-193">Depois que forem carregados arquivos Olá, use Olá de código a seguir toocreate uma tabela usando Olá **hbaseapp**:</span><span class="sxs-lookup"><span data-stu-id="b274c-193">After hello files are uploaded, use hello following code toocreate a table using hello **hbaseapp**:</span></span>

        Start-HBaseExample -className com.microsoft.examples.CreateTable -clusterName hdinsightclustername

    <span data-ttu-id="b274c-194">Substituir **hdinsightclustername** com nome de saudação do cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="b274c-194">Replace **hdinsightclustername** with hello name of your HDInsight cluster.</span></span>

    <span data-ttu-id="b274c-195">Esse comando cria uma nova tabela chamada **pessoas** em seu cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="b274c-195">This command creates a new table named **people** in your HDInsight cluster.</span></span> <span data-ttu-id="b274c-196">Este comando não mostra nenhuma saída na janela do console de saudação.</span><span class="sxs-lookup"><span data-stu-id="b274c-196">This command does not show any output in hello console window.</span></span>
6. <span data-ttu-id="b274c-197">toosearch de entradas na tabela de hello, use Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="b274c-197">toosearch for entries in hello table, use hello following command:</span></span>

        Start-HBaseExample -className com.microsoft.examples.SearchByEmail -clusterName hdinsightclustername -emailRegex contoso.com

    <span data-ttu-id="b274c-198">Substituir **hdinsightclustername** com nome de saudação do cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="b274c-198">Replace **hdinsightclustername** with hello name of your HDInsight cluster.</span></span>

    <span data-ttu-id="b274c-199">Esse comando usa Olá **SearchByEmail** classe toosearch para todas as linhas onde hello **contactinformation** família de coluna e hello **email** coluna contém a cadeia de caracteres de saudação **contoso.com**. Você deve receber Olá resultados a seguir:</span><span class="sxs-lookup"><span data-stu-id="b274c-199">This command uses hello **SearchByEmail** class toosearch for any rows where hello **contactinformation** column family and hello **email** column, contains hello string **contoso.com**. You should receive hello following results:</span></span>

          Franklin Holtz - ID: 2
          Franklin Holtz - franklin@contoso.com - ID: 2
          Rae Schroeder - ID: 4
          Rae Schroeder - rae@contoso.com - ID: 4
          Gabriela Ingram - ID: 6
          Gabriela Ingram - gabriela@contoso.com - ID: 6

    <span data-ttu-id="b274c-200">Usando **fabrikam.com** para Olá `-emailRegex` valor retorna usuários Olá que têm **fabrikam.com** no campo de email hello.</span><span class="sxs-lookup"><span data-stu-id="b274c-200">Using **fabrikam.com** for hello `-emailRegex` value returns hello users that have **fabrikam.com** in hello email field.</span></span> <span data-ttu-id="b274c-201">Desde que esta pesquisa é implementada usando um filtro de baseadas em expressão regular, você também pode inserir expressões regulares, como **^ r**, quais entradas retorna onde o email Olá começa com hello letra 'r'.</span><span class="sxs-lookup"><span data-stu-id="b274c-201">Since this search is implemented by using a regular expression-based filter, you can also enter regular expressions, such as **^r**, which returns entries where hello email begins with hello letter 'r'.</span></span>

## <a name="delete-hello-table"></a><span data-ttu-id="b274c-202">Excluir tabela Olá</span><span class="sxs-lookup"><span data-stu-id="b274c-202">Delete hello table</span></span>
<span data-ttu-id="b274c-203">Quando tiver terminado com o exemplo hello, comando a seguir do uso Olá de saudação do hello Azure PowerShell sessão toodelete **pessoas** tabela usada neste exemplo:</span><span class="sxs-lookup"><span data-stu-id="b274c-203">When you are done with hello example, use hello following command from hello Azure PowerShell session toodelete hello **people** table used in this example:</span></span>

    Start-HBaseExample -className com.microsoft.examples.DeleteTable -clusterName hdinsightclustername

<span data-ttu-id="b274c-204">Substituir **hdinsightclustername** com nome de saudação do cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="b274c-204">Replace **hdinsightclustername** with hello name of your HDInsight cluster.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="b274c-205">Solucionar problemas</span><span class="sxs-lookup"><span data-stu-id="b274c-205">Troubleshooting</span></span>
### <a name="no-results-or-unexpected-results-when-using-start-hbaseexample"></a><span data-ttu-id="b274c-206">Nenhum resultado ou resultados inesperados ao usar o Start-HBaseExample</span><span class="sxs-lookup"><span data-stu-id="b274c-206">No results or unexpected results when using Start-HBaseExample</span></span>
<span data-ttu-id="b274c-207">Saudação de uso `-showErr` parâmetro tooview saudação padrão erro (STDERR) que é gerado durante o trabalho de saudação em execução.</span><span class="sxs-lookup"><span data-stu-id="b274c-207">Use hello `-showErr` parameter tooview hello standard error (STDERR) that is produced while running hello job.</span></span>
