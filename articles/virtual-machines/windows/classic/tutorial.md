---
title: "uma máquina virtual no portal do Azure de saudação do aaaCreate | Microsoft Docs"
description: "Crie uma máquina virtual Windows no hello portal do Azure."
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
ms.openlocfilehash: 3848a3d06a7ce377633db78ea385826ed40f94fd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-machine-running-windows-in-hello-azure-portal"></a><span data-ttu-id="81a28-103">Criar uma máquina virtual executando o Windows hello portal do Azure</span><span class="sxs-lookup"><span data-stu-id="81a28-103">Create a virtual machine running Windows in hello Azure portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="81a28-104">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="81a28-104">Azure portal</span></span>](tutorial.md)
> * [<span data-ttu-id="81a28-105">PowerShell: Implantação clássica</span><span class="sxs-lookup"><span data-stu-id="81a28-105">PowerShell: Classic deployment</span></span>](create-powershell.md)
>
>

<br>

> [!IMPORTANT]
> <span data-ttu-id="81a28-106">O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Gerenciador de Recursos e Clássico](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="81a28-106">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="81a28-107">Este artigo aborda usando o modelo de implantação clássico hello.</span><span class="sxs-lookup"><span data-stu-id="81a28-107">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="81a28-108">A Microsoft recomenda que mais novas implantações de usam o modelo do Gerenciador de recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="81a28-108">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="81a28-109">Saiba como muito[executar essas etapas usando o modelo de implantação do Gerenciador de recursos de saudação](../../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) usando Olá **portal do Azure**.</span><span class="sxs-lookup"><span data-stu-id="81a28-109">Learn how too[perform these steps using hello Resource Manager deployment model](../../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) using hello **Azure portal**.</span></span>

<span data-ttu-id="81a28-110">Este tutorial mostra como toocreate um Azure máquina virtual (VM) executando o Windows hello portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="81a28-110">This tutorial shows you how toocreate an Azure virtual machine (VM) running Windows in hello Azure portal.</span></span> <span data-ttu-id="81a28-111">Vamos usar uma imagem do Windows Server como um exemplo, mas isso é apenas uma de saudação muitas imagens ofertas do Azure.</span><span class="sxs-lookup"><span data-stu-id="81a28-111">We'll use a Windows Server image as an example, but that's just one of hello many images Azure offers.</span></span> <span data-ttu-id="81a28-112">Observe que as opções de imagem dependem de sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="81a28-112">Note that your image choices depend on your subscription.</span></span> <span data-ttu-id="81a28-113">Por exemplo, imagens de área de trabalho do Windows podem ser assinantes tooMSDN disponíveis.</span><span class="sxs-lookup"><span data-stu-id="81a28-113">For example, Windows desktop images may be available tooMSDN subscribers.</span></span>

<span data-ttu-id="81a28-114">Esta seção mostra como Olá toouse **painel** em Olá tooselect portal do Azure e, em seguida, criar máquina virtual de saudação.</span><span class="sxs-lookup"><span data-stu-id="81a28-114">This section shows you how toouse hello **Dashboard** in hello Azure portal tooselect and then create hello virtual machine.</span></span>

<span data-ttu-id="81a28-115">Também é possível criar VMs usando [suas próprias imagens](createupload-vhd.md).</span><span class="sxs-lookup"><span data-stu-id="81a28-115">You can also create VMs using [your own images](createupload-vhd.md).</span></span> <span data-ttu-id="81a28-116">toolearn sobre este e outros métodos, consulte [toocreate de diferentes maneiras uma máquina virtual Windows](../../virtual-machines-windows-creation-choices.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="81a28-116">toolearn about this and other methods, see [Different ways toocreate a Windows virtual machine](../../virtual-machines-windows-creation-choices.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<!-- 02/27/2017 Video removed as it was based on hello classic portal. -->

## <span data-ttu-id="81a28-117"><a id="createvirtualmachine"></a>Criar máquina virtual de saudação</span><span class="sxs-lookup"><span data-stu-id="81a28-117"><a id="createvirtualmachine"> </a>Create hello virtual machine</span></span>
[!INCLUDE [virtual-machines-create-WindowsVM](../../../../includes/virtual-machines-create-windowsvm.md)]

## <a name="next-steps"></a><span data-ttu-id="81a28-118">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="81a28-118">Next steps</span></span>
* <span data-ttu-id="81a28-119">Saiba como muito[criar uma VM usando o modelo de implantação do Gerenciador de recursos de saudação](../../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) em Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="81a28-119">Learn how too[create a VM using hello Resource Manager deployment model](../../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) in hello Azure portal.</span></span>
* <span data-ttu-id="81a28-120">Faça logon na máquina virtual de toohello.</span><span class="sxs-lookup"><span data-stu-id="81a28-120">Log on toohello virtual machine.</span></span> <span data-ttu-id="81a28-121">Para obter instruções, consulte [fazer logon na máquina virtual de tooa executando o Windows Server](connect-logon.md).</span><span class="sxs-lookup"><span data-stu-id="81a28-121">For instructions, see [Log on tooa virtual machine running Windows Server](connect-logon.md).</span></span>
* <span data-ttu-id="81a28-122">Anexe um toostore de dados do disco.</span><span class="sxs-lookup"><span data-stu-id="81a28-122">Attach a disk toostore data.</span></span> <span data-ttu-id="81a28-123">Você pode anexar tanto discos vazios como discos que contenham dados.</span><span class="sxs-lookup"><span data-stu-id="81a28-123">You can attach both empty disks and disks that contain data.</span></span> <span data-ttu-id="81a28-124">Para obter instruções, consulte Olá [anexar dados disco tooa máquina virtual do Windows criada com o modelo de implantação clássico Olá](attach-disk.md).</span><span class="sxs-lookup"><span data-stu-id="81a28-124">For instructions, see hello [Attach a data disk tooa Windows virtual machine created with hello classic deployment model](attach-disk.md).</span></span>
