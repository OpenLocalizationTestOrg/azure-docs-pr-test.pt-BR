---
title: "aaaManage vários ambientes na malha do serviço | Microsoft Docs"
description: "Aplicativos de malha do serviço podem ser executados em clusters que variam em tamanho de um toothousands de máquina de máquinas. Em alguns casos, você desejará tooconfigure seu aplicativo diferentes para esses ambientes variados. Este artigo aborda como parâmetros de aplicativo diferente de toodefine por ambiente."
services: service-fabric
documentationcenter: .net
author: mikkelhegn
manager: timlt
editor: 
ms.assetid: f406eac9-7271-4c37-a0d3-0a2957b60537
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: mikkelhegn
ms.openlocfilehash: 2b3327e0e1a3bbd35a50835e720619f308b1b501
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-application-parameters-for-multiple-environments"></a><span data-ttu-id="ba7ea-105">Gerenciar parâmetros do aplicativo para vários ambientes</span><span class="sxs-lookup"><span data-stu-id="ba7ea-105">Manage application parameters for multiple environments</span></span>
<span data-ttu-id="ba7ea-106">Você pode criar clusters de malha do serviço do Azure, usando qualquer parte de um toomany milhares de máquinas.</span><span class="sxs-lookup"><span data-stu-id="ba7ea-106">You can create Azure Service Fabric clusters by using anywhere from one toomany thousands of machines.</span></span> <span data-ttu-id="ba7ea-107">Enquanto os binários de aplicativo podem ser executado sem modificação nesse amplo espectro de ambientes, você geralmente deseja tooconfigure Olá aplicativo diferente, dependendo do número de saudação de máquinas que você estiver implantando em.</span><span class="sxs-lookup"><span data-stu-id="ba7ea-107">While application binaries can run without modification across this wide spectrum of environments, you often want tooconfigure hello application differently, depending on hello number of machines you're deploying to.</span></span>

<span data-ttu-id="ba7ea-108">Como um exemplo simples, considere a `InstanceCount` para um serviço sem estado.</span><span class="sxs-lookup"><span data-stu-id="ba7ea-108">As a simple example, consider `InstanceCount` for a stateless service.</span></span> <span data-ttu-id="ba7ea-109">Quando você estiver executando aplicativos no Azure, geralmente convém tooset este toohello especial valor de parâmetro "-1".</span><span class="sxs-lookup"><span data-stu-id="ba7ea-109">When you are running applications in Azure, you generally want tooset this parameter toohello special value of "-1".</span></span> <span data-ttu-id="ba7ea-110">Essa configuração garante que o serviço está em execução em cada nó no cluster hello (ou todos os nós no tipo de nó Olá se você tiver definido uma restrição de posicionamento).</span><span class="sxs-lookup"><span data-stu-id="ba7ea-110">This configuration ensures that your service is running on every node in hello cluster (or every node in hello node type if you have set a placement constraint).</span></span> <span data-ttu-id="ba7ea-111">No entanto, essa configuração não é adequada para um cluster de computador único porque você não pode ter vários processos escutando Olá mesmo ponto de extremidade em um único computador.</span><span class="sxs-lookup"><span data-stu-id="ba7ea-111">However, this configuration is not suitable for a single-machine cluster since you cannot have multiple processes listening on hello same endpoint on a single machine.</span></span> <span data-ttu-id="ba7ea-112">Em vez disso, você normalmente define `InstanceCount` muito "1".</span><span class="sxs-lookup"><span data-stu-id="ba7ea-112">Instead, you typically set `InstanceCount` too"1".</span></span>

