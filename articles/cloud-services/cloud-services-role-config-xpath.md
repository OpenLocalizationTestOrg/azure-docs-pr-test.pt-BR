---
title: "roteiro do aaaCloud serviços de função config XPath | Microsoft Docs"
description: "Olá várias configurações de XPath, que você poderá usar as configurações de tooexpose de configuração de função serviço de nuvem hello como uma variável de ambiente."
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
ms.openlocfilehash: 27f98f956a1c790c9bb30f9fefe1ab1736b2b150
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="expose-role-configuration-settings-as-an-environment-variable-with-xpath"></a><span data-ttu-id="d6f4a-103">Expor as definições de configuração da função como uma variável de ambiente com o XPath</span><span class="sxs-lookup"><span data-stu-id="d6f4a-103">Expose role configuration settings as an environment variable with XPath</span></span>
<span data-ttu-id="d6f4a-104">No trabalho de serviço de nuvem hello ou arquivo de definição de serviço de função da web, você pode expor os valores de configuração de tempo de execução como variáveis de ambiente.</span><span class="sxs-lookup"><span data-stu-id="d6f4a-104">In hello cloud service worker or web role service definition file, you can expose runtime configuration values as environment variables.</span></span> <span data-ttu-id="d6f4a-105">Olá valores de XPath a seguir têm suporte (que correspondem a valores de tooAPI).</span><span class="sxs-lookup"><span data-stu-id="d6f4a-105">hello following XPath values are supported (which correspond tooAPI values).</span></span>

