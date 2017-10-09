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
# <a name="specifying-volume-plugins-and-logging-drivers-for-your-container"></a>Especificar plugins de volume e drivers de log para seu contêiner

Service Fabric suporta especificação de [Plugins de volume Docker ](https://docs.docker.com/engine/extend/plugins_volume/) e [Drivers de log docker](https://docs.docker.com/engine/admin/logging/overview/) para o seu serviço de contêiner. Olá plug-ins são especificados no manifesto de aplicativo hello, conforme mostrado no hello manifesto a seguir:


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

Em Olá anterior de exemplo, Olá `Source` marca Olá `Volume` refere-se a pasta de origem toohello. pasta de origem Olá pode ser uma pasta no hello VM que hospeda os contêineres de saudação ou um repositório remoto persistente. Olá `Destination` marca é local Olá Olá `Source` é mapeada toowithin Olá executando o contêiner. 

Ao especificar um plug-in do volume, o Service Fabric cria automaticamente volume hello usando Olá parâmetros especificados. Olá `Source` marca é o nome de saudação do volume hello e hello `Driver` marca Especifica plug-in de driver de volume hello. Opções podem ser especificadas usando Olá `DriverOption` marca conforme Olá trecho de código a seguir:

```xml
<Volume Source="myvolume1" Destination="c:\testmountlocation4" Driver="azurefile" IsReadOnly="true">
           <DriverOption Name="share" Value="models"/>
</Volume>
```

Se um driver de log do Docker for especificado, é necessário toodeploy Olá toohandle de agentes (ou contêineres) registra no cluster hello.  Olá `DriverOption` marca pode ser usado toospecify log driver opções.

Consulte toohello cluster do Service Fabric do artigos toodeploy contêineres tooa a seguir:


[Implantar um contêiner no Service Fabric](service-fabric-deploy-container.md)

