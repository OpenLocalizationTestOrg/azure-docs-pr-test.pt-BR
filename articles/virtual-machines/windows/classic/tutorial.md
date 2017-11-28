---
title: Criar uma VM no portal do Azure | Microsoft Docs
description: "Crie uma máquina virtual do Windows no Portal do Azure."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 1871f823-ebd7-4eff-9a22-8e2411555595
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/30/2017
ms.author: cynthn
ms.openlocfilehash: 0981872ff819fdf49a9cc97afce3c212013ce76b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-virtual-machine-running-windows-in-the-azure-portal"></a><span data-ttu-id="7437e-103">Criar uma máquina virtual executando o Windows no portal do Azure</span><span class="sxs-lookup"><span data-stu-id="7437e-103">Create a virtual machine running Windows in the Azure portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="7437e-104">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="7437e-104">Azure portal</span></span>](tutorial.md)
> * [<span data-ttu-id="7437e-105">PowerShell: Implantação clássica</span><span class="sxs-lookup"><span data-stu-id="7437e-105">PowerShell: Classic deployment</span></span>](create-powershell.md)
>
>

<br>

> [!IMPORTANT]
> <span data-ttu-id="7437e-106">O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Gerenciador de Recursos e Clássico](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="7437e-106">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="7437e-107">Este artigo aborda o uso do modelo de implantação Clássica.</span><span class="sxs-lookup"><span data-stu-id="7437e-107">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="7437e-108">A Microsoft recomenda que a maioria das implantações novas use o modelo do Gerenciador de Recursos.</span><span class="sxs-lookup"><span data-stu-id="7437e-108">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="7437e-109">Saiba como [executar estas etapas usando o modelo de implantação do Resource Manager](../../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) no **portal do Azure**.</span><span class="sxs-lookup"><span data-stu-id="7437e-109">Learn how to [perform these steps using the Resource Manager deployment model](../../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) using the **Azure portal**.</span></span>

<span data-ttu-id="7437e-110">Este tutorial mostra como criar uma VM (máquina virtual) do Azure executando Windows no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="7437e-110">This tutorial shows you how to create an Azure virtual machine (VM) running Windows in the Azure portal.</span></span> <span data-ttu-id="7437e-111">Vamos usar uma imagem do Windows Server como exemplo, mas ela é apenas uma das muitas imagens que o Azure oferece.</span><span class="sxs-lookup"><span data-stu-id="7437e-111">We'll use a Windows Server image as an example, but that's just one of the many images Azure offers.</span></span> <span data-ttu-id="7437e-112">Observe que as opções de imagem dependem de sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="7437e-112">Note that your image choices depend on your subscription.</span></span> <span data-ttu-id="7437e-113">Por exemplo, imagens da área de trabalho do Windows podem estar disponíveis para assinantes do MSDN.</span><span class="sxs-lookup"><span data-stu-id="7437e-113">For example, Windows desktop images may be available to MSDN subscribers.</span></span>

<span data-ttu-id="7437e-114">Esta seção mostra como usar o **Painel** no portal do Azure para selecionar e criar a máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="7437e-114">This section shows you how to use the **Dashboard** in the Azure portal to select and then create the virtual machine.</span></span>

<span data-ttu-id="7437e-115">Também é possível criar VMs usando [suas próprias imagens](createupload-vhd.md).</span><span class="sxs-lookup"><span data-stu-id="7437e-115">You can also create VMs using [your own images](createupload-vhd.md).</span></span> <span data-ttu-id="7437e-116">Para saber mais sobre esse e outros métodos, consulte [Diferentes maneiras de criar uma máquina virtual do Windows](../../virtual-machines-windows-creation-choices.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="7437e-116">To learn about this and other methods, see [Different ways to create a Windows virtual machine](../../virtual-machines-windows-creation-choices.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<!-- 02/27/2017 Video removed as it was based on the classic portal. -->

## <span data-ttu-id="7437e-117"><a id="createvirtualmachine"> </a>Criar a máquina virtual</span><span class="sxs-lookup"><span data-stu-id="7437e-117"><a id="createvirtualmachine"> </a>Create the virtual machine</span></span>
[!INCLUDE [virtual-machines-create-WindowsVM](../../../../includes/virtual-machines-create-windowsvm.md)]

## <a name="next-steps"></a><span data-ttu-id="7437e-118">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="7437e-118">Next steps</span></span>
* <span data-ttu-id="7437e-119">Saiba como [criar uma VM usando o modelo de implantação do Resource Manager](../../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="7437e-119">Learn how to [create a VM using the Resource Manager deployment model](../../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) in the Azure portal.</span></span>
* <span data-ttu-id="7437e-120">Faça logon na máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="7437e-120">Log on to the virtual machine.</span></span> <span data-ttu-id="7437e-121">Para obter instruções, veja [Fazer logon em uma máquina virtual que executa o Windows Server](connect-logon.md).</span><span class="sxs-lookup"><span data-stu-id="7437e-121">For instructions, see [Log on to a virtual machine running Windows Server](connect-logon.md).</span></span>
* <span data-ttu-id="7437e-122">Anexe um disco para armazenar dados.</span><span class="sxs-lookup"><span data-stu-id="7437e-122">Attach a disk to store data.</span></span> <span data-ttu-id="7437e-123">Você pode anexar tanto discos vazios como discos que contenham dados.</span><span class="sxs-lookup"><span data-stu-id="7437e-123">You can attach both empty disks and disks that contain data.</span></span> <span data-ttu-id="7437e-124">Para obter instruções, veja [Anexar um disco de dados a uma máquina virtual do Windows criada com o modelo de implantação clássico](attach-disk.md).</span><span class="sxs-lookup"><span data-stu-id="7437e-124">For instructions, see the [Attach a data disk to a Windows virtual machine created with the classic deployment model](attach-disk.md).</span></span>
