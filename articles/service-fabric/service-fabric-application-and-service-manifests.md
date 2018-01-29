---
title: "Descrevendo os serviços e aplicativos do Azure Service Fabric | Microsoft Docs"
description: "Descreve como os manifestos são usados para descrever serviços e aplicativos do Service Fabric."
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
ms.date: 12/07/2017
ms.author: ryanwi
ms.openlocfilehash: 8e0cf78aef7e973188ce9581ec94f012f6ecde90
ms.sourcegitcommit: e266df9f97d04acfc4a843770fadfd8edf4fa2b7
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/11/2017
---
# <a name="service-fabric-application-and-service-manifests"></a>Manifestos de serviço e aplicativo do Service Fabric
Este artigo descreve como os serviços e aplicativos do Service Fabric são definidos e atualizados usando os arquivos. ServiceManifest.xml e ApplicationManifest.xml.  O esquema XML para esses arquivos de manifesto está documentado em [documentação do esquema ServiceFabricServiceModel.xsd](service-fabric-service-model-schema.md).

## <a name="describe-a-service-in-servicemanifestxml"></a>Descrevem um serviço em ServiceManifest.xml
O manifesto do serviço declarativamente define o tipo de serviço e a versão. Ele especifica os metadados de serviço, como o tipo de serviço, propriedades de integridade, métricas de balanceamento de carga, binários de serviço e arquivos de configuração.  Trocando em miúdos, ele descreve os pacotes de código, de configuração e de dados que compõem um pacote de serviço para dar suporte a um ou mais tipos de serviço. Um manifesto do serviço pode conter vários pacotes de código, de configuração e de dados, que podem ser atualizados de forma independente. Aqui está um manifesto de serviço para o serviço de front-end da web ASP.NET Core do [aplicativo de exemplo de votação](https://github.com/Azure-Samples/service-fabric-dotnet-quickstart):

```xml
<?xml version="1.0" encoding="utf-8"?>
<ServiceManifest Name="VotingWebPkg"
                 Version="1.0.0"
                 xmlns="http://schemas.microsoft.com/2011/01/fabric"
                 xmlns:xsd="http://www.w3.org/2001/XMLSchema"
                 xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
  <ServiceTypes>
    <!-- This is the name of your ServiceType. 
         This name must match the string used in RegisterServiceType call in Program.cs. -->
    <StatelessServiceType ServiceTypeName="VotingWebType" />
  </ServiceTypes>

  <!-- Code package is your service executable. -->
  <CodePackage Name="Code" Version="1.0.0">
    <EntryPoint>
      <ExeHost>
        <Program>VotingWeb.exe</Program>
        <WorkingFolder>CodePackage</WorkingFolder>
      </ExeHost>
    </EntryPoint>
  </CodePackage>

  <!-- Config package is the contents of the Config directoy under PackageRoot that contains an 
       independently-updateable and versioned set of custom configuration settings for your service. -->
  <ConfigPackage Name="Config" Version="1.0.0" />

  <Resources>
    <Endpoints>
      <!-- This endpoint is used by the communication listener to obtain the port on which to 
           listen. Please note that if your service is partitioned, this port is shared with 
           replicas of different partitions that are placed in your code. -->
      <Endpoint Protocol="http" Name="ServiceEndpoint" Type="Input" Port="8080" />
    </Endpoints>
  </Resources>
</ServiceManifest>
```

**Version** são cadeias de caracteres não estruturadas e não analisadas pelo sistema. Atributos de versão são usados para a versão de cada componente para atualizações.

**ServiceTypes** declara para quais tipos de serviço há suporte pelos **CodePackages** neste manifesto. Quando um serviço é instanciado em relação a um desses tipos de serviço, todos os pacotes de código declarados nesse manifesto são ativados com a execução de seus pontos de entrada. Os processos resultantes devem registrar os tipos de serviço com suporte no tempo de execução. Os tipos de serviço são declarados no nível do manifesto e não no nível do pacote de código. Assim, quando há vários pacotes de código, eles são todos ativados sempre que o sistema procurar por qualquer um dos tipos de serviço declarados.

O executável especificado pelo **EntryPoint** normalmente é o host de serviço de longa duração. **SetupEntryPoint** é um ponto de entrada privilegiado que é executado com as mesmas credenciais da Malha do Serviço (normalmente, a conta *LocalSystem* ) antes de qualquer outro ponto de entrada.  A presença de um ponto de entrada de instalação separado evita a necessidade de executar o host de serviço com altos privilégios por longos períodos de tempo. O executável especificado pelo **EntryPoint** é executado depois que o **SetupEntryPoint** é encerrado com êxito. Se o processo terminar ou falhar, o processo resultante é monitorado e reiniciado (começando novamente com **SetupEntryPoint**) .  

Cenários típicos de uso do **SetupEntryPoint** quando você executa um executável antes do início do serviço ou você executa uma operação com privilégios elevados. Por exemplo:

* Configurar e inicializar as variáveis de ambiente que o serviço executável precisa. Isso não é limitado a apenas executáveis gravados usando os modelos de programação do Service Fabric. Por exemplo, npm.exe precisa de algumas variáveis de ambiente configurados para implantar um aplicativo node.js.
* Configurando o controle de acesso, instalando certificados de segurança.

Para obter mais detalhes sobre como configurar o **SetupEntryPoint**, confira [Configurar a política para um ponto de entrada de instalação do serviço](service-fabric-application-runas-security.md)

**EnvironmentVariables** (não definido no exemplo anterior) fornece uma lista de variáveis de ambiente que são definidas para este pacote de códigos. As variáveis do ambiente podem ser substituídas no `ApplicationManifest.xml` para fornecer valores diferentes para instâncias de serviço diferentes. 

**DataPackage** (não definido no exemplo anterior) declara uma pasta nomeada pelo atributo **Name**, que contém dados estáticos arbitrários a serem consumidos pelo processo no tempo de execução.

**ConfigPackage** declara uma pasta nomeada pelo atributo **Name**, que contém um arquivo *Settings.xml*. Esse arquivo de configurações contém seções de configurações de par chave-valor, definido pelo usuário, que o processo lê de volta no tempo de execução. Durante a atualização, se apenas a **versão** do **ConfigPackage** tiver sido alterada, o processo de execução não será reiniciado. Em vez disso, um retorno de chamada notifica o processo de que as definições de configuração foram alteradas para que possam ser recarregadas dinamicamente. Aqui está um exemplo do arquivo *Settings.xml* :

```xml
<Settings xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/2011/01/fabric">
  <Section Name="MyConfigurationSection">
    <Parameter Name="MySettingA" Value="Example1" />
    <Parameter Name="MySettingB" Value="Example2" />
  </Section>
</Settings>
```

**Recursos**, tais como endpoints, que são usados pelo serviço sejam declarados/alterados sem alterar o código compilado.  Acesso aos recursos que são especificados no manifesto do serviço pode ser controlado por meio do **SecurityGroup** no manifesto do aplicativo.  Quando um recurso de **Endpoint** é definido no manifesto do serviço, o Service Fabric atribui portas do intervalo de portas reservadas do aplicativo quando uma porta não é explicitamente especificada.  Leia mais sobre [especificar ou substituir os recursos de endpoint](service-fabric-service-manifest-resources.md).


<!--
For more information about other features supported by service manifests, refer to the following articles:

*TODO: LoadMetrics, PlacementConstraints, ServicePlacementPolicies
*TODO: Health properties
*TODO: Trace filters
*TODO: Configuration overrides
-->

## <a name="describe-an-application-in-applicationmanifestxml"></a>Descrever um aplicativo ApplicationManifest.xml
O manifesto do aplicativo declarativamente descreve o tipo de aplicativo e a versão. Ele especifica os metadados de composição de serviço, como nomes estáveis, esquema de particionamento, fator de replicação/contagem de instância, política de segurança/isolamento, restrições de posicionamento, substituições de configuração e tipos de serviço membro. Também são descritos os domínios de balanceamento de carga no qual o aplicativo é colocado.

Portanto, um manifesto de aplicativo descreve os elementos no nível do aplicativo e faz referência a um ou mais manifestos do serviço para compor um tipo de aplicativo. Aqui está o manifesto do aplicativo para o [aplicativo de exemplo de votação](https://github.com/Azure-Samples/service-fabric-dotnet-quickstart):

```xml
<?xml version="1.0" encoding="utf-8"?>
<ApplicationManifest xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" ApplicationTypeName="VotingType" ApplicationTypeVersion="1.0.0" xmlns="http://schemas.microsoft.com/2011/01/fabric">
  <Parameters>
    <Parameter Name="VotingData_MinReplicaSetSize" DefaultValue="3" />
    <Parameter Name="VotingData_PartitionCount" DefaultValue="1" />
    <Parameter Name="VotingData_TargetReplicaSetSize" DefaultValue="3" />
    <Parameter Name="VotingWeb_InstanceCount" DefaultValue="-1" />
  </Parameters>
  <!-- Import the ServiceManifest from the ServicePackage. The ServiceManifestName and ServiceManifestVersion 
       should match the Name and Version attributes of the ServiceManifest element defined in the 
       ServiceManifest.xml file. -->
  <ServiceManifestImport>
    <ServiceManifestRef ServiceManifestName="VotingDataPkg" ServiceManifestVersion="1.0.0" />
    <ConfigOverrides />
  </ServiceManifestImport>
  <ServiceManifestImport>
    <ServiceManifestRef ServiceManifestName="VotingWebPkg" ServiceManifestVersion="1.0.0" />
    <ConfigOverrides />
  </ServiceManifestImport>
  <DefaultServices>
    <!-- The section below creates instances of service types, when an instance of this 
         application type is created. You can also create one or more instances of service type using the 
         ServiceFabric PowerShell module.
         
         The attribute ServiceTypeName below must match the name defined in the imported ServiceManifest.xml file. -->
    <Service Name="VotingData">
      <StatefulService ServiceTypeName="VotingDataType" TargetReplicaSetSize="[VotingData_TargetReplicaSetSize]" MinReplicaSetSize="[VotingData_MinReplicaSetSize]">
        <UniformInt64Partition PartitionCount="[VotingData_PartitionCount]" LowKey="0" HighKey="25" />
      </StatefulService>
    </Service>
    <Service Name="VotingWeb" ServicePackageActivationMode="ExclusiveProcess">
      <StatelessService ServiceTypeName="VotingWebType" InstanceCount="[VotingWeb_InstanceCount]">
        <SingletonPartition />
      </StatelessService>
    </Service>
  </DefaultServices>
</ApplicationManifest>
```

Manifestos de serviço, como atributos **Versão** , são cadeias de caracteres não estruturadas e não analisadas pelo sistema. Atributos de versão também são usados para a versão de cada componente para atualizações.

**Parâmetros** define os parâmetros usados em todo o manifesto do aplicativo. Os valores desses parâmetros pode ser fornecido quando o aplicativo é instanciado e pode substituir as definições de configuração do serviço ou aplicativo.  O valor de parâmetro padrão é usado se o valor não for alterado durante a instanciação do aplicativo. Para saber como manter aplicativos diferentes e parâmetros de serviço para ambientes individuais, consulte [Gerenciar parâmetros de aplicativo para vários ambientes](service-fabric-manage-multiple-environment-app-configuration.md).

**ServiceManifestImport** contém referências a manifestos de serviço que compõem esse tipo de aplicativo. Um manifesto de aplicativo pode conter várias importações de manifesto do serviço, cada um deles pode ser atualizado de forma independente. Os manifestos de serviço importados determinam quais tipos de serviço são válidos nesse tipo de aplicativo. Dentro de ServiceManifestImport, você substitui os valores de configuração em Settings.xml e nas variáveis de ambiente dos arquivos ServiceManifest.xml. **Políticas** (não definido no exemplo anterior) para associação de endpoint, segurança e acesso, e o compartilhamento de pacote pode ser definido em manifestos do serviço importado.  Para mais informações, consulte [Configurar políticas de segurança para seu aplicativo](service-fabric-application-runas-security.md).

**DefaultServices** declara as instâncias de serviço que são criadas automaticamente sempre que um aplicativo é instanciado em relação a esse tipo de aplicativo. Serviços padrão são apenas uma conveniência e se comportam como serviços normais em todos os aspectos após terem sido criados. Eles são atualizados com qualquer outro serviço na instância do aplicativo e também podem ser removidos. Um manifesto de aplicativo pode conter vários serviços padrão.

**Certificados** (não definido no exemplo anterior) declara os certificados usados para [configurar endpoints HTTPS](service-fabric-service-manifest-resources.md#example-specifying-an-https-endpoint-for-your-service) ou [criptografar segredos no manifesto do aplicativo](service-fabric-application-secret-management.md).

**Políticas** (não definido no exemplo anterior) descreve a coleta de log, [executar como padrão](service-fabric-application-runas-security.md), [integridade](service-fabric-health-introduction.md#health-policies) e políticas de [acesso de segurança](service-fabric-application-runas-security.md) a serem definidas no nível do aplicativo.

**Entidades** (não definido no exemplo anterior) descrevem as entidades de segurança (usuários ou grupos) necessárias para [executar serviços e proteger recursos do serviço](service-fabric-application-runas-security.md).  As entidades de segurança são referenciadas nas seções de **Políticas**.





<!--
For more information about other features supported by application manifests, refer to the following articles:

*TODO: Security, Principals, RunAs, SecurityAccessPolicy
*TODO: Service Templates
-->



## <a name="next-steps"></a>Próximas etapas
- [Empacotar um aplicativo](service-fabric-package-apps.md) e prepará-lo para a implantação.
- [Implantar e remover aplicativos](service-fabric-deploy-remove-applications.md).
- [Configurar parâmetros e variáveis de ambiente para instâncias diferentes do aplicativo](service-fabric-manage-multiple-environment-app-configuration.md).
- [Configurar políticas de segurança para seu aplicativo](service-fabric-application-runas-security.md).
- [Configurar endpoints HTTPS](service-fabric-service-manifest-resources.md#example-specifying-an-https-endpoint-for-your-service).
- [Criptografar segredos no manifesto do aplicativo](service-fabric-application-secret-management.md)

<!--Image references-->
[appmodel-diagram]: ./media/service-fabric-application-model/application-model.png
[cluster-imagestore-apptypes]: ./media/service-fabric-application-model/cluster-imagestore-apptypes.png
[cluster-application-instances]: media/service-fabric-application-model/cluster-application-instances.png



