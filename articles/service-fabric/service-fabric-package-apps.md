---
title: aaaPackage um aplicativo do Azure Service Fabric | Microsoft Docs
description: "Como toopackage um aplicativo de malha do serviço antes de implantar o cluster tooa."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: mani-ramaswamy
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: ryanwi
ms.openlocfilehash: b3918e1e25e532acdc9440855213e1fa364ea000
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="package-an-application"></a>Preparar um aplicativo
Este artigo descreve como toopackage um aplicativo de serviço de malha e torná-lo pronto para a implantação.

## <a name="package-layout"></a>Layout do pacote
manifesto do aplicativo Hello, um ou mais manifestos de serviço e outros pacotes necessários arquivos devem ser organizados em um layout específico para implantação em um cluster do Service Fabric. manifestos de exemplo Hello neste artigo precisaria toobe organizado em Olá estrutura de diretórios a seguir:

```
PS D:\temp> tree /f .\MyApplicationType

D:\TEMP\MYAPPLICATIONTYPE
│   ApplicationManifest.xml
│
└───MyServiceManifest
    │   ServiceManifest.xml
    │
    ├───MyCode
    │       MyServiceHost.exe
    │
    ├───MyConfig
    │       Settings.xml
    │
    └───MyData
            init.dat
```

pastas de saudação são nomeadas toomatch Olá **nome** atributos de cada elemento correspondente. Por exemplo, se hello o manifesto de serviço contidos dois pacotes de código com nomes de saudação **MyCodeA** e **MyCodeB**, em seguida, duas pastas com hello mesmos nomes conteria Olá binários necessários para cada código pacote.

## <a name="use-setupentrypoint"></a>Use o SetupEntryPoint
Cenários típicos de uso **SetupEntryPoint** são quando precisar de um executável antes do início do serviço de saudação do toorun ou precisar tooperform uma operação com privilégios elevados. Por exemplo:

* Configurando e inicializar variáveis de ambiente que Olá necessidades executável do serviço. Não é limitado tooonly executáveis gravados por meio de modelos de programação de malha do serviço de saudação. Por exemplo, npm.exe precisa de algumas variáveis de ambiente configurados para implantar um aplicativo node.js.
* Configurando o controle de acesso, instalando certificados de segurança.

Para obter mais informações sobre como Olá tooconfigure **SetupEntryPoint**, consulte [configurar política de saudação para um ponto de entrada de configuração de serviço](service-fabric-application-runas-security.md)

<a id="Package-App"></a>
## <a name="configure"></a>Configurar
### <a name="build-a-package-by-using-visual-studio"></a>Compilar um pacote usando o Visual Studio
Se você usar o Visual Studio 2015 toocreate seu aplicativo, você pode usar o hello pacote tooautomatically comando cria um pacote que corresponda layout Olá descrito acima.

toocreate um pacote, clique em projeto de aplicativo hello no Gerenciador de soluções e escolha o comando de pacote hello, conforme mostrado abaixo:

![Empacotando um aplicativo no Visual Studio][vs-package-command]

Quando a compactação estiver concluída, você pode encontrar o local de saudação do pacote de saudação no hello **saída** janela. Olá empacotamento ocorrerá automaticamente quando você implantar ou depura seu aplicativo no Visual Studio.

### <a name="build-a-package-by-command-line"></a>Criar um pacote pela linha de comando
Também é possível tooprogrammatically pacote usando o aplicativo `msbuild.exe`. Bastidores hello, Visual Studio é executá-lo para a saída de hello é o mesma.

```shell
D:\Temp> msbuild HelloWorld.sfproj /t:Package
```

## <a name="test-hello-package"></a>Pacote de saudação do teste
Você pode verificar a estrutura do pacote hello localmente por meio do PowerShell usando Olá [ServiceFabricApplicationPackage teste](/powershell/module/servicefabric/test-servicefabricapplicationpackage?view=azureservicefabricps) comando.
Esse comando verifica se há problemas de análise de manifesto e também todas as referências. Esse comando verifica apenas a exatidão estrutural Olá de diretórios de saudação e arquivos no pacote de saudação.
Ele não verifica qualquer conteúdo do pacote de códigos ou dados do hello além de verificar se todos os arquivos necessários estão presentes.

