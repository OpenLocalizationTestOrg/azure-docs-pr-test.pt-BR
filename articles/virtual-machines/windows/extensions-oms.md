---
title: "aaaOMS extensão de máquina virtual do Azure para Windows | Microsoft Docs"
description: "Implante o agente do OMS Olá na máquina virtual do Windows usando uma extensão de máquina virtual."
services: virtual-machines-windows
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: feae6176-2373-4034-b5d9-a32c6b4e1f10
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 03/14/2017
ms.author: nepeters
ms.openlocfilehash: 3000f66c0acdec1d1fad2125b8c6b72a92b1ec92
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="oms-virtual-machine-extension-for-windows"></a><span data-ttu-id="02cdc-103">Extensão da máquina virtual do OMS para Windows</span><span class="sxs-lookup"><span data-stu-id="02cdc-103">OMS virtual machine extension for Windows</span></span>

<span data-ttu-id="02cdc-104">O OMS (Operations Management Suite) fornece recursos de monitoramento, alertas e correção de alertas nos ativos locais e da nuvem.</span><span class="sxs-lookup"><span data-stu-id="02cdc-104">Operations Management Suite (OMS) provides monitoring, alerting, and alert remediation capabilities across cloud and on-premises assets.</span></span> <span data-ttu-id="02cdc-105">Olá extensão de máquina virtual do agente do OMS para Windows é publicada e suporte da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="02cdc-105">hello OMS Agent virtual machine extension for Windows is published and supported by Microsoft.</span></span> <span data-ttu-id="02cdc-106">extensão de saudação instala o agente do OMS Olá em máquinas virtuais do Azure e registra as máquinas virtuais em um espaço de trabalho existente do OMS.</span><span class="sxs-lookup"><span data-stu-id="02cdc-106">hello extension installs hello OMS agent on Azure virtual machines, and enrolls virtual machines into an existing OMS workspace.</span></span> <span data-ttu-id="02cdc-107">Saudação de detalhes neste documento suporte a plataformas, configurações e opções de implantação para Olá extensão de máquina virtual do OMS para Windows.</span><span class="sxs-lookup"><span data-stu-id="02cdc-107">This document details hello supported platforms, configurations, and deployment options for hello OMS virtual machine extension for Windows.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="02cdc-108">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="02cdc-108">Prerequisites</span></span>

### <a name="operating-system"></a><span data-ttu-id="02cdc-109">Sistema operacional</span><span class="sxs-lookup"><span data-stu-id="02cdc-109">Operating system</span></span>
<span data-ttu-id="02cdc-110">Olá extensão do agente do OMS para Windows podem ser executado em Windows Server 2008 R2, 2012, 2012 R2 e 2016 libera.</span><span class="sxs-lookup"><span data-stu-id="02cdc-110">hello OMS Agent extension for Windows can be run against Windows Server 2008 R2, 2012, 2012 R2, and 2016 releases.</span></span>

### <a name="internet-connectivity"></a><span data-ttu-id="02cdc-111">Conectividade com a Internet</span><span class="sxs-lookup"><span data-stu-id="02cdc-111">Internet connectivity</span></span>
<span data-ttu-id="02cdc-112">Olá extensão do agente do OMS para Windows requer que a máquina virtual Olá destino toohello conectado à internet.</span><span class="sxs-lookup"><span data-stu-id="02cdc-112">hello OMS Agent extension for Windows requires that hello target virtual machine is connected toohello internet.</span></span> 

## <a name="extension-schema"></a><span data-ttu-id="02cdc-113">Esquema de extensão</span><span class="sxs-lookup"><span data-stu-id="02cdc-113">Extension schema</span></span>

<span data-ttu-id="02cdc-114">Olá JSON a seguir mostra esquema Olá Olá extensão do agente do OMS.</span><span class="sxs-lookup"><span data-stu-id="02cdc-114">hello following JSON shows hello schema for hello OMS Agent extension.</span></span> <span data-ttu-id="02cdc-115">extensão de saudação requer a chave de Id e o espaço de trabalho de espaço de trabalho de saudação do espaço de trabalho do OMS Olá destino, eles podem ser encontrados no portal do OMS hello.</span><span class="sxs-lookup"><span data-stu-id="02cdc-115">hello extension requires hello workspace Id and workspace key from hello target OMS workspace, these can be found in hello OMS portal.</span></span> <span data-ttu-id="02cdc-116">Porque a chave do espaço de trabalho Olá deve ser tratado como dados confidenciais, devem ser armazenado em uma configuração protegida.</span><span class="sxs-lookup"><span data-stu-id="02cdc-116">Because hello workspace key should be treated as sensitive data, it should be stored in a protected setting configuration.</span></span> <span data-ttu-id="02cdc-117">Dados de configuração de extensão protegido de VM do Azure é criptografados e descriptografados apenas na máquina de virtual de destino hello.</span><span class="sxs-lookup"><span data-stu-id="02cdc-117">Azure VM extension protected setting data is encrypted, and only decrypted on hello target virtual machine.</span></span> <span data-ttu-id="02cdc-118">Observe que **workspaceId** e **workspaceKey** diferenciam maiúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="02cdc-118">Note that **workspaceId** and **workspaceKey** are case-sensitive.</span></span>

