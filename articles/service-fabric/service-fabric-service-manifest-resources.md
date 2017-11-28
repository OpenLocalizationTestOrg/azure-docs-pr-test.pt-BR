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
# <a name="specify-resources-in-a-service-manifest"></a><span data-ttu-id="04bdb-103">Especificar recursos em um manifesto do serviço</span><span class="sxs-lookup"><span data-stu-id="04bdb-103">Specify resources in a service manifest</span></span>
## <a name="overview"></a><span data-ttu-id="04bdb-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="04bdb-104">Overview</span></span>
<span data-ttu-id="04bdb-105">manifesto do serviço Olá permite que os recursos que são usados por Olá serviço toobe declarado/alterado sem alterar o código de saudação compilado.</span><span class="sxs-lookup"><span data-stu-id="04bdb-105">hello service manifest allows resources that are used by hello service toobe declared/changed without changing hello compiled code.</span></span> <span data-ttu-id="04bdb-106">Malha do serviço do Azure dá suporte à configuração de recursos de ponto de extremidade para o serviço de saudação.</span><span class="sxs-lookup"><span data-stu-id="04bdb-106">Azure Service Fabric supports configuration of endpoint resources for hello service.</span></span> <span data-ttu-id="04bdb-107">Olá acessar toohello os recursos que são especificados no manifesto do serviço Olá podem ser controlados por meio de Olá SecurityGroup no manifesto de aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="04bdb-107">hello access toohello resources that are specified in hello service manifest can be controlled via hello SecurityGroup in hello application manifest.</span></span> <span data-ttu-id="04bdb-108">declaração de saudação de recursos permite que esses toobe recursos alterados no momento da implantação, o que significa que o serviço de saudação não precisa toointroduce um novo mecanismo de configuração.</span><span class="sxs-lookup"><span data-stu-id="04bdb-108">hello declaration of resources allows these resources toobe changed at deployment time, meaning hello service doesn't need toointroduce a new configuration mechanism.</span></span> <span data-ttu-id="04bdb-109">Olá definição de esquema de arquivo ServiceManifest.xml de saudação é instalada com hello SDK do Service Fabric e ferramentas muito*C:\Program Files\Microsoft SDKs\Service Fabric\schemas\ServiceFabricServiceModel.xsd*.</span><span class="sxs-lookup"><span data-stu-id="04bdb-109">hello schema definition for hello ServiceManifest.xml file is installed with hello Service Fabric SDK and tools too*C:\Program Files\Microsoft SDKs\Service Fabric\schemas\ServiceFabricServiceModel.xsd*.</span></span>

## <a name="endpoints"></a><span data-ttu-id="04bdb-110">Pontos de extremidade</span><span class="sxs-lookup"><span data-stu-id="04bdb-110">Endpoints</span></span>
<span data-ttu-id="04bdb-111">Quando um recurso de ponto de extremidade é definido no manifesto do serviço hello, o Service Fabric atribui portas do intervalo de portas de aplicativo hello reservado quando uma porta não for especificada explicitamente.</span><span class="sxs-lookup"><span data-stu-id="04bdb-111">When an endpoint resource is defined in hello service manifest, Service Fabric assigns ports from hello reserved application port range when a port isn't specified explicitly.</span></span> <span data-ttu-id="04bdb-112">Por exemplo, procure no ponto de extremidade Olá *ServiceEndpoint1* especificado no fragmento de manifesto Olá fornecido após este parágrafo.</span><span class="sxs-lookup"><span data-stu-id="04bdb-112">For example, look at hello endpoint *ServiceEndpoint1* specified in hello manifest snippet provided after this paragraph.</span></span> <span data-ttu-id="04bdb-113">Além disso, os serviços também podem solicitar uma porta específica em um recurso.</span><span class="sxs-lookup"><span data-stu-id="04bdb-113">Additionally, services can also request a specific port in a resource.</span></span> <span data-ttu-id="04bdb-114">Réplicas de serviço em execução em nós de cluster diferente podem ser atribuídas diferentes números de porta, enquanto as réplicas de um serviço em execução no Olá a mesma porta de saudação do compartilhamento de nó.</span><span class="sxs-lookup"><span data-stu-id="04bdb-114">Service replicas running on different cluster nodes can be assigned different port numbers, while replicas of a service running on hello same node share hello port.</span></span> <span data-ttu-id="04bdb-115">réplicas de serviço Olá podem usar essas portas conforme necessário para a replicação e escutar solicitações de clientes.</span><span class="sxs-lookup"><span data-stu-id="04bdb-115">hello service replicas can then use these ports as needed for replication and listening for client requests.</span></span>

```xml
<Resources>
  <Endpoints>
    <Endpoint Name="ServiceEndpoint1" Protocol="http"/>
    <Endpoint Name="ServiceEndpoint2" Protocol="http" Port="80"/>
    <Endpoint Name="ServiceEndpoint3" Protocol="https"/>
  </Endpoints>
</Resources>
```

