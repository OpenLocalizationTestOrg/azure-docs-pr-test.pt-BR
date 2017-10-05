---
title: "Extensão da máquina virtual do OMS Azure para Linux | Microsoft Docs"
description: "Implante o agente do OMS na máquina virtual Linux usando uma extensão da máquina virtual."
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
ms.openlocfilehash: 138fc8c98ea6f409b28407b20851c96ecc618b09
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="oms-virtual-machine-extension-for-linux"></a><span data-ttu-id="a7b1c-103">Extensão da máquina virtual do OMS para Linux</span><span class="sxs-lookup"><span data-stu-id="a7b1c-103">OMS virtual machine extension for Linux</span></span>

## <a name="overview"></a><span data-ttu-id="a7b1c-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="a7b1c-104">Overview</span></span>

<span data-ttu-id="a7b1c-105">O OMS (Operations Management Suite) fornece recursos de monitoramento, alertas e correção de alertas nos ativos locais e da nuvem.</span><span class="sxs-lookup"><span data-stu-id="a7b1c-105">Operations Management Suite (OMS) provides monitoring, alerting, and alert remediation capabilities across cloud and on-premises assets.</span></span> <span data-ttu-id="a7b1c-106">A extensão da máquina virtual do agente do OMS para Linux é publicada e recebe suporte da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="a7b1c-106">The OMS Agent virtual machine extension for Linux is published and supported by Microsoft.</span></span> <span data-ttu-id="a7b1c-107">A extensão instala o agente do OMS em máquinas virtuais do Azure e registra máquinas virtuais em um espaço de trabalho OMS existente.</span><span class="sxs-lookup"><span data-stu-id="a7b1c-107">The extension installs the OMS agent on Azure virtual machines, and enrolls virtual machines into an existing OMS workspace.</span></span> <span data-ttu-id="a7b1c-108">Este documento detalha as plataformas com opções de plataformas, configurações e implantação com suporte para a extensão da máquina virtual do OMS para Linux.</span><span class="sxs-lookup"><span data-stu-id="a7b1c-108">This document details the supported platforms, configurations, and deployment options for the OMS virtual machine extension for Linux.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a7b1c-109">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="a7b1c-109">Prerequisites</span></span>

### <a name="operating-system"></a><span data-ttu-id="a7b1c-110">Sistema operacional</span><span class="sxs-lookup"><span data-stu-id="a7b1c-110">Operating system</span></span>

<span data-ttu-id="a7b1c-111">A extensão do agente do OMS pode ser executada nessas distribuições do Linux.</span><span class="sxs-lookup"><span data-stu-id="a7b1c-111">The OMS Agent extension can be run against these Linux distributions.</span></span>

