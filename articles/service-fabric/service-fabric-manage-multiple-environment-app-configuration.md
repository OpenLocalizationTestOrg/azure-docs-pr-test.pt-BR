---
title: "Gerenciar vários ambientes no Service Fabric | Microsoft Docs"
description: "Os aplicativos do Service Fabric podem ser executados em clusters que variam de tamanho de um computador para milhares de computadores. Em alguns casos, você desejará configurar seu aplicativo de forma diferente para esses ambientes variados. Este artigo aborda como definir parâmetros de aplicativo diferentes por ambiente."
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
ms.openlocfilehash: 9317b3f0b7984e795c4205360ed58e2c4f3fbcb1
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="manage-application-parameters-for-multiple-environments"></a><span data-ttu-id="8f89e-105">Gerenciar parâmetros do aplicativo para vários ambientes</span><span class="sxs-lookup"><span data-stu-id="8f89e-105">Manage application parameters for multiple environments</span></span>
<span data-ttu-id="8f89e-106">Você pode criar clusters do Service Fabric usando em qualquer lugar de um a milhares de computadores.</span><span class="sxs-lookup"><span data-stu-id="8f89e-106">You can create Azure Service Fabric clusters by using anywhere from one to many thousands of machines.</span></span> <span data-ttu-id="8f89e-107">Embora os binários de aplicativo possam ser executados sem modificação em um amplo espectro de ambientes, com frequência, você desejará configurar o aplicativo de forma diferente, dependendo do número de computadores em que ele estiver sendo implantado.</span><span class="sxs-lookup"><span data-stu-id="8f89e-107">While application binaries can run without modification across this wide spectrum of environments, you often want to configure the application differently, depending on the number of machines you're deploying to.</span></span>

<span data-ttu-id="8f89e-108">Como um exemplo simples, considere a `InstanceCount` para um serviço sem estado.</span><span class="sxs-lookup"><span data-stu-id="8f89e-108">As a simple example, consider `InstanceCount` for a stateless service.</span></span> <span data-ttu-id="8f89e-109">Quando você estiver executando aplicativos no Azure, geralmente, você desejará definir esse parâmetro como o valor especial “-1”.</span><span class="sxs-lookup"><span data-stu-id="8f89e-109">When you are running applications in Azure, you generally want to set this parameter to the special value of "-1".</span></span> <span data-ttu-id="8f89e-110">Essa configuração garante que o serviço esteja em execução em cada nó no cluster (ou em todos os nós no tipo de nó, caso você tenha definido uma restrição de posicionamento).</span><span class="sxs-lookup"><span data-stu-id="8f89e-110">This configuration ensures that your service is running on every node in the cluster (or every node in the node type if you have set a placement constraint).</span></span> <span data-ttu-id="8f89e-111">No entanto, essa configuração não é adequada para um cluster de um único computador, pois não é possível ter vários processos escutando o mesmo ponto de extremidade em um único computador.</span><span class="sxs-lookup"><span data-stu-id="8f89e-111">However, this configuration is not suitable for a single-machine cluster since you cannot have multiple processes listening on the same endpoint on a single machine.</span></span> <span data-ttu-id="8f89e-112">Em vez disso, normalmente, você define `InstanceCount` como “1”.</span><span class="sxs-lookup"><span data-stu-id="8f89e-112">Instead, you typically set `InstanceCount` to "1".</span></span>

## <a name="specifying-environment-specific-parameters"></a><span data-ttu-id="8f89e-113">Especificando parâmetros específicos do ambiente</span><span class="sxs-lookup"><span data-stu-id="8f89e-113">Specifying environment-specific parameters</span></span>
<span data-ttu-id="8f89e-114">A solução para esse problema de configuração é um conjunto de serviços padrão parametrizados e arquivos de parâmetros do aplicativo que preencham os valores de parâmetro para um determinado ambiente.</span><span class="sxs-lookup"><span data-stu-id="8f89e-114">The solution to this configuration issue is a set of parameterized default services and application parameter files that fill in those parameter values for a given environment.</span></span> <span data-ttu-id="8f89e-115">Os parâmetros padrão dos serviços e do aplicativo são configurados nos manifestos do aplicativo e do serviço.</span><span class="sxs-lookup"><span data-stu-id="8f89e-115">Default services and application parameters are configured in the application and service manifests.</span></span> <span data-ttu-id="8f89e-116">A definição de esquema dos arquivos ServiceManifest.xml e ApplicationManifest.xml é instalada com o SDK do e as ferramentas do Service Fabric em *C:\Arquivos de Programas\Microsoft SDKs\Service Fabric\schemas\ServiceFabricServiceModel.xsd*.</span><span class="sxs-lookup"><span data-stu-id="8f89e-116">The schema definition for the ServiceManifest.xml and ApplicationManifest.xml files is installed with the Service Fabric SDK and tools to *C:\Program Files\Microsoft SDKs\Service Fabric\schemas\ServiceFabricServiceModel.xsd*.</span></span>

