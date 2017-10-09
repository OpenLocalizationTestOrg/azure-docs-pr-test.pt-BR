---
title: "aaaOMS extensão de máquina virtual do Azure para Linux | Microsoft Docs"
description: "Implante o agente do OMS Olá na máquina virtual do Linux usando uma extensão de máquina virtual."
services: virtual-machines-linux
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: c7bbf210-7d71-4a37-ba47-9c74567a9ea6
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 04/26/2017
ms.author: nepeters
ms.openlocfilehash: 0fc8003d1fae6c043eef18ae78d12f9304b70832
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="oms-virtual-machine-extension-for-linux"></a><span data-ttu-id="8cee0-103">Extensão da máquina virtual do OMS para Linux</span><span class="sxs-lookup"><span data-stu-id="8cee0-103">OMS virtual machine extension for Linux</span></span>

## <a name="overview"></a><span data-ttu-id="8cee0-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="8cee0-104">Overview</span></span>

<span data-ttu-id="8cee0-105">O OMS (Operations Management Suite) fornece recursos de monitoramento, alertas e correção de alertas nos ativos locais e da nuvem.</span><span class="sxs-lookup"><span data-stu-id="8cee0-105">Operations Management Suite (OMS) provides monitoring, alerting, and alert remediation capabilities across cloud and on-premises assets.</span></span> <span data-ttu-id="8cee0-106">Olá extensão de máquina virtual do agente do OMS para Linux é publicada e suporte da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="8cee0-106">hello OMS Agent virtual machine extension for Linux is published and supported by Microsoft.</span></span> <span data-ttu-id="8cee0-107">extensão de saudação instala o agente do OMS Olá em máquinas virtuais do Azure e registra as máquinas virtuais em um espaço de trabalho existente do OMS.</span><span class="sxs-lookup"><span data-stu-id="8cee0-107">hello extension installs hello OMS agent on Azure virtual machines, and enrolls virtual machines into an existing OMS workspace.</span></span> <span data-ttu-id="8cee0-108">Saudação de detalhes neste documento suporte a plataformas, configurações e opções de implantação para Olá extensão de máquina virtual do OMS para Linux.</span><span class="sxs-lookup"><span data-stu-id="8cee0-108">This document details hello supported platforms, configurations, and deployment options for hello OMS virtual machine extension for Linux.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8cee0-109">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="8cee0-109">Prerequisites</span></span>

### <a name="operating-system"></a><span data-ttu-id="8cee0-110">Sistema operacional</span><span class="sxs-lookup"><span data-stu-id="8cee0-110">Operating system</span></span>

<span data-ttu-id="8cee0-111">Olá extensão do agente do OMS pode ser executado em relação a essas distribuições do Linux.</span><span class="sxs-lookup"><span data-stu-id="8cee0-111">hello OMS Agent extension can be run against these Linux distributions.</span></span>

| <span data-ttu-id="8cee0-112">Distribuição</span><span class="sxs-lookup"><span data-stu-id="8cee0-112">Distribution</span></span> | <span data-ttu-id="8cee0-113">Versão</span><span class="sxs-lookup"><span data-stu-id="8cee0-113">Version</span></span> |
|---|---|
| <span data-ttu-id="8cee0-114">CentOS Linux</span><span class="sxs-lookup"><span data-stu-id="8cee0-114">CentOS Linux</span></span> | <span data-ttu-id="8cee0-115">5, 6 e 7</span><span class="sxs-lookup"><span data-stu-id="8cee0-115">5, 6, and 7</span></span> |
| <span data-ttu-id="8cee0-116">Oracle Linux</span><span class="sxs-lookup"><span data-stu-id="8cee0-116">Oracle Linux</span></span> | <span data-ttu-id="8cee0-117">5, 6 e 7</span><span class="sxs-lookup"><span data-stu-id="8cee0-117">5, 6, and 7</span></span> |
| <span data-ttu-id="8cee0-118">Red Hat Enterprise Linux Server</span><span class="sxs-lookup"><span data-stu-id="8cee0-118">Red Hat Enterprise Linux Server</span></span> | <span data-ttu-id="8cee0-119">5, 6 e 7</span><span class="sxs-lookup"><span data-stu-id="8cee0-119">5, 6 and 7</span></span> |
| <span data-ttu-id="8cee0-120">Debian GNU/Linux</span><span class="sxs-lookup"><span data-stu-id="8cee0-120">Debian GNU/Linux</span></span> | <span data-ttu-id="8cee0-121">6, 7 e 8</span><span class="sxs-lookup"><span data-stu-id="8cee0-121">6, 7, and 8</span></span> |
| <span data-ttu-id="8cee0-122">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="8cee0-122">Ubuntu</span></span> | <span data-ttu-id="8cee0-123">12.04 LTS, 14.04 LTS, 15.04, 15.10, 16.04 LTS</span><span class="sxs-lookup"><span data-stu-id="8cee0-123">12.04 LTS, 14.04 LTS, 15.04, 15.10, 16.04 LTS</span></span> |
| <span data-ttu-id="8cee0-124">SUSE Linux Enterprise Server</span><span class="sxs-lookup"><span data-stu-id="8cee0-124">SUSE Linux Enterprise Server</span></span> | <span data-ttu-id="8cee0-125">11 e 12</span><span class="sxs-lookup"><span data-stu-id="8cee0-125">11 and 12</span></span> |

