---
title: aaaCreate um disco gerenciado em um VHD no Azure | Microsoft Docs
description: "Crie um disco gerenciado de um VHD que está atualmente em uma conta de armazenamento do Azure, usando o modelo de implantação do Gerenciador de recursos de saudação."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 02/05/2017
ms.author: cynthn
ms.openlocfilehash: 77adaac5419186ff85039fe2c4752f021aa5e448
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-managed-disks-from-unmanaged-disks-in-a-storage-account"></a><span data-ttu-id="33183-103">Criar discos gerenciados a partir de discos não gerenciados em uma conta de armazenamento</span><span class="sxs-lookup"><span data-stu-id="33183-103">Create managed disks from unmanaged disks in a storage account</span></span>

<span data-ttu-id="33183-104">É possível criar um disco gerenciado a partir de um disco de dados existente ou de um disco de sistema operacional que está localizado atualmente em uma conta de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="33183-104">A managed disk can be created from an existing data disk or an OS disk that is currently in an Azure storage account.</span></span> <span data-ttu-id="33183-105">Também é possível criar um disco vazio que pode ser usado como um novo disco de dados para uma VM.</span><span class="sxs-lookup"><span data-stu-id="33183-105">You can also create an empty disk that can be used as a new data disk for a VM.</span></span> 

## <a name="before-you-begin"></a><span data-ttu-id="33183-106">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="33183-106">Before you begin</span></span>
<span data-ttu-id="33183-107">Se você usar o PowerShell, certifique-se de que você tem a versão mais recente Olá de saudação módulo AzureRM.Compute PowerShell.</span><span class="sxs-lookup"><span data-stu-id="33183-107">If you use PowerShell, make sure that you have hello latest version of hello AzureRM.Compute PowerShell module.</span></span> <span data-ttu-id="33183-108">Executar Olá tooinstall de comando a seguir.</span><span class="sxs-lookup"><span data-stu-id="33183-108">Run hello following command tooinstall it.</span></span>

```powershell
Install-Module AzureRM.Compute -RequiredVersion 2.6.0
```
<span data-ttu-id="33183-109">Para saber mais, confira [Azure PowerShell Versioning](/powershell/azure/overview) (Controle de versão do Azure PowerShell).</span><span class="sxs-lookup"><span data-stu-id="33183-109">For more information, see [Azure PowerShell Versioning](/powershell/azure/overview).</span></span>


## <a name="create-a-managed-disk-from-a-vhd-in-an-azure-storage-account"></a><span data-ttu-id="33183-110">Criar um disco gerenciado de um VHD em uma conta de armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="33183-110">Create a managed disk from a VHD in an Azure storage account</span></span>

<span data-ttu-id="33183-111">No exemplo hello, podemos criar um disco de um VHD como disco gerenciado e atribua-o parâmetro toohello **$Disco1** toouse mais tarde.</span><span class="sxs-lookup"><span data-stu-id="33183-111">In hello example we create a disk from a VHD as managed disk and assign it toohello parameter **$disk1** toouse later.</span></span> 

<span data-ttu-id="33183-112">Olá disco gerenciado será criado no hello **Oeste dos EUA** local, em um grupo de recursos denominado **myResourceGroup**.</span><span class="sxs-lookup"><span data-stu-id="33183-112">hello managed disk will be created in hello **West-US** location, in a resource group named **myResourceGroup**.</span></span> <span data-ttu-id="33183-113">disco Olá será nomeado **myDisk** e ele será criado de um arquivo do VHD chamado **myDisk.vhd** é carregado anteriormente chamada de conta de armazenamento tooa **mystorageaccount**.</span><span class="sxs-lookup"><span data-stu-id="33183-113">hello disk will be named **myDisk** and it will be created from a VHD file named **myDisk.vhd** we previously uploaded tooa storage account named **mystorageaccount**.</span></span> <span data-ttu-id="33183-114">disco gerenciado Olá será criado no armazenamento de premium localmente redundante (LRS).</span><span class="sxs-lookup"><span data-stu-id="33183-114">hello managed disk will be created in premium locally-redundant storage (LRS).</span></span> <span data-ttu-id="33183-115">StandardLRS e PremiumLRS são apenas Olá **- AccountType** opções disponíveis para discos de gerenciado.</span><span class="sxs-lookup"><span data-stu-id="33183-115">StandardLRS and PremiumLRS are hello only **-AccountType** options available for managed disks.</span></span> 

