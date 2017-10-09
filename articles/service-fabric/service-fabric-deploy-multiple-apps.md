---
title: aaaDeploy um aplicativo Node. js que usa o MongoDB | Microsoft Docs
description: "Instruções passo a passo sobre como toopackage vários cluster convidado do executáveis toodeploy tooan Azure Service Fabric"
services: service-fabric
documentationcenter: .net
author: msfussell
manager: timlt
editor: 
ms.assetid: b76bb756-c1ba-49f9-9666-e9807cf8f92f
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/02/2017
ms.author: msfussell;mikhegn
ms.openlocfilehash: 2775080f0d9d42d6ba15cca911e23067106be26d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-multiple-guest-executables"></a>Implantar vários executáveis de convidado
Este artigo mostra como toopackage e implantar várias tooAzure de executáveis de convidado do Service Fabric. Para criar e implantar um único pacote de malha do serviço, leia como muito[implantar um tooService executável de convidado malha](service-fabric-deploy-existing-app.md).

Embora este passo a passo mostra como toodeploy um aplicativo com um front-end de Node. js que usa o MongoDB como repositório de dados hello, você pode aplicar tooany aplicativo hello etapas tem dependências em outro aplicativo.   

Você pode usar o Visual Studio tooproduce Olá pacote de aplicativo que contém vários executáveis de convidado. Consulte [toopackage com o Visual Studio um aplicativo existente](service-fabric-deploy-existing-app.md). Após ter adicionado o executável de convidado primeiro hello, clique com botão direito no projeto de aplicativo hello e selecione Olá **Adicionar -> serviço de malha do novo serviço** tooadd Olá segunda convidado projeto executável toohello solução. Observação: Se você escolher a fonte de saudação toolink em Olá projeto do Visual Studio, criação de solução do Visual Studio Olá, garantirá que seu pacote de aplicativo é o toodate com alterações feitas na fonte de saudação. 

