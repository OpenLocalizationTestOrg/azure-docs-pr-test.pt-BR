---
title: modelo de aplicativo do Service Fabric aaaAzure | Microsoft Docs
description: "Como toomodel e descrevem os aplicativos e serviços na malha do serviço."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: mani-ramaswamy
ms.assetid: 17a99380-5ed8-4ed9-b884-e9b827431b02
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: ryanwi
ms.openlocfilehash: 54c4d026e7d556be5f697d4a6f2ee886687e1c35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="model-an-application-in-service-fabric"></a>Modelar um aplicativo no Malha do Serviço
Este artigo fornece uma visão geral do modelo de aplicativo do Azure Service Fabric hello e como toodefine um aplicativo e serviço por meio de arquivos de manifesto.

## <a name="understand-hello-application-model"></a>Entender o modelo de aplicativo hello
Um aplicativo é uma coleção de serviços membros que executam determinadas funções. Um serviço executa uma função completa e autônoma e pode iniciar e executar independentemente de outros serviços.  Um serviço é composto de código, configuração e dados. Para cada serviço, código consiste em binários executáveis hello, a configuração consiste em configurações de serviço que podem ser carregadas no tempo de execução e dados consistem em dados estáticos arbitrário toobe consumido pelo serviço de saudação. Cada componente nesse modelo hierárquico de aplicativo pode ser atualizado e transformado em outra versão independentemente.

![modelo de aplicativo do Service Fabric Olá][appmodel-diagram]

Um tipo de aplicativo é uma categorização de um aplicativo e consiste em um pacote de tipos de serviço. Um tipo de serviço é uma categorização de um serviço. categorização de saudação pode ter diferentes definições e configurações, mas permanece de funcionalidade de núcleo Olá Olá mesmo. Olá, instâncias de um serviço são variações de configuração de serviço diferente de saudação do hello mesmo tipo de serviço.  

Classes (ou "tipos") de aplicativos e serviços são descritas por meio de arquivos XML (manifestos de aplicativo e manifestos do serviço).  Olá manifestos são modelos de saudação em relação ao qual os aplicativos podem ser instanciados do cluster de saudação repositório de imagens. Olá definição de esquema para o arquivo ServiceManifest.xml e ApplicationManifest.xml de saudação é instalada com hello SDK do Service Fabric e ferramentas muito*C:\Program Files\Microsoft SDKs\Service Fabric\schemas\ServiceFabricServiceModel.xsd*.

código de saudação para instâncias diferentes de aplicativos executados como processos separados, mesmo quando hospedados por Olá mesmo nó de malha do serviço. Além disso, o ciclo de vida de saudação de cada instância de aplicativo pode ser gerenciado (por exemplo, atualizado) independentemente. Olá diagrama a seguir mostra como os tipos de aplicativos são compostos de tipos de serviço, que por sua vez, são compostos de código, configuração e pacotes de dados. diagrama de saudação toosimplify, apenas pacotes de dados/de configuração de código Olá para `ServiceType4` são mostrados, embora cada tipo de serviço inclui alguns ou todos os tipos de pacotes.

![Tipos de aplicativos do Service Fabric e tipos de serviço][cluster-imagestore-apptypes]

Dois arquivos de manifesto diferentes são usados toodescribe aplicativos e serviços: Olá manifesto do serviço e o manifesto do aplicativo. Manifestos são abordados detalhadamente em Olá seções a seguir.

Pode haver uma ou mais instâncias de um tipo de serviço ativo no cluster hello. Por exemplo, instâncias de serviço com monitoração de estado ou réplicas atingir alta confiabilidade replicando o estado entre as réplicas localizadas em diferentes nós de cluster de saudação. Replicação essencialmente fornece redundância para Olá toobe de serviço disponível, mesmo se um nó em um cluster falha. Um [particionada serviço](service-fabric-concepts-partitioning.md) mais divide seu estado (e o estado de toothat de padrões de acesso) em nós de cluster de saudação.

Olá diagrama a seguir mostra a relação Olá entre aplicativos e instâncias de serviço, partições e réplicas.

![Partições e réplicas dentro de um serviço][cluster-application-instances]

> [!TIP]
> Você pode exibir o layout de saudação de aplicativos em um cluster usando a ferramenta de Gerenciador do Service Fabric Olá disponível em http://&lt;yourclusteraddress&gt;: 19080/Explorer. Para obter mais informações, consulte [Visualizando o cluster com o Service Fabric Explorer](service-fabric-visualizing-your-cluster.md).
> 
> 

## <a name="describe-a-service"></a>Descrever um serviço
manifesto do serviço Olá declarativamente define a versão e o tipo de serviço hello. Ele especifica os metadados de serviço, como o tipo de serviço, propriedades de integridade, métricas de balanceamento de carga, binários de serviço e arquivos de configuração.  Ou seja, ele descreve pacotes de código, configuração e dados de saudação que compõem um toosupport do pacote de serviço um ou mais tipos de serviço. Aqui está um manifesto do serviço de exemplo simples:

