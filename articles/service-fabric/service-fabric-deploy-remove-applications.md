---
title: "Implantação de aplicativos do Azure Service Fabric | Microsoft Docs"
description: Como implantar e remover aplicativos no Service Fabric usando o PowerShell.
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
ms.date: 01/19/2018
ms.author: ryanwi
ms.openlocfilehash: cd3c97bc95fb7ccfaa0dbf2d7ca76ae598a4b320
ms.sourcegitcommit: 817c3db817348ad088711494e97fc84c9b32f19d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/20/2018
---
# <a name="deploy-and-remove-applications-using-powershell"></a>Implantar e remover aplicativos usando o PowerShell
> [!div class="op_single_selector"]
> * [Resource Manager](service-fabric-application-arm-resource.md)
> * [PowerShell](service-fabric-deploy-remove-applications.md)
> * [CLI do Service Fabric](service-fabric-application-lifecycle-sfctl.md)
> * [APIs de FabricClient](service-fabric-deploy-remove-applications-fabricclient.md)

<br/>

Assim que um [tipo de aplicativo for empacotado][10], ele está pronto para implantação em um cluster do Azure Service Fabric. A implantação envolve as três etapas a seguir:

1. Carregue o pacote de aplicativos no repositório de imagens.
2. Registre o tipo do aplicativo com o caminho relativo do repositório de imagens.
3. Crie a instância do aplicativo.

Depois que o aplicativo implantado não é mais necessário, você pode excluir a instância do aplicativo e seu tipo de aplicativo. Remover completamente um aplicativo do cluster envolve as seguintes etapas:

1. Remova (ou exclua) a execução da instância do aplicativo.
2. Cancele o registro do tipo de aplicativo se você não precisar mais dele.
3. Remova o pacote de aplicativos do repositório de imagens.

Se você usar o Visual Studio para implantar e depurar aplicativos no cluster de desenvolvimento local, todas as etapas anteriores serão tratadas automaticamente por meio de um script do PowerShell.  Esse script é encontrado na pasta *Scripts* do projeto do aplicativo. Este artigo fornece informações sobre o que esse script faz para que você possa executar as mesmas operações fora do Visual Studio. 

