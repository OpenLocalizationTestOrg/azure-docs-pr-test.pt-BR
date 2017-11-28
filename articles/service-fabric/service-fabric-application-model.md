---
title: Modelo de aplicativo do Azure Service Fabric | Microsoft Docs
description: "Como modelar e descrever aplicativos e serviços no Service Fabric."
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
ms.date: 8/9/2017
ms.author: ryanwi
ms.openlocfilehash: e30482427b88eb3e58d39075c7f0734664b79aa2
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="model-an-application-in-service-fabric"></a><span data-ttu-id="48597-103">Modelar um aplicativo no Malha do Serviço</span><span class="sxs-lookup"><span data-stu-id="48597-103">Model an application in Service Fabric</span></span>
<span data-ttu-id="48597-104">Este artigo fornece uma visão geral do modelo de aplicativo do Azure Service Fabric e descreve como definir um aplicativo e um serviço por meio de arquivos de manifesto.</span><span class="sxs-lookup"><span data-stu-id="48597-104">This article provides an overview of the Azure Service Fabric application model and how to define an application and service via manifest files.</span></span>

## <a name="understand-the-application-model"></a><span data-ttu-id="48597-105">Entenda o modelo de aplicativo</span><span class="sxs-lookup"><span data-stu-id="48597-105">Understand the application model</span></span>
<span data-ttu-id="48597-106">Um aplicativo é uma coleção de serviços membros que executam determinadas funções.</span><span class="sxs-lookup"><span data-stu-id="48597-106">An application is a collection of constituent services that perform a certain function or functions.</span></span> <span data-ttu-id="48597-107">Um serviço executa uma função completa e autônoma e pode iniciar e executar independentemente de outros serviços.</span><span class="sxs-lookup"><span data-stu-id="48597-107">A service performs a complete and standalone function and can start and run independently of other services.</span></span>  <span data-ttu-id="48597-108">Um serviço é composto de código, configuração e dados.</span><span class="sxs-lookup"><span data-stu-id="48597-108">A service is composed of code, configuration, and data.</span></span> <span data-ttu-id="48597-109">Para cada serviço, o código consiste em binários executáveis, a configuração consiste em configurações do serviço que podem ser carregadas no tempo de execução e os dados consistem em dados estáticos arbitrários a serem consumidos pelo serviço.</span><span class="sxs-lookup"><span data-stu-id="48597-109">For each service, code consists of the executable binaries, configuration consists of service settings that can be loaded at run time, and data consists of arbitrary static data to be consumed by the service.</span></span> <span data-ttu-id="48597-110">Cada componente nesse modelo hierárquico de aplicativo pode ser atualizado e transformado em outra versão independentemente.</span><span class="sxs-lookup"><span data-stu-id="48597-110">Each component in this hierarchical application model can be versioned and upgraded independently.</span></span>

![O modelo de aplicativo Service Fabric][appmodel-diagram]

<span data-ttu-id="48597-112">Um tipo de aplicativo é uma categorização de um aplicativo e consiste em um pacote de tipos de serviço.</span><span class="sxs-lookup"><span data-stu-id="48597-112">An application type is a categorization of an application and consists of a bundle of service types.</span></span> <span data-ttu-id="48597-113">Um tipo de serviço é uma categorização de um serviço.</span><span class="sxs-lookup"><span data-stu-id="48597-113">A service type is a categorization of a service.</span></span> <span data-ttu-id="48597-114">A categorização pode ter diferentes definições e configurações, mas a funcionalidade núcleo permanece a mesma.</span><span class="sxs-lookup"><span data-stu-id="48597-114">The categorization can have different settings and configurations, but the core functionality remains the same.</span></span> <span data-ttu-id="48597-115">As instâncias de um serviço são as diferentes variações de configuração de serviço de um mesmo tipo de serviço.</span><span class="sxs-lookup"><span data-stu-id="48597-115">The instances of a service are the different service configuration variations of the same service type.</span></span>  