<span data-ttu-id="04bdb-116">Consulte também[configuração com monitoração de estado confiável dos serviços](service-fabric-reliable-services-configuration.md) tooread mais sobre como fazer referência a pontos de extremidade do arquivo de configurações de pacote de configuração de saudação (settings.xml).</span><span class="sxs-lookup"><span data-stu-id="04bdb-116">Refer too[Configuring stateful Reliable Services](service-fabric-reliable-services-configuration.md) tooread more about referencing endpoints from hello config package settings file (settings.xml).</span></span>

## <a name="example-specifying-an-http-endpoint-for-your-service"></a><span data-ttu-id="04bdb-117">Exemplo: especificando um ponto de extremidade HTTP para o serviço</span><span class="sxs-lookup"><span data-stu-id="04bdb-117">Example: specifying an HTTP endpoint for your service</span></span>
<span data-ttu-id="04bdb-118">Olá manifesto de serviço a seguir define um recurso de ponto de extremidade TCP e dois recursos de ponto de extremidade HTTP no hello &lt;recursos&gt; elemento.</span><span class="sxs-lookup"><span data-stu-id="04bdb-118">hello following service manifest defines one TCP endpoint resource and two HTTP endpoint resources in hello &lt;Resources&gt; element.</span></span>

<span data-ttu-id="04bdb-119">A ACL é automaticamente aplicada aos pontos de extremidade HTTP pelo Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="04bdb-119">HTTP endpoints are automatically ACL'd by Service Fabric.</span></span>

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

## <a name="example-specifying-an-https-endpoint-for-your-service"></a><span data-ttu-id="04bdb-120">Exemplo: especificando um ponto de extremidade HTTPS para o serviço</span><span class="sxs-lookup"><span data-stu-id="04bdb-120">Example: specifying an HTTPS endpoint for your service</span></span>
<span data-ttu-id="04bdb-121">Olá protocolo HTTPS fornece autenticação de servidor e também é usada para criptografar a comunicação cliente-servidor.</span><span class="sxs-lookup"><span data-stu-id="04bdb-121">hello HTTPS protocol provides server authentication and is also used for encrypting client-server communication.</span></span> <span data-ttu-id="04bdb-122">tooenable HTTPS no serviço do Service Fabric, especificar o protocolo de saudação em Olá *recursos -> pontos de extremidade -> ponto de extremidade* seção saudação do manifesto do serviço, conforme mostrado anteriormente para o ponto de extremidade Olá *ServiceEndpoint3* .</span><span class="sxs-lookup"><span data-stu-id="04bdb-122">tooenable HTTPS on your Service Fabric service, specify hello protocol in hello *Resources -> Endpoints -> Endpoint* section of hello service manifest, as shown earlier for hello endpoint *ServiceEndpoint3*.</span></span>

> [!NOTE]
> <span data-ttu-id="04bdb-123">O protocolo de um serviço não pode ser alterado durante a atualização do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="04bdb-123">A service’s protocol cannot be changed during application upgrade.</span></span> <span data-ttu-id="04bdb-124">Se ele for alterado durante a atualização, será uma alteração significativa.</span><span class="sxs-lookup"><span data-stu-id="04bdb-124">If it is changed during upgrade, it is a breaking change.</span></span>
> 
> 

<span data-ttu-id="04bdb-125">Aqui está um exemplo ApplicationManifest que você precisa tooset para HTTPS.</span><span class="sxs-lookup"><span data-stu-id="04bdb-125">Here is an example ApplicationManifest that you need tooset for HTTPS.</span></span> <span data-ttu-id="04bdb-126">impressão digital de saudação do certificado deve ser fornecido.</span><span class="sxs-lookup"><span data-stu-id="04bdb-126">hello thumbprint for your certificate must be provided.</span></span> <span data-ttu-id="04bdb-127">Olá EndpointRef é tooEndpointResource uma referência em ServiceManifest, para que você definir o protocolo HTTPS de saudação.</span><span class="sxs-lookup"><span data-stu-id="04bdb-127">hello EndpointRef is a reference tooEndpointResource in ServiceManifest, for which you set hello HTTPS protocol.</span></span> <span data-ttu-id="04bdb-128">Você pode adicionar mais de um EndpointCertificate.</span><span class="sxs-lookup"><span data-stu-id="04bdb-128">You can add more than one EndpointCertificate.</span></span>  

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

## <a name="overriding-endpoints-in-servicemanifestxml"></a><span data-ttu-id="04bdb-129">Substituição dos pontos de extremidade em ServiceManifest.xml</span><span class="sxs-lookup"><span data-stu-id="04bdb-129">Overriding Endpoints in ServiceManifest.xml</span></span>

