---
title: "Especificando pontos de extremidade de serviço do Service Fabric | Microsoft Docs"
description: "Como descrever os recursos de ponto de extremidade em um manifesto do serviço, incluindo como configurar pontos de extremidade HTTPS"
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
ms.openlocfilehash: 08141edfbc8be9bf7bf303419e1e482d5f884860
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="specify-resources-in-a-service-manifest"></a><span data-ttu-id="45be2-103">Especificar recursos em um manifesto do serviço</span><span class="sxs-lookup"><span data-stu-id="45be2-103">Specify resources in a service manifest</span></span>
## <a name="overview"></a><span data-ttu-id="45be2-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="45be2-104">Overview</span></span>
<span data-ttu-id="45be2-105">O manifesto do serviço permite que os recursos usados pelo serviço sejam declarados/alterados sem alterar o código compilado.</span><span class="sxs-lookup"><span data-stu-id="45be2-105">The service manifest allows resources that are used by the service to be declared/changed without changing the compiled code.</span></span> <span data-ttu-id="45be2-106">O Azure Service Fabric dá suporte à configuração dos recursos de ponto de extremidade para o serviço.</span><span class="sxs-lookup"><span data-stu-id="45be2-106">Azure Service Fabric supports configuration of endpoint resources for the service.</span></span> <span data-ttu-id="45be2-107">O acesso aos recursos que são especificados no manifesto do serviço pode ser controlado por meio do SecurityGroup no manifesto do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="45be2-107">The access to the resources that are specified in the service manifest can be controlled via the SecurityGroup in the application manifest.</span></span> <span data-ttu-id="45be2-108">A declaração de recursos permite que esses recursos sejam alterados no momento da implantação, o que significa que o serviço não precisa apresentar um novo mecanismo de configuração.</span><span class="sxs-lookup"><span data-stu-id="45be2-108">The declaration of resources allows these resources to be changed at deployment time, meaning the service doesn't need to introduce a new configuration mechanism.</span></span> <span data-ttu-id="45be2-109">A definição de esquema para o arquivo ServiceManifest.xml é instalada com o SDK e as ferramentas do Service Fabric em *C:\Arquivos de Programas\Microsoft SDKs\Service Fabric\schemas\ServiceFabricServiceModel.xsd*.</span><span class="sxs-lookup"><span data-stu-id="45be2-109">The schema definition for the ServiceManifest.xml file is installed with the Service Fabric SDK and tools to *C:\Program Files\Microsoft SDKs\Service Fabric\schemas\ServiceFabricServiceModel.xsd*.</span></span>

## <a name="endpoints"></a><span data-ttu-id="45be2-110">Pontos de extremidade</span><span class="sxs-lookup"><span data-stu-id="45be2-110">Endpoints</span></span>
<span data-ttu-id="45be2-111">Quando um recurso de ponto de extremidade é definido no manifesto do serviço, o Service Fabric atribui portas do intervalo de portas reservadas do aplicativo quando uma porta não é explicitamente especificada.</span><span class="sxs-lookup"><span data-stu-id="45be2-111">When an endpoint resource is defined in the service manifest, Service Fabric assigns ports from the reserved application port range when a port isn't specified explicitly.</span></span> <span data-ttu-id="45be2-112">Por exemplo, examine o ponto de extremidade *ServiceEndpoint1* especificado no trecho de manifesto fornecido após este parágrafo.</span><span class="sxs-lookup"><span data-stu-id="45be2-112">For example, look at the endpoint *ServiceEndpoint1* specified in the manifest snippet provided after this paragraph.</span></span> <span data-ttu-id="45be2-113">Além disso, os serviços também podem solicitar uma porta específica em um recurso.</span><span class="sxs-lookup"><span data-stu-id="45be2-113">Additionally, services can also request a specific port in a resource.</span></span> <span data-ttu-id="45be2-114">As réplicas do serviço em execução em nós diferentes do cluster podem receber números de porta diferentes, enquanto as réplicas do mesmo serviço em execução no mesmo nó compartilham a porta.</span><span class="sxs-lookup"><span data-stu-id="45be2-114">Service replicas running on different cluster nodes can be assigned different port numbers, while replicas of a service running on the same node share the port.</span></span> <span data-ttu-id="45be2-115">As réplicas de serviço podem usar essas portas conforme a necessidade para replicação e escuta de solicitações de clientes.</span><span class="sxs-lookup"><span data-stu-id="45be2-115">The service replicas can then use these ports as needed for replication and listening for client requests.</span></span>

