---
title: "aaaResize uma VM do Windows no modelo de implantação clássico Olá - Azure | Microsoft Docs"
description: "Redimensione uma máquina virtual do Windows criada no modelo de implantação clássico hello, usando o Powershell do Azure."
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
ms.openlocfilehash: 39fab14431e2351c9515b0611e850eccfec7a798
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="resize-a-windows-vm-created-in-hello-classic-deployment-model"></a><span data-ttu-id="b889e-103">Redimensionar uma VM do Windows criada no modelo de implantação clássico Olá</span><span class="sxs-lookup"><span data-stu-id="b889e-103">Resize a Windows VM created in hello classic deployment model</span></span>
<span data-ttu-id="b889e-104">Este artigo mostra como tooresize uma VM do Windows criados no modelo de implantação clássico hello usando o Powershell do Azure.</span><span class="sxs-lookup"><span data-stu-id="b889e-104">This article shows you how tooresize a Windows VM, created in hello classic deployment model using Azure Powershell.</span></span>

<span data-ttu-id="b889e-105">Ao considerar Olá capacidade tooresize uma VM, há dois conceitos que controlam o intervalo de saudação da máquina virtual do tamanhos disponíveis tooresize hello.</span><span class="sxs-lookup"><span data-stu-id="b889e-105">When considering hello ability tooresize a VM, there are two concepts which control hello range of sizes available tooresize hello virtual machine.</span></span> <span data-ttu-id="b889e-106">Olá primeiro conceito é região Olá sua VM é implantada.</span><span class="sxs-lookup"><span data-stu-id="b889e-106">hello first concept is hello region in which your VM is deployed.</span></span> <span data-ttu-id="b889e-107">lista de saudação de tamanhos de VM disponíveis na região é na guia de serviços de saudação da página de web hello regiões do Azure.</span><span class="sxs-lookup"><span data-stu-id="b889e-107">hello list of VM sizes available in region is under hello Services tab of hello Azure Regions web page.</span></span> <span data-ttu-id="b889e-108">conceito segundo Olá é hardware físico de saudação hospedando sua VM.</span><span class="sxs-lookup"><span data-stu-id="b889e-108">hello second concept is hello physical hardware currently hosting your VM.</span></span> <span data-ttu-id="b889e-109">servidores físicos do Hello hospedando VMs são agrupados em clusters de hardware físico comum.</span><span class="sxs-lookup"><span data-stu-id="b889e-109">hello physical servers hosting VMs are grouped together in clusters of common physical hardware.</span></span> <span data-ttu-id="b889e-110">método Hello de alterar o tamanho de uma VM é diferente dependendo se hello desejado novo tamanho da VM é suportado por cluster de hardware Olá hospedando Olá VM.</span><span class="sxs-lookup"><span data-stu-id="b889e-110">hello method of changing a VM size differs depending on if hello desired new VM size is supported by hello hardware cluster currently hosting hello VM.</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="b889e-111">O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Gerenciador de Recursos e Clássico](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="b889e-111">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="b889e-112">Este artigo aborda usando o modelo de implantação clássico hello.</span><span class="sxs-lookup"><span data-stu-id="b889e-112">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="b889e-113">A Microsoft recomenda que mais novas implantações de usam o modelo do Gerenciador de recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="b889e-113">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="b889e-114">Você também pode [redimensionar uma VM criada no modelo de implantação do Gerenciador de recursos de saudação](../resize-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="b889e-114">You can also [resize a VM created in hello Resource Manager deployment model](../resize-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

## <a name="add-your-account"></a><span data-ttu-id="b889e-115">Adicionar sua conta</span><span class="sxs-lookup"><span data-stu-id="b889e-115">Add your account</span></span>
<span data-ttu-id="b889e-116">Você deve configurar o Azure PowerShell toowork com clássicos recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="b889e-116">You must configure Azure PowerShell toowork with classic Azure resources.</span></span> <span data-ttu-id="b889e-117">Siga as próximas etapas, Olá recursos clássicos do toomanage tooconfigure PowerShell do Azure.</span><span class="sxs-lookup"><span data-stu-id="b889e-117">Follow hello steps below tooconfigure Azure PowerShell toomanage classic resources.</span></span>

1. <span data-ttu-id="b889e-118">No prompt do PowerShell hello, digite `Add-AzureAccount` e clique em **Enter**.</span><span class="sxs-lookup"><span data-stu-id="b889e-118">At hello PowerShell prompt, type `Add-AzureAccount` and click **Enter**.</span></span> 
2. <span data-ttu-id="b889e-119">Digite hello endereço de email associado à sua assinatura do Azure e clique em **continuar**.</span><span class="sxs-lookup"><span data-stu-id="b889e-119">Type in hello email address associated with your Azure subscription and click **Continue**.</span></span> 
3. <span data-ttu-id="b889e-120">Digite a senha Olá para sua conta.</span><span class="sxs-lookup"><span data-stu-id="b889e-120">Type in hello password for your account.</span></span> 
4. <span data-ttu-id="b889e-121">Clique em **Entrar**.</span><span class="sxs-lookup"><span data-stu-id="b889e-121">Click **Sign in**.</span></span> 

## <a name="resize-in-hello-same-hardware-cluster"></a><span data-ttu-id="b889e-122">Redimensionar em Olá mesmo cluster de hardware</span><span class="sxs-lookup"><span data-stu-id="b889e-122">Resize in hello same hardware cluster</span></span>
<span data-ttu-id="b889e-123">tooresize um tamanho da VM tooa disponível no cluster de hardware Olá hospedagem Olá VM, execute Olá etapas a seguir.</span><span class="sxs-lookup"><span data-stu-id="b889e-123">tooresize a VM tooa size available in hello hardware cluster hosting hello VM, perform hello following steps.</span></span>

1. <span data-ttu-id="b889e-124">Execute Olá Olá tamanhos de VM Olá toolist disponíveis no cluster de hardware Olá hospeda serviço de nuvem Olá que contém a VM de comando do PowerShell a seguir.</span><span class="sxs-lookup"><span data-stu-id="b889e-124">Run hello following PowerShell command toolist hello VM sizes available in hello hardware cluster hosting hello cloud service which contains hello VM.</span></span>
   
    ```powershell
    Get-AzureService | where {$_.ServiceName -eq "<cloudServiceName>"}
    ```
2. <span data-ttu-id="b889e-125">Execute Olá comandos tooresize Olá VM a seguir.</span><span class="sxs-lookup"><span data-stu-id="b889e-125">Run hello following commands tooresize hello VM.</span></span>
   
    ```powershell
    Get-AzureVM -ServiceName <cloudServiceName> -Name <vmName> | Set-AzureVMSize -InstanceSize <newVMSize> | Update-AzureVM
    ```

## <a name="resize-on-a-new-hardware-cluster"></a><span data-ttu-id="b889e-126">Redimensionar em um novo cluster de hardware</span><span class="sxs-lookup"><span data-stu-id="b889e-126">Resize on a new hardware cluster</span></span>
<span data-ttu-id="b889e-127">tooresize um tamanho de tooa VM não está disponível no cluster de hardware Olá hospedando Olá VM, hello serviço de nuvem e todas as VMs no serviço de nuvem Olá devem ser recriadas.</span><span class="sxs-lookup"><span data-stu-id="b889e-127">tooresize a VM tooa size not available in hello hardware cluster hosting hello VM, hello cloud service and all VMs in hello cloud service must be recreated.</span></span> <span data-ttu-id="b889e-128">Cada serviço de nuvem é hospedado em um cluster de hardware única para que todas as VMs no serviço de nuvem Olá devem ser um tamanho que tenha suporte em um cluster de hardware.</span><span class="sxs-lookup"><span data-stu-id="b889e-128">Each cloud service is hosted on a single hardware cluster so all VMs in hello cloud service must be a size that is supported on a hardware cluster.</span></span> <span data-ttu-id="b889e-129">Olá etapas a seguir descrevem como tooresize uma VM excluindo e recriando, em seguida, Olá nuvem serviço.</span><span class="sxs-lookup"><span data-stu-id="b889e-129">hello following steps will describe how tooresize a VM by deleting and then recreating hello cloud service.</span></span>

1. <span data-ttu-id="b889e-130">Execute Olá PowerShell comando toolist Olá tamanhos de VM disponíveis na região Olá a seguir.</span><span class="sxs-lookup"><span data-stu-id="b889e-130">Run hello following PowerShell command toolist hello VM sizes available in hello region.</span></span> 
   
    ```powershell
    Get-AzureLocation | where {$_.Name -eq "<locationName>"}
    ```
2. <span data-ttu-id="b889e-131">Anote todas as configurações para cada VM no serviço de nuvem Olá que contém a saudação VM toobe redimensionado.</span><span class="sxs-lookup"><span data-stu-id="b889e-131">Make note of all configuration settings for each VM in hello cloud service which contains hello VM toobe resized.</span></span> 
3. <span data-ttu-id="b889e-132">Exclua todas as VMs no serviço de nuvem Olá selecionar os discos de Olá Olá opção tooretain para cada VM.</span><span class="sxs-lookup"><span data-stu-id="b889e-132">Delete all VMs in hello cloud service selecting hello option tooretain hello disks for each VM.</span></span>
4. <span data-ttu-id="b889e-133">Recrie Olá VM toobe redimensionado usando tamanho da VM Olá desejado.</span><span class="sxs-lookup"><span data-stu-id="b889e-133">Recreate hello VM toobe resized using hello desired VM size.</span></span>
5. <span data-ttu-id="b889e-134">Recrie todas as outras VMs que estavam no serviço de nuvem hello usando um tamanho VM disponível no cluster de hardware Olá agora hospedando o serviço de nuvem Olá.</span><span class="sxs-lookup"><span data-stu-id="b889e-134">Recreate all other VMs which were in hello cloud service using a VM size available in hello hardware cluster now hosting hello cloud service.</span></span>

<span data-ttu-id="b889e-135">Um exemplo de script para excluir e recriar um serviço de nuvem usando um novo tamanho VM pode ser encontrado [aqui](https://github.com/Azure/azure-vm-scripts).</span><span class="sxs-lookup"><span data-stu-id="b889e-135">A sample script for deleting and recreating a cloud service using a new VM size can be found [here](https://github.com/Azure/azure-vm-scripts).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="b889e-136">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="b889e-136">Next steps</span></span>
* <span data-ttu-id="b889e-137">[Redimensionar uma VM criada no modelo de implantação do Gerenciador de recursos de saudação](../resize-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="b889e-137">[Resize a VM created in hello Resource Manager deployment model](../resize-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

