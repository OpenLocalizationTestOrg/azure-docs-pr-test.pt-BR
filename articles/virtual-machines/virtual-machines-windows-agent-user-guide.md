---
title: "Visão geral do agente de máquina Virtual de aaaAzure | Microsoft Docs"
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
ms.openlocfilehash: 178766925673419cd661dbb460b8427bbfaf54e7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-virtual-machine-agent-overview"></a><span data-ttu-id="3bc9e-103">Visão geral do Agente de Máquina Virtual do Azure</span><span class="sxs-lookup"><span data-stu-id="3bc9e-103">Azure Virtual Machine Agent overview</span></span>

<span data-ttu-id="3bc9e-104">Olá agente da máquina Virtual Microsoft Azure (agente de VM) é um processo seguro e leve que gerencia a interação de VM com hello controlador de malha do Azure.</span><span class="sxs-lookup"><span data-stu-id="3bc9e-104">hello Microsoft Azure Virtual Machine Agent (VM Agent) is a secured, lightweight process that manages VM interaction with hello Azure Fabric Controller.</span></span> <span data-ttu-id="3bc9e-105">Olá agente de VM tem papel fundamental na habilitação e execução de extensões de máquina virtual do Azure.</span><span class="sxs-lookup"><span data-stu-id="3bc9e-105">hello VM Agent has a primary role in enabling and executing Azure virtual machine extensions.</span></span> <span data-ttu-id="3bc9e-106">Extensões de VM habilitam a configuração máquinas virtuais pós-implantação, como instalação e configuração de software.</span><span class="sxs-lookup"><span data-stu-id="3bc9e-106">VM Extensions enabling post deployment configuration of virtual machines, such as installing and configuring software.</span></span> <span data-ttu-id="3bc9e-107">Extensões de máquina virtual também habilitar os recursos de recuperação como redefinir a senha administrativa saudação de uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="3bc9e-107">Virtual machine extensions also enable recovery features such as resetting hello administrative password of a virtual machine.</span></span> <span data-ttu-id="3bc9e-108">Sem hello Azure VM Agent, extensões de máquina virtual não podem ser executadas.</span><span class="sxs-lookup"><span data-stu-id="3bc9e-108">Without hello Azure VM Agent, virtual machine extensions cannot be run.</span></span>

<span data-ttu-id="3bc9e-109">Este documento fornece detalhes sobre a instalação, a detecção e a remoção de saudação agente da máquina Virtual do Azure.</span><span class="sxs-lookup"><span data-stu-id="3bc9e-109">This document details installation, detection, and removal of hello Azure Virtual Machine Agent.</span></span>

## <a name="install-hello-vm-agent"></a><span data-ttu-id="3bc9e-110">Instalar Olá agente de VM</span><span class="sxs-lookup"><span data-stu-id="3bc9e-110">Install hello VM Agent</span></span>

### <a name="azure-gallery-image"></a><span data-ttu-id="3bc9e-111">Imagem da galeria do Azure</span><span class="sxs-lookup"><span data-stu-id="3bc9e-111">Azure gallery image</span></span>

<span data-ttu-id="3bc9e-112">Hello Azure VM Agent é instalado por padrão em qualquer máquina virtual do Windows implantada a partir de uma imagem da Galeria do Azure.</span><span class="sxs-lookup"><span data-stu-id="3bc9e-112">hello Azure VM Agent is installed by default on any Windows virtual machine deployed from an Azure Gallery image.</span></span> <span data-ttu-id="3bc9e-113">Quando implantar uma imagem da Galeria do Azure de saudação Portal, o PowerShell, Interface de linha de comando ou um modelo do Gerenciador de recursos do Azure, hello que Azure VM Agent também é instalado.</span><span class="sxs-lookup"><span data-stu-id="3bc9e-113">When deploying an Azure gallery image from hello Portal, PowerShell, Command Line Interface, or an Azure Resource Manager template, hello Azure VM Agent is also be installed.</span></span> 

### <a name="manual-installation"></a><span data-ttu-id="3bc9e-114">Instalação manual</span><span class="sxs-lookup"><span data-stu-id="3bc9e-114">Manual installation</span></span>

