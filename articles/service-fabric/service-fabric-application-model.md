---
title: modelo de aplicativo do Service Fabric aaaAzure | Microsoft Docs
description: "Como toomodel e descrevem os aplicativos e serviços na malha do serviço."
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
ms.openlocfilehash: 54c4d026e7d556be5f697d4a6f2ee886687e1c35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="model-an-application-in-service-fabric"></a><span data-ttu-id="8b2db-103">Modelar um aplicativo no Malha do Serviço</span><span class="sxs-lookup"><span data-stu-id="8b2db-103">Model an application in Service Fabric</span></span>
<span data-ttu-id="8b2db-104">Este artigo fornece uma visão geral do modelo de aplicativo do Azure Service Fabric hello e como toodefine um aplicativo e serviço por meio de arquivos de manifesto.</span><span class="sxs-lookup"><span data-stu-id="8b2db-104">This article provides an overview of hello Azure Service Fabric application model and how toodefine an application and service via manifest files.</span></span>

## <a name="understand-hello-application-model"></a><span data-ttu-id="8b2db-105">Entender o modelo de aplicativo hello</span><span class="sxs-lookup"><span data-stu-id="8b2db-105">Understand hello application model</span></span>
<span data-ttu-id="8b2db-106">Um aplicativo é uma coleção de serviços membros que executam determinadas funções.</span><span class="sxs-lookup"><span data-stu-id="8b2db-106">An application is a collection of constituent services that perform a certain function or functions.</span></span> <span data-ttu-id="8b2db-107">Um serviço executa uma função completa e autônoma e pode iniciar e executar independentemente de outros serviços.</span><span class="sxs-lookup"><span data-stu-id="8b2db-107">A service performs a complete and standalone function and can start and run independently of other services.</span></span>  <span data-ttu-id="8b2db-108">Um serviço é composto de código, configuração e dados.</span><span class="sxs-lookup"><span data-stu-id="8b2db-108">A service is composed of code, configuration, and data.</span></span> <span data-ttu-id="8b2db-109">Para cada serviço, código consiste em binários executáveis hello, a configuração consiste em configurações de serviço que podem ser carregadas no tempo de execução e dados consistem em dados estáticos arbitrário toobe consumido pelo serviço de saudação.</span><span class="sxs-lookup"><span data-stu-id="8b2db-109">For each service, code consists of hello executable binaries, configuration consists of service settings that can be loaded at run time, and data consists of arbitrary static data toobe consumed by hello service.</span></span> <span data-ttu-id="8b2db-110">Cada componente nesse modelo hierárquico de aplicativo pode ser atualizado e transformado em outra versão independentemente.</span><span class="sxs-lookup"><span data-stu-id="8b2db-110">Each component in this hierarchical application model can be versioned and upgraded independently.</span></span>

![modelo de aplicativo do Service Fabric Olá][appmodel-diagram]

<span data-ttu-id="8b2db-112">Um tipo de aplicativo é uma categorização de um aplicativo e consiste em um pacote de tipos de serviço.</span><span class="sxs-lookup"><span data-stu-id="8b2db-112">An application type is a categorization of an application and consists of a bundle of service types.</span></span> <span data-ttu-id="8b2db-113">Um tipo de serviço é uma categorização de um serviço.</span><span class="sxs-lookup"><span data-stu-id="8b2db-113">A service type is a categorization of a service.</span></span> <span data-ttu-id="8b2db-114">categorização de saudação pode ter diferentes definições e configurações, mas permanece de funcionalidade de núcleo Olá Olá mesmo.</span><span class="sxs-lookup"><span data-stu-id="8b2db-114">hello categorization can have different settings and configurations, but hello core functionality remains hello same.</span></span> <span data-ttu-id="8b2db-115">Olá, instâncias de um serviço são variações de configuração de serviço diferente de saudação do hello mesmo tipo de serviço.</span><span class="sxs-lookup"><span data-stu-id="8b2db-115">hello instances of a service are hello different service configuration variations of hello same service type.</span></span>  