### <a name="default-services"></a><span data-ttu-id="8f89e-117">Serviços padrão</span><span class="sxs-lookup"><span data-stu-id="8f89e-117">Default services</span></span>
<span data-ttu-id="8f89e-118">Os aplicativos do Service Fabric são compostos de uma coleção de instâncias de serviço.</span><span class="sxs-lookup"><span data-stu-id="8f89e-118">Service Fabric applications are made up of a collection of service instances.</span></span> <span data-ttu-id="8f89e-119">Embora seja possível para você criar um aplicativo vazio e, em seguida, criar dinamicamente todas as instâncias de serviço, a maioria dos aplicativos tem um conjunto de serviços principais que sempre deverá ser criado quando o aplicativo for instanciado.</span><span class="sxs-lookup"><span data-stu-id="8f89e-119">While it is possible for you to create an empty application and then create all service instances dynamically, most applications have a set of core services that should always be created when the application is instantiated.</span></span> <span data-ttu-id="8f89e-120">Eles são chamados de "serviços padrão".</span><span class="sxs-lookup"><span data-stu-id="8f89e-120">These are referred to as "default services".</span></span> <span data-ttu-id="8f89e-121">Eles são especificados no manifesto do aplicativo, com espaços reservados para configuração por ambiente incluídos entre colchetes adicionais:</span><span class="sxs-lookup"><span data-stu-id="8f89e-121">They are specified in the application manifest, with placeholders for per-environment configuration included in square brackets:</span></span>

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

<span data-ttu-id="8f89e-122">Cada um dos parâmetros nomeados deve ser definido dentro do elemento Parameters do manifesto do aplicativo:</span><span class="sxs-lookup"><span data-stu-id="8f89e-122">Each of the named parameters must be defined within the Parameters element of the application manifest:</span></span>

```xml
    <Parameters>
        <Parameter Name="Stateful1_MinReplicaSetSize" DefaultValue="3" />
        <Parameter Name="Stateful1_PartitionCount" DefaultValue="1" />
        <Parameter Name="Stateful1_TargetReplicaSetSize" DefaultValue="3" />
    </Parameters>
```

<span data-ttu-id="8f89e-123">O atributo DefaultValue especifica o valor a ser usado na ausência de um parâmetro mais específico para um determinado ambiente.</span><span class="sxs-lookup"><span data-stu-id="8f89e-123">The DefaultValue attribute specifies the value to be used in the absence of a more-specific parameter for a given environment.</span></span>

> [!NOTE]
> <span data-ttu-id="8f89e-124">Nem todos os parâmetros da instância de serviço são adequados para a configuração por ambiente.</span><span class="sxs-lookup"><span data-stu-id="8f89e-124">Not all service instance parameters are suitable for per-environment configuration.</span></span> <span data-ttu-id="8f89e-125">No exemplo acima, os valores LowKey e HighKey para o esquema de particionamento do serviço são definidos explicitamente para todas as instâncias do serviço, já que o intervalo de partição é uma função do domínio de dados, não do ambiente.</span><span class="sxs-lookup"><span data-stu-id="8f89e-125">In the example above, the LowKey and HighKey values for the service's partitioning scheme are explicitly defined for all instances of the service since the partition range is a function of the data domain, not the environment.</span></span>
> 
> 

### <a name="per-environment-service-configuration-settings"></a><span data-ttu-id="8f89e-126">Definições de configuração de serviço por ambiente</span><span class="sxs-lookup"><span data-stu-id="8f89e-126">Per-environment service configuration settings</span></span>
<span data-ttu-id="8f89e-127">O [modelo de aplicativo do Service Fabric](service-fabric-application-model.md) permite que os serviços incluam pacotes de configuração com pares de chave e valor personalizados legíveis em tempo de execução.</span><span class="sxs-lookup"><span data-stu-id="8f89e-127">The [Service Fabric application model](service-fabric-application-model.md) enables services to include configuration packages that contain custom key-value pairs that are readable at run time.</span></span> <span data-ttu-id="8f89e-128">Os valores dessas configurações também podem ser diferenciados pelo ambiente por meio da especificação de uma `ConfigOverride` no manifesto do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="8f89e-128">The values of these settings can also be differentiated by environment by specifying a `ConfigOverride` in the application manifest.</span></span>

