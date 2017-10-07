---
title: "Grupos de recursos do Azure que contêm extensões de VM do aaaExporting | Microsoft Docs"
description: "Exporte modelos do Resource Manager que incluem as extensões da máquina virtual."
services: virtual-machines-windows
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 7f4e2ca6-f1c7-4f59-a2cc-8f63132de279
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 12/05/2016
ms.author: nepeters
ms.openlocfilehash: cdbc2030988a19fe68429e8733dc60536c264abf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="exporting-resource-groups-that-contain-vm-extensions"></a><span data-ttu-id="4da5e-103">Exportar Grupos de Recursos que contêm extensões de VM</span><span class="sxs-lookup"><span data-stu-id="4da5e-103">Exporting Resource Groups that contain VM extensions</span></span>

<span data-ttu-id="4da5e-104">Os Grupos de Recursos do Azure podem ser exportados para um novo modelo do Resource Manager que, depois, pode ser reimplantado.</span><span class="sxs-lookup"><span data-stu-id="4da5e-104">Azure Resource Groups can be exported into a new Resource Manager template that can then be redeployed.</span></span> <span data-ttu-id="4da5e-105">Olá processo de exportação interpreta os recursos existentes e cria um modelo do Gerenciador de recursos que quando implantado resulta em um grupo de recursos semelhantes.</span><span class="sxs-lookup"><span data-stu-id="4da5e-105">hello export process interprets existing resources, and creates a Resource Manager template that when deployed results in a similar Resource Group.</span></span> <span data-ttu-id="4da5e-106">Ao usar a opção de exportação de grupo de recursos de saudação em relação a um grupo de recursos que contém as extensões de máquina Virtual, vários toobe necessidade de itens considerado como compatibilidade de extensão e protegido configurações.</span><span class="sxs-lookup"><span data-stu-id="4da5e-106">When using hello Resource Group export option against a Resource Group containing Virtual Machine extensions, several items need toobe considered such as extension compatibility and protected settings.</span></span>

<span data-ttu-id="4da5e-107">Este documento detalha como funciona o processo de exportação do grupo de recursos de saudação sobre extensões de máquina virtual, incluindo uma lista de extensões de suporte, e detalhes sobre o tratamento seguro dados.</span><span class="sxs-lookup"><span data-stu-id="4da5e-107">This document details how hello Resource Group export process works regarding virtual machine extensions, including a list of supported extensions, and details on handling secured data.</span></span>

## <a name="supported-virtual-machine-extensions"></a><span data-ttu-id="4da5e-108">Extensões da máquina virtual com suporte</span><span class="sxs-lookup"><span data-stu-id="4da5e-108">Supported Virtual Machine Extensions</span></span>

<span data-ttu-id="4da5e-109">Há muitas extensões da máquina virtual disponíveis.</span><span class="sxs-lookup"><span data-stu-id="4da5e-109">Many Virtual Machine extensions are available.</span></span> <span data-ttu-id="4da5e-110">Nem todas as extensões podem ser exportadas para um modelo do Gerenciador de recursos usando o recurso de "Script de automação" hello.</span><span class="sxs-lookup"><span data-stu-id="4da5e-110">Not all extensions can be exported into a Resource Manager template using hello “Automation Script” feature.</span></span> <span data-ttu-id="4da5e-111">Não há suporte para uma extensão de máquina virtual, precisa toobe manualmente colocado de volta em modelo exportado hello.</span><span class="sxs-lookup"><span data-stu-id="4da5e-111">If a virtual machine extension is not supported, it needs toobe manually placed back into hello exported template.</span></span>

<span data-ttu-id="4da5e-112">Olá extensões a seguir podem ser exportadas com o recurso de script de automação de saudação.</span><span class="sxs-lookup"><span data-stu-id="4da5e-112">hello following extensions can be exported with hello automation script feature.</span></span>

