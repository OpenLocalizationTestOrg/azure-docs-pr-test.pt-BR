---
title: "aaaDeploy um tooAzure executável existente do Service Fabric | Microsoft Docs"
description: "Passo a passo sobre como toopackage um aplicativo existente como um executável de convidado, para que ele possa ser implantado cluster do Service Fabric tooa"
services: service-fabric
documentationcenter: .net
author: msfussell
manager: timlt
editor: 
ms.assetid: d799c1c6-75eb-4b8a-9f94-bf4f3dadf4c3
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 07/02/2017
ms.author: mfussell;mikhegn
ms.openlocfilehash: 5599802bdb6bda2407a138d77e12148ccb64f437
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-guest-executable-tooservice-fabric"></a>Implantar um tooService executável de convidado malha
Você pode executar qualquer tipo de código, como Node.js, Java ou C++ no Service Fabric como um serviço. Service Fabric se refere a tipos de toothese de serviços como convidado executáveis.

Os executáveis convidados são tratados pela Service Fabric como serviços sem monitoração de estado. Como resultado, eles são colocados em nós em um cluster, com base na disponibilidade e em outras métricas. Este artigo descreve como toopackage e implantar um cluster de malha do serviço de tooa executável de convidado, usando o Visual Studio ou um utilitário de linha de comando.

Neste artigo, vamos abranger Olá etapas toopackage um executável de convidado e implantá-lo tooService malha.  

## <a name="benefits-of-running-a-guest-executable-in-service-fabric"></a>Benefícios de executar um executável convidado no Service Fabric
Há várias toorunning de vantagens convidado executável em um cluster do Service Fabric:

* Alta disponibilidade. Os aplicativos que são executados no Service Fabric estão no modo de alta disponibilidade. O Service Fabric garante que as instâncias de um aplicativo estão em execução.
* Monitoramento de integridade. O monitoramento de integridade do Service Fabric detecta se um aplicativo está em execução e fornece informações de diagnóstico se houver uma falha.   
* Gerenciamento do ciclo de vida do aplicativo. Além de fornecer atualizações sem tempo de inatividade, o Service Fabric fornece versão anterior do toohello de reversão automática se houver um evento de integridade inválido relatado durante uma atualização.    
* Densidade. Você pode executar vários aplicativos em um cluster, o que elimina a necessidade de saudação de toorun cada aplicativo em seu próprio hardware.
* Descoberta: Usando REST você pode chamar toofind de serviço de nomeação de malha do serviço Olá outros serviços em cluster hello. 