```xml
<?xml version="1.0" encoding="utf-8" ?>
<ServiceManifest Name="MyServiceManifest" Version="SvcManifestVersion1" xmlns="http://schemas.microsoft.com/2011/01/fabric" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
  <Description>An example service manifest</Description>
  <ServiceTypes>
    <StatelessServiceType ServiceTypeName="MyServiceType" />
  </ServiceTypes>
  <CodePackage Name="MyCode" Version="CodeVersion1">
    <SetupEntryPoint>
      <ExeHost>
        <Program>MySetup.bat</Program>
      </ExeHost>
    </SetupEntryPoint>
    <EntryPoint>
      <ExeHost>
        <Program>MyServiceHost.exe</Program>
      </ExeHost>
    </EntryPoint>
    <EnvironmentVariables>
      <EnvironmentVariable Name="MyEnvVariable" Value=""/>
      <EnvironmentVariable Name="HttpGatewayPort" Value="19080"/>
    </EnvironmentVariables>
  </CodePackage>
  <ConfigPackage Name="MyConfig" Version="ConfigVersion1" />
  <DataPackage Name="MyData" Version="DataVersion1" />
</ServiceManifest>
```

**Versão** atributos são cadeias de caracteres não estruturadas e não analisada pelo sistema hello. Atributos de versão é usada tooversion cada componente para atualizações.

**ServiceTypes** declara para quais tipos de serviço há suporte pelos **CodePackages** neste manifesto. Quando um serviço é instanciado em relação a um desses tipos de serviço, todos os pacotes de código declarados nesse manifesto são ativados com a execução de seus pontos de entrada. processos resultantes Olá são tipos de serviço tooregister esperado Olá tem suportada em tempo de execução. Tipos de serviço são declarados no nível de manifesto de saudação e não Olá nível de pacote de código. Portanto quando há vários pacotes de código, eles são todos ativados sempre que o sistema Olá procura por qualquer uma das Olá declarado como tipos de serviço.

**SetupEntryPoint** é um ponto de entrada com privilégios que é executado com hello mesmo credenciais como Service Fabric (normalmente Olá *LocalSystem* conta) antes de qualquer outro ponto de entrada. executável de saudação especificado por **EntryPoint** normalmente é o host de serviço de longa execução hello. presença de saudação de um ponto de entrada de instalação separado evita que o host de serviço toorun Olá com altos privilégios por longos períodos de tempo. executável de saudação especificado por **EntryPoint** é executado após a **SetupEntryPoint** é encerrada com êxito. Se o processo de saudação nunca termina ou falha, o processo resultante Olá é monitorado e reiniciado (começando novamente com **SetupEntryPoint**).  

Cenários típicos de uso **SetupEntryPoint** são quando você executa um executável antes do início do serviço de saudação ou executar uma operação com privilégios elevados. Por exemplo:

* Configurando e inicializar variáveis de ambiente que Olá necessidades executável do serviço. Isso não é limitado tooonly executáveis gravados por meio de modelos de programação de malha do serviço de saudação. Por exemplo, npm.exe precisa de algumas variáveis de ambiente configurados para implantar um aplicativo node.js.
* Configurando o controle de acesso, instalando certificados de segurança.

Para obter mais detalhes sobre como Olá tooconfigure **SetupEntryPoint** consulte [configurar política de saudação para um ponto de entrada de configuração de serviço](service-fabric-application-runas-security.md)

**EnvironmentVariables** fornece uma lista de variáveis de ambiente que são definidas para este pacote de códigos. Environmentment variáveis podem ser substituídas na Olá `ApplicationManifest.xml` tooprovide de valores diferentes para instâncias de serviço diferente. 

**DataPackage** declara uma pasta nomeada pelo Olá **nome** atributo, que contém dados estáticos arbitrário toobe consumido pelo processo de saudação em tempo de execução.

**ConfigPackage** declara uma pasta nomeada pelo Olá **nome** atributo, que contém um *Settings.xml* arquivo. arquivo de configurações de saudação contém seções de configurações de par definida pelo usuário, o valor de chave que Olá processo ler de volta no tempo de execução. Durante uma atualização, se apenas Olá **ConfigPackage** **versão** foi alterado, Olá executando o processo não será reiniciado. Em vez disso, um retorno de chamada notifica o processo de saudação configurações foram alteradas para que possam ser recarregadas dinamicamente. Aqui está um exemplo do arquivo *Settings.xml* :

```xml
<Settings xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/2011/01/fabric">
  <Section Name="MyConfigurationSection">
    <Parameter Name="MySettingA" Value="Example1" />
    <Parameter Name="MySettingB" Value="Example2" />
  </Section>
</Settings>
```