```json
{
    "type": "extensions",
    "name": "OMSExtension",
    "apiVersion": "[variables('apiVersion')]",
    "location": "[resourceGroup().location]",
    "dependsOn": [
        "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'))]"
    ],
    "properties": {
        "publisher": "Microsoft.EnterpriseCloud.Monitoring",
        "type": "MicrosoftMonitoringAgent",
        "typeHandlerVersion": "1.0",
        "autoUpgradeMinorVersion": true,
        "settings": {
            "workspaceId": "myWorkSpaceId"
        },
        "protectedSettings": {
            "workspaceKey": "myWorkspaceKey"
        }
    }
}
```
### <a name="property-values"></a><span data-ttu-id="02cdc-119">Valores de propriedade</span><span class="sxs-lookup"><span data-stu-id="02cdc-119">Property values</span></span>

| <span data-ttu-id="02cdc-120">Nome</span><span class="sxs-lookup"><span data-stu-id="02cdc-120">Name</span></span> | <span data-ttu-id="02cdc-121">Valor/Exemplo</span><span class="sxs-lookup"><span data-stu-id="02cdc-121">Value / Example</span></span> |
| ---- | ---- |
| <span data-ttu-id="02cdc-122">apiVersion</span><span class="sxs-lookup"><span data-stu-id="02cdc-122">apiVersion</span></span> | <span data-ttu-id="02cdc-123">2015-06-15</span><span class="sxs-lookup"><span data-stu-id="02cdc-123">2015-06-15</span></span> |
| <span data-ttu-id="02cdc-124">publicador</span><span class="sxs-lookup"><span data-stu-id="02cdc-124">publisher</span></span> | <span data-ttu-id="02cdc-125">Microsoft.EnterpriseCloud.Monitoring</span><span class="sxs-lookup"><span data-stu-id="02cdc-125">Microsoft.EnterpriseCloud.Monitoring</span></span> |
| <span data-ttu-id="02cdc-126">type</span><span class="sxs-lookup"><span data-stu-id="02cdc-126">type</span></span> | <span data-ttu-id="02cdc-127">MicrosoftMonitoringAgent</span><span class="sxs-lookup"><span data-stu-id="02cdc-127">MicrosoftMonitoringAgent</span></span> |
| <span data-ttu-id="02cdc-128">typeHandlerVersion</span><span class="sxs-lookup"><span data-stu-id="02cdc-128">typeHandlerVersion</span></span> | <span data-ttu-id="02cdc-129">1.0</span><span class="sxs-lookup"><span data-stu-id="02cdc-129">1.0</span></span> |
| <span data-ttu-id="02cdc-130">workspaceId (por exemplo)</span><span class="sxs-lookup"><span data-stu-id="02cdc-130">workspaceId (e.g)</span></span> | <span data-ttu-id="02cdc-131">6f680a37-00c6-41c7-a93f-1437e3462574</span><span class="sxs-lookup"><span data-stu-id="02cdc-131">6f680a37-00c6-41c7-a93f-1437e3462574</span></span> |
| <span data-ttu-id="02cdc-132">workspaceKey (por exemplo)</span><span class="sxs-lookup"><span data-stu-id="02cdc-132">workspaceKey (e.g)</span></span> | <span data-ttu-id="02cdc-133">z4bU3p1/GrnWpQkky4gdabWXAhbWSTz70hm4m2Xt92XI+rSRgE8qVvRhsGo9TXffbrTahyrwv35W0pOqQAU7uQ==</span><span class="sxs-lookup"><span data-stu-id="02cdc-133">z4bU3p1/GrnWpQkky4gdabWXAhbWSTz70hm4m2Xt92XI+rSRgE8qVvRhsGo9TXffbrTahyrwv35W0pOqQAU7uQ==</span></span> |

## <a name="template-deployment"></a><span data-ttu-id="02cdc-134">Implantação de modelo</span><span class="sxs-lookup"><span data-stu-id="02cdc-134">Template deployment</span></span>