<span data-ttu-id="8b2db-116">Classes (ou "tipos") de aplicativos e serviços são descritas por meio de arquivos XML (manifestos de aplicativo e manifestos do serviço).</span><span class="sxs-lookup"><span data-stu-id="8b2db-116">Classes (or "types") of applications and services are described through XML files (application manifests and service manifests).</span></span>  <span data-ttu-id="8b2db-117">Olá manifestos são modelos de saudação em relação ao qual os aplicativos podem ser instanciados do cluster de saudação repositório de imagens.</span><span class="sxs-lookup"><span data-stu-id="8b2db-117">hello manifests are hello templates against which applications can be instantiated from hello cluster's image store.</span></span> <span data-ttu-id="8b2db-118">Olá definição de esquema para o arquivo ServiceManifest.xml e ApplicationManifest.xml de saudação é instalada com hello SDK do Service Fabric e ferramentas muito*C:\Program Files\Microsoft SDKs\Service Fabric\schemas\ServiceFabricServiceModel.xsd*.</span><span class="sxs-lookup"><span data-stu-id="8b2db-118">hello schema definition for hello ServiceManifest.xml and ApplicationManifest.xml file is installed with hello Service Fabric SDK and tools too*C:\Program Files\Microsoft SDKs\Service Fabric\schemas\ServiceFabricServiceModel.xsd*.</span></span>

<span data-ttu-id="8b2db-119">código de saudação para instâncias diferentes de aplicativos executados como processos separados, mesmo quando hospedados por Olá mesmo nó de malha do serviço.</span><span class="sxs-lookup"><span data-stu-id="8b2db-119">hello code for different application instances run as separate processes even when hosted by hello same Service Fabric node.</span></span> <span data-ttu-id="8b2db-120">Além disso, o ciclo de vida de saudação de cada instância de aplicativo pode ser gerenciado (por exemplo, atualizado) independentemente.</span><span class="sxs-lookup"><span data-stu-id="8b2db-120">Furthermore, hello lifecycle of each application instance can be managed (for example, upgraded) independently.</span></span> <span data-ttu-id="8b2db-121">Olá diagrama a seguir mostra como os tipos de aplicativos são compostos de tipos de serviço, que por sua vez, são compostos de código, configuração e pacotes de dados.</span><span class="sxs-lookup"><span data-stu-id="8b2db-121">hello following diagram shows how application types are composed of service types, which in turn are composed of code, configuration, and data packages.</span></span> <span data-ttu-id="8b2db-122">diagrama de saudação toosimplify, apenas pacotes de dados/de configuração de código Olá para `ServiceType4` são mostrados, embora cada tipo de serviço inclui alguns ou todos os tipos de pacotes.</span><span class="sxs-lookup"><span data-stu-id="8b2db-122">toosimplify hello diagram, only hello code/config/data packages for `ServiceType4` are shown, though each service type would include some or all those package types.</span></span>

![Tipos de aplicativos do Service Fabric e tipos de serviço][cluster-imagestore-apptypes]

<span data-ttu-id="8b2db-124">Dois arquivos de manifesto diferentes são usados toodescribe aplicativos e serviços: Olá manifesto do serviço e o manifesto do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="8b2db-124">Two different manifest files are used toodescribe applications and services: hello service manifest and application manifest.</span></span> <span data-ttu-id="8b2db-125">Manifestos são abordados detalhadamente em Olá seções a seguir.</span><span class="sxs-lookup"><span data-stu-id="8b2db-125">Manifests are covered in detail in hello following sections.</span></span>

<span data-ttu-id="8b2db-126">Pode haver uma ou mais instâncias de um tipo de serviço ativo no cluster hello.</span><span class="sxs-lookup"><span data-stu-id="8b2db-126">There can be one or more instances of a service type active in hello cluster.</span></span> <span data-ttu-id="8b2db-127">Por exemplo, instâncias de serviço com monitoração de estado ou réplicas atingir alta confiabilidade replicando o estado entre as réplicas localizadas em diferentes nós de cluster de saudação.</span><span class="sxs-lookup"><span data-stu-id="8b2db-127">For example, stateful service instances, or replicas, achieve high reliability by replicating state between replicas located on different nodes in hello cluster.</span></span> <span data-ttu-id="8b2db-128">Replicação essencialmente fornece redundância para Olá toobe de serviço disponível, mesmo se um nó em um cluster falha.</span><span class="sxs-lookup"><span data-stu-id="8b2db-128">Replication essentially provides redundancy for hello service toobe available even if one node in a cluster fails.</span></span> <span data-ttu-id="8b2db-129">Um [particionada serviço](service-fabric-concepts-partitioning.md) mais divide seu estado (e o estado de toothat de padrões de acesso) em nós de cluster de saudação.</span><span class="sxs-lookup"><span data-stu-id="8b2db-129">A [partitioned service](service-fabric-concepts-partitioning.md) further divides its state (and access patterns toothat state) across nodes in hello cluster.</span></span>