```
PS D:\temp> Test-ServiceFabricApplicationPackage .\MyApplicationType
False
Test-ServiceFabricApplicationPackage : hello EntryPoint MySetup.bat is not found.
FileName: C:\Users\servicefabric\AppData\Local\Temp\TestApplicationPackage_7195781181\nrri205a.e2h\MyApplicationType\MyServiceManifest\ServiceManifest.xml
```

Este erro mostra que Olá *MySetup.bat* arquivo referenciado no manifesto do serviço Olá **SetupEntryPoint** está ausente no pacote de código hello. Depois que o arquivo ausente Olá é adicionado, passa a verificação do aplicativo hello:

```
PS D:\temp> tree /f .\MyApplicationType

D:\TEMP\MYAPPLICATIONTYPE
│   ApplicationManifest.xml
│
└───MyServiceManifest
    │   ServiceManifest.xml
    │
    ├───MyCode
    │       MyServiceHost.exe
    │       MySetup.bat
    │
    ├───MyConfig
    │       Settings.xml
    │
    └───MyData
            init.dat

PS D:\temp> Test-ServiceFabricApplicationPackage .\MyApplicationType
True
PS D:\temp>
```

Se seu aplicativo tiver [parâmetros do aplicativo](service-fabric-manage-multiple-environment-app-configuration.md) definidos, você poderá passá-los em [Test-ServiceFabricApplicationPackage](/powershell/module/servicefabric/test-servicefabricapplicationpackage?view=azureservicefabricps) para a validação correta.

Se você souber cluster Olá onde o aplicativo hello será implantado, é recomendável passar no hello `ImageStoreConnectionString` parâmetro. Nesse caso, o pacote de Olá também é validado em relação a versões anteriores do aplicativo hello que já estão em execução no cluster hello. Por exemplo, a validação de saudação pode detectar se um pacote com hello mesma versão, mas conteúdo diferente já foi implantada.  

Depois que o aplicativo hello é empacotado corretamente e passa a validação, avalie com base no tamanho hello e número de saudação de arquivos se a compactação é necessária.