## <a name="specifying-environment-specific-parameters"></a><span data-ttu-id="ba7ea-113">Especificando parâmetros específicos do ambiente</span><span class="sxs-lookup"><span data-stu-id="ba7ea-113">Specifying environment-specific parameters</span></span>
<span data-ttu-id="ba7ea-114">problema de configuração de toothis Olá solução é um conjunto de serviços padrão com parâmetros e arquivos de parâmetro de aplicativo que preencham os valores de parâmetro para um determinado ambiente.</span><span class="sxs-lookup"><span data-stu-id="ba7ea-114">hello solution toothis configuration issue is a set of parameterized default services and application parameter files that fill in those parameter values for a given environment.</span></span> <span data-ttu-id="ba7ea-115">Serviços padrão e parâmetros do aplicativo são configurados no aplicativo hello e manifestos do serviço.</span><span class="sxs-lookup"><span data-stu-id="ba7ea-115">Default services and application parameters are configured in hello application and service manifests.</span></span> <span data-ttu-id="ba7ea-116">Olá definição de esquema para arquivos ServiceManifest.xml e ApplicationManifest.xml de saudação é instalada com hello SDK do Service Fabric e ferramentas muito*C:\Program Files\Microsoft SDKs\Service Fabric\schemas\ServiceFabricServiceModel.xsd*.</span><span class="sxs-lookup"><span data-stu-id="ba7ea-116">hello schema definition for hello ServiceManifest.xml and ApplicationManifest.xml files is installed with hello Service Fabric SDK and tools too*C:\Program Files\Microsoft SDKs\Service Fabric\schemas\ServiceFabricServiceModel.xsd*.</span></span>

### <a name="default-services"></a><span data-ttu-id="ba7ea-117">Serviços padrão</span><span class="sxs-lookup"><span data-stu-id="ba7ea-117">Default services</span></span>
<span data-ttu-id="ba7ea-118">Os aplicativos do Service Fabric são compostos de uma coleção de instâncias de serviço.</span><span class="sxs-lookup"><span data-stu-id="ba7ea-118">Service Fabric applications are made up of a collection of service instances.</span></span> <span data-ttu-id="ba7ea-119">Enquanto é possível toocreate um aplicativo vazio e, em seguida, criar dinamicamente todas as instâncias de serviço, a maioria dos aplicativos têm um conjunto de serviços principais que sempre deve ser criada quando o aplicativo hello é instanciado.</span><span class="sxs-lookup"><span data-stu-id="ba7ea-119">While it is possible for you toocreate an empty application and then create all service instances dynamically, most applications have a set of core services that should always be created when hello application is instantiated.</span></span> <span data-ttu-id="ba7ea-120">Esses são chamados tooas "serviços padrão".</span><span class="sxs-lookup"><span data-stu-id="ba7ea-120">These are referred tooas "default services".</span></span> <span data-ttu-id="ba7ea-121">Eles são especificados no manifesto de aplicativo hello, com espaços reservados para a configuração de per ambiente incluído entre colchetes:</span><span class="sxs-lookup"><span data-stu-id="ba7ea-121">They are specified in hello application manifest, with placeholders for per-environment configuration included in square brackets:</span></span>

```xml
  <DefaultServices>
      <Service Name="Stateful1">
          <StatefulService
              ServiceTypeName="Stateful1Type"
              TargetReplicaSetSize="[Stateful1_TargetReplicaSetSize]"
              MinReplicaSetSize="[Stateful1_MinReplicaSetSize]">

              <UniformInt64Partition
                  PartitionCount="[Stateful1_PartitionCount]"
                  LowKey="-9223372036854775808"
                  HighKey="9223372036854775807"
              />
        </StatefulService>
    </Service>
  </DefaultServices>
```

<span data-ttu-id="ba7ea-122">Cada Olá parâmetros nomeado deve ser definida no elemento de parâmetros Olá Olá do manifesto do aplicativo:</span><span class="sxs-lookup"><span data-stu-id="ba7ea-122">Each of hello named parameters must be defined within hello Parameters element of hello application manifest:</span></span>

```xml
    <Parameters>
        <Parameter Name="Stateful1_MinReplicaSetSize" DefaultValue="3" />
        <Parameter Name="Stateful1_PartitionCount" DefaultValue="1" />
        <Parameter Name="Stateful1_TargetReplicaSetSize" DefaultValue="3" />
    </Parameters>
```

<span data-ttu-id="ba7ea-123">atributo DefaultValue de saudação especifica Olá valor toobe usado na ausência de saudação de um parâmetro mais específicas para um determinado ambiente.</span><span class="sxs-lookup"><span data-stu-id="ba7ea-123">hello DefaultValue attribute specifies hello value toobe used in hello absence of a more-specific parameter for a given environment.</span></span>