## <a name="samples"></a>Exemplos
* [Exemplo de empacotamento e implantação de um executável convidado](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started)
* [Exemplo de dois convidado executáveis (c# e nodejs) se comunicar por meio do serviço de nomenclatura hello usando REST](https://github.com/Azure-Samples/service-fabric-dotnet-containers)

## <a name="manually-package-hello-multiple-guest-executable-application"></a>Manualmente o pacote hello vários aplicativo executável de convidado
Como alternativa, você pode empacotar manualmente executável de convidado hello. Para empacotamento manual de hello, este artigo usa a ferramenta de empacotamento do Service Fabric hello, está disponível em [http://aka.ms/servicefabricpacktool](http://aka.ms/servicefabricpacktool).

### <a name="packaging-hello-nodejs-application"></a>Saudação de empacotamento aplicativo Node. js
Este artigo pressupõe que o Node. js não está instalado em nós de Olá no cluster do Service Fabric hello. Como consequência, você precisa tooadd Node.exe toohello diretório de raiz do seu aplicativo de nó antes do empacotamento. estrutura de diretório de saudação do aplicativo do Node. js hello (usando a estrutura do web Express e o mecanismo de modelo Jade) deve ser semelhante toohello um abaixo:

```
|-- NodeApplication
    |-- bin
        |-- www
    |-- node_modules
        |-- .bin
        |-- express
        |-- jade
        |-- etc.
    |-- public
        |-- images
        |-- etc.
    |-- routes
        |-- index.js
        |-- users.js
    |-- views
        |-- index.jade
        |-- etc.
    |-- app.js
    |-- package.json
    |-- node.exe
```

Como uma próxima etapa, você cria um pacote de aplicativo hello aplicativo Node. js. código de saudação abaixo cria um pacote de aplicativo de malha do serviço que contém o aplicativo do hello Node. js.

```
.\ServiceFabricAppPackageUtil.exe /source:'[yourdirectory]\MyNodeApplication' /target:'[yourtargetdirectory] /appname:NodeService /exe:'node.exe' /ma:'bin/www' /AppType:NodeAppType
```

Abaixo está uma descrição dos parâmetros de saudação que estão sendo usadas:

* **/Source** pontos toohello diretório de aplicativo hello que deve ser empacotado.
* **/Target** define Olá diretório no qual Olá pacote deve ser criado. Este diretório tem toobe diferente saudação do diretório de origem.
* **/appname** define o nome do aplicativo de saudação do aplicativo existente hello. É importante toounderstand que isso se traduz toohello nome do serviço no manifesto de saudação e não toohello nome do aplicativo de malha do serviço.
* **/exe** define Olá executável que Service Fabric deve toolaunch, neste caso `node.exe`.
* **/ma** define o argumento de saudação que está sendo usado toolaunch Olá executável. Como o Node. js não estiver instalado, do Service Fabric precisa de servidor de web toolaunch Olá Node. js executando `node.exe bin/www`.  `/ma:'bin/www'`informa Olá empacotamento ferramenta toouse `bin/ma` como argumento de saudação para node.exe.
* **/ O tipo de aplicativo** define o nome do tipo de aplicativo hello Service Fabric.

Se você procurar o diretório toohello que foi especificado no parâmetro de /target hello, você pode ver que essa ferramenta Olá criou um pacote de malha do serviço totalmente funcional conforme mostrado abaixo:

```
|--[yourtargetdirectory]
    |-- NodeApplication
        |-- C
              |-- bin
              |-- data
              |-- node_modules
              |-- public
              |-- routes
              |-- views
              |-- app.js
              |-- package.json
              |-- node.exe
        |-- config
              |--Settings.xml
        |-- ServiceManifest.xml
    |-- ApplicationManifest.xml
```
Olá ServiceManifest.xml gerado agora tem uma seção que descreve como o servidor de web Node.js Olá deve ser iniciada, conforme mostrado no trecho de código Olá abaixo:

```xml
<CodePackage Name="C" Version="1.0">
    <EntryPoint>
        <ExeHost>
            <Program>node.exe</Program>
            <Arguments>'bin/www'</Arguments>
            <WorkingFolder>CodePackage</WorkingFolder>
        </ExeHost>
    </EntryPoint>
</CodePackage>
```
Neste exemplo, o servidor de web de Node. js Olá escuta tooport 3000, portanto, você precisa de informações de ponto de extremidade Olá tooupdate no arquivo ServiceManifest.xml de saudação conforme mostrado abaixo.   

```xml
<Resources>
      <Endpoints>
         <Endpoint Name="NodeServiceEndpoint" Protocol="http" Port="3000" Type="Input" />
      </Endpoints>
</Resources>
```
### <a name="packaging-hello-mongodb-application"></a>Saudação de empacotamento MongoDB aplicativo
Agora que você empacotar aplicativo do Node. js hello, você pode vá em frente e MongoDB do pacote. Como mencionado anteriormente, Olá etapas que você percorrer agora não são tooNode.js específico e MongoDB. Na verdade, se aplicam a aplicativos tooall devem toobe reunido como um aplicativo de malha do serviço.  

toopackage MongoDB, você deseja toomake-se de que você empacotar Mongod.exe e Mongo.exe. Ambos os binários estão localizados em Olá `bin` diretório de seu diretório de instalação do MongoDB. estrutura de diretórios Olá parece semelhante toohello um abaixo.

```
|-- MongoDB
    |-- bin
        |-- mongod.exe
        |-- mongo.exe
        |-- anybinary.exe
```
Service Fabric precisa toostart MongoDB com um toohello semelhante do comando um abaixo, para que você precise Olá toouse `/ma` parâmetro ao empacotar o MongoDB.

```
mongod.exe --dbpath [path toodata]
```
> [!NOTE]
> dados de Olá não estão sendo preservados no caso de saudação de uma falha de nó se você colocar o diretório de dados do MongoDB Olá no diretório local de saudação do nó de saudação. Você deve usar o armazenamento durável ou implementar um conjunto ordem tooprevent perda de dados de réplicas do MongoDB.  
>
>

No shell de comando do PowerShell ou hello, podemos executar a ferramenta de empacotamento de Olá com hello parâmetros a seguir:

```
.\ServiceFabricAppPackageUtil.exe /source: [yourdirectory]\MongoDB' /target:'[yourtargetdirectory]' /appname:MongoDB /exe:'bin\mongod.exe' /ma:'--dbpath [path toodata]' /AppType:NodeAppType
```

No pacote de aplicativo do Service Fabric tooyour do pedido tooadd MongoDB, você precisa toomake-se de que o parâmetro hello /target pontos toohello mesmo diretório que já contém o manifesto do aplicativo hello junto com o aplicativo do hello Node. js. Você também precisa toomake-se de que você está usando Olá mesmo nome ApplicationType.

Vamos procurar o diretório toohello e examinar qual ferramenta Olá criou.

```
|--[yourtargetdirectory]
    |-- MyNodeApplication
    |-- MongoDB
        |-- C
            |--bin
                |-- mongod.exe
                |-- mongo.exe
                |-- etc.
        |-- config
            |--Settings.xml
        |-- ServiceManifest.xml
    |-- ApplicationManifest.xml
```
Como você pode ver, ferramenta Olá adicionado um novo diretório de toohello de pasta, MongoDB, que contém os binários do MongoDB hello. Se você abrir Olá `ApplicationManifest.xml` arquivo, você pode ver que o pacote hello agora contém o aplicativo de Node. js hello e MongoDB. Olá código a seguir mostra o hello conteúdo saudação do manifesto do aplicativo.

```xml
<ApplicationManifest xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" ApplicationTypeName="MyNodeApp" ApplicationTypeVersion="1.0" xmlns="http://schemas.microsoft.com/2011/01/fabric">
   <ServiceManifestImport>
      <ServiceManifestRef ServiceManifestName="MongoDB" ServiceManifestVersion="1.0" />
   </ServiceManifestImport>
   <ServiceManifestImport>
      <ServiceManifestRef ServiceManifestName="NodeService" ServiceManifestVersion="1.0" />
   </ServiceManifestImport>
   <DefaultServices>
      <Service Name="MongoDBService">
         <StatelessService ServiceTypeName="MongoDB">
            <SingletonPartition />
         </StatelessService>
      </Service>
      <Service Name="NodeServiceService">
         <StatelessService ServiceTypeName="NodeService">
            <SingletonPartition />
         </StatelessService>
      </Service>
   </DefaultServices>
</ApplicationManifest>  
```

### <a name="publishing-hello-application"></a>Aplicativo de publicação hello
Olá última etapa é toopublish Olá aplicativo toohello Service Fabric cluster local usando scripts do PowerShell Olá abaixo:

```
Connect-ServiceFabricCluster localhost:19000

Write-Host 'Copying application package...'
Copy-ServiceFabricApplicationPackage -ApplicationPackagePath '[yourtargetdirectory]' -ImageStoreConnectionString 'file:C:\SfDevCluster\Data\ImageStoreShare' -ApplicationPackagePathInImageStore 'NodeAppType'

Write-Host 'Registering application type...'
Register-ServiceFabricApplicationType -ApplicationPathInImageStore 'NodeAppType'

New-ServiceFabricApplication -ApplicationName 'fabric:/NodeApp' -ApplicationTypeName 'NodeAppType' -ApplicationTypeVersion 1.0  
```

Após o aplicativo hello cluster local toohello publicado com êxito, é possível acessar o aplicativo de Node. js de saudação na porta de saudação que é inserido no manifesto do serviço de saudação do aplicativo de Node. js hello – por exemplo, http://localhost:3000.

Neste tutorial, você viu como tooeasily pacote dois aplicativos existentes como um aplicativo de malha do serviço. Você também aprendeu como toodeploy-tooService malha para que ele pode se beneficiar Olá de alguns recursos de malha do serviço, como integração alta disponibilidade e integridade do sistema.


## <a name="adding-more-guest-executables-tooan-existing-application-using-yeoman-on-linux"></a>Adicionando mais convidado executáveis tooan aplicativo existente usando Yeoman no Linux

tooadd outro tooan aplicativo de serviço já criado usando `yo`, executar Olá etapas a seguir: 
1. Alterar o diretório raiz de toohello do aplicativo existente hello.  Por exemplo, `cd ~/YeomanSamples/MyApplication`, se `MyApplication` é um aplicativo hello criado por Yeoman.
2. Execute `yo azuresfguest:AddService` e fornecer detalhes necessários hello.

## <a name="next-steps"></a>Próximas etapas
* Saiba mais sobre como implantar contêineres com a [Visão geral de contêineres e do Service Fabric](service-fabric-containers-overview.md)
* [Exemplo de empacotamento e implantação de um executável convidado](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started)
* [Exemplo de dois convidado executáveis (c# e nodejs) se comunicar por meio do serviço de nomenclatura hello usando REST](https://github.com/Azure-Samples/service-fabric-dotnet-containers)