```xml
<Resources>
  <Endpoints>
    <Endpoint Name="ServiceEndpoint1" Protocol="http"/>
    <Endpoint Name="ServiceEndpoint2" Protocol="http" Port="80"/>
    <Endpoint Name="ServiceEndpoint3" Protocol="https"/>
  </Endpoints>
</Resources>
```

<span data-ttu-id="45be2-116">Consulte [Configurando o Reliable Services com estado](service-fabric-reliable-services-configuration.md) para ler mais sobre como fazer referência a pontos de extremidade por meio do arquivo de configurações do pacote de configuração (settings.xml).</span><span class="sxs-lookup"><span data-stu-id="45be2-116">Refer to [Configuring stateful Reliable Services](service-fabric-reliable-services-configuration.md) to read more about referencing endpoints from the config package settings file (settings.xml).</span></span>

## <a name="example-specifying-an-http-endpoint-for-your-service"></a><span data-ttu-id="45be2-117">Exemplo: especificando um ponto de extremidade HTTP para o serviço</span><span class="sxs-lookup"><span data-stu-id="45be2-117">Example: specifying an HTTP endpoint for your service</span></span>
<span data-ttu-id="45be2-118">O manifesto do serviço a seguir define um recurso de ponto de extremidade TCP e dois recursos de ponto de extremidade HTTP no elemento &lt;Recursos&gt;.</span><span class="sxs-lookup"><span data-stu-id="45be2-118">The following service manifest defines one TCP endpoint resource and two HTTP endpoint resources in the &lt;Resources&gt; element.</span></span>

<span data-ttu-id="45be2-119">A ACL é automaticamente aplicada aos pontos de extremidade HTTP pelo Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="45be2-119">HTTP endpoints are automatically ACL'd by Service Fabric.</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<ServiceManifest Name="Stateful1Pkg"
                 Version="1.0.0"
                 xmlns="http://schemas.microsoft.com/2011/01/fabric"
                 xmlns:xsd="http://www.w3.org/2001/XMLSchema"
                 xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
  <ServiceTypes>
    <!-- This is the name of your ServiceType.
         This name must match the string used in the RegisterServiceType call in Program.cs. -->
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

  <!-- Config package is the contents of the Config directoy under PackageRoot that contains an
       independently updateable and versioned set of custom configuration settings for your service. -->
  <ConfigPackage Name="Config" Version="1.0.0" />

  <Resources>
    <Endpoints>
      <!-- This endpoint is used by the communication listener to obtain the port number on which to
           listen. Note that if your service is partitioned, this port is shared with
           replicas of different partitions that are placed in your code. -->
      <Endpoint Name="ServiceEndpoint1" Protocol="http"/>
      <Endpoint Name="ServiceEndpoint2" Protocol="http" Port="80"/>
      <Endpoint Name="ServiceEndpoint3" Protocol="https"/>

      <!-- This endpoint is used by the replicator for replicating the state of your service.
           This endpoint is configured through the ReplicatorSettings config section in the Settings.xml
           file under the ConfigPackage. -->
      <Endpoint Name="ReplicatorEndpoint" />
    </Endpoints>
  </Resources>