| <span data-ttu-id="4da5e-113">Extensão</span><span class="sxs-lookup"><span data-stu-id="4da5e-113">Extension</span></span> ||||
|---|---|---|---|
| <span data-ttu-id="4da5e-114">Acronis Backup</span><span class="sxs-lookup"><span data-stu-id="4da5e-114">Acronis Backup</span></span> | <span data-ttu-id="4da5e-115">Datadog Windows Agent</span><span class="sxs-lookup"><span data-stu-id="4da5e-115">Datadog Windows Agent</span></span> | <span data-ttu-id="4da5e-116">OS Patching For Linux</span><span class="sxs-lookup"><span data-stu-id="4da5e-116">OS Patching For Linux</span></span> | <span data-ttu-id="4da5e-117">VM Snapshot Linux</span><span class="sxs-lookup"><span data-stu-id="4da5e-117">VM Snapshot Linux</span></span>
| <span data-ttu-id="4da5e-118">Acronis Backup Linux</span><span class="sxs-lookup"><span data-stu-id="4da5e-118">Acronis Backup Linux</span></span> | <span data-ttu-id="4da5e-119">Extensão do Docker</span><span class="sxs-lookup"><span data-stu-id="4da5e-119">Docker Extension</span></span> | <span data-ttu-id="4da5e-120">Puppet Agent</span><span class="sxs-lookup"><span data-stu-id="4da5e-120">Puppet Agent</span></span> |
| <span data-ttu-id="4da5e-121">Bg Info</span><span class="sxs-lookup"><span data-stu-id="4da5e-121">Bg Info</span></span> | <span data-ttu-id="4da5e-122">DSC Extension</span><span class="sxs-lookup"><span data-stu-id="4da5e-122">DSC Extension</span></span> | <span data-ttu-id="4da5e-123">Site 24x7 Apm Insight</span><span class="sxs-lookup"><span data-stu-id="4da5e-123">Site 24x7 Apm Insight</span></span> |
| <span data-ttu-id="4da5e-124">BMC CTM Agent Linux</span><span class="sxs-lookup"><span data-stu-id="4da5e-124">BMC CTM Agent Linux</span></span> | <span data-ttu-id="4da5e-125">Dynatrace Linux</span><span class="sxs-lookup"><span data-stu-id="4da5e-125">Dynatrace Linux</span></span> | <span data-ttu-id="4da5e-126">Site 24x7 Linux Server</span><span class="sxs-lookup"><span data-stu-id="4da5e-126">Site 24x7 Linux Server</span></span> |
| <span data-ttu-id="4da5e-127">BMC CTM Agent Windows</span><span class="sxs-lookup"><span data-stu-id="4da5e-127">BMC CTM Agent Windows</span></span> | <span data-ttu-id="4da5e-128">Dynatrace Windows</span><span class="sxs-lookup"><span data-stu-id="4da5e-128">Dynatrace Windows</span></span> | <span data-ttu-id="4da5e-129">Site 24x7 Windows Server</span><span class="sxs-lookup"><span data-stu-id="4da5e-129">Site 24x7 Windows Server</span></span> |
| <span data-ttu-id="4da5e-130">Chef Client</span><span class="sxs-lookup"><span data-stu-id="4da5e-130">Chef Client</span></span> | <span data-ttu-id="4da5e-131">HPE Security Application Defender</span><span class="sxs-lookup"><span data-stu-id="4da5e-131">HPE Security Application Defender</span></span> | <span data-ttu-id="4da5e-132">Trend Micro DSA</span><span class="sxs-lookup"><span data-stu-id="4da5e-132">Trend Micro DSA</span></span> |
| <span data-ttu-id="4da5e-133">Custom Script</span><span class="sxs-lookup"><span data-stu-id="4da5e-133">Custom Script</span></span> | <span data-ttu-id="4da5e-134">IaaS Antimalware</span><span class="sxs-lookup"><span data-stu-id="4da5e-134">IaaS Antimalware</span></span> | <span data-ttu-id="4da5e-135">Trend Micro DSA Linux</span><span class="sxs-lookup"><span data-stu-id="4da5e-135">Trend Micro DSA Linux</span></span> |
| <span data-ttu-id="4da5e-136">Extensão de script personalizado</span><span class="sxs-lookup"><span data-stu-id="4da5e-136">Custom Script Extension</span></span> | <span data-ttu-id="4da5e-137">Diagnóstico do IaaS</span><span class="sxs-lookup"><span data-stu-id="4da5e-137">IaaS Diagnostics</span></span> | <span data-ttu-id="4da5e-138">Acesso de VM para Linux</span><span class="sxs-lookup"><span data-stu-id="4da5e-138">VM Access For Linux</span></span> |
| <span data-ttu-id="4da5e-139">Script Personalizado para Linux</span><span class="sxs-lookup"><span data-stu-id="4da5e-139">Custom Script for Linux</span></span> | <span data-ttu-id="4da5e-140">Linux Chef Client</span><span class="sxs-lookup"><span data-stu-id="4da5e-140">Linux Chef Client</span></span> | <span data-ttu-id="4da5e-141">Acesso de VM para Linux</span><span class="sxs-lookup"><span data-stu-id="4da5e-141">VM Access For Linux</span></span> |
| <span data-ttu-id="4da5e-142">Datadog Linux Agent</span><span class="sxs-lookup"><span data-stu-id="4da5e-142">Datadog Linux Agent</span></span> | <span data-ttu-id="4da5e-143">Diagnóstico do Linux</span><span class="sxs-lookup"><span data-stu-id="4da5e-143">Linux Diagnostic</span></span> | <span data-ttu-id="4da5e-144">VM Snapshot</span><span class="sxs-lookup"><span data-stu-id="4da5e-144">VM Snapshot</span></span> |