> [!NOTE]
> <span data-ttu-id="ba7ea-124">Nem todos os parâmetros da instância de serviço são adequados para a configuração por ambiente.</span><span class="sxs-lookup"><span data-stu-id="ba7ea-124">Not all service instance parameters are suitable for per-environment configuration.</span></span> <span data-ttu-id="ba7ea-125">O exemplo hello acima, Olá LowKey e HighKey valores para o esquema de particionamento do serviço Olá são definidos explicitamente para todas as instâncias do serviço de saudação desde que o intervalo de partição Olá é uma função de saudação do domínio de dados, não o ambiente hello.</span><span class="sxs-lookup"><span data-stu-id="ba7ea-125">In hello example above, hello LowKey and HighKey values for hello service's partitioning scheme are explicitly defined for all instances of hello service since hello partition range is a function of hello data domain, not hello environment.</span></span>
> 
> 

### <a name="per-environment-service-configuration-settings"></a><span data-ttu-id="ba7ea-126">Definições de configuração de serviço por ambiente</span><span class="sxs-lookup"><span data-stu-id="ba7ea-126">Per-environment service configuration settings</span></span>
<span data-ttu-id="ba7ea-127">Olá [o modelo de aplicativo do Service Fabric](service-fabric-application-model.md) habilita serviços tooinclude pacotes de configuração que contém pares chave-valor personalizados que podem ser lidos em tempo de execução.</span><span class="sxs-lookup"><span data-stu-id="ba7ea-127">hello [Service Fabric application model](service-fabric-application-model.md) enables services tooinclude configuration packages that contain custom key-value pairs that are readable at run time.</span></span> <span data-ttu-id="ba7ea-128">os valores Hello dessas configurações também podem ser diferenciados pelo ambiente especificando um `ConfigOverride` no manifesto de aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="ba7ea-128">hello values of these settings can also be differentiated by environment by specifying a `ConfigOverride` in hello application manifest.</span></span>

<span data-ttu-id="ba7ea-129">Suponha que você tenha Olá após a configuração no arquivo Config\Settings.xml Olá Olá `Stateful1` serviço:</span><span class="sxs-lookup"><span data-stu-id="ba7ea-129">Suppose that you have hello following setting in hello Config\Settings.xml file for hello `Stateful1` service:</span></span>

```xml
  <Section Name="MyConfigSection">
     <Parameter Name="MaxQueueSize" Value="25" />
  </Section>
```
<span data-ttu-id="ba7ea-130">toooverride esse valor para um par de aplicativo/ambiente específico, crie um `ConfigOverride` quando você importa o manifesto do serviço Olá no manifesto de aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="ba7ea-130">toooverride this value for a specific application/environment pair, create a `ConfigOverride` when you import hello service manifest in hello application manifest.</span></span>

```xml
  <ConfigOverrides>
     <ConfigOverride Name="Config">
        <Settings>
           <Section Name="MyConfigSection">
              <Parameter Name="MaxQueueSize" Value="[Stateful1_MaxQueueSize]" />
           </Section>
        </Settings>
     </ConfigOverride>
  </ConfigOverrides>
```
<span data-ttu-id="ba7ea-131">Esse parâmetro pode então ser configurado pelo ambiente como mostrado acima.</span><span class="sxs-lookup"><span data-stu-id="ba7ea-131">This parameter can then be configured by environment as shown above.</span></span> <span data-ttu-id="ba7ea-132">Você pode fazer isso declará-la na seção de parâmetros de saudação do manifesto de aplicativo hello e especificando valores específicos de ambiente nos arquivos de parâmetro de aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="ba7ea-132">You can do this by declaring it in hello parameters section of hello application manifest and specifying environment-specific values in hello application parameter files.</span></span>

