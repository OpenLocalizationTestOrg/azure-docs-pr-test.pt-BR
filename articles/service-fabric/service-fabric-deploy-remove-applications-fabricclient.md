---
title: "aaaAzure implantação de aplicativos do Service Fabric | Microsoft Docs"
description: "Use Olá toodeploy FabricClient APIs e remover aplicativos na malha do serviço."
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
ms.date: 07/07/2017
ms.author: ryanwi
ms.openlocfilehash: b2986b71c461f3e785ba16ec1b827fe47ad852fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-remove-applications-using-fabricclient"></a>Implantar e remover aplicativos usando FabricClient
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
Conecte-se o cluster toohello criando um [FabricClient](/dotnet/api/system.fabric.fabricclient) instância antes de executar qualquer uma das Olá exemplos de código neste artigo. Para obter exemplos de cluster de desenvolvimento local tooa conexão ou um cluster remoto ou o cluster protegido usando o Active Directory do Azure, X509 certificados ou consulte Active Directory do Windows [conectar tooa segura cluster](service-fabric-connect-to-secure-cluster.md#connect-to-a-cluster-using-the-fabricclient-apis). cluster de desenvolvimento local em toohello tooconnect, execute Olá seguinte:

```csharp
// Connect toohello local cluster.
FabricClient fabricClient = new FabricClient();
```

## <a name="upload-hello-application-package"></a>Carregar pacote de aplicativo hello
Suponha que você crie e empacote um aplicativo chamado *MyApplication* no Visual Studio. Por padrão, o nome do tipo de aplicativo hello listado no hello ApplicationManifest.xml é "MyApplicationType".  Olá pacote de aplicativo, que contém o manifesto de aplicativo necessário hello, manifestos do serviço e pacotes de dados/de configuração de código, está localizado em *C:\Users\&lt; nome de usuário&gt;\Documents\Visual 2017\Projects\ Studio MyApplication\MyApplication\pkg\Debug*.

Carregar pacote de aplicativo hello coloca em um local que seja acessível pelos componentes do hello internos do Service Fabric. Serviço de malha verifica o pacote de aplicativo hello durante o registro de saudação do pacote de aplicativo hello. No entanto, se você quiser tooverify Olá pacote do aplicativo localmente (ou seja, antes de carregar), use Olá [ServiceFabricApplicationPackage teste](/powershell/module/servicefabric/test-servicefabricapplicationpackage?view=azureservicefabricps) cmdlet.

Olá [CopyApplicationPackage](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.copyapplicationpackage) API carrega o repositório de imagens do hello aplicativo pacote toohello cluster. 

Se o pacote de aplicativo hello é grande e/ou tem muitos arquivos, você pode [compactá-los](service-fabric-package-apps.md#compress-a-package) e copie-o repositório de imagens toohello usando o PowerShell. compactação de saudação reduz o tamanho de saudação e número de saudação de arquivos.

Consulte [entender a cadeia de conexão de repositório de imagens Olá](service-fabric-image-store-connection-string.md) para obter mais informações sobre repositório de imagens hello e imagem armazenam a cadeia de caracteres de conexão.

## <a name="register-hello-application-package"></a>Registrar pacote de aplicativo hello
tipo de aplicativo Hello e versão declarados no manifesto de aplicativo hello ficam disponível para uso quando o pacote de aplicativo hello está registrado. sistema Olá lê o pacote de saudação carregado na etapa anterior Olá, verifica o pacote de saudação, processa o conteúdo do pacote hello e copia o local do hello processado pacote tooan interno do sistema.  

Olá [ProvisionApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.provisionapplicationasync) API registra Olá tipo de aplicativo no cluster hello e disponibilizá-lo para implantação.

Olá [GetApplicationTypeListAsync](/dotnet/api/system.fabric.fabricclient.queryclient.getapplicationtypelistasync) API fornece informações sobre todos os tipos de aplicativo registrado com êxito. Você pode usar essa API toodetermine quando é feito registro hello.

## <a name="create-an-application-instance"></a>Criar uma instância do aplicativo
Você pode instanciar um aplicativo de qualquer tipo de aplicativo que foi registrado com êxito usando Olá [CreateApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.createapplicationasync) API. nome de saudação de cada aplicativo deve começar com hello *"fabric:"* esquema e deve ser exclusivo para cada instância do aplicativo (dentro de um cluster). Todos os serviços padrão definidos no manifesto de aplicativo de saudação do tipo de aplicativo de destino Olá também são criados.

Várias instâncias do aplicativo podem ser criadas para qualquer determinada versão de um tipo de aplicativo registrado. Cada instância do aplicativo é executada isoladamente, com seu próprio diretório de trabalho e conjunto de processos.

toosee chamado aplicativos e serviços estão em execução no cluster hello, executar Olá [GetApplicationListAsync](/dotnet/api/system.fabric.fabricclient.queryclient.getapplicationlistasync) e [GetServiceListAsync](/dotnet/api/system.fabric.fabricclient.queryclient.getservicelistasync) APIs.

## <a name="create-a-service-instance"></a>Crie uma instância de serviço
Você pode instanciar um serviço de um tipo de serviço usando Olá [CreateServiceAsync](/dotnet/api/system.fabric.fabricclient.servicemanagementclient.createserviceasync) API.  Se o serviço de saudação é declarado como um serviço padrão no manifesto de aplicativo hello, serviço Olá é instanciado quando o aplicativo hello é instanciado.  Olá chamada [CreateServiceAsync](/dotnet/api/system.fabric.fabricclient.servicemanagementclient.createserviceasync) API para um serviço que já é instanciado retornará uma exceção do tipo FabricException que contém um código de erro com um valor de FabricErrorCode.ServiceAlreadyExists.

## <a name="remove-a-service-instance"></a>Remover uma instância de serviço
Quando uma instância de serviço não for mais necessário, você poderá removê-lo da saudação executando a instância do aplicativo por chamada hello [DeleteServiceAsync](/dotnet/api/system.fabric.fabricclient.servicemanagementclient.deleteserviceasync) API.  

> [!WARNING]
> Essa operação não pode ser revertida e o estado do serviço não pode ser recuperado.

## <a name="remove-an-application-instance"></a>Remover uma instância do aplicativo
Quando uma instância de aplicativo não for mais necessário, você poderá removê-lo permanentemente por nome usando Olá [DeleteApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.deleteapplicationasync) API. [DeleteApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.deleteapplicationasync) remove automaticamente todos os serviços que pertencem a aplicativo toohello bem, permanentemente, removendo todos os estados de serviço.

> [!WARNING]
> Essa operação não pode ser revertida e o estado do aplicativo não pode ser recuperado.

## <a name="unregister-an-application-type"></a>Cancelar o registro de um tipo de aplicativo
Quando uma versão específica de um tipo de aplicativo não for mais necessário, você deve cancelar o registro dessa versão específica do tipo de aplicativo hello usando Olá [Unregister-ServiceFabricApplicationType](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.unprovisionapplicationasync) API. Versões não utilizadas ao cancelar o registro aplicativo tipos versões de espaço de armazenamento usado pelo repositório de imagens de saudação. Uma versão de um tipo de aplicativo pode ser cancelada, desde que nenhum aplicativo é instanciado em relação a essa versão do tipo de aplicativo hello e nenhuma atualização de aplicativo está fazendo referência a essa versão do tipo de aplicativo hello.

## <a name="remove-an-application-package-from-hello-image-store"></a>Remover um pacote de aplicativo hello do repositório de imagens
Quando um pacote de aplicativo não for mais necessário, você poderá excluí-la da saudação imagem repositório toofree recursos do sistema usando Olá [RemoveApplicationPackage](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.removeapplicationpackage) API.

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
Problema: a API [CopyApplicationPackage](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.copyapplicationpackage) atinge o tempo limite para um pacote de aplicativos grande (na ordem de GB).
Experimente:
- Especificar um tempo limite maior para o método [CopyApplicationPackage](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.copyapplicationpackage) com o parâmetro `timeout`. Por padrão, o tempo limite de saudação é 30 minutos.
- Verifique a conexão de rede de saudação entre o computador de origem e o cluster. Se a conexão de saudação estiver lenta, considere o uso de uma máquina com uma conexão de rede melhor.
Se máquina do cliente Olá for em outra região de cluster hello, considere usando um computador cliente em uma região mais próxima ou mesmo como cluster hello.
- Verifique se você está sofrendo limitação externa. Por exemplo, quando o repositório de imagens Olá é armazenamento toouse configurada do azure, carregamento pode ser limitado.

Problema: o upload do pacote foi concluído com êxito, mas a API [ProvisionApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.provisionapplicationasync) atinge o tempo limite. Experimente:
- [Compactar pacote hello](service-fabric-package-apps.md#compress-a-package) antes de copiar toohello repositório de imagens.
compactação Olá reduz o tamanho do hello e Olá vários arquivos, que por sua vez reduz a quantidade de saudação do tráfego e funciona malha esse serviço devem executar. operação de carregamento de saudação pode ser mais lenta (especialmente se você incluir o tempo de compactação de saudação), mas o tipo de aplicativo hello registrar e cancelar o registro são mais rápidos.
- Especifique um tempo limite maior para a API [ProvisionApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.provisionapplicationasync) com o parâmetro `timeout`.

### <a name="deploy-application-package-with-many-files"></a>Implantar pacote de aplicativos com muitos arquivos
Problema: [ProvisionApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.provisionapplicationasync) atinge o tempo limite para um pacote de aplicativos com muitos arquivos (na ordem de milhares).
Experimente:
- [Compactar pacote hello](service-fabric-package-apps.md#compress-a-package) antes de copiar toohello repositório de imagens. compactação de saudação reduz o número de saudação de arquivos.
- Especifique um tempo limite maior para [ProvisionApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.provisionapplicationasync) com o parâmetro `timeout`.

## <a name="code-example"></a>Exemplo de código
Olá exemplo a seguir copia um repositório de imagens de toohello de pacote de aplicativo, provisiona o tipo de aplicativo hello, cria uma instância de aplicativo, cria uma instância de serviço, remove a instância do aplicativo de hello, cancelar provisiona tipo de aplicativo hello, e Exclui o pacote de aplicativo Olá Olá do repositório de imagens.

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Reflection;
using System.Threading.Tasks;

using System.Fabric;
using System.Fabric.Description;
using System.Threading;

namespace ServiceFabricAppLifecycle
{
class Program
{
static void Main(string[] args)
{

    string clusterConnection = "localhost:19000";
    string appName = "fabric:/MyApplication";
    string appType = "MyApplicationType";
    string appVersion = "1.0.0";
    string serviceName = "fabric:/MyApplication/Stateless1";
    string imageStoreConnectionString = "file:C:\\SfDevCluster\\Data\\ImageStoreShare";
    string packagePathInImageStore = "MyApplication";
    string packagePath = "C:\\Users\\username\\Documents\\Visual Studio 2017\\Projects\\MyApplication\\MyApplication\\pkg\\Debug";
    string serviceType = "Stateless1Type";

    // Connect toohello cluster.
    FabricClient fabricClient = new FabricClient(clusterConnection);

    // Copy hello application package tooa location in hello image store
    try
    {
        fabricClient.ApplicationManager.CopyApplicationPackage(imageStoreConnectionString, packagePath, packagePathInImageStore);
        Console.WriteLine("Application package copied too{0}", packagePathInImageStore);
    }
    catch (AggregateException ae)
    {
        Console.WriteLine("Application package copy tooImage Store failed: ");
        foreach (Exception ex in ae.InnerExceptions)
        {
            Console.WriteLine("HResult: {0} Message: {1}", ex.HResult, ex.Message);
        }
    }

    // Provision hello application.  "MyApplicationV1" is hello folder in hello image store where hello application package is located. 
    // hello application type with name "MyApplicationType" and version "1.0.0" (both are found in hello application manifest) 
    // is now registered in hello cluster.            
    try
    {
        fabricClient.ApplicationManager.ProvisionApplicationAsync(packagePathInImageStore).Wait();

        Console.WriteLine("Provisioned application type {0}", packagePathInImageStore);
    }
    catch (AggregateException ae)
    {
        Console.WriteLine("Provision Application Type failed:");

        foreach (Exception ex in ae.InnerExceptions)
        {
            Console.WriteLine("HResult: {0} Message: {1}", ex.HResult, ex.Message);
        }
    }

    //  Create hello application instance.
    try
    {
        ApplicationDescription appDesc = new ApplicationDescription(new Uri(appName), appType, appVersion);
        fabricClient.ApplicationManager.CreateApplicationAsync(appDesc).Wait();
        Console.WriteLine("Created application instance of type {0}, version {1}", appType, appVersion);
    }
    catch (AggregateException ae)
    {
        Console.WriteLine("CreateApplication failed.");
        foreach (Exception ex in ae.InnerExceptions)
        {
            Console.WriteLine("HResult: {0} Message: {1}", ex.HResult, ex.Message);
        }
    }

    // Create hello stateless service description.  For stateful services, use a StatefulServiceDescription object.
    StatelessServiceDescription serviceDescription = new StatelessServiceDescription();
    serviceDescription.ApplicationName = new Uri(appName);
    serviceDescription.InstanceCount = 1;
    serviceDescription.PartitionSchemeDescription = new SingletonPartitionSchemeDescription();
    serviceDescription.ServiceName = new Uri(serviceName);
    serviceDescription.ServiceTypeName = serviceType;

    // Create hello service instance.  If hello service is declared as a default service in hello ApplicationManifest.xml,
    // hello service instance is already running and this call will fail.
    try
    {
        fabricClient.ServiceManager.CreateServiceAsync(serviceDescription).Wait();
        Console.WriteLine("Created service instance {0}", serviceName);
    }
    catch (AggregateException ae)
    {
        Console.WriteLine("CreateService failed.");
        foreach (Exception ex in ae.InnerExceptions)
        {
            Console.WriteLine("HResult: {0} Message: {1}", ex.HResult, ex.Message);
        }
    }

    // Delete a service instance.
    try
    {
        DeleteServiceDescription deleteServiceDescription = new DeleteServiceDescription(new Uri(serviceName));

        fabricClient.ServiceManager.DeleteServiceAsync(deleteServiceDescription);
        Console.WriteLine("Deleted service instance {0}", serviceName);
    }
    catch (AggregateException ae)
    {
        Console.WriteLine("DeleteService failed.");
        foreach (Exception ex in ae.InnerExceptions)
        {
            Console.WriteLine("HResult: {0} Message: {1}", ex.HResult, ex.Message);
        }
    }

    // Delete an application instance from hello application type.
    try
    {
        DeleteApplicationDescription deleteApplicationDescription = new DeleteApplicationDescription(new Uri(appName));

        fabricClient.ApplicationManager.DeleteApplicationAsync(deleteApplicationDescription).Wait();
        Console.WriteLine("Deleted application instance {0}", appName);
    }
    catch (AggregateException ae)
    {
        Console.WriteLine("DeleteApplication failed.");
        foreach (Exception ex in ae.InnerExceptions)
        {
            Console.WriteLine("HResult: {0} Message: {1}", ex.HResult, ex.Message);
        }
    }

    // Un-provision hello application type.
    try
    {
        fabricClient.ApplicationManager.UnprovisionApplicationAsync(appType, appVersion).Wait();
        Console.WriteLine("Un-provisioned application type {0}, version {1}", appType, appVersion);
    }
    catch (AggregateException ae)
    {
        Console.WriteLine("Un-provision application type failed: ");
        foreach (Exception ex in ae.InnerExceptions)
        {
            Console.WriteLine("HResult: {0} Message: {1}", ex.HResult, ex.Message);
        }
    }

    // Delete hello application package from a location in hello image store.
    try
    {
        fabricClient.ApplicationManager.RemoveApplicationPackage(imageStoreConnectionString, packagePathInImageStore);
        Console.WriteLine("Application package removed from {0}", packagePathInImageStore);
    }
    catch (AggregateException ae)
    {
        Console.WriteLine("Application package removal from Image Store failed: ");
        foreach (Exception ex in ae.InnerExceptions)
        {
            Console.WriteLine("HResult: {0} Message: {1}", ex.HResult, ex.Message);
        }
    }

    Console.WriteLine("Hit enter...");
    Console.Read();
}        
}
}

```

## <a name="next-steps"></a>Próximas etapas
[Atualização de aplicativos do Service Fabric](service-fabric-application-upgrade.md)

[Introdução à integridade da Malha do Serviço](service-fabric-health-introduction.md)

[Diagnosticar e solucionar problemas de um serviço da Malha do Serviço](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)

[Modelar um aplicativo na Malha do Serviço](service-fabric-application-model.md)

<!--Link references--In actual articles, you only need a single period before hello slash-->
[10]: service-fabric-application-model.md
[11]: service-fabric-application-upgrade.md