### <a name="internet-connectivity"></a><span data-ttu-id="8cee0-126">Conectividade com a Internet</span><span class="sxs-lookup"><span data-stu-id="8cee0-126">Internet connectivity</span></span>

<span data-ttu-id="8cee0-127">Olá extensão do agente do OMS para Linux requer que a máquina virtual Olá destino é toohello conectado à internet.</span><span class="sxs-lookup"><span data-stu-id="8cee0-127">hello OMS Agent extension for Linux requires that hello target virtual machine is connected toohello internet.</span></span> 

## <a name="extension-schema"></a><span data-ttu-id="8cee0-128">Esquema de extensão</span><span class="sxs-lookup"><span data-stu-id="8cee0-128">Extension schema</span></span>

<span data-ttu-id="8cee0-129">Olá JSON a seguir mostra esquema Olá Olá extensão do agente do OMS.</span><span class="sxs-lookup"><span data-stu-id="8cee0-129">hello following JSON shows hello schema for hello OMS Agent extension.</span></span> <span data-ttu-id="8cee0-130">extensão de saudação requer a chave de ID e o espaço de trabalho de espaço de trabalho de saudação do espaço de trabalho OMS do destino Olá; Esses valores podem ser encontrados no portal do OMS hello.</span><span class="sxs-lookup"><span data-stu-id="8cee0-130">hello extension requires hello workspace ID and workspace key from hello target OMS workspace; these values can be found in hello OMS portal.</span></span> <span data-ttu-id="8cee0-131">Porque a chave do espaço de trabalho Olá deve ser tratado como dados confidenciais, devem ser armazenado em uma configuração protegida.</span><span class="sxs-lookup"><span data-stu-id="8cee0-131">Because hello workspace key should be treated as sensitive data, it should be stored in a protected setting configuration.</span></span> <span data-ttu-id="8cee0-132">Dados de configuração de extensão protegido de VM do Azure é criptografados e descriptografados apenas na máquina de virtual de destino hello.</span><span class="sxs-lookup"><span data-stu-id="8cee0-132">Azure VM extension protected setting data is encrypted, and only decrypted on hello target virtual machine.</span></span> <span data-ttu-id="8cee0-133">Observe que **workspaceId** e **workspaceKey** diferenciam maiúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="8cee0-133">Note that **workspaceId** and **workspaceKey** are case-sensitive.</span></span>

```json
{
  "type": "extensions",
  "name": "OMSExtension",
  "apiVersion": "2015-06-15",
  "location": "<location>",
  "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/', <vm-name>)]"
  ],
  "properties": {
    "publisher": "Microsoft.EnterpriseCloud.Monitoring",
    "type": "OmsAgentForLinux",
    "typeHandlerVersion": "1.4",
    "settings": {
      "workspaceId": "myWorkspaceId"
    },
    "protectedSettings": {
      "workspaceKey": "myWorkSpaceKey"
    }
  }
}
```

### <a name="property-values"></a><span data-ttu-id="8cee0-134">Valores de propriedade</span><span class="sxs-lookup"><span data-stu-id="8cee0-134">Property values</span></span>

