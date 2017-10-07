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
# <a name="how-toocontainerize-your-service-fabric-reliable-services-and-reliable-actors-preview"></a><span data-ttu-id="6b9fe-104">Como toocontainerize seu confiável de malha do serviço serviços e agentes confiável (visualização)</span><span class="sxs-lookup"><span data-stu-id="6b9fe-104">How toocontainerize your Service Fabric Reliable Services and Reliable Actors (Preview)</span></span>

<span data-ttu-id="6b9fe-105">O Service Fabric oferece suporte a colocação em contêineres de microsserviços do Service Fabric (serviços baseados em Reliable Services e Reliable Actors).</span><span class="sxs-lookup"><span data-stu-id="6b9fe-105">Service Fabric supports containerizing Service Fabric microservices (Reliable Services, and Reliable Actor based services).</span></span> <span data-ttu-id="6b9fe-106">Para saber mais, confira [contêineres do Service Fabric](service-fabric-containers-overview.md).</span><span class="sxs-lookup"><span data-stu-id="6b9fe-106">For more information, see [service fabric containers](service-fabric-containers-overview.md).</span></span>


 <span data-ttu-id="6b9fe-107">Este recurso está em visualização e este artigo fornece Olá tooget de várias etapas em seu serviço está em execução dentro de um contêiner.</span><span class="sxs-lookup"><span data-stu-id="6b9fe-107">This feature is in preview and this article provides hello various steps tooget your service running inside a container.</span></span>  

> [!NOTE]
> <span data-ttu-id="6b9fe-108">Esse recurso está na versão prévia e não tem suporte.</span><span class="sxs-lookup"><span data-stu-id="6b9fe-108">This feature is in preview and is not supported in production.</span></span> <span data-ttu-id="6b9fe-109">Atualmente, esse recurso só funciona para Windows.</span><span class="sxs-lookup"><span data-stu-id="6b9fe-109">Currently this feature only works for Windows.</span></span>

## <a name="steps-toocontainerize-your-service-fabric-application"></a><span data-ttu-id="6b9fe-110">Etapas toocontainerize seu aplicativo de malha do serviço</span><span class="sxs-lookup"><span data-stu-id="6b9fe-110">Steps toocontainerize your Service Fabric Application</span></span>

1. <span data-ttu-id="6b9fe-111">Abra seu aplicativo do Service Fabric no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="6b9fe-111">Open your Service Fabric application in Visual Studio.</span></span>