<span data-ttu-id="48597-116">Classes (ou "tipos") de aplicativos e serviços são descritas por meio de arquivos XML (manifestos de aplicativo e manifestos do serviço).</span><span class="sxs-lookup"><span data-stu-id="48597-116">Classes (or "types") of applications and services are described through XML files (application manifests and service manifests).</span></span>  <span data-ttu-id="48597-117">Os manifestos são os modelos de aplicativos que poderão ser instanciados do repositório de imagens do cluster.</span><span class="sxs-lookup"><span data-stu-id="48597-117">The manifests are the templates against which applications can be instantiated from the cluster's image store.</span></span> <span data-ttu-id="48597-118">A definição de esquema dos arquivos ServiceManifest.xml e ApplicationManifest.xml é instalada com o SDK e as ferramentas do Service Fabric em *C:\Arquivos de Programas\Microsoft SDKs\Service Fabric\schemas\ServiceFabricServiceModel.xsd*.</span><span class="sxs-lookup"><span data-stu-id="48597-118">The schema definition for the ServiceManifest.xml and ApplicationManifest.xml file is installed with the Service Fabric SDK and tools to *C:\Program Files\Microsoft SDKs\Service Fabric\schemas\ServiceFabricServiceModel.xsd*.</span></span>

<span data-ttu-id="48597-119">O código para instâncias do aplicativo diferentes será executado como processos separados, mesmo quando hospedadas pelo mesmo nó do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="48597-119">The code for different application instances run as separate processes even when hosted by the same Service Fabric node.</span></span> <span data-ttu-id="48597-120">Além disso, o ciclo de vida de cada instância do aplicativo pode ser gerenciado (por exemplo, atualizado) independentemente.</span><span class="sxs-lookup"><span data-stu-id="48597-120">Furthermore, the lifecycle of each application instance can be managed (for example, upgraded) independently.</span></span> <span data-ttu-id="48597-121">O diagrama a seguir mostra como os tipos de aplicativo são compostos de tipos de serviço, que, por sua vez, são compostos de código, configuração e pacotes de dados.</span><span class="sxs-lookup"><span data-stu-id="48597-121">The following diagram shows how application types are composed of service types, which in turn are composed of code, configuration, and data packages.</span></span> <span data-ttu-id="48597-122">Para simplificar o diagrama, somente os pacotes de código/configuração/dados de `ServiceType4` são mostrados, embora cada tipo de serviço inclua alguns ou todos os tipos de pacote.</span><span class="sxs-lookup"><span data-stu-id="48597-122">To simplify the diagram, only the code/config/data packages for `ServiceType4` are shown, though each service type would include some or all those package types.</span></span>

![Tipos de aplicativos do Service Fabric e tipos de serviço][cluster-imagestore-apptypes]

<span data-ttu-id="48597-124">Dois arquivos de manifesto diferentes são usados para descrever aplicativos e serviços: o manifesto do serviço e o manifesto do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="48597-124">Two different manifest files are used to describe applications and services: the service manifest and application manifest.</span></span> <span data-ttu-id="48597-125">Manifestos são abordados detalhadamente nas seções a seguir.</span><span class="sxs-lookup"><span data-stu-id="48597-125">Manifests are covered in detail in the following sections.</span></span>

<span data-ttu-id="48597-126">Pode haver uma ou mais instâncias de um tipo de serviço ativo no cluster.</span><span class="sxs-lookup"><span data-stu-id="48597-126">There can be one or more instances of a service type active in the cluster.</span></span> <span data-ttu-id="48597-127">Por exemplo, instâncias de serviço com estado, ou réplicas, alcançam alta confiabilidade replicando o estado entre as réplicas localizadas em diferentes nós do cluster.</span><span class="sxs-lookup"><span data-stu-id="48597-127">For example, stateful service instances, or replicas, achieve high reliability by replicating state between replicas located on different nodes in the cluster.</span></span> <span data-ttu-id="48597-128">Essencialmente a replicação fornece redundância para que o serviço esteja disponível mesmo se um nó em um cluster falhar.</span><span class="sxs-lookup"><span data-stu-id="48597-128">Replication essentially provides redundancy for the service to be available even if one node in a cluster fails.</span></span> <span data-ttu-id="48597-129">Um [serviço particionado](service-fabric-concepts-partitioning.md) divide ainda mais seu estado (e padrões de acesso a esse estado) pelos nós do cluster.</span><span class="sxs-lookup"><span data-stu-id="48597-129">A [partitioned service](service-fabric-concepts-partitioning.md) further divides its state (and access patterns to that state) across nodes in the cluster.</span></span>

