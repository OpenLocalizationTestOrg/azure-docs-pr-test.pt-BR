---
title: "aaaVirtual computador extensões e recursos para Linux | Microsoft Docs"
description: "Saiba quais extensões estão disponíveis para as máquinas virtuais do Azure, agrupadas pelas funcionalidades fornecidas ou aperfeiçoadas."
services: virtual-machines-linux
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: 52f5d0ec-8f75-49e7-9e15-88d46b420e63
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 04/26/2017
ms.author: nepeters
ms.openlocfilehash: e0d2ce794c76815ccc6743e8788ee5d9d931e9a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="virtual-machine-extensions-and-features-for-linux"></a><span data-ttu-id="6ea3e-103">Recursos e extensões da máquina virtual para Linux</span><span class="sxs-lookup"><span data-stu-id="6ea3e-103">Virtual machine extensions and features for Linux</span></span>

<span data-ttu-id="6ea3e-104">Extensões da máquina virtual do Azure são pequenos aplicativos que fornecem tarefas de configuração e automação pós-implantação nas máquinas virtuais do Azure.</span><span class="sxs-lookup"><span data-stu-id="6ea3e-104">Azure virtual machine extensions are small applications that provide post-deployment configuration and automation tasks on Azure virtual machines.</span></span> <span data-ttu-id="6ea3e-105">Por exemplo, se uma máquina virtual requer a instalação de software, proteção contra vírus ou a configuração do Docker, uma extensão de VM pode ser usado toocomplete essas tarefas.</span><span class="sxs-lookup"><span data-stu-id="6ea3e-105">For example, if a virtual machine requires software installation, anti-virus protection, or Docker configuration, a VM extension can be used toocomplete these tasks.</span></span> <span data-ttu-id="6ea3e-106">Extensões VM do Azure podem ser executadas usando Olá CLI do Azure, o PowerShell, modelos do Gerenciador de recursos do Azure e Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="6ea3e-106">Azure VM extensions can be run using hello Azure CLI, PowerShell, Azure Resource Manager templates, and hello Azure portal.</span></span> <span data-ttu-id="6ea3e-107">Extensões podem ser agrupadas com uma nova implantação de máquina virtual ou executar qualquer sistema existente.</span><span class="sxs-lookup"><span data-stu-id="6ea3e-107">Extensions can be bundled with a new virtual machine deployment, or run against any existing system.</span></span>

<span data-ttu-id="6ea3e-108">Este documento fornece uma visão geral de extensões de VM, pré-requisitos para usar extensões de VM do Azure e orientação sobre como toodetect, gerenciar e remover extensões da VM.</span><span class="sxs-lookup"><span data-stu-id="6ea3e-108">This document provides an overview of VM extensions, prerequisites for using Azure VM extensions, and guidance on how toodetect, manage, and remove VM extensions.</span></span> <span data-ttu-id="6ea3e-109">Este documento fornece informações generalizadas, pois há muitas extensões de VM disponíveis e cada uma delas tem uma configuração possivelmente exclusiva.</span><span class="sxs-lookup"><span data-stu-id="6ea3e-109">This document provides generalized information because many VM extensions are available, each with a potentially unique configuration.</span></span> <span data-ttu-id="6ea3e-110">Detalhes de extensão podem ser encontrados em cada extensão individuais do documento toohello específico.</span><span class="sxs-lookup"><span data-stu-id="6ea3e-110">Extension-specific details can be found in each document specific toohello individual extension.</span></span>

## <a name="use-cases-and-samples"></a><span data-ttu-id="6ea3e-111">Casos de uso e exemplos</span><span class="sxs-lookup"><span data-stu-id="6ea3e-111">Use cases and samples</span></span>

<span data-ttu-id="6ea3e-112">Há várias extensões de VM do Azure diferentes disponíveis, cada uma com um caso de uso específico.</span><span class="sxs-lookup"><span data-stu-id="6ea3e-112">Several different Azure VM extensions are available, each with a specific use case.</span></span> <span data-ttu-id="6ea3e-113">Alguns exemplos incluem:</span><span class="sxs-lookup"><span data-stu-id="6ea3e-113">Some examples are:</span></span>