<span data-ttu-id="8b2db-130">Olá diagrama a seguir mostra a relação Olá entre aplicativos e instâncias de serviço, partições e réplicas.</span><span class="sxs-lookup"><span data-stu-id="8b2db-130">hello following diagram shows hello relationship between applications and service instances, partitions, and replicas.</span></span>

![Partições e réplicas dentro de um serviço][cluster-application-instances]

> [!TIP]
> <span data-ttu-id="8b2db-132">Você pode exibir o layout de saudação de aplicativos em um cluster usando a ferramenta de Gerenciador do Service Fabric Olá disponível em http://&lt;yourclusteraddress&gt;: 19080/Explorer.</span><span class="sxs-lookup"><span data-stu-id="8b2db-132">You can view hello layout of applications in a cluster using hello Service Fabric Explorer tool available at http://&lt;yourclusteraddress&gt;:19080/Explorer.</span></span> <span data-ttu-id="8b2db-133">Para obter mais informações, consulte [Visualizando o cluster com o Service Fabric Explorer](service-fabric-visualizing-your-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="8b2db-133">For more information, see [Visualizing your cluster with Service Fabric Explorer](service-fabric-visualizing-your-cluster.md).</span></span>
> 
> 

## <a name="describe-a-service"></a><span data-ttu-id="8b2db-134">Descrever um serviço</span><span class="sxs-lookup"><span data-stu-id="8b2db-134">Describe a service</span></span>
<span data-ttu-id="8b2db-135">manifesto do serviço Olá declarativamente define a versão e o tipo de serviço hello.</span><span class="sxs-lookup"><span data-stu-id="8b2db-135">hello service manifest declaratively defines hello service type and version.</span></span> <span data-ttu-id="8b2db-136">Ele especifica os metadados de serviço, como o tipo de serviço, propriedades de integridade, métricas de balanceamento de carga, binários de serviço e arquivos de configuração.</span><span class="sxs-lookup"><span data-stu-id="8b2db-136">It specifies service metadata such as service type, health properties, load-balancing metrics, service binaries, and configuration files.</span></span>  <span data-ttu-id="8b2db-137">Ou seja, ele descreve pacotes de código, configuração e dados de saudação que compõem um toosupport do pacote de serviço um ou mais tipos de serviço.</span><span class="sxs-lookup"><span data-stu-id="8b2db-137">Put another way, it describes hello code, configuration, and data packages that compose a service package toosupport one or more service types.</span></span> <span data-ttu-id="8b2db-138">Aqui está um manifesto do serviço de exemplo simples:</span><span class="sxs-lookup"><span data-stu-id="8b2db-138">Here is a simple example service manifest:</span></span>

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

<span data-ttu-id="8b2db-139">**Versão** atributos são cadeias de caracteres não estruturadas e não analisada pelo sistema hello.</span><span class="sxs-lookup"><span data-stu-id="8b2db-139">**Version** attributes are unstructured strings and not parsed by hello system.</span></span> <span data-ttu-id="8b2db-140">Atributos de versão é usada tooversion cada componente para atualizações.</span><span class="sxs-lookup"><span data-stu-id="8b2db-140">Version attributes are used tooversion each component for upgrades.</span></span>

