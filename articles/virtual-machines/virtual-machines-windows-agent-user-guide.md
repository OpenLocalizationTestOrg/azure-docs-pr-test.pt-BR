---
title: "Visão Geral dos Agente de Máquina Virtual do Azure | Microsoft Docs"
description: "Visão Geral do Agente de Máquina Virtual do Azure"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 0a1f212e-053e-4a39-9910-8d622959f594
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 03/28/2017
ms.author: nepeters
ms.openlocfilehash: accfd5f0fec69175e584528ff9f6db66402cb89e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-virtual-machine-agent-overview"></a><span data-ttu-id="c1225-103">Visão geral do Agente de Máquina Virtual do Azure</span><span class="sxs-lookup"><span data-stu-id="c1225-103">Azure Virtual Machine Agent overview</span></span>

<span data-ttu-id="c1225-104">O Agente de VM (Máquina Virtual) do Microsoft Azure é um processo seguro e leve que gerencia a interação da VM com o Controlador de Malha do Azure.</span><span class="sxs-lookup"><span data-stu-id="c1225-104">The Microsoft Azure Virtual Machine Agent (VM Agent) is a secured, lightweight process that manages VM interaction with the Azure Fabric Controller.</span></span> <span data-ttu-id="c1225-105">O Agente de VM tem uma função fundamental na habilitação e execução de extensões de máquina virtual do Azure.</span><span class="sxs-lookup"><span data-stu-id="c1225-105">The VM Agent has a primary role in enabling and executing Azure virtual machine extensions.</span></span> <span data-ttu-id="c1225-106">Extensões de VM habilitam a configuração máquinas virtuais pós-implantação, como instalação e configuração de software.</span><span class="sxs-lookup"><span data-stu-id="c1225-106">VM Extensions enabling post deployment configuration of virtual machines, such as installing and configuring software.</span></span> <span data-ttu-id="c1225-107">Extensões de máquina virtual também habilitam os recursos de recuperação como redefinir a senha administrativa de uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="c1225-107">Virtual machine extensions also enable recovery features such as resetting the administrative password of a virtual machine.</span></span> <span data-ttu-id="c1225-108">Sem o Agente de VM do Azure, não é possível executar extensões da máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="c1225-108">Without the Azure VM Agent, virtual machine extensions cannot be run.</span></span>

<span data-ttu-id="c1225-109">Este documento fornece detalhes sobre a instalação, detecção e remoção do Agente de Máquina Virtual do Azure.</span><span class="sxs-lookup"><span data-stu-id="c1225-109">This document details installation, detection, and removal of the Azure Virtual Machine Agent.</span></span>

## <a name="install-the-vm-agent"></a><span data-ttu-id="c1225-110">Instalar o Agente VM</span><span class="sxs-lookup"><span data-stu-id="c1225-110">Install the VM Agent</span></span>

### <a name="azure-gallery-image"></a><span data-ttu-id="c1225-111">Imagem da galeria do Azure</span><span class="sxs-lookup"><span data-stu-id="c1225-111">Azure gallery image</span></span>

<span data-ttu-id="c1225-112">O Agente de VM do Azure é instalado por padrão em qualquer máquina virtual Windows implantada de uma imagem da Galeria do Azure.</span><span class="sxs-lookup"><span data-stu-id="c1225-112">The Azure VM Agent is installed by default on any Windows virtual machine deployed from an Azure Gallery image.</span></span> <span data-ttu-id="c1225-113">Ao implantar uma imagem da Galeria do Azure do Portal, PowerShell, Interface de Linha de Comando ou de um modelo do Azure Resource Manager, o Agente de VM do Azure também é instalado.</span><span class="sxs-lookup"><span data-stu-id="c1225-113">When deploying an Azure gallery image from the Portal, PowerShell, Command Line Interface, or an Azure Resource Manager template, the Azure VM Agent is also be installed.</span></span> 

### <a name="manual-installation"></a><span data-ttu-id="c1225-114">Instalação manual</span><span class="sxs-lookup"><span data-stu-id="c1225-114">Manual installation</span></span>

