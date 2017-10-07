---
title: "pontos de extremidade de serviço de malha do serviço aaaSpecifying | Microsoft Docs"
description: "Como os recursos de ponto de extremidade toodescribe em um serviço de manifesto, incluindo como tooset pontos de extremidade HTTPS"
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: da36cbdb-6531-4dae-88e8-a311ab71520d
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: subramar
ms.openlocfilehash: a4ebee353ce5cf86583673674246094f03f368be
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="specify-resources-in-a-service-manifest"></a>Especificar recursos em um manifesto do serviço
## <a name="overview"></a>Visão geral
manifesto do serviço Olá permite que os recursos que são usados por Olá serviço toobe declarado/alterado sem alterar o código de saudação compilado. Malha do serviço do Azure dá suporte à configuração de recursos de ponto de extremidade para o serviço de saudação. Olá acessar toohello os recursos que são especificados no manifesto do serviço Olá podem ser controlados por meio de Olá SecurityGroup no manifesto de aplicativo hello. declaração de saudação de recursos permite que esses toobe recursos alterados no momento da implantação, o que significa que o serviço de saudação não precisa toointroduce um novo mecanismo de configuração. Olá definição de esquema de arquivo ServiceManifest.xml de saudação é instalada com hello SDK do Service Fabric e ferramentas muito*C:\Program Files\Microsoft SDKs\Service Fabric\schemas\ServiceFabricServiceModel.xsd*.

## <a name="endpoints"></a>Pontos de extremidade
Quando um recurso de ponto de extremidade é definido no manifesto do serviço hello, o Service Fabric atribui portas do intervalo de portas de aplicativo hello reservado quando uma porta não for especificada explicitamente. Por exemplo, procure no ponto de extremidade Olá *ServiceEndpoint1* especificado no fragmento de manifesto Olá fornecido após este parágrafo. Além disso, os serviços também podem solicitar uma porta específica em um recurso. Réplicas de serviço em execução em nós de cluster diferente podem ser atribuídas diferentes números de porta, enquanto as réplicas de um serviço em execução no Olá a mesma porta de saudação do compartilhamento de nó. réplicas de serviço Olá podem usar essas portas conforme necessário para a replicação e escutar solicitações de clientes.

```xml
<Resources>
  <Endpoints>
    <Endpoint Name="ServiceEndpoint1" Protocol="http"/>
    <Endpoint Name="ServiceEndpoint2" Protocol="http" Port="80"/>
    <Endpoint Name="ServiceEndpoint3" Protocol="https"/>
  </Endpoints>
</Resources>
```

Consulte também[configuração com monitoração de estado confiável dos serviços](service-fabric-reliable-services-configuration.md) tooread mais sobre como fazer referência a pontos de extremidade do arquivo de configurações de pacote de configuração de saudação (settings.xml).

## <a name="example-specifying-an-http-endpoint-for-your-service"></a>Exemplo: especificando um ponto de extremidade HTTP para o serviço
Olá manifesto de serviço a seguir define um recurso de ponto de extremidade TCP e dois recursos de ponto de extremidade HTTP no hello &lt;recursos&gt; elemento.

A ACL é automaticamente aplicada aos pontos de extremidade HTTP pelo Service Fabric.