## <a name="export-hello-resource-group"></a><span data-ttu-id="4da5e-145">Saudação de exportação de grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="4da5e-145">Export hello Resource Group</span></span>

<span data-ttu-id="4da5e-146">tooexport um grupo de recursos em um modelo reutilizável, Olá concluir as etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="4da5e-146">tooexport a Resource Group into a reusable template, complete hello following steps:</span></span>

1. <span data-ttu-id="4da5e-147">Entrar toohello portal do Azure</span><span class="sxs-lookup"><span data-stu-id="4da5e-147">Sign in toohello Azure portal</span></span>
2. <span data-ttu-id="4da5e-148">No hello Menu Hub, clique em grupos de recursos</span><span class="sxs-lookup"><span data-stu-id="4da5e-148">On hello Hub Menu, click Resource Groups</span></span>
3. <span data-ttu-id="4da5e-149">Selecione o grupo de recursos de destino de saudação da lista de saudação</span><span class="sxs-lookup"><span data-stu-id="4da5e-149">Select hello target resource group from hello list</span></span>
4. <span data-ttu-id="4da5e-150">Na folha de grupo de recursos de saudação, clique em Script de automação</span><span class="sxs-lookup"><span data-stu-id="4da5e-150">In hello Resource Group blade, click Automation Script</span></span>

![Exportação de modelo](./media/extensions-export-templates/template-export.png)

<span data-ttu-id="4da5e-152">Olá script do Azure Resource Manager automações produz um modelo do Gerenciador de recursos, um arquivo de parâmetros e vários scripts de implantação de exemplo, como o PowerShell e a CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="4da5e-152">hello Azure Resource Manager automations script produces a Resource Manager template, a parameters file, and several sample deployment scripts such as PowerShell and Azure CLI.</span></span> <span data-ttu-id="4da5e-153">Neste ponto, modelo exportado Olá pode ser obtido com o botão de download hello, adicionado como uma biblioteca de modelos de toohello modelo novo ou reimplantado com hello botão implantar.</span><span class="sxs-lookup"><span data-stu-id="4da5e-153">At this point, hello exported template can be downloaded using hello download button, added as a new template toohello template library, or redeployed using hello deploy button.</span></span>

## <a name="configure-protected-settings"></a><span data-ttu-id="4da5e-154">Definir as configurações protegidas</span><span class="sxs-lookup"><span data-stu-id="4da5e-154">Configure protected settings</span></span>

<span data-ttu-id="4da5e-155">Muitas extensões da máquina virtual do Azure incluem uma definição de configurações protegidas que criptografa dados confidenciais, como credenciais e cadeias de configuração.</span><span class="sxs-lookup"><span data-stu-id="4da5e-155">Many Azure virtual machine extensions include a protected settings configuration, that encrypts sensitive data such as credentials and configuration strings.</span></span> <span data-ttu-id="4da5e-156">Configurações protegidas não são exportadas com o script de automação de saudação.</span><span class="sxs-lookup"><span data-stu-id="4da5e-156">Protected settings are not exported with hello automation script.</span></span> <span data-ttu-id="4da5e-157">Se precisam de configurações necessárias e protegidas toobe reinserida hello exportada modelado.</span><span class="sxs-lookup"><span data-stu-id="4da5e-157">If necessary, protected settings need toobe reinserted into hello exported templated.</span></span>

