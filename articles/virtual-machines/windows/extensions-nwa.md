---
title: "aaaAzure extensão de máquina virtual do agente do Inspetor de rede para Windows | Microsoft Docs"
description: "Implante Olá agente do Inspetor de rede na máquina virtual do Windows usando uma extensão de máquina virtual."
services: virtual-machines-windows
documentationcenter: 
author: dennisg
manager: amku
editor: 
tags: azure-resource-manager
ms.assetid: 27e46af7-2150-45e8-b084-ba33de8c5e3f
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 02/14/2017
ms.author: dennisg
ms.openlocfilehash: 21298706e462ff32c4d314f9a1ad127074ddf481
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="network-watcher-agent-virtual-machine-extension-for-windows"></a><span data-ttu-id="08551-103">Extensão da máquina virtual do Agente do Observador de Rede para Windows</span><span class="sxs-lookup"><span data-stu-id="08551-103">Network Watcher Agent virtual machine extension for Windows</span></span>

## <a name="overview"></a><span data-ttu-id="08551-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="08551-104">Overview</span></span>

<span data-ttu-id="08551-105">[Observador de Rede do Azure](https://review.docs.microsoft.com/en-us/azure/network-watcher/) é um serviço de monitoramento de desempenho, diagnóstico e análise de rede que permite o monitoramento de redes do Azure.</span><span class="sxs-lookup"><span data-stu-id="08551-105">[Azure Network Watcher](https://review.docs.microsoft.com/en-us/azure/network-watcher/) is a network performance monitoring, diagnostic, and analytics service that allows monitoring for Azure networks.</span></span> <span data-ttu-id="08551-106">Olá extensão do agente do Inspetor de rede de máquina virtual é um requisito para alguns dos recursos de rede Inspetor Olá em máquinas virtuais do Azure.</span><span class="sxs-lookup"><span data-stu-id="08551-106">hello Network Watcher Agent virtual machine extension is a requirement for some of hello Network Watcher features on Azure virtual machines.</span></span> <span data-ttu-id="08551-107">Isso inclui capturar o tráfego de rede sob demanda e outras funcionalidades avançadas.</span><span class="sxs-lookup"><span data-stu-id="08551-107">This includes capturing network traffic on demand and other advanced functionality.</span></span>

<span data-ttu-id="08551-108">Saudação de detalhes neste documento suporte a plataformas e opções de implantação para Olá extensão do agente do Inspetor de rede de máquina virtual para Windows.</span><span class="sxs-lookup"><span data-stu-id="08551-108">This document details hello supported platforms and deployment options for hello Network Watcher Agent virtual machine extension for Windows.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="08551-109">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="08551-109">Prerequisites</span></span>

### <a name="operating-system"></a><span data-ttu-id="08551-110">Sistema operacional</span><span class="sxs-lookup"><span data-stu-id="08551-110">Operating system</span></span>

<span data-ttu-id="08551-111">Olá extensão do agente do Inspetor de rede para Windows podem ser executado em Windows Server 2008 R2, 2012, 2012 R2 e 2016 libera.</span><span class="sxs-lookup"><span data-stu-id="08551-111">hello Network Watcher Agent extension for Windows can be run against Windows Server 2008 R2, 2012, 2012 R2, and 2016 releases.</span></span> <span data-ttu-id="08551-112">Observe que Olá Nano Server não é suportado no momento.</span><span class="sxs-lookup"><span data-stu-id="08551-112">Note that hello Nano Server is not supported at this time.</span></span>

### <a name="internet-connectivity"></a><span data-ttu-id="08551-113">Conectividade com a Internet</span><span class="sxs-lookup"><span data-stu-id="08551-113">Internet connectivity</span></span>

<span data-ttu-id="08551-114">Alguns Olá funcionalidade de agente do Inspetor de rede requer que a máquina virtual Olá destino ser toohello conectado à Internet.</span><span class="sxs-lookup"><span data-stu-id="08551-114">Some of hello Network Watcher Agent functionality requires that hello target virtual machine be connected toohello Internet.</span></span> <span data-ttu-id="08551-115">Sem conexões de saída Olá capacidade tooestablish alguns dos recursos de agente do Inspetor de rede Olá podem mau funcionamento ou se tornar indisponível.</span><span class="sxs-lookup"><span data-stu-id="08551-115">Without hello ability tooestablish outgoing connections some of hello Network Watcher Agent features may malfunction or become unavailable.</span></span> <span data-ttu-id="08551-116">Para obter mais detalhes, consulte Olá [documentação do observador de rede](../../network-watcher/network-watcher-monitoring-overview.md).</span><span class="sxs-lookup"><span data-stu-id="08551-116">For more details, please see hello [Network Watcher documentation](../../network-watcher/network-watcher-monitoring-overview.md).</span></span>

## <a name="extension-schema"></a><span data-ttu-id="08551-117">Esquema de extensão</span><span class="sxs-lookup"><span data-stu-id="08551-117">Extension schema</span></span>

<span data-ttu-id="08551-118">Olá JSON a seguir mostra esquema Olá Olá extensão do agente do Inspetor de rede.</span><span class="sxs-lookup"><span data-stu-id="08551-118">hello following JSON shows hello schema for hello Network Watcher Agent extension.</span></span> <span data-ttu-id="08551-119">extensão de saudação não requer nem dá suporte a todas as configurações fornecidas pelo usuário no momento e se baseia em sua configuração padrão.</span><span class="sxs-lookup"><span data-stu-id="08551-119">hello extension neither requires nor supports any user-supplied settings at this time and relies on its default configuration.</span></span>

```json
{
    "type": "extensions",
    "name": "Microsoft.Azure.NetworkWatcher",
    "apiVersion": "[variables('apiVersion')]",
    "location": "[resourceGroup().location]",
    "dependsOn": [
        "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'))]"
    ],
    "properties": {
        "publisher": "Microsoft.Azure.NetworkWatcher",
        "type": "NetworkWatcherAgentWindows",
        "typeHandlerVersion": "1.4",
        "autoUpgradeMinorVersion": true
    }
}
```

### <a name="property-values"></a><span data-ttu-id="08551-120">Valores de propriedade</span><span class="sxs-lookup"><span data-stu-id="08551-120">Property values</span></span>

| <span data-ttu-id="08551-121">Nome</span><span class="sxs-lookup"><span data-stu-id="08551-121">Name</span></span> | <span data-ttu-id="08551-122">Valor/Exemplo</span><span class="sxs-lookup"><span data-stu-id="08551-122">Value / Example</span></span> |
| ---- | ---- |
| <span data-ttu-id="08551-123">apiVersion</span><span class="sxs-lookup"><span data-stu-id="08551-123">apiVersion</span></span> | <span data-ttu-id="08551-124">2015-06-15</span><span class="sxs-lookup"><span data-stu-id="08551-124">2015-06-15</span></span> |
| <span data-ttu-id="08551-125">publicador</span><span class="sxs-lookup"><span data-stu-id="08551-125">publisher</span></span> | <span data-ttu-id="08551-126">Microsoft.Azure.NetworkWatcher</span><span class="sxs-lookup"><span data-stu-id="08551-126">Microsoft.Azure.NetworkWatcher</span></span> |
| <span data-ttu-id="08551-127">type</span><span class="sxs-lookup"><span data-stu-id="08551-127">type</span></span> | <span data-ttu-id="08551-128">NetworkWatcherAgentWindows</span><span class="sxs-lookup"><span data-stu-id="08551-128">NetworkWatcherAgentWindows</span></span> |
| <span data-ttu-id="08551-129">typeHandlerVersion</span><span class="sxs-lookup"><span data-stu-id="08551-129">typeHandlerVersion</span></span> | <span data-ttu-id="08551-130">1.4</span><span class="sxs-lookup"><span data-stu-id="08551-130">1.4</span></span> |


## <a name="template-deployment"></a><span data-ttu-id="08551-131">Implantação de modelo</span><span class="sxs-lookup"><span data-stu-id="08551-131">Template deployment</span></span>

<span data-ttu-id="08551-132">Extensões de VM do Azure podem ser implantadas com modelos do Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="08551-132">Azure VM extensions can be deployed with Azure Resource Manager templates.</span></span> <span data-ttu-id="08551-133">esquema JSON Olá detalhada na seção anterior Olá pode ser usada em uma saudação de toorun de modelo do Azure Resource Manager extensão do agente do Inspetor de rede durante uma implantação de modelo do Gerenciador de recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="08551-133">hello JSON schema detailed in hello previous section can be used in an Azure Resource Manager template toorun hello Network Watcher Agent extension during an Azure Resource Manager template deployment.</span></span>

## <a name="powershell-deployment"></a><span data-ttu-id="08551-134">Implantação do PowerShell</span><span class="sxs-lookup"><span data-stu-id="08551-134">PowerShell deployment</span></span>

<span data-ttu-id="08551-135">Olá `Set-AzureRmVMExtension` comando pode ser usado toodeploy Olá agente do Inspetor de rede virtual machine extensão tooan máquina virtual existente.</span><span class="sxs-lookup"><span data-stu-id="08551-135">hello `Set-AzureRmVMExtension` command can be used toodeploy hello Network Watcher Agent virtual machine extension tooan existing virtual machine.</span></span>

```powershell
Set-AzureRmVMExtension -ResourceGroupName "myResourceGroup1" `
                       -Location "WestUS" `
                       -VMName "myVM1" `
                       -Name "networkWatcherAgent" `
                       -Publisher "Microsoft.Azure.NetworkWatcher" `
                       -Type "NetworkWatcherAgentWindows" `
                       -TypeHandlerVersion "1.4"
```

## <a name="troubleshooting-and-support"></a><span data-ttu-id="08551-136">Solução de problemas e suporte</span><span class="sxs-lookup"><span data-stu-id="08551-136">Troubleshooting and support</span></span>

### <a name="troubleshooting"></a><span data-ttu-id="08551-137">Solucionar problemas</span><span class="sxs-lookup"><span data-stu-id="08551-137">Troubleshooting</span></span>

<span data-ttu-id="08551-138">Dados sobre o estado de saudação de implantações de extensão podem ser recuperados da saudação portal do Azure e usando o módulo do PowerShell do Azure hello.</span><span class="sxs-lookup"><span data-stu-id="08551-138">Data about hello state of extension deployments can be retrieved from hello Azure portal, and by using hello Azure PowerShell module.</span></span> <span data-ttu-id="08551-139">estado da implantação Olá toosee de extensões para uma determinada VM, Olá execução usando o comando a seguir Olá módulo PowerShell do Azure.</span><span class="sxs-lookup"><span data-stu-id="08551-139">toosee hello deployment state of extensions for a given VM, run hello following command using hello Azure PowerShell module.</span></span>

```powershell
Get-AzureRmVMExtension -ResourceGroupName myResourceGroup1 -VMName myVM1 -Name networkWatcherAgent
```

<span data-ttu-id="08551-140">Execução de extensão é conectado toofiles encontrado no hello após o diretório de saída:</span><span class="sxs-lookup"><span data-stu-id="08551-140">Extension execution output is logged toofiles found in hello following directory:</span></span>

```cmd
C:\WindowsAzure\Logs\Plugins\Microsoft.Azure.NetworkWatcher.NetworkWatcherAgentWindows\
```

### <a name="support"></a><span data-ttu-id="08551-141">Suporte</span><span class="sxs-lookup"><span data-stu-id="08551-141">Support</span></span>

<span data-ttu-id="08551-142">Se você precisar de mais ajuda a qualquer momento neste artigo, você pode consulte a documentação do guia do usuário de Inspetor de rede toohello ou entre em contato com o hello Azure especialistas em Olá [fóruns MSDN Azure e o estouro de pilha](https://azure.microsoft.com/en-us/support/forums/).</span><span class="sxs-lookup"><span data-stu-id="08551-142">If you need more help at any point in this article, you can refer toohello Network Watcher User Guide documentation or contact hello Azure experts on hello [MSDN Azure and Stack Overflow forums](https://azure.microsoft.com/en-us/support/forums/).</span></span> <span data-ttu-id="08551-143">Como alternativa, você pode registrar um incidente de suporte do Azure.</span><span class="sxs-lookup"><span data-stu-id="08551-143">Alternatively, you can file an Azure support incident.</span></span> <span data-ttu-id="08551-144">Vá toohello [site de suporte do Azure](https://azure.microsoft.com/en-us/support/options/) e selecione obter suporte.</span><span class="sxs-lookup"><span data-stu-id="08551-144">Go toohello [Azure support site](https://azure.microsoft.com/en-us/support/options/) and select Get support.</span></span> <span data-ttu-id="08551-145">Para obter informações sobre como usar o suporte do Azure, leia Olá [perguntas frequentes sobre o suporte da Microsoft Azure](https://azure.microsoft.com/en-us/support/faq/).</span><span class="sxs-lookup"><span data-stu-id="08551-145">For information about using Azure Support, read hello [Microsoft Azure support FAQ](https://azure.microsoft.com/en-us/support/faq/).</span></span>