<span data-ttu-id="48597-130">O diagrama a seguir mostra a relação entre aplicativos e instâncias de serviço, partições e réplicas.</span><span class="sxs-lookup"><span data-stu-id="48597-130">The following diagram shows the relationship between applications and service instances, partitions, and replicas.</span></span>

![Partições e réplicas dentro de um serviço][cluster-application-instances]

> [!TIP]
> <span data-ttu-id="48597-132">É possível exibir o layout de aplicativos em um cluster usando a ferramenta Service Fabric Explorer disponível em http://&lt;yourclusteraddress&gt;:19080/Explorer.</span><span class="sxs-lookup"><span data-stu-id="48597-132">You can view the layout of applications in a cluster using the Service Fabric Explorer tool available at http://&lt;yourclusteraddress&gt;:19080/Explorer.</span></span> <span data-ttu-id="48597-133">Para obter mais informações, consulte [Visualizando o cluster com o Service Fabric Explorer](service-fabric-visualizing-your-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="48597-133">For more information, see [Visualizing your cluster with Service Fabric Explorer](service-fabric-visualizing-your-cluster.md).</span></span>
> 
> 

## <a name="describe-a-service"></a><span data-ttu-id="48597-134">Descrever um serviço</span><span class="sxs-lookup"><span data-stu-id="48597-134">Describe a service</span></span>
<span data-ttu-id="48597-135">O manifesto do serviço declarativamente define o tipo de serviço e a versão.</span><span class="sxs-lookup"><span data-stu-id="48597-135">The service manifest declaratively defines the service type and version.</span></span> <span data-ttu-id="48597-136">Ele especifica os metadados de serviço, como o tipo de serviço, propriedades de integridade, métricas de balanceamento de carga, binários de serviço e arquivos de configuração.</span><span class="sxs-lookup"><span data-stu-id="48597-136">It specifies service metadata such as service type, health properties, load-balancing metrics, service binaries, and configuration files.</span></span>  <span data-ttu-id="48597-137">Trocando em miúdos, ele descreve os pacotes de código, de configuração e de dados que compõem um pacote de serviço para dar suporte a um ou mais tipos de serviço.</span><span class="sxs-lookup"><span data-stu-id="48597-137">Put another way, it describes the code, configuration, and data packages that compose a service package to support one or more service types.</span></span> <span data-ttu-id="48597-138">Aqui está um manifesto do serviço de exemplo simples:</span><span class="sxs-lookup"><span data-stu-id="48597-138">Here is a simple example service manifest:</span></span>

```xml
<?xml version="1.0" encoding="utf-8" ?>
<ServiceManifest Name="MyServiceManifest" Version="SvcManifestVersion1" xmlns="http://schemas.microsoft.com/2011/01/fabric" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
  <Description>An example service manifest</Description>
  <ServiceTypes>
    <StatelessServiceType ServiceTypeName="MyServiceType" />
  </ServiceTypes>
  <CodePackage Name="MyCode" Version="CodeVersion1">
    <SetupEntryPoint>
      <ExeHost>
        <Program>MySetup.bat</Program>
      </ExeHost>
    </SetupEntryPoint>
    <EntryPoint>
      <ExeHost>
        <Program>MyServiceHost.exe</Program>
      </ExeHost>
    </EntryPoint>
    <EnvironmentVariables>
      <EnvironmentVariable Name="MyEnvVariable" Value=""/>
      <EnvironmentVariable Name="HttpGatewayPort" Value="19080"/>
    </EnvironmentVariables>
  </CodePackage>
  <ConfigPackage Name="MyConfig" Version="ConfigVersion1" />
  <DataPackage Name="MyData" Version="DataVersion1" />
</ServiceManifest>
```

<span data-ttu-id="48597-139">**Version** são cadeias de caracteres não estruturadas e não analisadas pelo sistema.</span><span class="sxs-lookup"><span data-stu-id="48597-139">**Version** attributes are unstructured strings and not parsed by the system.</span></span> <span data-ttu-id="48597-140">Atributos de versão são usados para a versão de cada componente para atualizações.</span><span class="sxs-lookup"><span data-stu-id="48597-140">Version attributes are used to version each component for upgrades.</span></span>

