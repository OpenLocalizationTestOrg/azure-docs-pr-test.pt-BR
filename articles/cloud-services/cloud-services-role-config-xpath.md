---
title: "Folha de consulta do XPath da configuração da Função dos Serviços de Nuvem | Microsoft Docs"
description: "As várias configurações do XPath que podem ser usadas na configuração da função do serviço de nuvem para expor as configurações como uma variável de ambiente."
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: c51e4493-0643-4d05-bc44-06c76bcbf7d1
ms.service: cloud-services
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/19/2017
ms.author: adegeo
ms.openlocfilehash: fd6efac829d3fd9e2840362b8d2ff423add566d9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="expose-role-configuration-settings-as-an-environment-variable-with-xpath"></a><span data-ttu-id="535a2-103">Expor as definições de configuração da função como uma variável de ambiente com o XPath</span><span class="sxs-lookup"><span data-stu-id="535a2-103">Expose role configuration settings as an environment variable with XPath</span></span>
<span data-ttu-id="535a2-104">No arquivo de definição de serviço de função web ou do trabalho do serviço de nuvem, é possível expor os valores de configuração do tempo de execução como variáveis de ambiente.</span><span class="sxs-lookup"><span data-stu-id="535a2-104">In the cloud service worker or web role service definition file, you can expose runtime configuration values as environment variables.</span></span> <span data-ttu-id="535a2-105">Há suporte para os valores do XPath a seguir (que correspondem aos valores da API).</span><span class="sxs-lookup"><span data-stu-id="535a2-105">The following XPath values are supported (which correspond to API values).</span></span>

