---
title: Migrar do Java SDK para Maven - Atualizar Aplicativos Java do Azure Service Fabric antigos para usar Maven | Microsoft Docs
description: "Atualize aplicativos Java mais antigos que costumavam usar o SDK de Java do Service Fabric para buscar as dependências de Java do Service Fabric do Maven. Depois de concluir esta instalação, os seus aplicativos Java mais antigos poderiam ser compilados."
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
ms.openlocfilehash: 2123c5f26d77045bd22af56a844fdbf222930e7b
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="update-your-previous-java-service-fabric-application-to-fetch-java-libraries-from-maven"></a><span data-ttu-id="7cbfa-104">Atualize seu aplicativo Java de Service Fabric anterior para buscar bibliotecas Java do Maven</span><span class="sxs-lookup"><span data-stu-id="7cbfa-104">Update your previous Java Service Fabric application to fetch Java libraries from Maven</span></span>
<span data-ttu-id="7cbfa-105">Recentemente, movemos os binários de Java do Service Fabric do SDK de Java do Service Fabric para hospedagem do Maven.</span><span class="sxs-lookup"><span data-stu-id="7cbfa-105">We have recently moved Service Fabric Java binaries from the Service Fabric Java SDK to Maven hosting.</span></span> <span data-ttu-id="7cbfa-106">Agora você pode usar **mavencentral** para buscar as dependências mais recentes de Java do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="7cbfa-106">Now you can use **mavencentral** to fetch the latest Service Fabric Java dependencies.</span></span> <span data-ttu-id="7cbfa-107">Esse início rápido o ajuda a atualizar seus aplicativos Java existentes, que você criou anteriormente para ser usado com o SDK de Java do Service Fabric, usando qualquer modelo Yeoman ou Eclipse, para ser compatível com a compilação baseada em Maven.</span><span class="sxs-lookup"><span data-stu-id="7cbfa-107">This quick-start helps you update your existing Java applications, which you earlier created to be used with Service Fabric Java SDK, using either Yeoman template or Eclipse, to be compatible with the Maven based build.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7cbfa-108">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="7cbfa-108">Prerequisites</span></span>
1. <span data-ttu-id="7cbfa-109">Primeiro você precisa desinstalar o SDK de Java existente.</span><span class="sxs-lookup"><span data-stu-id="7cbfa-109">First you need to uninstall the existing Java SDK.</span></span>

  ```bash
  sudo dpkg -r servicefabricsdkjava
  ```
2. <span data-ttu-id="7cbfa-110">Instale a CLI do Service Fabric mais recente seguindo as etapas mencionadas [aqui](service-fabric-cli.md).</span><span class="sxs-lookup"><span data-stu-id="7cbfa-110">Install the latest Service Fabric CLI following the steps mentioned [here](service-fabric-cli.md).</span></span>

3. <span data-ttu-id="7cbfa-111">Para criar e trabalhar nos aplicativos Java do Service Fabric, você precisa ter o JDK 1.8 e o Gradle instalados.</span><span class="sxs-lookup"><span data-stu-id="7cbfa-111">To build and work on the Service Fabric Java applications, you need to ensure that you have JDK 1.8 and Gradle installed.</span></span> <span data-ttu-id="7cbfa-112">Se ainda não instalou, poderá executar o seguinte para instalar o JDK 1.8 (openjdk-8-jdk) e o Gradle -</span><span class="sxs-lookup"><span data-stu-id="7cbfa-112">If not yet installed, you can run the following to install JDK 1.8 (openjdk-8-jdk) and Gradle -</span></span>

 ```bash
 sudo apt-get install openjdk-8-jdk-headless
 sudo apt-get install gradle
 ```