> [!NOTE]
> <span data-ttu-id="ba7ea-133">No caso de saudação de definições de configuração de serviço, há três locais em que o valor de saudação de uma chave pode ser definido: pacote de configuração de serviço hello, o manifesto do aplicativo hello e arquivo de parâmetro de aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="ba7ea-133">In hello case of service configuration settings, there are three places where hello value of a key can be set: hello service configuration package, hello application manifest, and hello application parameter file.</span></span> <span data-ttu-id="ba7ea-134">Malha do serviço será sempre escolher Olá parâmetro do arquivo de aplicativo primeiro (se especificado), em seguida, Olá manifesto do aplicativo e hello, por fim, o pacote de configuração.</span><span class="sxs-lookup"><span data-stu-id="ba7ea-134">Service Fabric will always choose from hello application parameter file first (if specified), then hello application manifest, and finally hello configuration package.</span></span>
> 
> 

### <a name="setting-and-using-environment-variables"></a><span data-ttu-id="ba7ea-135">Configurando e usando variáveis de ambiente</span><span class="sxs-lookup"><span data-stu-id="ba7ea-135">Setting and using environment variables</span></span> 
<span data-ttu-id="ba7ea-136">Você pode especificar e definir variáveis de ambiente no arquivo ServiceManifest.xml de saudação e, em seguida, substituir no arquivo de ApplicationManifest.xml Olá em uma base por instância.</span><span class="sxs-lookup"><span data-stu-id="ba7ea-136">You can specify and set environment variables in hello ServiceManifest.xml file and then override these in hello ApplicationManifest.xml file on a per instance basis.</span></span>
<span data-ttu-id="ba7ea-137">Olá exemplo a seguir mostra duas variáveis de ambiente, um com um valor definido e outros Olá é substituído.</span><span class="sxs-lookup"><span data-stu-id="ba7ea-137">hello example below shows two environment variables, one with a value set and hello other is overridden.</span></span> <span data-ttu-id="ba7ea-138">Você pode usar parâmetros de valores de variáveis de ambiente tooset em Olá mesma forma que eles foram usados para substituições de configuração do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="ba7ea-138">You can use application parameters tooset environment variables values in hello same way that these were used for config overrides.</span></span>

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
<span data-ttu-id="ba7ea-139">variáveis de ambiente toooverride Olá no hello ApplicationManifest.xml, pacote de códigos de saudação de referência em Olá ServiceManifest com hello `EnvironmentOverrides` elemento.</span><span class="sxs-lookup"><span data-stu-id="ba7ea-139">toooverride hello environment variables in hello ApplicationManifest.xml, reference hello code package in hello ServiceManifest with hello `EnvironmentOverrides` element.</span></span>

```xml
  <ServiceManifestImport>
    <ServiceManifestRef ServiceManifestName="FrontEndServicePkg" ServiceManifestVersion="1.0.0" />
    <EnvironmentOverrides CodePackageRef="MyCode">
      <EnvironmentVariable Name="MyEnvVariable" Value="mydata"/>
    </EnvironmentOverrides>
  </ServiceManifestImport>
 ``` 
 <span data-ttu-id="ba7ea-140">Quando Olá serviço instância nomeada é criado, você pode acessar variáveis de ambiente de saudação do código.</span><span class="sxs-lookup"><span data-stu-id="ba7ea-140">Once hello named service instance is created you can access hello environment variables from code.</span></span> <span data-ttu-id="ba7ea-141">Por exemplo, no c# Faça a seguir Olá</span><span class="sxs-lookup"><span data-stu-id="ba7ea-141">e.g. In C# you can do hello following</span></span>

```csharp
    string EnvVariable = Environment.GetEnvironmentVariable("MyEnvVariable");
```

### <a name="service-fabric-environment-variables"></a><span data-ttu-id="ba7ea-142">Variáveis de ambiente do Service Fabric</span><span class="sxs-lookup"><span data-stu-id="ba7ea-142">Service Fabric environment variables</span></span>
<span data-ttu-id="ba7ea-143">O Service Fabric tem variáveis de ambiente internas definidas para cada instância de serviço.</span><span class="sxs-lookup"><span data-stu-id="ba7ea-143">Service Fabric has built in environment variables set for each service instance.</span></span> <span data-ttu-id="ba7ea-144">Olá lista completa de variáveis de ambiente é abaixo, onde hello aqueles em negrito são Olá aquelas que você usará em seu serviço, Olá outros que está sendo usada pelo tempo de execução do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="ba7ea-144">hello full list of environment variables is below, where hello ones in bold are hello ones that you will use in your service, hello other being used by Service Fabric runtime.</span></span> 