<span data-ttu-id="04bdb-130">Em Olá ApplicationManifest adicione uma seção de ResourceOverrides que será uma seção de tooConfigOverrides irmão.</span><span class="sxs-lookup"><span data-stu-id="04bdb-130">In hello ApplicationManifest add a ResourceOverrides section which will be a sibling tooConfigOverrides section.</span></span> <span data-ttu-id="04bdb-131">Nesta seção, você pode especificar Olá substituição para a seção de pontos de extremidade de saudação na seção de recursos de saudação especificada no manifesto do serviço de saudação.</span><span class="sxs-lookup"><span data-stu-id="04bdb-131">In this section you can specify hello override for hello Endpoints section in hello resources section specified in hello Service manifest.</span></span>

<span data-ttu-id="04bdb-132">Em ordem toooverride ponto de extremidade no ServiceManifest usando o altere ApplicationParameters Olá ApplicationManifest como a seguir:</span><span class="sxs-lookup"><span data-stu-id="04bdb-132">In order toooverride EndPoint in ServiceManifest using ApplicationParameters change hello ApplicationManifest as following:</span></span>

<span data-ttu-id="04bdb-133">Em Olá seção servicemanifestimport ao adicionar uma nova seção "ResourceOverrides"</span><span class="sxs-lookup"><span data-stu-id="04bdb-133">In hello ServiceManifestImport section add a new section "ResourceOverrides"</span></span>

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

<span data-ttu-id="04bdb-134">Em Olá que adicionar parâmetros abaixo:</span><span class="sxs-lookup"><span data-stu-id="04bdb-134">In hello Parameters add below:</span></span>

```xml
  <Parameters>
    <Parameter Name="Port" DefaultValue="" />
    <Parameter Name="Protocol" DefaultValue="" />
    <Parameter Name="Type" DefaultValue="" />
    <Parameter Name="Port1" DefaultValue="" />
    <Parameter Name="Protocol1" DefaultValue="" />
  </Parameters>
```

<span data-ttu-id="04bdb-135">Ao implantar o aplicativo hello agora você pode transmitir esses valores como ApplicationParameters por exemplo:</span><span class="sxs-lookup"><span data-stu-id="04bdb-135">While deploying hello application now you can pass in these values as ApplicationParameters for example:</span></span>

```powershell
PS C:\> New-ServiceFabricApplication -ApplicationName fabric:/myapp -ApplicationTypeName "AppType" -ApplicationTypeVersion "1.0.0" -ApplicationParameter @{Port='1001'; Protocol='https'; Type='Input'; Port1='2001'; Protocol='http'}
```

<span data-ttu-id="04bdb-136">Observação: Se os valores hello fornecem para Olá ApplicationParameters está vazia voltarmos padrão toohello valor fornecido no hello ServiceManifest para Olá correspondente EndPointName.</span><span class="sxs-lookup"><span data-stu-id="04bdb-136">Note: If hello values provide for hello ApplicationParameters is empty we go back toohello default value provided in hello ServiceManifest for hello corresponding EndPointName.</span></span>

<span data-ttu-id="04bdb-137">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="04bdb-137">For example:</span></span>

<span data-ttu-id="04bdb-138">Se estiver no hello ServiceManifest especificado</span><span class="sxs-lookup"><span data-stu-id="04bdb-138">If in hello ServiceManifest you specified</span></span>

```xml
  <Resources>
    <Endpoints>
      <Endpoint Name="ServiceEndpoint1" Protocol="tcp"/>
    </Endpoints>
  </Resources>
```

<span data-ttu-id="04bdb-139">Olá Port1 e valor Protocol1 parâmetros do aplicativo é nulo ou vazio.</span><span class="sxs-lookup"><span data-stu-id="04bdb-139">And hello Port1 and Protocol1 value for Application parameters is null or empty.</span></span> <span data-ttu-id="04bdb-140">porta Olá ainda é decidida por ServiceFabric.</span><span class="sxs-lookup"><span data-stu-id="04bdb-140">hello port is still decided by ServiceFabric.</span></span> <span data-ttu-id="04bdb-141">E Olá protocolo tcp.</span><span class="sxs-lookup"><span data-stu-id="04bdb-141">And hello Protocol will tcp.</span></span>

<span data-ttu-id="04bdb-142">Vamos supor que você especifica um valor incorreto.</span><span class="sxs-lookup"><span data-stu-id="04bdb-142">Suppose you specify a wrong value.</span></span> <span data-ttu-id="04bdb-143">Por exemplo, para Porta você especificou um valor de cadeia de caracteres "Foo" em vez de um int.  Novo ServiceFabricApplication comando falhará com um erro: parâmetro de substituição de saudação com nome 'ServiceEndpoint1' do atributo 'Port1' na seção 'ResourceOverrides' é inválido.</span><span class="sxs-lookup"><span data-stu-id="04bdb-143">Like for Port you specified a string value "Foo" instead of an int.  New-ServiceFabricApplication command will fail with an error : hello override parameter with name 'ServiceEndpoint1' attribute 'Port1' in section 'ResourceOverrides' is invalid.</span></span> <span data-ttu-id="04bdb-144">valor de saudação especificado é 'Foo' e necessária é 'int'.</span><span class="sxs-lookup"><span data-stu-id="04bdb-144">hello value specified is 'Foo' and required is 'int'.</span></span>