<span data-ttu-id="d6f4a-106">Esses valores de XPath também estão disponíveis por meio de saudação [Microsoft.WindowsAzure.ServiceRuntime](https://msdn.microsoft.com/library/microsoft.windowsazure.serviceruntime.roleenvironment.aspx) biblioteca.</span><span class="sxs-lookup"><span data-stu-id="d6f4a-106">These XPath values are also available through hello [Microsoft.WindowsAzure.ServiceRuntime](https://msdn.microsoft.com/library/microsoft.windowsazure.serviceruntime.roleenvironment.aspx) library.</span></span> 

## <a name="app-running-in-emulator"></a><span data-ttu-id="d6f4a-107">Aplicativo em execução no emulador</span><span class="sxs-lookup"><span data-stu-id="d6f4a-107">App running in emulator</span></span>
<span data-ttu-id="d6f4a-108">Indica que o aplicativo hello está sendo executado no emulador de saudação.</span><span class="sxs-lookup"><span data-stu-id="d6f4a-108">Indicates that hello app is running in hello emulator.</span></span>

| <span data-ttu-id="d6f4a-109">Tipo</span><span class="sxs-lookup"><span data-stu-id="d6f4a-109">Type</span></span> | <span data-ttu-id="d6f4a-110">Exemplo</span><span class="sxs-lookup"><span data-stu-id="d6f4a-110">Example</span></span> |
| --- | --- |
| <span data-ttu-id="d6f4a-111">XPath</span><span class="sxs-lookup"><span data-stu-id="d6f4a-111">XPath</span></span> |<span data-ttu-id="d6f4a-112">xpath="/RoleEnvironment/Deployment/@emulated"</span><span class="sxs-lookup"><span data-stu-id="d6f4a-112">xpath="/RoleEnvironment/Deployment/@emulated"</span></span> |
| <span data-ttu-id="d6f4a-113">Código</span><span class="sxs-lookup"><span data-stu-id="d6f4a-113">Code</span></span> |<span data-ttu-id="d6f4a-114">var x = RoleEnvironment.IsEmulated;</span><span class="sxs-lookup"><span data-stu-id="d6f4a-114">var x = RoleEnvironment.IsEmulated;</span></span> |

## <a name="deployment-id"></a><span data-ttu-id="d6f4a-115">ID de Implantação</span><span class="sxs-lookup"><span data-stu-id="d6f4a-115">Deployment ID</span></span>
<span data-ttu-id="d6f4a-116">Recupera a ID de implantação de saudação para instância de saudação.</span><span class="sxs-lookup"><span data-stu-id="d6f4a-116">Retrieves hello deployment ID for hello instance.</span></span>

| <span data-ttu-id="d6f4a-117">Tipo</span><span class="sxs-lookup"><span data-stu-id="d6f4a-117">Type</span></span> | <span data-ttu-id="d6f4a-118">Exemplo</span><span class="sxs-lookup"><span data-stu-id="d6f4a-118">Example</span></span> |
| --- | --- |
| <span data-ttu-id="d6f4a-119">XPath</span><span class="sxs-lookup"><span data-stu-id="d6f4a-119">XPath</span></span> |<span data-ttu-id="d6f4a-120">xpath="/RoleEnvironment/Deployment/@id"</span><span class="sxs-lookup"><span data-stu-id="d6f4a-120">xpath="/RoleEnvironment/Deployment/@id"</span></span> |
| <span data-ttu-id="d6f4a-121">Código</span><span class="sxs-lookup"><span data-stu-id="d6f4a-121">Code</span></span> |<span data-ttu-id="d6f4a-122">var deploymentId = RoleEnvironment.DeploymentId;</span><span class="sxs-lookup"><span data-stu-id="d6f4a-122">var deploymentId = RoleEnvironment.DeploymentId;</span></span> |

## <a name="role-id"></a><span data-ttu-id="d6f4a-123">ID de Função</span><span class="sxs-lookup"><span data-stu-id="d6f4a-123">Role ID</span></span>
<span data-ttu-id="d6f4a-124">Recupera Olá ID da função atual para a instância de saudação.</span><span class="sxs-lookup"><span data-stu-id="d6f4a-124">Retrieves hello current role ID for hello instance.</span></span>

| <span data-ttu-id="d6f4a-125">Tipo</span><span class="sxs-lookup"><span data-stu-id="d6f4a-125">Type</span></span> | <span data-ttu-id="d6f4a-126">Exemplo</span><span class="sxs-lookup"><span data-stu-id="d6f4a-126">Example</span></span> |
| --- | --- |
| <span data-ttu-id="d6f4a-127">XPath</span><span class="sxs-lookup"><span data-stu-id="d6f4a-127">XPath</span></span> |<span data-ttu-id="d6f4a-128">xpath="/RoleEnvironment/CurrentInstance/@id"</span><span class="sxs-lookup"><span data-stu-id="d6f4a-128">xpath="/RoleEnvironment/CurrentInstance/@id"</span></span> |
| <span data-ttu-id="d6f4a-129">Código</span><span class="sxs-lookup"><span data-stu-id="d6f4a-129">Code</span></span> |<span data-ttu-id="d6f4a-130">var id = RoleEnvironment.CurrentRoleInstance.Id;</span><span class="sxs-lookup"><span data-stu-id="d6f4a-130">var id = RoleEnvironment.CurrentRoleInstance.Id;</span></span> |

## <a name="update-domain"></a><span data-ttu-id="d6f4a-131">Domínio de atualização</span><span class="sxs-lookup"><span data-stu-id="d6f4a-131">Update domain</span></span>
<span data-ttu-id="d6f4a-132">Recupera o domínio de atualização de saudação da instância de saudação.</span><span class="sxs-lookup"><span data-stu-id="d6f4a-132">Retrieves hello update domain of hello instance.</span></span>

| <span data-ttu-id="d6f4a-133">Tipo</span><span class="sxs-lookup"><span data-stu-id="d6f4a-133">Type</span></span> | <span data-ttu-id="d6f4a-134">Exemplo</span><span class="sxs-lookup"><span data-stu-id="d6f4a-134">Example</span></span> |
| --- | --- |
| <span data-ttu-id="d6f4a-135">XPath</span><span class="sxs-lookup"><span data-stu-id="d6f4a-135">XPath</span></span> |<span data-ttu-id="d6f4a-136">xpath="/RoleEnvironment/CurrentInstance/@updateDomain"</span><span class="sxs-lookup"><span data-stu-id="d6f4a-136">xpath="/RoleEnvironment/CurrentInstance/@updateDomain"</span></span> |
| <span data-ttu-id="d6f4a-137">Código</span><span class="sxs-lookup"><span data-stu-id="d6f4a-137">Code</span></span> |<span data-ttu-id="d6f4a-138">var ud = RoleEnvironment.CurrentRoleInstance.UpdateDomain;</span><span class="sxs-lookup"><span data-stu-id="d6f4a-138">var ud = RoleEnvironment.CurrentRoleInstance.UpdateDomain;</span></span> |

## <a name="fault-domain"></a><span data-ttu-id="d6f4a-139">Domínios de falha</span><span class="sxs-lookup"><span data-stu-id="d6f4a-139">Fault domain</span></span>
<span data-ttu-id="d6f4a-140">Recupera o domínio de falha de saudação da instância de saudação.</span><span class="sxs-lookup"><span data-stu-id="d6f4a-140">Retrieves hello fault domain of hello instance.</span></span>

| <span data-ttu-id="d6f4a-141">Tipo</span><span class="sxs-lookup"><span data-stu-id="d6f4a-141">Type</span></span> | <span data-ttu-id="d6f4a-142">Exemplo</span><span class="sxs-lookup"><span data-stu-id="d6f4a-142">Example</span></span> |
| --- | --- |
| <span data-ttu-id="d6f4a-143">XPath</span><span class="sxs-lookup"><span data-stu-id="d6f4a-143">XPath</span></span> |<span data-ttu-id="d6f4a-144">xpath="/RoleEnvironment/CurrentInstance/@faultDomain"</span><span class="sxs-lookup"><span data-stu-id="d6f4a-144">xpath="/RoleEnvironment/CurrentInstance/@faultDomain"</span></span> |
| <span data-ttu-id="d6f4a-145">Código</span><span class="sxs-lookup"><span data-stu-id="d6f4a-145">Code</span></span> |<span data-ttu-id="d6f4a-146">var fd = RoleEnvironment.CurrentRoleInstance.FaultDomain;</span><span class="sxs-lookup"><span data-stu-id="d6f4a-146">var fd = RoleEnvironment.CurrentRoleInstance.FaultDomain;</span></span> |

## <a name="role-name"></a><span data-ttu-id="d6f4a-147">Nome da função</span><span class="sxs-lookup"><span data-stu-id="d6f4a-147">Role name</span></span>
<span data-ttu-id="d6f4a-148">Recupera o nome da função hello de instâncias de saudação.</span><span class="sxs-lookup"><span data-stu-id="d6f4a-148">Retrieves hello role name of hello instances.</span></span>

| <span data-ttu-id="d6f4a-149">Tipo</span><span class="sxs-lookup"><span data-stu-id="d6f4a-149">Type</span></span> | <span data-ttu-id="d6f4a-150">Exemplo</span><span class="sxs-lookup"><span data-stu-id="d6f4a-150">Example</span></span> |
| --- | --- |
| <span data-ttu-id="d6f4a-151">XPath</span><span class="sxs-lookup"><span data-stu-id="d6f4a-151">XPath</span></span> |<span data-ttu-id="d6f4a-152">xpath="/RoleEnvironment/CurrentInstance/@roleName"</span><span class="sxs-lookup"><span data-stu-id="d6f4a-152">xpath="/RoleEnvironment/CurrentInstance/@roleName"</span></span> |
| <span data-ttu-id="d6f4a-153">Código</span><span class="sxs-lookup"><span data-stu-id="d6f4a-153">Code</span></span> |<span data-ttu-id="d6f4a-154">var rname = RoleEnvironment.CurrentRoleInstance.Role.Name;</span><span class="sxs-lookup"><span data-stu-id="d6f4a-154">var rname = RoleEnvironment.CurrentRoleInstance.Role.Name;</span></span> |

## <a name="config-setting"></a><span data-ttu-id="d6f4a-155">Definição de configuração</span><span class="sxs-lookup"><span data-stu-id="d6f4a-155">Config setting</span></span>
<span data-ttu-id="d6f4a-156">Recupera valor Olá Olá especificado de configuração.</span><span class="sxs-lookup"><span data-stu-id="d6f4a-156">Retrieves hello value of hello specified configuration setting.</span></span>

| <span data-ttu-id="d6f4a-157">Tipo</span><span class="sxs-lookup"><span data-stu-id="d6f4a-157">Type</span></span> | <span data-ttu-id="d6f4a-158">Exemplo</span><span class="sxs-lookup"><span data-stu-id="d6f4a-158">Example</span></span> |
| --- | --- |
| <span data-ttu-id="d6f4a-159">XPath</span><span class="sxs-lookup"><span data-stu-id="d6f4a-159">XPath</span></span> |<span data-ttu-id="d6f4a-160">xpath="/RoleEnvironment/CurrentInstance/ConfigurationSettings/ConfigurationSetting[@name='Setting1']/@value"</span><span class="sxs-lookup"><span data-stu-id="d6f4a-160">xpath="/RoleEnvironment/CurrentInstance/ConfigurationSettings/ConfigurationSetting[@name='Setting1']/@value"</span></span> |
| <span data-ttu-id="d6f4a-161">Código</span><span class="sxs-lookup"><span data-stu-id="d6f4a-161">Code</span></span> |<span data-ttu-id="d6f4a-162">var setting = RoleEnvironment.GetConfigurationSettingValue("Setting1");</span><span class="sxs-lookup"><span data-stu-id="d6f4a-162">var setting = RoleEnvironment.GetConfigurationSettingValue("Setting1");</span></span> |

## <a name="local-storage-path"></a><span data-ttu-id="d6f4a-163">Caminho do armazenamento local</span><span class="sxs-lookup"><span data-stu-id="d6f4a-163">Local storage path</span></span>
<span data-ttu-id="d6f4a-164">Recupera o caminho de armazenamento local de saudação da instância de saudação.</span><span class="sxs-lookup"><span data-stu-id="d6f4a-164">Retrieves hello local storage path for hello instance.</span></span>

| <span data-ttu-id="d6f4a-165">Tipo</span><span class="sxs-lookup"><span data-stu-id="d6f4a-165">Type</span></span> | <span data-ttu-id="d6f4a-166">Exemplo</span><span class="sxs-lookup"><span data-stu-id="d6f4a-166">Example</span></span> |
| --- | --- |
| <span data-ttu-id="d6f4a-167">XPath</span><span class="sxs-lookup"><span data-stu-id="d6f4a-167">XPath</span></span> |<span data-ttu-id="d6f4a-168">xpath="/RoleEnvironment/CurrentInstance/LocalResources/LocalResource[@name='LocalStore1']/@path"</span><span class="sxs-lookup"><span data-stu-id="d6f4a-168">xpath="/RoleEnvironment/CurrentInstance/LocalResources/LocalResource[@name='LocalStore1']/@path"</span></span> |
| <span data-ttu-id="d6f4a-169">Código</span><span class="sxs-lookup"><span data-stu-id="d6f4a-169">Code</span></span> |<span data-ttu-id="d6f4a-170">var localResourcePath = RoleEnvironment.GetLocalResource("LocalStore1").RootPath;</span><span class="sxs-lookup"><span data-stu-id="d6f4a-170">var localResourcePath = RoleEnvironment.GetLocalResource("LocalStore1").RootPath;</span></span> |

## <a name="local-storage-size"></a><span data-ttu-id="d6f4a-171">Tamanho do armazenamento local</span><span class="sxs-lookup"><span data-stu-id="d6f4a-171">Local storage size</span></span>
<span data-ttu-id="d6f4a-172">Recupera o tamanho de saudação do armazenamento local Olá instância de saudação.</span><span class="sxs-lookup"><span data-stu-id="d6f4a-172">Retrieves hello size of hello local storage for hello instance.</span></span>

| <span data-ttu-id="d6f4a-173">Tipo</span><span class="sxs-lookup"><span data-stu-id="d6f4a-173">Type</span></span> | <span data-ttu-id="d6f4a-174">Exemplo</span><span class="sxs-lookup"><span data-stu-id="d6f4a-174">Example</span></span> |
| --- | --- |
| <span data-ttu-id="d6f4a-175">XPath</span><span class="sxs-lookup"><span data-stu-id="d6f4a-175">XPath</span></span> |<span data-ttu-id="d6f4a-176">xpath="/RoleEnvironment/CurrentInstance/LocalResources/LocalResource[@name='LocalStore1']/@sizeInMB"</span><span class="sxs-lookup"><span data-stu-id="d6f4a-176">xpath="/RoleEnvironment/CurrentInstance/LocalResources/LocalResource[@name='LocalStore1']/@sizeInMB"</span></span> |
| <span data-ttu-id="d6f4a-177">Código</span><span class="sxs-lookup"><span data-stu-id="d6f4a-177">Code</span></span> |<span data-ttu-id="d6f4a-178">var localResourceSizeInMB = RoleEnvironment.GetLocalResource("LocalStore1").MaximumSizeInMegabytes;</span><span class="sxs-lookup"><span data-stu-id="d6f4a-178">var localResourceSizeInMB = RoleEnvironment.GetLocalResource("LocalStore1").MaximumSizeInMegabytes;</span></span> |

## <a name="endpoint-protocol"></a><span data-ttu-id="d6f4a-179">Protocolo do ponto de extremidade</span><span class="sxs-lookup"><span data-stu-id="d6f4a-179">Endpoint protocol</span></span>
<span data-ttu-id="d6f4a-180">Recupera o protocolo de ponto de extremidade de saudação para instância de saudação.</span><span class="sxs-lookup"><span data-stu-id="d6f4a-180">Retrieves hello endpoint protocol for hello instance.</span></span>

| <span data-ttu-id="d6f4a-181">Tipo</span><span class="sxs-lookup"><span data-stu-id="d6f4a-181">Type</span></span> | <span data-ttu-id="d6f4a-182">Exemplo</span><span class="sxs-lookup"><span data-stu-id="d6f4a-182">Example</span></span> |
| --- | --- |
| <span data-ttu-id="d6f4a-183">XPath</span><span class="sxs-lookup"><span data-stu-id="d6f4a-183">XPath</span></span> |<span data-ttu-id="d6f4a-184">xpath="/RoleEnvironment/CurrentInstance/Endpoints/Endpoint[@name='Endpoint1']/@protocol"</span><span class="sxs-lookup"><span data-stu-id="d6f4a-184">xpath="/RoleEnvironment/CurrentInstance/Endpoints/Endpoint[@name='Endpoint1']/@protocol"</span></span> |
| <span data-ttu-id="d6f4a-185">Código</span><span class="sxs-lookup"><span data-stu-id="d6f4a-185">Code</span></span> |<span data-ttu-id="d6f4a-186">var prot = RoleEnvironment.CurrentRoleInstance.InstanceEndpoints["Endpoint1"].Protocol;</span><span class="sxs-lookup"><span data-stu-id="d6f4a-186">var prot = RoleEnvironment.CurrentRoleInstance.InstanceEndpoints["Endpoint1"].Protocol;</span></span> |

## <a name="endpoint-ip"></a><span data-ttu-id="d6f4a-187">IP do ponto de extremidade</span><span class="sxs-lookup"><span data-stu-id="d6f4a-187">Endpoint IP</span></span>
<span data-ttu-id="d6f4a-188">Obtém Olá especificado o endereço IP do ponto de extremidade.</span><span class="sxs-lookup"><span data-stu-id="d6f4a-188">Gets hello specified endpoint's IP address.</span></span>

| <span data-ttu-id="d6f4a-189">Tipo</span><span class="sxs-lookup"><span data-stu-id="d6f4a-189">Type</span></span> | <span data-ttu-id="d6f4a-190">Exemplo</span><span class="sxs-lookup"><span data-stu-id="d6f4a-190">Example</span></span> |
| --- | --- |
| <span data-ttu-id="d6f4a-191">XPath</span><span class="sxs-lookup"><span data-stu-id="d6f4a-191">XPath</span></span> |<span data-ttu-id="d6f4a-192">xpath="/RoleEnvironment/CurrentInstance/Endpoints/Endpoint[@name='Endpoint1']/@address"</span><span class="sxs-lookup"><span data-stu-id="d6f4a-192">xpath="/RoleEnvironment/CurrentInstance/Endpoints/Endpoint[@name='Endpoint1']/@address"</span></span> |
| <span data-ttu-id="d6f4a-193">Código</span><span class="sxs-lookup"><span data-stu-id="d6f4a-193">Code</span></span> |<span data-ttu-id="d6f4a-194">var address = RoleEnvironment.CurrentRoleInstance.InstanceEndpoints["Endpoint1"].IPEndpoint.Address</span><span class="sxs-lookup"><span data-stu-id="d6f4a-194">var address = RoleEnvironment.CurrentRoleInstance.InstanceEndpoints["Endpoint1"].IPEndpoint.Address</span></span> |

## <a name="endpoint-port"></a><span data-ttu-id="d6f4a-195">Porta do ponto de extremidade</span><span class="sxs-lookup"><span data-stu-id="d6f4a-195">Endpoint port</span></span>
<span data-ttu-id="d6f4a-196">Recupera a porta do ponto de extremidade Olá para instância de saudação.</span><span class="sxs-lookup"><span data-stu-id="d6f4a-196">Retrieves hello endpoint port for hello instance.</span></span>

| <span data-ttu-id="d6f4a-197">Tipo</span><span class="sxs-lookup"><span data-stu-id="d6f4a-197">Type</span></span> | <span data-ttu-id="d6f4a-198">Exemplo</span><span class="sxs-lookup"><span data-stu-id="d6f4a-198">Example</span></span> |
| --- | --- |
| <span data-ttu-id="d6f4a-199">XPath</span><span class="sxs-lookup"><span data-stu-id="d6f4a-199">XPath</span></span> |<span data-ttu-id="d6f4a-200">xpath="/RoleEnvironment/CurrentInstance/Endpoints/Endpoint[@name='Endpoint1']/@port"</span><span class="sxs-lookup"><span data-stu-id="d6f4a-200">xpath="/RoleEnvironment/CurrentInstance/Endpoints/Endpoint[@name='Endpoint1']/@port"</span></span> |
| <span data-ttu-id="d6f4a-201">Código</span><span class="sxs-lookup"><span data-stu-id="d6f4a-201">Code</span></span> |<span data-ttu-id="d6f4a-202">var port = RoleEnvironment.CurrentRoleInstance.InstanceEndpoints["Endpoint1"].IPEndpoint.Port;</span><span class="sxs-lookup"><span data-stu-id="d6f4a-202">var port = RoleEnvironment.CurrentRoleInstance.InstanceEndpoints["Endpoint1"].IPEndpoint.Port;</span></span> |

## <a name="example"></a><span data-ttu-id="d6f4a-203">Exemplo</span><span class="sxs-lookup"><span data-stu-id="d6f4a-203">Example</span></span>
<span data-ttu-id="d6f4a-204">Aqui está um exemplo de uma função de trabalho que cria uma tarefa de inicialização com uma variável de ambiente denominada `TestIsEmulated` definir toohello [ @emulated valor xpath](#app-running-in-emulator).</span><span class="sxs-lookup"><span data-stu-id="d6f4a-204">Here is an example of a worker role that creates a startup task with an environment variable named `TestIsEmulated` set toohello [@emulated xpath value](#app-running-in-emulator).</span></span> 

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

## <a name="next-steps"></a><span data-ttu-id="d6f4a-205">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="d6f4a-205">Next steps</span></span>
<span data-ttu-id="d6f4a-206">Saiba mais sobre Olá [ServiceConfiguration](cloud-services-model-and-package.md#serviceconfigurationcscfg) arquivo.</span><span class="sxs-lookup"><span data-stu-id="d6f4a-206">Learn more about hello [ServiceConfiguration.cscfg](cloud-services-model-and-package.md#serviceconfigurationcscfg) file.</span></span>

<span data-ttu-id="d6f4a-207">Crie um pacote [ServicePackage.cspkg](cloud-services-model-and-package.md#servicepackagecspkg) .</span><span class="sxs-lookup"><span data-stu-id="d6f4a-207">Create a [ServicePackage.cspkg](cloud-services-model-and-package.md#servicepackagecspkg) package.</span></span>

<span data-ttu-id="d6f4a-208">Habilite a [área de trabalho remota](cloud-services-role-enable-remote-desktop.md) para uma função.</span><span class="sxs-lookup"><span data-stu-id="d6f4a-208">Enable [remote desktop](cloud-services-role-enable-remote-desktop.md) for a role.</span></span>

