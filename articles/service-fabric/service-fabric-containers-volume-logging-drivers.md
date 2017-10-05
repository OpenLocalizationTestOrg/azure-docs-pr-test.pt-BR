---
title: "Versão Prévia do Docker Compose do Azure Service Fabric | Microsoft Docs"
description: "O Azure Service Fabric aceita o formato do Docker Compose para facilitar a orquestração dos contêineres existentes usando o Service Fabric. No momento, esse suporte está na versão prévia."
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: ab49c4b9-74a8-4907-b75b-8d2ee84c6d90
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: subramar
ms.openlocfilehash: b12ef95add6347621f7d4865fac46568f91a1e12
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="specifying-volume-plugins-and-logging-drivers-for-your-container"></a><span data-ttu-id="47493-104">Especificar plugins de volume e drivers de log para seu contêiner</span><span class="sxs-lookup"><span data-stu-id="47493-104">Specifying volume plugins and logging drivers for your container</span></span>

<span data-ttu-id="47493-105">Service Fabric suporta especificação de [Plugins de volume Docker ](https://docs.docker.com/engine/extend/plugins_volume/) e [Drivers de log docker](https://docs.docker.com/engine/admin/logging/overview/) para o seu serviço de contêiner.</span><span class="sxs-lookup"><span data-stu-id="47493-105">Service Fabric supports specifying [Docker volume plugins](https://docs.docker.com/engine/extend/plugins_volume/) and [Docker logging drivers](https://docs.docker.com/engine/admin/logging/overview/) for your container service.</span></span> <span data-ttu-id="47493-106">Os plugins são especificados no manifesto do aplicativo, conforme mostrado no seguinte manifesto:</span><span class="sxs-lookup"><span data-stu-id="47493-106">The plugins are specified in the application manifest as shown in the following manifest:</span></span>


```xml
?xml version="1.0" encoding="UTF-8"?>
<ApplicationManifest ApplicationTypeName="WinNodeJsApp" ApplicationTypeVersion="1.0" xmlns="http://schemas.microsoft.com/2011/01/fabric" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
    <Description>Calculator Application</Description>
    <Parameters>
        <Parameter Name="ServiceInstanceCount" DefaultValue="3"></Parameter>
      <Parameter Name="MyCpuShares" DefaultValue="3"></Parameter>
    </Parameters>
    <ServiceManifestImport>
        <ServiceManifestRef ServiceManifestName="NodeServicePackage" ServiceManifestVersion="1.0"/>
     <Policies>
       <ContainerHostPolicies CodePackageRef="NodeService.Code" Isolation="hyperv"> 
        <PortBinding ContainerPort="8905" EndpointRef="Endpoint1"/>
        <RepositoryCredentials PasswordEncrypted="false" Password="****" AccountName="test"/>
        <LogConfig Driver="etwlogs" >
          <DriverOption Name="test" Value="vale"/>
        </LogConfig>
        <Volume Source="c:\workspace" Destination="c:\testmountlocation1" IsReadOnly="false"></Volume>
        <Volume Source="d:\myfolder" Destination="c:\testmountlocation2" IsReadOnly="true"> </Volume>
        <Volume Source="myexternalvolume" Destination="c:\testmountlocation3" Driver="sf" IsReadOnly="true"></Volume>
       </ContainerHostPolicies>
   </Policies>
    </ServiceManifestImport>
    <ServiceTemplates>
        <StatelessService ServiceTypeName="StatelessNodeService" InstanceCount="5">
            <SingletonPartition></SingletonPartition>
        </StatelessService>
    </ServiceTemplates>
</ApplicationManifest>
```

<span data-ttu-id="47493-107">No exemplo anterior, a `Source` marca para `Volume` refere-se à pasta de origem.</span><span class="sxs-lookup"><span data-stu-id="47493-107">In the preceding example, the `Source` tag for the `Volume` refers to the source folder.</span></span> <span data-ttu-id="47493-108">A pasta de origem pode ser uma pasta na VM que hospeda os contêineres ou um armazenamento remoto persistente.</span><span class="sxs-lookup"><span data-stu-id="47493-108">The source folder could be a folder in the VM that hosts the containers or a persistent remote store.</span></span> <span data-ttu-id="47493-109">A marca `Destination` é o local para onde `Source` será mapeado no contêiner em execução.</span><span class="sxs-lookup"><span data-stu-id="47493-109">The `Destination` tag is the location that the `Source` is mapped to within the running container.</span></span> 

<span data-ttu-id="47493-110">Ao especificar um plug-in do volume, o Service Fabric cria automaticamente o volume usando os parâmetros especificados.</span><span class="sxs-lookup"><span data-stu-id="47493-110">When specifying a volume plugin, Service Fabric automatically creates the volume using the parameters specified.</span></span> <span data-ttu-id="47493-111">A marca `Source` é o nome do volume e a marca `Driver` especifica o plug-in do driver do volume.</span><span class="sxs-lookup"><span data-stu-id="47493-111">The `Source` tag is the name of the volume, and the `Driver` tag specifies the volume driver plugin.</span></span> <span data-ttu-id="47493-112">As opções podem ser especificadas usando a marca `DriverOption` conforme mostrado no trecho a seguir:</span><span class="sxs-lookup"><span data-stu-id="47493-112">Options can be specified using the `DriverOption` tag as shown in the following snippet:</span></span>

```xml
<Volume Source="myvolume1" Destination="c:\testmountlocation4" Driver="azurefile" IsReadOnly="true">
           <DriverOption Name="share" Value="models"/>
</Volume>
```

<span data-ttu-id="47493-113">Se um driver de log docker for especificado, será necessário implantar agentes (ou contêineres) para tratar os logs no cluster.</span><span class="sxs-lookup"><span data-stu-id="47493-113">If a Docker log driver is specified, it is necessary to deploy agents (or containers) to handle the logs in the cluster.</span></span>  <span data-ttu-id="47493-114">A marca `DriverOption` também pode ser usada para especificar opções de driver de log.</span><span class="sxs-lookup"><span data-stu-id="47493-114">The `DriverOption` tag can be used to specify log driver options as well.</span></span>

<span data-ttu-id="47493-115">Consulte os seguintes artigos para implantar contêineres em um cluster do Service Fabric:</span><span class="sxs-lookup"><span data-stu-id="47493-115">Refer to the following articles to deploy containers to a Service Fabric cluster:</span></span>


[<span data-ttu-id="47493-116">Implantar um contêiner no Service Fabric</span><span class="sxs-lookup"><span data-stu-id="47493-116">Deploy a container on Service Fabric</span></span>](service-fabric-deploy-container.md)