- <span data-ttu-id="6ea3e-114">Aplica PowerShell Desired configurações tooa máquina virtual em estado usando Olá extensão DSC para Linux.</span><span class="sxs-lookup"><span data-stu-id="6ea3e-114">Apply PowerShell Desired State configurations tooa virtual machine using hello DSC extension for Linux.</span></span> <span data-ttu-id="6ea3e-115">Para saber mais, confira [Extensão de configuração de Estado Desejado do Azure](https://github.com/Azure/azure-linux-extensions/tree/master/DSC).</span><span class="sxs-lookup"><span data-stu-id="6ea3e-115">For more information, see [Azure Desired State configuration extension](https://github.com/Azure/azure-linux-extensions/tree/master/DSC).</span></span>
- <span data-ttu-id="6ea3e-116">Configure o monitoramento de uma máquina virtual com hello extensão VM de agente de monitoramento da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="6ea3e-116">Configure monitoring of a virtual machine with hello Microsoft Monitoring Agent VM extension.</span></span> <span data-ttu-id="6ea3e-117">Para obter mais informações, consulte [como toomonitor uma VM do Linux](tutorial-monitoring.md).</span><span class="sxs-lookup"><span data-stu-id="6ea3e-117">For more information, see [How toomonitor a Linux VM](tutorial-monitoring.md).</span></span>
- <span data-ttu-id="6ea3e-118">Configure o monitoramento da infra-estrutura do Azure com hello Datadog extensão.</span><span class="sxs-lookup"><span data-stu-id="6ea3e-118">Configure monitoring of your Azure infrastructure with hello Datadog extension.</span></span> <span data-ttu-id="6ea3e-119">Para obter mais informações, consulte Olá [Datadog blog](https://www.datadoghq.com/blog/introducing-azure-monitoring-with-one-click-datadog-deployment/).</span><span class="sxs-lookup"><span data-stu-id="6ea3e-119">For more information, see hello [Datadog blog](https://www.datadoghq.com/blog/introducing-azure-monitoring-with-one-click-datadog-deployment/).</span></span>
- <span data-ttu-id="6ea3e-120">Configure um host Docker em uma máquina virtual do Azure usando a extensão de VM Docker hello.</span><span class="sxs-lookup"><span data-stu-id="6ea3e-120">Configure a Docker host on an Azure virtual machine using hello Docker VM extension.</span></span> <span data-ttu-id="6ea3e-121">Para saber mais, confira [Extensão de VM do Docker](dockerextension.md).</span><span class="sxs-lookup"><span data-stu-id="6ea3e-121">For more information, see [Docker VM extension](dockerextension.md).</span></span>

<span data-ttu-id="6ea3e-122">Além disso extensões específicas de tooprocess, uma extensão de Script personalizado está disponível para máquinas virtuais Windows e Linux.</span><span class="sxs-lookup"><span data-stu-id="6ea3e-122">In addition tooprocess-specific extensions, a Custom Script extension is available for both Windows and Linux virtual machines.</span></span> <span data-ttu-id="6ea3e-123">Olá extensão de Script personalizado para Linux permite que qualquer toobe de script Bash executado em uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="6ea3e-123">hello Custom Script extension for Linux allows any Bash script toobe run on a virtual machine.</span></span> <span data-ttu-id="6ea3e-124">Scripts personalizados são úteis para a criação de implantações do Azure que exigem uma configuração que vai além da capacidade das ferramentas nativas do Azure.</span><span class="sxs-lookup"><span data-stu-id="6ea3e-124">Custom scripts are useful for designing Azure deployments that require configuration beyond what native Azure tooling can provide.</span></span> <span data-ttu-id="6ea3e-125">Para saber mais, confira [Extensão de Script Personalizado de VM do Linux](extensions-customscript.md).</span><span class="sxs-lookup"><span data-stu-id="6ea3e-125">For more information, see [Linux VM Custom Script extension](extensions-customscript.md).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="6ea3e-126">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="6ea3e-126">Prerequisites</span></span>

<span data-ttu-id="6ea3e-127">Cada extensão da máquina virtual pode ter seu próprio conjunto de pré-requisitos.</span><span class="sxs-lookup"><span data-stu-id="6ea3e-127">Each virtual machine extension might have its own set of prerequisites.</span></span> <span data-ttu-id="6ea3e-128">Por exemplo, Olá extensão da VM Docker tem um pré-requisito de uma distribuição de Linux com suporte.</span><span class="sxs-lookup"><span data-stu-id="6ea3e-128">For instance, hello Docker VM extension has a prerequisite of a supported Linux distribution.</span></span> <span data-ttu-id="6ea3e-129">Requisitos das extensões individuais são detalhados na documentação do hello específicas da extensão.</span><span class="sxs-lookup"><span data-stu-id="6ea3e-129">Requirements of individual extensions are detailed in hello extension-specific documentation.</span></span>

### <a name="azure-vm-agent"></a><span data-ttu-id="6ea3e-130">Agente de VM do Azure</span><span class="sxs-lookup"><span data-stu-id="6ea3e-130">Azure VM agent</span></span>

<span data-ttu-id="6ea3e-131">Agente de VM do Azure Olá gerencia as interações entre uma máquina virtual do Azure e o controlador de malha do Azure hello.</span><span class="sxs-lookup"><span data-stu-id="6ea3e-131">hello Azure VM agent manages interactions between an Azure virtual machine and hello Azure fabric controller.</span></span> <span data-ttu-id="6ea3e-132">Olá VM agent é responsável por muitos aspectos funcionais de implantação e gerenciamento de máquinas virtuais do Azure, incluindo a execução de extensões de VM.</span><span class="sxs-lookup"><span data-stu-id="6ea3e-132">hello VM agent is responsible for many functional aspects of deploying and managing Azure virtual machines, including running VM extensions.</span></span> <span data-ttu-id="6ea3e-133">Agente de VM do Azure Olá foi pré-instalado no imagens do Azure Marketplace e pode ser instalada manualmente nos sistemas operacionais com suporte.</span><span class="sxs-lookup"><span data-stu-id="6ea3e-133">hello Azure VM agent is preinstalled on Azure Marketplace images and can be installed manually on supported operating systems.</span></span>

<span data-ttu-id="6ea3e-134">Para saber mais sobre os sistemas operacionais com suporte e as instruções de instalação, confira [Agente de máquina virtual do Azure](../windows/classic/agents-and-extensions.md).</span><span class="sxs-lookup"><span data-stu-id="6ea3e-134">For information on supported operating systems and installation instructions, see [Azure virtual machine agent](../windows/classic/agents-and-extensions.md).</span></span>

## <a name="discover-vm-extensions"></a><span data-ttu-id="6ea3e-135">Descobrir extensões de VM</span><span class="sxs-lookup"><span data-stu-id="6ea3e-135">Discover VM extensions</span></span>

<span data-ttu-id="6ea3e-136">Muitas extensões de VM diferentes estão disponíveis para uso com as máquinas virtuais do Azure.</span><span class="sxs-lookup"><span data-stu-id="6ea3e-136">Many different VM extensions are available for use with Azure virtual machines.</span></span> <span data-ttu-id="6ea3e-137">toosee uma lista completa, execute Olá comando com hello CLI do Azure a seguir, substituindo o local do exemplo hello pelo local de saudação de sua escolha.</span><span class="sxs-lookup"><span data-stu-id="6ea3e-137">toosee a complete list, run hello following command with hello Azure CLI, replacing hello example location with hello location of your choice.</span></span>

```azurecli
az vm extension image list --location westus -o table
```

## <a name="run-vm-extensions"></a><span data-ttu-id="6ea3e-138">Executar extensões de VM</span><span class="sxs-lookup"><span data-stu-id="6ea3e-138">Run VM extensions</span></span>

<span data-ttu-id="6ea3e-139">Extensões de máquina virtual do Azure podem ser executadas em máquinas virtuais existentes, que são úteis quando você precisa toomake alterações de configuração ou recuperar de conectividade em uma VM já implantada.</span><span class="sxs-lookup"><span data-stu-id="6ea3e-139">Azure virtual machine extensions can be run on existing virtual machines, which are useful when you need toomake configuration changes or recover connectivity on an already deployed VM.</span></span> <span data-ttu-id="6ea3e-140">As extensões de VM também podem ser agrupadas com implantações de modelo do Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="6ea3e-140">VM extensions can also be bundled with Azure Resource Manager template deployments.</span></span> <span data-ttu-id="6ea3e-141">Ao usar extensões com modelos do Resource Manager, as máquinas virtuais do Azure podem ser implantadas e configuradas sem intervenção pós-implantação.</span><span class="sxs-lookup"><span data-stu-id="6ea3e-141">By using extensions with Resource Manager templates, Azure virtual machines can be deployed and configured without post-deployment intervention.</span></span>

<span data-ttu-id="6ea3e-142">Olá métodos a seguir pode ser usado toorun uma extensão em uma máquina virtual existente.</span><span class="sxs-lookup"><span data-stu-id="6ea3e-142">hello following methods can be used toorun an extension against an existing virtual machine.</span></span>

### <a name="azure-cli"></a><span data-ttu-id="6ea3e-143">CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="6ea3e-143">Azure CLI</span></span>

<span data-ttu-id="6ea3e-144">Extensões de máquina virtual do Azure podem ser executadas em uma máquina virtual existente usando Olá `az vm extension set` comando.</span><span class="sxs-lookup"><span data-stu-id="6ea3e-144">Azure virtual machine extensions can be run against an existing virtual machine by using hello `az vm extension set` command.</span></span> <span data-ttu-id="6ea3e-145">Este exemplo executa a extensão do script personalizado Olá contra uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="6ea3e-145">This example runs hello custom script extension against a virtual machine.</span></span>

```azurecli
az vm extension set `
  --resource-group exttest `
  --vm-name exttest `
  --name customScript `
  --publisher Microsoft.Azure.Extensions `
  --settings '{"fileUris": ["https://gist.github.com/ahmetalpbalkan/b5d4a856fe15464015ae87d5587a4439/raw/466f5c30507c990a4d5a2f5c79f901fa89a80841/hello.sh"],"commandToExecute": "./hello.sh"}'
```

<span data-ttu-id="6ea3e-146">Olá script produz saída semelhante toohello texto a seguir:</span><span class="sxs-lookup"><span data-stu-id="6ea3e-146">hello script produces output similar toohello following text:</span></span>

```azurecli
info:    Executing command vm extension set
+ Looking up hello VM "myVM"
+ Installing extension "CustomScript", VM: "mvVM"
info:    vm extension set command OK
```

### <a name="azure-portal"></a><span data-ttu-id="6ea3e-147">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="6ea3e-147">Azure portal</span></span>

<span data-ttu-id="6ea3e-148">Extensões de VM podem ser aplicadas tooan de máquina virtual existente por meio de saudação portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="6ea3e-148">VM extensions can be applied tooan existing virtual machine through hello Azure portal.</span></span> <span data-ttu-id="6ea3e-149">toodo portanto, selecione a máquina virtual de saudação, escolha **extensões**e clique em **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="6ea3e-149">toodo so, select hello virtual machine, choose **Extensions**, and click **Add**.</span></span> <span data-ttu-id="6ea3e-150">Selecione a extensão de saudação quer Olá lista de extensões disponíveis e siga as instruções de saudação do Assistente de saudação.</span><span class="sxs-lookup"><span data-stu-id="6ea3e-150">Select hello extension you want from hello list of available extensions and follow hello instructions in hello wizard.</span></span>

<span data-ttu-id="6ea3e-151">Olá imagem a seguir mostra instalação Olá Olá extensão de Script personalizado de Linux do hello portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="6ea3e-151">hello following image shows hello installation of hello Linux Custom Script extension from hello Azure portal.</span></span>

![Instalar a extensão de script personalizado](./media/extensions-features/installscriptextensionlinux.png)

### <a name="azure-resource-manager-templates"></a><span data-ttu-id="6ea3e-153">Modelos do Gerenciador de Recursos do Azure</span><span class="sxs-lookup"><span data-stu-id="6ea3e-153">Azure Resource Manager templates</span></span>

<span data-ttu-id="6ea3e-154">Extensões de VM podem ser adicionado tooan Azure Resource Manager modelo e executado com a implantação de saudação do modelo de saudação.</span><span class="sxs-lookup"><span data-stu-id="6ea3e-154">VM extensions can be added tooan Azure Resource Manager template and executed with hello deployment of hello template.</span></span> <span data-ttu-id="6ea3e-155">Ao implantar uma extensão com um modelo, você pode criar implantações do Azure totalmente configuradas.</span><span class="sxs-lookup"><span data-stu-id="6ea3e-155">When you deploy an extension with a template, you can create fully configured Azure deployments.</span></span> <span data-ttu-id="6ea3e-156">Por exemplo, hello que JSON a seguir é obtido a partir de um modelo do Gerenciador de recursos.</span><span class="sxs-lookup"><span data-stu-id="6ea3e-156">For example, hello following JSON is taken from a Resource Manager template.</span></span> <span data-ttu-id="6ea3e-157">Olá modelo implanta um conjunto de VMs com balanceamento de carga e um banco de dados do SQL Azure e, em seguida, instala um aplicativo .NET Core em cada VM.</span><span class="sxs-lookup"><span data-stu-id="6ea3e-157">hello template deploys a set of load-balanced virtual machines and an Azure SQL database, and then installs a .NET Core application on each VM.</span></span> <span data-ttu-id="6ea3e-158">Olá extensão de VM cuida Olá da instalação do software.</span><span class="sxs-lookup"><span data-stu-id="6ea3e-158">hello VM extension takes care of hello software installation.</span></span>

<span data-ttu-id="6ea3e-159">Para obter mais informações, consulte Olá completo [modelo do Gerenciador de recursos](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-linux).</span><span class="sxs-lookup"><span data-stu-id="6ea3e-159">For more information, see hello full [Resource Manager template](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-linux).</span></span>

```json
{
    "apiVersion": "2015-06-15",
    "type": "extensions",
    "name": "config-app",
    "location": "[resourceGroup().location]",
    "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/', concat(variables('vmName'),copyindex()))]"
    ],
    "tags": {
    "displayName": "config-app"
    },
    "properties": {
    "publisher": "Microsoft.Azure.Extensions",
    "type": "CustomScript",
    "typeHandlerVersion": "2.0",
    "autoUpgradeMinorVersion": true,
    "settings": {
        "fileUris": [
        "https://raw.githubusercontent.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-linux/scripts/config-music.sh"
        ]
    },
    "protectedSettings": {
        "commandToExecute": "[concat('sudo sh config-music.sh ',variables('musicStoreSqlName'), ' ', parameters('adminUsername'), ' ', parameters('sqlAdminPassword'))]"
    }
    }
}
```

<span data-ttu-id="6ea3e-160">Para obter mais informações, confira [Criação de modelos do Azure Resource Manager](../windows/template-description.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#extensions).</span><span class="sxs-lookup"><span data-stu-id="6ea3e-160">For more information, see [Authoring Azure Resource Manager templates](../windows/template-description.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#extensions).</span></span>

## <a name="secure-vm-extension-data"></a><span data-ttu-id="6ea3e-161">Proteger dados de extensão da VM</span><span class="sxs-lookup"><span data-stu-id="6ea3e-161">Secure VM extension data</span></span>

<span data-ttu-id="6ea3e-162">Quando você estiver executando uma extensão de VM, talvez seja necessário tooinclude informações confidenciais, como as credenciais, nomes de conta de armazenamento e chaves de acesso da conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="6ea3e-162">When you're running a VM extension, it may be necessary tooinclude sensitive information such as credentials, storage account names, and storage account access keys.</span></span> <span data-ttu-id="6ea3e-163">Muitas extensões VM incluem uma configuração protegida que criptografa os dados e a descriptografa apenas dentro de saudação máquina de virtual de destino.</span><span class="sxs-lookup"><span data-stu-id="6ea3e-163">Many VM extensions include a protected configuration that encrypts data and only decrypts it inside hello target virtual machine.</span></span> <span data-ttu-id="6ea3e-164">Cada extensão tem um esquema específico de configuração protegida, e cada um é detalhado na documentação específica à extensão.</span><span class="sxs-lookup"><span data-stu-id="6ea3e-164">Each extension has a specific protected configuration schema, and each is detailed in extension-specific documentation.</span></span>

<span data-ttu-id="6ea3e-165">saudação de exemplo a seguir mostra uma instância do hello extensão de Script personalizado para Linux.</span><span class="sxs-lookup"><span data-stu-id="6ea3e-165">hello following example shows an instance of hello Custom Script extension for Linux.</span></span> <span data-ttu-id="6ea3e-166">Observe que tooexecute de comando Olá inclui um conjunto de credenciais.</span><span class="sxs-lookup"><span data-stu-id="6ea3e-166">Notice that hello command tooexecute includes a set of credentials.</span></span> <span data-ttu-id="6ea3e-167">Neste exemplo, a saudação comando tooexecute não será criptografado.</span><span class="sxs-lookup"><span data-stu-id="6ea3e-167">In this example, hello command tooexecute will not be encrypted.</span></span>


```json
{
  "apiVersion": "2015-06-15",
  "type": "extensions",
  "name": "config-app",
  "location": "[resourceGroup().location]",
  "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/', concat(variables('vmName'),copyindex()))]"
  ],
  "tags": {
    "displayName": "config-app"
  },
  "properties": {
    "publisher": "Microsoft.Azure.Extensions",
    "type": "CustomScript",
    "typeHandlerVersion": "2.0",
    "autoUpgradeMinorVersion": true,
    "settings": {
      "fileUris": [
        "https://raw.githubusercontent.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-linux/scripts/config-music.sh"
      ],
      "commandToExecute": "[concat('sudo sh config-music.sh ',variables('musicStoreSqlName'), ' ', parameters('adminUsername'), ' ', parameters('sqlAdminPassword'))]"
    }
  }
}
```

<span data-ttu-id="6ea3e-168">Olá móvel **comando tooexecute** propriedade toohello **protegido** configuração protege a cadeia de caracteres de execução de saudação.</span><span class="sxs-lookup"><span data-stu-id="6ea3e-168">Moving hello **command tooexecute** property toohello **protected** configuration secures hello execution string.</span></span>

```json
{
  "apiVersion": "2015-06-15",
  "type": "extensions",
  "name": "config-app",
  "location": "[resourceGroup().location]",
  "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/', concat(variables('vmName'),copyindex()))]"
  ],
  "tags": {
    "displayName": "config-app"
  },
  "properties": {
    "publisher": "Microsoft.Azure.Extensions",
    "type": "CustomScript",
    "typeHandlerVersion": "2.0",
    "autoUpgradeMinorVersion": true,
    "settings": {
      "fileUris": [
        "https://raw.githubusercontent.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-linux/scripts/config-music.sh"
      ]
    },
    "protectedSettings": {
      "commandToExecute": "[concat('sudo sh config-music.sh ',variables('musicStoreSqlName'), ' ', parameters('adminUsername'), ' ', parameters('sqlAdminPassword'))]"
    }
  }
}
```

## <a name="troubleshoot-vm-extensions"></a><span data-ttu-id="6ea3e-169">Solucionar problemas de extensões de VM</span><span class="sxs-lookup"><span data-stu-id="6ea3e-169">Troubleshoot VM extensions</span></span>

<span data-ttu-id="6ea3e-170">Cada extensão VM pode ter a extensão de toohello específica de etapas de solução de problemas.</span><span class="sxs-lookup"><span data-stu-id="6ea3e-170">Each VM extension may have troubleshooting steps specific toohello extension.</span></span> <span data-ttu-id="6ea3e-171">Por exemplo, quando você estiver usando a extensão de Script personalizado hello, detalhes de execução de script podem ser encontrados localmente na Olá máquina virtual no qual a extensão de saudação foi executado.</span><span class="sxs-lookup"><span data-stu-id="6ea3e-171">For example, when you're using hello Custom Script extension, script execution details can be found locally on hello virtual machine on which hello extension was run.</span></span> <span data-ttu-id="6ea3e-172">As etapas de solução de problemas específicas à extensão são detalhadas na documentação associada.</span><span class="sxs-lookup"><span data-stu-id="6ea3e-172">Any extension-specific troubleshooting steps are detailed in extension-specific documentation.</span></span>

<span data-ttu-id="6ea3e-173">Olá etapas de solução de problemas a seguir se aplicam a tooall extensões de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="6ea3e-173">hello following troubleshooting steps apply tooall virtual machine extensions.</span></span>

### <a name="view-extension-status"></a><span data-ttu-id="6ea3e-174">Exibir o status da extensão</span><span class="sxs-lookup"><span data-stu-id="6ea3e-174">View extension status</span></span>

<span data-ttu-id="6ea3e-175">Depois que uma extensão de máquina virtual tiver sido executada em uma máquina virtual, use Olá seguindo o status da extensão de tooreturn comando CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="6ea3e-175">After a virtual machine extension has been run against a virtual machine, use hello following Azure CLI command tooreturn extension status.</span></span> <span data-ttu-id="6ea3e-176">Substitua os nomes de parâmetro de exemplo por seus próprios valores.</span><span class="sxs-lookup"><span data-stu-id="6ea3e-176">Replace example parameter names with your own values.</span></span>

```azurecli
az vm extension list --resource-group myResourceGroup --vm-name myVM -o table
```

<span data-ttu-id="6ea3e-177">saída de Hello aparência Olá texto a seguir:</span><span class="sxs-lookup"><span data-stu-id="6ea3e-177">hello output looks like hello following text:</span></span>

```azurecli
AutoUpgradeMinorVersion    Location    Name          ProvisioningState    Publisher                   ResourceGroup      TypeHandlerVersion  VirtualMachineExtensionType
-------------------------  ----------  ------------  -------------------  --------------------------  ---------------  --------------------  -----------------------------
True                       westus      customScript  Succeeded            Microsoft.Azure.Extensions  exttest                             2  customScript
```

<span data-ttu-id="6ea3e-178">Status da extensão de execução também podem ser encontradas no hello portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="6ea3e-178">Extension execution status can also be found in hello Azure portal.</span></span> <span data-ttu-id="6ea3e-179">status de saudação tooview de uma extensão, a máquina virtual de select Olá, escolha **extensões**, e selecione Olá extensão desejado.</span><span class="sxs-lookup"><span data-stu-id="6ea3e-179">tooview hello status of an extension, select hello virtual machine, choose **Extensions**, and select hello desired extension.</span></span>

### <a name="rerun-a-vm-extension"></a><span data-ttu-id="6ea3e-180">Executar novamente uma extensão de VM</span><span class="sxs-lookup"><span data-stu-id="6ea3e-180">Rerun a VM extension</span></span>

<span data-ttu-id="6ea3e-181">Pode haver casos em que uma extensão de máquina virtual deve toobe novamente.</span><span class="sxs-lookup"><span data-stu-id="6ea3e-181">There may be cases in which a virtual machine extension needs toobe rerun.</span></span> <span data-ttu-id="6ea3e-182">Você pode executar novamente uma extensão, removendo-a e, em seguida, executar novamente a extensão de saudação com um método de execução de sua escolha.</span><span class="sxs-lookup"><span data-stu-id="6ea3e-182">You can rerun an extension by removing it, and then rerunning hello extension with an execution method of your choice.</span></span> <span data-ttu-id="6ea3e-183">tooremove uma extensão, executar Olá após o comando com hello CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="6ea3e-183">tooremove an extension, run hello following command with hello Azure CLI.</span></span> <span data-ttu-id="6ea3e-184">Substitua os nomes de parâmetro de exemplo por seus próprios valores.</span><span class="sxs-lookup"><span data-stu-id="6ea3e-184">Replace example parameter names with your own values.</span></span>

```azurecli
az vm extension delete --name customScript --resource-group myResourceGroup --vm-name myVM
```

<span data-ttu-id="6ea3e-185">Você pode remover uma extensão usando Olá etapas Olá portal do Azure:</span><span class="sxs-lookup"><span data-stu-id="6ea3e-185">You can remove an extension by using hello following steps in hello Azure portal:</span></span>

1. <span data-ttu-id="6ea3e-186">Selecione uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="6ea3e-186">Select a virtual machine.</span></span>
2. <span data-ttu-id="6ea3e-187">Escolha **Extensões**.</span><span class="sxs-lookup"><span data-stu-id="6ea3e-187">Choose **Extensions**.</span></span>
3. <span data-ttu-id="6ea3e-188">Selecione a extensão de saudação desejada.</span><span class="sxs-lookup"><span data-stu-id="6ea3e-188">Select hello desired extension.</span></span>
4. <span data-ttu-id="6ea3e-189">Escolha **Desinstalar**.</span><span class="sxs-lookup"><span data-stu-id="6ea3e-189">Choose **Uninstall**.</span></span>

## <a name="common-vm-extension-reference"></a><span data-ttu-id="6ea3e-190">Referência à extensão VM comum</span><span class="sxs-lookup"><span data-stu-id="6ea3e-190">Common VM extension reference</span></span>
| <span data-ttu-id="6ea3e-191">Nome da extensão</span><span class="sxs-lookup"><span data-stu-id="6ea3e-191">Extension name</span></span> | <span data-ttu-id="6ea3e-192">Descrição</span><span class="sxs-lookup"><span data-stu-id="6ea3e-192">Description</span></span> | <span data-ttu-id="6ea3e-193">Mais informações</span><span class="sxs-lookup"><span data-stu-id="6ea3e-193">More information</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6ea3e-194">Extensão de Script Personalizado para Linux</span><span class="sxs-lookup"><span data-stu-id="6ea3e-194">Custom Script extension for Linux</span></span> |<span data-ttu-id="6ea3e-195">Executar scripts em uma máquina virtual do Azure</span><span class="sxs-lookup"><span data-stu-id="6ea3e-195">Run scripts against an Azure virtual machine</span></span> |[<span data-ttu-id="6ea3e-196">Extensão de Script Personalizado para Linux</span><span class="sxs-lookup"><span data-stu-id="6ea3e-196">Custom Script extension for Linux</span></span>](extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) |
| <span data-ttu-id="6ea3e-197">Extensão do Docker</span><span class="sxs-lookup"><span data-stu-id="6ea3e-197">Docker extension</span></span> |<span data-ttu-id="6ea3e-198">Instale Olá Docker daemon toosupport remotos comandos.</span><span class="sxs-lookup"><span data-stu-id="6ea3e-198">Install hello Docker daemon toosupport remote Docker commands.</span></span> |[<span data-ttu-id="6ea3e-199">Extensão de VM do Docker</span><span class="sxs-lookup"><span data-stu-id="6ea3e-199">Docker VM extension</span></span>](dockerextension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) |
| <span data-ttu-id="6ea3e-200">Extensão de acesso à VM</span><span class="sxs-lookup"><span data-stu-id="6ea3e-200">VM Access extension</span></span> |<span data-ttu-id="6ea3e-201">Recuperar o acesso tooan máquina virtual do Azure</span><span class="sxs-lookup"><span data-stu-id="6ea3e-201">Regain access tooan Azure virtual machine</span></span> |[<span data-ttu-id="6ea3e-202">Extensão de acesso à VM</span><span class="sxs-lookup"><span data-stu-id="6ea3e-202">VM Access extension</span></span>](https://github.com/Azure/azure-linux-extensions/tree/master/VMAccess) |
| <span data-ttu-id="6ea3e-203">Extensão de Diagnóstico do Azure</span><span class="sxs-lookup"><span data-stu-id="6ea3e-203">Azure Diagnostics extension</span></span> |<span data-ttu-id="6ea3e-204">Gerenciar Diagnóstico do Azure</span><span class="sxs-lookup"><span data-stu-id="6ea3e-204">Manage Azure Diagnostics</span></span> |[<span data-ttu-id="6ea3e-205">Extensão de Diagnóstico do Azure</span><span class="sxs-lookup"><span data-stu-id="6ea3e-205">Azure Diagnostics extension</span></span>](https://azure.microsoft.com/blog/windows-azure-virtual-machine-monitoring-with-wad-extension/) |
| <span data-ttu-id="6ea3e-206">Extensão de Acesso à VM do Azure</span><span class="sxs-lookup"><span data-stu-id="6ea3e-206">Azure VM Access extension</span></span> |<span data-ttu-id="6ea3e-207">Gerenciar usuários e credenciais</span><span class="sxs-lookup"><span data-stu-id="6ea3e-207">Manage users and credentials</span></span> |[<span data-ttu-id="6ea3e-208">Extensão de Acesso à VM para Linux</span><span class="sxs-lookup"><span data-stu-id="6ea3e-208">VM Access extension for Linux</span></span>](https://azure.microsoft.com/en-us/blog/using-vmaccess-extension-to-reset-login-credentials-for-linux-vm/) |