## <a name="samples"></a>Exemplos
* [Exemplo de empacotamento e implantação de um executável convidado](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started)
* [Exemplo de dois convidado executáveis (c# e nodejs) se comunicar por meio do serviço de nomenclatura hello usando REST](https://github.com/Azure-Samples/service-fabric-dotnet-containers)

## <a name="overview-of-application-and-service-manifest-files"></a>Visão geral do aplicativo e dos arquivos de manifesto do serviço
Como parte da implantação de um executável de convidado, é útil toounderstand Olá Service Fabric modelo de pacotes e implantação conforme descrito em [modelo de aplicativo](service-fabric-application-model.md). modelo de empacotamento do Service Fabric Olá se baseia em dois arquivos XML: Olá manifestos de aplicativo e serviço. Olá definição de esquema para hello arquivos ApplicationManifest.xml e ServiceManifest.xml é instalado com hello no SDK do Service Fabric *C:\Program Files\Microsoft SDKs\Service Fabric\schemas\ServiceFabricServiceModel.xsd*.

* **O manifesto do aplicativo** o manifesto do aplicativo hello é usado toodescribe Olá aplicativo. Lista serviços Olá que compõem a ele e outros parâmetros que são usado toodefine devem ser implantados como um ou mais serviços, como número de saudação de instâncias.

  No Service Fabric, um aplicativo é uma unidade de implantação e atualização. Um aplicativo pode ser atualizado como uma única unidade em que falhas e reversões potencias são gerenciadas. Service Fabric garante que o processo de atualização Olá seja bem-sucedida, ou se Olá atualização falhar, não deixe aplicativo hello em um estado instável ou desconhecido.
* **Manifesto do serviço** manifesto do serviço Olá descreve os componentes de saudação de um serviço. Ele inclui dados, como nome de saudação e tipo de serviço e seu código e configuração. Olá manifesto de serviço também inclui alguns parâmetros adicionais que podem ser usados tooconfigure serviço de saudação quando ele é implantado.

## <a name="application-package-file-structure"></a>Estrutura de arquivos do pacote de aplicativos
toodeploy tooService um aplicativo do Fabric, aplicativo hello deve seguir uma estrutura de diretório predefinidos. a seguir Olá é um exemplo de estrutura.

```
|-- ApplicationPackageRoot
    |-- GuestService1Pkg
        |-- Code
            |-- existingapp.exe
        |-- Config
            |-- Settings.xml
        |-- Data
        |-- ServiceManifest.xml
    |-- ApplicationManifest.xml
```

Olá ApplicationPackageRoot contém arquivo applicationmanifest. XML Olá que define o aplicativo hello. Um subdiretório para cada serviço incluído no aplicativo hello é usado toocontain todos Olá artefatos de serviço Olá requer. Esses subdiretórios são Olá ServiceManifest.xml e, geralmente, Olá a seguir:

* *Código*. Este diretório contém código de saudação do serviço.
* *Config*. Este diretório contém um arquivo Settings.xml (e outros arquivos, se necessário) que o serviço de saudação pode acessar no tempo de execução tooretrieve configurações específicas.
* *Dados*. Este é um diretório adicional toostore local dados adicionais que talvez seja necessário serviço hello. Dados devem ser dados apenas efêmera toostore usado. Malha do serviço faz não copiar ou replicar o diretório de dados do alterações toohello se precisar de serviço Olá toobe realocado (por exemplo, durante o failover).

> [!NOTE]
> Você não tem toocreate Olá `config` e `data` diretórios se você não precisar deles.
>
>

## <a name="package-an-existing-executable"></a>Empacotar um executável existente
Ao empacotar um executável de convidado, você pode escolher qualquer toouse um modelo de projeto do Visual Studio ou muito[criar manualmente o pacote de aplicativo hello](#manually). Usando o Visual Studio, Olá a estrutura do pacote de aplicativos e arquivos de manifesto são criados pelo novo modelo de projeto Olá para você.

> [!TIP]
> toopackage de maneira mais fácil de saudação um executável em um serviço existente do Windows é toouse Visual Studio e no Linux toouse Yeoman
>

## <a name="use-visual-studio-toopackage-and-deploy-an-existing-executable"></a>Use o Visual Studio toopackage e implantar um arquivo executável existente
O Visual Studio fornece uma estrutura de serviço toohelp de modelo de serviço é implantar um cluster do convidado tooa executável do Service Fabric.

1. Escolha **Arquivo** > **Novo Projeto** e crie um aplicativo de Service Fabric.
2. Escolha **executável de convidado** como modelo de serviço hello.
3. Clique em **procurar** tooselect pasta de saudação com o executável e preencha o restante de saudação do serviço de Olá Olá parâmetros toocreate.
   * *Comportamento do Pacote de Código*. Pode ser conjunto toocopy todo o conteúdo de saudação do toohello sua pasta projeto do Visual Studio, que é útil se Olá executável não for alterada. Se você espera toochange executável hello e desejar Olá capacidade toopick backup novas compilações dinamicamente, você pode escolher toolink toohello pasta em vez disso. Você pode usar pastas vinculadas ao criar o projeto de aplicativo hello no Visual Studio. Isso vincula o local de origem toohello do projeto Olá, possibilitando que os convidados Olá tooupdate executável em seu destino de origem. Essas atualizações se tornam parte do pacote de aplicativo hello na compilação.
   * *Programa* Especifica Olá executável que deve ser executado o serviço de saudação toostart.
   * *Argumentos* Especifica argumentos de saudação que devem ser passados toohello executável. Pode ser uma lista de parâmetros com argumentos.
   * *Pasta de trabalho* Especifica Olá a pasta de trabalho para processo de saudação que será toobe iniciado. Você pode especificar três valores:
     * `CodeBase`Especifica esse diretório de trabalho Olá vai toobe definir diretório de código toohello no pacote de aplicativo hello (`Code` directory mostrada a saudação anterior a estrutura de arquivos).
     * `CodePackage`Especifica esse diretório de trabalho Olá vai toobe definir toohello raiz do pacote de aplicativo hello (`GuestService1Pkg` mostra a saudação anterior a estrutura de arquivos).
     * `Work`Especifica que os arquivos de saudação são colocados em uma subpasta chamada de trabalho.
4. Dê um nome ao seu serviço e clique em **OK**.
5. Se seu serviço precisa de um ponto de extremidade de comunicação, agora você pode adicionar arquivos do tipo toohello ServiceManifest.xml, porta e protocolo de saudação. Por exemplo: `<Endpoint Name="NodeAppTypeEndpoint" Protocol="http" Port="3000" UriScheme="http" PathSuffix="myapp/" Type="Input" />`.
6. Agora você pode usar o pacote de saudação e publicar ação contra o cluster local, depuração Olá solução no Visual Studio. Quando estiver pronto, você pode publicar cluster remoto da saudação aplicativo tooa ou check-in de controle de toosource Olá solução.
7. Ir para o fim de toohello de toosee este artigo como tooview seu serviço executável de convidado em execução no Gerenciador do Service Fabric.

## <a name="use-yoeman-toopackage-and-deploy-an-existing-executable-on-linux"></a>Use Yoeman toopackage e implantar um executável existente no Linux

procedimento de saudação para criar e implantar um convidado executável no Linux é Olá igual ao implantar um aplicativo de java csharp.

1. Em um terminal, digite `yo azuresfguest`.
2. Nome do seu aplicativo.
3. Nome do seu serviço e fornecer detalhes de saudação incluindo caminho do executável do hello e parâmetros de saudação com que precisa ser chamada.

Yeoman cria um pacote de aplicativos com o aplicativo apropriado hello e arquivos de manifesto juntamente com instalar e desinstalar scripts.

<a id="manually"></a>

## <a name="manually-package-and-deploy-an-existing-executable"></a>Empacotar e implantar manualmente um executável existente
processo de saudação do empacotamento manualmente um executável de convidado se baseia na Olá etapas gerais a seguir:

1. Crie estrutura de diretório do pacote de saudação.
2. Adicione arquivos de código e configuração do aplicativo hello.
3. Edite o arquivo de manifesto de serviço hello.
4. Edite o arquivo de manifesto de aplicativo hello.

<!--
>[AZURE.NOTE] We do provide a packaging tool that allows you toocreate hello ApplicationPackage automatically. hello tool is currently in preview. You can download it from [here](http://aka.ms/servicefabricpacktool).
-->

### <a name="create-hello-package-directory-structure"></a>Criar estrutura de diretório do pacote de saudação
Você pode iniciar, criando a estrutura de diretórios hello, conforme descrito em Olá anterior seção, "Estrutura de arquivo de pacote de aplicativos".

### <a name="add-hello-applications-code-and-configuration-files"></a>Adicionar arquivos de código e configuração do aplicativo hello
Depois que você criou a estrutura de diretórios hello, você pode adicionar arquivos de código e configuração do aplicativo hello em diretórios de código e configuração de saudação. Você também pode criar diretórios adicionais ou subpastas em pastas de código ou configuração de saudação.

Service Fabric um `xcopy` conteúdo de saudação do hello diretório raiz do aplicativo, portanto, não há nenhum toouse estrutura predefinida diferente de criar dois diretórios principais, código e configurações. (Você pode escolher nomes diferentes, se desejar. Mais detalhes estão na próxima seção, hello.)

> [!NOTE]
> Certifique-se de incluir todos os arquivos de saudação e as dependências de Olá necessidades do aplicativo. Service Fabric copia Olá conteúdo do pacote de aplicativo hello em todos os nós no cluster Olá onde os serviços do aplicativo hello são toobe será implantado. pacote de saudação deve conter todo o código Olá aplicativo hello precisa toorun. Não suponha que as dependências de saudação já estão instaladas.
>
>

### <a name="edit-hello-service-manifest-file"></a>Editar o arquivo de manifesto de serviço Olá
Olá próxima etapa é Olá tooedit Olá serviço arquivo de manifesto tooinclude informações a seguir:

* nome de Olá Olá do tipo de serviço. Essa é uma ID do Service Fabric usa tooidentify um serviço.
* comando toouse toolaunch Olá aplicativo Hello (ExeHost).
* Qualquer script que precisa tooset toobe executar o aplicativo hello (SetupEntrypoint).

Olá, a seguir é um exemplo de um `ServiceManifest.xml` arquivo:

```xml
<?xml version="1.0" encoding="utf-8"?>
<ServiceManifest xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" Name="NodeApp" Version="1.0.0.0" xmlns="http://schemas.microsoft.com/2011/01/fabric">
   <ServiceTypes>
      <StatelessServiceType ServiceTypeName="NodeApp" UseImplicitHost="true"/>
   </ServiceTypes>
   <CodePackage Name="code" Version="1.0.0.0">
      <SetupEntryPoint>
         <ExeHost>
             <Program>scripts\launchConfig.cmd</Program>
         </ExeHost>
      </SetupEntryPoint>
      <EntryPoint>
         <ExeHost>
            <Program>node.exe</Program>
            <Arguments>bin/www</Arguments>
            <WorkingFolder>CodePackage</WorkingFolder>
         </ExeHost>
      </EntryPoint>
   </CodePackage>
   <Resources>
      <Endpoints>
         <Endpoint Name="NodeAppTypeEndpoint" Protocol="http" Port="3000" Type="Input" />
      </Endpoints>
   </Resources>
</ServiceManifest>
```

Olá seções a seguir passa pelo partes diferentes de saudação do arquivo de saudação que você precisa tooupdate.

#### <a name="update-servicetypes"></a>Atualizar ServiceTypes
```xml
<ServiceTypes>
  <StatelessServiceType ServiceTypeName="NodeApp" UseImplicitHost="true" />
</ServiceTypes>
```

* Você pode escolher qualquer nome que desejar para `ServiceTypeName`. Olá valor é usado em Olá `ApplicationManifest.xml` tooidentify Olá serviço de arquivo.
* Especifique `UseImplicitHost="true"`. Esse atributo diz Service Fabric que serviço Olá baseia-se em um aplicativo independente, para todos os Service Fabric precisa toodo toolaunch-lo como um processo e monitorar sua integridade.

#### <a name="update-codepackage"></a>Atualizar CodePackage
elemento de CodePackage Olá Especifica o local de saudação (e versão) do código de saudação do serviço.

```xml
<CodePackage Name="Code" Version="1.0.0.0">
```

Olá `Name` elemento é usado toospecify Olá nome do diretório Olá no pacote de aplicativo hello que contém o código do serviço hello. `CodePackage`também tem Olá `version` atributo. Isso pode ser usado toospecify versão de saudação do código-Olá e pode também ser usado código do serviço de saudação tooupgrade usando a infraestrutura de gerenciamento de ciclo de vida do aplicativo hello na malha do serviço.

#### <a name="optional-update-setupentrypoint"></a>Opcional: atualizar SetupEntrypoint
```xml
<SetupEntryPoint>
   <ExeHost>
       <Program>scripts\launchConfig.cmd</Program>
   </ExeHost>
</SetupEntryPoint>
```
elemento do Hello SetupEntryPoint é usado toospecify qualquer arquivo executável ou em lotes que deve ser executado antes que o código de saudação do serviço é iniciado. É uma etapa opcional, portanto não precisa toobe incluído se não houver nenhum inicialização necessária. Olá SetupEntryPoint é executado sempre que o serviço Olá for reiniciado.

Como há apenas um SetupEntryPoint, scripts de instalação necessário toobe agrupado em um arquivo único lote, se a instalação do aplicativo hello requer vários scripts. Olá SetupEntryPoint pode executar qualquer tipo de arquivo: arquivos executáveis, arquivos em lotes e cmdlets do PowerShell. Para obter mais detalhes, confira [Configure SetupEntryPoint](service-fabric-application-runas-security.md)(Configurar SetupEntryPoint).

Em Olá anterior de exemplo, Olá SetupEntryPoint executa um arquivo em lotes chamado `LaunchConfig.cmd` que é localizado na Olá `scripts` subdiretório do diretório de código hello (supondo que o elemento de pasta de trabalho de saudação é definido tooCodeBase).

#### <a name="update-entrypoint"></a>Atualizar EntryPoint
```xml
<EntryPoint>
  <ExeHost>
    <Program>node.exe</Program>
    <Arguments>bin/www</Arguments>
    <WorkingFolder>CodeBase</WorkingFolder>
  </ExeHost>
</EntryPoint>
```

Olá `EntryPoint` elemento no arquivo de manifesto de serviço Olá é usado toospecify como serviço de saudação toolaunch. Olá `ExeHost` elemento Especifica hello executável (e argumentos) que deve ser usado toolaunch Olá serviço.

* `Program`Especifica o nome de saudação do executável de saudação que deve iniciar o serviço de saudação.
* `Arguments`Especifica argumentos de saudação que devem ser passados toohello executável. Pode ser uma lista de parâmetros com argumentos.
* `WorkingFolder`Especifica o diretório de trabalho de saudação do processo Olá vai toobe iniciado. Você pode especificar três valores:
  * `CodeBase`Especifica esse diretório de trabalho Olá vai toobe definir diretório de código toohello no pacote de aplicativo hello (`Code` diretório no hello anterior a estrutura de arquivos).
  * `CodePackage`Especifica esse diretório de trabalho Olá vai toobe definir toohello raiz do pacote de aplicativo hello (`GuestService1Pkg` no hello anterior a estrutura de arquivos).
    * `Work`Especifica que os arquivos de saudação são colocados em uma subpasta chamada de trabalho.

Olá pasta de trabalho é diretório de trabalho útil tooset Olá correto para que os caminhos relativos podem ser usados por qualquer um dos scripts de inicialização ou o aplicativo hello.

#### <a name="update-endpoints-and-register-with-naming-service-for-communication"></a>Atualizar pontos de extremidade e registrar com o Serviço de Nomenclatura para comunicação
```xml
<Endpoints>
   <Endpoint Name="NodeAppTypeEndpoint" Protocol="http" Port="3000" Type="Input" />
</Endpoints>

```
Em Olá anterior de exemplo, Olá `Endpoint` elemento Especifica os pontos de extremidade de saudação que aplicativo hello pode escutar em. Neste exemplo, Olá aplicativo Node. js escuta http na porta 3000.

Além disso você pode pedir Service Fabric toopublish toohello esse ponto de extremidade Naming Service para que outros serviços podem descobrir o serviço de toothis de endereço de ponto de extremidade de saudação. Isso permite que você toocommunicate capaz de toobe entre os serviços que são executáveis de convidado.
Hello endereço de ponto de extremidade publicados tem Olá forma `UriScheme://IPAddressOrFQDN:Port/PathSuffix`. `UriScheme` e `PathSuffix` são atributos opcionais. `IPAddressOrFQDN`é Olá endereço IP ou nome de domínio totalmente qualificado do nó Olá este executável é colocada no e ele é calculado para você.

No hello exemplo a seguir, uma vez o serviço Olá é implantado, no Gerenciador do Service Fabric você ver um ponto de extremidade semelhante muito`http://10.1.4.92:3000/myapp/` publicado Olá instância de serviço. Se esta for um computador local, você verá `http://localhost:3000/myapp/`.

```xml
<Endpoints>
   <Endpoint Name="NodeAppTypeEndpoint" Protocol="http" Port="3000"  UriScheme="http" PathSuffix="myapp/" Type="Input" />
</Endpoints>
```
Você pode usar esses endereços com [proxy reverso](service-fabric-reverseproxy.md) toocommunicate entre serviços.

### <a name="edit-hello-application-manifest-file"></a>Editar o arquivo de manifesto de aplicativo hello
Depois que você configurou Olá `Servicemanifest.xml` arquivo, você precisa toomake toohello algumas alterações `ApplicationManifest.xml` tooensure Olá de arquivo correto para o tipo de serviço e o nome são usados.

```xml
<?xml version="1.0" encoding="utf-8"?>
<ApplicationManifest xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" ApplicationTypeName="NodeAppType" ApplicationTypeVersion="1.0" xmlns="http://schemas.microsoft.com/2011/01/fabric">
   <ServiceManifestImport>
      <ServiceManifestRef ServiceManifestName="NodeApp" ServiceManifestVersion="1.0.0.0" />
   </ServiceManifestImport>
</ApplicationManifest>
```

#### <a name="servicemanifestimport"></a>ServiceManifestImport
Em Olá `ServiceManifestImport` elemento, você pode especificar um ou mais serviços que você deseja tooinclude no aplicativo hello. Os serviços são referenciados com `ServiceManifestName`, que especifica o nome de saudação do diretório de saudação onde hello `ServiceManifest.xml` arquivo está localizado.

```xml
<ServiceManifestImport>
  <ServiceManifestRef ServiceManifestName="NodeApp" ServiceManifestVersion="1.0.0.0" />
</ServiceManifestImport>
```

## <a name="set-up-logging"></a>Configurar registro em log
Para executáveis de convidado, é útil toobe toosee capaz de console logs toofind out se os scripts de configuração de aplicativo e Olá mostram erros.
Redirecionamento de console pode ser configurado no hello `ServiceManifest.xml` arquivo usando Olá `ConsoleRedirection` elemento.

> [!WARNING]
> Nunca use a política de redirecionamento do console de saudação em um aplicativo que é implantado na produção, pois isso pode afetar o failover de aplicativo hello. *Só* use isso para fins de depuração e de desenvolvimento locais.  
>
>

```xml
<EntryPoint>
  <ExeHost>
    <Program>node.exe</Program>
    <Arguments>bin/www</Arguments>
    <WorkingFolder>CodeBase</WorkingFolder>
    <ConsoleRedirection FileRetentionCount="5" FileMaxSizeInKb="2048"/>
  </ExeHost>
</EntryPoint>
```

`ConsoleRedirection`pode ser um diretório de trabalho usado tooredirect console saída (stdout e stderr) tooa. Isso fornece Olá capacidade tooverify que não existem erros durante a instalação de saudação ou execução do aplicativo hello no cluster do Service Fabric hello.

`FileRetentionCount`Determina quantos arquivos são salvos no diretório de trabalho hello. Um valor de 5, por exemplo, significa que os arquivos de log Olá para execuções de cinco anterior Olá são armazenados no diretório de trabalho hello.

`FileMaxSizeInKb`Especifica o tamanho máximo de Olá Olá dos arquivos de log.

Arquivos de log são salvos em um dos diretórios de trabalho do serviço de saudação. toodetermine onde Olá arquivos estão localizados, use o Service Fabric Explorer toodetermine qual serviço de saudação do nó está em execução e o diretório de trabalho está sendo usado. Esse processo é abordado mais adiante neste artigo.

## <a name="deployment"></a>Implantação
Olá última etapa é muito[implantar seu aplicativo](service-fabric-deploy-remove-applications.md). Olá mostra de script do PowerShell a seguir como toodeploy seu cluster de desenvolvimento local do aplicativo toohello e iniciar um novo serviço de malha do serviço.

```PowerShell

Connect-ServiceFabricCluster localhost:19000

Write-Host 'Copying application package...'
Copy-ServiceFabricApplicationPackage -ApplicationPackagePath 'C:\Dev\MultipleApplications' -ImageStoreConnectionString 'file:C:\SfDevCluster\Data\ImageStoreShare' -ApplicationPackagePathInImageStore 'nodeapp'

Write-Host 'Registering application type...'
Register-ServiceFabricApplicationType -ApplicationPathInImageStore 'nodeapp'

New-ServiceFabricApplication -ApplicationName 'fabric:/nodeapp' -ApplicationTypeName 'NodeAppType' -ApplicationTypeVersion 1.0

New-ServiceFabricService -ApplicationName 'fabric:/nodeapp' -ServiceName 'fabric:/nodeapp/nodeappservice' -ServiceTypeName 'NodeApp' -Stateless -PartitionSchemeSingleton -InstanceCount 1

```

>[!TIP]
> [Compactar pacote hello](service-fabric-package-apps.md#compress-a-package) antes de copiar o repositório de imagens toohello se o pacote de saudação é grande ou tem muitos arquivos. Leia mais [aqui](service-fabric-deploy-remove-applications.md#upload-the-application-package).
>

Um serviço do Service Fabric pode ser implantado em várias "configurações". Por exemplo, ele pode ser implantado como uma ou várias instâncias, ou pode ser implantado de forma que há uma instância do serviço de saudação em cada nó do cluster do Service Fabric hello.

Olá `InstanceCount` parâmetro hello `New-ServiceFabricService` cmdlet é usado toospecify quantas instâncias do serviço de saudação devem ser iniciadas no cluster do Service Fabric hello. Você pode definir Olá `InstanceCount` valor, dependendo do tipo de saudação do aplicativo que você está implantando. Olá dois os cenários mais comuns são:

* `InstanceCount = "1"`. Nesse caso, apenas uma instância do serviço de saudação é implantada no cluster hello. Agendador do Service Fabric determina qual serviço de saudação do nó será toobe implantado em.
* `InstanceCount ="-1"`. Nesse caso, uma instância do serviço de saudação é implantada em cada nó no cluster do Service Fabric hello. resultado Hello está tendo um (e apenas um) instância do serviço de saudação para cada nó de cluster hello.

Essa é uma configuração útil para aplicativos front-end (por exemplo, um ponto de extremidade REST), porque aplicativos cliente precisam muito "conectar" tooany de nós de Olá no ponto de extremidade da saudação toouse Olá cluster. Essa configuração também pode ser usada quando, por exemplo, todos os nós do cluster do Service Fabric Olá são conectados tooa balanceador de carga. O tráfego do cliente, em seguida, pode ser distribuído em serviço Olá que está em execução em todos os nós no cluster de saudação.

## <a name="check-your-running-application"></a>Verificar seu aplicativo em execução
No Gerenciador do Service Fabric, identifica o nó de saudação onde o serviço hello está sendo executado. Neste exemplo, ele está executando no Node1:

![Nó em que o serviço está em execução](./media/service-fabric-deploy-existing-app/nodeappinsfx.png)

Se você navegar nó toohello e procurar toohello aplicativo, você verá informações de nó essencial hello, incluindo sua localização no disco.

![Local no disco](./media/service-fabric-deploy-existing-app/locationondisk2.png)

Se você procurar o diretório toohello usando o Gerenciador de servidores, você pode encontrar o diretório de trabalho hello e pasta de log do serviço hello, conforme mostrado no hello captura de tela a seguir: 

![Local do log](./media/service-fabric-deploy-existing-app/loglocation.png)

## <a name="next-steps"></a>Próximas etapas
Neste artigo, você aprendeu como toopackage um executável de convidado e implantá-lo tooService malha. Consulte Olá artigos para tarefas e informações relacionadas a seguir.

* [Exemplo para empacotar e implantar um executável de convidado](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started), incluindo uma versão de pré-lançamento do toohello de link da ferramenta de empacotamento Olá
* [Exemplo de dois convidado executáveis (c# e nodejs) se comunicar por meio do serviço de nomenclatura hello usando REST](https://github.com/Azure-Samples/service-fabric-dotnet-containers)
* [Implantar vários executáveis de convidado](service-fabric-deploy-multiple-apps.md)
* [Criar seu primeiro aplicativo do Service Fabric usando o Visual Studio](service-fabric-create-your-first-application-in-visual-studio.md)