<span data-ttu-id="8f89e-129">Suponha que você tenha a seguinte configuração no arquivo Config\Settings.xml para o serviço `Stateful1`:</span><span class="sxs-lookup"><span data-stu-id="8f89e-129">Suppose that you have the following setting in the Config\Settings.xml file for the `Stateful1` service:</span></span>

```xml
  <Section Name="MyConfigSection">
     <Parameter Name="MaxQueueSize" Value="25" />
  </Section>
```
<span data-ttu-id="8f89e-130">Para substituir esse valor por um par de aplicativo/ambiente específico, crie uma `ConfigOverride` ao importar o manifesto do serviço no manifesto do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="8f89e-130">To override this value for a specific application/environment pair, create a `ConfigOverride` when you import the service manifest in the application manifest.</span></span>

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
<span data-ttu-id="8f89e-131">Esse parâmetro pode então ser configurado pelo ambiente como mostrado acima.</span><span class="sxs-lookup"><span data-stu-id="8f89e-131">This parameter can then be configured by environment as shown above.</span></span> <span data-ttu-id="8f89e-132">Você pode fazer isso declarando-o na seção de parâmetros do manifesto do aplicativo e especificando valores específicos nos arquivos de parâmetro do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="8f89e-132">You can do this by declaring it in the parameters section of the application manifest and specifying environment-specific values in the application parameter files.</span></span>

> [!NOTE]
> <span data-ttu-id="8f89e-133">No caso de definições de configuração de serviço, há três locais onde o valor de uma chave pode ser definido: o pacote de configuração de serviço, o manifesto do aplicativo e o arquivo de parâmetro do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="8f89e-133">In the case of service configuration settings, there are three places where the value of a key can be set: the service configuration package, the application manifest, and the application parameter file.</span></span> <span data-ttu-id="8f89e-134">O Service Fabric sempre escolherá o arquivo de parâmetro de aplicativo primeiro (se especificado), o manifesto do aplicativo e, por fim, o pacote de configuração.</span><span class="sxs-lookup"><span data-stu-id="8f89e-134">Service Fabric will always choose from the application parameter file first (if specified), then the application manifest, and finally the configuration package.</span></span>
> 
> 

### <a name="setting-and-using-environment-variables"></a><span data-ttu-id="8f89e-135">Configurando e usando variáveis de ambiente</span><span class="sxs-lookup"><span data-stu-id="8f89e-135">Setting and using environment variables</span></span> 
<span data-ttu-id="8f89e-136">Você pode especificar e definir variáveis de ambiente no arquivo ServiceManifest.xml e, em seguida, substituí-las no arquivo ApplicationManifest.xml de acordo com a instância.</span><span class="sxs-lookup"><span data-stu-id="8f89e-136">You can specify and set environment variables in the ServiceManifest.xml file and then override these in the ApplicationManifest.xml file on a per instance basis.</span></span>
<span data-ttu-id="8f89e-137">O exemplo abaixo mostra duas variáveis de ambiente, uma com um valor definido e a outra é substituída.</span><span class="sxs-lookup"><span data-stu-id="8f89e-137">The example below shows two environment variables, one with a value set and the other is overridden.</span></span> <span data-ttu-id="8f89e-138">Você pode usar os parâmetros de aplicativo para definir valores de variáveis de ambiente da mesma forma que eles foram usados para substituições de configuração.</span><span class="sxs-lookup"><span data-stu-id="8f89e-138">You can use application parameters to set environment variables values in the same way that these were used for config overrides.</span></span>

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
<span data-ttu-id="8f89e-139">Para substituir as variáveis de ambiente no ApplicationManifest.xml, faça referência ao pacote de códigos no ServiceManifest com o elemento `EnvironmentOverrides`.</span><span class="sxs-lookup"><span data-stu-id="8f89e-139">To override the environment variables in the ApplicationManifest.xml, reference the code package in the ServiceManifest with the `EnvironmentOverrides` element.</span></span>

