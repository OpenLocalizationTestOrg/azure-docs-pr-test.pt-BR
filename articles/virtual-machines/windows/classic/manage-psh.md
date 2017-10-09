---
title: "aaaManage suas máquinas virtuais usando o PowerShell do Azure | Microsoft Docs"
description: "Saiba mais sobre comandos que você pode usar tarefas tooautomate no gerenciamento de suas máquinas virtuais."
services: virtual-machines-windows
documentationcenter: windows
author: singhkays
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 7cdf9bd3-6578-4069-8a95-e8585f04a394
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 10/12/2016
ms.author: kasing
ms.openlocfilehash: e4ca6f098519243a321eac98b6692790fe18c22c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-your-virtual-machines-by-using-azure-powershell"></a><span data-ttu-id="2e9e0-103">Gerenciar suas máquinas virtuais usando o Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="2e9e0-103">Manage your virtual machines by using Azure PowerShell</span></span>
> [!IMPORTANT] 
> <span data-ttu-id="2e9e0-104">O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Gerenciador de Recursos e Clássico](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="2e9e0-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="2e9e0-105">Este artigo aborda usando o modelo de implantação clássico hello.</span><span class="sxs-lookup"><span data-stu-id="2e9e0-105">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="2e9e0-106">A Microsoft recomenda que mais novas implantações de usam o modelo do Gerenciador de recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="2e9e0-106">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="2e9e0-107">Para comandos comuns do PowerShell usando o modelo do Gerenciador de recursos de hello, consulte [aqui](../../virtual-machines-windows-ps-common-ref.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="2e9e0-107">For common PowerShell commands using hello Resource Manager model, see [here](../../virtual-machines-windows-ps-common-ref.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="2e9e0-108">Muitas tarefas que você executa a cada dia toomanage suas VMs podem ser automatizadas usando cmdlets do PowerShell do Azure.</span><span class="sxs-lookup"><span data-stu-id="2e9e0-108">Many tasks you do each day toomanage your VMs can be automated by using Azure PowerShell cmdlets.</span></span> <span data-ttu-id="2e9e0-109">Este artigo fornece comandos de exemplo para as tarefas mais simples e tooarticles links que mostram comandos Olá para tarefas mais complexas.</span><span class="sxs-lookup"><span data-stu-id="2e9e0-109">This article gives you example commands for simpler tasks, and links tooarticles that show hello commands for more complex tasks.</span></span>

> [!NOTE]
> <span data-ttu-id="2e9e0-110">Se você ainda não tiver instalado e configurado o Azure PowerShell, você pode obter as instruções no artigo Olá [como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="2e9e0-110">If you haven't installed and configured Azure PowerShell yet, you can get instructions in hello article [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>
> 
> 

## <a name="how-toouse-hello-example-commands"></a><span data-ttu-id="2e9e0-111">Como toouse Olá comandos de exemplo</span><span class="sxs-lookup"><span data-stu-id="2e9e0-111">How toouse hello example commands</span></span>
<span data-ttu-id="2e9e0-112">Você precisará tooreplace parte do texto de saudação em Olá comandos com o texto que é apropriado para seu ambiente.</span><span class="sxs-lookup"><span data-stu-id="2e9e0-112">You'll need tooreplace some of hello text in hello commands with text that's appropriate for your environment.</span></span> <span data-ttu-id="2e9e0-113">Olá < e > símbolos indicam texto necessário tooreplace.</span><span class="sxs-lookup"><span data-stu-id="2e9e0-113">hello < and > symbols indicate text you need tooreplace.</span></span> <span data-ttu-id="2e9e0-114">Quando você substituir o texto de saudação, remover Olá símbolos, mas deixe Olá aspas no lugar.</span><span class="sxs-lookup"><span data-stu-id="2e9e0-114">When you replace hello text, remove hello symbols but leave hello quote marks in place.</span></span>

## <a name="get-a-vm"></a><span data-ttu-id="2e9e0-115">Obter uma VM</span><span class="sxs-lookup"><span data-stu-id="2e9e0-115">Get a VM</span></span>
<span data-ttu-id="2e9e0-116">Essa é uma tarefa básica que você usará com frequência.</span><span class="sxs-lookup"><span data-stu-id="2e9e0-116">This is a basic task you'll use often.</span></span> <span data-ttu-id="2e9e0-117">Usá-lo tooget informações sobre uma VM, executar tarefas em uma máquina virtual ou obter saída toostore em uma variável.</span><span class="sxs-lookup"><span data-stu-id="2e9e0-117">Use it tooget information about a VM, perform tasks on a VM, or get output toostore in a variable.</span></span>

<span data-ttu-id="2e9e0-118">tooget informações sobre Olá VM, execute este comando, substituindo tudo entre aspas hello, incluindo hello < e > caracteres:</span><span class="sxs-lookup"><span data-stu-id="2e9e0-118">tooget information about hello VM, run this command, replacing everything in hello quotes, including hello < and > characters:</span></span>

     Get-AzureVM -ServiceName "<cloud service name>" -Name "<virtual machine name>"

<span data-ttu-id="2e9e0-119">Olá toostore de saída em uma variável $vm, execute:</span><span class="sxs-lookup"><span data-stu-id="2e9e0-119">toostore hello output in a $vm variable, run:</span></span>

    $vm = Get-AzureVM -ServiceName "<cloud service name>" -Name "<virtual machine name>"

## <a name="log-on-tooa-windows-based-vm"></a><span data-ttu-id="2e9e0-120">Faça logon no tooa VM baseado no Windows</span><span class="sxs-lookup"><span data-stu-id="2e9e0-120">Log on tooa Windows-based VM</span></span>
<span data-ttu-id="2e9e0-121">Execute estes comandos:</span><span class="sxs-lookup"><span data-stu-id="2e9e0-121">Run these commands:</span></span>

> [!NOTE]
> <span data-ttu-id="2e9e0-122">Você pode obter a máquina virtual de saudação e o nome do serviço de nuvem da exibição de saudação do hello **Get-AzureVM** comando.</span><span class="sxs-lookup"><span data-stu-id="2e9e0-122">You can get hello virtual machine and cloud service name from hello display of hello **Get-AzureVM** command.</span></span>
> 
> <span data-ttu-id="2e9e0-123">$svcName = "<cloud service name>" $vmName = "<virtual machine name>" $localPath = "< unidade e a pasta toostore de local Olá baixado arquivo RDP, exemplo: c:\temp >" $localFile = $localPath + "\" + $vmname +". rdp"Get-AzureRemoteDesktopFile - ServiceName $svcName-nome $vmName - LocalPath $localFile-iniciar</span><span class="sxs-lookup"><span data-stu-id="2e9e0-123">$svcName = "<cloud service name>" $vmName = "<virtual machine name>" $localPath = "<drive and folder location toostore hello downloaded RDP file, example: c:\temp >" $localFile = $localPath + "\" + $vmname + ".rdp" Get-AzureRemoteDesktopFile -ServiceName $svcName -Name $vmName -LocalPath $localFile -Launch</span></span>
> 
> 

## <a name="stop-a-vm"></a><span data-ttu-id="2e9e0-124">Parar uma VM</span><span class="sxs-lookup"><span data-stu-id="2e9e0-124">Stop a VM</span></span>
<span data-ttu-id="2e9e0-125">Execute este comando:</span><span class="sxs-lookup"><span data-stu-id="2e9e0-125">Run this command:</span></span>

    Stop-AzureVM -ServiceName "<cloud service name>" -Name "<virtual machine name>"

> [!IMPORTANT]
> <span data-ttu-id="2e9e0-126">Use este Olá tookeep de parâmetro IP virtual (VIP) da nuvem de saudação do serviço caso ele esteja Olá última VM no serviço em nuvem.</span><span class="sxs-lookup"><span data-stu-id="2e9e0-126">Use this parameter tookeep hello virtual IP (VIP) of hello cloud service in case it's hello last VM in that cloud service.</span></span> <br><br> <span data-ttu-id="2e9e0-127">Se você usar o parâmetro de StayProvisioned hello, você ainda será cobrado por Olá VM.</span><span class="sxs-lookup"><span data-stu-id="2e9e0-127">If you use hello StayProvisioned parameter, you'll still be billed for hello VM.</span></span>
> 
> 

## <a name="start-a-vm"></a><span data-ttu-id="2e9e0-128">Iniciar uma VM</span><span class="sxs-lookup"><span data-stu-id="2e9e0-128">Start a VM</span></span>
<span data-ttu-id="2e9e0-129">Execute este comando:</span><span class="sxs-lookup"><span data-stu-id="2e9e0-129">Run this command:</span></span>

    Start-AzureVM -ServiceName "<cloud service name>" -Name "<virtual machine name>"

## <a name="attach-a-data-disk"></a><span data-ttu-id="2e9e0-130">Anexar um disco de dados</span><span class="sxs-lookup"><span data-stu-id="2e9e0-130">Attach a data disk</span></span>
<span data-ttu-id="2e9e0-131">Essa tarefa requer algumas etapas.</span><span class="sxs-lookup"><span data-stu-id="2e9e0-131">This task requires a few steps.</span></span> <span data-ttu-id="2e9e0-132">Primeiro, você pode usar hello * Add-AzureDataDisk * cmdlet tooadd Olá toohello $vm objeto de disco.</span><span class="sxs-lookup"><span data-stu-id="2e9e0-132">First, you use hello ****Add-AzureDataDisk**** cmdlet tooadd hello disk toohello $vm object.</span></span> <span data-ttu-id="2e9e0-133">Em seguida, você use **Update-AzureVM** configuração de saudação do cmdlet tooupdate de saudação VM.</span><span class="sxs-lookup"><span data-stu-id="2e9e0-133">Then, you use **Update-AzureVM** cmdlet tooupdate hello configuration of hello VM.</span></span>

<span data-ttu-id="2e9e0-134">Você também precisará toodecide se tooattach um novo disco ou uma que contém dados.</span><span class="sxs-lookup"><span data-stu-id="2e9e0-134">You'll also need toodecide whether tooattach a new disk or one that contains data.</span></span> <span data-ttu-id="2e9e0-135">Para um novo disco, o comando de saudação cria o arquivo. vhd de saudação e anexa-o.</span><span class="sxs-lookup"><span data-stu-id="2e9e0-135">For a new disk, hello command creates hello .vhd file and attaches it.</span></span>

<span data-ttu-id="2e9e0-136">tooattach um novo disco, execute este comando:</span><span class="sxs-lookup"><span data-stu-id="2e9e0-136">tooattach a new disk, run this command:</span></span>

    Add-AzureDataDisk -CreateNew -DiskSizeInGB 128 -DiskLabel "<main>" -LUN <0> -VM $vm | Update-AzureVM

<span data-ttu-id="2e9e0-137">tooattach um disco de dados existente, execute este comando:</span><span class="sxs-lookup"><span data-stu-id="2e9e0-137">tooattach an existing data disk, run this command:</span></span>

    Add-AzureDataDisk -Import -DiskName "<MyExistingDisk>" -LUN <0> | Update-AzureVM

<span data-ttu-id="2e9e0-138">tooattach discos de dados de um arquivo. vhd existente no armazenamento de blob, execute este comando:</span><span class="sxs-lookup"><span data-stu-id="2e9e0-138">tooattach data disks from an existing .vhd file in blob storage, run this command:</span></span>

    Add-AzureDataDisk -ImportFrom -MediaLocation `
              "<https://mystorage.blob.core.windows.net/mycontainer/MyExistingDisk.vhd>" `
              -DiskLabel "<main>" -LUN <0> |
              Update-AzureVM

## <a name="create-a-windows-based-vm"></a><span data-ttu-id="2e9e0-139">Criar uma VM baseada no Windows</span><span class="sxs-lookup"><span data-stu-id="2e9e0-139">Create a Windows-based VM</span></span>
<span data-ttu-id="2e9e0-140">toocreate uma nova máquina de virtual baseado no Windows no Azure, use as instruções de saudação no [toocreate de usar o Azure PowerShell e pré-configurar máquinas virtuais baseadas em Windows](create-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="2e9e0-140">toocreate a new Windows-based virtual machine in Azure, use hello instructions in [Use Azure PowerShell toocreate and preconfigure Windows-based virtual machines](create-powershell.md).</span></span> <span data-ttu-id="2e9e0-141">Este tópico apresenta etapas você na criação de saudação de um comando set que do PowerShell do Azure cria uma VM com base em Windows que pode ser pré-configurados:</span><span class="sxs-lookup"><span data-stu-id="2e9e0-141">This topic steps you through hello creation of an Azure PowerShell command set that creates a Windows-based VM that can be preconfigured:</span></span>

* <span data-ttu-id="2e9e0-142">Com associação de domínio do Active Directory.</span><span class="sxs-lookup"><span data-stu-id="2e9e0-142">With Active Directory domain membership.</span></span>
* <span data-ttu-id="2e9e0-143">Com discos adicionais.</span><span class="sxs-lookup"><span data-stu-id="2e9e0-143">With additional disks.</span></span>
* <span data-ttu-id="2e9e0-144">Como membro de um conjunto de balanceamento de carga existente.</span><span class="sxs-lookup"><span data-stu-id="2e9e0-144">As a member of an existing load-balanced set.</span></span>
* <span data-ttu-id="2e9e0-145">Com um endereço IP estático.</span><span class="sxs-lookup"><span data-stu-id="2e9e0-145">With a static IP address.</span></span>