<span data-ttu-id="8b2db-141">**ServiceTypes** declara para quais tipos de serviço há suporte pelos **CodePackages** neste manifesto.</span><span class="sxs-lookup"><span data-stu-id="8b2db-141">**ServiceTypes** declares what service types are supported by **CodePackages** in this manifest.</span></span> <span data-ttu-id="8b2db-142">Quando um serviço é instanciado em relação a um desses tipos de serviço, todos os pacotes de código declarados nesse manifesto são ativados com a execução de seus pontos de entrada.</span><span class="sxs-lookup"><span data-stu-id="8b2db-142">When a service is instantiated against one of these service types, all code packages declared in this manifest are activated by running their entry points.</span></span> <span data-ttu-id="8b2db-143">processos resultantes Olá são tipos de serviço tooregister esperado Olá tem suportada em tempo de execução.</span><span class="sxs-lookup"><span data-stu-id="8b2db-143">hello resulting processes are expected tooregister hello supported service types at run time.</span></span> <span data-ttu-id="8b2db-144">Tipos de serviço são declarados no nível de manifesto de saudação e não Olá nível de pacote de código.</span><span class="sxs-lookup"><span data-stu-id="8b2db-144">Service types are declared at hello manifest level and not hello code package level.</span></span> <span data-ttu-id="8b2db-145">Portanto quando há vários pacotes de código, eles são todos ativados sempre que o sistema Olá procura por qualquer uma das Olá declarado como tipos de serviço.</span><span class="sxs-lookup"><span data-stu-id="8b2db-145">So when there are multiple code packages, they are all activated whenever hello system looks for any one of hello declared service types.</span></span>

<span data-ttu-id="8b2db-146">**SetupEntryPoint** é um ponto de entrada com privilégios que é executado com hello mesmo credenciais como Service Fabric (normalmente Olá *LocalSystem* conta) antes de qualquer outro ponto de entrada.</span><span class="sxs-lookup"><span data-stu-id="8b2db-146">**SetupEntryPoint** is a privileged entry point that runs with hello same credentials as Service Fabric (typically hello *LocalSystem* account) before any other entry point.</span></span> <span data-ttu-id="8b2db-147">executável de saudação especificado por **EntryPoint** normalmente é o host de serviço de longa execução hello.</span><span class="sxs-lookup"><span data-stu-id="8b2db-147">hello executable specified by **EntryPoint** is typically hello long-running service host.</span></span> <span data-ttu-id="8b2db-148">presença de saudação de um ponto de entrada de instalação separado evita que o host de serviço toorun Olá com altos privilégios por longos períodos de tempo.</span><span class="sxs-lookup"><span data-stu-id="8b2db-148">hello presence of a separate setup entry point avoids having toorun hello service host with high privileges for extended periods of time.</span></span> <span data-ttu-id="8b2db-149">executável de saudação especificado por **EntryPoint** é executado após a **SetupEntryPoint** é encerrada com êxito.</span><span class="sxs-lookup"><span data-stu-id="8b2db-149">hello executable specified by **EntryPoint** is run after **SetupEntryPoint** exits successfully.</span></span> <span data-ttu-id="8b2db-150">Se o processo de saudação nunca termina ou falha, o processo resultante Olá é monitorado e reiniciado (começando novamente com **SetupEntryPoint**).</span><span class="sxs-lookup"><span data-stu-id="8b2db-150">If hello process ever terminates or crashes, hello resulting process is monitored and restarted (beginning again with **SetupEntryPoint**).</span></span>  

<span data-ttu-id="8b2db-151">Cenários típicos de uso **SetupEntryPoint** são quando você executa um executável antes do início do serviço de saudação ou executar uma operação com privilégios elevados.</span><span class="sxs-lookup"><span data-stu-id="8b2db-151">Typical scenarios for using **SetupEntryPoint** are when you run an executable before hello service starts or you perform an operation with elevated privileges.</span></span> <span data-ttu-id="8b2db-152">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="8b2db-152">For example:</span></span>

* <span data-ttu-id="8b2db-153">Configurando e inicializar variáveis de ambiente que Olá necessidades executável do serviço.</span><span class="sxs-lookup"><span data-stu-id="8b2db-153">Setting up and initializing environment variables that hello service executable needs.</span></span> <span data-ttu-id="8b2db-154">Isso não é limitado tooonly executáveis gravados por meio de modelos de programação de malha do serviço de saudação.</span><span class="sxs-lookup"><span data-stu-id="8b2db-154">This is not limited tooonly executables written via hello Service Fabric programming models.</span></span> <span data-ttu-id="8b2db-155">Por exemplo, npm.exe precisa de algumas variáveis de ambiente configurados para implantar um aplicativo node.js.</span><span class="sxs-lookup"><span data-stu-id="8b2db-155">For example, npm.exe needs some environment variables configured for deploying a node.js application.</span></span>
* <span data-ttu-id="8b2db-156">Configurando o controle de acesso, instalando certificados de segurança.</span><span class="sxs-lookup"><span data-stu-id="8b2db-156">Setting up access control by installing security certificates.</span></span>