1.  <span data-ttu-id="33183-116">Defina alguns parâmetros</span><span class="sxs-lookup"><span data-stu-id="33183-116">Set some parameters</span></span>

    ```powershell
    $rgName = "myResourceGroup"
    $location = "West Central US"
    $diskName = "myDisk"
    $vhdUri = "https://mystorageaccount.blob.core.windows.net/vhds/myDisk.vhd"
    ```

2. <span data-ttu-id="33183-117">Crie disco de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="33183-117">Create hello data disk.</span></span> 
    ```powershell
    $disk1 = New-AzureRmDisk -DiskName $diskName -Disk (New-AzureRmDiskConfig -AccountType PremiumLRS -Location $location -CreateOption Import -SourceUri $vhdUri) -ResourceGroupName $rgName
    ```
    
    

## <a name="create-an-empty-data-disk-as-a-managed-disk"></a><span data-ttu-id="33183-118">Criar um disco de dados vazio como um disco gerenciado</span><span class="sxs-lookup"><span data-stu-id="33183-118">Create an empty data disk as a managed disk</span></span>

<span data-ttu-id="33183-119">No exemplo hello, podemos criar um disco de dados vazio como disco gerenciado e atribua-o parâmetro toohello **$dataDisk2** toouse mais tarde.</span><span class="sxs-lookup"><span data-stu-id="33183-119">In hello example we create an empty data disk as managed disk and assign it toohello parameter **$dataDisk2** toouse later.</span></span> <span data-ttu-id="33183-120">Um disco de dados vazio será necessário toobe inicializado logon toohello VM e usar o diskmgmt.msc ou [remotamente usando um script e WinRM](attach-disk-ps.md#initialize-the-disk), uma vez que é anexado tooa executando VM.</span><span class="sxs-lookup"><span data-stu-id="33183-120">An empty data disk will need toobe initialized logging in toohello VM and using diskmgmt.msc or [remotely using WinRM and a script](attach-disk-ps.md#initialize-the-disk), once it is attached tooa running VM.</span></span>

<span data-ttu-id="33183-121">disco de dados vazio do Hello será criado na Olá **Central Oeste dos EUA** local, em um grupo de recursos denominado **myResourceGroup**.</span><span class="sxs-lookup"><span data-stu-id="33183-121">hello empty data disk will be created in hello **West Central US** location, in a resource group named **myResourceGroup**.</span></span> <span data-ttu-id="33183-122">disco Olá será nomeado **myEmptyDataDisk**.</span><span class="sxs-lookup"><span data-stu-id="33183-122">hello disk will be named **myEmptyDataDisk**.</span></span> <span data-ttu-id="33183-123">disco vazio Olá será criado no armazenamento de premium localmente redundante (LRS).</span><span class="sxs-lookup"><span data-stu-id="33183-123">hello empty disk will be created in premium locally-redundant storage (LRS).</span></span> <span data-ttu-id="33183-124">StandardLRS e PremiumLRS são apenas Olá **- AccountType** opções disponíveis para discos de gerenciado.</span><span class="sxs-lookup"><span data-stu-id="33183-124">StandardLRS and PremiumLRS are hello only **-AccountType** options available for managed disks.</span></span>

<span data-ttu-id="33183-125">tamanho do disco Olá neste exemplo é de 128GB, mas você deve escolher um tamanho que atenda às necessidades de saudação de aplicativos em execução na sua VM.</span><span class="sxs-lookup"><span data-stu-id="33183-125">hello disk size in this example is 128GB, but you should choose a size that meets hello needs of any applications running on your VM.</span></span>

1.  <span data-ttu-id="33183-126">Defina alguns parâmetros</span><span class="sxs-lookup"><span data-stu-id="33183-126">Set some parameters</span></span>

    ```powershell
    $rgName = "myResourceGroup"
    $location = "West Central US"
    $dataDiskName = "myEmptyDataDisk"
    ```

2. <span data-ttu-id="33183-127">Crie disco de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="33183-127">Create hello data disk.</span></span>
    ```powershell
    $dataDisk2 = New-AzureRmDisk -DiskName $dataDiskName -Disk (New-AzureRmDiskConfig -AccountType PremiumLRS -Location $location -CreateOption Empty -DiskSizeGB 128) -ResourceGroupName $rgName
    ```
    
## <a name="next-steps"></a><span data-ttu-id="33183-128">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="33183-128">Next Steps</span></span>   
- <span data-ttu-id="33183-129">Se você já tiver uma máquina virtual, poderá [anexar um disco de dados](attach-disk-portal.md).</span><span class="sxs-lookup"><span data-stu-id="33183-129">If you already have a VM, you can [attach a data disk](attach-disk-portal.md).</span></span>