Outra maneira de implantar um aplicativo é usando o provisionamento externo. O pacote de aplicativos pode ser [empacotado como `sfpkg` ](service-fabric-package-apps.md#create-an-sfpkg) e carregado em um repositório externo. Nesse caso, o carregamento para o repositório de imagens não é necessário. A implantação precisa das etapas a seguir:

1. Carregar o `sfpkg` em um repositório externo. O repositório externo pode ser qualquer repositório que exponha um ponto de extremidade do REST http ou https.
2. Registre o tipo de aplicativo usando o URI de download externo e as informações de tipo de aplicativo.
2. Crie a instância do aplicativo.

Para limpeza, remova as instâncias do aplicativo e cancele o registro do tipo de aplicativo. Como o pacote não foi copiado para o repositório de imagens, não há nenhum local temporário para limpeza. O provisionamento de repositório externo está disponível a partir do Service Fabric versão 6.1.

>[!NOTE]
> Atualmente o Visual Studio não oferece suporte para o provisionamento externo.

 
## <a name="connect-to-the-cluster"></a>Conectar-se ao cluster
Antes de executar qualquer comando do PowerShell neste artigo, sempre comece usando [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) para se conectar ao cluster do Service Fabric. Para se conectar ao cluster de desenvolvimento local, execute o seguinte:

```powershell
PS C:\>Connect-ServiceFabricCluster
```

Para obter exemplos de como se conectar a um cluster remoto ou protegido usando o Azure Active Directory, certificados X509 ou Active Directory do Windows, veja [Conectar-se a um cluster seguro](service-fabric-connect-to-secure-cluster.md).

## <a name="upload-the-application-package"></a>Carregar o pacote de aplicativos
O carregamento do pacote de aplicativos coloca-o em um local acessível por componentes internos do Service Fabric.
Se quiser verificar o pacote de aplicativos localmente, use o cmdlet [Test-ServiceFabricApplicationPackage](/powershell/module/servicefabric/test-servicefabricapplicationpackage?view=azureservicefabricps).

O comando [Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) carrega o pacote do aplicativo para o Repositório de Imagens do cluster.

Suponha que você crie e empacote um aplicativo chamado *MyApplication* no Visual Studio 2015. Por padrão, o nome do tipo de aplicativo listado no ApplicationManifest.xml é "MyApplicationType".  O pacote de aplicativos, que contém o manifesto do aplicativo, os manifestos de serviço e os pacotes de códigos/configurações/dados necessários, está localizado em *C:\Users\\<nome de usuário\>\Documents\Visual Studio 2015\Projects\MyApplication\MyApplication\pkg\Debug*. 

O comando a seguir lista o conteúdo do pacote de aplicativos:

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

Se o pacote de aplicativos for grande e/ou tiver vários arquivos, você poderá [compactá-lo](service-fabric-package-apps.md#compress-a-package). A compactação reduz o tamanho e o número de arquivos.
O efeito colateral é que o registro e o cancelamento do registro do tipo de aplicativo são mais rápidos. O tempo de upload poderá ser mais lento atualmente, especialmente se você incluir o tempo usado para compactar o pacote. 

Para compactar um pacote, use o mesmo comando [Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps). A compactação pode ser feita separadamente do upload pelo uso do sinalizador `SkipCopy` ou então junto com a operação de upload. Aplicar compactação em um pacote compactado é não operacional.
Para descompactar um pacote compactado, use o mesmo comando [Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) com a opção `UncompressPackage`.

O cmdlet a seguir compacta o pacote sem copiá-lo para o repositório de imagens. O pacote agora inclui arquivos compactados para os pacotes `Code` e `Config`. O aplicativo e os manifestos do serviço não são compactados porque eles são necessários para várias operações internas (como compartilhamento do pacote, extração da versão e nome do tipo de aplicativo para determinadas validações). Compactar os manifestos tornaria essas operações ineficientes.

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

Para pacotes de aplicativos grandes, a compactação leva tempo. Para obter melhores resultados, use uma unidade SSD rápida. Os tempos de compactação e o tamanho do pacote compactado também diferem com base no conteúdo do pacote.
Por exemplo, eis aqui as estatísticas de compactação para alguns pacotes, que mostram o tamanho a inicial e o do pacote compactado, com o tempo de compactação.

|Tamanho inicial (MB)|Contagem de arquivos|Tempo de compactação|Tamanho do pacote compactado (MB)|
|----------------:|---------:|---------------:|---------------------------:|
|100|100|00:00:03.3547592|60|
|512|100|00:00:16.3850303|307|
|1.024|500|00:00:32.5907950|615|
|2.048|1000|00:01:04.3775554|1231|
|5012|100|00:02:45.2951288|3074|

Depois que um pacote é compactado, ele pode ser carregado para um ou vários clusters do Service Fabric conforme necessário. O mecanismo de implantação é o mesmo para pacotes compactados e não compactados. Pacotes compactados são armazenados como tal no repositório de imagens do cluster. Os pacotes são descompactados no nó, antes do aplicativo ser executado.


O exemplo a seguir carrega o pacote para o armazenamento de imagens em uma pasta chamada "MyApplicationV1":

```powershell
PS C:\> Copy-ServiceFabricApplicationPackage -ApplicationPackagePath $path -ApplicationPackagePathInImageStore MyApplicationV1 -TimeoutSec 1800
```

Se você não especificar o parâmetro *-ApplicationPackagePathInImageStore*, o pacote de aplicativos será copiado para a pasta "Debug" no repositório de imagens.

>[!NOTE]
>O **Copy-ServiceFabricApplicationPackage** detectará automaticamente a cadeia de conexão do repositório de imagens adequada se a sessão do PowerShell estiver conectada a um cluster do Service Fabric. Para versões do Service Fabric anteriores à 5.6, o argumento **-ImageStoreConnectionString** deve ser fornecido explicitamente.
>
>```powershell
>PS C:\> Copy-ServiceFabricApplicationPackage -ApplicationPackagePath $path -ApplicationPackagePathInImageStore MyApplicationV1 -ImageStoreConnectionString (Get-ImageStoreConnectionStringFromClusterManifest(Get-ServiceFabricClusterManifest)) -TimeoutSec 1800
>```
>
>O cmdlet **Get-ImageStoreConnectionStringFromClusterManifest** , que faz parte do módulo do PowerShell do SDK do Service Fabric, é usado para obter a cadeia de conexão do repositório de imagens.  Para importar o módulo do SDK, execute:
>
>```powershell
>Import-Module "$ENV:ProgramFiles\Microsoft SDKs\Service Fabric\Tools\PSModule\ServiceFabricSDK\ServiceFabricSDK.psm1"
>```
>
>Confira [Noções básicas sobre a configuração ImageStoreConnectionString](service-fabric-image-store-connection-string.md) para obter informações suplementares sobre o repositório de imagens e a cadeia de conexão de armazenamento de imagens.
>
>
>

O tempo necessário que leva para carregar um pacote difere, dependendo de vários fatores. Alguns desses fatores são o número de arquivos no pacote, o tamanho do pacote e os tamanhos dos arquivos. A velocidade da rede entre o computador de origem e o cluster do Service Fabric também afeta o tempo de upload. O tempo limite padrão para [Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) é de 30 minutos.
Dependendo dos fatores descritos, talvez você precise aumentar o tempo limite. Se você estiver compactando o pacote na chamada de cópia, você também precisará considerar o tempo de compactação.



## <a name="register-the-application-package"></a>Registrar o pacote de aplicativos
O tipo e a versão do aplicativo declarados no manifesto do aplicativo tornam-se disponíveis para uso quando o pacote de aplicativos é registrado. O sistema lê o pacote carregado na etapa anterior, verifica o pacote, processa o conteúdo do pacote e copia o pacote processado em um local interno do sistema.  

Execute o cmdlet [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) para registrar o tipo de aplicativo no cluster e disponibilizá-lo para implantação:

### <a name="register-the-application-package-copied-to-image-store"></a>Registrar o pacote de aplicativos copiado para o repositório de imagens
Quando um pacote foi copiado anteriormente para o repositório de imagens, a operação de registro especifica o caminho relativo no repositório de imagens.

```powershell
PS C:\> Register-ServiceFabricApplicationType -ApplicationPackagePathInImageStore MyApplicationV1
Register application type succeeded
```

"MyApplicationV1" é a pasta no repositório de imagens em que o pacote de aplicativos se encontra. O tipo de aplicativo com o nome "MyApplicationType" e a versão "1.0.0" (ambos são encontradas no manifesto do aplicativo) agora é registrado no cluster.

### <a name="register-the-application-package-copied-to-an-external-store"></a>Registrar o pacote de aplicativos copiado para um repositório externo
A partir do Service Fabric versão 6.1, o provisionamento oferece suporte para fazer o download do pacote de um repositório externo. O download do URI representa o caminho para o [ `sfpkg` pacote de aplicativos](service-fabric-package-apps.md#create-an-sfpkg) de onde o pacote de aplicativos pode ser baixado usando protocolos HTTP ou HTTPS. O pacote deve ter sido carregado anteriormente para esse local externo. O URI deve permitir o acesso de leitura para que o Service Fabric possa fazer o download do arquivo. O arquivo `sfpkg` deve ter a extensão ".sfpkg". A operação de provisionamento deve incluir as informações de tipo de aplicativo, como encontrado no manifesto do aplicativo.

```
PS C:\> Register-ServiceFabricApplicationType -ApplicationPackageDownloadUri "https://sftestresources.blob.core.windows.net:443/sfpkgholder/MyAppPackage.sfpkg" -ApplicationTypeName MyApp -ApplicationTypeVersion V1 -Async
```

O comando [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) retornará somente depois que o sistema tiver registrado com êxito o pacote de aplicativos. O tempo que se leva para o registro depende do tamanho e do conteúdo do pacote de aplicativos. O parâmetro **-TimeoutSec** pode ser usado para fornecer um tempo limite maior, se necessário (o tempo limite padrão é 60 segundos).

Se você tiver um pacote de aplicativos grande ou estiver experienciando tempos limite sendo atingidos, use o parâmetro **-Async**. O comando retorna quando o cluster aceita o comando de registro. A operação de registro continua conforme necessário.
O comando [Get-ServiceFabricApplicationType](/powershell/module/servicefabric/get-servicefabricapplicationtype?view=azureservicefabricps) lista todas as versões de tipo de aplicativo registradas com êxito e seus status de registro. Você pode usar esse comando para determinar quando o registro é feito.

```powershell
PS C:\> Get-ServiceFabricApplicationType

ApplicationTypeName    : MyApplicationType
ApplicationTypeVersion : 1.0.0
Status                 : Available
DefaultParameters      : { "Stateless1_InstanceCount" = "-1" }
```

## <a name="remove-an-application-package-from-the-image-store"></a>Remover um pacote de aplicativos do repositório de imagens
Se um pacote foi copiado para o repositório de imagens, você deve removê-lo do local temporário depois que o aplicativo for registrado com êxito. Excluir pacotes de aplicativos do repositório de imagens libera recursos do sistema. Manter pacotes de aplicativos não utilizados consome o armazenamento em disco e leva a problemas de desempenho do aplicativo.

```powershell
PS C:\>Remove-ServiceFabricApplicationPackage -ApplicationPackagePathInImageStore MyApplicationV1
```

## <a name="create-the-application"></a>Criar o aplicativo
É possível instanciar um aplicativo de qualquer versão do tipo de aplicativo registrada com êxito usando o cmdlet [New-ServiceFabricApplication](/powershell/module/servicefabric/new-servicefabricapplication?view=azureservicefabricps). O nome de cada aplicativo deve começar com o esquema *"fabric:"* e ser exclusivo para cada instância do aplicativo. Quaisquer serviços padrão definidos no manifesto do aplicativo do tipo de aplicativo de destino também são criados.

```powershell
PS C:\> New-ServiceFabricApplication fabric:/MyApp MyApplicationType 1.0.0

ApplicationName        : fabric:/MyApp
ApplicationTypeName    : MyApplicationType
ApplicationTypeVersion : 1.0.0
ApplicationParameters  : {}
```
Várias instâncias do aplicativo podem ser criadas para qualquer determinada versão de um tipo de aplicativo registrado. Cada instância do aplicativo é executada isoladamente, com seu próprio processo e diretório de trabalho.

Para ver quais apps e serviços nomeados estão em execução no cluster, execute os cmdlets [Get-ServiceFabricApplication](/powershell/servicefabric/vlatest/get-servicefabricapplication) e [Get-ServiceFabricService](/powershell/module/servicefabric/get-servicefabricservice?view=azureservicefabricps):

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
Quando uma instância de aplicativo não é mais necessária, você pode removê-la permanentemente pelo nome usando o cmdlet [Remove-ServiceFabricApplication](/powershell/module/servicefabric/remove-servicefabricapplication?view=azureservicefabricps). [Remove-ServiceFabricApplication](/powershell/module/servicefabric/remove-servicefabricapplication?view=azureservicefabricps) também remove automaticamente todos os serviços que pertencem ao aplicativo, removendo permanentemente todos os estados de serviço. 

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
Quando uma versão específica de um tipo de aplicativo não é mais necessária, cancele o registro do tipo de aplicativo usando o cmdlet [Unregister-ServiceFabricApplicationType](/powershell/module/servicefabric/unregister-servicefabricapplicationtype?view=azureservicefabricps). Cancelar o registro de tipos de aplicativos não utilizados libera espaço de armazenamento utilizado pelo repositório de imagens removendo os arquivos de tipo de aplicativo. Cancelar o registro de um tipo de aplicativo não remove o pacote de aplicativos copiado para o local temporário do repositório de imagens se a cópia para o repositório de imagens foi usada. Um tipo de aplicativo pode ter seu registro cancelado, desde que não existam aplicativos instanciados nele e nenhuma atualização de aplicativo pendente que faça referência a ele.

Execute [Get-ServiceFabricApplicationType](/powershell/module/servicefabric/get-servicefabricapplicationtype?view=azureservicefabricps) para ver os tipos de aplicativo registrados no cluster no momento:

```powershell
PS C:\> Get-ServiceFabricApplicationType

ApplicationTypeName    : MyApplicationType
ApplicationTypeVersion : 1.0.0
Status                 : Available
DefaultParameters      : { "Stateless1_InstanceCount" = "-1" }
```

Execute [Unregister-ServiceFabricApplicationType](/powershell/module/servicefabric/unregister-servicefabricapplicationtype?view=azureservicefabricps) para cancelar o registro de um tipo de aplicativo específico:

```powershell
PS C:\> Unregister-ServiceFabricApplicationType MyApplicationType 1.0.0
```

## <a name="troubleshooting"></a>solução de problemas
### <a name="copy-servicefabricapplicationpackage-asks-for-an-imagestoreconnectionstring"></a>Copy-ServiceFabricApplicationPackage solicita um ImageStoreConnectionString
O ambiente do SDK da Malha do Serviço já deve ter os padrões corretos configurados. Mas, se necessário, o ImageStoreConnectionString para todos os comandos deve corresponder ao valor que o cluster de Malha do Serviço está usando. Você pode encontrar ImageStoreConnectionString no manifesto do cluster, recuperado usando os comandos [Get-ServiceFabricClusterManifest](/powershell/module/servicefabric/get-servicefabricclustermanifest?view=azureservicefabricps) e Get-ImageStoreConnectionStringFromClusterManifest:

```powershell
PS C:\> Get-ImageStoreConnectionStringFromClusterManifest(Get-ServiceFabricClusterManifest)
```

O cmdlet **Get-ImageStoreConnectionStringFromClusterManifest** , que faz parte do módulo do PowerShell do SDK do Service Fabric, é usado para obter a cadeia de conexão do repositório de imagens.  Para importar o módulo do SDK, execute:

```powershell
Import-Module "$ENV:ProgramFiles\Microsoft SDKs\Service Fabric\Tools\PSModule\ServiceFabricSDK\ServiceFabricSDK.psm1"
```

ImageStoreConnectionString é encontrado no manifesto do cluster:

```xml
<ClusterManifest xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" Name="Server-Default-SingleNode" Version="1.0" xmlns="http://schemas.microsoft.com/2011/01/fabric">

    [...]

    <Section Name="Management">
      <Parameter Name="ImageStoreConnectionString" Value="file:D:\ServiceFabric\Data\ImageStore" />
    </Section>

    [...]
```

Confira [Noções básicas sobre a configuração ImageStoreConnectionString](service-fabric-image-store-connection-string.md) para obter informações suplementares sobre o repositório de imagens e a cadeia de conexão de armazenamento de imagens.

### <a name="deploy-large-application-package"></a>Implantar um pacote de aplicativos grande
Problema: [Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) atinge o tempo limite para um pacote de aplicativos grande (na ordem de GB).
Experimente:
- Especificar um tempo limite maior para o comando [Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) com o parâmetro `TimeoutSec`. Por padrão, o tempo limite é de 30 minutos.
- Verifique a conexão de rede entre o computador de origem e o cluster. Se a conexão estiver lenta, considere usar um computador com uma conexão de rede melhor.
Se o computador cliente estiver em uma região diferente do cluster, considere usar um computador cliente em uma região mais próxima ou na mesma que o cluster.
- Verifique se você está sofrendo limitação externa. Por exemplo, quando o repositório de imagens é configurado para usar o Armazenamento do Azure, o upload pode ser limitado.

Problema: o upload do pacote foi concluído com êxito, mas [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) atingiu o tempo limite. Experimente:
- [Compactar o pacote](service-fabric-package-apps.md#compress-a-package) antes de copiar para o repositório de imagens.
A compactação reduz o tamanho e o número de arquivos, o que por sua vez reduz a quantidade de tráfego e trabalho que o Service Fabric deve executar. A operação de upload pode ser mais lenta (especialmente se você incluir o tempo de compactação), mas as operações de registrar e cancelar o registro do tipo de aplicativo são mais rápidas.
- Especificar um tempo limite maior para o comando [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) com o parâmetro `TimeoutSec`.
- Especifique a opção `Async` para [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps). O comando retorna quando o cluster aceita o comando e o registro do tipo de aplicativo continua de modo assíncrono. Por esse motivo, não é necessário especificar um tempo limite maior nesse caso. O comando [Get-ServiceFabricApplicationType](/powershell/module/servicefabric/get-servicefabricapplicationtype?view=azureservicefabricps) lista todas as versões do tipo de aplicativo registradas com êxito e seu status de registro. Você pode usar esse comando para determinar quando o registro é feito.

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
- [Compactar o pacote](service-fabric-package-apps.md#compress-a-package) antes de copiar para o repositório de imagens. A compactação reduz o número de arquivos.
- Especificar um tempo limite maior para o comando [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) com o parâmetro `TimeoutSec`.
- Especifique a opção `Async` para [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps). O comando retorna quando o cluster aceita o comando e o registro do tipo de aplicativo continua de modo assíncrono.
Por esse motivo, não é necessário especificar um tempo limite maior nesse caso. O comando [Get-ServiceFabricApplicationType](/powershell/module/servicefabric/get-servicefabricapplicationtype?view=azureservicefabricps) lista todas as versões do tipo de aplicativo registradas com êxito e seu status de registro. Você pode usar esse comando para determinar quando o registro é feito.

```powershell
PS C:\> Get-ServiceFabricApplicationType

ApplicationTypeName    : MyApplicationType
ApplicationTypeVersion : 1.0.0
Status                 : Available
DefaultParameters      : { "Stateless1_InstanceCount" = "-1" }
```

## <a name="next-steps"></a>Próximas etapas
[Preparar um aplicativo](service-fabric-package-apps.md)

[Atualização de aplicativos do Service Fabric](service-fabric-application-upgrade.md)

[Introdução à integridade da Malha do Serviço](service-fabric-health-introduction.md)

[Diagnosticar e solucionar problemas de um serviço da Malha do Serviço](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)

[Modelar um aplicativo na Malha do Serviço](service-fabric-application-model.md)

<!--Link references--In actual articles, you only need a single period before the slash-->
[10]: service-fabric-package-apps.md
[11]: service-fabric-application-upgrade.md