> [!NOTE]
> Um manifesto do serviço pode conter vários pacotes de código, de configuração e de dados. Cada um deles pode ser transformado em versão independentemente.
> 
> 

<!--
For more information about other features supported by service manifests, refer toohello following articles:

*TODO: LoadMetrics, PlacementConstraints, ServicePlacementPolicies
*TODO: Resources
*TODO: Health properties
*TODO: Trace filters
*TODO: Configuration overrides
-->

## <a name="describe-an-application"></a>Descrever um aplicativo
o manifesto do aplicativo Hello declarativamente descreve a versão e o tipo de aplicativo hello. Ele especifica os metadados de composição de serviço, como nomes estáveis, esquema de particionamento, fator de replicação/contagem de instância, política de segurança/isolamento, restrições de posicionamento, substituições de configuração e tipos de serviço membro. domínios de balanceamento de carga de saudação no qual o aplicativo hello é colocado também são descritos.

Assim, um manifesto de aplicativo descreve elementos em nível de aplicativo hello e faz referência a um ou mais serviços manifestos toocompose um tipo de aplicativo. Aqui está um manifesto de aplicativo de exemplo simples:

```xml
<?xml version="1.0" encoding="utf-8" ?>
<ApplicationManifest
      ApplicationTypeName="MyApplicationType"
      ApplicationTypeVersion="AppManifestVersion1"
      xmlns="http://schemas.microsoft.com/2011/01/fabric"
      xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
  <Description>An example application manifest</Description>
  <ServiceManifestImport>
    <ServiceManifestRef ServiceManifestName="MyServiceManifest" ServiceManifestVersion="SvcManifestVersion1"/>
    <ConfigOverrides/>
    <EnvironmentOverrides CodePackageRef="MyCode"/>
  </ServiceManifestImport>
  <DefaultServices>
     <Service Name="MyService">
         <StatelessService ServiceTypeName="MyServiceType" InstanceCount="1">
             <SingletonPartition/>
         </StatelessService>
     </Service>
  </DefaultServices>
</ApplicationManifest>
```

Manifestos de serviço, como **versão** atributos são cadeias de caracteres não estruturadas e não são analisados pelo sistema hello. Atributos de versão também é usada tooversion cada componente para atualizações.

**Servicemanifestimport ao** contém manifestos de tooservice de referências que compõem esse tipo de aplicativo. Os manifestos de serviço importados determinam quais tipos de serviço são válidos nesse tipo de aplicativo. Dentro de Olá servicemanifestimport ao, você substituem os valores de configuração em Settings.xml e o ambiente de variáveis nos arquivos ServiceManifest.xml. 


**DefaultServices** declara as instâncias de serviço que são criadas automaticamente sempre que um aplicativo é instanciado em relação a esse tipo de aplicativo. Serviços padrão são apenas uma conveniência e se comportam como serviços normais em todos os aspectos após terem sido criados. Eles são atualizados juntamente com outros serviços na instância do aplicativo hello e também podem ser removidos.

> [!NOTE]
> Um manifesto de aplicativo pode conter várias importações de manifesto do serviço e serviços padrão. Cada importação de manifesto do serviço pode ser transformada em versão independentemente.
> 
> 

toolearn como toomaintain diferentes do aplicativo e os parâmetros de serviço para ambientes individuais, consulte [gerenciar parâmetros do aplicativo para vários ambientes](service-fabric-manage-multiple-environment-app-configuration.md).

<!--
For more information about other features supported by application manifests, refer toohello following articles:

*TODO: Application parameters
*TODO: Security, Principals, RunAs, SecurityAccessPolicy
*TODO: Service Templates
-->



## <a name="next-steps"></a>Próximas etapas
[Empacotar um aplicativo](service-fabric-package-apps.md) e torná-lo pronto toodeploy.

[Implantar e remover aplicativos] [ 10] descreve como instâncias do aplicativo toouse PowerShell toomanage.

[Gerenciando parâmetros do aplicativo para vários ambientes] [ 11] descreve como tooconfigure parâmetros e variáveis de ambiente para instâncias de aplicativo diferente.

[Configurar políticas de segurança para seu aplicativo] [ 12] descreve como os serviços de toorun em acesso de toorestrict de políticas de segurança.

Os [modelos de hospedagem de aplicativo][13] descrevem a relação entre réplicas (ou instâncias) de um serviço implantado e o processo de host do serviço.

<!--Image references-->
[appmodel-diagram]: ./media/service-fabric-application-model/application-model.png
[cluster-imagestore-apptypes]: ./media/service-fabric-application-model/cluster-imagestore-apptypes.png
[cluster-application-instances]: media/service-fabric-application-model/cluster-application-instances.png

<!--Link references--In actual articles, you only need a single period before hello slash-->
[10]: service-fabric-deploy-remove-applications.md
[11]: service-fabric-manage-multiple-environment-app-configuration.md
[12]: service-fabric-application-runas-security.md
[13]: service-fabric-hosting-model.md