<span data-ttu-id="3bc9e-115">Agente de VM do Windows Hello pode ser instalado manualmente usando um pacote do Windows installer.</span><span class="sxs-lookup"><span data-stu-id="3bc9e-115">hello Windows VM agent can be manually installed using a Windows installer package.</span></span> <span data-ttu-id="3bc9e-116">A instalação manual pode ser necessária ao criar uma imagem de máquina virtual personalizada que será implantada no Azure.</span><span class="sxs-lookup"><span data-stu-id="3bc9e-116">Manual installation may be necessary when creating a custom virtual machine image that will be deployed in Azure.</span></span> <span data-ttu-id="3bc9e-117">toomanually saudação de instalação do agente de VM do Windows, baixar o instalador do agente de VM Olá deste local [Download do Windows Azure VM Agent](http://go.microsoft.com/fwlink/?LinkID=394789).</span><span class="sxs-lookup"><span data-stu-id="3bc9e-117">toomanually install hello Windows VM Agent, download hello VM Agent installer from this location [Windows Azure VM Agent Download](http://go.microsoft.com/fwlink/?LinkID=394789).</span></span> 

<span data-ttu-id="3bc9e-118">Olá agente de VM pode ser instalado, clique duas vezes o arquivo de instalador do windows hello.</span><span class="sxs-lookup"><span data-stu-id="3bc9e-118">hello VM Agent can be installed by double-clicking hello windows installer file.</span></span> <span data-ttu-id="3bc9e-119">Para uma instalação autônoma ou automatizada hello do agente de VM, execute Olá comando a seguir.</span><span class="sxs-lookup"><span data-stu-id="3bc9e-119">For an automated or unattended installation of hello VM agent, run hello following command.</span></span>

```cmd
msiexec.exe /i WindowsAzureVmAgent.2.7.1198.778.rd_art_stable.160617-1120.fre /quiet
```

## <a name="detect-hello-vm-agent"></a><span data-ttu-id="3bc9e-120">Detectar Olá agente de VM</span><span class="sxs-lookup"><span data-stu-id="3bc9e-120">Detect hello VM Agent</span></span>

### <a name="powershell"></a><span data-ttu-id="3bc9e-121">PowerShell</span><span class="sxs-lookup"><span data-stu-id="3bc9e-121">PowerShell</span></span>

<span data-ttu-id="3bc9e-122">módulo do PowerShell do Azure Resource Manager Olá pode ser usado tooretrieve informações sobre as máquinas virtuais do Azure.</span><span class="sxs-lookup"><span data-stu-id="3bc9e-122">hello Azure Resource Manager PowerShell module can be used tooretrieve information about Azure Virtual Machines.</span></span> <span data-ttu-id="3bc9e-123">Executando `Get-AzureRmVM` retorna uma grande quantidade de informações incluindo Olá estado para hello Azure VM Agent de provisionamento.</span><span class="sxs-lookup"><span data-stu-id="3bc9e-123">Running `Get-AzureRmVM` returns quite a bit of information including hello provisioning state for hello Azure VM Agent.</span></span>

```PowerShell
Get-AzureRmVM
```

<span data-ttu-id="3bc9e-124">Olá, a seguir é apenas um subconjunto de saudação `Get-AzureRmVM` saída.</span><span class="sxs-lookup"><span data-stu-id="3bc9e-124">hello following is just a subset of hello `Get-AzureRmVM` output.</span></span> <span data-ttu-id="3bc9e-125">Saudação de aviso `ProvisionVMAgent` propriedade aninhado em `OSProfile`, essa propriedade pode ser usado toodetermine se o agente de VM Olá tiver sido implantado toohello virtual machine.</span><span class="sxs-lookup"><span data-stu-id="3bc9e-125">Notice hello `ProvisionVMAgent` property nested inside `OSProfile`, this property can be used toodetermine if hello VM agent has been deployed toohello virtual machine.</span></span>

```PowerShell
OSProfile                  :
  ComputerName             : myVM
  AdminUsername            : muUserName
  WindowsConfiguration     :
    ProvisionVMAgent       : True
    EnableAutomaticUpdates : True
```

<span data-ttu-id="3bc9e-126">saudação de script a seguir pode ser usado tooreturn uma lista concisa de nomes de máquina virtual e o estado de saudação do hello agente de VM.</span><span class="sxs-lookup"><span data-stu-id="3bc9e-126">hello following script can be used tooreturn a concise list of virtual machine names and hello state of hello VM Agent.</span></span>

```PowerShell
$vms = Get-AzureRmVM

foreach ($vm in $vms) {
    $agent = $vm | Select -ExpandProperty OSProfile | Select -ExpandProperty Windowsconfiguration | Select ProvisionVMAgent
    Write-Host $vm.Name $agent.ProvisionVMAgent
}
```

### <a name="manual-detection"></a><span data-ttu-id="3bc9e-127">Detecção Manual</span><span class="sxs-lookup"><span data-stu-id="3bc9e-127">Manual Detection</span></span>

<span data-ttu-id="3bc9e-128">Quando conectado tooa VM do Windows Azure, o Gerenciador de tarefas pode ser usado tooexamine processos em execução.</span><span class="sxs-lookup"><span data-stu-id="3bc9e-128">When logged in tooa Windows Azure VM, task manager can be used tooexamine running processes.</span></span> <span data-ttu-id="3bc9e-129">toocheck para hello Azure VM Agent, abra o Gerenciador de tarefas > clique Olá guia de detalhes e procure um nome de processo `WindowsAzureGuestAgent.exe`.</span><span class="sxs-lookup"><span data-stu-id="3bc9e-129">toocheck for hello Azure VM Agent, open Task Manager > click hello details tab, and look for a process name `WindowsAzureGuestAgent.exe`.</span></span> <span data-ttu-id="3bc9e-130">presença de Hello desse processo indica que o agente de VM hello está instalado.</span><span class="sxs-lookup"><span data-stu-id="3bc9e-130">hello presence of this process indicates that hello VM agent is installed.</span></span>

## <a name="upgrade-hello-vm-agent"></a><span data-ttu-id="3bc9e-131">Atualizar Olá agente de VM</span><span class="sxs-lookup"><span data-stu-id="3bc9e-131">Upgrade hello VM Agent</span></span>

<span data-ttu-id="3bc9e-132">Hello Azure VM Agent do Windows será atualizado automaticamente.</span><span class="sxs-lookup"><span data-stu-id="3bc9e-132">hello Azure VM Agent for Windows is automatically upgraded.</span></span> <span data-ttu-id="3bc9e-133">Conforme novas máquinas virtuais são implantada tooAzure, eles recebem agente VM mais recente da saudação.</span><span class="sxs-lookup"><span data-stu-id="3bc9e-133">As new virtual machines are deployed tooAzure, they receive hello latest VM agent.</span></span> <span data-ttu-id="3bc9e-134">Imagens VM personalizadas devem ser atualizadas manualmente tooinclude Olá novo agente de VM.</span><span class="sxs-lookup"><span data-stu-id="3bc9e-134">Custom VM images should be manually updated tooinclude hello new VM agent.</span></span>
