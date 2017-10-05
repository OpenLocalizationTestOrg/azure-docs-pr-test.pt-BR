---
title: "Redimensionar uma VM do Windows no modelo de implantação clássico – Azure | Microsoft Docs"
description: "Redimensione uma máquina virtual do Windows criada no modelo de implantação clássico usando o Azure PowerShell."
services: virtual-machines-windows
documentationcenter: 
author: Drewm3
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: e3038215-001c-406e-904d-e0f4e326a4c7
ms.service: virtual-machines-windows
ms.workload: na
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 10/19/2016
ms.author: drewm
ms.openlocfilehash: 4277bc8394c7ba140291e9dc776162e87deab96b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="resize-a-windows-vm-created-in-the-classic-deployment-model"></a><span data-ttu-id="5bc5b-103">Redimensionar uma VM do Windows criada no modelo de implantação clássico</span><span class="sxs-lookup"><span data-stu-id="5bc5b-103">Resize a Windows VM created in the classic deployment model</span></span>
<span data-ttu-id="5bc5b-104">Este artigo mostra como redimensionar uma VM do Windows criada no modelo de implantação clássico usando o Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="5bc5b-104">This article shows you how to resize a Windows VM, created in the classic deployment model using Azure Powershell.</span></span>

<span data-ttu-id="5bc5b-105">Ao considerar a capacidade de redimensionar uma VM, há dois conceitos que controlam o intervalo de tamanhos disponíveis para redimensionar a máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="5bc5b-105">When considering the ability to resize a VM, there are two concepts which control the range of sizes available to resize the virtual machine.</span></span> <span data-ttu-id="5bc5b-106">O primeiro conceito é a região na qual a VM está implantada.</span><span class="sxs-lookup"><span data-stu-id="5bc5b-106">The first concept is the region in which your VM is deployed.</span></span> <span data-ttu-id="5bc5b-107">A lista de tamanhos de VM disponíveis na região está na guia Serviços da página da Web Regiões do Azure.</span><span class="sxs-lookup"><span data-stu-id="5bc5b-107">The list of VM sizes available in region is under the Services tab of the Azure Regions web page.</span></span> <span data-ttu-id="5bc5b-108">O segundo conceito é o hardware físico que atualmente hospeda sua VM.</span><span class="sxs-lookup"><span data-stu-id="5bc5b-108">The second concept is the physical hardware currently hosting your VM.</span></span> <span data-ttu-id="5bc5b-109">Os servidores físicos que hospedam as VMs são agrupados em clusters de hardware físico comum.</span><span class="sxs-lookup"><span data-stu-id="5bc5b-109">The physical servers hosting VMs are grouped together in clusters of common physical hardware.</span></span> <span data-ttu-id="5bc5b-110">O método para alterar o tamanho de uma VM varia dependendo de se o cluster de hardware que atualmente hospeda a VM tem suporte para o novo tamanho de VM desejado.</span><span class="sxs-lookup"><span data-stu-id="5bc5b-110">The method of changing a VM size differs depending on if the desired new VM size is supported by the hardware cluster currently hosting the VM.</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="5bc5b-111">O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Gerenciador de Recursos e Clássico](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="5bc5b-111">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="5bc5b-112">Este artigo aborda o uso do modelo de implantação Clássica.</span><span class="sxs-lookup"><span data-stu-id="5bc5b-112">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="5bc5b-113">A Microsoft recomenda que a maioria das implantações novas use o modelo do Gerenciador de Recursos.</span><span class="sxs-lookup"><span data-stu-id="5bc5b-113">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="5bc5b-114">Você também pode [redimensionar uma VM criada no modelo de implantação do Resource Manager](../resize-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="5bc5b-114">You can also [resize a VM created in the Resource Manager deployment model](../resize-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

## <a name="add-your-account"></a><span data-ttu-id="5bc5b-115">Adicionar sua conta</span><span class="sxs-lookup"><span data-stu-id="5bc5b-115">Add your account</span></span>
<span data-ttu-id="5bc5b-116">Você deve configurar o Azure PowerShell para trabalhar com os recursos clássicos do Azure.</span><span class="sxs-lookup"><span data-stu-id="5bc5b-116">You must configure Azure PowerShell to work with classic Azure resources.</span></span> <span data-ttu-id="5bc5b-117">Siga as etapas abaixo para configurar o Azure PowerShell para gerenciar os recursos clássicos.</span><span class="sxs-lookup"><span data-stu-id="5bc5b-117">Follow the steps below to configure Azure PowerShell to manage classic resources.</span></span>

1. <span data-ttu-id="5bc5b-118">No prompt do PowerShell, digite `Add-AzureAccount` e clique em **Enter**.</span><span class="sxs-lookup"><span data-stu-id="5bc5b-118">At the PowerShell prompt, type `Add-AzureAccount` and click **Enter**.</span></span> 
2. <span data-ttu-id="5bc5b-119">Digite o endereço de email associado à sua assinatura do Azure e clique em **Continuar**.</span><span class="sxs-lookup"><span data-stu-id="5bc5b-119">Type in the email address associated with your Azure subscription and click **Continue**.</span></span> 
3. <span data-ttu-id="5bc5b-120">Digite a senha da sua conta.</span><span class="sxs-lookup"><span data-stu-id="5bc5b-120">Type in the password for your account.</span></span> 
4. <span data-ttu-id="5bc5b-121">Clique em **Entrar**.</span><span class="sxs-lookup"><span data-stu-id="5bc5b-121">Click **Sign in**.</span></span> 

## <a name="resize-in-the-same-hardware-cluster"></a><span data-ttu-id="5bc5b-122">Redimensionar no mesmo cluster de hardware</span><span class="sxs-lookup"><span data-stu-id="5bc5b-122">Resize in the same hardware cluster</span></span>
<span data-ttu-id="5bc5b-123">Para redimensionar uma VM para um tamanho disponível no cluster de hardware que hospeda a VM, execute as seguintes etapas.</span><span class="sxs-lookup"><span data-stu-id="5bc5b-123">To resize a VM to a size available in the hardware cluster hosting the VM, perform the following steps.</span></span>

1. <span data-ttu-id="5bc5b-124">Execute o seguinte comando do PowerShell para listar os tamanhos de VM disponíveis no cluster de hardware que hospeda o serviço de nuvem que contém a VM.</span><span class="sxs-lookup"><span data-stu-id="5bc5b-124">Run the following PowerShell command to list the VM sizes available in the hardware cluster hosting the cloud service which contains the VM.</span></span>
   
    ```powershell
    Get-AzureService | where {$_.ServiceName -eq "<cloudServiceName>"}
    ```
2. <span data-ttu-id="5bc5b-125">Execute os seguintes comandos para redimensionar a VM.</span><span class="sxs-lookup"><span data-stu-id="5bc5b-125">Run the following commands to resize the VM.</span></span>
   
    ```powershell
    Get-AzureVM -ServiceName <cloudServiceName> -Name <vmName> | Set-AzureVMSize -InstanceSize <newVMSize> | Update-AzureVM
    ```

## <a name="resize-on-a-new-hardware-cluster"></a><span data-ttu-id="5bc5b-126">Redimensionar em um novo cluster de hardware</span><span class="sxs-lookup"><span data-stu-id="5bc5b-126">Resize on a new hardware cluster</span></span>
<span data-ttu-id="5bc5b-127">Para redimensionar uma VM para um tamanho indisponível no cluster de hardware que hospeda a VM, a nuvem de serviço e todas as VMs no serviço de nuvem devem ser recriadas.</span><span class="sxs-lookup"><span data-stu-id="5bc5b-127">To resize a VM to a size not available in the hardware cluster hosting the VM, the cloud service and all VMs in the cloud service must be recreated.</span></span> <span data-ttu-id="5bc5b-128">Cada serviço de nuvem é hospedado em um único cluster de hardware, de modo que todas as VMs no serviço de nuvem devem ter um tamanho com suporte em um cluster de hardware.</span><span class="sxs-lookup"><span data-stu-id="5bc5b-128">Each cloud service is hosted on a single hardware cluster so all VMs in the cloud service must be a size that is supported on a hardware cluster.</span></span> <span data-ttu-id="5bc5b-129">As etapas a seguir descreverão como redimensionar uma VM excluindo e recriando o serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="5bc5b-129">The following steps will describe how to resize a VM by deleting and then recreating the cloud service.</span></span>

1. <span data-ttu-id="5bc5b-130">Execute o seguinte comando do PowerShell para listar os tamanhos de VM disponíveis na região.</span><span class="sxs-lookup"><span data-stu-id="5bc5b-130">Run the following PowerShell command to list the VM sizes available in the region.</span></span> 
   
    ```powershell
    Get-AzureLocation | where {$_.Name -eq "<locationName>"}
    ```
2. <span data-ttu-id="5bc5b-131">Anote todas as configurações para cada VM no serviço de nuvem que contém a VM a ser redimensionada.</span><span class="sxs-lookup"><span data-stu-id="5bc5b-131">Make note of all configuration settings for each VM in the cloud service which contains the VM to be resized.</span></span> 
3. <span data-ttu-id="5bc5b-132">Exclua todas as VMs no serviço de nuvem selecionando a opção para reter os discos para cada VM.</span><span class="sxs-lookup"><span data-stu-id="5bc5b-132">Delete all VMs in the cloud service selecting the option to retain the disks for each VM.</span></span>
4. <span data-ttu-id="5bc5b-133">Recrie a VM a ser redimensionada usando o tamanho de VM desejado.</span><span class="sxs-lookup"><span data-stu-id="5bc5b-133">Recreate the VM to be resized using the desired VM size.</span></span>
5. <span data-ttu-id="5bc5b-134">Recrie todas as outras VMs que estavam no serviço de nuvem usando um tamanho de VM disponível no cluster de hardware que agora hospeda o serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="5bc5b-134">Recreate all other VMs which were in the cloud service using a VM size available in the hardware cluster now hosting the cloud service.</span></span>

<span data-ttu-id="5bc5b-135">Um exemplo de script para excluir e recriar um serviço de nuvem usando um novo tamanho VM pode ser encontrado [aqui](https://github.com/Azure/azure-vm-scripts).</span><span class="sxs-lookup"><span data-stu-id="5bc5b-135">A sample script for deleting and recreating a cloud service using a new VM size can be found [here](https://github.com/Azure/azure-vm-scripts).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="5bc5b-136">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="5bc5b-136">Next steps</span></span>
* <span data-ttu-id="5bc5b-137">[Redimensione uma VM criada no modelo de implantação do Gerenciador de Recursos](../resize-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="5bc5b-137">[Resize a VM created in the Resource Manager deployment model](../resize-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

