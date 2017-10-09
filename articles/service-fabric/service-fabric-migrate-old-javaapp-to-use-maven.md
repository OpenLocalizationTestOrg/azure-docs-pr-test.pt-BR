---
title: aaaMigrate do Java SDK tooMaven - atualizar antigo toouse de aplicativos Java do Azure Service Fabric Maven | Microsoft Docs
description: "Atualize Olá aplicativos mais antigos Java que usado toouse Olá SDK de Java do Service Fabric toofetch dependências de serviço do Fabric Java do Maven. Depois de concluir esta instalação, seus aplicativos mais antigos do Java seria capaz de toobuild."
services: service-fabric
documentationcenter: java
author: sayantancs
manager: timlt
editor: 
ms.assetid: bf84458f-4b87-4de1-9844-19909e368deb
ms.service: service-fabric
ms.devlang: java
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/23/2017
ms.author: saysa
ms.openlocfilehash: 11b979facd7b3865141a6d3a035a6021dd06ca0c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="update-your-previous-java-service-fabric-application-toofetch-java-libraries-from-maven"></a><span data-ttu-id="64e1a-104">Atualizar seu anterior Java Service Fabric application toofetch Java bibliotecas do Maven</span><span class="sxs-lookup"><span data-stu-id="64e1a-104">Update your previous Java Service Fabric application toofetch Java libraries from Maven</span></span>
<span data-ttu-id="64e1a-105">Podemos recentemente moveu binários Java de malha do serviço de saudação SDK de Java do Service Fabric tooMaven hospedagem.</span><span class="sxs-lookup"><span data-stu-id="64e1a-105">We have recently moved Service Fabric Java binaries from hello Service Fabric Java SDK tooMaven hosting.</span></span> <span data-ttu-id="64e1a-106">Agora você pode usar **mavencentral** dependências de serviço malha Java toofetch hello mais recentes.</span><span class="sxs-lookup"><span data-stu-id="64e1a-106">Now you can use **mavencentral** toofetch hello latest Service Fabric Java dependencies.</span></span> <span data-ttu-id="64e1a-107">Início rápido ajuda a atualizar seus aplicativos Java existentes, o que você criou anteriormente toobe usada com o SDK do Service Fabric Java, usando qualquer Yeoman modelo ou Eclipse, toobe compatível com hello build Maven com base.</span><span class="sxs-lookup"><span data-stu-id="64e1a-107">This quick-start helps you update your existing Java applications, which you earlier created toobe used with Service Fabric Java SDK, using either Yeoman template or Eclipse, toobe compatible with hello Maven based build.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="64e1a-108">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="64e1a-108">Prerequisites</span></span>
1. <span data-ttu-id="64e1a-109">Primeiro é necessário toouninstall Olá existente do Java SDK.</span><span class="sxs-lookup"><span data-stu-id="64e1a-109">First you need toouninstall hello existing Java SDK.</span></span>

  ```bash
  sudo dpkg -r servicefabricsdkjava
  ```
2. <span data-ttu-id="64e1a-110">A seguir instalação hello mais recente CLI de malha do serviço Olá as etapas mencionadas [aqui](service-fabric-cli.md).</span><span class="sxs-lookup"><span data-stu-id="64e1a-110">Install hello latest Service Fabric CLI following hello steps mentioned [here](service-fabric-cli.md).</span></span>

3. <span data-ttu-id="64e1a-111">toobuild e o trabalho em aplicativos de serviço do Fabric Java Olá, é necessário tooensure que você tenha o JDK 1.8 e Gradle instalado.</span><span class="sxs-lookup"><span data-stu-id="64e1a-111">toobuild and work on hello Service Fabric Java applications, you need tooensure that you have JDK 1.8 and Gradle installed.</span></span> <span data-ttu-id="64e1a-112">Se ainda não estiver instalado, você poderá executar Olá seguintes tooinstall JDK 1.8 (openjdk-8-jdk) e Gradle -</span><span class="sxs-lookup"><span data-stu-id="64e1a-112">If not yet installed, you can run hello following tooinstall JDK 1.8 (openjdk-8-jdk) and Gradle -</span></span>

 ```bash
 sudo apt-get install openjdk-8-jdk-headless
 sudo apt-get install gradle
 ```