### <a name="step-1---remove-template-parameter"></a><span data-ttu-id="4da5e-158">Etapa 1: Remover o parâmetro de modelo</span><span class="sxs-lookup"><span data-stu-id="4da5e-158">Step 1 - Remove template parameter</span></span>

<span data-ttu-id="4da5e-159">Quando saudação do que grupo de recursos é exportado, um parâmetro de modelo único é criada tooprovide toohello um valor exportado configurações protegidas.</span><span class="sxs-lookup"><span data-stu-id="4da5e-159">When hello Resource Group is exported, a single template parameter is created tooprovide a value toohello exported protected settings.</span></span> <span data-ttu-id="4da5e-160">Esse parâmetro pode ser removido.</span><span class="sxs-lookup"><span data-stu-id="4da5e-160">This parameter can be removed.</span></span> <span data-ttu-id="4da5e-161">parâmetro de saudação tooremove, examine a lista de parâmetros de saudação e excluir parâmetro hello que parece semelhante exemplo JSON toothis.</span><span class="sxs-lookup"><span data-stu-id="4da5e-161">tooremove hello parameter, look through hello parameter list and delete hello parameter that looks similar toothis JSON example.</span></span>

```json
"extensions_extensionname_protectedSettings": {
    "defaultValue": null,
    "type": "SecureObject"
}
```

### <a name="step-2---get-protected-settings-properties"></a><span data-ttu-id="4da5e-162">Etapa 2: Obter as propriedades das configurações protegidas</span><span class="sxs-lookup"><span data-stu-id="4da5e-162">Step 2 - Get protected settings properties</span></span>

