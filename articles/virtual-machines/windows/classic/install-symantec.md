---
title: aaaInstall Symantec Endpoint Protection em uma VM do Windows Azure | Microsoft Docs
description: "Saiba como tooinstall e configurar a extensão de segurança Olá Symantec Endpoint Protection em um novo ou existente VM do Azure criado com o modelo de implantação clássico Olá."
services: virtual-machines-windows
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 19dcebc7-da6b-4510-907b-d64088e81fa2
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-multiple
ms.devlang: na
ms.topic: article
ms.date: 03/31/2017
ms.author: iainfou
ms.openlocfilehash: cb6083366185c26c9f43ff94d835cd90725de5b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooinstall-and-configure-symantec-endpoint-protection-on-a-windows-vm"></a><span data-ttu-id="e3e1d-103">Como tooinstall e configurar o Symantec Endpoint Protection em uma VM do Windows</span><span class="sxs-lookup"><span data-stu-id="e3e1d-103">How tooinstall and configure Symantec Endpoint Protection on a Windows VM</span></span>
> [!IMPORTANT] 
> <span data-ttu-id="e3e1d-104">O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Gerenciador de Recursos e Clássico](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="e3e1d-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="e3e1d-105">Este artigo aborda usando o modelo de implantação clássico hello.</span><span class="sxs-lookup"><span data-stu-id="e3e1d-105">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="e3e1d-106">A Microsoft recomenda que mais novas implantações de usam o modelo do Gerenciador de recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="e3e1d-106">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span>

<span data-ttu-id="e3e1d-107">Este artigo mostra como tooinstall e configurar o cliente do hello Symantec Endpoint Protection em uma máquina virtual existente (VM) executando o Windows Server.</span><span class="sxs-lookup"><span data-stu-id="e3e1d-107">This article shows you how tooinstall and configure hello Symantec Endpoint Protection client on an existing virtual machine (VM) running Windows Server.</span></span> <span data-ttu-id="e3e1d-108">Este cliente completo inclui serviços como proteção contra vírus e spyware, firewall e prevenção contra intrusão.</span><span class="sxs-lookup"><span data-stu-id="e3e1d-108">This full client includes services such as virus and spyware protection, firewall, and intrusion prevention.</span></span> <span data-ttu-id="e3e1d-109">cliente de saudação é instalado como uma extensão de segurança usando Olá agente de VM.</span><span class="sxs-lookup"><span data-stu-id="e3e1d-109">hello client is installed as a security extension by using hello VM Agent.</span></span>

<span data-ttu-id="e3e1d-110">Se você tiver uma assinatura existente da Symantec para uma solução local, você pode usá-lo tooprotect suas máquinas virtuais do Azure.</span><span class="sxs-lookup"><span data-stu-id="e3e1d-110">If you have an existing subscription from Symantec for an on-premises solution, you can use it tooprotect your Azure virtual machines.</span></span> <span data-ttu-id="e3e1d-111">Se ainda não for cliente, você poderá se inscrever em uma assinatura de avaliação.</span><span class="sxs-lookup"><span data-stu-id="e3e1d-111">If you're not a customer yet, you can sign up for a trial subscription.</span></span> <span data-ttu-id="e3e1d-112">Para obter mais informações sobre essa solução, consulte [Symantec Endpoint Protection na plataforma Azure da Microsoft][Symantec].</span><span class="sxs-lookup"><span data-stu-id="e3e1d-112">For more information about this solution, see [Symantec Endpoint Protection on Microsoft's Azure platform][Symantec].</span></span> <span data-ttu-id="e3e1d-113">Essa página também contém informações de toolicensing links e instruções para instalar o cliente de saudação se você já é um cliente do Symantec.</span><span class="sxs-lookup"><span data-stu-id="e3e1d-113">This page also has links toolicensing information and instructions for installing hello client if you're already a Symantec customer.</span></span>