<span data-ttu-id="c1225-115">O agente de VM do Windows pode ser instalado manualmente usando um pacote do Windows Installer.</span><span class="sxs-lookup"><span data-stu-id="c1225-115">The Windows VM agent can be manually installed using a Windows installer package.</span></span> <span data-ttu-id="c1225-116">A instalação manual pode ser necessária ao criar uma imagem de máquina virtual personalizada que será implantada no Azure.</span><span class="sxs-lookup"><span data-stu-id="c1225-116">Manual installation may be necessary when creating a custom virtual machine image that will be deployed in Azure.</span></span> <span data-ttu-id="c1225-117">Para instalar o Agente de VM do Windows manualmente, baixe o instalador do Agente de VM deste local [Download do Agente de VM do Microsoft Azure](http://go.microsoft.com/fwlink/?LinkID=394789).</span><span class="sxs-lookup"><span data-stu-id="c1225-117">To manually install the Windows VM Agent, download the VM Agent installer from this location [Windows Azure VM Agent Download](http://go.microsoft.com/fwlink/?LinkID=394789).</span></span> 

<span data-ttu-id="c1225-118">O Agente de VM pode ser instalado clicando duas vezes no arquivo do Windows Installer.</span><span class="sxs-lookup"><span data-stu-id="c1225-118">The VM Agent can be installed by double-clicking the windows installer file.</span></span> <span data-ttu-id="c1225-119">Para uma instalação silenciosa ou autônomo do agente de VM, execute o comando a seguir.</span><span class="sxs-lookup"><span data-stu-id="c1225-119">For an automated or unattended installation of the VM agent, run the following command.</span></span>

```cmd
msiexec.exe /i WindowsAzureVmAgent.2.7.1198.778.rd_art_stable.160617-1120.fre /quiet
```

## <a name="detect-the-vm-agent"></a><span data-ttu-id="c1225-120">Detectar o Agente de VM</span><span class="sxs-lookup"><span data-stu-id="c1225-120">Detect the VM Agent</span></span>

### <a name="powershell"></a><span data-ttu-id="c1225-121">PowerShell</span><span class="sxs-lookup"><span data-stu-id="c1225-121">PowerShell</span></span>

<span data-ttu-id="c1225-122">O módulo do Azure Resource Manager PowerShell pode ser usado para recuperar informações sobre as Máquinas Virtuais do Azure.</span><span class="sxs-lookup"><span data-stu-id="c1225-122">The Azure Resource Manager PowerShell module can be used to retrieve information about Azure Virtual Machines.</span></span> <span data-ttu-id="c1225-123">Executar `Get-AzureRmVM` retorna bastante informação, incluindo o estado de provisionamento do Agente de VM do Azure.</span><span class="sxs-lookup"><span data-stu-id="c1225-123">Running `Get-AzureRmVM` returns quite a bit of information including the provisioning state for the Azure VM Agent.</span></span>

```PowerShell
Get-AzureRmVM
```

<span data-ttu-id="c1225-124">Este é apenas um subconjunto da saída do `Get-AzureRmVM`.</span><span class="sxs-lookup"><span data-stu-id="c1225-124">The following is just a subset of the `Get-AzureRmVM` output.</span></span> <span data-ttu-id="c1225-125">Observe a propriedade `ProvisionVMAgent` aninhada em `OSProfile`, que poderá ser usada para determinar se o agente de VM foi implantado na máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="c1225-125">Notice the `ProvisionVMAgent` property nested inside `OSProfile`, this property can be used to determine if the VM agent has been deployed to the virtual machine.</span></span>

```PowerShell
OSProfile                  :
  ComputerName             : myVM
  AdminUsername            : muUserName
  WindowsConfiguration     :
    ProvisionVMAgent       : True
    EnableAutomaticUpdates : True
```

<span data-ttu-id="c1225-126">O script a seguir pode ser usado para retornar uma lista concisa de nomes de máquina virtual e o estado do Agente de VM.</span><span class="sxs-lookup"><span data-stu-id="c1225-126">The following script can be used to return a concise list of virtual machine names and the state of the VM Agent.</span></span>

```PowerShell
$vms = Get-AzureRmVM

foreach ($vm in $vms) {
    $agent = $vm | Select -ExpandProperty OSProfile | Select -ExpandProperty Windowsconfiguration | Select ProvisionVMAgent
    Write-Host $vm.Name $agent.ProvisionVMAgent
}
```

### <a name="manual-detection"></a><span data-ttu-id="c1225-127">Detecção Manual</span><span class="sxs-lookup"><span data-stu-id="c1225-127">Manual Detection</span></span>

<span data-ttu-id="c1225-128">Quando conectado a uma VM do Microsoft Azure, o gerenciador de tarefas pode ser usado para examinar os processos em execução.</span><span class="sxs-lookup"><span data-stu-id="c1225-128">When logged in to a Windows Azure VM, task manager can be used to examine running processes.</span></span> <span data-ttu-id="c1225-129">Para verificar o Agente de VM do Azure, abra o Gerenciador de Tarefas > clique na guia Detalhes e procure pelo nome de processo `WindowsAzureGuestAgent.exe`.</span><span class="sxs-lookup"><span data-stu-id="c1225-129">To check for the Azure VM Agent, open Task Manager > click the details tab, and look for a process name `WindowsAzureGuestAgent.exe`.</span></span> <span data-ttu-id="c1225-130">A presença desse processo indica que o agente de VM está instalado.</span><span class="sxs-lookup"><span data-stu-id="c1225-130">The presence of this process indicates that the VM agent is installed.</span></span>

## <a name="upgrade-the-vm-agent"></a><span data-ttu-id="c1225-131">Atualizar o Agente de VM</span><span class="sxs-lookup"><span data-stu-id="c1225-131">Upgrade the VM Agent</span></span>

<span data-ttu-id="c1225-132">O Agente de VM do Azure para Windows é atualizado automaticamente.</span><span class="sxs-lookup"><span data-stu-id="c1225-132">The Azure VM Agent for Windows is automatically upgraded.</span></span> <span data-ttu-id="c1225-133">Conforme novas máquinas virtuais são implantadas no Azure, elas receberão o agente de VM mais recente.</span><span class="sxs-lookup"><span data-stu-id="c1225-133">As new virtual machines are deployed to Azure, they receive the latest VM agent.</span></span> <span data-ttu-id="c1225-134">Imagens de VM personalizadas devem ser atualizadas manualmente para incluir o novo agente de VM.</span><span class="sxs-lookup"><span data-stu-id="c1225-134">Custom VM images should be manually updated to include the new VM agent.</span></span>