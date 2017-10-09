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
# <a name="update-your-previous-java-service-fabric-application-toofetch-java-libraries-from-maven"></a>Atualizar seu anterior Java Service Fabric application toofetch Java bibliotecas do Maven
Podemos recentemente moveu binários Java de malha do serviço de saudação SDK de Java do Service Fabric tooMaven hospedagem. Agora você pode usar **mavencentral** dependências de serviço malha Java toofetch hello mais recentes. Início rápido ajuda a atualizar seus aplicativos Java existentes, o que você criou anteriormente toobe usada com o SDK do Service Fabric Java, usando qualquer Yeoman modelo ou Eclipse, toobe compatível com hello build Maven com base.

## <a name="prerequisites"></a>Pré-requisitos
1. Primeiro é necessário toouninstall Olá existente do Java SDK.

  ```bash
  sudo dpkg -r servicefabricsdkjava
  ```
2. A seguir instalação hello mais recente CLI de malha do serviço Olá as etapas mencionadas [aqui](service-fabric-cli.md).

3. toobuild e o trabalho em aplicativos de serviço do Fabric Java Olá, é necessário tooensure que você tenha o JDK 1.8 e Gradle instalado. Se ainda não estiver instalado, você poderá executar Olá seguintes tooinstall JDK 1.8 (openjdk-8-jdk) e Gradle -

 ```bash
 sudo apt-get install openjdk-8-jdk-headless
 sudo apt-get install gradle
 ```
4. Scripts de instalação/desinstalação Olá atualização de seu aplicativo toouse Olá nova CLI de malha de serviço Olá etapas mencionadas [aqui](service-fabric-application-lifecycle-sfctl.md). Você pode se referir a introdução de tooour [exemplos](https://github.com/Azure-Samples/service-fabric-java-getting-started) para referência.

>[!TIP]
> Após a desinstalação Olá SDK de Java do Service Fabric, Yeoman não funcionará. Siga Olá pré-requisitos mencionados [aqui](service-fabric-create-your-first-linux-application-with-java.md) toohave Yeoman de malha do serviço Java gerador de modelo para cima e funcionando.

## <a name="service-fabric-java-libraries-on-maven"></a>Bibliotecas Java do Service Fabric no Maven
As bibliotecas Java do Service Fabric foram hospedadas no Maven. Você pode adicionar dependências Olá Olá ``pom.xml`` ou ``build.gradle`` de bibliotecas do Java de malha do serviço de toouse projetos do **mavenCentral**.

### <a name="actors"></a>Atores

Suporte Reliable Actor do Service Fabric para seu aplicativo.

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

### <a name="services"></a>Serviços

Suporte do Serviço sem Estado do Service Fabric para seu aplicativo.

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

### <a name="others"></a>Outros
#### <a name="transport"></a>Transporte

Suporte da camada de transporte para aplicativo Java do Service Fabric. Você não precisa tooexplicitly adicionar essa dependência tooyour Reliable Actor ou aplicativos de serviço, a menos que o programa na camada de transporte hello.

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

#### <a name="fabric-support"></a>Suporte do Fabric

Suporte ao nível do sistema para o serviço de malha, que fala toonative Service Fabric runtime. Você não precisa tooexplicitly adicionar essa dependência tooyour Reliable Actor ou aplicativos de serviço. Isso é buscado automaticamente do Maven, quando você incluir Olá outras dependências acima.

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


## <a name="migrating-service-fabric-stateless-service"></a>Migrar Serviço sem Estado do Service Fabric

toobe toobuild capaz de sua malha do serviço sem monitoração de estado Java serviço existente usando dependências do Service Fabric buscadas no Maven, você precisa Olá tooupdate ``build.gradle`` arquivo hello serviço. Ele usava toobe como as seguintes:
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
Agora, toofetch dependências de saudação do Maven, Olá **atualizado** ``build.gradle`` teria partes correspondente Olá as seguintes:
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
Em geral, tooget uma ideia geral sobre como o script de construção Olá seria semelhante para um serviço de Java do Service Fabric sem monitoração de estado, você pode fazer referência tooany exemplo nossos exemplos de guia de Introdução. Aqui está a saudação [gradle](https://github.com/Azure-Samples/service-fabric-java-getting-started/blob/master/Services/EchoServer/EchoServer1.0/EchoServerService/build.gradle) para exemplo de EchoServer hello.

## <a name="migrating-service-fabric-actor-service"></a>Migrar Serviço de Ator do Service Fabric

toobe toobuild capaz de seu aplicativo Java de ator do Service Fabric existente usando as dependências do Service Fabric buscadas no Maven, você precisa Olá tooupdate ``build.gradle`` arquivo dentro do pacote de interface de saudação e no pacote de serviço hello. Se você tiver um pacote TestClient, será necessário tooupdate que também. Portanto, em seu ator ``Myactor``, seguinte Olá seria locais de saudação que precisam tooupdate -
```
./Myactor/build.gradle
./MyactorInterface/build.gradle
./MyactorTestClient/build.gradle
```

#### <a name="updating-build-script-for-hello-interface-project"></a>Atualizando o script de compilação de projeto de interface de saudação

Ele usava toobe como as seguintes:
```
dependencies {
    compile fileTree(dir: '/opt/microsoft/sdk/servicefabric/java/packages/lib', include: ['*.jar'])
}
.
.
```
Agora, toofetch dependências de saudação do Maven, Olá **atualizado** ``build.gradle`` teria partes correspondente Olá as seguintes:
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

#### <a name="updating-build-script-for-hello-actor-project"></a>Atualizando o script de compilação de projeto de ator Olá

Ele usava toobe como as seguintes:
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
Agora, toofetch dependências de saudação do Maven, Olá **atualizado** ``build.gradle`` teria partes correspondente Olá as seguintes:
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

#### <a name="updating-build-script-for-hello-test-client-project"></a>Atualizando o script de compilação para o projeto de cliente de teste Olá

As alterações aqui são alterações toohello semelhantes discutidas na seção anterior, ou seja, projeto de ator Olá. Olá anteriormente Gradle toobe script usado como as seguintes:
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
Agora, toofetch dependências de saudação do Maven, Olá **atualizado** ``build.gradle`` teria partes correspondente Olá as seguintes:
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

## <a name="next-steps"></a>Próximas etapas

* [Criar e implantar seu primeiro aplicativo Java do Service Fabric no Linux usando o Yeoman](service-fabric-create-your-first-linux-application-with-java.md)
* [Criar e implantar seu primeiro aplicativo Java do Service Fabric no Linux usando o plug-in Service Fabric para o Eclipse](service-fabric-get-started-eclipse.md)
* [Interagir com clusters de malha do serviço usando Olá CLI de malha do serviço](service-fabric-cli.md)