## <a name="install-symantec-endpoint-protection-on-an-existing-vm"></a><span data-ttu-id="e3e1d-114">Instalar o Symantec Endpoint Protection em uma VM existente</span><span class="sxs-lookup"><span data-stu-id="e3e1d-114">Install Symantec Endpoint Protection on an existing VM</span></span>
<span data-ttu-id="e3e1d-115">Antes de começar, você precisa seguir hello:</span><span class="sxs-lookup"><span data-stu-id="e3e1d-115">Before you begin, you need hello following:</span></span>

* <span data-ttu-id="e3e1d-116">módulo do PowerShell do Azure Hello, versão 0.8.2 ou posterior, no computador do trabalho.</span><span class="sxs-lookup"><span data-stu-id="e3e1d-116">hello Azure PowerShell module, version 0.8.2 or later, on your work computer.</span></span> <span data-ttu-id="e3e1d-117">Você pode verificar a versão de saudação do PowerShell do Azure que você instalou com hello **azure Get-Module | versão de formato de tabela** comando.</span><span class="sxs-lookup"><span data-stu-id="e3e1d-117">You can check hello version of Azure PowerShell that you have installed with hello **Get-Module azure | format-table version** command.</span></span> <span data-ttu-id="e3e1d-118">Para obter instruções e uma versão mais recente do link toohello, consulte [como tooInstall e configurar o Azure PowerShell][PS].</span><span class="sxs-lookup"><span data-stu-id="e3e1d-118">For instructions and a link toohello latest version, see [How tooInstall and Configure Azure PowerShell][PS].</span></span> <span data-ttu-id="e3e1d-119">Faça logon tooyour assinatura do Azure usando `Add-AzureAccount`.</span><span class="sxs-lookup"><span data-stu-id="e3e1d-119">Log in tooyour Azure subscription using `Add-AzureAccount`.</span></span>
* <span data-ttu-id="e3e1d-120">Olá Olá de agente de VM em execução em Máquina Virtual do Azure.</span><span class="sxs-lookup"><span data-stu-id="e3e1d-120">hello VM Agent running on hello Azure Virtual Machine.</span></span>

<span data-ttu-id="e3e1d-121">Primeiro, verifique se esse Olá que VM Agent já está instalado na máquina virtual de saudação.</span><span class="sxs-lookup"><span data-stu-id="e3e1d-121">First, verify that hello VM Agent is already installed on hello virtual machine.</span></span> <span data-ttu-id="e3e1d-122">Preencha o nome de serviço de nuvem hello e nome da máquina virtual e execute Olá comandos em um prompt de comando do PowerShell do Azure de nível de administrador a seguir.</span><span class="sxs-lookup"><span data-stu-id="e3e1d-122">Fill in hello cloud service name and virtual machine name, and then run hello following commands at an administrator-level Azure PowerShell command prompt.</span></span> <span data-ttu-id="e3e1d-123">Substitua tudo entre aspas hello, incluindo hello < e > caracteres.</span><span class="sxs-lookup"><span data-stu-id="e3e1d-123">Replace everything within hello quotes, including hello < and > characters.</span></span>

> [!TIP]
> <span data-ttu-id="e3e1d-124">Se você não souber o serviço de nuvem hello e nomes de máquina virtual, execute **Get-AzureVM** nomes de saudação toolist para todas as máquinas virtuais em sua assinatura atual.</span><span class="sxs-lookup"><span data-stu-id="e3e1d-124">If you don't know hello cloud service and virtual machine names, run **Get-AzureVM** toolist hello names for all virtual machines in your current subscription.</span></span>

```powershell
$CSName = "<cloud service name>"
$VMName = "<virtual machine name>"
$vm = Get-AzureVM -ServiceName $CSName -Name $VMName
write-host $vm.VM.ProvisionGuestAgent
```

