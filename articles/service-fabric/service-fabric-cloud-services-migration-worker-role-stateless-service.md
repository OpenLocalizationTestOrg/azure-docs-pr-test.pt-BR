---
title: "aaaConvert toomicroservices de aplicativos de serviços de nuvem do Azure | Microsoft Docs"
description: "Este guia compara da Web de serviços de nuvem e funções de trabalho e do Service Fabric serviços sem estado toohelp migram de serviços de nuvem tooService malha."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: 5880ebb3-8b54-4be8-af4b-95a1bc082603
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/29/2017
ms.author: vturecek
ms.openlocfilehash: c43b11623b2ba7f6069782a8b7e030c82572a6e2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="guide-tooconverting-web-and-worker-roles-tooservice-fabric-stateless-services"></a>Guia tooconverting serviços Web e funções de trabalho tooService malha sem monitoração de estado
Este artigo descreve como toomigrate sua nuvem serviços Web e funções de trabalho tooService malha sem monitoração de estado dos serviços. Este é o caminho de migração mais simples saudação do serviços de nuvem tooService malha de aplicativos cuja arquitetura geral será aproximadamente toostay Olá mesmo.

## <a name="cloud-service-project-tooservice-fabric-application-project"></a>O projeto de aplicativo do serviço project tooService malha de nuvem
 Um projeto de serviço de nuvem e um projeto de aplicativo do Service Fabric têm uma estrutura semelhante e ambas as unidade de implantação Olá representam de seu aplicativo - ou seja, eles cada definem Olá completo pacote toorun implantado seu aplicativo. Um projeto de Serviço de Nuvem contém uma ou mais funções de trabalho ou Web. Da mesma forma, um projeto de aplicativo Service Fabric contém um ou mais serviços. 

diferença de saudação é que Casais de projeto de serviço de nuvem Olá Olá a implantação de aplicativos com uma implantação de VM e, portanto, contém as definições de configuração da VM, enquanto o projeto de aplicativo do Service Fabric Olá define apenas um aplicativo que será implantado tooa o conjunto de máquinas virtuais existentes em um cluster do Service Fabric. cluster do Service Fabric Olá em si é implantado apenas uma vez, por meio de um modelo do Gerenciador de recursos ou através de saudação portal do Azure e o Service Fabric vários aplicativos podem ser implantados tooit.

![Comparação de projeto dos Serviços de Nuvem e do Service Fabric][3]

## <a name="worker-role-toostateless-service"></a>Serviço de toostateless de função de trabalho
Conceitualmente, uma função de trabalho representa uma carga de trabalho sem monitoração de estado, que significa que todas as instâncias de carga de trabalho de saudação é idêntica e solicitações podem ser roteado tooany instância a qualquer momento. Cada instância não é solicitação anterior de saudação tooremember esperado. Estado de carga de trabalho Olá opera em é gerenciado por um armazenamento de estado externo, como o armazenamento de tabela do Azure ou banco de dados de documento do Azure. No Service Fabric, esse tipo de carga de trabalho é representado por um serviço sem estado. Olá mais simples abordagem toomigrating um tooService de função de trabalho malha pode ser feita pela conversão tooa de código da função de trabalho sem monitoração de estado do serviço.

![Função de trabalho tooStateless serviço][4]

## <a name="web-role-toostateless-service"></a>Função toostateless serviço Web
TooWorker semelhante função, uma função Web também representa uma carga de trabalho sem monitoração de estado, e portanto conceitualmente muito pode ser mapeado tooa serviço sem monitoração de estado do serviço de malha. No entanto, diferentemente das funções Web, o Service Fabric não dá suporte a IIS. toomigrate um aplicativo web de um serviço sem monitoração de estado de tooa de função Web requer primeiro framework web tooa móvel que pode ser auto-hospedado e não dependem de IIS ou System. Web, como o ASP.NET Core 1.

| **Aplicativo** | **Com suporte** | **Caminho de migração** |
| --- | --- | --- |
| Web Forms do ASP.NET |Não |Converter tooASP.NET principal 1 MVC |
| ASP.NET MVC |Com migração |Atualização tooASP.NET principal 1 MVC |
| API Web ASP.NET |Com migração |Usar o servidor auto-hospedado ou o ASP.NET Core 1 |
| ASP.NET Core 1 |Sim |N/D |