```xml
  <ServiceManifestImport>
    <ServiceManifestRef ServiceManifestName="FrontEndServicePkg" ServiceManifestVersion="1.0.0" />
    <EnvironmentOverrides CodePackageRef="MyCode">
      <EnvironmentVariable Name="MyEnvVariable" Value="mydata"/>
    </EnvironmentOverrides>
  </ServiceManifestImport>
 ``` 
 <span data-ttu-id="8f89e-140">Depois que a instância de serviço nomeada for criada, você poderá acessar as variáveis de ambiente no código.</span><span class="sxs-lookup"><span data-stu-id="8f89e-140">Once the named service instance is created you can access the environment variables from code.</span></span> <span data-ttu-id="8f89e-141">Por exemplo, em C#, você pode fazer o seguinte</span><span class="sxs-lookup"><span data-stu-id="8f89e-141">e.g. In C# you can do the following</span></span>

```csharp
    string EnvVariable = Environment.GetEnvironmentVariable("MyEnvVariable");
```

### <a name="service-fabric-environment-variables"></a><span data-ttu-id="8f89e-142">Variáveis de ambiente do Service Fabric</span><span class="sxs-lookup"><span data-stu-id="8f89e-142">Service Fabric environment variables</span></span>
<span data-ttu-id="8f89e-143">O Service Fabric tem variáveis de ambiente internas definidas para cada instância de serviço.</span><span class="sxs-lookup"><span data-stu-id="8f89e-143">Service Fabric has built in environment variables set for each service instance.</span></span> <span data-ttu-id="8f89e-144">A lista completa de variáveis de ambiente pode ser consultada logo abaixo. Os itens destacados em negrito são os que você utilizará em seu serviço; o restante será usado pelo tempo de execução do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="8f89e-144">The full list of environment variables is below, where the ones in bold are the ones that you will use in your service, the other being used by Service Fabric runtime.</span></span> 

* <span data-ttu-id="8f89e-145">Fabric_ApplicationHostId</span><span class="sxs-lookup"><span data-stu-id="8f89e-145">Fabric_ApplicationHostId</span></span>
* <span data-ttu-id="8f89e-146">Fabric_ApplicationHostType</span><span class="sxs-lookup"><span data-stu-id="8f89e-146">Fabric_ApplicationHostType</span></span>
* <span data-ttu-id="8f89e-147">Fabric_ApplicationId</span><span class="sxs-lookup"><span data-stu-id="8f89e-147">Fabric_ApplicationId</span></span>
* <span data-ttu-id="8f89e-148">**Fabric_ApplicationName**</span><span class="sxs-lookup"><span data-stu-id="8f89e-148">**Fabric_ApplicationName**</span></span>
* <span data-ttu-id="8f89e-149">Fabric_CodePackageInstanceId</span><span class="sxs-lookup"><span data-stu-id="8f89e-149">Fabric_CodePackageInstanceId</span></span>
* <span data-ttu-id="8f89e-150">**Fabric_CodePackageName**</span><span class="sxs-lookup"><span data-stu-id="8f89e-150">**Fabric_CodePackageName**</span></span>
* <span data-ttu-id="8f89e-151">**Fabric_Endpoint_[YourServiceName]TypeEndpoint**</span><span class="sxs-lookup"><span data-stu-id="8f89e-151">**Fabric_Endpoint_[YourServiceName]TypeEndpoint**</span></span>
* <span data-ttu-id="8f89e-152">**Fabric_Folder_App_Log**</span><span class="sxs-lookup"><span data-stu-id="8f89e-152">**Fabric_Folder_App_Log**</span></span>
* <span data-ttu-id="8f89e-153">**Fabric_Folder_App_Temp**</span><span class="sxs-lookup"><span data-stu-id="8f89e-153">**Fabric_Folder_App_Temp**</span></span>
* <span data-ttu-id="8f89e-154">**Fabric_Folder_App_Work**</span><span class="sxs-lookup"><span data-stu-id="8f89e-154">**Fabric_Folder_App_Work**</span></span>
* <span data-ttu-id="8f89e-155">**Fabric_Folder_Application**</span><span class="sxs-lookup"><span data-stu-id="8f89e-155">**Fabric_Folder_Application**</span></span>
* <span data-ttu-id="8f89e-156">Fabric_NodeId</span><span class="sxs-lookup"><span data-stu-id="8f89e-156">Fabric_NodeId</span></span>
* <span data-ttu-id="8f89e-157">**Fabric_NodeIPOrFQDN**</span><span class="sxs-lookup"><span data-stu-id="8f89e-157">**Fabric_NodeIPOrFQDN**</span></span>
* <span data-ttu-id="8f89e-158">**Fabric_NodeName**</span><span class="sxs-lookup"><span data-stu-id="8f89e-158">**Fabric_NodeName**</span></span>
* <span data-ttu-id="8f89e-159">Fabric_RuntimeConnectionAddress</span><span class="sxs-lookup"><span data-stu-id="8f89e-159">Fabric_RuntimeConnectionAddress</span></span>
* <span data-ttu-id="8f89e-160">Fabric_ServicePackageInstanceId</span><span class="sxs-lookup"><span data-stu-id="8f89e-160">Fabric_ServicePackageInstanceId</span></span>
* <span data-ttu-id="8f89e-161">Fabric_ServicePackageName</span><span class="sxs-lookup"><span data-stu-id="8f89e-161">Fabric_ServicePackageName</span></span>
* <span data-ttu-id="8f89e-162">Fabric_ServicePackageVersionInstance</span><span class="sxs-lookup"><span data-stu-id="8f89e-162">Fabric_ServicePackageVersionInstance</span></span>
* <span data-ttu-id="8f89e-163">FabricPackageFileName</span><span class="sxs-lookup"><span data-stu-id="8f89e-163">FabricPackageFileName</span></span>