4. <span data-ttu-id="64e1a-113">Scripts de instalação/desinstalação Olá atualização de seu aplicativo toouse Olá nova CLI de malha de serviço Olá etapas mencionadas [aqui](service-fabric-application-lifecycle-sfctl.md).</span><span class="sxs-lookup"><span data-stu-id="64e1a-113">Update hello install/uninstall scripts of your application toouse hello new Service Fabric CLI following hello steps mentioned [here](service-fabric-application-lifecycle-sfctl.md).</span></span> <span data-ttu-id="64e1a-114">Você pode se referir a introdução de tooour [exemplos](https://github.com/Azure-Samples/service-fabric-java-getting-started) para referência.</span><span class="sxs-lookup"><span data-stu-id="64e1a-114">You can refer tooour getting-started [examples](https://github.com/Azure-Samples/service-fabric-java-getting-started) for reference.</span></span>

>[!TIP]
> <span data-ttu-id="64e1a-115">Após a desinstalação Olá SDK de Java do Service Fabric, Yeoman não funcionará.</span><span class="sxs-lookup"><span data-stu-id="64e1a-115">After uninstalling hello Service Fabric Java SDK, Yeoman will not work.</span></span> <span data-ttu-id="64e1a-116">Siga Olá pré-requisitos mencionados [aqui](service-fabric-create-your-first-linux-application-with-java.md) toohave Yeoman de malha do serviço Java gerador de modelo para cima e funcionando.</span><span class="sxs-lookup"><span data-stu-id="64e1a-116">Follow hello Prerequisites mentioned [here](service-fabric-create-your-first-linux-application-with-java.md) toohave Service Fabric Yeoman Java template generator up and working.</span></span>

## <a name="service-fabric-java-libraries-on-maven"></a><span data-ttu-id="64e1a-117">Bibliotecas Java do Service Fabric no Maven</span><span class="sxs-lookup"><span data-stu-id="64e1a-117">Service Fabric Java libraries on Maven</span></span>
<span data-ttu-id="64e1a-118">As bibliotecas Java do Service Fabric foram hospedadas no Maven.</span><span class="sxs-lookup"><span data-stu-id="64e1a-118">Service Fabric Java libraries have been hosted in Maven.</span></span> <span data-ttu-id="64e1a-119">Você pode adicionar dependências Olá Olá ``pom.xml`` ou ``build.gradle`` de bibliotecas do Java de malha do serviço de toouse projetos do **mavenCentral**.</span><span class="sxs-lookup"><span data-stu-id="64e1a-119">You can add hello dependencies in hello ``pom.xml`` or ``build.gradle`` of your projects toouse Service Fabric Java libraries from **mavenCentral**.</span></span>

### <a name="actors"></a><span data-ttu-id="64e1a-120">Atores</span><span class="sxs-lookup"><span data-stu-id="64e1a-120">Actors</span></span>

<span data-ttu-id="64e1a-121">Suporte Reliable Actor do Service Fabric para seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="64e1a-121">Service Fabric Reliable Actor support for your application.</span></span>

  ```XML
  <dependency>
      <groupId>com.microsoft.servicefabric</groupId>
      <artifactId>sf-actors-preview</artifactId>
      <version>0.10.0</version>
  </dependency>
  ```

  ```gradle
  repositories {
      mavenCentral()
  }
  dependencies {
      compile 'com.microsoft.servicefabric:sf-actors-preview:0.10.0'
  }
  ```

### <a name="services"></a><span data-ttu-id="64e1a-122">Serviços</span><span class="sxs-lookup"><span data-stu-id="64e1a-122">Services</span></span>

<span data-ttu-id="64e1a-123">Suporte do Serviço sem Estado do Service Fabric para seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="64e1a-123">Service Fabric Stateless Service support for your application.</span></span>

  ```XML
  <dependency>
      <groupId>com.microsoft.servicefabric</groupId>
      <artifactId>sf-services-preview</artifactId>
      <version>0.10.0</version>
  </dependency>
  ```

  ```gradle
  repositories {
      mavenCentral()
  }
  dependencies {
      compile 'com.microsoft.servicefabric:sf-services-preview:0.10.0'
  }
  ```

### <a name="others"></a><span data-ttu-id="64e1a-124">Outros</span><span class="sxs-lookup"><span data-stu-id="64e1a-124">Others</span></span>
#### <a name="transport"></a><span data-ttu-id="64e1a-125">Transporte</span><span class="sxs-lookup"><span data-stu-id="64e1a-125">Transport</span></span>

<span data-ttu-id="64e1a-126">Suporte da camada de transporte para aplicativo Java do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="64e1a-126">Transport layer support for Service Fabric Java application.</span></span> <span data-ttu-id="64e1a-127">Você não precisa tooexplicitly adicionar essa dependência tooyour Reliable Actor ou aplicativos de serviço, a menos que o programa na camada de transporte hello.</span><span class="sxs-lookup"><span data-stu-id="64e1a-127">You do not need tooexplicitly add this dependency tooyour Reliable Actor or Service applications, unless you program at hello transport layer.</span></span>

  ```XML
  <dependency>
      <groupId>com.microsoft.servicefabric</groupId>
      <artifactId>sf-transport-preview</artifactId>
      <version>0.10.0</version>
  </dependency>
  ```

  ```gradle
  repositories {
      mavenCentral()
  }
  dependencies {
      compile 'com.microsoft.servicefabric:sf-transport-preview:0.10.0'
  }
  ```

#### <a name="fabric-support"></a><span data-ttu-id="64e1a-128">Suporte do Fabric</span><span class="sxs-lookup"><span data-stu-id="64e1a-128">Fabric support</span></span>

<span data-ttu-id="64e1a-129">Suporte ao nível do sistema para o serviço de malha, que fala toonative Service Fabric runtime.</span><span class="sxs-lookup"><span data-stu-id="64e1a-129">System level support for Service Fabric, which talks toonative Service Fabric runtime.</span></span> <span data-ttu-id="64e1a-130">Você não precisa tooexplicitly adicionar essa dependência tooyour Reliable Actor ou aplicativos de serviço.</span><span class="sxs-lookup"><span data-stu-id="64e1a-130">You do not need tooexplicitly add this dependency tooyour Reliable Actor or Service applications.</span></span> <span data-ttu-id="64e1a-131">Isso é buscado automaticamente do Maven, quando você incluir Olá outras dependências acima.</span><span class="sxs-lookup"><span data-stu-id="64e1a-131">This gets fetched automatically from Maven, when you include hello other dependencies above.</span></span>

  ```XML
  <dependency>
      <groupId>com.microsoft.servicefabric</groupId>
      <artifactId>sf-preview</artifactId>
      <version>0.10.0</version>
  </dependency>
  ```

  ```gradle
  repositories {
      mavenCentral()
  }
  dependencies {
      compile 'com.microsoft.servicefabric:sf-preview:0.10.0'
  }
  ```


## <a name="migrating-service-fabric-stateless-service"></a><span data-ttu-id="64e1a-132">Migrar Serviço sem Estado do Service Fabric</span><span class="sxs-lookup"><span data-stu-id="64e1a-132">Migrating Service Fabric Stateless Service</span></span>

<span data-ttu-id="64e1a-133">toobe toobuild capaz de sua malha do serviço sem monitoração de estado Java serviço existente usando dependências do Service Fabric buscadas no Maven, você precisa Olá tooupdate ``build.gradle`` arquivo hello serviço.</span><span class="sxs-lookup"><span data-stu-id="64e1a-133">toobe able toobuild your existing Service Fabric stateless Java service using Service Fabric dependencies fetched from Maven, you need tooupdate hello ``build.gradle`` file inside hello Service.</span></span> <span data-ttu-id="64e1a-134">Ele usava toobe como as seguintes:</span><span class="sxs-lookup"><span data-stu-id="64e1a-134">Previously it used toobe like as follows -</span></span>
```
dependencies {
    compile fileTree(dir: '/opt/microsoft/sdk/servicefabric/java/packages/lib', include: ['*.jar'])
    compile project(':Interface')
}
.
.
.
jar {
    manifest {
    attributes(
                'Main-Class': 'statelessservice.MyStatelessServiceHost',
                "Class-Path": configurations.compile.collect { 'lib/' + it.getName() }.join(' '))
    baseName "MyStateless"
    destinationDir = file('./../MyStatelessApplication/MyStatelessPkg/Code')
}
.
.
.
task copyDeps <<{
    copy {
        from("/opt/microsoft/sdk/servicefabric/java/packages/lib")
        into("./../MyStatelessApplication/MyStatelessPkg/Code/lib")
        include('*.jar')
    }
    copy {
        from("/opt/microsoft/sdk/servicefabric/java/packages/lib")
        into("./../MyStatelessApplication/MyStatelessPkg/Code/lib")
        include('libj*.so')
    }
}
```
<span data-ttu-id="64e1a-135">Agora, toofetch dependências de saudação do Maven, Olá **atualizado** ``build.gradle`` teria partes correspondente Olá as seguintes:</span><span class="sxs-lookup"><span data-stu-id="64e1a-135">Now, toofetch hello dependencies from Maven, hello **updated** ``build.gradle`` would have hello corresponding parts as follows -</span></span>
```
repositories {
        mavenCentral()
}

configurations {
    azuresf
}

dependencies {
    compile project(':Interface')
    azuresf ('com.microsoft.servicefabric:sf-services-preview:0.10.0')
    compile fileTree(dir: 'lib', include: '*.jar')
}

task explodeDeps(type: Copy, dependsOn:configurations.azuresf) { task ->
    configurations.azuresf.filter { it.toString().contains("native-preview") }.each{
        from zipTree(it)
    }
    configurations.azuresf.filter { !it.toString().contains("native-preview") }.each {
        from it
    }
    into "lib"
    include "libj*.so", "*.jar"
}

compileJava.dependsOn(explodeDeps)
.
.
.
jar {
    manifest {
        def mpath = configurations.compile.collect {'lib/'+it.getName()}.join (' ')
        mpath = mpath + ' ' + configurations.azuresf.collect {'lib/'+it.getName()}.join (' ')
        attributes(
                'Main-Class': 'statelessservice.MyStatelessServiceHost',
                "Class-Path": mpath)
    baseName "MyStateless"
    destinationDir = file('./../MyStatelessApplication/MyStatelessPkg/Code')
   }
}
.
.
.
task copyDeps <<{
    copy {
        from("lib/")
        into("./../MyStatelessApplication/MyStatelessPkg/Code/lib")
        include('*')
    }
}
```
<span data-ttu-id="64e1a-136">Em geral, tooget uma ideia geral sobre como o script de construção Olá seria semelhante para um serviço de Java do Service Fabric sem monitoração de estado, você pode fazer referência tooany exemplo nossos exemplos de guia de Introdução.</span><span class="sxs-lookup"><span data-stu-id="64e1a-136">In general, tooget an overall idea about how hello build script would look like for a Service Fabric stateless Java service, you can refer tooany sample from our getting-started examples.</span></span> <span data-ttu-id="64e1a-137">Aqui está a saudação [gradle](https://github.com/Azure-Samples/service-fabric-java-getting-started/blob/master/Services/EchoServer/EchoServer1.0/EchoServerService/build.gradle) para exemplo de EchoServer hello.</span><span class="sxs-lookup"><span data-stu-id="64e1a-137">Here is hello [build.gradle](https://github.com/Azure-Samples/service-fabric-java-getting-started/blob/master/Services/EchoServer/EchoServer1.0/EchoServerService/build.gradle) for hello EchoServer sample.</span></span>

## <a name="migrating-service-fabric-actor-service"></a><span data-ttu-id="64e1a-138">Migrar Serviço de Ator do Service Fabric</span><span class="sxs-lookup"><span data-stu-id="64e1a-138">Migrating Service Fabric Actor Service</span></span>

<span data-ttu-id="64e1a-139">toobe toobuild capaz de seu aplicativo Java de ator do Service Fabric existente usando as dependências do Service Fabric buscadas no Maven, você precisa Olá tooupdate ``build.gradle`` arquivo dentro do pacote de interface de saudação e no pacote de serviço hello.</span><span class="sxs-lookup"><span data-stu-id="64e1a-139">toobe able toobuild your existing Service Fabric Actor Java application using Service Fabric dependencies fetched from Maven, you need tooupdate hello ``build.gradle`` file inside hello interface package and in hello Service package.</span></span> <span data-ttu-id="64e1a-140">Se você tiver um pacote TestClient, será necessário tooupdate que também.</span><span class="sxs-lookup"><span data-stu-id="64e1a-140">If you have a TestClient package, you need tooupdate that as well.</span></span> <span data-ttu-id="64e1a-141">Portanto, em seu ator ``Myactor``, seguinte Olá seria locais de saudação que precisam tooupdate -</span><span class="sxs-lookup"><span data-stu-id="64e1a-141">So, for your actor ``Myactor``, hello following would be hello places where you need tooupdate -</span></span>
```
./Myactor/build.gradle
./MyactorInterface/build.gradle
./MyactorTestClient/build.gradle
```

#### <a name="updating-build-script-for-hello-interface-project"></a><span data-ttu-id="64e1a-142">Atualizando o script de compilação de projeto de interface de saudação</span><span class="sxs-lookup"><span data-stu-id="64e1a-142">Updating build script for hello interface project</span></span>

<span data-ttu-id="64e1a-143">Ele usava toobe como as seguintes:</span><span class="sxs-lookup"><span data-stu-id="64e1a-143">Previously it used toobe like as follows -</span></span>
```
dependencies {
    compile fileTree(dir: '/opt/microsoft/sdk/servicefabric/java/packages/lib', include: ['*.jar'])
}
.
.
```
<span data-ttu-id="64e1a-144">Agora, toofetch dependências de saudação do Maven, Olá **atualizado** ``build.gradle`` teria partes correspondente Olá as seguintes:</span><span class="sxs-lookup"><span data-stu-id="64e1a-144">Now, toofetch hello dependencies from Maven, hello **updated** ``build.gradle`` would have hello corresponding parts as follows -</span></span>
```
repositories {
    mavenCentral()
}

configurations {
    azuresf
}

dependencies {
    azuresf ('com.microsoft.servicefabric:sf-actors-preview:0.10.0')
    compile fileTree(dir: 'lib', include: '*.jar')
}

task explodeDeps(type: Copy, dependsOn:configurations.azuresf) { task ->
    configurations.azuresf.filter { it.toString().contains("native-preview") }.each{
        from zipTree(it)
    }
    configurations.azuresf.filter { !it.toString().contains("native-preview") }.each {
        from it
    }
    into "lib"
    include "libj*.so", "*.jar"
}

compileJava.dependsOn(explodeDeps)
.
.
```

#### <a name="updating-build-script-for-hello-actor-project"></a><span data-ttu-id="64e1a-145">Atualizando o script de compilação de projeto de ator Olá</span><span class="sxs-lookup"><span data-stu-id="64e1a-145">Updating build script for hello actor project</span></span>

<span data-ttu-id="64e1a-146">Ele usava toobe como as seguintes:</span><span class="sxs-lookup"><span data-stu-id="64e1a-146">Previously it used toobe like as follows -</span></span>
```
dependencies {
    compile fileTree(dir: '/opt/microsoft/sdk/servicefabric/java/packages/lib', include: ['*.jar'])
    compile project(':MyactorInterface')
}
.
.
.
jar {
    manifest {
    attributes(
                'Main-Class': 'reliableactor.MyactorHost',
                "Class-Path": configurations.compile.collect { 'lib/' + it.getName() }.join(' '))
      baseName "myactor"
    destinationDir = file('./../myjavaapp/MyactorPkg/Code')
    }
}
.
.
.
task copyDeps<< {
    copy {
        from("/opt/microsoft/sdk/servicefabric/java/packages/lib")
        into("./../myjavaapp/MyactorPkg/Code/lib")
        include('*.jar')
    }
    copy {
        from("/opt/microsoft/sdk/servicefabric/java/packages/lib")
        into("./../myjavaapp/MyactorPkg/Code/lib")
        include('libj*.so')
    }
    copy {
        from("../MyactorInterface/out/lib")
        into("./../myjavaapp/MyactorPkg/Code/lib")
        include('*.jar')
    }
}
```
<span data-ttu-id="64e1a-147">Agora, toofetch dependências de saudação do Maven, Olá **atualizado** ``build.gradle`` teria partes correspondente Olá as seguintes:</span><span class="sxs-lookup"><span data-stu-id="64e1a-147">Now, toofetch hello dependencies from Maven, hello **updated** ``build.gradle`` would have hello corresponding parts as follows -</span></span>
```
repositories {
    mavenCentral()
}

configurations {
    azuresf
}

dependencies {
    compile project(':MyactorInterface')
    azuresf ('com.microsoft.servicefabric:sf-actors-preview:0.10.0')
    compile fileTree(dir: 'lib', include: '*.jar')
}

task explodeDeps(type: Copy, dependsOn:configurations.azuresf) { task ->
    configurations.azuresf.filter { it.toString().contains("native-preview") }.each{
        from zipTree(it)
    }
    configurations.azuresf.filter { !it.toString().contains("native-preview") }.each {
        from it
    }
    into "lib"
    include "libj*.so", "*.jar"
}

compileJava.dependsOn(explodeDeps)
.
.
.
jar {
    manifest {
        def mpath = configurations.compile.collect {'lib/'+it.getName()}.join (' ')
        mpath = mpath + ' ' + configurations.azuresf.collect {'lib/'+it.getName()}.join (' ')
        attributes(
                'Main-Class': 'reliableactor.MyactorHost',
                "Class-Path": mpath)
    baseName "myactor"
    destinationDir = file('../myjavaapp/MyactorPkg/Code')}
 }
.
.
.
task copyDeps<< {
      copy {
              from("lib/")
              into("../myjavaapp/MyactorPkg/Code/lib")
              include('*')
      }
      copy {
              from("../MyactorInterface/out/lib")
              into("../myjavaapp/MyactorPkg/Code/lib")
              include('*.jar')
      }
}
```

#### <a name="updating-build-script-for-hello-test-client-project"></a><span data-ttu-id="64e1a-148">Atualizando o script de compilação para o projeto de cliente de teste Olá</span><span class="sxs-lookup"><span data-stu-id="64e1a-148">Updating build script for hello test client project</span></span>

<span data-ttu-id="64e1a-149">As alterações aqui são alterações toohello semelhantes discutidas na seção anterior, ou seja, projeto de ator Olá.</span><span class="sxs-lookup"><span data-stu-id="64e1a-149">Changes here are similar toohello changes discussed in previous section, that is, hello actor project.</span></span> <span data-ttu-id="64e1a-150">Olá anteriormente Gradle toobe script usado como as seguintes:</span><span class="sxs-lookup"><span data-stu-id="64e1a-150">Previously hello Gradle script used toobe like as follows -</span></span>
```
dependencies {
    compile fileTree(dir: '/opt/microsoft/sdk/servicefabric/java/packages/lib', include: ['*.jar'])
      compile project(':MyactorInterface')
}
.
.
.
jar
{
    manifest {
    attributes(
        'Main-Class': 'reliableactor.test.MyactorTestClient',
        "Class-Path": configurations.compile.collect { 'lib/' + it.getName() }.join(' '))
    }
    baseName "myactor-test"
  destinationDir = file('out/lib')
}
.
.
.
task copyDeps<< {
        copy {
                from("/opt/microsoft/sdk/servicefabric/java/packages/lib")
                into("./out/lib/lib")
                include('*.jar')
        }
        copy {
                from("/opt/microsoft/sdk/servicefabric/java/packages/lib")
                into("./out/lib/lib")
                include('libj*.so')
        }
        copy {
                from("../MyactorInterface/out/lib")
                into("./out/lib/lib")
                include('*.jar')
        }
}
```
<span data-ttu-id="64e1a-151">Agora, toofetch dependências de saudação do Maven, Olá **atualizado** ``build.gradle`` teria partes correspondente Olá as seguintes:</span><span class="sxs-lookup"><span data-stu-id="64e1a-151">Now, toofetch hello dependencies from Maven, hello **updated** ``build.gradle`` would have hello corresponding parts as follows -</span></span>
```
repositories {
    mavenCentral()
}

configurations {
    azuresf
}

dependencies {
    compile project(':MyactorInterface')
    azuresf ('com.microsoft.servicefabric:sf-actors-preview:0.10.0')
    compile fileTree(dir: 'lib', include: '*.jar')
}

task explodeDeps(type: Copy, dependsOn:configurations.azuresf) { task ->
    configurations.azuresf.filter { it.toString().contains("native-preview") }.each{
        from zipTree(it)
    }
    configurations.azuresf.filter { !it.toString().contains("native-preview") }.each {
        from it
    }
    into "lib"
    include "libj*.so", "*.jar"
}

compileJava.dependsOn(explodeDeps)
.
.
.
jar
{
    manifest {
        def mpath = configurations.compile.collect {'lib/'+it.getName()}.join (' ')
        mpath = mpath + ' ' + configurations.azuresf.collect {'lib/'+it.getName()}.join (' ')
    attributes(
                'Main-Class': 'reliableactor.test.MyactorTestClient',
                "Class-Path": mpath)
    baseName "myactor-test"
    destinationDir = file('./out/lib')
        }
}
.
.
.
task copyDeps<< {
        copy {
                from("lib/")
                into("./out/lib/lib")
                include('*')
        }
        copy {
                from("../MyactorInterface/out/lib")
                into("./out/lib/lib")
                include('*.jar')
        }
}
```

## <a name="next-steps"></a><span data-ttu-id="64e1a-152">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="64e1a-152">Next steps</span></span>

* [<span data-ttu-id="64e1a-153">Criar e implantar seu primeiro aplicativo Java do Service Fabric no Linux usando o Yeoman</span><span class="sxs-lookup"><span data-stu-id="64e1a-153">Create and deploy your first Service Fabric Java application on Linux by using Yeoman</span></span>](service-fabric-create-your-first-linux-application-with-java.md)
* [<span data-ttu-id="64e1a-154">Criar e implantar seu primeiro aplicativo Java do Service Fabric no Linux usando o plug-in Service Fabric para o Eclipse</span><span class="sxs-lookup"><span data-stu-id="64e1a-154">Create and deploy your first Service Fabric Java application on Linux by using Service Fabric Plugin for Eclipse</span></span>](service-fabric-get-started-eclipse.md)
* [<span data-ttu-id="64e1a-155">Interagir com clusters de malha do serviço usando Olá CLI de malha do serviço</span><span class="sxs-lookup"><span data-stu-id="64e1a-155">Interact with Service Fabric clusters using hello Service Fabric CLI</span></span>](service-fabric-cli.md)