```xml
<?xml version="1.0" encoding="utf-8"?>
<ServiceManifest Name="Stateful1Pkg"
                 Version="1.0.0"
                 xmlns="http://schemas.microsoft.com/2011/01/fabric"
                 xmlns:xsd="http://www.w3.org/2001/XMLSchema"
                 xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
  <ServiceTypes>
    <!-- This is hello name of your ServiceType.
         This name must match hello string used in hello RegisterServiceType call in Program.cs. -->
    <StatefulServiceType ServiceTypeName="Stateful1Type" HasPersistedState="true" />
  </ServiceTypes>

  <!-- Code package is your service executable. -->
  <CodePackage Name="Code" Version="1.0.0">
    <EntryPoint>
      <ExeHost>
        <Program>Stateful1.exe</Program>
      </ExeHost>
    </EntryPoint>
  </CodePackage>

  <!-- Config package is hello contents of hello Config directoy under PackageRoot that contains an
       independently updateable and versioned set of custom configuration settings for your service. -->
  <ConfigPackage Name="Config" Version="1.0.0" />

  <Resources>
    <Endpoints>
      <!-- This endpoint is used by hello communication listener tooobtain hello port number on which to
           listen. Note that if your service is partitioned, this port is shared with
           replicas of different partitions that are placed in your code. -->
      <Endpoint Name="ServiceEndpoint1" Protocol="http"/>
      <Endpoint Name="ServiceEndpoint2" Protocol="http" Port="80"/>
      <Endpoint Name="ServiceEndpoint3" Protocol="https"/>

      <!-- This endpoint is used by hello replicator for replicating hello state of your service.
           This endpoint is configured through hello ReplicatorSettings config section in hello Settings.xml
           file under hello ConfigPackage. -->
      <Endpoint Name="ReplicatorEndpoint" />
    </Endpoints>
  </Resources>
</ServiceManifest>
```

## <a name="example-specifying-an-https-endpoint-for-your-service"></a>Exemplo: especificando um ponto de extremidade HTTPS para o serviço
Olá protocolo HTTPS fornece autenticação de servidor e também é usada para criptografar a comunicação cliente-servidor. tooenable HTTPS no serviço do Service Fabric, especificar o protocolo de saudação em Olá *recursos -> pontos de extremidade -> ponto de extremidade* seção saudação do manifesto do serviço, conforme mostrado anteriormente para o ponto de extremidade Olá *ServiceEndpoint3* .

> [!NOTE]
> O protocolo de um serviço não pode ser alterado durante a atualização do aplicativo. Se ele for alterado durante a atualização, será uma alteração significativa.
> 
> 

Aqui está um exemplo ApplicationManifest que você precisa tooset para HTTPS. impressão digital de saudação do certificado deve ser fornecido. Olá EndpointRef é tooEndpointResource uma referência em ServiceManifest, para que você definir o protocolo HTTPS de saudação. Você pode adicionar mais de um EndpointCertificate.  

```xml
<?xml version="1.0" encoding="utf-8"?>
<ApplicationManifest ApplicationTypeName="Application1Type"
                     ApplicationTypeVersion="1.0.0"
                     xmlns="http://schemas.microsoft.com/2011/01/fabric"
                     xmlns:xsd="http://www.w3.org/2001/XMLSchema"
                     xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
  <Parameters>
    <Parameter Name="Stateful1_MinReplicaSetSize" DefaultValue="3" />
    <Parameter Name="Stateful1_PartitionCount" DefaultValue="1" />
    <Parameter Name="Stateful1_TargetReplicaSetSize" DefaultValue="3" />
  </Parameters>
  <!-- Import hello ServiceManifest from hello ServicePackage. hello ServiceManifestName and ServiceManifestVersion
       should match hello Name and Version attributes of hello ServiceManifest element defined in the
       ServiceManifest.xml file. -->
  <ServiceManifestImport>
    <ServiceManifestRef ServiceManifestName="Stateful1Pkg" ServiceManifestVersion="1.0.0" />
    <ConfigOverrides />
    <Policies>
      <EndpointBindingPolicy CertificateRef="TestCert1" EndpointRef="ServiceEndpoint3"/>
    </Policies>
  </ServiceManifestImport>
  <DefaultServices>
    <!-- hello section below creates instances of service types when an instance of this
         application type is created. You can also create one or more instances of service type by using the
         Service Fabric PowerShell module.

         hello attribute ServiceTypeName below must match hello name defined in hello imported ServiceManifest.xml file. -->
    <Service Name="Stateful1">
      <StatefulService ServiceTypeName="Stateful1Type" TargetReplicaSetSize="[Stateful1_TargetReplicaSetSize]" MinReplicaSetSize="[Stateful1_ ]">
        <UniformInt64Partition PartitionCount="[Stateful1_PartitionCount]" LowKey="-9223372036854775808" HighKey="9223372036854775807" />
      </StatefulService>
    </Service>
  </DefaultServices>
  <Certificates>
    <EndpointCertificate Name="TestCert1" X509FindValue="FF FF FF FF FF FF FF FF FF FF FF FF FF FF FF FF FF FF FF F0" X509StoreName="MY" />  
  </Certificates>
</ApplicationManifest>
```