4. <span data-ttu-id="7cbfa-113">Atualizar os scripts de instalação/desinstalação do seu aplicativo para usar a CLI do novo Service Fabric seguindo as etapas mencionadas [aqui](service-fabric-application-lifecycle-sfctl.md).</span><span class="sxs-lookup"><span data-stu-id="7cbfa-113">Update the install/uninstall scripts of your application to use the new Service Fabric CLI following the steps mentioned [here](service-fabric-application-lifecycle-sfctl.md).</span></span> <span data-ttu-id="7cbfa-114">Você pode consultar os nossos [exemplos](https://github.com/Azure-Samples/service-fabric-java-getting-started) de introdução para referência.</span><span class="sxs-lookup"><span data-stu-id="7cbfa-114">You can refer to our getting-started [examples](https://github.com/Azure-Samples/service-fabric-java-getting-started) for reference.</span></span>

>[!TIP]
> <span data-ttu-id="7cbfa-115">Depois de desinstalar o SDK de Java do Service Fabric, o Yeoman não funcionará.</span><span class="sxs-lookup"><span data-stu-id="7cbfa-115">After uninstalling the Service Fabric Java SDK, Yeoman will not work.</span></span> <span data-ttu-id="7cbfa-116">Siga os pré-requisitos mencionados [aqui](service-fabric-create-your-first-linux-application-with-java.md) para que o gerador de modelos de Java Yeoman do Service Fabric funcione.</span><span class="sxs-lookup"><span data-stu-id="7cbfa-116">Follow the Prerequisites mentioned [here](service-fabric-create-your-first-linux-application-with-java.md) to have Service Fabric Yeoman Java template generator up and working.</span></span>

## <a name="service-fabric-java-libraries-on-maven"></a><span data-ttu-id="7cbfa-117">Bibliotecas Java do Service Fabric no Maven</span><span class="sxs-lookup"><span data-stu-id="7cbfa-117">Service Fabric Java libraries on Maven</span></span>
<span data-ttu-id="7cbfa-118">As bibliotecas Java do Service Fabric foram hospedadas no Maven.</span><span class="sxs-lookup"><span data-stu-id="7cbfa-118">Service Fabric Java libraries have been hosted in Maven.</span></span> <span data-ttu-id="7cbfa-119">Você pode adicionar as dependências no ``pom.xml`` ou no ``build.gradle`` de seus projetos para usar as bibliotecas Java do Service Fabric no **mavenCentral**.</span><span class="sxs-lookup"><span data-stu-id="7cbfa-119">You can add the dependencies in the ``pom.xml`` or ``build.gradle`` of your projects to use Service Fabric Java libraries from **mavenCentral**.</span></span>

### <a name="actors"></a><span data-ttu-id="7cbfa-120">Atores</span><span class="sxs-lookup"><span data-stu-id="7cbfa-120">Actors</span></span>

<span data-ttu-id="7cbfa-121">Suporte Reliable Actor do Service Fabric para seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="7cbfa-121">Service Fabric Reliable Actor support for your application.</span></span>

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

### <a name="services"></a><span data-ttu-id="7cbfa-122">Serviços</span><span class="sxs-lookup"><span data-stu-id="7cbfa-122">Services</span></span>

<span data-ttu-id="7cbfa-123">Suporte do Serviço sem Estado do Service Fabric para seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="7cbfa-123">Service Fabric Stateless Service support for your application.</span></span>

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

### <a name="others"></a><span data-ttu-id="7cbfa-124">Outros</span><span class="sxs-lookup"><span data-stu-id="7cbfa-124">Others</span></span>
#### <a name="transport"></a><span data-ttu-id="7cbfa-125">Transporte</span><span class="sxs-lookup"><span data-stu-id="7cbfa-125">Transport</span></span>

<span data-ttu-id="7cbfa-126">Suporte da camada de transporte para aplicativo Java do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="7cbfa-126">Transport layer support for Service Fabric Java application.</span></span> <span data-ttu-id="7cbfa-127">Você não precisa adicionar explicitamente essa dependência aos seus aplicativos Reliable Actor ou Service, a menos que programe na camada de transporte.</span><span class="sxs-lookup"><span data-stu-id="7cbfa-127">You do not need to explicitly add this dependency to your Reliable Actor or Service applications, unless you program at the transport layer.</span></span>

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

#### <a name="fabric-support"></a><span data-ttu-id="7cbfa-128">Suporte do Fabric</span><span class="sxs-lookup"><span data-stu-id="7cbfa-128">Fabric support</span></span>

<span data-ttu-id="7cbfa-129">Suporte no nível do sistema para o Service Fabric, que se comunica com a execução nativa do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="7cbfa-129">System level support for Service Fabric, which talks to native Service Fabric runtime.</span></span> <span data-ttu-id="7cbfa-130">Você não precisa adicionar explicitamente essa dependência aos seus aplicativos Reliable Actor ou Service.</span><span class="sxs-lookup"><span data-stu-id="7cbfa-130">You do not need to explicitly add this dependency to your Reliable Actor or Service applications.</span></span> <span data-ttu-id="7cbfa-131">Isso é conseguido automaticamente no Maven, quando você inclui as outras dependências acima.</span><span class="sxs-lookup"><span data-stu-id="7cbfa-131">This gets fetched automatically from Maven, when you include the other dependencies above.</span></span>

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


## <a name="migrating-service-fabric-stateless-service"></a><span data-ttu-id="7cbfa-132">Migrar Serviço sem Estado do Service Fabric</span><span class="sxs-lookup"><span data-stu-id="7cbfa-132">Migrating Service Fabric Stateless Service</span></span>

<span data-ttu-id="7cbfa-133">Para ser capaz de criar seu serviço Java sem estado do Service Fabric existente usando as dependências do Service Fabric buscadas no Maven, você precisa atualizar o arquivo ``build.gradle`` dentro do Service.</span><span class="sxs-lookup"><span data-stu-id="7cbfa-133">To be able to build your existing Service Fabric stateless Java service using Service Fabric dependencies fetched from Maven, you need to update the ``build.gradle`` file inside the Service.</span></span> <span data-ttu-id="7cbfa-134">Anteriormente ele funcionava da seguinte forma -</span><span class="sxs-lookup"><span data-stu-id="7cbfa-134">Previously it used to be like as follows -</span></span>
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
<span data-ttu-id="7cbfa-135">Agora, ao buscar as dependências do Maven, o ``build.gradle`` **atualizado** teria as partes correspondentes conforme a seguir -</span><span class="sxs-lookup"><span data-stu-id="7cbfa-135">Now, to fetch the dependencies from Maven, the **updated** ``build.gradle`` would have the corresponding parts as follows -</span></span>
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
<span data-ttu-id="7cbfa-136">Em geral, para obter uma ideia geral sobre como o script de compilação seria semelhante para um serviço de Java sem estado do Service Fabric, você pode consultar qualquer um dos nossos exemplos de introdução.</span><span class="sxs-lookup"><span data-stu-id="7cbfa-136">In general, to get an overall idea about how the build script would look like for a Service Fabric stateless Java service, you can refer to any sample from our getting-started examples.</span></span> <span data-ttu-id="7cbfa-137">Aqui está o [gradle](https://github.com/Azure-Samples/service-fabric-java-getting-started/blob/master/Services/EchoServer/EchoServer1.0/EchoServerService/build.gradle) para o exemplo EchoServer.</span><span class="sxs-lookup"><span data-stu-id="7cbfa-137">Here is the [build.gradle](https://github.com/Azure-Samples/service-fabric-java-getting-started/blob/master/Services/EchoServer/EchoServer1.0/EchoServerService/build.gradle) for the EchoServer sample.</span></span>

## <a name="migrating-service-fabric-actor-service"></a><span data-ttu-id="7cbfa-138">Migrar Serviço de Ator do Service Fabric</span><span class="sxs-lookup"><span data-stu-id="7cbfa-138">Migrating Service Fabric Actor Service</span></span>

<span data-ttu-id="7cbfa-139">Para ser capaz de criar seu aplicativo Java do Ator do Service Fabric existente usando as dependências do Service Fabric buscadas no Maven, você precisa atualizar o arquivo ``build.gradle`` dentro do pacote de interface e no pacote do Service.</span><span class="sxs-lookup"><span data-stu-id="7cbfa-139">To be able to build your existing Service Fabric Actor Java application using Service Fabric dependencies fetched from Maven, you need to update the ``build.gradle`` file inside the interface package and in the Service package.</span></span> <span data-ttu-id="7cbfa-140">Se você tiver um pacote TestClient, você precisa atualizar ele também.</span><span class="sxs-lookup"><span data-stu-id="7cbfa-140">If you have a TestClient package, you need to update that as well.</span></span> <span data-ttu-id="7cbfa-141">Portanto, para o seu ator ``Myactor``, os lugares que você precisaria atualizar seriam os seguintes -</span><span class="sxs-lookup"><span data-stu-id="7cbfa-141">So, for your actor ``Myactor``, the following would be the places where you need to update -</span></span>
```
./Myactor/build.gradle
./MyactorInterface/build.gradle
./MyactorTestClient/build.gradle
```

#### <a name="updating-build-script-for-the-interface-project"></a><span data-ttu-id="7cbfa-142">Atualizar o script de compilação para o projeto de interface</span><span class="sxs-lookup"><span data-stu-id="7cbfa-142">Updating build script for the interface project</span></span>

<span data-ttu-id="7cbfa-143">Anteriormente ele funcionava da seguinte forma -</span><span class="sxs-lookup"><span data-stu-id="7cbfa-143">Previously it used to be like as follows -</span></span>
```
dependencies {
    compile fileTree(dir: '/opt/microsoft/sdk/servicefabric/java/packages/lib', include: ['*.jar'])
}
.
.
```
<span data-ttu-id="7cbfa-144">Agora, ao buscar as dependências do Maven, o ``build.gradle`` **atualizado** teria as partes correspondentes conforme a seguir -</span><span class="sxs-lookup"><span data-stu-id="7cbfa-144">Now, to fetch the dependencies from Maven, the **updated** ``build.gradle`` would have the corresponding parts as follows -</span></span>
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

#### <a name="updating-build-script-for-the-actor-project"></a><span data-ttu-id="7cbfa-145">Atualizar o script de compilação para o projeto do ator</span><span class="sxs-lookup"><span data-stu-id="7cbfa-145">Updating build script for the actor project</span></span>

<span data-ttu-id="7cbfa-146">Anteriormente ele funcionava da seguinte forma -</span><span class="sxs-lookup"><span data-stu-id="7cbfa-146">Previously it used to be like as follows -</span></span>
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
<span data-ttu-id="7cbfa-147">Agora, ao buscar as dependências do Maven, o ``build.gradle`` **atualizado** teria as partes correspondentes conforme a seguir -</span><span class="sxs-lookup"><span data-stu-id="7cbfa-147">Now, to fetch the dependencies from Maven, the **updated** ``build.gradle`` would have the corresponding parts as follows -</span></span>
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

#### <a name="updating-build-script-for-the-test-client-project"></a><span data-ttu-id="7cbfa-148">Atualizar o script de compilação para o projeto do cliente de teste</span><span class="sxs-lookup"><span data-stu-id="7cbfa-148">Updating build script for the test client project</span></span>

<span data-ttu-id="7cbfa-149">As alterações aqui são semelhantes às alterações discutidas na seção anterior, ou seja, o projeto de ator.</span><span class="sxs-lookup"><span data-stu-id="7cbfa-149">Changes here are similar to the changes discussed in previous section, that is, the actor project.</span></span> <span data-ttu-id="7cbfa-150">Anteriormente, o script de Gradle era da seguinte forma -</span><span class="sxs-lookup"><span data-stu-id="7cbfa-150">Previously the Gradle script used to be like as follows -</span></span>
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
<span data-ttu-id="7cbfa-151">Agora, ao buscar as dependências do Maven, o ``build.gradle`` **atualizado** teria as partes correspondentes conforme a seguir -</span><span class="sxs-lookup"><span data-stu-id="7cbfa-151">Now, to fetch the dependencies from Maven, the **updated** ``build.gradle`` would have the corresponding parts as follows -</span></span>
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

## <a name="next-steps"></a><span data-ttu-id="7cbfa-152">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="7cbfa-152">Next steps</span></span>

* [<span data-ttu-id="7cbfa-153">Criar e implantar seu primeiro aplicativo Java do Service Fabric no Linux usando o Yeoman</span><span class="sxs-lookup"><span data-stu-id="7cbfa-153">Create and deploy your first Service Fabric Java application on Linux by using Yeoman</span></span>](service-fabric-create-your-first-linux-application-with-java.md)
* [<span data-ttu-id="7cbfa-154">Criar e implantar seu primeiro aplicativo Java do Service Fabric no Linux usando o plug-in Service Fabric para o Eclipse</span><span class="sxs-lookup"><span data-stu-id="7cbfa-154">Create and deploy your first Service Fabric Java application on Linux by using Service Fabric Plugin for Eclipse</span></span>](service-fabric-get-started-eclipse.md)
* [<span data-ttu-id="7cbfa-155">Interagir com os clusters do Service Fabric usando a CLI do Service Fabric</span><span class="sxs-lookup"><span data-stu-id="7cbfa-155">Interact with Service Fabric clusters using the Service Fabric CLI</span></span>](service-fabric-cli.md)