<span data-ttu-id="48597-141">**ServiceTypes** declara para quais tipos de serviço há suporte pelos **CodePackages** neste manifesto.</span><span class="sxs-lookup"><span data-stu-id="48597-141">**ServiceTypes** declares what service types are supported by **CodePackages** in this manifest.</span></span> <span data-ttu-id="48597-142">Quando um serviço é instanciado em relação a um desses tipos de serviço, todos os pacotes de código declarados nesse manifesto são ativados com a execução de seus pontos de entrada.</span><span class="sxs-lookup"><span data-stu-id="48597-142">When a service is instantiated against one of these service types, all code packages declared in this manifest are activated by running their entry points.</span></span> <span data-ttu-id="48597-143">Os processos resultantes devem registrar os tipos de serviço com suporte no tempo de execução.</span><span class="sxs-lookup"><span data-stu-id="48597-143">The resulting processes are expected to register the supported service types at run time.</span></span> <span data-ttu-id="48597-144">Os tipos de serviço são declarados no nível do manifesto e não no nível do pacote de código.</span><span class="sxs-lookup"><span data-stu-id="48597-144">Service types are declared at the manifest level and not the code package level.</span></span> <span data-ttu-id="48597-145">Assim, quando há vários pacotes de código, eles são todos ativados sempre que o sistema procurar por qualquer um dos tipos de serviço declarados.</span><span class="sxs-lookup"><span data-stu-id="48597-145">So when there are multiple code packages, they are all activated whenever the system looks for any one of the declared service types.</span></span>

<span data-ttu-id="48597-146">**SetupEntryPoint** é um ponto de entrada privilegiado que é executado com as mesmas credenciais da Malha do Serviço (normalmente, a conta *LocalSystem* ) antes de qualquer outro ponto de entrada.</span><span class="sxs-lookup"><span data-stu-id="48597-146">**SetupEntryPoint** is a privileged entry point that runs with the same credentials as Service Fabric (typically the *LocalSystem* account) before any other entry point.</span></span> <span data-ttu-id="48597-147">O executável especificado pelo **EntryPoint** normalmente é o host de serviço de longa duração.</span><span class="sxs-lookup"><span data-stu-id="48597-147">The executable specified by **EntryPoint** is typically the long-running service host.</span></span> <span data-ttu-id="48597-148">A presença de um ponto de entrada de instalação separado evita a necessidade de executar o host de serviço com altos privilégios por longos períodos de tempo.</span><span class="sxs-lookup"><span data-stu-id="48597-148">The presence of a separate setup entry point avoids having to run the service host with high privileges for extended periods of time.</span></span> <span data-ttu-id="48597-149">O executável especificado pelo **EntryPoint** é executado depois que o **SetupEntryPoint** é encerrado com êxito.</span><span class="sxs-lookup"><span data-stu-id="48597-149">The executable specified by **EntryPoint** is run after **SetupEntryPoint** exits successfully.</span></span> <span data-ttu-id="48597-150">Se o processo terminar ou falhar, o processo resultante é monitorado e reiniciado (começando novamente com **SetupEntryPoint**) .</span><span class="sxs-lookup"><span data-stu-id="48597-150">If the process ever terminates or crashes, the resulting process is monitored and restarted (beginning again with **SetupEntryPoint**).</span></span>  

<span data-ttu-id="48597-151">Cenários típicos de uso do **SetupEntryPoint** quando você executa um executável antes do início do serviço ou você executa uma operação com privilégios elevados.</span><span class="sxs-lookup"><span data-stu-id="48597-151">Typical scenarios for using **SetupEntryPoint** are when you run an executable before the service starts or you perform an operation with elevated privileges.</span></span> <span data-ttu-id="48597-152">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="48597-152">For example:</span></span>

* <span data-ttu-id="48597-153">Configurar e inicializar as variáveis de ambiente que o serviço executável precisa.</span><span class="sxs-lookup"><span data-stu-id="48597-153">Setting up and initializing environment variables that the service executable needs.</span></span> <span data-ttu-id="48597-154">Isso não é limitado a apenas executáveis gravados usando os modelos de programação do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="48597-154">This is not limited to only executables written via the Service Fabric programming models.</span></span> <span data-ttu-id="48597-155">Por exemplo, npm.exe precisa de algumas variáveis de ambiente configurados para implantar um aplicativo node.js.</span><span class="sxs-lookup"><span data-stu-id="48597-155">For example, npm.exe needs some environment variables configured for deploying a node.js application.</span></span>
* <span data-ttu-id="48597-156">Configurando o controle de acesso, instalando certificados de segurança.</span><span class="sxs-lookup"><span data-stu-id="48597-156">Setting up access control by installing security certificates.</span></span>

