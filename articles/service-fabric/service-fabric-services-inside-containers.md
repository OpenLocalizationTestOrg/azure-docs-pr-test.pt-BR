---
title: "Como colocar em contêineres os microsserviços do Azure Service Fabric (versão prévia)"
description: "O Azure Service Fabric adicionou novas funcionalidades para colocar em contêineres seus microsserviços do Service Fabric. Esse recurso está atualmente na visualização."
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
ms.openlocfilehash: 6f8ad0bad8d1ae861e6b72f7e1a32ab0675813c2
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-containerize-your-service-fabric-reliable-services-and-reliable-actors-preview"></a><span data-ttu-id="97634-104">Como colocar em contêineres seus Reliable Services e Reliable Actors do Service Fabric (versão prévia)</span><span class="sxs-lookup"><span data-stu-id="97634-104">How to containerize your Service Fabric Reliable Services and Reliable Actors (Preview)</span></span>

<span data-ttu-id="97634-105">O Service Fabric oferece suporte a colocação em contêineres de microsserviços do Service Fabric (serviços baseados em Reliable Services e Reliable Actors).</span><span class="sxs-lookup"><span data-stu-id="97634-105">Service Fabric supports containerizing Service Fabric microservices (Reliable Services, and Reliable Actor based services).</span></span> <span data-ttu-id="97634-106">Para saber mais, confira [contêineres do Service Fabric](service-fabric-containers-overview.md).</span><span class="sxs-lookup"><span data-stu-id="97634-106">For more information, see [service fabric containers](service-fabric-containers-overview.md).</span></span>


 <span data-ttu-id="97634-107">Este recurso está em versão prévia, e este artigo fornece as várias etapas para executar seu serviço dentro de um contêiner.</span><span class="sxs-lookup"><span data-stu-id="97634-107">This feature is in preview and this article provides the various steps to get your service running inside a container.</span></span>  

> [!NOTE]
> <span data-ttu-id="97634-108">Esse recurso está na versão prévia e não tem suporte.</span><span class="sxs-lookup"><span data-stu-id="97634-108">This feature is in preview and is not supported in production.</span></span> <span data-ttu-id="97634-109">Atualmente, esse recurso só funciona para Windows.</span><span class="sxs-lookup"><span data-stu-id="97634-109">Currently this feature only works for Windows.</span></span>

## <a name="steps-to-containerize-your-service-fabric-application"></a><span data-ttu-id="97634-110">Etapas para colocar seu aplicativo do Service Fabric em contêineres</span><span class="sxs-lookup"><span data-stu-id="97634-110">Steps to containerize your Service Fabric Application</span></span>

1. <span data-ttu-id="97634-111">Abra seu aplicativo do Service Fabric no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="97634-111">Open your Service Fabric application in Visual Studio.</span></span>

