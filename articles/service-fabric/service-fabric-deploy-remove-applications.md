---
title: "aaaAzure implantação de aplicativos do Service Fabric | Microsoft Docs"
description: "Como toodeploy e remova os aplicativos na malha do serviço usando o PowerShell."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: b120ffbf-f1e3-4b26-a492-347c29f8f66b
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/01/2017
ms.author: ryanwi
ms.openlocfilehash: 3de9c6a937ee7b29bf9ec86d6e9e631487797507
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-remove-applications-using-powershell"></a>Implantar e remover aplicativos usando o PowerShell
> [!div class="op_single_selector"]
> * [PowerShell](service-fabric-deploy-remove-applications.md)
> * [Visual Studio](service-fabric-publish-app-remote-cluster.md)
> * [APIs de FabricClient](service-fabric-deploy-remove-applications-fabricclient.md)
> 
> 

<br/>

Assim que um [tipo de aplicativo for empacotado][10], ele está pronto para implantação em um cluster do Azure Service Fabric. Implantação envolve Olá três etapas a seguir:

1. Carregar o repositório de imagens toohello do pacote de aplicativo hello
2. Registrar o tipo de aplicativo hello
3. Criar instância de aplicativo hello

Depois que um aplicativo é implantado e uma instância está em execução no cluster hello, você pode excluir a instância do aplicativo hello e seu tipo de aplicativo. toocompletely remover um aplicativo de cluster Olá envolve Olá etapas a seguir:

1. Remover (ou excluir) Olá executando a instância do aplicativo
2. Cancelar o registro do tipo de aplicativo hello se você não precisar mais dela
3. Remover o pacote de aplicativo hello saudação do repositório de imagens

Se você usar [Visual Studio para implantar e depurar aplicativos](service-fabric-publish-app-remote-cluster.md) no cluster de desenvolvimento local, todos os Olá etapas anteriores são tratadas automaticamente por meio de um script do PowerShell.  Esse script é encontrado no hello *Scripts* pasta do projeto de aplicativo hello. Este artigo fornece informações detalhadas sobre o que esse script está fazendo para que você possa executar Olá mesmas operações fora do Visual Studio. 
 