<span data-ttu-id="48597-157">Para obter mais detalhes sobre como configurar o **SetupEntryPoint**, confira [Configurar a política para um ponto de entrada de instalação do serviço](service-fabric-application-runas-security.md)</span><span class="sxs-lookup"><span data-stu-id="48597-157">For more details on how to configure the **SetupEntryPoint** see [Configure the policy for a service setup entry point](service-fabric-application-runas-security.md)</span></span>

<span data-ttu-id="48597-158">**EnvironmentVariables** fornece uma lista de variáveis de ambiente que são definidas para este pacote de códigos.</span><span class="sxs-lookup"><span data-stu-id="48597-158">**EnvironmentVariables** provides a list of environment variables that are set for this code package.</span></span> <span data-ttu-id="48597-159">As variáveis do ambiente podem ser substituídas no `ApplicationManifest.xml` para fornecer valores diferentes para instâncias de serviço diferentes.</span><span class="sxs-lookup"><span data-stu-id="48597-159">Environmentment variables can be overridden in the `ApplicationManifest.xml` to provide different values for different service instances.</span></span> 

<span data-ttu-id="48597-160">**DataPackage** declara uma pasta nomeada pelo atributo **Name**, que contém dados estáticos arbitrários a serem consumidos pelo processo no tempo de execução.</span><span class="sxs-lookup"><span data-stu-id="48597-160">**DataPackage** declares a folder, named by the **Name** attribute, that contains arbitrary static data to be consumed by the process at run time.</span></span>

<span data-ttu-id="48597-161">**ConfigPackage** declara uma pasta nomeada pelo atributo **Name**, que contém um arquivo *Settings.xml*.</span><span class="sxs-lookup"><span data-stu-id="48597-161">**ConfigPackage** declares a folder, named by the **Name** attribute, that contains a *Settings.xml* file.</span></span> <span data-ttu-id="48597-162">Esse arquivo de configurações contém seções de configurações de par chave-valor, definido pelo usuário, que o processo lê de volta no tempo de execução.</span><span class="sxs-lookup"><span data-stu-id="48597-162">The settings file contains sections of user-defined, key-value pair settings that the process reads back at run time.</span></span> <span data-ttu-id="48597-163">Durante a atualização, se apenas a **versão** do **ConfigPackage** tiver sido alterada, o processo de execução não será reiniciado.</span><span class="sxs-lookup"><span data-stu-id="48597-163">During an upgrade, if only the **ConfigPackage** **version** has changed, then the running process is not restarted.</span></span> <span data-ttu-id="48597-164">Em vez disso, um retorno de chamada notifica o processo de que as definições de configuração foram alteradas para que possam ser recarregadas dinamicamente.</span><span class="sxs-lookup"><span data-stu-id="48597-164">Instead, a callback notifies the process that configuration settings have changed so they can be reloaded dynamically.</span></span> <span data-ttu-id="48597-165">Aqui está um exemplo do arquivo *Settings.xml* :</span><span class="sxs-lookup"><span data-stu-id="48597-165">Here is an example *Settings.xml* file:</span></span>

```xml
<Settings xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/2011/01/fabric">
  <Section Name="MyConfigurationSection">
    <Parameter Name="MySettingA" Value="Example1" />
    <Parameter Name="MySettingB" Value="Example2" />
  </Section>
</Settings>
```

> [!NOTE]
> <span data-ttu-id="48597-166">Um manifesto do serviço pode conter vários pacotes de código, de configuração e de dados.</span><span class="sxs-lookup"><span data-stu-id="48597-166">A service manifest can contain multiple code, configuration, and data packages.</span></span> <span data-ttu-id="48597-167">Cada um deles pode ser transformado em versão independentemente.</span><span class="sxs-lookup"><span data-stu-id="48597-167">Each of those can be versioned independently.</span></span>
> 
> 

<!--
For more information about other features supported by service manifests, refer to the following articles:

