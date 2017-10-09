---
title: "aaaAzure compor visualização do Service Fabric Docker | Microsoft Docs"
description: "Malha do Azure do serviço aceita Docker Compose toomake de formato-lo mais fácil contêineres de exsiting tooorchestrate usando o Service Fabric. No momento, esse suporte está na versão prévia."
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
ms.openlocfilehash: 824044fd698f0ed94c4212722bc82187905315dc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="specifying-volume-plugins-and-logging-drivers-for-your-container"></a><span data-ttu-id="7cdc8-104">Especificar plugins de volume e drivers de log para seu contêiner</span><span class="sxs-lookup"><span data-stu-id="7cdc8-104">Specifying volume plugins and logging drivers for your container</span></span>

<span data-ttu-id="7cdc8-105">Service Fabric suporta especificação de [Plugins de volume Docker ](https://docs.docker.com/engine/extend/plugins_volume/) e [Drivers de log docker](https://docs.docker.com/engine/admin/logging/overview/) para o seu serviço de contêiner.</span><span class="sxs-lookup"><span data-stu-id="7cdc8-105">Service Fabric supports specifying [Docker volume plugins](https://docs.docker.com/engine/extend/plugins_volume/) and [Docker logging drivers](https://docs.docker.com/engine/admin/logging/overview/) for your container service.</span></span> <span data-ttu-id="7cdc8-106">Olá plug-ins são especificados no manifesto de aplicativo hello, conforme mostrado no hello manifesto a seguir:</span><span class="sxs-lookup"><span data-stu-id="7cdc8-106">hello plugins are specified in hello application manifest as shown in hello following manifest:</span></span>


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

<span data-ttu-id="7cdc8-107">Em Olá anterior de exemplo, Olá `Source` marca Olá `Volume` refere-se a pasta de origem toohello.</span><span class="sxs-lookup"><span data-stu-id="7cdc8-107">In hello preceding example, hello `Source` tag for hello `Volume` refers toohello source folder.</span></span> <span data-ttu-id="7cdc8-108">pasta de origem Olá pode ser uma pasta no hello VM que hospeda os contêineres de saudação ou um repositório remoto persistente.</span><span class="sxs-lookup"><span data-stu-id="7cdc8-108">hello source folder could be a folder in hello VM that hosts hello containers or a persistent remote store.</span></span> <span data-ttu-id="7cdc8-109">Olá `Destination` marca é local Olá Olá `Source` é mapeada toowithin Olá executando o contêiner.</span><span class="sxs-lookup"><span data-stu-id="7cdc8-109">hello `Destination` tag is hello location that hello `Source` is mapped toowithin hello running container.</span></span> 

<span data-ttu-id="7cdc8-110">Ao especificar um plug-in do volume, o Service Fabric cria automaticamente volume hello usando Olá parâmetros especificados.</span><span class="sxs-lookup"><span data-stu-id="7cdc8-110">When specifying a volume plugin, Service Fabric automatically creates hello volume using hello parameters specified.</span></span> <span data-ttu-id="7cdc8-111">Olá `Source` marca é o nome de saudação do volume hello e hello `Driver` marca Especifica plug-in de driver de volume hello.</span><span class="sxs-lookup"><span data-stu-id="7cdc8-111">hello `Source` tag is hello name of hello volume, and hello `Driver` tag specifies hello volume driver plugin.</span></span> <span data-ttu-id="7cdc8-112">Opções podem ser especificadas usando Olá `DriverOption` marca conforme Olá trecho de código a seguir:</span><span class="sxs-lookup"><span data-stu-id="7cdc8-112">Options can be specified using hello `DriverOption` tag as shown in hello following snippet:</span></span>

```xml
<Volume Source="myvolume1" Destination="c:\testmountlocation4" Driver="azurefile" IsReadOnly="true">
           <DriverOption Name="share" Value="models"/>
</Volume>
```

<span data-ttu-id="7cdc8-113">Se um driver de log do Docker for especificado, é necessário toodeploy Olá toohandle de agentes (ou contêineres) registra no cluster hello.</span><span class="sxs-lookup"><span data-stu-id="7cdc8-113">If a Docker log driver is specified, it is necessary toodeploy agents (or containers) toohandle hello logs in hello cluster.</span></span>  <span data-ttu-id="7cdc8-114">Olá `DriverOption` marca pode ser usado toospecify log driver opções.</span><span class="sxs-lookup"><span data-stu-id="7cdc8-114">hello `DriverOption` tag can be used toospecify log driver options as well.</span></span>

<span data-ttu-id="7cdc8-115">Consulte toohello cluster do Service Fabric do artigos toodeploy contêineres tooa a seguir:</span><span class="sxs-lookup"><span data-stu-id="7cdc8-115">Refer toohello following articles toodeploy containers tooa Service Fabric cluster:</span></span>


[<span data-ttu-id="7cdc8-116">Implantar um contêiner no Service Fabric</span><span class="sxs-lookup"><span data-stu-id="7cdc8-116">Deploy a container on Service Fabric</span></span>](service-fabric-deploy-container.md)