* <span data-ttu-id="ba7ea-145">Fabric_ApplicationHostId</span><span class="sxs-lookup"><span data-stu-id="ba7ea-145">Fabric_ApplicationHostId</span></span>
* <span data-ttu-id="ba7ea-146">Fabric_ApplicationHostType</span><span class="sxs-lookup"><span data-stu-id="ba7ea-146">Fabric_ApplicationHostType</span></span>
* <span data-ttu-id="ba7ea-147">Fabric_ApplicationId</span><span class="sxs-lookup"><span data-stu-id="ba7ea-147">Fabric_ApplicationId</span></span>
* <span data-ttu-id="ba7ea-148">**Fabric_ApplicationName**</span><span class="sxs-lookup"><span data-stu-id="ba7ea-148">**Fabric_ApplicationName**</span></span>
* <span data-ttu-id="ba7ea-149">Fabric_CodePackageInstanceId</span><span class="sxs-lookup"><span data-stu-id="ba7ea-149">Fabric_CodePackageInstanceId</span></span>
* <span data-ttu-id="ba7ea-150">**Fabric_CodePackageName**</span><span class="sxs-lookup"><span data-stu-id="ba7ea-150">**Fabric_CodePackageName**</span></span>
* <span data-ttu-id="ba7ea-151">**Fabric_Endpoint_[YourServiceName]TypeEndpoint**</span><span class="sxs-lookup"><span data-stu-id="ba7ea-151">**Fabric_Endpoint_[YourServiceName]TypeEndpoint**</span></span>
* <span data-ttu-id="ba7ea-152">**Fabric_Folder_App_Log**</span><span class="sxs-lookup"><span data-stu-id="ba7ea-152">**Fabric_Folder_App_Log**</span></span>
* <span data-ttu-id="ba7ea-153">**Fabric_Folder_App_Temp**</span><span class="sxs-lookup"><span data-stu-id="ba7ea-153">**Fabric_Folder_App_Temp**</span></span>
* <span data-ttu-id="ba7ea-154">**Fabric_Folder_App_Work**</span><span class="sxs-lookup"><span data-stu-id="ba7ea-154">**Fabric_Folder_App_Work**</span></span>
* <span data-ttu-id="ba7ea-155">**Fabric_Folder_Application**</span><span class="sxs-lookup"><span data-stu-id="ba7ea-155">**Fabric_Folder_Application**</span></span>
* <span data-ttu-id="ba7ea-156">Fabric_NodeId</span><span class="sxs-lookup"><span data-stu-id="ba7ea-156">Fabric_NodeId</span></span>
* <span data-ttu-id="ba7ea-157">**Fabric_NodeIPOrFQDN**</span><span class="sxs-lookup"><span data-stu-id="ba7ea-157">**Fabric_NodeIPOrFQDN**</span></span>
* <span data-ttu-id="ba7ea-158">**Fabric_NodeName**</span><span class="sxs-lookup"><span data-stu-id="ba7ea-158">**Fabric_NodeName**</span></span>
* <span data-ttu-id="ba7ea-159">Fabric_RuntimeConnectionAddress</span><span class="sxs-lookup"><span data-stu-id="ba7ea-159">Fabric_RuntimeConnectionAddress</span></span>
* <span data-ttu-id="ba7ea-160">Fabric_ServicePackageInstanceId</span><span class="sxs-lookup"><span data-stu-id="ba7ea-160">Fabric_ServicePackageInstanceId</span></span>
* <span data-ttu-id="ba7ea-161">Fabric_ServicePackageName</span><span class="sxs-lookup"><span data-stu-id="ba7ea-161">Fabric_ServicePackageName</span></span>
* <span data-ttu-id="ba7ea-162">Fabric_ServicePackageVersionInstance</span><span class="sxs-lookup"><span data-stu-id="ba7ea-162">Fabric_ServicePackageVersionInstance</span></span>
* <span data-ttu-id="ba7ea-163">FabricPackageFileName</span><span class="sxs-lookup"><span data-stu-id="ba7ea-163">FabricPackageFileName</span></span>