<span data-ttu-id="02cdc-135">Extensões de VM do Azure podem ser implantadas com modelos do Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="02cdc-135">Azure VM extensions can be deployed with Azure Resource Manager templates.</span></span> <span data-ttu-id="02cdc-136">esquema JSON Olá detalhada na seção anterior Olá pode ser usada em uma saudação de toorun de modelo do Azure Resource Manager extensão do agente do OMS durante uma implantação de modelo do Gerenciador de recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="02cdc-136">hello JSON schema detailed in hello previous section can be used in an Azure Resource Manager template toorun hello OMS Agent extension during an Azure Resource Manager template deployment.</span></span> <span data-ttu-id="02cdc-137">Um modelo de exemplo que inclui a extensão de VM de agente do OMS Olá pode ser encontrado no hello [Galeria de início rápido do Azure](https://github.com/Azure/azure-quickstart-templates/tree/master/201-oms-extension-windows-vm).</span><span class="sxs-lookup"><span data-stu-id="02cdc-137">A sample template that includes hello OMS Agent VM extension can be found on hello [Azure Quick Start Gallery](https://github.com/Azure/azure-quickstart-templates/tree/master/201-oms-extension-windows-vm).</span></span> 

<span data-ttu-id="02cdc-138">Olá JSON para uma extensão de máquina virtual pode ser aninhado dentro do recurso de máquina virtual de saudação ou colocado na raiz de saudação ou de nível superior de um modelo JSON do Gerenciador de recursos.</span><span class="sxs-lookup"><span data-stu-id="02cdc-138">hello JSON for a virtual machine extension can be nested inside hello virtual machine resource, or placed at hello root or top level of a Resource Manager JSON template.</span></span> <span data-ttu-id="02cdc-139">posicionamento de saudação do hello JSON afeta o valor de saudação do nome do recurso hello e tipo.</span><span class="sxs-lookup"><span data-stu-id="02cdc-139">hello placement of hello JSON affects hello value of hello resource name and type.</span></span> <span data-ttu-id="02cdc-140">Para obter mais informações, consulte [Definir o nome e o tipo de recursos filho](../../azure-resource-manager/resource-manager-template-child-resource.md).</span><span class="sxs-lookup"><span data-stu-id="02cdc-140">For more information, see [Set name and type for child resources](../../azure-resource-manager/resource-manager-template-child-resource.md).</span></span> 

<span data-ttu-id="02cdc-141">Olá exemplo a seguir supõe extensão do OMS hello está aninhado em Olá recurso da máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="02cdc-141">hello following example assumes hello OMS extension is nested inside hello virtual machine resource.</span></span> <span data-ttu-id="02cdc-142">Ao aninhar o recurso de extensão hello, Olá JSON é colocado no hello `"resources": []` objeto da máquina virtual de saudação.</span><span class="sxs-lookup"><span data-stu-id="02cdc-142">When nesting hello extension resource, hello JSON is placed in hello `"resources": []` object of hello virtual machine.</span></span>


```json
{
    "type": "extensions",
    "name": "OMSExtension",
    "apiVersion": "[variables('apiVersion')]",
    "location": "[resourceGroup().location]",
    "dependsOn": [
        "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'))]"
    ],
    "properties": {
        "publisher": "Microsoft.EnterpriseCloud.Monitoring",
        "type": "MicrosoftMonitoringAgent",
        "typeHandlerVersion": "1.0",
        "autoUpgradeMinorVersion": true,
        "settings": {
            "workspaceId": "myWorkSpaceId"
        },
        "protectedSettings": {
            "workspaceKey": "myWorkspaceKey"
        }
    }
}
```

<span data-ttu-id="02cdc-143">Ao inserir extensão Olá JSON na raiz de saudação do modelo Olá, nome do recurso de saudação inclui uma máquina virtual do referência toohello pai e tipo hello reflete configuração aninhada Olá.</span><span class="sxs-lookup"><span data-stu-id="02cdc-143">When placing hello extension JSON at hello root of hello template, hello resource name includes a reference toohello parent virtual machine, and hello type reflects hello nested configuration.</span></span> 

```json
{
    "type": "Microsoft.Compute/virtualMachines/extensions",
    "name": "<parentVmResource>/OMSExtension",
    "apiVersion": "[variables('apiVersion')]",
    "location": "[resourceGroup().location]",
    "dependsOn": [
        "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'))]"
    ],
    "properties": {
        "publisher": "Microsoft.EnterpriseCloud.Monitoring",
        "type": "MicrosoftMonitoringAgent",
        "typeHandlerVersion": "1.0",
        "autoUpgradeMinorVersion": true,
        "settings": {
            "workspaceId": "myWorkSpaceId"
        },
        "protectedSettings": {
            "workspaceKey": "myWorkspaceKey"
        }
    }
}
```

## <a name="powershell-deployment"></a><span data-ttu-id="02cdc-144">Implantação do PowerShell</span><span class="sxs-lookup"><span data-stu-id="02cdc-144">PowerShell deployment</span></span>

<span data-ttu-id="02cdc-145">Olá `Set-AzureRmVMExtension` comando pode ser usado toodeploy Olá agente do OMS máquina virtual extensão tooan máquina virtual existente.</span><span class="sxs-lookup"><span data-stu-id="02cdc-145">hello `Set-AzureRmVMExtension` command can be used toodeploy hello OMS Agent virtual machine extension tooan existing virtual machine.</span></span> <span data-ttu-id="02cdc-146">Antes de executar o comando hello, configurações públicas e privadas de saudação necessário toobe armazenado em uma tabela de hash do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="02cdc-146">Before running hello command, hello public and private configurations need toobe stored in a PowerShell hash table.</span></span> 

```powershell
$PublicSettings = @{"workspaceId" = "myWorkspaceId"}
$ProtectedSettings = @{"workspaceKey" = "myWorkspaceKey"}

Set-AzureRmVMExtension -ExtensionName "Microsoft.EnterpriseCloud.Monitoring" `
    -ResourceGroupName "myResourceGroup" `
    -VMName "myVM" `
    -Publisher "Microsoft.EnterpriseCloud.Monitoring" `
    -ExtensionType "MicrosoftMonitoringAgent" `
    -TypeHandlerVersion 1.0 `
    -Settings $PublicSettings `
    -ProtectedSettings $ProtectedSettings `
    -Location WestUS ` 
```

## <a name="troubleshoot-and-support"></a><span data-ttu-id="02cdc-147">Solução de problemas e suporte</span><span class="sxs-lookup"><span data-stu-id="02cdc-147">Troubleshoot and support</span></span>

### <a name="troubleshoot"></a><span data-ttu-id="02cdc-148">Solucionar problemas</span><span class="sxs-lookup"><span data-stu-id="02cdc-148">Troubleshoot</span></span>

<span data-ttu-id="02cdc-149">Dados sobre o estado de saudação de implantações de extensão podem ser recuperados da saudação portal do Azure e usando o módulo do PowerShell do Azure hello.</span><span class="sxs-lookup"><span data-stu-id="02cdc-149">Data about hello state of extension deployments can be retrieved from hello Azure portal, and by using hello Azure PowerShell module.</span></span> <span data-ttu-id="02cdc-150">estado da implantação Olá toosee de extensões para uma determinada VM, Olá execução usando o comando a seguir Olá módulo PowerShell do Azure.</span><span class="sxs-lookup"><span data-stu-id="02cdc-150">toosee hello deployment state of extensions for a given VM, run hello following command using hello Azure PowerShell module.</span></span>

```powershell
Get-AzureRmVMExtension -ResourceGroupName myResourceGroup -VMName myVM -Name myExtensionName
```

<span data-ttu-id="02cdc-151">Execução de extensão é conectado toofiles encontrado no hello após o diretório de saída:</span><span class="sxs-lookup"><span data-stu-id="02cdc-151">Extension execution output is logged toofiles found in hello following directory:</span></span>

```cmd
C:\WindowsAzure\Logs\Plugins\Microsoft.EnterpriseCloud.Monitoring.MicrosoftMonitoringAgent\
```

### <a name="support"></a><span data-ttu-id="02cdc-152">Suporte</span><span class="sxs-lookup"><span data-stu-id="02cdc-152">Support</span></span>

<span data-ttu-id="02cdc-153">Se você precisar de mais ajuda a qualquer momento neste artigo, você pode contatar hello Azure especialistas em Olá [fóruns MSDN Azure e o estouro de pilha](https://azure.microsoft.com/en-us/support/forums/).</span><span class="sxs-lookup"><span data-stu-id="02cdc-153">If you need more help at any point in this article, you can contact hello Azure experts on hello [MSDN Azure and Stack Overflow forums](https://azure.microsoft.com/en-us/support/forums/).</span></span> <span data-ttu-id="02cdc-154">Como alternativa, você pode registrar um incidente de suporte do Azure.</span><span class="sxs-lookup"><span data-stu-id="02cdc-154">Alternatively, you can file an Azure support incident.</span></span> <span data-ttu-id="02cdc-155">Vá toohello [site de suporte do Azure](https://azure.microsoft.com/en-us/support/options/) e selecione obter suporte.</span><span class="sxs-lookup"><span data-stu-id="02cdc-155">Go toohello [Azure support site](https://azure.microsoft.com/en-us/support/options/) and select Get support.</span></span> <span data-ttu-id="02cdc-156">Para obter informações sobre como usar o suporte do Azure, leia Olá [perguntas frequentes sobre o suporte da Microsoft Azure](https://azure.microsoft.com/en-us/support/faq/).</span><span class="sxs-lookup"><span data-stu-id="02cdc-156">For information about using Azure Support, read hello [Microsoft Azure support FAQ](https://azure.microsoft.com/en-us/support/faq/).</span></span>
