---
title: "aaaAzure extensão de máquina virtual do agente do Inspetor de rede para Linux | Microsoft Docs"
description: "Implante Olá agente do Inspetor de rede na máquina virtual do Linux usando uma extensão de máquina virtual."
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
ms.openlocfilehash: 84bed132cbda83d0917be490f9a50914578952a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="network-watcher-agent-virtual-machine-extension-for-linux"></a><span data-ttu-id="aee6e-103">Extensão da máquina virtual do Agente do Observador de Rede do Azure para Linux</span><span class="sxs-lookup"><span data-stu-id="aee6e-103">Network Watcher Agent virtual machine extension for Linux</span></span>

## <a name="overview"></a><span data-ttu-id="aee6e-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="aee6e-104">Overview</span></span>

<span data-ttu-id="aee6e-105">[Observador de Rede do Azure](https://review.docs.microsoft.com/en-us/azure/network-watcher/) é um serviço de monitoramento de desempenho, diagnóstico e análise de rede que permite o monitoramento de redes do Azure.</span><span class="sxs-lookup"><span data-stu-id="aee6e-105">[Azure Network Watcher](https://review.docs.microsoft.com/en-us/azure/network-watcher/) is a network performance monitoring, diagnostic, and analytics service that allows monitoring for Azure networks.</span></span> <span data-ttu-id="aee6e-106">Olá extensão do agente do Inspetor de rede de máquina virtual é um requisito para alguns dos recursos de rede Inspetor Olá em máquinas virtuais do Azure.</span><span class="sxs-lookup"><span data-stu-id="aee6e-106">hello Network Watcher Agent virtual machine extension is a requirement for some of hello Network Watcher features on Azure virtual machines.</span></span> <span data-ttu-id="aee6e-107">Isso inclui capturar o tráfego de rede sob demanda e outras funcionalidades avançadas.</span><span class="sxs-lookup"><span data-stu-id="aee6e-107">This includes capturing network traffic on demand and other advanced functionality.</span></span>

<span data-ttu-id="aee6e-108">Saudação de detalhes neste documento suporte a plataformas e opções de implantação para Olá extensão do agente do Inspetor de rede de máquina virtual para Linux.</span><span class="sxs-lookup"><span data-stu-id="aee6e-108">This document details hello supported platforms and deployment options for hello Network Watcher Agent virtual machine extension for Linux.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="aee6e-109">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="aee6e-109">Prerequisites</span></span>

### <a name="operating-system"></a><span data-ttu-id="aee6e-110">Sistema operacional</span><span class="sxs-lookup"><span data-stu-id="aee6e-110">Operating system</span></span>

<span data-ttu-id="aee6e-111">Olá extensão do agente do Inspetor de rede pode ser executada em relação a essas distribuições do Linux:</span><span class="sxs-lookup"><span data-stu-id="aee6e-111">hello Network Watcher Agent extension can be run against these Linux distributions:</span></span>

| <span data-ttu-id="aee6e-112">Distribuição</span><span class="sxs-lookup"><span data-stu-id="aee6e-112">Distribution</span></span> | <span data-ttu-id="aee6e-113">Versão</span><span class="sxs-lookup"><span data-stu-id="aee6e-113">Version</span></span> |
|---|---|
| <span data-ttu-id="aee6e-114">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="aee6e-114">Ubuntu</span></span> | <span data-ttu-id="aee6e-115">16.04 LTS, 14.04 LTS e 12.04 LTS</span><span class="sxs-lookup"><span data-stu-id="aee6e-115">16.04 LTS, 14.04 LTS and 12.04 LTS</span></span> |
| <span data-ttu-id="aee6e-116">Debian</span><span class="sxs-lookup"><span data-stu-id="aee6e-116">Debian</span></span> | <span data-ttu-id="aee6e-117">7 e 8</span><span class="sxs-lookup"><span data-stu-id="aee6e-117">7 and 8</span></span> |
| <span data-ttu-id="aee6e-118">RedHat</span><span class="sxs-lookup"><span data-stu-id="aee6e-118">RedHat</span></span> | <span data-ttu-id="aee6e-119">6.x e 7.x</span><span class="sxs-lookup"><span data-stu-id="aee6e-119">6.x and 7.x</span></span> |
| <span data-ttu-id="aee6e-120">Oracle Linux</span><span class="sxs-lookup"><span data-stu-id="aee6e-120">Oracle Linux</span></span> | <span data-ttu-id="aee6e-121">7x</span><span class="sxs-lookup"><span data-stu-id="aee6e-121">7x</span></span> |
| <span data-ttu-id="aee6e-122">Suse</span><span class="sxs-lookup"><span data-stu-id="aee6e-122">Suse</span></span> | <span data-ttu-id="aee6e-123">11 e 12</span><span class="sxs-lookup"><span data-stu-id="aee6e-123">11 and 12</span></span> |
| <span data-ttu-id="aee6e-124">OpenSuse</span><span class="sxs-lookup"><span data-stu-id="aee6e-124">OpenSuse</span></span> | <span data-ttu-id="aee6e-125">7.0</span><span class="sxs-lookup"><span data-stu-id="aee6e-125">7.0</span></span> |
| <span data-ttu-id="aee6e-126">CentOS</span><span class="sxs-lookup"><span data-stu-id="aee6e-126">CentOS</span></span> | <span data-ttu-id="aee6e-127">7.0</span><span class="sxs-lookup"><span data-stu-id="aee6e-127">7.0</span></span> |

<span data-ttu-id="aee6e-128">Observe que o CoreOS não tem suporte neste momento.</span><span class="sxs-lookup"><span data-stu-id="aee6e-128">Note that CoreOS is not supported at this time.</span></span>

### <a name="internet-connectivity"></a><span data-ttu-id="aee6e-129">Conectividade com a Internet</span><span class="sxs-lookup"><span data-stu-id="aee6e-129">Internet connectivity</span></span>

<span data-ttu-id="aee6e-130">Alguns Olá funcionalidade de agente do Inspetor de rede requer que a máquina virtual Olá destino ser toohello conectado à Internet.</span><span class="sxs-lookup"><span data-stu-id="aee6e-130">Some of hello Network Watcher Agent functionality requires that hello target virtual machine be connected toohello Internet.</span></span> <span data-ttu-id="aee6e-131">Sem conexões de saída Olá capacidade tooestablish alguns dos recursos de agente do Inspetor de rede Olá podem mau funcionamento ou se tornar indisponível.</span><span class="sxs-lookup"><span data-stu-id="aee6e-131">Without hello ability tooestablish outgoing connections some of hello Network Watcher Agent features may malfunction or become unavailable.</span></span> <span data-ttu-id="aee6e-132">Para obter mais detalhes, consulte Olá [documentação do observador de rede](https://review.docs.microsoft.com/en-us/azure/network-watcher/).</span><span class="sxs-lookup"><span data-stu-id="aee6e-132">For more details, please see hello [Network Watcher documentation](https://review.docs.microsoft.com/en-us/azure/network-watcher/).</span></span>

## <a name="extension-schema"></a><span data-ttu-id="aee6e-133">Esquema de extensão</span><span class="sxs-lookup"><span data-stu-id="aee6e-133">Extension schema</span></span>

<span data-ttu-id="aee6e-134">Olá JSON a seguir mostra esquema Olá Olá extensão do agente do Inspetor de rede.</span><span class="sxs-lookup"><span data-stu-id="aee6e-134">hello following JSON shows hello schema for hello Network Watcher Agent extension.</span></span> <span data-ttu-id="aee6e-135">extensão de saudação não requer nem dá suporte a todas as configurações fornecidas pelo usuário no momento e se baseia em sua configuração padrão.</span><span class="sxs-lookup"><span data-stu-id="aee6e-135">hello extension neither requires nor supports any user-supplied settings at this time and relies on its default configuration.</span></span>

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

### <a name="property-values"></a><span data-ttu-id="aee6e-136">Valores de propriedade</span><span class="sxs-lookup"><span data-stu-id="aee6e-136">Property values</span></span>

| <span data-ttu-id="aee6e-137">Nome</span><span class="sxs-lookup"><span data-stu-id="aee6e-137">Name</span></span> | <span data-ttu-id="aee6e-138">Valor/Exemplo</span><span class="sxs-lookup"><span data-stu-id="aee6e-138">Value / Example</span></span> |
| ---- | ---- |
| <span data-ttu-id="aee6e-139">apiVersion</span><span class="sxs-lookup"><span data-stu-id="aee6e-139">apiVersion</span></span> | <span data-ttu-id="aee6e-140">2015-06-15</span><span class="sxs-lookup"><span data-stu-id="aee6e-140">2015-06-15</span></span> |
| <span data-ttu-id="aee6e-141">publicador</span><span class="sxs-lookup"><span data-stu-id="aee6e-141">publisher</span></span> | <span data-ttu-id="aee6e-142">Microsoft.Azure.NetworkWatcher</span><span class="sxs-lookup"><span data-stu-id="aee6e-142">Microsoft.Azure.NetworkWatcher</span></span> |
| <span data-ttu-id="aee6e-143">type</span><span class="sxs-lookup"><span data-stu-id="aee6e-143">type</span></span> | <span data-ttu-id="aee6e-144">NetworkWatcherAgentLinux</span><span class="sxs-lookup"><span data-stu-id="aee6e-144">NetworkWatcherAgentLinux</span></span> |
| <span data-ttu-id="aee6e-145">typeHandlerVersion</span><span class="sxs-lookup"><span data-stu-id="aee6e-145">typeHandlerVersion</span></span> | <span data-ttu-id="aee6e-146">1.4</span><span class="sxs-lookup"><span data-stu-id="aee6e-146">1.4</span></span> |

## <a name="template-deployment"></a><span data-ttu-id="aee6e-147">Implantação de modelo</span><span class="sxs-lookup"><span data-stu-id="aee6e-147">Template deployment</span></span>

<span data-ttu-id="aee6e-148">Extensões de VM do Azure podem ser implantadas com modelos do Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="aee6e-148">Azure VM extensions can be deployed with Azure Resource Manager templates.</span></span> <span data-ttu-id="aee6e-149">esquema JSON Olá detalhada na seção anterior Olá pode ser usada em uma saudação de toorun de modelo do Azure Resource Manager extensão do agente do Inspetor de rede durante uma implantação de modelo do Gerenciador de recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="aee6e-149">hello JSON schema detailed in hello previous section can be used in an Azure Resource Manager template toorun hello Network Watcher Agent extension during an Azure Resource Manager template deployment.</span></span>

## <a name="azure-cli-deployment"></a><span data-ttu-id="aee6e-150">Implantação da CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="aee6e-150">Azure CLI deployment</span></span>

<span data-ttu-id="aee6e-151">Olá CLI do Azure pode ser usado toodeploy Olá rede Inspetor agente VM extensão tooan máquina virtual existente.</span><span class="sxs-lookup"><span data-stu-id="aee6e-151">hello Azure CLI can be used toodeploy hello Network Watcher Agent VM extension tooan existing virtual machine.</span></span>

```azurecli
azure vm extension set myResourceGroup1 myVM1 NetworkWatcherAgentLinux Microsoft.Azure.NetworkWatcher 1.4
```

## <a name="troubleshooting-and-support"></a><span data-ttu-id="aee6e-152">Solução de problemas e suporte</span><span class="sxs-lookup"><span data-stu-id="aee6e-152">Troubleshooting and support</span></span>

### <a name="troubleshooting"></a><span data-ttu-id="aee6e-153">Solucionar problemas</span><span class="sxs-lookup"><span data-stu-id="aee6e-153">Troubleshooting</span></span>

<span data-ttu-id="aee6e-154">Dados sobre o estado de saudação de implantações de extensão podem ser recuperados da saudação portal do Azure e usando Olá CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="aee6e-154">Data about hello state of extension deployments can be retrieved from hello Azure portal, and by using hello Azure CLI.</span></span> <span data-ttu-id="aee6e-155">estado da implantação Olá toosee de extensões para uma determinada VM, execute hello usando o comando a seguir Olá CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="aee6e-155">toosee hello deployment state of extensions for a given VM, run hello following command using hello Azure CLI.</span></span>

```azurecli
azure vm extension get myResourceGroup1 myVM1
```

<span data-ttu-id="aee6e-156">Execução de extensão é conectado toofiles encontrado no hello após o diretório de saída:</span><span class="sxs-lookup"><span data-stu-id="aee6e-156">Extension execution output is logged toofiles found in hello following directory:</span></span>

`
/var/log/azure/Microsoft.Azure.NetworkWatcher.NetworkWatcherAgentLinux/
`

### <a name="support"></a><span data-ttu-id="aee6e-157">Suporte</span><span class="sxs-lookup"><span data-stu-id="aee6e-157">Support</span></span>

<span data-ttu-id="aee6e-158">Se você precisar de mais ajuda a qualquer momento neste artigo, você pode consulte a documentação do observador de rede toohello ou entre em contato com o hello Azure especialistas em Olá [fóruns MSDN Azure e o estouro de pilha](https://azure.microsoft.com/en-us/support/forums/).</span><span class="sxs-lookup"><span data-stu-id="aee6e-158">If you need more help at any point in this article, you can refer toohello Network Watcher documentation or contact hello Azure experts on hello [MSDN Azure and Stack Overflow forums](https://azure.microsoft.com/en-us/support/forums/).</span></span> <span data-ttu-id="aee6e-159">Como alternativa, você pode registrar um incidente de suporte do Azure.</span><span class="sxs-lookup"><span data-stu-id="aee6e-159">Alternatively, you can file an Azure support incident.</span></span> <span data-ttu-id="aee6e-160">Vá toohello [site de suporte do Azure](https://azure.microsoft.com/en-us/support/options/) e selecione obter suporte.</span><span class="sxs-lookup"><span data-stu-id="aee6e-160">Go toohello [Azure support site](https://azure.microsoft.com/en-us/support/options/) and select Get support.</span></span> <span data-ttu-id="aee6e-161">Para obter informações sobre como usar o suporte do Azure, leia Olá [perguntas frequentes sobre o suporte da Microsoft Azure](https://azure.microsoft.com/en-us/support/faq/).</span><span class="sxs-lookup"><span data-stu-id="aee6e-161">For information about using Azure Support, read hello [Microsoft Azure support FAQ](https://azure.microsoft.com/en-us/support/faq/).</span></span>