2. <span data-ttu-id="6b9fe-112">Adicionar classe [SFBinaryLoader.cs](https://github.com/Azure/service-fabric-scripts-and-templates/blob/master/code/SFBinaryLoaderForContainers/SFBinaryLoader.cs) tooyour projeto.</span><span class="sxs-lookup"><span data-stu-id="6b9fe-112">Add class [SFBinaryLoader.cs](https://github.com/Azure/service-fabric-scripts-and-templates/blob/master/code/SFBinaryLoaderForContainers/SFBinaryLoader.cs) tooyour project.</span></span> <span data-ttu-id="6b9fe-113">Olá código essa classe é um binários de tempo de execução do auxiliar toocorrectly carga Olá Service Fabric dentro de seu aplicativo durante a execução dentro de um contêiner.</span><span class="sxs-lookup"><span data-stu-id="6b9fe-113">hello code in this class is a helper toocorrectly load hello Service Fabric runtime binaries inside your application when running inside a container.</span></span>

3. <span data-ttu-id="6b9fe-114">Para cada pacote de código que deseja toocontainerize, inicializar o carregador de saudação no ponto de entrada de programa hello.</span><span class="sxs-lookup"><span data-stu-id="6b9fe-114">For each code package you would like toocontainerize, initialize hello loader at hello program entry point.</span></span> <span data-ttu-id="6b9fe-115">Adicione um construtor estático de Olá Olá arquivo de ponto de entrada do programa de tooyour de trecho código a seguir mostrado.</span><span class="sxs-lookup"><span data-stu-id="6b9fe-115">Add hello static constructor shown in hello following code snippet tooyour program entry point file.</span></span>

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

4. <span data-ttu-id="6b9fe-116">Compilar e [empacotar](service-fabric-package-apps.md#Package-App) seu projeto.</span><span class="sxs-lookup"><span data-stu-id="6b9fe-116">Build and [package](service-fabric-package-apps.md#Package-App) your project.</span></span> <span data-ttu-id="6b9fe-117">toobuild e criar um pacote, clique com botão direito Olá aplicativo no Gerenciador de soluções e escolha Olá **pacote** comando.</span><span class="sxs-lookup"><span data-stu-id="6b9fe-117">toobuild and create a package, right-click hello application project in Solution Explorer and choose hello **Package** command.</span></span>

5. <span data-ttu-id="6b9fe-118">Para cada pacote de código, você precisa toocontainerize, Olá executar script do PowerShell [CreateDockerPackage.ps1](https://github.com/Azure/service-fabric-scripts-and-templates/blob/master/scripts/CodePackageToDockerPackage/CreateDockerPackage.ps1).</span><span class="sxs-lookup"><span data-stu-id="6b9fe-118">For every code package you need toocontainerize, run hello PowerShell script [CreateDockerPackage.ps1](https://github.com/Azure/service-fabric-scripts-and-templates/blob/master/scripts/CodePackageToDockerPackage/CreateDockerPackage.ps1).</span></span> <span data-ttu-id="6b9fe-119">uso de saudação é o seguinte:</span><span class="sxs-lookup"><span data-stu-id="6b9fe-119">hello usage is as follows:</span></span>
  ```powershell
    $codePackagePath = 'Path toohello code package toocontainerize.'
    $dockerPackageOutputDirectoryPath = 'Output path for hello generated docker folder.'
    $applicationExeName = 'Name of hello ode package executable.'
    CreateDockerPackage.ps1 -CodePackageDirectoryPath $codePackagePath -DockerPackageOutputDirectoryPath $dockerPackageOutputDirectoryPath -ApplicationExeName $applicationExeName
 ```
  <span data-ttu-id="6b9fe-120">script Hello cria uma pasta com artefatos de Docker em $dockerPackageOutputDirectoryPath.</span><span class="sxs-lookup"><span data-stu-id="6b9fe-120">hello script creates a folder with Docker artifacts at $dockerPackageOutputDirectoryPath.</span></span> <span data-ttu-id="6b9fe-121">Modificar Olá gerado Dockerfile tooexpose todas as portas, executadas scripts de instalação etc. com base em suas necessidades.</span><span class="sxs-lookup"><span data-stu-id="6b9fe-121">Modify hello generated Dockerfile tooexpose any ports, run setup scripts etc. based on your needs.</span></span>

6. <span data-ttu-id="6b9fe-122">Em seguida você precisa muito[criar](service-fabric-get-started-containers.md#Build-Containers) e [push](service-fabric-get-started-containers.md#Push-Containers) seu repositório de tooyour do pacote de contêiner do Docker.</span><span class="sxs-lookup"><span data-stu-id="6b9fe-122">Next you need too[build](service-fabric-get-started-containers.md#Build-Containers) and [push](service-fabric-get-started-containers.md#Push-Containers) your Docker container package tooyour repository.</span></span>

7. <span data-ttu-id="6b9fe-123">Modificar hello ApplicationManifest.xml e ServiceManifest.xml tooadd sua imagem de contêiner, informações do repositório, a autenticação do registro e mapeamento de porta para o host.</span><span class="sxs-lookup"><span data-stu-id="6b9fe-123">Modify hello ApplicationManifest.xml and ServiceManifest.xml tooadd your container image, repository information, registry authentication, and port-to-host mapping.</span></span> <span data-ttu-id="6b9fe-124">Para modificar os manifestos hello, consulte [criar um aplicativo de contêiner do Azure Service Fabric](service-fabric-get-started-containers.md).</span><span class="sxs-lookup"><span data-stu-id="6b9fe-124">For modifying hello manifests, see [Create an Azure Service Fabric container application](service-fabric-get-started-containers.md).</span></span> <span data-ttu-id="6b9fe-125">definição de pacote de código Olá no hello serviço necessidades manifesto toobe substituído com a imagem de contêiner correspondente.</span><span class="sxs-lookup"><span data-stu-id="6b9fe-125">hello code package definition in hello service manifest needs toobe replaced with corresponding container image.</span></span> <span data-ttu-id="6b9fe-126">Certifique-se de que toochange Olá EntryPoint tooa ContainerHost tipo.</span><span class="sxs-lookup"><span data-stu-id="6b9fe-126">Make sure toochange hello EntryPoint tooa ContainerHost type.</span></span>

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

8. <span data-ttu-id="6b9fe-127">Adicione mapeamento de porta para o host Olá para o replicador e o ponto de extremidade de serviço.</span><span class="sxs-lookup"><span data-stu-id="6b9fe-127">Add hello port-to-host mapping for your replicator and service endpoint.</span></span> <span data-ttu-id="6b9fe-128">Como ambas as essas portas são atribuídas em tempo de execução pela malha do serviço, Olá ContainerPort é definido toozero toouse Olá atribuído a porta para mapeamento.</span><span class="sxs-lookup"><span data-stu-id="6b9fe-128">Since both these ports are assigned at runtime by Service Fabric, hello ContainerPort is set toozero toouse hello assigned port for mapping.</span></span>

 ```xml
<Policies>
  <ContainerHostPolicies CodePackageRef="Code">
    <PortBinding ContainerPort="0" EndpointRef="ServiceEndpoint"/>
    <PortBinding ContainerPort="0" EndpointRef="ReplicatorEndpoint"/>
  </ContainerHostPolicies>
</Policies>
 ```

9. <span data-ttu-id="6b9fe-129">tootest este aplicativo, você precisa toodeploy-tooa cluster que está executando a versão 5.7 ou superior.</span><span class="sxs-lookup"><span data-stu-id="6b9fe-129">tootest this application, you need toodeploy it tooa cluster that is running version 5.7 or higher.</span></span> <span data-ttu-id="6b9fe-130">Além disso, você precisa tooedit e atualizar tooenable de configurações de cluster Olá esse recurso de visualização.</span><span class="sxs-lookup"><span data-stu-id="6b9fe-130">In addition, you need tooedit and update hello cluster settings tooenable this preview feature.</span></span> <span data-ttu-id="6b9fe-131">Siga as etapas de saudação neste [artigo](service-fabric-cluster-fabric-settings.md) configuração de saudação tooadd mostrada a seguir.</span><span class="sxs-lookup"><span data-stu-id="6b9fe-131">Follow hello steps in this [article](service-fabric-cluster-fabric-settings.md) tooadd hello setting shown next.</span></span>
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
10. <span data-ttu-id="6b9fe-132">Próxima [implantar](service-fabric-deploy-remove-applications.md) Olá editado cluster de toothis do pacote de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="6b9fe-132">Next [deploy](service-fabric-deploy-remove-applications.md) hello edited application package toothis cluster.</span></span>

<span data-ttu-id="6b9fe-133">Agora você deve ter um aplicativo do Service Fabric em contêineres executando seu cluster.</span><span class="sxs-lookup"><span data-stu-id="6b9fe-133">You should now have a containerized Service Fabric application running your cluster.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6b9fe-134">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="6b9fe-134">Next steps</span></span>
* <span data-ttu-id="6b9fe-135">Saiba mais sobre como executar [contêineres no Service Fabric](service-fabric-get-started-containers.md).</span><span class="sxs-lookup"><span data-stu-id="6b9fe-135">Learn more about running [containers on Service Fabric](service-fabric-get-started-containers.md).</span></span>
* <span data-ttu-id="6b9fe-136">Saiba mais sobre Olá Service Fabric [ciclo de vida do aplicativo](service-fabric-application-lifecycle.md).</span><span class="sxs-lookup"><span data-stu-id="6b9fe-136">Learn about hello Service Fabric [application life-cycle](service-fabric-application-lifecycle.md).</span></span>
