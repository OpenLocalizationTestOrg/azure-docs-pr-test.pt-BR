---
title: "Extensão da máquina virtual do Agente do Observador de Rede do Azure para Linux | Microsoft Docs"
description: "Implante o Agente do Observador de Rede do Azure na máquina virtual Linux usando uma extensão da máquina virtual."
services: virtual-machines-linux
documentationcenter: 
author: dennisg
manager: amku
editor: 
tags: azure-resource-manager
ms.assetid: 5c81e94c-e127-4dd2-ae83-a236c4512345
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 02/14/2017
ms.author: dennisg
ms.openlocfilehash: eaadd531b9e05a54446e61f98584ae9d75470a5f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="network-watcher-agent-virtual-machine-extension-for-linux"></a><span data-ttu-id="8d5c1-103">Extensão da máquina virtual do Agente do Observador de Rede do Azure para Linux</span><span class="sxs-lookup"><span data-stu-id="8d5c1-103">Network Watcher Agent virtual machine extension for Linux</span></span>

## <a name="overview"></a><span data-ttu-id="8d5c1-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="8d5c1-104">Overview</span></span>

<span data-ttu-id="8d5c1-105">[Observador de Rede do Azure](https://review.docs.microsoft.com/en-us/azure/network-watcher/) é um serviço de monitoramento de desempenho, diagnóstico e análise de rede que permite o monitoramento de redes do Azure.</span><span class="sxs-lookup"><span data-stu-id="8d5c1-105">[Azure Network Watcher](https://review.docs.microsoft.com/en-us/azure/network-watcher/) is a network performance monitoring, diagnostic, and analytics service that allows monitoring for Azure networks.</span></span> <span data-ttu-id="8d5c1-106">A extensão da máquina virtual do Agente do Observador de Rede é um requisito para alguns dos recursos do Observador de Rede em máquinas virtuais do Azure.</span><span class="sxs-lookup"><span data-stu-id="8d5c1-106">The Network Watcher Agent virtual machine extension is a requirement for some of the Network Watcher features on Azure virtual machines.</span></span> <span data-ttu-id="8d5c1-107">Isso inclui capturar o tráfego de rede sob demanda e outra funcionalidade avançada.</span><span class="sxs-lookup"><span data-stu-id="8d5c1-107">This includes capturing network traffic on demand and other advanced functionality.</span></span>

<span data-ttu-id="8d5c1-108">Este documento detalha as plataformas com opções de plataformas e implantação com suporte para a extensão da máquina virtual do Agente do Observador de Rede para Linux.</span><span class="sxs-lookup"><span data-stu-id="8d5c1-108">This document details the supported platforms and deployment options for the Network Watcher Agent virtual machine extension for Linux.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8d5c1-109">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="8d5c1-109">Prerequisites</span></span>

### <a name="operating-system"></a><span data-ttu-id="8d5c1-110">Sistema operacional</span><span class="sxs-lookup"><span data-stu-id="8d5c1-110">Operating system</span></span>

<span data-ttu-id="8d5c1-111">A extensão do Agente do Observador de rede pode ser executada nessas distribuições do Linux:</span><span class="sxs-lookup"><span data-stu-id="8d5c1-111">The Network Watcher Agent extension can be run against these Linux distributions:</span></span>

| <span data-ttu-id="8d5c1-112">Distribuição</span><span class="sxs-lookup"><span data-stu-id="8d5c1-112">Distribution</span></span> | <span data-ttu-id="8d5c1-113">Versão</span><span class="sxs-lookup"><span data-stu-id="8d5c1-113">Version</span></span> |
|---|---|
| <span data-ttu-id="8d5c1-114">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="8d5c1-114">Ubuntu</span></span> | <span data-ttu-id="8d5c1-115">16.04 LTS, 14.04 LTS e 12.04 LTS</span><span class="sxs-lookup"><span data-stu-id="8d5c1-115">16.04 LTS, 14.04 LTS and 12.04 LTS</span></span> |
| <span data-ttu-id="8d5c1-116">Debian</span><span class="sxs-lookup"><span data-stu-id="8d5c1-116">Debian</span></span> | <span data-ttu-id="8d5c1-117">7 e 8</span><span class="sxs-lookup"><span data-stu-id="8d5c1-117">7 and 8</span></span> |
| <span data-ttu-id="8d5c1-118">RedHat</span><span class="sxs-lookup"><span data-stu-id="8d5c1-118">RedHat</span></span> | <span data-ttu-id="8d5c1-119">6.x e 7.x</span><span class="sxs-lookup"><span data-stu-id="8d5c1-119">6.x and 7.x</span></span> |
| <span data-ttu-id="8d5c1-120">Oracle Linux</span><span class="sxs-lookup"><span data-stu-id="8d5c1-120">Oracle Linux</span></span> | <span data-ttu-id="8d5c1-121">7x</span><span class="sxs-lookup"><span data-stu-id="8d5c1-121">7x</span></span> |
| <span data-ttu-id="8d5c1-122">Suse</span><span class="sxs-lookup"><span data-stu-id="8d5c1-122">Suse</span></span> | <span data-ttu-id="8d5c1-123">11 e 12</span><span class="sxs-lookup"><span data-stu-id="8d5c1-123">11 and 12</span></span> |
| <span data-ttu-id="8d5c1-124">OpenSuse</span><span class="sxs-lookup"><span data-stu-id="8d5c1-124">OpenSuse</span></span> | <span data-ttu-id="8d5c1-125">7.0</span><span class="sxs-lookup"><span data-stu-id="8d5c1-125">7.0</span></span> |
| <span data-ttu-id="8d5c1-126">CentOS</span><span class="sxs-lookup"><span data-stu-id="8d5c1-126">CentOS</span></span> | <span data-ttu-id="8d5c1-127">7.0</span><span class="sxs-lookup"><span data-stu-id="8d5c1-127">7.0</span></span> |

<span data-ttu-id="8d5c1-128">Observe que o CoreOS não tem suporte neste momento.</span><span class="sxs-lookup"><span data-stu-id="8d5c1-128">Note that CoreOS is not supported at this time.</span></span>

### <a name="internet-connectivity"></a><span data-ttu-id="8d5c1-129">Conectividade com a Internet</span><span class="sxs-lookup"><span data-stu-id="8d5c1-129">Internet connectivity</span></span>

<span data-ttu-id="8d5c1-130">Algumas das funcionalidades do Agente do Observador de Rede exigem que a máquina virtual de destino esteja conectada à Internet.</span><span class="sxs-lookup"><span data-stu-id="8d5c1-130">Some of the Network Watcher Agent functionality requires that the target virtual machine be connected to the Internet.</span></span> <span data-ttu-id="8d5c1-131">Sem a capacidade de estabelecer conexões de saída, alguns dos recursos do Agente do Observador de Rede podem apresentar problemas ou se tornar indisponíveis.</span><span class="sxs-lookup"><span data-stu-id="8d5c1-131">Without the ability to establish outgoing connections some of the Network Watcher Agent features may malfunction or become unavailable.</span></span> <span data-ttu-id="8d5c1-132">Para obter mais detalhes, confira a [documentação do Observador de Rede](https://review.docs.microsoft.com/en-us/azure/network-watcher/).</span><span class="sxs-lookup"><span data-stu-id="8d5c1-132">For more details, please see the [Network Watcher documentation](https://review.docs.microsoft.com/en-us/azure/network-watcher/).</span></span>

## <a name="extension-schema"></a><span data-ttu-id="8d5c1-133">Esquema de extensão</span><span class="sxs-lookup"><span data-stu-id="8d5c1-133">Extension schema</span></span>

<span data-ttu-id="8d5c1-134">O JSON a seguir mostra o esquema para a extensão do Agente do Observador de Rede.</span><span class="sxs-lookup"><span data-stu-id="8d5c1-134">The following JSON shows the schema for the Network Watcher Agent extension.</span></span> <span data-ttu-id="8d5c1-135">A extensão não requer nem oferece suporte a nenhuma configuração fornecida pelo usuário no momento e se baseia em sua configuração padrão.</span><span class="sxs-lookup"><span data-stu-id="8d5c1-135">The extension neither requires nor supports any user-supplied settings at this time and relies on its default configuration.</span></span>

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
        "type": "NetworkWatcherAgentLinux",
        "typeHandlerVersion": "1.4",
        "autoUpgradeMinorVersion": true
    }
}
```

### <a name="property-values"></a><span data-ttu-id="8d5c1-136">Valores de propriedade</span><span class="sxs-lookup"><span data-stu-id="8d5c1-136">Property values</span></span>

| <span data-ttu-id="8d5c1-137">Nome</span><span class="sxs-lookup"><span data-stu-id="8d5c1-137">Name</span></span> | <span data-ttu-id="8d5c1-138">Valor/Exemplo</span><span class="sxs-lookup"><span data-stu-id="8d5c1-138">Value / Example</span></span> |
| ---- | ---- |
| <span data-ttu-id="8d5c1-139">apiVersion</span><span class="sxs-lookup"><span data-stu-id="8d5c1-139">apiVersion</span></span> | <span data-ttu-id="8d5c1-140">2015-06-15</span><span class="sxs-lookup"><span data-stu-id="8d5c1-140">2015-06-15</span></span> |
| <span data-ttu-id="8d5c1-141">publicador</span><span class="sxs-lookup"><span data-stu-id="8d5c1-141">publisher</span></span> | <span data-ttu-id="8d5c1-142">Microsoft.Azure.NetworkWatcher</span><span class="sxs-lookup"><span data-stu-id="8d5c1-142">Microsoft.Azure.NetworkWatcher</span></span> |
| <span data-ttu-id="8d5c1-143">type</span><span class="sxs-lookup"><span data-stu-id="8d5c1-143">type</span></span> | <span data-ttu-id="8d5c1-144">NetworkWatcherAgentLinux</span><span class="sxs-lookup"><span data-stu-id="8d5c1-144">NetworkWatcherAgentLinux</span></span> |
| <span data-ttu-id="8d5c1-145">typeHandlerVersion</span><span class="sxs-lookup"><span data-stu-id="8d5c1-145">typeHandlerVersion</span></span> | <span data-ttu-id="8d5c1-146">1.4</span><span class="sxs-lookup"><span data-stu-id="8d5c1-146">1.4</span></span> |

## <a name="template-deployment"></a><span data-ttu-id="8d5c1-147">Implantação de modelo</span><span class="sxs-lookup"><span data-stu-id="8d5c1-147">Template deployment</span></span>

<span data-ttu-id="8d5c1-148">Extensões de VM do Azure podem ser implantadas com modelos do Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="8d5c1-148">Azure VM extensions can be deployed with Azure Resource Manager templates.</span></span> <span data-ttu-id="8d5c1-149">O esquema JSON detalhado na seção anterior pode ser usado em um modelo do Azure Resource Manager para executar a extensão do Agente do Observador de Rede durante uma implantação do modelo do Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="8d5c1-149">The JSON schema detailed in the previous section can be used in an Azure Resource Manager template to run the Network Watcher Agent extension during an Azure Resource Manager template deployment.</span></span>

## <a name="azure-cli-deployment"></a><span data-ttu-id="8d5c1-150">Implantação da CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="8d5c1-150">Azure CLI deployment</span></span>

<span data-ttu-id="8d5c1-151">A CLI do Azure pode ser usado para implantar a extensão da VM do Agente do Observador de Rede para uma máquina virtual existente.</span><span class="sxs-lookup"><span data-stu-id="8d5c1-151">The Azure CLI can be used to deploy the Network Watcher Agent VM extension to an existing virtual machine.</span></span>

```azurecli
azure vm extension set myResourceGroup1 myVM1 NetworkWatcherAgentLinux Microsoft.Azure.NetworkWatcher 1.4
```

## <a name="troubleshooting-and-support"></a><span data-ttu-id="8d5c1-152">Solução de problemas e suporte</span><span class="sxs-lookup"><span data-stu-id="8d5c1-152">Troubleshooting and support</span></span>

### <a name="troubleshooting"></a><span data-ttu-id="8d5c1-153">Solucionar problemas</span><span class="sxs-lookup"><span data-stu-id="8d5c1-153">Troubleshooting</span></span>

<span data-ttu-id="8d5c1-154">Dados sobre o estado das implantações de extensão podem ser recuperados do Portal do Azure usando a CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="8d5c1-154">Data about the state of extension deployments can be retrieved from the Azure portal, and by using the Azure CLI.</span></span> <span data-ttu-id="8d5c1-155">Para ver o estado da implantação das extensões de uma determinada VM, execute o comando a seguir usando a CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="8d5c1-155">To see the deployment state of extensions for a given VM, run the following command using the Azure CLI.</span></span>

```azurecli
azure vm extension get myResourceGroup1 myVM1
```

<span data-ttu-id="8d5c1-156">A saída de execução da extensão é registrada nos arquivos localizados no seguinte diretório:</span><span class="sxs-lookup"><span data-stu-id="8d5c1-156">Extension execution output is logged to files found in the following directory:</span></span>

`
/var/log/azure/Microsoft.Azure.NetworkWatcher.NetworkWatcherAgentLinux/
`

### <a name="support"></a><span data-ttu-id="8d5c1-157">Suporte</span><span class="sxs-lookup"><span data-stu-id="8d5c1-157">Support</span></span>

<span data-ttu-id="8d5c1-158">Caso precise de mais ajuda a qualquer momento neste artigo, consulte a documentação do Observador de Rede ou entre em contato com os especialistas do Azure nos [fóruns do Azure e do Stack Overflow no MSDN](https://azure.microsoft.com/en-us/support/forums/).</span><span class="sxs-lookup"><span data-stu-id="8d5c1-158">If you need more help at any point in this article, you can refer to the Network Watcher documentation or contact the Azure experts on the [MSDN Azure and Stack Overflow forums](https://azure.microsoft.com/en-us/support/forums/).</span></span> <span data-ttu-id="8d5c1-159">Como alternativa, você pode registrar um incidente de suporte do Azure.</span><span class="sxs-lookup"><span data-stu-id="8d5c1-159">Alternatively, you can file an Azure support incident.</span></span> <span data-ttu-id="8d5c1-160">Vá para o [site de suporte do Azure](https://azure.microsoft.com/en-us/support/options/) e selecione Obter suporte.</span><span class="sxs-lookup"><span data-stu-id="8d5c1-160">Go to the [Azure support site](https://azure.microsoft.com/en-us/support/options/) and select Get support.</span></span> <span data-ttu-id="8d5c1-161">Para saber mais sobre como usar o suporte do Azure, leia as [Perguntas frequentes sobre o suporte do Microsoft Azure](https://azure.microsoft.com/en-us/support/faq/).</span><span class="sxs-lookup"><span data-stu-id="8d5c1-161">For information about using Azure Support, read the [Microsoft Azure support FAQ](https://azure.microsoft.com/en-us/support/faq/).</span></span>