| <span data-ttu-id="a7b1c-112">Distribuição</span><span class="sxs-lookup"><span data-stu-id="a7b1c-112">Distribution</span></span> | <span data-ttu-id="a7b1c-113">Versão</span><span class="sxs-lookup"><span data-stu-id="a7b1c-113">Version</span></span> |
|---|---|
| <span data-ttu-id="a7b1c-114">CentOS Linux</span><span class="sxs-lookup"><span data-stu-id="a7b1c-114">CentOS Linux</span></span> | <span data-ttu-id="a7b1c-115">5, 6 e 7</span><span class="sxs-lookup"><span data-stu-id="a7b1c-115">5, 6, and 7</span></span> |
| <span data-ttu-id="a7b1c-116">Oracle Linux</span><span class="sxs-lookup"><span data-stu-id="a7b1c-116">Oracle Linux</span></span> | <span data-ttu-id="a7b1c-117">5, 6 e 7</span><span class="sxs-lookup"><span data-stu-id="a7b1c-117">5, 6, and 7</span></span> |
| <span data-ttu-id="a7b1c-118">Red Hat Enterprise Linux Server</span><span class="sxs-lookup"><span data-stu-id="a7b1c-118">Red Hat Enterprise Linux Server</span></span> | <span data-ttu-id="a7b1c-119">5, 6 e 7</span><span class="sxs-lookup"><span data-stu-id="a7b1c-119">5, 6 and 7</span></span> |
| <span data-ttu-id="a7b1c-120">Debian GNU/Linux</span><span class="sxs-lookup"><span data-stu-id="a7b1c-120">Debian GNU/Linux</span></span> | <span data-ttu-id="a7b1c-121">6, 7 e 8</span><span class="sxs-lookup"><span data-stu-id="a7b1c-121">6, 7, and 8</span></span> |
| <span data-ttu-id="a7b1c-122">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="a7b1c-122">Ubuntu</span></span> | <span data-ttu-id="a7b1c-123">12.04 LTS, 14.04 LTS, 15.04, 15.10, 16.04 LTS</span><span class="sxs-lookup"><span data-stu-id="a7b1c-123">12.04 LTS, 14.04 LTS, 15.04, 15.10, 16.04 LTS</span></span> |
| <span data-ttu-id="a7b1c-124">SUSE Linux Enterprise Server</span><span class="sxs-lookup"><span data-stu-id="a7b1c-124">SUSE Linux Enterprise Server</span></span> | <span data-ttu-id="a7b1c-125">11 e 12</span><span class="sxs-lookup"><span data-stu-id="a7b1c-125">11 and 12</span></span> |

### <a name="internet-connectivity"></a><span data-ttu-id="a7b1c-126">Conectividade com a Internet</span><span class="sxs-lookup"><span data-stu-id="a7b1c-126">Internet connectivity</span></span>

<span data-ttu-id="a7b1c-127">A extensão do Agente do OMS para Linux requer que a máquina virtual de destino esteja conectada à Internet.</span><span class="sxs-lookup"><span data-stu-id="a7b1c-127">The OMS Agent extension for Linux requires that the target virtual machine is connected to the internet.</span></span> 

## <a name="extension-schema"></a><span data-ttu-id="a7b1c-128">Esquema de extensão</span><span class="sxs-lookup"><span data-stu-id="a7b1c-128">Extension schema</span></span>

<span data-ttu-id="a7b1c-129">O JSON a seguir mostra o esquema para a extensão do Agente do OMS.</span><span class="sxs-lookup"><span data-stu-id="a7b1c-129">The following JSON shows the schema for the OMS Agent extension.</span></span> <span data-ttu-id="a7b1c-130">A extensão requer a ID e a chave do espaço de trabalho do espaço de trabalho do OMS de destino, valores que podem ser encontrados no portal do OMS.</span><span class="sxs-lookup"><span data-stu-id="a7b1c-130">The extension requires the workspace ID and workspace key from the target OMS workspace; these values can be found in the OMS portal.</span></span> <span data-ttu-id="a7b1c-131">Como a chave do espaço de trabalho deve ser tratada como um dado confidencial, ela é armazenada em uma configuração protegida.</span><span class="sxs-lookup"><span data-stu-id="a7b1c-131">Because the workspace key should be treated as sensitive data, it should be stored in a protected setting configuration.</span></span> <span data-ttu-id="a7b1c-132">Os dados de configuração protegidos pela extensão da VM do Azure são criptografados, sendo descriptografados apenas na máquina virtual de destino.</span><span class="sxs-lookup"><span data-stu-id="a7b1c-132">Azure VM extension protected setting data is encrypted, and only decrypted on the target virtual machine.</span></span> <span data-ttu-id="a7b1c-133">Observe que **workspaceId** e **workspaceKey** diferenciam maiúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="a7b1c-133">Note that **workspaceId** and **workspaceKey** are case-sensitive.</span></span>

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

### <a name="property-values"></a><span data-ttu-id="a7b1c-134">Valores de propriedade</span><span class="sxs-lookup"><span data-stu-id="a7b1c-134">Property values</span></span>