<span data-ttu-id="8f89e-164">O código abaixo mostra como listar as variáveis de ambiente do Service Fabric</span><span class="sxs-lookup"><span data-stu-id="8f89e-164">The code belows shows how to list the Service Fabric environment variables</span></span>
 ```csharp
    foreach (DictionaryEntry de in Environment.GetEnvironmentVariables())
    {
        if (de.Key.ToString().StartsWith("Fabric"))
        {
            Console.WriteLine(" Environment variable {0} = {1}", de.Key, de.Value);
        }
    }
```
<span data-ttu-id="8f89e-165">Veja abaixo exemplos de variáveis de ambiente para um tipo de aplicativo chamado `GuestExe.Application` com um tipo de serviço chamado `FrontEndService` quando executado no computador de desenvolvimento local.</span><span class="sxs-lookup"><span data-stu-id="8f89e-165">The following are examples of environment variables for an application type called `GuestExe.Application` with a service type called `FrontEndService` when run on your local dev machine.</span></span>

* <span data-ttu-id="8f89e-166">**Fabric_ApplicationName = fabric:/GuestExe.Application**</span><span class="sxs-lookup"><span data-stu-id="8f89e-166">**Fabric_ApplicationName = fabric:/GuestExe.Application**</span></span>
* <span data-ttu-id="8f89e-167">**Fabric_CodePackageName = Code**</span><span class="sxs-lookup"><span data-stu-id="8f89e-167">**Fabric_CodePackageName = Code**</span></span>
* <span data-ttu-id="8f89e-168">**Fabric_Endpoint_FrontEndServiceTypeEndpoint = 80**</span><span class="sxs-lookup"><span data-stu-id="8f89e-168">**Fabric_Endpoint_FrontEndServiceTypeEndpoint = 80**</span></span>
* <span data-ttu-id="8f89e-169">**Fabric_NodeIPOrFQDN = localhost**</span><span class="sxs-lookup"><span data-stu-id="8f89e-169">**Fabric_NodeIPOrFQDN = localhost**</span></span>
* <span data-ttu-id="8f89e-170">**Fabric_NodeName = _Node_2**</span><span class="sxs-lookup"><span data-stu-id="8f89e-170">**Fabric_NodeName = _Node_2**</span></span>

### <a name="application-parameter-files"></a><span data-ttu-id="8f89e-171">Arquivos de parâmetros de aplicativo</span><span class="sxs-lookup"><span data-stu-id="8f89e-171">Application parameter files</span></span>
<span data-ttu-id="8f89e-172">O projeto de aplicativo do Service Fabric pode incluir um ou mais arquivos de parâmetro de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="8f89e-172">The Service Fabric application project can include one or more application parameter files.</span></span> <span data-ttu-id="8f89e-173">Cada um deles define os valores específicos para os parâmetros definidos no manifesto do aplicativo:</span><span class="sxs-lookup"><span data-stu-id="8f89e-173">Each of them defines the specific values for the parameters that are defined in the application manifest:</span></span>

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
<span data-ttu-id="8f89e-174">Por padrão, um novo aplicativo inclui três arquivos de parâmetro de aplicativo, chamados Local.1Node.xml, Local.5Node.xml e Cloud.xml:</span><span class="sxs-lookup"><span data-stu-id="8f89e-174">By default, a new application includes three application parameter files, named Local.1Node.xml, Local.5Node.xml, and Cloud.xml:</span></span>