<span data-ttu-id="4da5e-163">Como cada configuração protegido tem um conjunto de propriedades obrigatórias, uma lista dessas propriedades necessário toobe coletada.</span><span class="sxs-lookup"><span data-stu-id="4da5e-163">Because each protected setting has a set of required properties, a list of these properties need toobe gathered.</span></span> <span data-ttu-id="4da5e-164">Cada parâmetro de configuração de configurações protegidas de saudação pode ser encontrado no hello [esquema do Gerenciador de recursos do Azure no GitHub](https://raw.githubusercontent.com/Azure/azure-resource-manager-schemas/master/schemas/2015-08-01/Microsoft.Compute.json).</span><span class="sxs-lookup"><span data-stu-id="4da5e-164">Each parameter of hello protected settings configuration can be found in hello [Azure Resource Manager schema on GitHub](https://raw.githubusercontent.com/Azure/azure-resource-manager-schemas/master/schemas/2015-08-01/Microsoft.Compute.json).</span></span> <span data-ttu-id="4da5e-165">Esse esquema inclui apenas conjuntos de parâmetros Olá para extensões de saudação listadas na seção de visão geral de saudação deste documento.</span><span class="sxs-lookup"><span data-stu-id="4da5e-165">This schema only includes hello parameter sets for hello extensions listed in hello overview section of this document.</span></span> 

<span data-ttu-id="4da5e-166">De dentro do repositório de esquema Olá, procurar extensão Olá desejado, para este exemplo `IaaSDiagnostics`.</span><span class="sxs-lookup"><span data-stu-id="4da5e-166">From within hello schema repository, search for hello desired extension, for this example `IaaSDiagnostics`.</span></span> <span data-ttu-id="4da5e-167">Uma vez Olá extensões `protectedSettings` objeto foi localizado, tome nota de cada parâmetro.</span><span class="sxs-lookup"><span data-stu-id="4da5e-167">Once hello extensions `protectedSettings` object has been located, take note of each parameter.</span></span> <span data-ttu-id="4da5e-168">No exemplo de saudação do hello `IaasDiagnostic` extensão, Olá requer que os parâmetros são `storageAccountName`, `storageAccountKey`, e `storageAccountEndPoint`.</span><span class="sxs-lookup"><span data-stu-id="4da5e-168">In hello example of hello `IaasDiagnostic` extension, hello require parameters are `storageAccountName`, `storageAccountKey`, and `storageAccountEndPoint`.</span></span>

```json
"protectedSettings": {
    "type": "object",
    "properties": {
        "storageAccountName": {
            "type": "string"
        },
        "storageAccountKey": {
            "type": "string"
        },
        "storageAccountEndPoint": {
            "type": "string"
        }
    },
    "required": [
        "storageAccountName",
        "storageAccountKey",
        "storageAccountEndPoint"
    ]
}
```

### <a name="step-3---re-create-hello-protected-configuration"></a><span data-ttu-id="4da5e-169">Etapa 3 - configuração de saudação protegida recriar</span><span class="sxs-lookup"><span data-stu-id="4da5e-169">Step 3 - Re-create hello protected configuration</span></span>

<span data-ttu-id="4da5e-170">No modelo exportado de hello, procure `protectedSettings` e substitua hello exportada protegido de configuração do objeto com um novo que inclui parâmetros de extensão Olá necessário e um valor para cada um.</span><span class="sxs-lookup"><span data-stu-id="4da5e-170">On hello exported template, search for `protectedSettings` and replace hello exported protected setting object with a new one that includes hello required extension parameters and a value for each one.</span></span>

<span data-ttu-id="4da5e-171">No exemplo de saudação do hello `IaasDiagnostic` extensão, Olá novo protegido configuração seria semelhante a saudação de exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="4da5e-171">In hello example of hello `IaasDiagnostic` extension, hello new protected setting configuration would look like hello following example:</span></span>

```json
"protectedSettings": {
    "storageAccountName": "[parameters('storageAccountName')]",
    "storageAccountKey": "[parameters('storageAccountKey')]",
    "storageAccountEndPoint": "https://core.windows.net"
}
```

<span data-ttu-id="4da5e-172">recurso de extensão final Olá parece semelhante toohello JSON de exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="4da5e-172">hello final extension resource looks similar toohello following JSON example:</span></span>

```json
{
    "name": "Microsoft.Insights.VMDiagnosticsSettings",
    "type": "extensions",
    "location": "[resourceGroup().location]",
    "apiVersion": "[variables('apiVersion')]",
    "dependsOn": [
        "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'))]"
    ],
    "tags": {
        "displayName": "AzureDiagnostics"
    },
    "properties": {
        "publisher": "Microsoft.Azure.Diagnostics",
        "type": "IaaSDiagnostics",
        "typeHandlerVersion": "1.5",
        "autoUpgradeMinorVersion": true,
        "settings": {
            "xmlCfg": "[base64(concat(variables('wadcfgxstart'), variables('wadmetricsresourceid'), variables('vmName'), variables('wadcfgxend')))]",
            "storageAccount": "[parameters('existingdiagnosticsStorageAccountName')]"
        },
        "protectedSettings": {
            "storageAccountName": "[parameters('storageAccountName')]",
            "storageAccountKey": "[parameters('storageAccountKey')]",
            "storageAccountEndPoint": "https://core.windows.net"
        }
    }
}
```

<span data-ttu-id="4da5e-173">Se usar os valores de propriedade de tooprovide de parâmetros de modelo, será necessário toobe criado.</span><span class="sxs-lookup"><span data-stu-id="4da5e-173">If using template parameters tooprovide property values, these need toobe created.</span></span> <span data-ttu-id="4da5e-174">Ao criar parâmetros de modelo para definir valores de protegido, verifique Olá de toouse-se de que `SecureString` tipo de parâmetro para que os valores confidenciais são protegidos.</span><span class="sxs-lookup"><span data-stu-id="4da5e-174">When creating template parameters for protected setting values, make sure toouse hello `SecureString` parameter type so that sensitive values are secured.</span></span> <span data-ttu-id="4da5e-175">Para saber mais sobre como usar parâmetros, confira [Criação de modelos do Azure Resource Manager](../../resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="4da5e-175">For more information on using parameters, see [Authoring Azure Resource Manager templates](../../resource-group-authoring-templates.md).</span></span>

<span data-ttu-id="4da5e-176">No exemplo de saudação do hello `IaasDiagnostic` extensão, Olá parâmetros a seguir seria criado na seção de parâmetros de saudação do modelo do Gerenciador de recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="4da5e-176">In hello example of hello `IaasDiagnostic` extension, hello following parameters would be created in hello parameters section of hello Resource Manager template.</span></span>

```json
"storageAccountName": {
    "defaultValue": null,
    "type": "SecureString"
},
"storageAccountKey": {
    "defaultValue": null,
    "type": "SecureString"
}
```

<span data-ttu-id="4da5e-177">Neste ponto, o modelo de saudação pode ser implantado usando qualquer método de implantação de modelo.</span><span class="sxs-lookup"><span data-stu-id="4da5e-177">At this point, hello template can be deployed using any template deployment method.</span></span>