<span data-ttu-id="ba7ea-164">Olá belows de código mostra como toolist Olá variáveis de ambiente do Service Fabric</span><span class="sxs-lookup"><span data-stu-id="ba7ea-164">hello code belows shows how toolist hello Service Fabric environment variables</span></span>
 ```csharp
    foreach (DictionaryEntry de in Environment.GetEnvironmentVariables())
    {
        if (de.Key.ToString().StartsWith("Fabric"))
        {
            Console.WriteLine(" Environment variable {0} = {1}", de.Key, de.Value);
        }
    }
```
<span data-ttu-id="ba7ea-165">Olá, estes são exemplos de variáveis de ambiente para um tipo de aplicativo chamado `GuestExe.Application` com um tipo de serviço chamado `FrontEndService` quando executado em sua máquina de desenvolvimento local.</span><span class="sxs-lookup"><span data-stu-id="ba7ea-165">hello following are examples of environment variables for an application type called `GuestExe.Application` with a service type called `FrontEndService` when run on your local dev machine.</span></span>

* <span data-ttu-id="ba7ea-166">**Fabric_ApplicationName = fabric:/GuestExe.Application**</span><span class="sxs-lookup"><span data-stu-id="ba7ea-166">**Fabric_ApplicationName = fabric:/GuestExe.Application**</span></span>
* <span data-ttu-id="ba7ea-167">**Fabric_CodePackageName = Code**</span><span class="sxs-lookup"><span data-stu-id="ba7ea-167">**Fabric_CodePackageName = Code**</span></span>
* <span data-ttu-id="ba7ea-168">**Fabric_Endpoint_FrontEndServiceTypeEndpoint = 80**</span><span class="sxs-lookup"><span data-stu-id="ba7ea-168">**Fabric_Endpoint_FrontEndServiceTypeEndpoint = 80**</span></span>
* <span data-ttu-id="ba7ea-169">**Fabric_NodeIPOrFQDN = localhost**</span><span class="sxs-lookup"><span data-stu-id="ba7ea-169">**Fabric_NodeIPOrFQDN = localhost**</span></span>
* <span data-ttu-id="ba7ea-170">**Fabric_NodeName = _Node_2**</span><span class="sxs-lookup"><span data-stu-id="ba7ea-170">**Fabric_NodeName = _Node_2**</span></span>

### <a name="application-parameter-files"></a><span data-ttu-id="ba7ea-171">Arquivos de parâmetros de aplicativo</span><span class="sxs-lookup"><span data-stu-id="ba7ea-171">Application parameter files</span></span>
<span data-ttu-id="ba7ea-172">projeto de aplicativo do Service Fabric Olá pode incluir um ou mais arquivos de parâmetro de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="ba7ea-172">hello Service Fabric application project can include one or more application parameter files.</span></span> <span data-ttu-id="ba7ea-173">Cada uma delas define valores específicos de saudação para parâmetros de saudação que são definidos no manifesto de aplicativo hello:</span><span class="sxs-lookup"><span data-stu-id="ba7ea-173">Each of them defines hello specific values for hello parameters that are defined in hello application manifest:</span></span>

```xml
    <!-- ApplicationParameters\Local.xml -->

    <Application Name="fabric:/Application1" xmlns="http://schemas.microsoft.com/2011/01/fabric">
        <Parameters>
            <Parameter Name ="Stateful1_MinReplicaSetSize" Value="3" />
            <Parameter Name="Stateful1_PartitionCount" Value="1" />
            <Parameter Name="Stateful1_TargetReplicaSetSize" Value="3" />
        </Parameters>
    </Application>
```
<span data-ttu-id="ba7ea-174">Por padrão, um novo aplicativo inclui três arquivos de parâmetro de aplicativo, chamados Local.1Node.xml, Local.5Node.xml e Cloud.xml:</span><span class="sxs-lookup"><span data-stu-id="ba7ea-174">By default, a new application includes three application parameter files, named Local.1Node.xml, Local.5Node.xml, and Cloud.xml:</span></span>