![Arquivos de parâmetros de aplicativo no Gerenciador de Soluções][app-parameters-solution-explorer]

<span data-ttu-id="8f89e-176">Para criar um arquivo de parâmetro, basta copiar e colar um existente e fornecer um novo nome a ele.</span><span class="sxs-lookup"><span data-stu-id="8f89e-176">To create a parameter file, simply copy and paste an existing one and give it a new name.</span></span>

## <a name="identifying-environment-specific-parameters-during-deployment"></a><span data-ttu-id="8f89e-177">Identificando parâmetros específicos do ambiente durante a implantação</span><span class="sxs-lookup"><span data-stu-id="8f89e-177">Identifying environment-specific parameters during deployment</span></span>
<span data-ttu-id="8f89e-178">No momento da implantação, você precisa escolher o arquivo de parâmetro adequado para aplicar ao seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="8f89e-178">At deployment time, you need to choose the appropriate parameter file to apply with your application.</span></span> <span data-ttu-id="8f89e-179">Você pode fazer isso por meio da caixa de diálogo Publicar no Visual Studio ou por meio do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="8f89e-179">You can do this through the Publish dialog in Visual Studio or through PowerShell.</span></span>

### <a name="deploy-from-visual-studio"></a><span data-ttu-id="8f89e-180">Implantar com o Visual Studio</span><span class="sxs-lookup"><span data-stu-id="8f89e-180">Deploy from Visual Studio</span></span>
<span data-ttu-id="8f89e-181">Você pode escolher na lista de arquivos de parâmetro disponíveis ao publicar seu aplicativo no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="8f89e-181">You can choose from the list of available parameter files when you publish your application in Visual Studio.</span></span>

![Escolher um arquivo de parâmetro na caixa de diálogo Publicar][publishdialog]

### <a name="deploy-from-powershell"></a><span data-ttu-id="8f89e-183">Implantar do PowerShell</span><span class="sxs-lookup"><span data-stu-id="8f89e-183">Deploy from PowerShell</span></span>
<span data-ttu-id="8f89e-184">O script `Deploy-FabricApplication.ps1` do PowerShell incluído no modelo de projeto de aplicativo aceita um perfil de publicação como parâmetro, e o PublishProfile contém uma referência para o arquivo de parâmetros do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="8f89e-184">The `Deploy-FabricApplication.ps1` PowerShell script included in the application project template accepts a publish profile as a parameter and the PublishProfile contains a reference to the application parameters file.</span></span>

  ```PowerShell
    ./Deploy-FabricApplication -ApplicationPackagePath <app_package_path> -PublishProfileFile <publishprofile_path>
  ```

## <a name="next-steps"></a><span data-ttu-id="8f89e-185">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="8f89e-185">Next steps</span></span>
<span data-ttu-id="8f89e-186">Para saber mais sobre alguns dos principais conceitos discutidos neste tópico, confira a [visão geral técnica do Service Fabric](service-fabric-technical-overview.md).</span><span class="sxs-lookup"><span data-stu-id="8f89e-186">To learn more about some of the core concepts that are discussed in this topic, see the [Service Fabric technical overview](service-fabric-technical-overview.md).</span></span> <span data-ttu-id="8f89e-187">Para obter informações sobre outras funcionalidades de gerenciamento de aplicativo disponíveis no Visual Studio, confira [Gerenciar seus aplicativos do Service Fabric no Visual Studio](service-fabric-manage-application-in-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="8f89e-187">For information about other app management capabilities that are available in Visual Studio, see [Manage your Service Fabric applications in Visual Studio](service-fabric-manage-application-in-visual-studio.md).</span></span>

<!-- Image references -->

[publishdialog]: ./media/service-fabric-manage-multiple-environment-app-configuration/publish-dialog-choose-app-config.png
[app-parameters-solution-explorer]:./media/service-fabric-manage-multiple-environment-app-configuration/app-parameters-in-solution-explorer.png