| <span data-ttu-id="8cee0-135">Nome</span><span class="sxs-lookup"><span data-stu-id="8cee0-135">Name</span></span> | <span data-ttu-id="8cee0-136">Valor/Exemplo</span><span class="sxs-lookup"><span data-stu-id="8cee0-136">Value / Example</span></span> |
| ---- | ---- |
| <span data-ttu-id="8cee0-137">apiVersion</span><span class="sxs-lookup"><span data-stu-id="8cee0-137">apiVersion</span></span> | <span data-ttu-id="8cee0-138">2015-06-15</span><span class="sxs-lookup"><span data-stu-id="8cee0-138">2015-06-15</span></span> |
| <span data-ttu-id="8cee0-139">publicador</span><span class="sxs-lookup"><span data-stu-id="8cee0-139">publisher</span></span> | <span data-ttu-id="8cee0-140">Microsoft.EnterpriseCloud.Monitoring</span><span class="sxs-lookup"><span data-stu-id="8cee0-140">Microsoft.EnterpriseCloud.Monitoring</span></span> |
| <span data-ttu-id="8cee0-141">type</span><span class="sxs-lookup"><span data-stu-id="8cee0-141">type</span></span> | <span data-ttu-id="8cee0-142">OmsAgentForLinux</span><span class="sxs-lookup"><span data-stu-id="8cee0-142">OmsAgentForLinux</span></span> |
| <span data-ttu-id="8cee0-143">typeHandlerVersion</span><span class="sxs-lookup"><span data-stu-id="8cee0-143">typeHandlerVersion</span></span> | <span data-ttu-id="8cee0-144">1.4</span><span class="sxs-lookup"><span data-stu-id="8cee0-144">1.4</span></span> |
| <span data-ttu-id="8cee0-145">workspaceId (por exemplo)</span><span class="sxs-lookup"><span data-stu-id="8cee0-145">workspaceId (e.g)</span></span> | <span data-ttu-id="8cee0-146">6f680a37-00c6-41c7-a93f-1437e3462574</span><span class="sxs-lookup"><span data-stu-id="8cee0-146">6f680a37-00c6-41c7-a93f-1437e3462574</span></span> |
| <span data-ttu-id="8cee0-147">workspaceKey (por exemplo)</span><span class="sxs-lookup"><span data-stu-id="8cee0-147">workspaceKey (e.g)</span></span> | <span data-ttu-id="8cee0-148">z4bU3p1/GrnWpQkky4gdabWXAhbWSTz70hm4m2Xt92XI+rSRgE8qVvRhsGo9TXffbrTahyrwv35W0pOqQAU7uQ==</span><span class="sxs-lookup"><span data-stu-id="8cee0-148">z4bU3p1/GrnWpQkky4gdabWXAhbWSTz70hm4m2Xt92XI+rSRgE8qVvRhsGo9TXffbrTahyrwv35W0pOqQAU7uQ==</span></span> |


## <a name="template-deployment"></a><span data-ttu-id="8cee0-149">Implantação de modelo</span><span class="sxs-lookup"><span data-stu-id="8cee0-149">Template deployment</span></span>

