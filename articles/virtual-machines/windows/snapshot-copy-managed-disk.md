---
title: "aaaCreate uma cópia de um disco gerenciado do Azure para backup | Microsoft Docs"
description: "Saiba como toocreate uma cópia de um toouse de disco gerenciado do Azure para fazer backup ou solução de problemas de disco emite."
documentationcenter: 
author: cwatson-cat
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 15eb778e-fc07-45ef-bdc8-9090193a6d20
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 2/9/2017
ms.author: cwatson
ms.openlocfilehash: 2f33dbbee624bcd813f3c7c3e3401072d0933714
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-copy-of-a-vhd-stored-as-an-azure-managed-disk-by-using-managed-snapshots"></a><span data-ttu-id="4179f-103">Criar uma cópia de um VHD armazenado como um Disco Gerenciado do Azure usando instantâneos gerenciados</span><span class="sxs-lookup"><span data-stu-id="4179f-103">Create a copy of a VHD stored as an Azure Managed Disk by using Managed Snapshots</span></span>
<span data-ttu-id="4179f-104">Tirar um instantâneo de um disco gerenciados para backup ou criar um disco gerenciado de instantâneo hello e anexá-lo tooa tootroubleshoot de máquina virtual de teste.</span><span class="sxs-lookup"><span data-stu-id="4179f-104">Take a snapshot of a Managed Disk for backup or create a Managed Disk from hello snapshot and attach it tooa test virtual machine tootroubleshoot.</span></span> <span data-ttu-id="4179f-105">Um Instantâneo Gerenciado é uma cópia pontual completa de um Disco Gerenciado da VM.</span><span class="sxs-lookup"><span data-stu-id="4179f-105">A Managed Snapshot is a full point-in-time copy of a VM Managed Disk.</span></span> <span data-ttu-id="4179f-106">Ele cria uma cópia somente leitura do seu VHD e, por padrão, a armazena como um Disco Gerenciado Standard.</span><span class="sxs-lookup"><span data-stu-id="4179f-106">It creates a read-only copy of your VHD and, by default, stores it as a Standard Managed Disk.</span></span> <span data-ttu-id="4179f-107">Para saber mais sobre Managed Disks, confira [Visão geral dos Managed Disks](managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="4179f-107">For more information about Managed Disks, see [Azure Managed Disks overview](managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span></span>

<span data-ttu-id="4179f-108">Para saber mais sobre preços, confira [Preços de Armazenamento do Azure](https://azure.microsoft.com/pricing/details/managed-disks/).</span><span class="sxs-lookup"><span data-stu-id="4179f-108">For information about pricing, see [Azure Storage Pricing](https://azure.microsoft.com/pricing/details/managed-disks/).</span></span> 

## <a name="before-you-begin"></a><span data-ttu-id="4179f-109">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="4179f-109">Before you begin</span></span>
<span data-ttu-id="4179f-110">Se você usar o PowerShell, certifique-se de que você tem a versão mais recente Olá de saudação módulo AzureRM.Compute PowerShell.</span><span class="sxs-lookup"><span data-stu-id="4179f-110">If you use PowerShell, make sure that you have hello latest version of hello AzureRM.Compute PowerShell module.</span></span> <span data-ttu-id="4179f-111">Executar Olá tooinstall de comando a seguir.</span><span class="sxs-lookup"><span data-stu-id="4179f-111">Run hello following command tooinstall it.</span></span>

```
Install-Module AzureRM.Compute -RequiredVersion 2.6.0
```
<span data-ttu-id="4179f-112">Para saber mais, confira [Azure PowerShell Versioning](/powershell/azure/overview) (Controle de versão do Azure PowerShell).</span><span class="sxs-lookup"><span data-stu-id="4179f-112">For more information, see [Azure PowerShell Versioning](/powershell/azure/overview).</span></span>

## <a name="copy-hello-vhd-with-a-snapshot"></a><span data-ttu-id="4179f-113">Copiar Olá VHD com um instantâneo</span><span class="sxs-lookup"><span data-stu-id="4179f-113">Copy hello VHD with a snapshot</span></span>
<span data-ttu-id="4179f-114">Use Olá portal do Azure ou do PowerShell tootake um instantâneo de saudação disco gerenciado.</span><span class="sxs-lookup"><span data-stu-id="4179f-114">Use either hello Azure portal or PowerShell tootake a snapshot of hello Managed Disk.</span></span>

### <a name="use-azure-portal-tootake-a-snapshot"></a><span data-ttu-id="4179f-115">Use tootake portal do Azure um instantâneo</span><span class="sxs-lookup"><span data-stu-id="4179f-115">Use Azure portal tootake a snapshot</span></span> 

1. <span data-ttu-id="4179f-116">Entrar toohello [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="4179f-116">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="4179f-117">Iniciando na parte superior esquerda do hello, clique em **novo** e procure **instantâneo**.</span><span class="sxs-lookup"><span data-stu-id="4179f-117">Starting in hello upper left, click **New** and search for **snapshot**.</span></span>
3. <span data-ttu-id="4179f-118">Na folha de instantâneo hello, clique em **criar**.</span><span class="sxs-lookup"><span data-stu-id="4179f-118">In hello Snapshot blade, click **Create**.</span></span>
4. <span data-ttu-id="4179f-119">Insira um **nome** para instantâneo de saudação.</span><span class="sxs-lookup"><span data-stu-id="4179f-119">Enter a **Name** for hello snapshot.</span></span>
5. <span data-ttu-id="4179f-120">Selecione uma existente [grupo de recursos](../../azure-resource-manager/resource-group-overview.md#resource-groups) ou nome de saudação do tipo para um novo.</span><span class="sxs-lookup"><span data-stu-id="4179f-120">Select an existing [Resource group](../../azure-resource-manager/resource-group-overview.md#resource-groups) or type hello name for a new one.</span></span> 
6. <span data-ttu-id="4179f-121">Selecione um Local do datacenter do Azure.</span><span class="sxs-lookup"><span data-stu-id="4179f-121">Select an Azure datacenter Location.</span></span>  
7. <span data-ttu-id="4179f-122">Para **disco de origem**, selecione Olá toosnapshot de disco gerenciado.</span><span class="sxs-lookup"><span data-stu-id="4179f-122">For **Source disk**, select hello Managed Disk toosnapshot.</span></span>
8. <span data-ttu-id="4179f-123">Selecione Olá **tipo de conta** instantâneo de saudação do toouse toostore.</span><span class="sxs-lookup"><span data-stu-id="4179f-123">Select hello **Account type** toouse toostore hello snapshot.</span></span> <span data-ttu-id="4179f-124">É recomendável **Standard_LRS**, a menos que você precise dele armazenado em um disco de alto desempenho.</span><span class="sxs-lookup"><span data-stu-id="4179f-124">We recommend **Standard_LRS** unless you need it stored on a high performing disk.</span></span>
9. <span data-ttu-id="4179f-125">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="4179f-125">Click **Create**.</span></span>

### <a name="use-powershell-tootake-a-snapshot"></a><span data-ttu-id="4179f-126">Use o PowerShell tootake um instantâneo</span><span class="sxs-lookup"><span data-stu-id="4179f-126">Use PowerShell tootake a snapshot</span></span>
<span data-ttu-id="4179f-127">Hello etapas a seguir mostram como tooget Olá VHD disco toobe copiado, criar hello configurações de instantâneos e tirar um instantâneo do disco hello usando o cmdlet Olá novo AzureRmSnapshot<!--Add link toocmdlet when available-->.</span><span class="sxs-lookup"><span data-stu-id="4179f-127">hello following steps show you how tooget hello VHD disk toobe copied, create hello snapshot configurations, and take a snapshot of hello disk by using hello New-AzureRmSnapshot cmdlet<!--Add link toocmdlet when available-->.</span></span> 

1. <span data-ttu-id="4179f-128">Defina alguns parâmetros.</span><span class="sxs-lookup"><span data-stu-id="4179f-128">Set some parameters.</span></span> 

 ```powershell
$resourceGroupName = 'myResourceGroup' 
$location = 'southeastasia' 
$dataDiskName = 'ContosoMD_datadisk1' 
$snapshotName = 'ContosoMD_datadisk1_snapshot1'  
```
  <span data-ttu-id="4179f-129">Substitua os valores de parâmetro hello:</span><span class="sxs-lookup"><span data-stu-id="4179f-129">Replace hello parameter values:</span></span>
  -  <span data-ttu-id="4179f-130">"myResourceGroup" com o grupo de recursos da VM hello.</span><span class="sxs-lookup"><span data-stu-id="4179f-130">"myResourceGroup" with hello VM's resource group.</span></span>
  -  <span data-ttu-id="4179f-131">"southeastasia" com a localização geográfica hello, onde você deseja que o instantâneo gerenciado armazenado.</span><span class="sxs-lookup"><span data-stu-id="4179f-131">"southeastasia" with hello geographic location where you want your Managed Snapshot stored.</span></span> <!---How do you look these up? -->
  -  <span data-ttu-id="4179f-132">"ContosoMD_datadisk1" com o nome de saudação do disco VHD Olá que você deseja toocopy.</span><span class="sxs-lookup"><span data-stu-id="4179f-132">"ContosoMD_datadisk1" with hello name of hello VHD disk that you want toocopy.</span></span>
  -  <span data-ttu-id="4179f-133">"ContosoMD_datadisk1_snapshot1" hello nome você deseja toouse para novo instantâneo de saudação.</span><span class="sxs-lookup"><span data-stu-id="4179f-133">"ContosoMD_datadisk1_snapshot1" with hello name you want toouse for hello new snapshot.</span></span>

2. <span data-ttu-id="4179f-134">Obter toobe de disco VHD Olá copiado.</span><span class="sxs-lookup"><span data-stu-id="4179f-134">Get hello VHD disk toobe copied.</span></span>

 ```powershell
$disk = Get-AzureRmDisk -ResourceGroupName $resourceGroupName -DiskName $dataDiskName 
```
3. <span data-ttu-id="4179f-135">Crie hello configurações de instantâneos.</span><span class="sxs-lookup"><span data-stu-id="4179f-135">Create hello snapshot configurations.</span></span> 

 ```powershell
$snapshot =  New-AzureRmSnapshotConfig -SourceUri $disk.Id -CreateOption Copy -Location $location 
```
4. <span data-ttu-id="4179f-136">Tire instantâneo hello.</span><span class="sxs-lookup"><span data-stu-id="4179f-136">Take hello snapshot.</span></span>

 ```powershell
New-AzureRmSnapshot -Snapshot $snapshot -SnapshotName $snapshotName -ResourceGroupName $resourceGroupName 
```
<span data-ttu-id="4179f-137">Se você planejar toouse Olá instantâneo toocreate um disco gerenciado e anexá-lo uma VM que precisa toobe alto desempenho, use o parâmetro hello `-AccountType Premium_LRS` com o comando Olá AzureRmSnapshot de novo.</span><span class="sxs-lookup"><span data-stu-id="4179f-137">If you plan toouse hello snapshot toocreate a Managed Disk and attach it a VM that needs toobe high performing, use hello parameter `-AccountType Premium_LRS` with hello New-AzureRmSnapshot command.</span></span> <span data-ttu-id="4179f-138">parâmetro Hello cria o instantâneo de saudação para que ela é armazenada como um disco de gerenciado para Premium.</span><span class="sxs-lookup"><span data-stu-id="4179f-138">hello parameter creates hello snapshot so that it's stored as a Premium Managed Disk.</span></span> <span data-ttu-id="4179f-139">Os Discos Gerenciados Premium são mais caros que os Standard.</span><span class="sxs-lookup"><span data-stu-id="4179f-139">Premium Managed Disks are more expensive than Standard.</span></span> <span data-ttu-id="4179f-140">Portanto, assegure-se de que os discos Premium sejam realmente necessários antes de usar esse parâmetro.</span><span class="sxs-lookup"><span data-stu-id="4179f-140">So be sure you really need Premium before using that parameter.</span></span>