<span data-ttu-id="535a2-106">Esses valores do XPath também estão disponíveis por meio da biblioteca [Microsoft.WindowsAzure.ServiceRuntime](https://msdn.microsoft.com/library/microsoft.windowsazure.serviceruntime.roleenvironment.aspx) .</span><span class="sxs-lookup"><span data-stu-id="535a2-106">These XPath values are also available through the [Microsoft.WindowsAzure.ServiceRuntime](https://msdn.microsoft.com/library/microsoft.windowsazure.serviceruntime.roleenvironment.aspx) library.</span></span> 

## <a name="app-running-in-emulator"></a><span data-ttu-id="535a2-107">Aplicativo em execução no emulador</span><span class="sxs-lookup"><span data-stu-id="535a2-107">App running in emulator</span></span>
<span data-ttu-id="535a2-108">Indica que o aplicativo está em execução no emulador.</span><span class="sxs-lookup"><span data-stu-id="535a2-108">Indicates that the app is running in the emulator.</span></span>

| <span data-ttu-id="535a2-109">Tipo</span><span class="sxs-lookup"><span data-stu-id="535a2-109">Type</span></span> | <span data-ttu-id="535a2-110">Exemplo</span><span class="sxs-lookup"><span data-stu-id="535a2-110">Example</span></span> |
| --- | --- |
| <span data-ttu-id="535a2-111">XPath</span><span class="sxs-lookup"><span data-stu-id="535a2-111">XPath</span></span> |<span data-ttu-id="535a2-112">xpath="/RoleEnvironment/Deployment/@emulated"</span><span class="sxs-lookup"><span data-stu-id="535a2-112">xpath="/RoleEnvironment/Deployment/@emulated"</span></span> |
| <span data-ttu-id="535a2-113">Código</span><span class="sxs-lookup"><span data-stu-id="535a2-113">Code</span></span> |<span data-ttu-id="535a2-114">var x = RoleEnvironment.IsEmulated;</span><span class="sxs-lookup"><span data-stu-id="535a2-114">var x = RoleEnvironment.IsEmulated;</span></span> |

## <a name="deployment-id"></a><span data-ttu-id="535a2-115">ID de Implantação</span><span class="sxs-lookup"><span data-stu-id="535a2-115">Deployment ID</span></span>
<span data-ttu-id="535a2-116">Recupera a ID de implantação da instância.</span><span class="sxs-lookup"><span data-stu-id="535a2-116">Retrieves the deployment ID for the instance.</span></span>

| <span data-ttu-id="535a2-117">Tipo</span><span class="sxs-lookup"><span data-stu-id="535a2-117">Type</span></span> | <span data-ttu-id="535a2-118">Exemplo</span><span class="sxs-lookup"><span data-stu-id="535a2-118">Example</span></span> |
| --- | --- |
| <span data-ttu-id="535a2-119">XPath</span><span class="sxs-lookup"><span data-stu-id="535a2-119">XPath</span></span> |<span data-ttu-id="535a2-120">xpath="/RoleEnvironment/Deployment/@id"</span><span class="sxs-lookup"><span data-stu-id="535a2-120">xpath="/RoleEnvironment/Deployment/@id"</span></span> |
| <span data-ttu-id="535a2-121">Código</span><span class="sxs-lookup"><span data-stu-id="535a2-121">Code</span></span> |<span data-ttu-id="535a2-122">var deploymentId = RoleEnvironment.DeploymentId;</span><span class="sxs-lookup"><span data-stu-id="535a2-122">var deploymentId = RoleEnvironment.DeploymentId;</span></span> |

## <a name="role-id"></a><span data-ttu-id="535a2-123">ID de Função</span><span class="sxs-lookup"><span data-stu-id="535a2-123">Role ID</span></span>
<span data-ttu-id="535a2-124">Recupera a ID de função atual da instância.</span><span class="sxs-lookup"><span data-stu-id="535a2-124">Retrieves the current role ID for the instance.</span></span>

| <span data-ttu-id="535a2-125">Tipo</span><span class="sxs-lookup"><span data-stu-id="535a2-125">Type</span></span> | <span data-ttu-id="535a2-126">Exemplo</span><span class="sxs-lookup"><span data-stu-id="535a2-126">Example</span></span> |
| --- | --- |
| <span data-ttu-id="535a2-127">XPath</span><span class="sxs-lookup"><span data-stu-id="535a2-127">XPath</span></span> |<span data-ttu-id="535a2-128">xpath="/RoleEnvironment/CurrentInstance/@id"</span><span class="sxs-lookup"><span data-stu-id="535a2-128">xpath="/RoleEnvironment/CurrentInstance/@id"</span></span> |
| <span data-ttu-id="535a2-129">Código</span><span class="sxs-lookup"><span data-stu-id="535a2-129">Code</span></span> |<span data-ttu-id="535a2-130">var id = RoleEnvironment.CurrentRoleInstance.Id;</span><span class="sxs-lookup"><span data-stu-id="535a2-130">var id = RoleEnvironment.CurrentRoleInstance.Id;</span></span> |

## <a name="update-domain"></a><span data-ttu-id="535a2-131">Domínio de atualização</span><span class="sxs-lookup"><span data-stu-id="535a2-131">Update domain</span></span>
<span data-ttu-id="535a2-132">Recupera o domínio de atualização da instância.</span><span class="sxs-lookup"><span data-stu-id="535a2-132">Retrieves the update domain of the instance.</span></span>

| <span data-ttu-id="535a2-133">Tipo</span><span class="sxs-lookup"><span data-stu-id="535a2-133">Type</span></span> | <span data-ttu-id="535a2-134">Exemplo</span><span class="sxs-lookup"><span data-stu-id="535a2-134">Example</span></span> |
| --- | --- |
| <span data-ttu-id="535a2-135">XPath</span><span class="sxs-lookup"><span data-stu-id="535a2-135">XPath</span></span> |<span data-ttu-id="535a2-136">xpath="/RoleEnvironment/CurrentInstance/@updateDomain"</span><span class="sxs-lookup"><span data-stu-id="535a2-136">xpath="/RoleEnvironment/CurrentInstance/@updateDomain"</span></span> |
| <span data-ttu-id="535a2-137">Código</span><span class="sxs-lookup"><span data-stu-id="535a2-137">Code</span></span> |<span data-ttu-id="535a2-138">var ud = RoleEnvironment.CurrentRoleInstance.UpdateDomain;</span><span class="sxs-lookup"><span data-stu-id="535a2-138">var ud = RoleEnvironment.CurrentRoleInstance.UpdateDomain;</span></span> |

## <a name="fault-domain"></a><span data-ttu-id="535a2-139">Domínios de falha</span><span class="sxs-lookup"><span data-stu-id="535a2-139">Fault domain</span></span>
<span data-ttu-id="535a2-140">Recupera o domínio de falha da instância.</span><span class="sxs-lookup"><span data-stu-id="535a2-140">Retrieves the fault domain of the instance.</span></span>

| <span data-ttu-id="535a2-141">Tipo</span><span class="sxs-lookup"><span data-stu-id="535a2-141">Type</span></span> | <span data-ttu-id="535a2-142">Exemplo</span><span class="sxs-lookup"><span data-stu-id="535a2-142">Example</span></span> |
| --- | --- |
| <span data-ttu-id="535a2-143">XPath</span><span class="sxs-lookup"><span data-stu-id="535a2-143">XPath</span></span> |<span data-ttu-id="535a2-144">xpath="/RoleEnvironment/CurrentInstance/@faultDomain"</span><span class="sxs-lookup"><span data-stu-id="535a2-144">xpath="/RoleEnvironment/CurrentInstance/@faultDomain"</span></span> |
| <span data-ttu-id="535a2-145">Código</span><span class="sxs-lookup"><span data-stu-id="535a2-145">Code</span></span> |<span data-ttu-id="535a2-146">var fd = RoleEnvironment.CurrentRoleInstance.FaultDomain;</span><span class="sxs-lookup"><span data-stu-id="535a2-146">var fd = RoleEnvironment.CurrentRoleInstance.FaultDomain;</span></span> |

## <a name="role-name"></a><span data-ttu-id="535a2-147">Nome da função</span><span class="sxs-lookup"><span data-stu-id="535a2-147">Role name</span></span>
<span data-ttu-id="535a2-148">Recupera o nome da função das instâncias.</span><span class="sxs-lookup"><span data-stu-id="535a2-148">Retrieves the role name of the instances.</span></span>

| <span data-ttu-id="535a2-149">Tipo</span><span class="sxs-lookup"><span data-stu-id="535a2-149">Type</span></span> | <span data-ttu-id="535a2-150">Exemplo</span><span class="sxs-lookup"><span data-stu-id="535a2-150">Example</span></span> |
| --- | --- |
| <span data-ttu-id="535a2-151">XPath</span><span class="sxs-lookup"><span data-stu-id="535a2-151">XPath</span></span> |<span data-ttu-id="535a2-152">xpath="/RoleEnvironment/CurrentInstance/@roleName"</span><span class="sxs-lookup"><span data-stu-id="535a2-152">xpath="/RoleEnvironment/CurrentInstance/@roleName"</span></span> |
| <span data-ttu-id="535a2-153">Código</span><span class="sxs-lookup"><span data-stu-id="535a2-153">Code</span></span> |<span data-ttu-id="535a2-154">var rname = RoleEnvironment.CurrentRoleInstance.Role.Name;</span><span class="sxs-lookup"><span data-stu-id="535a2-154">var rname = RoleEnvironment.CurrentRoleInstance.Role.Name;</span></span> |

## <a name="config-setting"></a><span data-ttu-id="535a2-155">Definição de configuração</span><span class="sxs-lookup"><span data-stu-id="535a2-155">Config setting</span></span>
<span data-ttu-id="535a2-156">Recupera o valor da definição de configuração especificada.</span><span class="sxs-lookup"><span data-stu-id="535a2-156">Retrieves the value of the specified configuration setting.</span></span>

| <span data-ttu-id="535a2-157">Tipo</span><span class="sxs-lookup"><span data-stu-id="535a2-157">Type</span></span> | <span data-ttu-id="535a2-158">Exemplo</span><span class="sxs-lookup"><span data-stu-id="535a2-158">Example</span></span> |
| --- | --- |
| <span data-ttu-id="535a2-159">XPath</span><span class="sxs-lookup"><span data-stu-id="535a2-159">XPath</span></span> |<span data-ttu-id="535a2-160">xpath="/RoleEnvironment/CurrentInstance/ConfigurationSettings/ConfigurationSetting[@name='Setting1']/@value"</span><span class="sxs-lookup"><span data-stu-id="535a2-160">xpath="/RoleEnvironment/CurrentInstance/ConfigurationSettings/ConfigurationSetting[@name='Setting1']/@value"</span></span> |
| <span data-ttu-id="535a2-161">Código</span><span class="sxs-lookup"><span data-stu-id="535a2-161">Code</span></span> |<span data-ttu-id="535a2-162">var setting = RoleEnvironment.GetConfigurationSettingValue("Setting1");</span><span class="sxs-lookup"><span data-stu-id="535a2-162">var setting = RoleEnvironment.GetConfigurationSettingValue("Setting1");</span></span> |

## <a name="local-storage-path"></a><span data-ttu-id="535a2-163">Caminho do armazenamento local</span><span class="sxs-lookup"><span data-stu-id="535a2-163">Local storage path</span></span>
<span data-ttu-id="535a2-164">Recupera o caminho do armazenamento local da instância.</span><span class="sxs-lookup"><span data-stu-id="535a2-164">Retrieves the local storage path for the instance.</span></span>

| <span data-ttu-id="535a2-165">Tipo</span><span class="sxs-lookup"><span data-stu-id="535a2-165">Type</span></span> | <span data-ttu-id="535a2-166">Exemplo</span><span class="sxs-lookup"><span data-stu-id="535a2-166">Example</span></span> |
| --- | --- |
| <span data-ttu-id="535a2-167">XPath</span><span class="sxs-lookup"><span data-stu-id="535a2-167">XPath</span></span> |<span data-ttu-id="535a2-168">xpath="/RoleEnvironment/CurrentInstance/LocalResources/LocalResource[@name='LocalStore1']/@path"</span><span class="sxs-lookup"><span data-stu-id="535a2-168">xpath="/RoleEnvironment/CurrentInstance/LocalResources/LocalResource[@name='LocalStore1']/@path"</span></span> |
| <span data-ttu-id="535a2-169">Código</span><span class="sxs-lookup"><span data-stu-id="535a2-169">Code</span></span> |<span data-ttu-id="535a2-170">var localResourcePath = RoleEnvironment.GetLocalResource("LocalStore1").RootPath;</span><span class="sxs-lookup"><span data-stu-id="535a2-170">var localResourcePath = RoleEnvironment.GetLocalResource("LocalStore1").RootPath;</span></span> |

## <a name="local-storage-size"></a><span data-ttu-id="535a2-171">Tamanho do armazenamento local</span><span class="sxs-lookup"><span data-stu-id="535a2-171">Local storage size</span></span>
<span data-ttu-id="535a2-172">Recupera o tamanho do armazenamento local da instância.</span><span class="sxs-lookup"><span data-stu-id="535a2-172">Retrieves the size of the local storage for the instance.</span></span>

| <span data-ttu-id="535a2-173">Tipo</span><span class="sxs-lookup"><span data-stu-id="535a2-173">Type</span></span> | <span data-ttu-id="535a2-174">Exemplo</span><span class="sxs-lookup"><span data-stu-id="535a2-174">Example</span></span> |
| --- | --- |
| <span data-ttu-id="535a2-175">XPath</span><span class="sxs-lookup"><span data-stu-id="535a2-175">XPath</span></span> |<span data-ttu-id="535a2-176">xpath="/RoleEnvironment/CurrentInstance/LocalResources/LocalResource[@name='LocalStore1']/@sizeInMB"</span><span class="sxs-lookup"><span data-stu-id="535a2-176">xpath="/RoleEnvironment/CurrentInstance/LocalResources/LocalResource[@name='LocalStore1']/@sizeInMB"</span></span> |
| <span data-ttu-id="535a2-177">Código</span><span class="sxs-lookup"><span data-stu-id="535a2-177">Code</span></span> |<span data-ttu-id="535a2-178">var localResourceSizeInMB = RoleEnvironment.GetLocalResource("LocalStore1").MaximumSizeInMegabytes;</span><span class="sxs-lookup"><span data-stu-id="535a2-178">var localResourceSizeInMB = RoleEnvironment.GetLocalResource("LocalStore1").MaximumSizeInMegabytes;</span></span> |

## <a name="endpoint-protocol"></a><span data-ttu-id="535a2-179">Protocolo do ponto de extremidade</span><span class="sxs-lookup"><span data-stu-id="535a2-179">Endpoint protocol</span></span>
<span data-ttu-id="535a2-180">Recupera o protocolo do ponto de extremidade da instância.</span><span class="sxs-lookup"><span data-stu-id="535a2-180">Retrieves the endpoint protocol for the instance.</span></span>

| <span data-ttu-id="535a2-181">Tipo</span><span class="sxs-lookup"><span data-stu-id="535a2-181">Type</span></span> | <span data-ttu-id="535a2-182">Exemplo</span><span class="sxs-lookup"><span data-stu-id="535a2-182">Example</span></span> |
| --- | --- |
| <span data-ttu-id="535a2-183">XPath</span><span class="sxs-lookup"><span data-stu-id="535a2-183">XPath</span></span> |<span data-ttu-id="535a2-184">xpath="/RoleEnvironment/CurrentInstance/Endpoints/Endpoint[@name='Endpoint1']/@protocol"</span><span class="sxs-lookup"><span data-stu-id="535a2-184">xpath="/RoleEnvironment/CurrentInstance/Endpoints/Endpoint[@name='Endpoint1']/@protocol"</span></span> |
| <span data-ttu-id="535a2-185">Código</span><span class="sxs-lookup"><span data-stu-id="535a2-185">Code</span></span> |<span data-ttu-id="535a2-186">var prot = RoleEnvironment.CurrentRoleInstance.InstanceEndpoints["Endpoint1"].Protocol;</span><span class="sxs-lookup"><span data-stu-id="535a2-186">var prot = RoleEnvironment.CurrentRoleInstance.InstanceEndpoints["Endpoint1"].Protocol;</span></span> |

## <a name="endpoint-ip"></a><span data-ttu-id="535a2-187">IP do ponto de extremidade</span><span class="sxs-lookup"><span data-stu-id="535a2-187">Endpoint IP</span></span>
<span data-ttu-id="535a2-188">Obtém o endereço IP do ponto de extremidade especificado.</span><span class="sxs-lookup"><span data-stu-id="535a2-188">Gets the specified endpoint's IP address.</span></span>

| <span data-ttu-id="535a2-189">Tipo</span><span class="sxs-lookup"><span data-stu-id="535a2-189">Type</span></span> | <span data-ttu-id="535a2-190">Exemplo</span><span class="sxs-lookup"><span data-stu-id="535a2-190">Example</span></span> |
| --- | --- |
| <span data-ttu-id="535a2-191">XPath</span><span class="sxs-lookup"><span data-stu-id="535a2-191">XPath</span></span> |<span data-ttu-id="535a2-192">xpath="/RoleEnvironment/CurrentInstance/Endpoints/Endpoint[@name='Endpoint1']/@address"</span><span class="sxs-lookup"><span data-stu-id="535a2-192">xpath="/RoleEnvironment/CurrentInstance/Endpoints/Endpoint[@name='Endpoint1']/@address"</span></span> |
| <span data-ttu-id="535a2-193">Código</span><span class="sxs-lookup"><span data-stu-id="535a2-193">Code</span></span> |<span data-ttu-id="535a2-194">var address = RoleEnvironment.CurrentRoleInstance.InstanceEndpoints["Endpoint1"].IPEndpoint.Address</span><span class="sxs-lookup"><span data-stu-id="535a2-194">var address = RoleEnvironment.CurrentRoleInstance.InstanceEndpoints["Endpoint1"].IPEndpoint.Address</span></span> |

## <a name="endpoint-port"></a><span data-ttu-id="535a2-195">Porta do ponto de extremidade</span><span class="sxs-lookup"><span data-stu-id="535a2-195">Endpoint port</span></span>
<span data-ttu-id="535a2-196">Recupera a porta do ponto de extremidade da instância.</span><span class="sxs-lookup"><span data-stu-id="535a2-196">Retrieves the endpoint port for the instance.</span></span>

| <span data-ttu-id="535a2-197">Tipo</span><span class="sxs-lookup"><span data-stu-id="535a2-197">Type</span></span> | <span data-ttu-id="535a2-198">Exemplo</span><span class="sxs-lookup"><span data-stu-id="535a2-198">Example</span></span> |
| --- | --- |
| <span data-ttu-id="535a2-199">XPath</span><span class="sxs-lookup"><span data-stu-id="535a2-199">XPath</span></span> |<span data-ttu-id="535a2-200">xpath="/RoleEnvironment/CurrentInstance/Endpoints/Endpoint[@name='Endpoint1']/@port"</span><span class="sxs-lookup"><span data-stu-id="535a2-200">xpath="/RoleEnvironment/CurrentInstance/Endpoints/Endpoint[@name='Endpoint1']/@port"</span></span> |
| <span data-ttu-id="535a2-201">Código</span><span class="sxs-lookup"><span data-stu-id="535a2-201">Code</span></span> |<span data-ttu-id="535a2-202">var port = RoleEnvironment.CurrentRoleInstance.InstanceEndpoints["Endpoint1"].IPEndpoint.Port;</span><span class="sxs-lookup"><span data-stu-id="535a2-202">var port = RoleEnvironment.CurrentRoleInstance.InstanceEndpoints["Endpoint1"].IPEndpoint.Port;</span></span> |

## <a name="example"></a><span data-ttu-id="535a2-203">Exemplo</span><span class="sxs-lookup"><span data-stu-id="535a2-203">Example</span></span>
<span data-ttu-id="535a2-204">Aqui está um exemplo de uma função de trabalho que cria uma tarefa de inicialização com uma variável de ambiente chamada `TestIsEmulated` definida como o [valor @emulated xpath](#app-running-in-emulator).</span><span class="sxs-lookup"><span data-stu-id="535a2-204">Here is an example of a worker role that creates a startup task with an environment variable named `TestIsEmulated` set to the [@emulated xpath value](#app-running-in-emulator).</span></span> 

```xml
<WorkerRole name="Role1">
    <ConfigurationSettings>
      <Setting name="Setting1" />
    </ConfigurationSettings>
    <LocalResources>
      <LocalStorage name="LocalStore1" sizeInMB="1024"/>
    </LocalResources>
    <Endpoints>
      <InternalEndpoint name="Endpoint1" protocol="tcp" />
    </Endpoints>
    <Startup>
      <Task commandLine="example.cmd inputParm">
        <Environment>
          <Variable name="TestConstant" value="Constant"/>
          <Variable name="TestEmptyValue" value=""/>
          <Variable name="TestIsEmulated">
            <RoleInstanceValue xpath="/RoleEnvironment/Deployment/@emulated"/>
          </Variable>
          ...
        </Environment>
      </Task>
    </Startup>
    <Runtime>
      <Environment>
        <Variable name="TestConstant" value="Constant"/>
        <Variable name="TestEmptyValue" value=""/>
        <Variable name="TestIsEmulated">
          <RoleInstanceValue xpath="/RoleEnvironment/Deployment/@emulated"/>
        </Variable>
        ...
      </Environment>
    </Runtime>
    ...
</WorkerRole>
```

## <a name="next-steps"></a><span data-ttu-id="535a2-205">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="535a2-205">Next steps</span></span>
<span data-ttu-id="535a2-206">Saiba mais sobre o arquivo [ServiceConfiguration.cscfg](cloud-services-model-and-package.md#serviceconfigurationcscfg) .</span><span class="sxs-lookup"><span data-stu-id="535a2-206">Learn more about the [ServiceConfiguration.cscfg](cloud-services-model-and-package.md#serviceconfigurationcscfg) file.</span></span>

<span data-ttu-id="535a2-207">Crie um pacote [ServicePackage.cspkg](cloud-services-model-and-package.md#servicepackagecspkg) .</span><span class="sxs-lookup"><span data-stu-id="535a2-207">Create a [ServicePackage.cspkg](cloud-services-model-and-package.md#servicepackagecspkg) package.</span></span>

<span data-ttu-id="535a2-208">Habilite a [área de trabalho remota](cloud-services-role-enable-remote-desktop.md) para uma função.</span><span class="sxs-lookup"><span data-stu-id="535a2-208">Enable [remote desktop](cloud-services-role-enable-remote-desktop.md) for a role.</span></span>