| <span data-ttu-id="a7b1c-135">Nome</span><span class="sxs-lookup"><span data-stu-id="a7b1c-135">Name</span></span> | <span data-ttu-id="a7b1c-136">Valor/Exemplo</span><span class="sxs-lookup"><span data-stu-id="a7b1c-136">Value / Example</span></span> |
| ---- | ---- |
| <span data-ttu-id="a7b1c-137">apiVersion</span><span class="sxs-lookup"><span data-stu-id="a7b1c-137">apiVersion</span></span> | <span data-ttu-id="a7b1c-138">2015-06-15</span><span class="sxs-lookup"><span data-stu-id="a7b1c-138">2015-06-15</span></span> |
| <span data-ttu-id="a7b1c-139">publicador</span><span class="sxs-lookup"><span data-stu-id="a7b1c-139">publisher</span></span> | <span data-ttu-id="a7b1c-140">Microsoft.EnterpriseCloud.Monitoring</span><span class="sxs-lookup"><span data-stu-id="a7b1c-140">Microsoft.EnterpriseCloud.Monitoring</span></span> |
| <span data-ttu-id="a7b1c-141">type</span><span class="sxs-lookup"><span data-stu-id="a7b1c-141">type</span></span> | <span data-ttu-id="a7b1c-142">OmsAgentForLinux</span><span class="sxs-lookup"><span data-stu-id="a7b1c-142">OmsAgentForLinux</span></span> |
| <span data-ttu-id="a7b1c-143">typeHandlerVersion</span><span class="sxs-lookup"><span data-stu-id="a7b1c-143">typeHandlerVersion</span></span> | <span data-ttu-id="a7b1c-144">1.4</span><span class="sxs-lookup"><span data-stu-id="a7b1c-144">1.4</span></span> |
| <span data-ttu-id="a7b1c-145">workspaceId (por exemplo)</span><span class="sxs-lookup"><span data-stu-id="a7b1c-145">workspaceId (e.g)</span></span> | <span data-ttu-id="a7b1c-146">6f680a37-00c6-41c7-a93f-1437e3462574</span><span class="sxs-lookup"><span data-stu-id="a7b1c-146">6f680a37-00c6-41c7-a93f-1437e3462574</span></span> |
| <span data-ttu-id="a7b1c-147">workspaceKey (por exemplo)</span><span class="sxs-lookup"><span data-stu-id="a7b1c-147">workspaceKey (e.g)</span></span> | <span data-ttu-id="a7b1c-148">z4bU3p1/GrnWpQkky4gdabWXAhbWSTz70hm4m2Xt92XI+rSRgE8qVvRhsGo9TXffbrTahyrwv35W0pOqQAU7uQ==</span><span class="sxs-lookup"><span data-stu-id="a7b1c-148">z4bU3p1/GrnWpQkky4gdabWXAhbWSTz70hm4m2Xt92XI+rSRgE8qVvRhsGo9TXffbrTahyrwv35W0pOqQAU7uQ==</span></span> |


## <a name="template-deployment"></a><span data-ttu-id="a7b1c-149">Implantação de modelo</span><span class="sxs-lookup"><span data-stu-id="a7b1c-149">Template deployment</span></span>