## <a name="overriding-endpoints-in-servicemanifestxml"></a>Substituição dos pontos de extremidade em ServiceManifest.xml

Em Olá ApplicationManifest adicione uma seção de ResourceOverrides que será uma seção de tooConfigOverrides irmão. Nesta seção, você pode especificar Olá substituição para a seção de pontos de extremidade de saudação na seção de recursos de saudação especificada no manifesto do serviço de saudação.

Em ordem toooverride ponto de extremidade no ServiceManifest usando o altere ApplicationParameters Olá ApplicationManifest como a seguir:

Em Olá seção servicemanifestimport ao adicionar uma nova seção "ResourceOverrides"

```xml
<ServiceManifestImport>
    <ServiceManifestRef ServiceManifestName="Stateless1Pkg" ServiceManifestVersion="1.0.0" />
    <ConfigOverrides />
    <ResourceOverrides>
      <Endpoints>
        <Endpoint Name="ServiceEndpoint" Port="[Port]" Protocol="[Protocol]" Type="[Type]" />
        <Endpoint Name="ServiceEndpoint1" Port="[Port1]" Protocol="[Protocol1] "/>
      </Endpoints>
    </ResourceOverrides>
        <Policies>
           <EndpointBindingPolicy CertificateRef="TestCert1" EndpointRef="ServiceEndpoint"/>
        </Policies>
  </ServiceManifestImport>
```

Em Olá que adicionar parâmetros abaixo:

```xml
  <Parameters>
    <Parameter Name="Port" DefaultValue="" />
    <Parameter Name="Protocol" DefaultValue="" />
    <Parameter Name="Type" DefaultValue="" />
    <Parameter Name="Port1" DefaultValue="" />
    <Parameter Name="Protocol1" DefaultValue="" />
  </Parameters>
```

Ao implantar o aplicativo hello agora você pode transmitir esses valores como ApplicationParameters por exemplo:

```powershell
PS C:\> New-ServiceFabricApplication -ApplicationName fabric:/myapp -ApplicationTypeName "AppType" -ApplicationTypeVersion "1.0.0" -ApplicationParameter @{Port='1001'; Protocol='https'; Type='Input'; Port1='2001'; Protocol='http'}
```

Observação: Se os valores hello fornecem para Olá ApplicationParameters está vazia voltarmos padrão toohello valor fornecido no hello ServiceManifest para Olá correspondente EndPointName.

Por exemplo:

Se estiver no hello ServiceManifest especificado

```xml
  <Resources>
    <Endpoints>
      <Endpoint Name="ServiceEndpoint1" Protocol="tcp"/>
    </Endpoints>
  </Resources>
```

Olá Port1 e valor Protocol1 parâmetros do aplicativo é nulo ou vazio. porta Olá ainda é decidida por ServiceFabric. E Olá protocolo tcp.

Vamos supor que você especifica um valor incorreto. Por exemplo, para Porta você especificou um valor de cadeia de caracteres "Foo" em vez de um int.  Novo ServiceFabricApplication comando falhará com um erro: parâmetro de substituição de saudação com nome 'ServiceEndpoint1' do atributo 'Port1' na seção 'ResourceOverrides' é inválido. valor de saudação especificado é 'Foo' e necessária é 'int'.