*TODO: LoadMetrics, PlacementConstraints, ServicePlacementPolicies
*TODO: Resources
*TODO: Health properties
*TODO: Trace filters
*TODO: Configuration overrides
-->

## <a name="describe-an-application"></a><span data-ttu-id="48597-168">Descrever um aplicativo</span><span class="sxs-lookup"><span data-stu-id="48597-168">Describe an application</span></span>
<span data-ttu-id="48597-169">O manifesto do aplicativo declarativamente descreve o tipo de aplicativo e a versão.</span><span class="sxs-lookup"><span data-stu-id="48597-169">The application manifest declaratively describes the application type and version.</span></span> <span data-ttu-id="48597-170">Ele especifica os metadados de composição de serviço, como nomes estáveis, esquema de particionamento, fator de replicação/contagem de instância, política de segurança/isolamento, restrições de posicionamento, substituições de configuração e tipos de serviço membro.</span><span class="sxs-lookup"><span data-stu-id="48597-170">It specifies service composition metadata such as stable names, partitioning scheme, instance count/replication factor, security/isolation policy, placement constraints, configuration overrides, and constituent service types.</span></span> <span data-ttu-id="48597-171">Também são descritos os domínios de balanceamento de carga no qual o aplicativo é colocado.</span><span class="sxs-lookup"><span data-stu-id="48597-171">The load-balancing domains into which the application is placed are also described.</span></span>

<span data-ttu-id="48597-172">Portanto, um manifesto de aplicativo descreve os elementos no nível do aplicativo e faz referência a um ou mais manifestos do serviço para compor um tipo de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="48597-172">Thus, an application manifest describes elements at the application level and references one or more service manifests to compose an application type.</span></span> <span data-ttu-id="48597-173">Aqui está um manifesto de aplicativo de exemplo simples:</span><span class="sxs-lookup"><span data-stu-id="48597-173">Here is a simple example application manifest:</span></span>

```xml
<?xml version="1.0" encoding="utf-8" ?>
<ApplicationManifest
      ApplicationTypeName="MyApplicationType"
      ApplicationTypeVersion="AppManifestVersion1"
      xmlns="http://schemas.microsoft.com/2011/01/fabric"
      xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
  <Description>An example application manifest</Description>
  <ServiceManifestImport>
    <ServiceManifestRef ServiceManifestName="MyServiceManifest" ServiceManifestVersion="SvcManifestVersion1"/>
    <ConfigOverrides/>
    <EnvironmentOverrides CodePackageRef="MyCode"/>
  </ServiceManifestImport>
  <DefaultServices>
     <Service Name="MyService">
         <StatelessService ServiceTypeName="MyServiceType" InstanceCount="1">
             <SingletonPartition/>
         </StatelessService>
     </Service>
  </DefaultServices>
</ApplicationManifest>
```

<span data-ttu-id="48597-174">Manifestos de serviço, como atributos **Versão** , são cadeias de caracteres não estruturadas e não analisadas pelo sistema.</span><span class="sxs-lookup"><span data-stu-id="48597-174">Like service manifests, **Version** attributes are unstructured strings and are not parsed by the system.</span></span> <span data-ttu-id="48597-175">Atributos de versão também são usados para a versão de cada componente para atualizações.</span><span class="sxs-lookup"><span data-stu-id="48597-175">Version attributes are also used to version each component for upgrades.</span></span>

<span data-ttu-id="48597-176">**ServiceManifestImport** contém referências a manifestos de serviço que compõem esse tipo de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="48597-176">**ServiceManifestImport** contains references to service manifests that compose this application type.</span></span> <span data-ttu-id="48597-177">Os manifestos de serviço importados determinam quais tipos de serviço são válidos nesse tipo de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="48597-177">Imported service manifests determine what service types are valid within this application type.</span></span> <span data-ttu-id="48597-178">Dentro de ServiceManifestImport, você substitui os valores de configuração em Settings.xml e nas variáveis de ambiente dos arquivos ServiceManifest.xml.</span><span class="sxs-lookup"><span data-stu-id="48597-178">Within the ServiceManifestImport, you override configuration values in Settings.xml and environment variables in ServiceManifest.xml files.</span></span> 