## <a name="entry-point-api-and-lifecycle"></a>API de ponto de entrada e ciclo de vida
As APIs de função de trabalho e do Service Fabric oferecem pontos de entrada semelhantes: 

| **Ponto de entrada** | **Função de trabalho** | **Serviço Service Fabric** |
| --- | --- | --- |
| Processando |`Run()` |`RunAsync()` |
| Iniciar VM |`OnStart()` |N/D |
| Parar VM |`OnStop()` |N/D |
| Abrir escuta para solicitações de cliente |N/D |<ul><li> `CreateServiceInstanceListener()` para serviços sem estado</li><li>`CreateServiceReplicaListener()` para serviços com estado</li></ul> |

### <a name="worker-role"></a>Função de trabalho
```C#

using Microsoft.WindowsAzure.ServiceRuntime;

namespace WorkerRole1
{
    public class WorkerRole : RoleEntryPoint
    {
        public override void Run()
        {
        }

        public override bool OnStart()
        {
        }

        public override void OnStop()
        {
        }
    }
}

```

### <a name="service-fabric-stateless-service"></a>Serviço sem estado do Service Fabric
```C#

using System.Collections.Generic;
using System.Threading;
using System.Threading.Tasks;
using Microsoft.ServiceFabric.Services.Communication.Runtime;
using Microsoft.ServiceFabric.Services.Runtime;

namespace Stateless1
{
    public class Stateless1 : StatelessService
    {
        protected override IEnumerable<ServiceInstanceListener> CreateServiceInstanceListeners()
        {
        }

        protected override Task RunAsync(CancellationToken cancelServiceInstance)
        {
        }
    }
}

```

Têm uma substituição de "Executar" primário em que o processamento toobegin. Os serviços do Service Fabric combinam `Run`, `Start` e `Stop` em um único ponto de entrada, `RunAsync`. O serviço deve começar a trabalhar quando `RunAsync` inicia e deve parar de funcionar quando hello `RunAsync` CancellationToken do método é sinalizado. 

Há várias diferenças importantes entre o ciclo de vida de saudação e tempo de vida de serviços de funções de trabalho e serviço de malha:

* **Ciclo de vida:** Olá maior diferença é que uma função de trabalho é uma VM e portanto o ciclo de vida é toohello empatado VM, que inclui eventos de ao Olá VM inícios e paradas. Um serviço de malha do serviço tem um ciclo de vida que é separado do ciclo de vida VM hello, portanto, não inclui eventos para quando o hello host VM ou máquina é iniciado e parar, pois eles não estão relacionados.
* **Tempo de vida:** uma instância de função de trabalho reciclará se hello `Run` sai do método. Olá `RunAsync` método em um serviço do Service Fabric Entretanto pode executar toocompletion e instância de serviço Olá permaneçam em. 

O Service Fabric fornece um ponto de entrada de configuração opcional de comunicação para serviços que escutam solicitações de cliente. Olá RunAsync e o ponto de entrada de comunicação são substituições opcionais nos serviços do Service Fabric - seu serviço pode escolher tooonly escutar solicitações de tooclient, ou apenas executar um loop de processamento, ou ambos - motivo pelo qual Olá método RunAsync é permitido tooexit sem reiniciar a instância de serviço Olá, porque ele pode continuar toolisten para solicitações de cliente.

## <a name="application-api-and-environment"></a>API de aplicativo e ambiente
ambiente de serviços de nuvem Olá API fornece informações e funcionalidade para a instância atual de VM hello, bem como informações sobre outras instâncias de função VM. Service Fabric fornece informações relacionadas tooits tempo de execução e algumas informações sobre o nó de saudação um serviço no momento está executando. 

| **Tarefa de ambiente** | **Serviços de Nuvem** | **Service Fabric** |
| --- | --- | --- |
| Notificação de alteração e Definições de Configuração |`RoleEnvironment` |`CodePackageActivationContext` |
| Armazenamento local |`RoleEnvironment` |`CodePackageActivationContext` |
| Informações de ponto de extremidade |`RoleInstance` <ul><li>Instância atual: `RoleEnvironment.CurrentRoleInstance`</li><li>Outras funções e instância: `RoleEnvironment.Roles`</li> |<ul><li>`NodeContext` para o endereço do nó atual</li><li>`FabricClient` e `ServicePartitionResolver` para descoberta de ponto de extremidade de serviço</li> |
| Ambiente de emulação |`RoleEnvironment.IsEmulated` |N/D |
| Eventos de alteração simultânea |`RoleEnvironment` |N/D |