<span data-ttu-id="8b2db-157">Para obter mais detalhes sobre como Olá tooconfigure **SetupEntryPoint** consulte [configurar política de saudação para um ponto de entrada de configuração de serviço](service-fabric-application-runas-security.md)</span><span class="sxs-lookup"><span data-stu-id="8b2db-157">For more details on how tooconfigure hello **SetupEntryPoint** see [Configure hello policy for a service setup entry point](service-fabric-application-runas-security.md)</span></span>

<span data-ttu-id="8b2db-158">**EnvironmentVariables** fornece uma lista de variáveis de ambiente que são definidas para este pacote de códigos.</span><span class="sxs-lookup"><span data-stu-id="8b2db-158">**EnvironmentVariables** provides a list of environment variables that are set for this code package.</span></span> <span data-ttu-id="8b2db-159">Environmentment variáveis podem ser substituídas na Olá `ApplicationManifest.xml` tooprovide de valores diferentes para instâncias de serviço diferente.</span><span class="sxs-lookup"><span data-stu-id="8b2db-159">Environmentment variables can be overridden in hello `ApplicationManifest.xml` tooprovide different values for different service instances.</span></span> 

<span data-ttu-id="8b2db-160">**DataPackage** declara uma pasta nomeada pelo Olá **nome** atributo, que contém dados estáticos arbitrário toobe consumido pelo processo de saudação em tempo de execução.</span><span class="sxs-lookup"><span data-stu-id="8b2db-160">**DataPackage** declares a folder, named by hello **Name** attribute, that contains arbitrary static data toobe consumed by hello process at run time.</span></span>

<span data-ttu-id="8b2db-161">**ConfigPackage** declara uma pasta nomeada pelo Olá **nome** atributo, que contém um *Settings.xml* arquivo.</span><span class="sxs-lookup"><span data-stu-id="8b2db-161">**ConfigPackage** declares a folder, named by hello **Name** attribute, that contains a *Settings.xml* file.</span></span> <span data-ttu-id="8b2db-162">arquivo de configurações de saudação contém seções de configurações de par definida pelo usuário, o valor de chave que Olá processo ler de volta no tempo de execução.</span><span class="sxs-lookup"><span data-stu-id="8b2db-162">hello settings file contains sections of user-defined, key-value pair settings that hello process reads back at run time.</span></span> <span data-ttu-id="8b2db-163">Durante uma atualização, se apenas Olá **ConfigPackage** **versão** foi alterado, Olá executando o processo não será reiniciado.</span><span class="sxs-lookup"><span data-stu-id="8b2db-163">During an upgrade, if only hello **ConfigPackage** **version** has changed, then hello running process is not restarted.</span></span> <span data-ttu-id="8b2db-164">Em vez disso, um retorno de chamada notifica o processo de saudação configurações foram alteradas para que possam ser recarregadas dinamicamente.</span><span class="sxs-lookup"><span data-stu-id="8b2db-164">Instead, a callback notifies hello process that configuration settings have changed so they can be reloaded dynamically.</span></span> <span data-ttu-id="8b2db-165">Aqui está um exemplo do arquivo *Settings.xml* :</span><span class="sxs-lookup"><span data-stu-id="8b2db-165">Here is an example *Settings.xml* file:</span></span>

```xml
<Settings xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/2011/01/fabric">
  <Section Name="MyConfigurationSection">
    <Parameter Name="MySettingA" Value="Example1" />
    <Parameter Name="MySettingB" Value="Example2" />
  </Section>
</Settings>
```