<span data-ttu-id="e3e1d-125">Se hello **write-host** comando exibe **True**, Olá VM Agent está instalado.</span><span class="sxs-lookup"><span data-stu-id="e3e1d-125">If hello **write-host** command displays **True**, hello VM Agent is installed.</span></span> <span data-ttu-id="e3e1d-126">Se ele exibe **False**, consulte as instruções de saudação e um toohello link baixar Olá postagem no blog do Azure [agente de VM e extensões – parte 2][Agent].</span><span class="sxs-lookup"><span data-stu-id="e3e1d-126">If it displays **False**, see hello instructions and a link toohello download in hello Azure blog post [VM Agent and Extensions - Part 2][Agent].</span></span>

<span data-ttu-id="e3e1d-127">Se Olá agente de VM é instalado, execute agente de Symantec Endpoint Protection esses comandos tooinstall hello.</span><span class="sxs-lookup"><span data-stu-id="e3e1d-127">If hello VM Agent is installed, run these commands tooinstall hello Symantec Endpoint Protection agent.</span></span>

```powershell
$Agent = Get-AzureVMAvailableExtension -Publisher Symantec -ExtensionName SymantecEndpointProtection

Set-AzureVMExtension -Publisher Symantec –Version $Agent.Version -ExtensionName SymantecEndpointProtection \
    -VM $vm | Update-AzureVM
```

<span data-ttu-id="e3e1d-128">tooverify que Olá Symantec extensão de segurança foi instalado e é atualizado:</span><span class="sxs-lookup"><span data-stu-id="e3e1d-128">tooverify that hello Symantec security extension has been installed and is up-to-date:</span></span>

1. <span data-ttu-id="e3e1d-129">Faça logon na máquina virtual de toohello.</span><span class="sxs-lookup"><span data-stu-id="e3e1d-129">Log on toohello virtual machine.</span></span> <span data-ttu-id="e3e1d-130">Para obter instruções, consulte [como tooLog no tooa Máquina Virtual executando o Windows Server][Logon].</span><span class="sxs-lookup"><span data-stu-id="e3e1d-130">For instructions, see [How tooLog on tooa Virtual Machine Running Windows Server][Logon].</span></span>
2. <span data-ttu-id="e3e1d-131">Para Windows Server 2008 R2, clique em **Iniciar > Symantec Endpoint Protection**.</span><span class="sxs-lookup"><span data-stu-id="e3e1d-131">For Windows Server 2008 R2, click **Start > Symantec Endpoint Protection**.</span></span> <span data-ttu-id="e3e1d-132">Para o Windows Server 2012 ou Windows Server 2012 R2, na tela de início do hello, digite **Symantec**e, em seguida, clique em **Symantec Endpoint Protection**.</span><span class="sxs-lookup"><span data-stu-id="e3e1d-132">For Windows Server 2012 or Windows Server 2012 R2, from hello start screen, type **Symantec**, and then click **Symantec Endpoint Protection**.</span></span>
3. <span data-ttu-id="e3e1d-133">De saudação **Status** guia da saudação **Status Symantec Endpoint Protection** janela, aplicar atualizações ou reinicie se necessário.</span><span class="sxs-lookup"><span data-stu-id="e3e1d-133">From hello **Status** tab of hello **Status-Symantec Endpoint Protection** window, apply updates or restart if needed.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="e3e1d-134">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="e3e1d-134">Additional resources</span></span>
<span data-ttu-id="e3e1d-135">[Como tooLog no tooa Máquina Virtual executando o Windows Server][Logon]</span><span class="sxs-lookup"><span data-stu-id="e3e1d-135">[How tooLog on tooa Virtual Machine Running Windows Server][Logon]</span></span>

<span data-ttu-id="e3e1d-136">[Recursos e Extensões de VM do Azure][Ext]</span><span class="sxs-lookup"><span data-stu-id="e3e1d-136">[Azure VM Extensions and Features][Ext]</span></span>

<!--Link references-->
[Symantec]: http://www.symantec.com/connect/blogs/symantec-endpoint-protection-now-microsoft-azure

[Create]:tutorial.md

[PS]: /powershell/azureps-cmdlets-docs

[Agent]: http://go.microsoft.com/fwlink/p/?LinkId=403947

[Logon]:connect-logon.md

[Ext]: http://go.microsoft.com/fwlink/p/?linkid=390493