## <a name="configuration-settings"></a>Definições de configuração
Definições de configuração em serviços de nuvem são definidas para uma função de VM e aplicam tooall instâncias dessa função VM. Essas configurações são pares chave-valor definidos nos arquivos ServiceConfiguration.*.cscfg e podem ser acessadas diretamente por meio do RoleEnvironment. Na malha do serviço, configurações se aplicam individualmente tooeach serviço e aplicativo tooeach, em vez de tooa VM, como uma máquina virtual pode hospedar vários serviços e aplicativos. Um serviço é composto de três pacotes:

* **Código:** contém os executáveis de serviço hello, binários, DLLs e outros arquivos toorun precisa de um serviço.
* **Config:** todos os arquivos de configuração e configurações de um serviço.
* **Dados:** arquivos de dados estáticos associados ao serviço hello.

Cada um desses pacotes pode ter controle de versão e atualização independentes. Serviços de tooCloud semelhante, um pacote de configuração podem ser acessados por meio de programação através de uma API e eventos são serviços de saudação toonotify disponíveis de uma alteração de pacote de configuração. Um arquivo Settings.xml pode ser usado para configuração de chave-valor e o acesso programático semelhante toohello aplicativo seção configurações de um arquivo App. config. No entanto, ao contrário dos Serviços de Nuvem, um pacote de configuração do Service Fabric pode conter arquivos de configuração em qualquer formato, seja XML, JSON, YAML ou formato binário personalizado. 

### <a name="accessing-configuration"></a>Acessando configuração
#### <a name="cloud-services"></a>Serviços de Nuvem
As definições de configuração do ServiceConfiguration.*.cscfg podem ser acessadas por meio do `RoleEnvironment`. Essas configurações são instâncias de função tooall globalmente disponíveis no hello mesma implantação do serviço de nuvem.

```C#

string value = RoleEnvironment.GetConfigurationSettingValue("Key");

```

#### <a name="service-fabric"></a>Service Fabric
Cada serviço tem seu próprio pacote de configuração individual. Não há nenhum mecanismo interno para as configurações globais que possa ser acessado por todos os aplicativos em um cluster. Ao usar especial Settings.xml configuração arquivo do Service Fabric dentro de um pacote de configuração, os valores em Settings.xml podem ser substituídos no nível de aplicativo hello, possibilitando a definições de configuração de nível de aplicativo.

Definições de configuração são acessos dentro de cada instância de serviço por meio do serviço Olá `CodePackageActivationContext`.

```C#

ConfigurationPackage configPackage = this.Context.CodePackageActivationContext.GetConfigurationPackageObject("Config");

// Access Settings.xml
KeyedCollection<string, ConfigurationProperty> parameters = configPackage.Settings.Sections["MyConfigSection"].Parameters;

string value = parameters["Key"]?.Value;

// Access custom configuration file:
using (StreamReader reader = new StreamReader(Path.Combine(configPackage.Path, "CustomConfig.json")))
{
    MySettings settings = JsonConvert.DeserializeObject<MySettings>(reader.ReadToEnd());
}

```

### <a name="configuration-update-events"></a>Eventos de atualização de configuração
#### <a name="cloud-services"></a>Serviços de Nuvem
Olá `RoleEnvironment.Changed` evento é usada toonotify todas as instâncias de função quando uma alteração ocorre em ambiente de saudação, como uma alteração de configuração. Isso é usado tooconsume atualizações de configuração sem reciclar instâncias de função ou reiniciar um processo de trabalho.

```C#

RoleEnvironment.Changed += RoleEnvironmentChanged;

private void RoleEnvironmentChanged(object sender, RoleEnvironmentChangedEventArgs e)
{
   // Get hello list of configuration changes
   var settingChanges = e.Changes.OfType<RoleEnvironmentConfigurationSettingChange>();
foreach (var settingChange in settingChanges) 
   {
      Trace.WriteLine("Setting: " + settingChange.ConfigurationSettingName, "Information");
   }
}

```