2. <span data-ttu-id="97634-112">Adicione a classe [SFBinaryLoader.cs](https://github.com/Azure/service-fabric-scripts-and-templates/blob/master/code/SFBinaryLoaderForContainers/SFBinaryLoader.cs) ao seu projeto.</span><span class="sxs-lookup"><span data-stu-id="97634-112">Add class [SFBinaryLoader.cs](https://github.com/Azure/service-fabric-scripts-and-templates/blob/master/code/SFBinaryLoaderForContainers/SFBinaryLoader.cs) to your project.</span></span> <span data-ttu-id="97634-113">O código nessa classe é um auxiliar para carregar corretamente os binários de tempo de execução do Service Fabric dentro de seu aplicativo durante a execução dentro de um contêiner.</span><span class="sxs-lookup"><span data-stu-id="97634-113">The code in this class is a helper to correctly load the Service Fabric runtime binaries inside your application when running inside a container.</span></span>

3. <span data-ttu-id="97634-114">Para cada pacote de código que você quer colocar em contêineres, inicialize o carregador no ponto de entrada do programa.</span><span class="sxs-lookup"><span data-stu-id="97634-114">For each code package you would like to containerize, initialize the loader at the program entry point.</span></span> <span data-ttu-id="97634-115">Adicione o construtor estático mostrado no trecho de código a seguir ao seu arquivo de ponto de entrada do programa.</span><span class="sxs-lookup"><span data-stu-id="97634-115">Add the static constructor shown in the following code snippet to your program entry point file.</span></span>

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
          /// This is the entry point of the service host process.
          /// </summary>
          private static void Main()
          {
  ```

4. <span data-ttu-id="97634-116">Compilar e [empacotar](service-fabric-package-apps.md#Package-App) seu projeto.</span><span class="sxs-lookup"><span data-stu-id="97634-116">Build and [package](service-fabric-package-apps.md#Package-App) your project.</span></span> <span data-ttu-id="97634-117">Para compilar e criar um pacote, clique com o botão direito do mouse no projeto de aplicativo no Gerenciador de Soluções e escolha o comando **Empacotar**.</span><span class="sxs-lookup"><span data-stu-id="97634-117">To build and create a package, right-click the application project in Solution Explorer and choose the **Package** command.</span></span>

5. <span data-ttu-id="97634-118">Para cada pacote de códigos que você precisa colocar em contêineres, execute o script do PowerShell [CreateDockerPackage.ps1](https://github.com/Azure/service-fabric-scripts-and-templates/blob/master/scripts/CodePackageToDockerPackage/CreateDockerPackage.ps1).</span><span class="sxs-lookup"><span data-stu-id="97634-118">For every code package you need to containerize, run the PowerShell script [CreateDockerPackage.ps1](https://github.com/Azure/service-fabric-scripts-and-templates/blob/master/scripts/CodePackageToDockerPackage/CreateDockerPackage.ps1).</span></span> <span data-ttu-id="97634-119">A utilização é o seguinte:</span><span class="sxs-lookup"><span data-stu-id="97634-119">The usage is as follows:</span></span>
  ```powershell
    $codePackagePath = 'Path to the code package to containerize.'
    $dockerPackageOutputDirectoryPath = 'Output path for the generated docker folder.'
    $applicationExeName = 'Name of the ode package executable.'
    CreateDockerPackage.ps1 -CodePackageDirectoryPath $codePackagePath -DockerPackageOutputDirectoryPath $dockerPackageOutputDirectoryPath -ApplicationExeName $applicationExeName
 ```
  <span data-ttu-id="97634-120">O script cria uma pasta com artefatos do Docker em $dockerPackageOutputDirectoryPath.</span><span class="sxs-lookup"><span data-stu-id="97634-120">The script creates a folder with Docker artifacts at $dockerPackageOutputDirectoryPath.</span></span> <span data-ttu-id="97634-121">Modifique o Dockerfile gerado para expor as portas, executar scripts de configuração etc. com base em suas necessidades.</span><span class="sxs-lookup"><span data-stu-id="97634-121">Modify the generated Dockerfile to expose any ports, run setup scripts etc. based on your needs.</span></span>

6. <span data-ttu-id="97634-122">Em seguida você precisa [compilar](service-fabric-get-started-containers.md#Build-Containers) e [enviar por push](service-fabric-get-started-containers.md#Push-Containers) seu pacote de contêineres do Docker ao seu repositório.</span><span class="sxs-lookup"><span data-stu-id="97634-122">Next you need to [build](service-fabric-get-started-containers.md#Build-Containers) and [push](service-fabric-get-started-containers.md#Push-Containers) your Docker container package to your repository.</span></span>

7. <span data-ttu-id="97634-123">Modifique o ApplicationManifest.xml e ServiceManifest.xml a fim de adicionar a imagem de contêiner, informações do repositório, autenticação do registro e mapeamento de porta ao host.</span><span class="sxs-lookup"><span data-stu-id="97634-123">Modify the ApplicationManifest.xml and ServiceManifest.xml to add your container image, repository information, registry authentication, and port-to-host mapping.</span></span> <span data-ttu-id="97634-124">Para modificar os manifestos, confira [Criar um aplicativo de contêiner do Azure Service Fabric](service-fabric-get-started-containers.md).</span><span class="sxs-lookup"><span data-stu-id="97634-124">For modifying the manifests, see [Create an Azure Service Fabric container application](service-fabric-get-started-containers.md).</span></span> <span data-ttu-id="97634-125">A definição de pacote de códigos no manifesto do serviço precisa ser substituída pela imagem de contêiner correspondente.</span><span class="sxs-lookup"><span data-stu-id="97634-125">The code package definition in the service manifest needs to be replaced with corresponding container image.</span></span> <span data-ttu-id="97634-126">Altere o Ponto de Entrada para um tipo de ContainerHost.</span><span class="sxs-lookup"><span data-stu-id="97634-126">Make sure to change the EntryPoint to a ContainerHost type.</span></span>

  ```xml
<!-- Code package is your service executable. -->
<CodePackage Name="Code" Version="1.0.0">
  <EntryPoint>
    <!-- Follow this link for more information about deploying Windows containers to Service Fabric: https://aka.ms/sfguestcontainers -->
    <ContainerHost>
      <ImageName>myregistry.azurecr.io/samples/helloworldapp</ImageName>
    </ContainerHost>
  </EntryPoint>
  <!-- Pass environment variables to your container: -->    
</CodePackage>
  ```

8. <span data-ttu-id="97634-127">Adicione o mapeamento de porta ao host para seu replicador e ponto de extremidade de serviço.</span><span class="sxs-lookup"><span data-stu-id="97634-127">Add the port-to-host mapping for your replicator and service endpoint.</span></span> <span data-ttu-id="97634-128">Como essas duas portas são atribuídas em tempo de execução pelo Service Fabric, o ContainerPort é definido como zero para usar a porta atribuída para mapeamento.</span><span class="sxs-lookup"><span data-stu-id="97634-128">Since both these ports are assigned at runtime by Service Fabric, the ContainerPort is set to zero to use the assigned port for mapping.</span></span>

 ```xml
<Policies>
  <ContainerHostPolicies CodePackageRef="Code">
    <PortBinding ContainerPort="0" EndpointRef="ServiceEndpoint"/>
    <PortBinding ContainerPort="0" EndpointRef="ReplicatorEndpoint"/>
  </ContainerHostPolicies>
</Policies>
 ```

9. <span data-ttu-id="97634-129">Para testar esse aplicativo, você precisa implantá-lo em um cluster que esteja executando a versão 5.7 ou superior.</span><span class="sxs-lookup"><span data-stu-id="97634-129">To test this application, you need to deploy it to a cluster that is running version 5.7 or higher.</span></span> <span data-ttu-id="97634-130">Além disso, você precisa editar e atualizar as configurações de cluster para habilitar esse recurso de visualização.</span><span class="sxs-lookup"><span data-stu-id="97634-130">In addition, you need to edit and update the cluster settings to enable this preview feature.</span></span> <span data-ttu-id="97634-131">Execute as etapas neste [artigo](service-fabric-cluster-fabric-settings.md) para adicionar a configuração mostrada a seguir.</span><span class="sxs-lookup"><span data-stu-id="97634-131">Follow the steps in this [article](service-fabric-cluster-fabric-settings.md) to add the setting shown next.</span></span>
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
10. <span data-ttu-id="97634-132">Depois, [implante](service-fabric-deploy-remove-applications.md) o pacote de aplicativos editado nesse cluster.</span><span class="sxs-lookup"><span data-stu-id="97634-132">Next [deploy](service-fabric-deploy-remove-applications.md) the edited application package to this cluster.</span></span>

<span data-ttu-id="97634-133">Agora você deve ter um aplicativo do Service Fabric em contêineres executando seu cluster.</span><span class="sxs-lookup"><span data-stu-id="97634-133">You should now have a containerized Service Fabric application running your cluster.</span></span>

## <a name="next-steps"></a><span data-ttu-id="97634-134">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="97634-134">Next steps</span></span>
* <span data-ttu-id="97634-135">Saiba mais sobre como executar [contêineres no Service Fabric](service-fabric-get-started-containers.md).</span><span class="sxs-lookup"><span data-stu-id="97634-135">Learn more about running [containers on Service Fabric](service-fabric-get-started-containers.md).</span></span>
* <span data-ttu-id="97634-136">Leia mais sobre o [ciclo de vida do aplicativo](service-fabric-application-lifecycle.md) do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="97634-136">Learn about the Service Fabric [application life-cycle](service-fabric-application-lifecycle.md).</span></span>
