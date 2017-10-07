---
title: "aaaHow toocontainerize microservices sua malha de serviço do Azure (visualização)"
description: "Malha do Azure do serviço foi adicionado novo toocontainerize de funcionalidade microservices sua malha de serviço. Esse recurso está atualmente na visualização."
services: service-fabric
documentationcenter: .net
author: anmolah
manager: anmolah
editor: anmolah
ms.assetid: 0b41efb3-4063-4600-89f5-b077ea81fa3a
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/04/2017
ms.author: anmola
ms.openlocfilehash: 6edaff73c0828707c7fa736669ba8084663d31ed
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocontainerize-your-service-fabric-reliable-services-and-reliable-actors-preview"></a>Como toocontainerize seu confiável de malha do serviço serviços e agentes confiável (visualização)

O Service Fabric oferece suporte a colocação em contêineres de microsserviços do Service Fabric (serviços baseados em Reliable Services e Reliable Actors). Para saber mais, confira [contêineres do Service Fabric](service-fabric-containers-overview.md).


 Este recurso está em visualização e este artigo fornece Olá tooget de várias etapas em seu serviço está em execução dentro de um contêiner.  

> [!NOTE]
> Esse recurso está na versão prévia e não tem suporte. Atualmente, esse recurso só funciona para Windows.

## <a name="steps-toocontainerize-your-service-fabric-application"></a>Etapas toocontainerize seu aplicativo de malha do serviço

1. Abra seu aplicativo do Service Fabric no Visual Studio.

2. Adicionar classe [SFBinaryLoader.cs](https://github.com/Azure/service-fabric-scripts-and-templates/blob/master/code/SFBinaryLoaderForContainers/SFBinaryLoader.cs) tooyour projeto. Olá código essa classe é um binários de tempo de execução do auxiliar toocorrectly carga Olá Service Fabric dentro de seu aplicativo durante a execução dentro de um contêiner.

3. Para cada pacote de código que deseja toocontainerize, inicializar o carregador de saudação no ponto de entrada de programa hello. Adicione um construtor estático de Olá Olá arquivo de ponto de entrada do programa de tooyour de trecho código a seguir mostrado.

  ```csharp
  namespace MyApplication
  {
      internal static class Program
      {
          static Program()
          {
              SFBinaryLoader.Initialize();
          }

          /// <summary>
          /// This is hello entry point of hello service host process.
          /// </summary>
          private static void Main()
          {
  ```

4. Compilar e [empacotar](service-fabric-package-apps.md#Package-App) seu projeto. toobuild e criar um pacote, clique com botão direito Olá aplicativo no Gerenciador de soluções e escolha Olá **pacote** comando.

5. Para cada pacote de código, você precisa toocontainerize, Olá executar script do PowerShell [CreateDockerPackage.ps1](https://github.com/Azure/service-fabric-scripts-and-templates/blob/master/scripts/CodePackageToDockerPackage/CreateDockerPackage.ps1). uso de saudação é o seguinte:
  ```powershell
    $codePackagePath = 'Path toohello code package toocontainerize.'
    $dockerPackageOutputDirectoryPath = 'Output path for hello generated docker folder.'
    $applicationExeName = 'Name of hello ode package executable.'
    CreateDockerPackage.ps1 -CodePackageDirectoryPath $codePackagePath -DockerPackageOutputDirectoryPath $dockerPackageOutputDirectoryPath -ApplicationExeName $applicationExeName
 ```
  script Hello cria uma pasta com artefatos de Docker em $dockerPackageOutputDirectoryPath. Modificar Olá gerado Dockerfile tooexpose todas as portas, executadas scripts de instalação etc. com base em suas necessidades.

6. Em seguida você precisa muito[criar](service-fabric-get-started-containers.md#Build-Containers) e [push](service-fabric-get-started-containers.md#Push-Containers) seu repositório de tooyour do pacote de contêiner do Docker.

7. Modificar hello ApplicationManifest.xml e ServiceManifest.xml tooadd sua imagem de contêiner, informações do repositório, a autenticação do registro e mapeamento de porta para o host. Para modificar os manifestos hello, consulte [criar um aplicativo de contêiner do Azure Service Fabric](service-fabric-get-started-containers.md). definição de pacote de código Olá no hello serviço necessidades manifesto toobe substituído com a imagem de contêiner correspondente. Certifique-se de que toochange Olá EntryPoint tooa ContainerHost tipo.

  ```xml
<!-- Code package is your service executable. -->
<CodePackage Name="Code" Version="1.0.0">
  <EntryPoint>
    <!-- Follow this link for more information about deploying Windows containers tooService Fabric: https://aka.ms/sfguestcontainers -->
    <ContainerHost>
      <ImageName>myregistry.azurecr.io/samples/helloworldapp</ImageName>
    </ContainerHost>
  </EntryPoint>
  <!-- Pass environment variables tooyour container: -->    
</CodePackage>
  ```

8. Adicione mapeamento de porta para o host Olá para o replicador e o ponto de extremidade de serviço. Como ambas as essas portas são atribuídas em tempo de execução pela malha do serviço, Olá ContainerPort é definido toozero toouse Olá atribuído a porta para mapeamento.

 ```xml
<Policies>
  <ContainerHostPolicies CodePackageRef="Code">
    <PortBinding ContainerPort="0" EndpointRef="ServiceEndpoint"/>
    <PortBinding ContainerPort="0" EndpointRef="ReplicatorEndpoint"/>
  </ContainerHostPolicies>
</Policies>
 ```

9. tootest este aplicativo, você precisa toodeploy-tooa cluster que está executando a versão 5.7 ou superior. Além disso, você precisa tooedit e atualizar tooenable de configurações de cluster Olá esse recurso de visualização. Siga as etapas de saudação neste [artigo](service-fabric-cluster-fabric-settings.md) configuração de saudação tooadd mostrada a seguir.
```
      {
        "name": "Hosting",
        "parameters": [
          {
            "name": "FabricContainerAppsEnabled",
            "value": "true"
          }
        ]
      }
```
10. Próxima [implantar](service-fabric-deploy-remove-applications.md) Olá editado cluster de toothis do pacote de aplicativo.

Agora você deve ter um aplicativo do Service Fabric em contêineres executando seu cluster.

## <a name="next-steps"></a>Próximas etapas
* Saiba mais sobre como executar [contêineres no Service Fabric](service-fabric-get-started-containers.md).
* Saiba mais sobre Olá Service Fabric [ciclo de vida do aplicativo](service-fabric-application-lifecycle.md).
