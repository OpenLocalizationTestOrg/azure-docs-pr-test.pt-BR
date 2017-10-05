---
title: "Extensão da máquina virtual do Agente do Observador de Rede do Azure para Windows | Microsoft Docs"
description: "Implante o Agente do Observador de Rede na máquina virtual Windows usando uma extensão da máquina virtual."
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
ms.openlocfilehash: b8d6a998bc86337b286a3434f44f762cca9b7e68
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="network-watcher-agent-virtual-machine-extension-for-windows"></a><span data-ttu-id="a5c9e-103">Extensão da máquina virtual do Agente do Observador de Rede para Windows</span><span class="sxs-lookup"><span data-stu-id="a5c9e-103">Network Watcher Agent virtual machine extension for Windows</span></span>

## <a name="overview"></a><span data-ttu-id="a5c9e-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="a5c9e-104">Overview</span></span>

<span data-ttu-id="a5c9e-105">[Observador de Rede do Azure](https://review.docs.microsoft.com/en-us/azure/network-watcher/) é um serviço de monitoramento de desempenho, diagnóstico e análise de rede que permite o monitoramento de redes do Azure.</span><span class="sxs-lookup"><span data-stu-id="a5c9e-105">[Azure Network Watcher](https://review.docs.microsoft.com/en-us/azure/network-watcher/) is a network performance monitoring, diagnostic, and analytics service that allows monitoring for Azure networks.</span></span> <span data-ttu-id="a5c9e-106">A extensão da máquina virtual do Agente do Observador de Rede é um requisito para alguns dos recursos do Observador de Rede em máquinas virtuais do Azure.</span><span class="sxs-lookup"><span data-stu-id="a5c9e-106">The Network Watcher Agent virtual machine extension is a requirement for some of the Network Watcher features on Azure virtual machines.</span></span> <span data-ttu-id="a5c9e-107">Isso inclui capturar o tráfego de rede sob demanda e outras funcionalidades avançadas.</span><span class="sxs-lookup"><span data-stu-id="a5c9e-107">This includes capturing network traffic on demand and other advanced functionality.</span></span>

<span data-ttu-id="a5c9e-108">Este documento detalha as opções com suporte de plataformas e implantação para a extensão da máquina virtual do Agente do Observador de Rede para Windows.</span><span class="sxs-lookup"><span data-stu-id="a5c9e-108">This document details the supported platforms and deployment options for the Network Watcher Agent virtual machine extension for Windows.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a5c9e-109">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="a5c9e-109">Prerequisites</span></span>

### <a name="operating-system"></a><span data-ttu-id="a5c9e-110">Sistema operacional</span><span class="sxs-lookup"><span data-stu-id="a5c9e-110">Operating system</span></span>

<span data-ttu-id="a5c9e-111">A extensão do Agente do Observador de Rede para Windows pode ser executada nas versões 2008 R2, 2012, 2012 R2 e 2016 do Windows Server.</span><span class="sxs-lookup"><span data-stu-id="a5c9e-111">The Network Watcher Agent extension for Windows can be run against Windows Server 2008 R2, 2012, 2012 R2, and 2016 releases.</span></span> <span data-ttu-id="a5c9e-112">Observe que o Servidor Nano não é suportado neste momento.</span><span class="sxs-lookup"><span data-stu-id="a5c9e-112">Note that the Nano Server is not supported at this time.</span></span>

### <a name="internet-connectivity"></a><span data-ttu-id="a5c9e-113">Conectividade com a Internet</span><span class="sxs-lookup"><span data-stu-id="a5c9e-113">Internet connectivity</span></span>

<span data-ttu-id="a5c9e-114">Algumas das funcionalidades do Agente do Observador de Rede exigem que a máquina virtual de destino esteja conectada à Internet.</span><span class="sxs-lookup"><span data-stu-id="a5c9e-114">Some of the Network Watcher Agent functionality requires that the target virtual machine be connected to the Internet.</span></span> <span data-ttu-id="a5c9e-115">Sem a capacidade de estabelecer conexões de saída, alguns dos recursos do Agente do Observador de Rede podem apresentar problemas ou se tornar indisponíveis.</span><span class="sxs-lookup"><span data-stu-id="a5c9e-115">Without the ability to establish outgoing connections some of the Network Watcher Agent features may malfunction or become unavailable.</span></span> <span data-ttu-id="a5c9e-116">Para obter mais detalhes, confira a [documentação do Observador de Rede](../../network-watcher/network-watcher-monitoring-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a5c9e-116">For more details, please see the [Network Watcher documentation](../../network-watcher/network-watcher-monitoring-overview.md).</span></span>

## <a name="extension-schema"></a><span data-ttu-id="a5c9e-117">Esquema de extensão</span><span class="sxs-lookup"><span data-stu-id="a5c9e-117">Extension schema</span></span>

<span data-ttu-id="a5c9e-118">O JSON a seguir mostra o esquema para a extensão do Agente do Observador de Rede.</span><span class="sxs-lookup"><span data-stu-id="a5c9e-118">The following JSON shows the schema for the Network Watcher Agent extension.</span></span> <span data-ttu-id="a5c9e-119">A extensão não requer nem oferece suporte a nenhuma configuração fornecida pelo usuário no momento e se baseia em sua configuração padrão.</span><span class="sxs-lookup"><span data-stu-id="a5c9e-119">The extension neither requires nor supports any user-supplied settings at this time and relies on its default configuration.</span></span>

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

### <a name="property-values"></a><span data-ttu-id="a5c9e-120">Valores de propriedade</span><span class="sxs-lookup"><span data-stu-id="a5c9e-120">Property values</span></span>

| <span data-ttu-id="a5c9e-121">Nome</span><span class="sxs-lookup"><span data-stu-id="a5c9e-121">Name</span></span> | <span data-ttu-id="a5c9e-122">Valor/Exemplo</span><span class="sxs-lookup"><span data-stu-id="a5c9e-122">Value / Example</span></span> |
| ---- | ---- |
| <span data-ttu-id="a5c9e-123">apiVersion</span><span class="sxs-lookup"><span data-stu-id="a5c9e-123">apiVersion</span></span> | <span data-ttu-id="a5c9e-124">2015-06-15</span><span class="sxs-lookup"><span data-stu-id="a5c9e-124">2015-06-15</span></span> |
| <span data-ttu-id="a5c9e-125">publicador</span><span class="sxs-lookup"><span data-stu-id="a5c9e-125">publisher</span></span> | <span data-ttu-id="a5c9e-126">Microsoft.Azure.NetworkWatcher</span><span class="sxs-lookup"><span data-stu-id="a5c9e-126">Microsoft.Azure.NetworkWatcher</span></span> |
| <span data-ttu-id="a5c9e-127">type</span><span class="sxs-lookup"><span data-stu-id="a5c9e-127">type</span></span> | <span data-ttu-id="a5c9e-128">NetworkWatcherAgentWindows</span><span class="sxs-lookup"><span data-stu-id="a5c9e-128">NetworkWatcherAgentWindows</span></span> |
| <span data-ttu-id="a5c9e-129">typeHandlerVersion</span><span class="sxs-lookup"><span data-stu-id="a5c9e-129">typeHandlerVersion</span></span> | <span data-ttu-id="a5c9e-130">1.4</span><span class="sxs-lookup"><span data-stu-id="a5c9e-130">1.4</span></span> |


## <a name="template-deployment"></a><span data-ttu-id="a5c9e-131">Implantação de modelo</span><span class="sxs-lookup"><span data-stu-id="a5c9e-131">Template deployment</span></span>

<span data-ttu-id="a5c9e-132">Extensões de VM do Azure podem ser implantadas com modelos do Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="a5c9e-132">Azure VM extensions can be deployed with Azure Resource Manager templates.</span></span> <span data-ttu-id="a5c9e-133">O esquema JSON detalhado na seção anterior pode ser usado em um modelo do Azure Resource Manager para executar a extensão do Agente do Observador de Rede durante uma implantação do modelo do Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="a5c9e-133">The JSON schema detailed in the previous section can be used in an Azure Resource Manager template to run the Network Watcher Agent extension during an Azure Resource Manager template deployment.</span></span>

## <a name="powershell-deployment"></a><span data-ttu-id="a5c9e-134">Implantação do PowerShell</span><span class="sxs-lookup"><span data-stu-id="a5c9e-134">PowerShell deployment</span></span>

<span data-ttu-id="a5c9e-135">O comando `Set-AzureRmVMExtension` pode ser usado para implantar a extensão da máquina virtual do Agente do Observador de Rede em uma máquina virtual existente.</span><span class="sxs-lookup"><span data-stu-id="a5c9e-135">The `Set-AzureRmVMExtension` command can be used to deploy the Network Watcher Agent virtual machine extension to an existing virtual machine.</span></span>

```powershell
Set-AzureRmVMExtension -ResourceGroupName "myResourceGroup1" `
                       -Location "WestUS" `
                       -VMName "myVM1" `
                       -Name "networkWatcherAgent" `
                       -Publisher "Microsoft.Azure.NetworkWatcher" `
                       -Type "NetworkWatcherAgentWindows" `
                       -TypeHandlerVersion "1.4"
```

## <a name="troubleshooting-and-support"></a><span data-ttu-id="a5c9e-136">Solução de problemas e suporte</span><span class="sxs-lookup"><span data-stu-id="a5c9e-136">Troubleshooting and support</span></span>

### <a name="troubleshooting"></a><span data-ttu-id="a5c9e-137">Solucionar problemas</span><span class="sxs-lookup"><span data-stu-id="a5c9e-137">Troubleshooting</span></span>

<span data-ttu-id="a5c9e-138">Os dados sobre o estado das implantações de extensão podem ser recuperados no Portal do Azure usando o módulo do Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a5c9e-138">Data about the state of extension deployments can be retrieved from the Azure portal, and by using the Azure PowerShell module.</span></span> <span data-ttu-id="a5c9e-139">Para ver o estado da implantação das extensões de uma determinada VM, execute o comando a seguir usando o módulo do Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a5c9e-139">To see the deployment state of extensions for a given VM, run the following command using the Azure PowerShell module.</span></span>

```powershell
Get-AzureRmVMExtension -ResourceGroupName myResourceGroup1 -VMName myVM1 -Name networkWatcherAgent
```

<span data-ttu-id="a5c9e-140">A saída de execução da extensão é registrada nos arquivos localizados no seguinte diretório:</span><span class="sxs-lookup"><span data-stu-id="a5c9e-140">Extension execution output is logged to files found in the following directory:</span></span>

```cmd
C:\WindowsAzure\Logs\Plugins\Microsoft.Azure.NetworkWatcher.NetworkWatcherAgentWindows\
```

### <a name="support"></a><span data-ttu-id="a5c9e-141">Suporte</span><span class="sxs-lookup"><span data-stu-id="a5c9e-141">Support</span></span>

<span data-ttu-id="a5c9e-142">Caso precise de mais ajuda em qualquer ponto deste artigo, veja a documentação Guia de Usuário do Observador de Rede ou contate os especialistas do Azure nos [fóruns do Azure e do Stack Overflow no MSDN](https://azure.microsoft.com/en-us/support/forums/).</span><span class="sxs-lookup"><span data-stu-id="a5c9e-142">If you need more help at any point in this article, you can refer to the Network Watcher User Guide documentation or contact the Azure experts on the [MSDN Azure and Stack Overflow forums](https://azure.microsoft.com/en-us/support/forums/).</span></span> <span data-ttu-id="a5c9e-143">Como alternativa, você pode registrar um incidente de suporte do Azure.</span><span class="sxs-lookup"><span data-stu-id="a5c9e-143">Alternatively, you can file an Azure support incident.</span></span> <span data-ttu-id="a5c9e-144">Vá para o [site de suporte do Azure](https://azure.microsoft.com/en-us/support/options/) e selecione Obter suporte.</span><span class="sxs-lookup"><span data-stu-id="a5c9e-144">Go to the [Azure support site](https://azure.microsoft.com/en-us/support/options/) and select Get support.</span></span> <span data-ttu-id="a5c9e-145">Para saber mais sobre como usar o suporte do Azure, leia as [Perguntas frequentes sobre o suporte do Microsoft Azure](https://azure.microsoft.com/en-us/support/faq/).</span><span class="sxs-lookup"><span data-stu-id="a5c9e-145">For information about using Azure Support, read the [Microsoft Azure support FAQ](https://azure.microsoft.com/en-us/support/faq/).</span></span>