![Arquivos de parâmetros de aplicativo no Gerenciador de Soluções][app-parameters-solution-explorer]

<span data-ttu-id="ba7ea-176">toocreate um arquivo de parâmetro, simplesmente copie e cole um existente e dê a ele um novo nome.</span><span class="sxs-lookup"><span data-stu-id="ba7ea-176">toocreate a parameter file, simply copy and paste an existing one and give it a new name.</span></span>

## <a name="identifying-environment-specific-parameters-during-deployment"></a><span data-ttu-id="ba7ea-177">Identificando parâmetros específicos do ambiente durante a implantação</span><span class="sxs-lookup"><span data-stu-id="ba7ea-177">Identifying environment-specific parameters during deployment</span></span>
<span data-ttu-id="ba7ea-178">No momento da implantação, você precisa toochoose Olá parâmetro apropriado arquivo tooapply com seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="ba7ea-178">At deployment time, you need toochoose hello appropriate parameter file tooapply with your application.</span></span> <span data-ttu-id="ba7ea-179">Você pode fazer isso por meio da caixa de diálogo de publicação de saudação no Visual Studio ou PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ba7ea-179">You can do this through hello Publish dialog in Visual Studio or through PowerShell.</span></span>

### <a name="deploy-from-visual-studio"></a><span data-ttu-id="ba7ea-180">Implantar com o Visual Studio</span><span class="sxs-lookup"><span data-stu-id="ba7ea-180">Deploy from Visual Studio</span></span>
<span data-ttu-id="ba7ea-181">Você pode escolher na lista de saudação de arquivos de parâmetros disponíveis quando você publicar seu aplicativo no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="ba7ea-181">You can choose from hello list of available parameter files when you publish your application in Visual Studio.</span></span>

![Escolha um arquivo de parâmetro na caixa de diálogo de publicação Olá][publishdialog]

### <a name="deploy-from-powershell"></a><span data-ttu-id="ba7ea-183">Implantar do PowerShell</span><span class="sxs-lookup"><span data-stu-id="ba7ea-183">Deploy from PowerShell</span></span>
<span data-ttu-id="ba7ea-184">Olá `Deploy-FabricApplication.ps1` script do PowerShell incluído no modelo de projeto de aplicativo hello aceita como um parâmetro de um perfil de publicação e Olá PublishProfile contém um arquivo de parâmetros de aplicativo de toohello de referência.</span><span class="sxs-lookup"><span data-stu-id="ba7ea-184">hello `Deploy-FabricApplication.ps1` PowerShell script included in hello application project template accepts a publish profile as a parameter and hello PublishProfile contains a reference toohello application parameters file.</span></span>

  ```PowerShell
    ./Deploy-FabricApplication -ApplicationPackagePath <app_package_path> -PublishProfileFile <publishprofile_path>
  ```

## <a name="next-steps"></a><span data-ttu-id="ba7ea-185">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="ba7ea-185">Next steps</span></span>
<span data-ttu-id="ba7ea-186">toolearn mais sobre alguns dos conceitos básicos de saudação que são abordados neste tópico, consulte Olá [visão geral técnica do Service Fabric](service-fabric-technical-overview.md).</span><span class="sxs-lookup"><span data-stu-id="ba7ea-186">toolearn more about some of hello core concepts that are discussed in this topic, see hello [Service Fabric technical overview](service-fabric-technical-overview.md).</span></span> <span data-ttu-id="ba7ea-187">Para obter informações sobre outras funcionalidades de gerenciamento de aplicativo disponíveis no Visual Studio, confira [Gerenciar seus aplicativos do Service Fabric no Visual Studio](service-fabric-manage-application-in-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="ba7ea-187">For information about other app management capabilities that are available in Visual Studio, see [Manage your Service Fabric applications in Visual Studio](service-fabric-manage-application-in-visual-studio.md).</span></span>

<!-- Image references -->

[publishdialog]: ./media/service-fabric-manage-multiple-environment-app-configuration/publish-dialog-choose-app-config.png
[app-parameters-solution-explorer]:./media/service-fabric-manage-multiple-environment-app-configuration/app-parameters-in-solution-explorer.png