<span data-ttu-id="48597-179">**DefaultServices** declara as instâncias de serviço que são criadas automaticamente sempre que um aplicativo é instanciado em relação a esse tipo de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="48597-179">**DefaultServices** declares service instances that are automatically created whenever an application is instantiated against this application type.</span></span> <span data-ttu-id="48597-180">Serviços padrão são apenas uma conveniência e se comportam como serviços normais em todos os aspectos após terem sido criados.</span><span class="sxs-lookup"><span data-stu-id="48597-180">Default services are just a convenience and behave like normal services in every respect after they have been created.</span></span> <span data-ttu-id="48597-181">Eles são atualizados com qualquer outro serviço na instância do aplicativo e também podem ser removidos.</span><span class="sxs-lookup"><span data-stu-id="48597-181">They are upgraded along with any other services in the application instance and can be removed as well.</span></span>

> [!NOTE]
> <span data-ttu-id="48597-182">Um manifesto de aplicativo pode conter várias importações de manifesto do serviço e serviços padrão.</span><span class="sxs-lookup"><span data-stu-id="48597-182">An application manifest can contain multiple service manifest imports and default services.</span></span> <span data-ttu-id="48597-183">Cada importação de manifesto do serviço pode ser transformada em versão independentemente.</span><span class="sxs-lookup"><span data-stu-id="48597-183">Each service manifest import can be versioned independently.</span></span>
> 
> 

<span data-ttu-id="48597-184">Para saber como manter aplicativos diferentes e parâmetros de serviço para ambientes individuais, consulte [Gerenciar parâmetros de aplicativo para vários ambientes](service-fabric-manage-multiple-environment-app-configuration.md).</span><span class="sxs-lookup"><span data-stu-id="48597-184">To learn how to maintain different application and service parameters for individual environments, see [Managing application parameters for multiple environments](service-fabric-manage-multiple-environment-app-configuration.md).</span></span>

<!--
For more information about other features supported by application manifests, refer to the following articles:

*TODO: Application parameters
*TODO: Security, Principals, RunAs, SecurityAccessPolicy
*TODO: Service Templates
-->



## <a name="next-steps"></a><span data-ttu-id="48597-185">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="48597-185">Next steps</span></span>
<span data-ttu-id="48597-186">[Empacotar um aplicativo](service-fabric-package-apps.md) e prepará-lo para a implantação.</span><span class="sxs-lookup"><span data-stu-id="48597-186">[Package an application](service-fabric-package-apps.md) and make it ready to deploy.</span></span>

<span data-ttu-id="48597-187">[Implantar e remover aplicativos][10] descreve como usar o PowerShell para gerenciar instâncias do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="48597-187">[Deploy and remove applications][10] describes how to use PowerShell to manage application instances.</span></span>

<span data-ttu-id="48597-188">[Gerenciamento de parâmetros do aplicativo para vários ambientes][11] descreve como configurar os parâmetros e variáveis de ambiente para diferentes instâncias do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="48597-188">[Managing application parameters for multiple environments][11] describes how to configure parameters and environment variables for different application instances.</span></span>

<span data-ttu-id="48597-189">[Configurar políticas de segurança para seu aplicativo][12] descreve como executar serviços sob políticas de segurança para restringir o acesso.</span><span class="sxs-lookup"><span data-stu-id="48597-189">[Configure security policies for your application][12] describes how to run services under security policies to restrict access.</span></span>

<span data-ttu-id="48597-190">Os [modelos de hospedagem de aplicativo][13] descrevem a relação entre réplicas (ou instâncias) de um serviço implantado e o processo de host do serviço.</span><span class="sxs-lookup"><span data-stu-id="48597-190">[Application hosting models][13] describe relationship between replicas (or instances) of a deployed service and service-host process.</span></span>

<!--Image references-->
[appmodel-diagram]: ./media/service-fabric-application-model/application-model.png
[cluster-imagestore-apptypes]: ./media/service-fabric-application-model/cluster-imagestore-apptypes.png
[cluster-application-instances]: media/service-fabric-application-model/cluster-application-instances.png

<!--Link references--In actual articles, you only need a single period before the slash-->
[10]: service-fabric-deploy-remove-applications.md
[11]: service-fabric-manage-multiple-environment-app-configuration.md
[12]: service-fabric-application-runas-security.md
[13]: service-fabric-hosting-model.md