</ServiceManifest>
```

## <a name="example-specifying-an-https-endpoint-for-your-service"></a><span data-ttu-id="45be2-120">Exemplo: especificando um ponto de extremidade HTTPS para o serviço</span><span class="sxs-lookup"><span data-stu-id="45be2-120">Example: specifying an HTTPS endpoint for your service</span></span>
<span data-ttu-id="45be2-121">O protocolo HTTPS fornece autenticação de servidor e também é usado para criptografar a comunicação cliente-servidor.</span><span class="sxs-lookup"><span data-stu-id="45be2-121">The HTTPS protocol provides server authentication and is also used for encrypting client-server communication.</span></span> <span data-ttu-id="45be2-122">Para habilitar o HTTPS em seu serviço do Service Fabric, especifique o protocolo na seção *Recursos -> Pontos de Extremidade -> Ponto de Extremidade* do manifesto do serviço, conforme mostrado anteriormente para o ponto de extremidade *ServiceEndpoint3*.</span><span class="sxs-lookup"><span data-stu-id="45be2-122">To enable HTTPS on your Service Fabric service, specify the protocol in the *Resources -> Endpoints -> Endpoint* section of the service manifest, as shown earlier for the endpoint *ServiceEndpoint3*.</span></span>

> [!NOTE]
> <span data-ttu-id="45be2-123">O protocolo de um serviço não pode ser alterado durante a atualização do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="45be2-123">A service’s protocol cannot be changed during application upgrade.</span></span> <span data-ttu-id="45be2-124">Se ele for alterado durante a atualização, será uma alteração significativa.</span><span class="sxs-lookup"><span data-stu-id="45be2-124">If it is changed during upgrade, it is a breaking change.</span></span>
> 
> 

<span data-ttu-id="45be2-125">Este está um exemplo de ApplicationManifest que precisa ser definido para HTTPS.</span><span class="sxs-lookup"><span data-stu-id="45be2-125">Here is an example ApplicationManifest that you need to set for HTTPS.</span></span> <span data-ttu-id="45be2-126">Deve ser fornecida impressão digital para seu certificado.</span><span class="sxs-lookup"><span data-stu-id="45be2-126">The thumbprint for your certificate must be provided.</span></span> <span data-ttu-id="45be2-127">O EndpointRef é uma referência a EndpointResource no ServiceManifest, para o qual você definiu o protocolo HTTPS.</span><span class="sxs-lookup"><span data-stu-id="45be2-127">The EndpointRef is a reference to EndpointResource in ServiceManifest, for which you set the HTTPS protocol.</span></span> <span data-ttu-id="45be2-128">Você pode adicionar mais de um EndpointCertificate.</span><span class="sxs-lookup"><span data-stu-id="45be2-128">You can add more than one EndpointCertificate.</span></span>  

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
  <!-- Import the ServiceManifest from the ServicePackage. The ServiceManifestName and ServiceManifestVersion
       should match the Name and Version attributes of the ServiceManifest element defined in the
       ServiceManifest.xml file. -->
  <ServiceManifestImport>
    <ServiceManifestRef ServiceManifestName="Stateful1Pkg" ServiceManifestVersion="1.0.0" />
    <ConfigOverrides />
    <Policies>
      <EndpointBindingPolicy CertificateRef="TestCert1" EndpointRef="ServiceEndpoint3"/>
    </Policies>
  </ServiceManifestImport>
  <DefaultServices>
    <!-- The section below creates instances of service types when an instance of this
         application type is created. You can also create one or more instances of service type by using the
         Service Fabric PowerShell module.

         The attribute ServiceTypeName below must match the name defined in the imported ServiceManifest.xml file. -->
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

## <a name="overriding-endpoints-in-servicemanifestxml"></a><span data-ttu-id="45be2-129">Substituição dos pontos de extremidade em ServiceManifest.xml</span><span class="sxs-lookup"><span data-stu-id="45be2-129">Overriding Endpoints in ServiceManifest.xml</span></span>

<span data-ttu-id="45be2-130">No ApplicationManifest, adicione uma seção ResourceOverrides que será uma irmã da seção ConfigOverrides.</span><span class="sxs-lookup"><span data-stu-id="45be2-130">In the ApplicationManifest add a ResourceOverrides section which will be a sibling to ConfigOverrides section.</span></span> <span data-ttu-id="45be2-131">Nessa seção, você pode especificar a substituição da seção Pontos de extremidade na seção de recursos especificada no Manifesto do serviço.</span><span class="sxs-lookup"><span data-stu-id="45be2-131">In this section you can specify the override for the Endpoints section in the resources section specified in the Service manifest.</span></span>

<span data-ttu-id="45be2-132">Para substituir o Ponto de extremidade no ServiceManifest usando ApplicationParameters, altere o ApplicationManifest da seguinte forma:</span><span class="sxs-lookup"><span data-stu-id="45be2-132">In order to override EndPoint in ServiceManifest using ApplicationParameters change the ApplicationManifest as following:</span></span>

<span data-ttu-id="45be2-133">Na seção ServiceManifestImport, adicione uma nova seção "ResourceOverrides"</span><span class="sxs-lookup"><span data-stu-id="45be2-133">In the ServiceManifestImport section add a new section "ResourceOverrides"</span></span>

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

<span data-ttu-id="45be2-134">Nos Parâmetros, adicione o seguinte:</span><span class="sxs-lookup"><span data-stu-id="45be2-134">In the Parameters add below:</span></span>

```xml
  <Parameters>
    <Parameter Name="Port" DefaultValue="" />
    <Parameter Name="Protocol" DefaultValue="" />
    <Parameter Name="Type" DefaultValue="" />
    <Parameter Name="Port1" DefaultValue="" />
    <Parameter Name="Protocol1" DefaultValue="" />
  </Parameters>