> [!NOTE]
> <span data-ttu-id="8b2db-166">Um manifesto do serviço pode conter vários pacotes de código, de configuração e de dados.</span><span class="sxs-lookup"><span data-stu-id="8b2db-166">A service manifest can contain multiple code, configuration, and data packages.</span></span> <span data-ttu-id="8b2db-167">Cada um deles pode ser transformado em versão independentemente.</span><span class="sxs-lookup"><span data-stu-id="8b2db-167">Each of those can be versioned independently.</span></span>
> 
> 

<!--
For more information about other features supported by service manifests, refer toohello following articles:

*TODO: LoadMetrics, PlacementConstraints, ServicePlacementPolicies
*TODO: Resources
*TODO: Health properties
*TODO: Trace filters
*TODO: Configuration overrides
-->

## <a name="describe-an-application"></a><span data-ttu-id="8b2db-168">Descrever um aplicativo</span><span class="sxs-lookup"><span data-stu-id="8b2db-168">Describe an application</span></span>
<span data-ttu-id="8b2db-169">o manifesto do aplicativo Hello declarativamente descreve a versão e o tipo de aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="8b2db-169">hello application manifest declaratively describes hello application type and version.</span></span> <span data-ttu-id="8b2db-170">Ele especifica os metadados de composição de serviço, como nomes estáveis, esquema de particionamento, fator de replicação/contagem de instância, política de segurança/isolamento, restrições de posicionamento, substituições de configuração e tipos de serviço membro.</span><span class="sxs-lookup"><span data-stu-id="8b2db-170">It specifies service composition metadata such as stable names, partitioning scheme, instance count/replication factor, security/isolation policy, placement constraints, configuration overrides, and constituent service types.</span></span> <span data-ttu-id="8b2db-171">domínios de balanceamento de carga de saudação no qual o aplicativo hello é colocado também são descritos.</span><span class="sxs-lookup"><span data-stu-id="8b2db-171">hello load-balancing domains into which hello application is placed are also described.</span></span>

<span data-ttu-id="8b2db-172">Assim, um manifesto de aplicativo descreve elementos em nível de aplicativo hello e faz referência a um ou mais serviços manifestos toocompose um tipo de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="8b2db-172">Thus, an application manifest describes elements at hello application level and references one or more service manifests toocompose an application type.</span></span> <span data-ttu-id="8b2db-173">Aqui está um manifesto de aplicativo de exemplo simples:</span><span class="sxs-lookup"><span data-stu-id="8b2db-173">Here is a simple example application manifest:</span></span>

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

<span data-ttu-id="8b2db-174">Manifestos de serviço, como **versão** atributos são cadeias de caracteres não estruturadas e não são analisados pelo sistema hello.</span><span class="sxs-lookup"><span data-stu-id="8b2db-174">Like service manifests, **Version** attributes are unstructured strings and are not parsed by hello system.</span></span> <span data-ttu-id="8b2db-175">Atributos de versão também é usada tooversion cada componente para atualizações.</span><span class="sxs-lookup"><span data-stu-id="8b2db-175">Version attributes are also used tooversion each component for upgrades.</span></span>

<span data-ttu-id="8b2db-176">**Servicemanifestimport ao** contém manifestos de tooservice de referências que compõem esse tipo de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="8b2db-176">**ServiceManifestImport** contains references tooservice manifests that compose this application type.</span></span> <span data-ttu-id="8b2db-177">Os manifestos de serviço importados determinam quais tipos de serviço são válidos nesse tipo de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="8b2db-177">Imported service manifests determine what service types are valid within this application type.</span></span> <span data-ttu-id="8b2db-178">Dentro de Olá servicemanifestimport ao, você substituem os valores de configuração em Settings.xml e o ambiente de variáveis nos arquivos ServiceManifest.xml.</span><span class="sxs-lookup"><span data-stu-id="8b2db-178">Within hello ServiceManifestImport, you override configuration values in Settings.xml and environment variables in ServiceManifest.xml files.</span></span> 


<span data-ttu-id="8b2db-179">**DefaultServices** declara as instâncias de serviço que são criadas automaticamente sempre que um aplicativo é instanciado em relação a esse tipo de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="8b2db-179">**DefaultServices** declares service instances that are automatically created whenever an application is instantiated against this application type.</span></span> <span data-ttu-id="8b2db-180">Serviços padrão são apenas uma conveniência e se comportam como serviços normais em todos os aspectos após terem sido criados.</span><span class="sxs-lookup"><span data-stu-id="8b2db-180">Default services are just a convenience and behave like normal services in every respect after they have been created.</span></span> <span data-ttu-id="8b2db-181">Eles são atualizados juntamente com outros serviços na instância do aplicativo hello e também podem ser removidos.</span><span class="sxs-lookup"><span data-stu-id="8b2db-181">They are upgraded along with any other services in hello application instance and can be removed as well.</span></span>