## <a name="connect-toohello-cluster"></a>Conecte-se o cluster toohello
Antes de executar quaisquer comandos do PowerShell neste artigo, sempre iniciar usando [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cluster do tooconnect toohello do Service Fabric. cluster de desenvolvimento local em toohello tooconnect, execute Olá seguinte:

```powershell
PS C:\>Connect-ServiceFabricCluster
```

Para obter exemplos de conexão tooa remoto cluster ou protegido usando o Active Directory do Azure, X509 certificados ou consulte Active Directory do Windows [conectar tooa segura cluster](service-fabric-connect-to-secure-cluster.md).

## <a name="upload-hello-application-package"></a>Carregar pacote de aplicativo hello
Carregar pacote de aplicativo hello coloca em um local que seja acessível pelos componentes internos do Service Fabric.
Se quiser que o pacote de aplicativo de saudação tooverify localmente, use Olá [ServiceFabricApplicationPackage teste](/powershell/module/servicefabric/test-servicefabricapplicationpackage?view=azureservicefabricps) cmdlet.

Olá [ServiceFabricApplicationPackage cópia](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) comando carregamentos Olá repositório de imagem do aplicativo pacotes toohello cluster.
Olá **ImageStoreConnectionStringFromClusterManifest Get** cmdlet, que é parte do módulo do PowerShell do SDK do Service Fabric Olá, é a imagem de saudação do tooget usado armazenar a cadeia de caracteres de conexão.  módulo SDK em Olá tooimport, execute:

```powershell
Import-Module "$ENV:ProgramFiles\Microsoft SDKs\Service Fabric\Tools\PSModule\ServiceFabricSDK\ServiceFabricSDK.psm1"
```

Suponha que você crie e empacote um aplicativo chamado *MyApplication* no Visual Studio 2015. Por padrão, o nome do tipo de aplicativo hello listado no hello ApplicationManifest.xml é "MyApplicationType".  Olá pacote de aplicativo, que contém o manifesto de aplicativo necessário hello, manifestos do serviço e pacotes de dados/de configuração de código, está localizado em *C:\Users\<username\>\Documents\Visual 2015\Projects\ Studio MyApplication\MyApplication\pkg\Debug*. 

Olá comando a seguir lista os conteúdos de Olá Olá do pacote de aplicativo:

```powershell
PS C:\> $path = 'C:\Users\<user\>\Documents\Visual Studio 2015\Projects\MyApplication\MyApplication\pkg\Debug'
PS C:\> tree /f $path
Folder PATH listing for volume OSDisk
Volume serial number is 0459-2393
C:\USERS\USER\DOCUMENTS\VISUAL STUDIO 2015\PROJECTS\MYAPPLICATION\MYAPPLICATION\PKG\DEBUG
│   ApplicationManifest.xml
│
└───Stateless1Pkg
    │   ServiceManifest.xml
    │
    ├───Code
    │       Microsoft.ServiceFabric.Data.dll
    │       Microsoft.ServiceFabric.Data.Interfaces.dll
    │       Microsoft.ServiceFabric.Internal.dll
    │       Microsoft.ServiceFabric.Internal.Strings.dll
    │       Microsoft.ServiceFabric.Services.dll
    │       ServiceFabricServiceModel.dll
    │       Stateless1.exe
    │       Stateless1.exe.config
    │       Stateless1.pdb
    │       System.Fabric.dll
    │       System.Fabric.Strings.dll
    │
    └───Config
            Settings.xml
```

Se o pacote de aplicativo hello é grande e/ou tem muitos arquivos, você pode [compactá-los](service-fabric-package-apps.md#compress-a-package). compactação de saudação reduz o tamanho de saudação e número de saudação de arquivos.
Olá, efeito colateral é que hello cancelamento do registro e registrar o tipo de aplicativo são mais rápidos. Tempo de carregamento pode ser mais lento no momento, especialmente se você incluir o pacote de saudação do hello tempo toocompress. 

toocompress um pacote, use Olá mesmo [ServiceFabricApplicationPackage cópia](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) comando. A compactação pode ser feita separado de carregamento, usando Olá `SkipCopy` sinalizador ou junto com hello operação de carregamento. Aplicar compactação em um pacote compactado é não operacional.
um pacote compactado, o uso de toouncompress Olá mesmo [cópia ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) com hello `UncompressPackage` alternar.

Olá cmdlet a seguir compacta pacote hello sem copiá-lo toohello repositório de imagens. pacote de saudação agora inclui os arquivos compactados para Olá `Code` e `Config` pacotes. Olá manifestos de aplicativo e Olá service não estão compactados, porque eles são necessários para várias operações internas (como compartilhamento de extração de versão e o nome de tipo de aplicativo para determinados validações de pacote). Manifestos de compactação Olá tornaria essas operações ineficiente.

```
PS C:\> Copy-ServiceFabricApplicationPackage -ApplicationPackagePath $path -CompressPackage -SkipCopy
PS C:\> tree /f $path
Folder PATH listing for volume OSDisk
Volume serial number is 0459-2393
C:\USERS\USER\DOCUMENTS\VISUAL STUDIO 2015\PROJECTS\MYAPPLICATION\MYAPPLICATION\PKG\DEBUG
|   ApplicationManifest.xml
|
└───Stateless1Pkg
       Code.zip
       Config.zip
       ServiceManifest.xml
```

Para pacotes de aplicativo grande, a compactação Olá leva tempo. Para obter melhores resultados, use uma unidade SSD rápida. tempos de compactação de Hello e tamanho de saudação do pacote compactado Olá também variam com base no conteúdo do pacote de saudação.
Por exemplo, aqui está o estatísticas de compactação para alguns pacotes, que mostram a saudação inicial e Olá tamanho de pacote compactado, com tempo de compactação de saudação.

|Tamanho inicial (MB)|Contagem de arquivos|Tempo de compactação|Tamanho do pacote compactado (MB)|
|----------------:|---------:|---------------:|---------------------------:|
|100|100|00:00:03.3547592|60|
|512|100|00:00:16.3850303|307|
|1.024|500|00:00:32.5907950|615|
|2.048|1000|00:01:04.3775554|1231|
|5012|100|00:02:45.2951288|3074|

Depois que um pacote é compactado, pode ser carregado tooone ou clusters de vários Service Fabric conforme necessário. mecanismo de implantação de saudação é o mesmo para os pacotes compactados e não compactados. Se o pacote de saudação for compactado, ela é armazenada como tal no repositório de imagens de cluster hello e é descompactado no nó de saudação antes que o aplicativo hello é executado.


Olá exemplo a seguir carrega repositório de imagens toohello do pacote hello, em uma pasta chamada "MyApplicationV1":

```powershell
PS C:\> Copy-ServiceFabricApplicationPackage -ApplicationPackagePath $path -ApplicationPackagePathInImageStore MyApplicationV1 -ImageStoreConnectionString (Get-ImageStoreConnectionStringFromClusterManifest(Get-ServiceFabricClusterManifest)) -TimeoutSec 1800
```

Olá **ImageStoreConnectionStringFromClusterManifest Get** cmdlet, que é parte do módulo do PowerShell do SDK do Service Fabric Olá, é a imagem de saudação do tooget usado armazenar a cadeia de caracteres de conexão.  módulo SDK em Olá tooimport, execute:

```powershell
Import-Module "$ENV:ProgramFiles\Microsoft SDKs\Service Fabric\Tools\PSModule\ServiceFabricSDK\ServiceFabricSDK.psm1"
```

Se você não especificar Olá *- ApplicationPackagePathInImageStore* parâmetro, pacote de aplicativo hello é copiado para hello "Depuração" no repositório de imagens de saudação.

Olá tempo tooupload um pacote difere dependendo de vários fatores. Alguns desses fatores são o número de saudação de arquivos no pacote de saudação, tamanho do pacote hello e tamanhos de arquivo hello. a velocidade da rede Olá entre máquina de origem hello e cluster do Service Fabric Olá também afeta o tempo de carregamento de saudação. Olá tempo limite padrão de [ServiceFabricApplicationPackage cópia](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) é de 30 minutos.
Dependendo Olá fatores descritos, você pode ter o tempo limite de saudação tooincrease. Se você estiver compactando pacote hello na chamada de cópia hello, será necessário tooalso considerar o tempo de compactação de saudação.

Consulte [entender a cadeia de conexão de repositório de imagens Olá](service-fabric-image-store-connection-string.md) para obter mais informações sobre repositório de imagens hello e imagem armazenam a cadeia de caracteres de conexão.

## <a name="register-hello-application-package"></a>Registrar pacote de aplicativo hello
tipo de aplicativo Hello e versão declarados no manifesto de aplicativo hello ficam disponível para uso quando o pacote de aplicativo hello está registrado. sistema Olá lê o pacote de saudação carregado na etapa anterior Olá, verifica o pacote de saudação, processa o conteúdo do pacote hello e copia o local do hello processado pacote tooan interno do sistema.  

Executar Olá [ServiceFabricApplicationType registro](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) tooregister cmdlet Olá tipo de aplicativo no cluster hello e disponibilizá-lo para implantação:

```powershell
PS C:\> Register-ServiceFabricApplicationType MyApplicationV1
Register application type succeeded
```

"MyApplicationV1" é a pasta de saudação no repositório de imagem Olá onde o pacote de aplicativo hello está localizado. saudação de tipo de aplicativo com o nome "MyApplicationType" e a versão "1.0.0" (ambos são encontradas no manifesto do aplicativo hello) agora é registrado no cluster de saudação.

Olá [ServiceFabricApplicationType registro](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) comando retorna somente depois que o sistema de saudação tem o pacote de aplicativo hello registrado com êxito. Quanto tempo leva de registro depende tamanho hello e o conteúdo do pacote de aplicativo hello. Se necessário, Olá **- TimeoutSec** parâmetro pode ser usado toosupply um tempo limite maior (tempo limite da saudação padrão é 60 segundos).

Se você tiver um aplicativo grande pacote ou se você estiver enfrentando tempos limite, use Olá **- Async** parâmetro. comando Olá retorna ao cluster Olá aceita o comando ' register ' hello, e o processamento de saudação continua conforme necessário.
Olá [ServiceFabricApplicationType Get](/powershell/module/servicefabric/get-servicefabricapplicationtype?view=azureservicefabricps) comando lista todas as versões do tipo de aplicativo registrado com êxito e seu status de registro. Você pode usar esse comando toodetermine ao Olá registro está pronto.

```powershell
PS C:\> Get-ServiceFabricApplicationType

ApplicationTypeName    : MyApplicationType
ApplicationTypeVersion : 1.0.0
Status                 : Available
DefaultParameters      : { "Stateless1_InstanceCount" = "-1" }
```

## <a name="create-hello-application"></a>Criar um aplicativo hello
Você pode instanciar um aplicativo de qualquer versão do tipo de aplicativo que foi registrado com êxito usando Olá [ServiceFabricApplication novo](/powershell/module/servicefabric/new-servicefabricapplication?view=azureservicefabricps) cmdlet. nome de saudação de cada aplicativo deve começar com hello *"fabric:"* esquema e deve ser exclusivo para cada instância do aplicativo. Todos os serviços padrão definidos no manifesto de aplicativo de saudação do tipo de aplicativo de destino Olá também são criados.

```powershell
PS C:\> New-ServiceFabricApplication fabric:/MyApp MyApplicationType 1.0.0

ApplicationName        : fabric:/MyApp
ApplicationTypeName    : MyApplicationType
ApplicationTypeVersion : 1.0.0
ApplicationParameters  : {}
```
Várias instâncias do aplicativo podem ser criadas para qualquer determinada versão de um tipo de aplicativo registrado. Cada instância do aplicativo é executada isoladamente, com seu próprio processo e diretório de trabalho.

toosee chamado aplicativos e serviços estão em execução no cluster hello, executar Olá [Get-ServiceFabricApplication](/powershell/servicefabric/vlatest/get-servicefabricapplication) e [ServiceFabricService Get](/powershell/module/servicefabric/get-servicefabricservice?view=azureservicefabricps) cmdlets:

```powershell
PS C:\> Get-ServiceFabricApplication  

ApplicationName        : fabric:/MyApp
ApplicationTypeName    : MyApplicationType
ApplicationTypeVersion : 1.0.0
ApplicationStatus      : Ready
HealthState            : Ok
ApplicationParameters  : {}

PS C:\> Get-ServiceFabricApplication | Get-ServiceFabricService

ServiceName            : fabric:/MyApp/Stateless1
ServiceKind            : Stateless
ServiceTypeName        : Stateless1Type
IsServiceGroup         : False
ServiceManifestVersion : 1.0.0
ServiceStatus          : Active
HealthState            : Ok
```

## <a name="remove-an-application"></a>Remover um aplicativo
Quando uma instância de aplicativo não for mais necessário, você poderá removê-lo permanentemente por nome usando Olá [ServiceFabricApplication remover](/powershell/module/servicefabric/remove-servicefabricapplication?view=azureservicefabricps) cmdlet. [Remover ServiceFabricApplication](/powershell/module/servicefabric/remove-servicefabricapplication?view=azureservicefabricps) remove automaticamente todos os serviços que pertencem a aplicativo toohello bem, permanentemente, removendo todos os estados de serviço. 

> [!WARNING]
> Essa operação não pode ser revertida e o estado do aplicativo não pode ser recuperado.

```powershell
PS C:\> Remove-ServiceFabricApplication fabric:/MyApp

Confirm
Continue with this operation?
[Y] Yes  [N] No  [S] Suspend  [?] Help (default is "Y"):
Remove application instance succeeded

PS C:\> Get-ServiceFabricApplication
```

## <a name="unregister-an-application-type"></a>Cancelar o registro de um tipo de aplicativo
Quando uma versão específica de um tipo de aplicativo não for mais necessário, você deve cancelar o registro do tipo de aplicativo hello usando Olá [ServiceFabricApplicationType Unregister](/powershell/module/servicefabric/unregister-servicefabricapplicationtype?view=azureservicefabricps) cmdlet. Cancelando o registro não usadas de aplicativo tipos versões espaço de armazenamento usado pelo repositório de imagem hello. Um tipo de aplicativo pode ter seu registro cancelado, desde que não existam aplicativos instanciados nele e nenhuma atualização de aplicativo pendente que faça referência a ele.

Executar [Get-ServiceFabricApplicationType](/powershell/module/servicefabric/get-servicefabricapplicationtype?view=azureservicefabricps) toosee Olá aplicativo atualmente registrados no cluster hello:

```powershell
PS C:\> Get-ServiceFabricApplicationType

ApplicationTypeName    : MyApplicationType
ApplicationTypeVersion : 1.0.0
Status                 : Available
DefaultParameters      : { "Stateless1_InstanceCount" = "-1" }
```

Executar [Unregister-ServiceFabricApplicationType](/powershell/module/servicefabric/unregister-servicefabricapplicationtype?view=azureservicefabricps) toounregister um tipo de aplicativo específico:

```powershell
PS C:\> Unregister-ServiceFabricApplicationType MyApplicationType 1.0.0
```

## <a name="remove-an-application-package-from-hello-image-store"></a>Remover um pacote de aplicativo hello do repositório de imagens
Quando um pacote de aplicativo não for mais necessário, você poderá excluí-la da saudação imagem repositório toofree recursos do sistema.

```powershell
PS C:\>Remove-ServiceFabricApplicationPackage -ApplicationPackagePathInImageStore MyApplicationV1 -ImageStoreConnectionString (Get-ImageStoreConnectionStringFromClusterManifest(Get-ServiceFabricClusterManifest))
```

## <a name="troubleshooting"></a>Solucionar problemas
### <a name="copy-servicefabricapplicationpackage-asks-for-an-imagestoreconnectionstring"></a>Copy-ServiceFabricApplicationPackage solicita um ImageStoreConnectionString
ambiente de SDK do Service Fabric Olá já deve ter Olá correto padrões configurar. Mas se necessário, Olá ImageStoreConnectionString para todos os comandos deve coincidir valor Olá que Olá malha do serviço de cluster está usando. Você pode encontrar hello ImageStoreConnectionString no manifesto do cluster hello, recuperadas usando Olá [Get-ServiceFabricClusterManifest](/powershell/module/servicefabric/get-servicefabricclustermanifest?view=azureservicefabricps) e comandos Get-ImageStoreConnectionStringFromClusterManifest:

```powershell
PS C:\> Get-ImageStoreConnectionStringFromClusterManifest(Get-ServiceFabricClusterManifest)
```

Olá **ImageStoreConnectionStringFromClusterManifest Get** cmdlet, que é parte do módulo do PowerShell do SDK do Service Fabric Olá, é a imagem de saudação do tooget usado armazenar a cadeia de caracteres de conexão.  módulo SDK em Olá tooimport, execute:

```powershell
Import-Module "$ENV:ProgramFiles\Microsoft SDKs\Service Fabric\Tools\PSModule\ServiceFabricSDK\ServiceFabricSDK.psm1"
```

Olá ImageStoreConnectionString foi encontrado no manifesto do cluster hello:

```xml
<ClusterManifest xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" Name="Server-Default-SingleNode" Version="1.0" xmlns="http://schemas.microsoft.com/2011/01/fabric">

    [...]

    <Section Name="Management">
      <Parameter Name="ImageStoreConnectionString" Value="file:D:\ServiceFabric\Data\ImageStore" />
    </Section>

    [...]
```

Consulte [entender a cadeia de conexão de repositório de imagens Olá](service-fabric-image-store-connection-string.md) para obter mais informações sobre repositório de imagens hello e imagem armazenam a cadeia de caracteres de conexão.

### <a name="deploy-large-application-package"></a>Implantar um pacote de aplicativos grande
Problema: [Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) atinge o tempo limite para um pacote de aplicativos grande (na ordem de GB).
Experimente:
- Especificar um tempo limite maior para o comando [Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) com o parâmetro `TimeoutSec`. Por padrão, o tempo limite de saudação é 30 minutos.
- Verifique a conexão de rede de saudação entre o computador de origem e o cluster. Se a conexão de saudação estiver lenta, considere o uso de uma máquina com uma conexão de rede melhor.
Se máquina do cliente Olá for em outra região de cluster hello, considere usando um computador cliente em uma região mais próxima ou mesmo como cluster hello.
- Verifique se você está sofrendo limitação externa. Por exemplo, quando o repositório de imagens Olá é armazenamento toouse configurada do azure, carregamento pode ser limitado.

Problema: o upload do pacote foi concluído com êxito, mas [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) atingiu o tempo limite. Experimente:
- [Compactar pacote hello](service-fabric-package-apps.md#compress-a-package) antes de copiar toohello repositório de imagens.
compactação Olá reduz o tamanho do hello e Olá vários arquivos, que por sua vez reduz a quantidade de saudação do tráfego e funciona malha esse serviço devem executar. operação de carregamento de saudação pode ser mais lenta (especialmente se você incluir o tempo de compactação de saudação), mas o tipo de aplicativo hello registrar e cancelar o registro são mais rápidos.
- Especificar um tempo limite maior para o comando [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) com o parâmetro `TimeoutSec`.
- Especifique a opção `Async` para [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps). comando Olá retorna quando o cluster Olá aceita o comando hello e registro de saudação do tipo de aplicativo hello continua assincronamente. Por esse motivo, há toospecify sem necessidade de um tempo limite maior nesse caso. Olá [ServiceFabricApplicationType Get](/powershell/module/servicefabric/get-servicefabricapplicationtype?view=azureservicefabricps) comando lista todas as versões do tipo de aplicativo registrado com êxito e seu status de registro. Você pode usar esse comando toodetermine ao Olá registro está pronto.

```powershell
PS C:\> Get-ServiceFabricApplicationType

ApplicationTypeName    : MyApplicationType
ApplicationTypeVersion : 1.0.0
Status                 : Available
DefaultParameters      : { "Stateless1_InstanceCount" = "-1" }
```

### <a name="deploy-application-package-with-many-files"></a>Implantar pacote de aplicativos com muitos arquivos
Problema: [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) atinge o tempo limite para um pacote de aplicativos com muitos arquivos (na ordem de milhares).
Experimente:
- [Compactar pacote hello](service-fabric-package-apps.md#compress-a-package) antes de copiar toohello repositório de imagens. compactação de saudação reduz o número de saudação de arquivos.
- Especificar um tempo limite maior para o comando [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) com o parâmetro `TimeoutSec`.
- Especifique a opção `Async` para [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps). comando Olá retorna quando o cluster Olá aceita o comando hello e registro de saudação do tipo de aplicativo hello continua assincronamente.
Por esse motivo, há toospecify sem necessidade de um tempo limite maior nesse caso. Olá [ServiceFabricApplicationType Get](/powershell/module/servicefabric/get-servicefabricapplicationtype?view=azureservicefabricps) comando lista todas as versões do tipo de aplicativo registrado com êxito e seu status de registro. Você pode usar esse comando toodetermine ao Olá registro está pronto.

```powershell
PS C:\> Get-ServiceFabricApplicationType

ApplicationTypeName    : MyApplicationType
ApplicationTypeVersion : 1.0.0
Status                 : Available
DefaultParameters      : { "Stateless1_InstanceCount" = "-1" }
```

## <a name="next-steps"></a>Próximas etapas
[Atualização de aplicativos do Service Fabric](service-fabric-application-upgrade.md)

[Introdução à integridade da Malha do Serviço](service-fabric-health-introduction.md)

[Diagnosticar e solucionar problemas de um serviço da Malha do Serviço](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)

[Modelar um aplicativo na Malha do Serviço](service-fabric-application-model.md)

<!--Link references--In actual articles, you only need a single period before hello slash-->
[10]: service-fabric-application-model.md
[11]: service-fabric-application-upgrade.md