```

<span data-ttu-id="45be2-135">Agora, durante e implantação do aplicativo, você pode passar esses valores como ApplicationParameters, por exemplo:</span><span class="sxs-lookup"><span data-stu-id="45be2-135">While deploying the application now you can pass in these values as ApplicationParameters for example:</span></span>

```powershell
PS C:\> New-ServiceFabricApplication -ApplicationName fabric:/myapp -ApplicationTypeName "AppType" -ApplicationTypeVersion "1.0.0" -ApplicationParameter @{Port='1001'; Protocol='https'; Type='Input'; Port1='2001'; Protocol='http'}
```

<span data-ttu-id="45be2-136">Observação: se os valores fornecidos para o ApplicationParameters estiverem vazios, volte para o valor padrão fornecido no ServiceManifest para o EndPointName correspondente.</span><span class="sxs-lookup"><span data-stu-id="45be2-136">Note: If the values provide for the ApplicationParameters is empty we go back to the default value provided in the ServiceManifest for the corresponding EndPointName.</span></span>

<span data-ttu-id="45be2-137">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="45be2-137">For example:</span></span>

<span data-ttu-id="45be2-138">Se estiver no ServiceManifest especificado</span><span class="sxs-lookup"><span data-stu-id="45be2-138">If in the ServiceManifest you specified</span></span>

```xml
  <Resources>
    <Endpoints>
      <Endpoint Name="ServiceEndpoint1" Protocol="tcp"/>
    </Endpoints>
  </Resources>
```

<span data-ttu-id="45be2-139">E o valor de Port1 e Protocol1 para parâmetros do Aplicativo for nulo ou vazio.</span><span class="sxs-lookup"><span data-stu-id="45be2-139">And the Port1 and Protocol1 value for Application parameters is null or empty.</span></span> <span data-ttu-id="45be2-140">A porta ainda é decidida pelo ServiceFabric.</span><span class="sxs-lookup"><span data-stu-id="45be2-140">The port is still decided by ServiceFabric.</span></span> <span data-ttu-id="45be2-141">E o protocolo será tcp.</span><span class="sxs-lookup"><span data-stu-id="45be2-141">And the Protocol will tcp.</span></span>

<span data-ttu-id="45be2-142">Vamos supor que você especifica um valor incorreto.</span><span class="sxs-lookup"><span data-stu-id="45be2-142">Suppose you specify a wrong value.</span></span> <span data-ttu-id="45be2-143">Por exemplo, para Porta você especificou um valor de cadeia de caracteres "Foo" em vez de um int.  O comando New-ServiceFabricApplication falhará com um erro: o parâmetro de substituição com o nome 'ServiceEndpoint1', atributo 'Port1' na seção 'ResourceOverrides' é inválido.</span><span class="sxs-lookup"><span data-stu-id="45be2-143">Like for Port you specified a string value "Foo" instead of an int.  New-ServiceFabricApplication command will fail with an error : The override parameter with name 'ServiceEndpoint1' attribute 'Port1' in section 'ResourceOverrides' is invalid.</span></span> <span data-ttu-id="45be2-144">O valor especificado é 'Foo', e exige 'int'.</span><span class="sxs-lookup"><span data-stu-id="45be2-144">The value specified is 'Foo' and required is 'int'.</span></span>