> [!NOTE]
> <span data-ttu-id="8b2db-182">Um manifesto de aplicativo pode conter várias importações de manifesto do serviço e serviços padrão.</span><span class="sxs-lookup"><span data-stu-id="8b2db-182">An application manifest can contain multiple service manifest imports and default services.</span></span> <span data-ttu-id="8b2db-183">Cada importação de manifesto do serviço pode ser transformada em versão independentemente.</span><span class="sxs-lookup"><span data-stu-id="8b2db-183">Each service manifest import can be versioned independently.</span></span>
> 
> 

<span data-ttu-id="8b2db-184">toolearn como toomaintain diferentes do aplicativo e os parâmetros de serviço para ambientes individuais, consulte [gerenciar parâmetros do aplicativo para vários ambientes](service-fabric-manage-multiple-environment-app-configuration.md).</span><span class="sxs-lookup"><span data-stu-id="8b2db-184">toolearn how toomaintain different application and service parameters for individual environments, see [Managing application parameters for multiple environments](service-fabric-manage-multiple-environment-app-configuration.md).</span></span>

<!--
For more information about other features supported by application manifests, refer toohello following articles:

*TODO: Application parameters
*TODO: Security, Principals, RunAs, SecurityAccessPolicy
*TODO: Service Templates
-->



## <a name="next-steps"></a><span data-ttu-id="8b2db-185">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="8b2db-185">Next steps</span></span>
<span data-ttu-id="8b2db-186">[Empacotar um aplicativo](service-fabric-package-apps.md) e torná-lo pronto toodeploy.</span><span class="sxs-lookup"><span data-stu-id="8b2db-186">[Package an application](service-fabric-package-apps.md) and make it ready toodeploy.</span></span>

<span data-ttu-id="8b2db-187">[Implantar e remover aplicativos] [ 10] descreve como instâncias do aplicativo toouse PowerShell toomanage.</span><span class="sxs-lookup"><span data-stu-id="8b2db-187">[Deploy and remove applications][10] describes how toouse PowerShell toomanage application instances.</span></span>

<span data-ttu-id="8b2db-188">[Gerenciando parâmetros do aplicativo para vários ambientes] [ 11] descreve como tooconfigure parâmetros e variáveis de ambiente para instâncias de aplicativo diferente.</span><span class="sxs-lookup"><span data-stu-id="8b2db-188">[Managing application parameters for multiple environments][11] describes how tooconfigure parameters and environment variables for different application instances.</span></span>

<span data-ttu-id="8b2db-189">[Configurar políticas de segurança para seu aplicativo] [ 12] descreve como os serviços de toorun em acesso de toorestrict de políticas de segurança.</span><span class="sxs-lookup"><span data-stu-id="8b2db-189">[Configure security policies for your application][12] describes how toorun services under security policies toorestrict access.</span></span>

<span data-ttu-id="8b2db-190">Os [modelos de hospedagem de aplicativo][13] descrevem a relação entre réplicas (ou instâncias) de um serviço implantado e o processo de host do serviço.</span><span class="sxs-lookup"><span data-stu-id="8b2db-190">[Application hosting models][13] describe relationship between replicas (or instances) of a deployed service and service-host process.</span></span>

<!--Image references-->
[appmodel-diagram]: ./media/service-fabric-application-model/application-model.png
[cluster-imagestore-apptypes]: ./media/service-fabric-application-model/cluster-imagestore-apptypes.png
[cluster-application-instances]: media/service-fabric-application-model/cluster-application-instances.png

<!--Link references--In actual articles, you only need a single period before hello slash-->
[10]: service-fabric-deploy-remove-applications.md
[11]: service-fabric-manage-multiple-environment-app-configuration.md
[12]: service-fabric-application-runas-security.md
[13]: service-fabric-hosting-model.md