#### <a name="service-fabric"></a>Service Fabric
Cada um dos três tipos de pacote hello em um serviço de código, configuração e dados - ter eventos notificam uma instância de serviço quando um pacote é atualizado, adicionado ou removido. Um serviço pode conter vários pacotes de cada tipo. Por exemplo, um serviço pode ter vários pacotes de configuração, cada um deles com controle de versão e atualização individuais. 

Esses eventos são alterações tooconsume disponíveis em pacotes de serviço sem reiniciar a instância do serviço hello.

```C#

this.Context.CodePackageActivationContext.ConfigurationPackageModifiedEvent +=
                    this.CodePackageActivationContext_ConfigurationPackageModifiedEvent;

private void CodePackageActivationContext_ConfigurationPackageModifiedEvent(object sender, PackageModifiedEventArgs<ConfigurationPackage> e)
{
    this.UpdateCustomConfig(e.NewPackage.Path);
    this.UpdateSettings(e.NewPackage.Settings);
}

```

## <a name="startup-tasks"></a>Tarefas de inicialização
As tarefas de inicialização são ações executadas antes de um aplicativo ser iniciado. Uma tarefa de inicialização é normalmente usada toorun scripts de instalação usando privilégios elevados. Os Serviços de Nuvem e o Service Fabric dão suporte a tarefas de inicialização. Olá principal diferença é que os serviços em nuvem, uma tarefa de inicialização é tooa empatado VM porque ela é parte de uma instância de função, enquanto na malha do serviço de uma tarefa de inicialização é serviço tooa associado, que não está associado tooany VM específica.

| Serviços de Nuvem | Service Fabric |
| --- | --- | --- |
| Configuração local |ServiceDefinition.csdef |
| Privilégios |"limitados" ou "elevados" |
| Sequenciamento |"simples", "em segundo plano", "primeiro plano" |

### <a name="cloud-services"></a>Serviços de Nuvem
Nos Serviços de Nuvem, um ponto de entrada de inicialização é configurado por função em ServiceDefinition.csdef. 

```xml

<ServiceDefinition>
    <Startup>
        <Task commandLine="Startup.cmd" executionContext="limited" taskType="simple" >
            <Environment>
                <Variable name="MyVersionNumber" value="1.0.0.0" />
            </Environment>
        </Task>
    </Startup>
    ...
</ServiceDefinition>

```

### <a name="service-fabric"></a>Service Fabric
No Service Fabric, um ponto de entrada de inicialização é configurado por serviço em ServiceManifest.xml:

```xml

<ServiceManifest>
  <CodePackage Name="Code" Version="1.0.0">
    <SetupEntryPoint>
      <ExeHost>
        <Program>Startup.bat</Program>
      </ExeHost>
    </SetupEntryPoint>
    ...
</ServiceManifest>

``` 

## <a name="a-note-about-development-environment"></a>Uma observação sobre o ambiente de desenvolvimento
Serviços de nuvem e malha do serviço são integrados com o Visual Studio com suporte para depuração, configurar e implantar as localmente e modelos de projeto e tooAzure. Os Serviços de Nuvem e o Service Fabric também fornecem um ambiente de tempo de execução de desenvolvimento local. Olá diferença é que enquanto o serviço de nuvem que emula o tempo de execução de desenvolvimento Olá Olá ambiente do Azure no qual ele é executado, Service Fabric não usa um emulador: usa Olá completa do Service Fabric runtime. Olá, é executado no computador de desenvolvimento local do ambiente do Service Fabric Olá mesmo ambiente que é executado em produção.

## <a name="next-steps"></a>Próximas etapas
Leia mais sobre serviços confiáveis do serviço de malha e diferenças fundamentais de saudação entre serviços de nuvem e toounderstand de arquitetura de aplicativo do Service Fabric como tootake aproveitar Olá completo conjunto de recursos de malha do serviço.

* [Introdução aos Reliable Services do Service Fabric](service-fabric-reliable-services-quick-start.md)
* [Diferenças de toohello guia conceitual entre os serviços de nuvem e do Service Fabric](service-fabric-cloud-services-migration-differences.md)

<!--Image references-->
[3]: ./media/service-fabric-cloud-services-migration-worker-role-stateless-service/service-fabric-cloud-service-projects.png
[4]: ./media/service-fabric-cloud-services-migration-worker-role-stateless-service/worker-role-to-stateless-service.png