## <a name="compress-a-package"></a>Compactar um pacote
Quando um pacote é grande ou tem vários arquivos, você pode compactá-lo para uma implantação mais rápida. A compactação reduz o número de saudação de arquivos e o tamanho de pacote de saudação.
Para um pacote de aplicativos compactados, [pacote de aplicativo hello Carregando](service-fabric-deploy-remove-applications.md#upload-the-application-package) pode levar mais comparados toouploading Olá descompactados pacote (especialmente se o tempo de compactação é acrescentado), mas [registrando](service-fabric-deploy-remove-applications.md#register-the-application-package) e [tipo de cancelamento do registro do aplicativo hello](service-fabric-deploy-remove-applications.md#unregister-an-application-type) são mais rápidos para um pacote de aplicativos compactados.

mecanismo de implantação de saudação é o mesmo para os pacotes compactados e não compactados. Se o pacote de saudação for compactado, ela é armazenada como tal no repositório de imagens de cluster hello e é descompactado no nó de saudação antes que o aplicativo hello é executado.
compactação de saudação substitui o pacote de Service Fabric válido de saudação com versão compactada Olá. pasta Olá deverá conceder permissões de gravação. A execução da compactação em um pacote já compactado não produz nenhuma alteração.

É possível compactar um pacote executando o comando do Powershell Olá [cópia ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) com `CompressPackage` alternar. Olá descompactar pacote com hello mesmo comando, usando `UncompressPackage` alternar.

Olá comando a seguir compacta pacote hello sem copiá-lo toohello repositório de imagens. Você pode copiar um pacote compactado tooone ou mais clusters de malha do serviço, conforme necessário, usando [cópia ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) sem Olá `SkipCopy` sinalizador.
pacote de saudação agora inclui os arquivos compactados para Olá `code`, `config`, e `data` pacotes. o manifesto do aplicativo Hello e Olá manifestos do serviço não estão compactados, porque eles são necessários para várias operações internas (como compartilhamento de extração de versão e o nome de tipo de aplicativo para determinados validações de pacote).
Manifestos de compactação Olá tornaria essas operações ineficiente.

```
PS D:\temp> tree /f .\MyApplicationType

D:\TEMP\MYAPPLICATIONTYPE
│   ApplicationManifest.xml
│
└───MyServiceManifest
    │   ServiceManifest.xml
    │
    ├───MyCode
    │       MyServiceHost.exe
    │       MySetup.bat
    │
    ├───MyConfig
    │       Settings.xml
    │
    └───MyData
            init.dat
PS D:\temp> Copy-ServiceFabricApplicationPackage -ApplicationPackagePath .\MyApplicationType -CompressPackage -SkipCopy

PS D:\temp> tree /f .\MyApplicationType

D:\TEMP\MYAPPLICATIONTYPE
│   ApplicationManifest.xml
│
└───MyServiceManifest
       ServiceManifest.xml
       MyCode.zip
       MyConfig.zip
       MyData.zip

```

Como alternativa, você pode compactar e copiar o pacote de saudação com [ServiceFabricApplicationPackage cópia](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) em uma única etapa.
Se o pacote de saudação for grande, forneça uma hora de tooallow de tempo limite alto o suficiente para compactação de pacote hello e o cluster de toohello de carregamento de saudação.
```
PS D:\temp> Copy-ServiceFabricApplicationPackage -ApplicationPackagePath .\MyApplicationType -ApplicationPackagePathInImageStore MyApplicationType -ImageStoreConnectionString fabric:ImageStore -CompressPackage -TimeoutSec 5400
```

Internamente, o Service Fabric calcula somas de verificação para pacotes de aplicativos Olá para validação. Ao usar a compactação, Olá somas de verificação são computadas em Olá compactado versões de cada pacote.
Se você copiou uma versão descompactada do seu pacote de aplicativo, e você desejar toouse compactação Olá mesmo pacote, você deve alterar as versões de saudação do hello `code`, `config`, e `data` incompatibilidade de soma de verificação de tooavoid de pacotes. Se os pacotes de saudação forem alterados, em vez de alterar a versão de hello, você pode usar [comparação provisionamento](service-fabric-application-upgrade-advanced.md). Com essa opção, não inclua pacote inalterado Olá em vez disso, referenciá-lo no manifesto do serviço hello.

Da mesma forma, se você carregou uma versão compactada do pacote de saudação e você desejar toouse um pacote não compactado, você deve atualizar a incompatibilidade de soma de verificação Olá versões tooavoid hello.

Olá pacote é agora empacotado corretamente, validado e compactado (se necessário), para que esteja pronta para [implantação](service-fabric-deploy-remove-applications.md) tooone ou uma malha de serviço mais clusters.

### <a name="compress-packages-when-deploying-using-visual-studio"></a>Compactar pacotes durante a implantação usando o Visual Studio
Você pode instruir pacotes toocompress do Visual Studio na implantação, adicionando Olá `CopyPackageParameters` tooyour elemento perfil de publicação e definir Olá `CompressPackage` atributo muito`true`.

``` xml
    <PublishProfile xmlns="http://schemas.microsoft.com/2015/05/fabrictools">
        <ClusterConnectionParameters ConnectionEndpoint="mycluster.westus.cloudapp.azure.com" />
        <ApplicationParameterFile Path="..\ApplicationParameters\Cloud.xml" />
        <CopyPackageParameters CompressPackage="true"/>
    </PublishProfile>
```

## <a name="next-steps"></a>Próximas etapas
[Implantar e remover aplicativos] [ 10] descreve como instâncias do aplicativo toouse PowerShell toomanage

[Gerenciando parâmetros do aplicativo para vários ambientes] [ 11] descreve como tooconfigure parâmetros e variáveis de ambiente para instâncias de aplicativo diferente.

[Configurar políticas de segurança para seu aplicativo] [ 12] descreve como os serviços de toorun em acesso de toorestrict de políticas de segurança.

<!--Image references-->
[vs-package-command]: ./media/service-fabric-package-apps/vs-package-command.png

<!--Link references--In actual articles, you only need a single period before hello slash-->
[10]: service-fabric-deploy-remove-applications.md
[11]: service-fabric-manage-multiple-environment-app-configuration.md
[12]: service-fabric-application-runas-security.md