<span data-ttu-id="a7b1c-150">Extensões de VM do Azure podem ser implantadas com modelos do Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="a7b1c-150">Azure VM extensions can be deployed with Azure Resource Manager templates.</span></span> <span data-ttu-id="a7b1c-151">Modelos são ideais ao implantar uma ou mais máquinas virtuais que exigem configuração pós-implantação, tal como integração ao OMS.</span><span class="sxs-lookup"><span data-stu-id="a7b1c-151">Templates are ideal when deploying one or more virtual machines that require post deployment configuration such as onboarding to OMS.</span></span> <span data-ttu-id="a7b1c-152">Um modelo do Resource Manager de exemplo que inclui a extensão de VM do agente do OMS pode ser encontrado na [Galeria de Início Rápido do Azure](https://github.com/Azure/azure-quickstart-templates/tree/master/201-oms-extension-ubuntu-vm).</span><span class="sxs-lookup"><span data-stu-id="a7b1c-152">A sample Resource Manager template that includes the OMS Agent VM extension can be found on the [Azure Quick Start Gallery](https://github.com/Azure/azure-quickstart-templates/tree/master/201-oms-extension-ubuntu-vm).</span></span> 

<span data-ttu-id="a7b1c-153">A configuração do JSON para uma extensão da máquina virtual pode ser aninhado dentro do recurso de máquina virtual ou localizado no nível de raiz ou superior de um modelo JSON do Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="a7b1c-153">The JSON configuration for a virtual machine extension can be nested inside the virtual machine resource, or placed at the root or top level of a Resource Manager JSON template.</span></span> <span data-ttu-id="a7b1c-154">O posicionamento da configuração do JSON afeta o valor do tipo e nome do recurso.</span><span class="sxs-lookup"><span data-stu-id="a7b1c-154">The placement of the JSON configuration affects the value of the resource name and type.</span></span> <span data-ttu-id="a7b1c-155">Para obter mais informações, consulte [Definir o nome e o tipo de recursos filho](../../azure-resource-manager/resource-manager-template-child-resource.md).</span><span class="sxs-lookup"><span data-stu-id="a7b1c-155">For more information, see [Set name and type for child resources](../../azure-resource-manager/resource-manager-template-child-resource.md).</span></span> 

<span data-ttu-id="a7b1c-156">O exemplo a seguir pressupõe que a extensão OMS esteja aninhada dentro do recurso de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="a7b1c-156">The following example assumes the OMS extension is nested inside the virtual machine resource.</span></span> <span data-ttu-id="a7b1c-157">Ao aninhar o recurso de extensão, o JSON é colocado no objeto `"resources": []` da máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="a7b1c-157">When nesting the extension resource, the JSON is placed in the `"resources": []` object of the virtual machine.</span></span>

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

<span data-ttu-id="a7b1c-158">Ao inserir o JSON da extensão na raiz do modelo, o nome do recurso inclui uma referência na máquina virtual pai e o tipo reflete a configuração aninhada.</span><span class="sxs-lookup"><span data-stu-id="a7b1c-158">When placing the extension JSON at the root of the template, the resource name includes a reference to the parent virtual machine, and the type reflects the nested configuration.</span></span>  

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

## <a name="azure-cli-deployment"></a><span data-ttu-id="a7b1c-159">Implantação da CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="a7b1c-159">Azure CLI deployment</span></span>

<span data-ttu-id="a7b1c-160">A CLI do Azure pode ser usado para implantar a extensão da VM do Agente do OMS para uma máquina virtual existente.</span><span class="sxs-lookup"><span data-stu-id="a7b1c-160">The Azure CLI can be used to deploy the OMS Agent VM extension to an existing virtual machine.</span></span> <span data-ttu-id="a7b1c-161">Substitua a chave e a ID do OMS por aqueles de seu espaço de trabalho do OMS.</span><span class="sxs-lookup"><span data-stu-id="a7b1c-161">Replace the OMS key and OMS ID with those from your OMS workspace.</span></span> 

```azurecli
az vm extension set \
  --resource-group myResourceGroup \
  --vm-name myVM \
  --name OmsAgentForLinux \
  --publisher Microsoft.EnterpriseCloud.Monitoring \
  --version 1.4 --protected-settings '{"workspaceKey": "omskey"}' \
  --settings '{"workspaceId": "omsid"}'
```

## <a name="troubleshoot-and-support"></a><span data-ttu-id="a7b1c-162">Solução de problemas e suporte</span><span class="sxs-lookup"><span data-stu-id="a7b1c-162">Troubleshoot and support</span></span>

### <a name="troubleshoot"></a><span data-ttu-id="a7b1c-163">Solucionar problemas</span><span class="sxs-lookup"><span data-stu-id="a7b1c-163">Troubleshoot</span></span>

<span data-ttu-id="a7b1c-164">Dados sobre o estado das implantações de extensão podem ser recuperados do Portal do Azure usando a CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="a7b1c-164">Data about the state of extension deployments can be retrieved from the Azure portal, and by using the Azure CLI.</span></span> <span data-ttu-id="a7b1c-165">Para ver o estado da implantação das extensões de uma determinada VM, execute o comando a seguir usando a CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="a7b1c-165">To see the deployment state of extensions for a given VM, run the following command using the Azure CLI.</span></span>

```azurecli
az vm extension list --resource-group myResourceGroup --vm-name myVM -o table
```

<span data-ttu-id="a7b1c-166">A saída de execução da extensão é registrada no seguinte arquivo:</span><span class="sxs-lookup"><span data-stu-id="a7b1c-166">Extension execution output is logged to the following file:</span></span>

```
/opt/microsoft/omsagent/bin/stdout
```

### <a name="error-codes-and-their-meanings"></a><span data-ttu-id="a7b1c-167">Códigos de erro e seus significados</span><span class="sxs-lookup"><span data-stu-id="a7b1c-167">Error codes and their meanings</span></span>

| <span data-ttu-id="a7b1c-168">Código do Erro</span><span class="sxs-lookup"><span data-stu-id="a7b1c-168">Error Code</span></span> | <span data-ttu-id="a7b1c-169">Significado</span><span class="sxs-lookup"><span data-stu-id="a7b1c-169">Meaning</span></span> | <span data-ttu-id="a7b1c-170">Ação possível</span><span class="sxs-lookup"><span data-stu-id="a7b1c-170">Possible Action</span></span> |
| :---: | --- | --- |
| <span data-ttu-id="a7b1c-171">10</span><span class="sxs-lookup"><span data-stu-id="a7b1c-171">10</span></span> | <span data-ttu-id="a7b1c-172">A VM já está conectada a um espaço de trabalho do OMS</span><span class="sxs-lookup"><span data-stu-id="a7b1c-172">VM is already connected to an OMS workspace</span></span> | <span data-ttu-id="a7b1c-173">Para conectar a VM ao espaço de trabalho especificado no esquema de extensão, defina stopOnMultipleConnections como falso nas configurações públicas ou remova esta propriedade.</span><span class="sxs-lookup"><span data-stu-id="a7b1c-173">To connect the VM to the workspace specified in the extension schema, set stopOnMultipleConnections to false in public settings or remove this property.</span></span> <span data-ttu-id="a7b1c-174">Essa VM é cobrada uma vez para cada espaço de trabalho ao qual está conectada.</span><span class="sxs-lookup"><span data-stu-id="a7b1c-174">This VM gets billed once for each workspace it is connected to.</span></span> |
| <span data-ttu-id="a7b1c-175">11</span><span class="sxs-lookup"><span data-stu-id="a7b1c-175">11</span></span> | <span data-ttu-id="a7b1c-176">Configuração inválida fornecida para a extensão</span><span class="sxs-lookup"><span data-stu-id="a7b1c-176">Invalid config provided to the extension</span></span> | <span data-ttu-id="a7b1c-177">Siga os exemplos anteriores para definir todos os valores de propriedade necessários para a implantação.</span><span class="sxs-lookup"><span data-stu-id="a7b1c-177">Follow the preceding examples to set all property values necessary for deployment.</span></span> |
| <span data-ttu-id="a7b1c-178">12</span><span class="sxs-lookup"><span data-stu-id="a7b1c-178">12</span></span> | <span data-ttu-id="a7b1c-179">O gerenciador de pacotes dpkg está bloqueado</span><span class="sxs-lookup"><span data-stu-id="a7b1c-179">The dpkg package manager is locked</span></span> | <span data-ttu-id="a7b1c-180">Verifique se todas as operações de atualização de dpkg no computador foram concluídas e tente novamente.</span><span class="sxs-lookup"><span data-stu-id="a7b1c-180">Make sure all dpkg update operations on the machine have finished and retry.</span></span> |
| <span data-ttu-id="a7b1c-181">20</span><span class="sxs-lookup"><span data-stu-id="a7b1c-181">20</span></span> | <span data-ttu-id="a7b1c-182">Habilitar chamado prematuramente</span><span class="sxs-lookup"><span data-stu-id="a7b1c-182">Enable called prematurely</span></span> | <span data-ttu-id="a7b1c-183">[Atualize o Agente Linux do Azure](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/update-agent) para a versão mais recente disponível.</span><span class="sxs-lookup"><span data-stu-id="a7b1c-183">[Update the Azure Linux Agent](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/update-agent) to the latest available version.</span></span> |
| <span data-ttu-id="a7b1c-184">51</span><span class="sxs-lookup"><span data-stu-id="a7b1c-184">51</span></span> | <span data-ttu-id="a7b1c-185">Não há suporte para essa extensão no sistema operacional da VM</span><span class="sxs-lookup"><span data-stu-id="a7b1c-185">This extension is not supported on the VM's operation system</span></span> | |
| <span data-ttu-id="a7b1c-186">55</span><span class="sxs-lookup"><span data-stu-id="a7b1c-186">55</span></span> | <span data-ttu-id="a7b1c-187">Não é possível conectar ao serviço do Microsoft Operations Management Suite</span><span class="sxs-lookup"><span data-stu-id="a7b1c-187">Cannot connect to the Microsoft Operations Management Suite service</span></span> | <span data-ttu-id="a7b1c-188">Verifique se o sistema tem acesso à Internet ou que um proxy HTTP válido foi fornecido.</span><span class="sxs-lookup"><span data-stu-id="a7b1c-188">Check that the system either has Internet access, or that a valid HTTP proxy has been provided.</span></span> <span data-ttu-id="a7b1c-189">Além disso, verifique a exatidão da ID do espaço de trabalho.</span><span class="sxs-lookup"><span data-stu-id="a7b1c-189">Additionally, check the correctness of the workspace ID.</span></span> |

<span data-ttu-id="a7b1c-190">Informações adicionais podem ser encontradas no [Guia de solução de problemas do OMS-Agent-for-Linux](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/Troubleshooting.md#).</span><span class="sxs-lookup"><span data-stu-id="a7b1c-190">Additional troubleshooting information can be found on the [OMS-Agent-for-Linux Troubleshooting Guide](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/Troubleshooting.md#).</span></span>

### <a name="support"></a><span data-ttu-id="a7b1c-191">Suporte</span><span class="sxs-lookup"><span data-stu-id="a7b1c-191">Support</span></span>

<span data-ttu-id="a7b1c-192">Caso precise de mais ajuda em qualquer ponto deste artigo, entre em contato com os especialistas do Azure nos [fóruns do Azure e do Stack Overflow no MSDN](https://azure.microsoft.com/en-us/support/forums/).</span><span class="sxs-lookup"><span data-stu-id="a7b1c-192">If you need more help at any point in this article, you can contact the Azure experts on the [MSDN Azure and Stack Overflow forums](https://azure.microsoft.com/en-us/support/forums/).</span></span> <span data-ttu-id="a7b1c-193">Como alternativa, você pode registrar um incidente de suporte do Azure.</span><span class="sxs-lookup"><span data-stu-id="a7b1c-193">Alternatively, you can file an Azure support incident.</span></span> <span data-ttu-id="a7b1c-194">Vá para o [site de suporte do Azure](https://azure.microsoft.com/en-us/support/options/) e selecione Obter suporte.</span><span class="sxs-lookup"><span data-stu-id="a7b1c-194">Go to the [Azure support site](https://azure.microsoft.com/en-us/support/options/) and select Get support.</span></span> <span data-ttu-id="a7b1c-195">Para saber mais sobre como usar o suporte do Azure, leia as [Perguntas frequentes sobre o suporte do Microsoft Azure](https://azure.microsoft.com/en-us/support/faq/).</span><span class="sxs-lookup"><span data-stu-id="a7b1c-195">For information about using Azure Support, read the [Microsoft Azure support FAQ](https://azure.microsoft.com/en-us/support/faq/).</span></span>