<span data-ttu-id="8cee0-150">Extensões de VM do Azure podem ser implantadas com modelos do Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="8cee0-150">Azure VM extensions can be deployed with Azure Resource Manager templates.</span></span> <span data-ttu-id="8cee0-151">Modelos são ideais ao implantar um ou mais máquinas virtuais que exigem configuração de implantação de post como tooOMS de integração.</span><span class="sxs-lookup"><span data-stu-id="8cee0-151">Templates are ideal when deploying one or more virtual machines that require post deployment configuration such as onboarding tooOMS.</span></span> <span data-ttu-id="8cee0-152">Um Gerenciador de recursos de modelo que inclui a extensão de VM de agente do OMS Olá pode ser encontrado no hello [Galeria de início rápido do Azure](https://github.com/Azure/azure-quickstart-templates/tree/master/201-oms-extension-ubuntu-vm).</span><span class="sxs-lookup"><span data-stu-id="8cee0-152">A sample Resource Manager template that includes hello OMS Agent VM extension can be found on hello [Azure Quick Start Gallery](https://github.com/Azure/azure-quickstart-templates/tree/master/201-oms-extension-ubuntu-vm).</span></span> 

<span data-ttu-id="8cee0-153">configuração de JSON Olá para uma extensão de máquina virtual pode ser aninhada dentro do recurso de máquina virtual de saudação ou colocada na raiz de saudação ou de nível superior de um modelo JSON do Gerenciador de recursos.</span><span class="sxs-lookup"><span data-stu-id="8cee0-153">hello JSON configuration for a virtual machine extension can be nested inside hello virtual machine resource, or placed at hello root or top level of a Resource Manager JSON template.</span></span> <span data-ttu-id="8cee0-154">posicionamento de saudação da configuração de JSON de saudação afeta o valor de saudação do nome do recurso hello e tipo.</span><span class="sxs-lookup"><span data-stu-id="8cee0-154">hello placement of hello JSON configuration affects hello value of hello resource name and type.</span></span> <span data-ttu-id="8cee0-155">Para obter mais informações, consulte [Definir o nome e o tipo de recursos filho](../../azure-resource-manager/resource-manager-template-child-resource.md).</span><span class="sxs-lookup"><span data-stu-id="8cee0-155">For more information, see [Set name and type for child resources](../../azure-resource-manager/resource-manager-template-child-resource.md).</span></span> 

<span data-ttu-id="8cee0-156">Olá exemplo a seguir supõe extensão do OMS hello está aninhado em Olá recurso da máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="8cee0-156">hello following example assumes hello OMS extension is nested inside hello virtual machine resource.</span></span> <span data-ttu-id="8cee0-157">Ao aninhar o recurso de extensão hello, Olá JSON é colocado no hello `"resources": []` objeto da máquina virtual de saudação.</span><span class="sxs-lookup"><span data-stu-id="8cee0-157">When nesting hello extension resource, hello JSON is placed in hello `"resources": []` object of hello virtual machine.</span></span>

```json
{
  "type": "extensions",
  "name": "OMSExtension",
  "apiVersion": "2015-06-15",
  "location": "<location>",
  "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/', <vm-name>)]"
  ],
  "properties": {
    "publisher": "Microsoft.EnterpriseCloud.Monitoring",
    "type": "OmsAgentForLinux",
    "typeHandlerVersion": "1.4",
    "settings": {
      "workspaceId": "myWorkspaceId"
    },
    "protectedSettings": {
      "workspaceKey": "myWorkSpaceKey"
    }
  }
}
```

<span data-ttu-id="8cee0-158">Ao inserir extensão Olá JSON na raiz de saudação do modelo Olá, nome do recurso de saudação inclui uma máquina virtual do referência toohello pai e tipo hello reflete configuração aninhada Olá.</span><span class="sxs-lookup"><span data-stu-id="8cee0-158">When placing hello extension JSON at hello root of hello template, hello resource name includes a reference toohello parent virtual machine, and hello type reflects hello nested configuration.</span></span>  

```json
{
  "type": "Microsoft.Compute/virtualMachines/extensions",
  "name": "<parentVmResource>/OMSExtension",
  "apiVersion": "2015-06-15",
  "location": "<location>",
  "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/', <vm-name>)]"
  ],
  "properties": {
    "publisher": "Microsoft.EnterpriseCloud.Monitoring",
    "type": "OmsAgentForLinux",
    "typeHandlerVersion": "1.4",
    "settings": {
      "workspaceId": "myWorkspaceId"
    },
    "protectedSettings": {
      "workspaceKey": "myWorkSpaceKey"
    }
  }
}
```

## <a name="azure-cli-deployment"></a><span data-ttu-id="8cee0-159">Implantação da CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="8cee0-159">Azure CLI deployment</span></span>

<span data-ttu-id="8cee0-160">Olá CLI do Azure pode ser usado toodeploy Olá VM de agente do OMS extensão tooan máquina virtual existente.</span><span class="sxs-lookup"><span data-stu-id="8cee0-160">hello Azure CLI can be used toodeploy hello OMS Agent VM extension tooan existing virtual machine.</span></span> <span data-ttu-id="8cee0-161">Substitua a chave OMS do hello e ID do OMS com os de seu espaço de trabalho do OMS.</span><span class="sxs-lookup"><span data-stu-id="8cee0-161">Replace hello OMS key and OMS ID with those from your OMS workspace.</span></span> 

```azurecli
az vm extension set \
  --resource-group myResourceGroup \
  --vm-name myVM \
  --name OmsAgentForLinux \
  --publisher Microsoft.EnterpriseCloud.Monitoring \
  --version 1.4 --protected-settings '{"workspaceKey": "omskey"}' \
  --settings '{"workspaceId": "omsid"}'
```

## <a name="troubleshoot-and-support"></a><span data-ttu-id="8cee0-162">Solução de problemas e suporte</span><span class="sxs-lookup"><span data-stu-id="8cee0-162">Troubleshoot and support</span></span>

### <a name="troubleshoot"></a><span data-ttu-id="8cee0-163">Solucionar problemas</span><span class="sxs-lookup"><span data-stu-id="8cee0-163">Troubleshoot</span></span>

<span data-ttu-id="8cee0-164">Dados sobre o estado de saudação de implantações de extensão podem ser recuperados da saudação portal do Azure e usando Olá CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="8cee0-164">Data about hello state of extension deployments can be retrieved from hello Azure portal, and by using hello Azure CLI.</span></span> <span data-ttu-id="8cee0-165">estado da implantação Olá toosee de extensões para uma determinada VM, execute hello usando o comando a seguir Olá CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="8cee0-165">toosee hello deployment state of extensions for a given VM, run hello following command using hello Azure CLI.</span></span>

```azurecli
az vm extension list --resource-group myResourceGroup --vm-name myVM -o table
```

<span data-ttu-id="8cee0-166">Execução de extensão é conectado toohello após o arquivo de saída:</span><span class="sxs-lookup"><span data-stu-id="8cee0-166">Extension execution output is logged toohello following file:</span></span>

```
/opt/microsoft/omsagent/bin/stdout
```

### <a name="error-codes-and-their-meanings"></a><span data-ttu-id="8cee0-167">Códigos de erro e seus significados</span><span class="sxs-lookup"><span data-stu-id="8cee0-167">Error codes and their meanings</span></span>

| <span data-ttu-id="8cee0-168">Código do Erro</span><span class="sxs-lookup"><span data-stu-id="8cee0-168">Error Code</span></span> | <span data-ttu-id="8cee0-169">Significado</span><span class="sxs-lookup"><span data-stu-id="8cee0-169">Meaning</span></span> | <span data-ttu-id="8cee0-170">Ação possível</span><span class="sxs-lookup"><span data-stu-id="8cee0-170">Possible Action</span></span> |
| :---: | --- | --- |
| <span data-ttu-id="8cee0-171">10</span><span class="sxs-lookup"><span data-stu-id="8cee0-171">10</span></span> | <span data-ttu-id="8cee0-172">VM já está conectado tooan espaço de trabalho do OMS</span><span class="sxs-lookup"><span data-stu-id="8cee0-172">VM is already connected tooan OMS workspace</span></span> | <span data-ttu-id="8cee0-173">tooconnect Olá VM toohello espaço de trabalho especificado no esquema de extensão Olá, defina stopOnMultipleConnections toofalse nas configurações de públicas ou remova esta propriedade.</span><span class="sxs-lookup"><span data-stu-id="8cee0-173">tooconnect hello VM toohello workspace specified in hello extension schema, set stopOnMultipleConnections toofalse in public settings or remove this property.</span></span> <span data-ttu-id="8cee0-174">Essa VM é cobrada uma vez para cada espaço de trabalho ao qual está conectada.</span><span class="sxs-lookup"><span data-stu-id="8cee0-174">This VM gets billed once for each workspace it is connected to.</span></span> |
| <span data-ttu-id="8cee0-175">11</span><span class="sxs-lookup"><span data-stu-id="8cee0-175">11</span></span> | <span data-ttu-id="8cee0-176">Extensão de toohello de configuração inválido fornecida</span><span class="sxs-lookup"><span data-stu-id="8cee0-176">Invalid config provided toohello extension</span></span> | <span data-ttu-id="8cee0-177">Siga Olá anterior exemplos tooset todos os valores de propriedade necessários à implantação.</span><span class="sxs-lookup"><span data-stu-id="8cee0-177">Follow hello preceding examples tooset all property values necessary for deployment.</span></span> |
| <span data-ttu-id="8cee0-178">12</span><span class="sxs-lookup"><span data-stu-id="8cee0-178">12</span></span> | <span data-ttu-id="8cee0-179">Gerenciador de pacote dpkg Hello está bloqueado</span><span class="sxs-lookup"><span data-stu-id="8cee0-179">hello dpkg package manager is locked</span></span> | <span data-ttu-id="8cee0-180">Verifique se o todas as operações de atualização de dpkg na máquina de saudação terminar e tente novamente.</span><span class="sxs-lookup"><span data-stu-id="8cee0-180">Make sure all dpkg update operations on hello machine have finished and retry.</span></span> |
| <span data-ttu-id="8cee0-181">20</span><span class="sxs-lookup"><span data-stu-id="8cee0-181">20</span></span> | <span data-ttu-id="8cee0-182">Habilitar chamado prematuramente</span><span class="sxs-lookup"><span data-stu-id="8cee0-182">Enable called prematurely</span></span> | <span data-ttu-id="8cee0-183">[Saudação de atualização do Azure Linux Agent](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/update-agent) toohello versão mais recente.</span><span class="sxs-lookup"><span data-stu-id="8cee0-183">[Update hello Azure Linux Agent](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/update-agent) toohello latest available version.</span></span> |
| <span data-ttu-id="8cee0-184">51</span><span class="sxs-lookup"><span data-stu-id="8cee0-184">51</span></span> | <span data-ttu-id="8cee0-185">Não há suporte para essa extensão no sistema de operação de saudação da VM</span><span class="sxs-lookup"><span data-stu-id="8cee0-185">This extension is not supported on hello VM's operation system</span></span> | |
| <span data-ttu-id="8cee0-186">55</span><span class="sxs-lookup"><span data-stu-id="8cee0-186">55</span></span> | <span data-ttu-id="8cee0-187">Não é possível conectar o serviço do Microsoft Operations Management Suite toohello</span><span class="sxs-lookup"><span data-stu-id="8cee0-187">Cannot connect toohello Microsoft Operations Management Suite service</span></span> | <span data-ttu-id="8cee0-188">Verifique se Olá sistema tem acesso à Internet ou que um proxy HTTP válido foi fornecido.</span><span class="sxs-lookup"><span data-stu-id="8cee0-188">Check that hello system either has Internet access, or that a valid HTTP proxy has been provided.</span></span> <span data-ttu-id="8cee0-189">Além disso, verifique a exatidão de saudação da ID do espaço de trabalho de saudação.</span><span class="sxs-lookup"><span data-stu-id="8cee0-189">Additionally, check hello correctness of hello workspace ID.</span></span> |

<span data-ttu-id="8cee0-190">Informações de solução de problemas adicionais podem ser encontradas em Olá [guia de solução de problemas de agente do OMS para Linux](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/Troubleshooting.md#).</span><span class="sxs-lookup"><span data-stu-id="8cee0-190">Additional troubleshooting information can be found on hello [OMS-Agent-for-Linux Troubleshooting Guide](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/Troubleshooting.md#).</span></span>

### <a name="support"></a><span data-ttu-id="8cee0-191">Suporte</span><span class="sxs-lookup"><span data-stu-id="8cee0-191">Support</span></span>

<span data-ttu-id="8cee0-192">Se você precisar de mais ajuda a qualquer momento neste artigo, você pode contatar hello Azure especialistas em Olá [fóruns MSDN Azure e o estouro de pilha](https://azure.microsoft.com/en-us/support/forums/).</span><span class="sxs-lookup"><span data-stu-id="8cee0-192">If you need more help at any point in this article, you can contact hello Azure experts on hello [MSDN Azure and Stack Overflow forums](https://azure.microsoft.com/en-us/support/forums/).</span></span> <span data-ttu-id="8cee0-193">Como alternativa, você pode registrar um incidente de suporte do Azure.</span><span class="sxs-lookup"><span data-stu-id="8cee0-193">Alternatively, you can file an Azure support incident.</span></span> <span data-ttu-id="8cee0-194">Vá toohello [site de suporte do Azure](https://azure.microsoft.com/en-us/support/options/) e selecione obter suporte.</span><span class="sxs-lookup"><span data-stu-id="8cee0-194">Go toohello [Azure support site](https://azure.microsoft.com/en-us/support/options/) and select Get support.</span></span> <span data-ttu-id="8cee0-195">Para obter informações sobre como usar o suporte do Azure, leia Olá [perguntas frequentes sobre o suporte da Microsoft Azure](https://azure.microsoft.com/en-us/support/faq/).</span><span class="sxs-lookup"><span data-stu-id="8cee0-195">For information about using Azure Support, read hello [Microsoft Azure support FAQ](https://azure.microsoft.com/en-us/support/faq/).</span></span>
