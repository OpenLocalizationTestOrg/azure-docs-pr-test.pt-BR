---
title: "Criar uma cópia de um Disco Gerenciado para backup | Microsoft Docs"
description: "Saiba como criar uma cópia de um Disco Gerenciado do Azure para usar no backup ou na solução de problemas de disco."
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
ms.openlocfilehash: a7527b12f4f0d2b45713a0c0109d81ff51293fd8
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-copy-of-a-vhd-stored-as-an-azure-managed-disk-by-using-managed-snapshots"></a><span data-ttu-id="d738a-103">Criar uma cópia de um VHD armazenado como um Disco Gerenciado do Azure usando instantâneos gerenciados</span><span class="sxs-lookup"><span data-stu-id="d738a-103">Create a copy of a VHD stored as an Azure Managed Disk by using Managed Snapshots</span></span>
<span data-ttu-id="d738a-104">Crie um instantâneo de um Disco Gerenciado para backup ou crie um Disco Gerenciado usando o instantâneo e anexe-o a uma máquina virtual de teste para solução de problemas.</span><span class="sxs-lookup"><span data-stu-id="d738a-104">Take a snapshot of a Managed Disk for backup or create a Managed Disk from the snapshot and attach it to a test virtual machine to troubleshoot.</span></span> <span data-ttu-id="d738a-105">Um Instantâneo Gerenciado é uma cópia pontual completa de um Disco Gerenciado da VM.</span><span class="sxs-lookup"><span data-stu-id="d738a-105">A Managed Snapshot is a full point-in-time copy of a VM Managed Disk.</span></span> <span data-ttu-id="d738a-106">Ele cria uma cópia somente leitura do seu VHD e, por padrão, a armazena como um Disco Gerenciado Standard.</span><span class="sxs-lookup"><span data-stu-id="d738a-106">It creates a read-only copy of your VHD and, by default, stores it as a Standard Managed Disk.</span></span> <span data-ttu-id="d738a-107">Para saber mais sobre Managed Disks, confira [Visão geral dos Managed Disks](managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="d738a-107">For more information about Managed Disks, see [Azure Managed Disks overview](managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span></span>

<span data-ttu-id="d738a-108">Para saber mais sobre preços, confira [Preços de Armazenamento do Azure](https://azure.microsoft.com/pricing/details/managed-disks/).</span><span class="sxs-lookup"><span data-stu-id="d738a-108">For information about pricing, see [Azure Storage Pricing](https://azure.microsoft.com/pricing/details/managed-disks/).</span></span> 

## <a name="before-you-begin"></a><span data-ttu-id="d738a-109">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="d738a-109">Before you begin</span></span>
<span data-ttu-id="d738a-110">Caso use o PowerShell, verifique se você tem a versão mais recente do módulo AzureRM.Compute do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d738a-110">If you use PowerShell, make sure that you have the latest version of the AzureRM.Compute PowerShell module.</span></span> <span data-ttu-id="d738a-111">Execute o comando a seguir para instalá-lo.</span><span class="sxs-lookup"><span data-stu-id="d738a-111">Run the following command to install it.</span></span>

```
Install-Module AzureRM.Compute -RequiredVersion 2.6.0
```
<span data-ttu-id="d738a-112">Para saber mais, confira [Azure PowerShell Versioning](/powershell/azure/overview) (Controle de versão do Azure PowerShell).</span><span class="sxs-lookup"><span data-stu-id="d738a-112">For more information, see [Azure PowerShell Versioning](/powershell/azure/overview).</span></span>

## <a name="copy-the-vhd-with-a-snapshot"></a><span data-ttu-id="d738a-113">Copiar o VHD com um instantâneo</span><span class="sxs-lookup"><span data-stu-id="d738a-113">Copy the VHD with a snapshot</span></span>
<span data-ttu-id="d738a-114">Use o Portal do Azure ou o PowerShell para criar um instantâneo do Disco Gerenciado.</span><span class="sxs-lookup"><span data-stu-id="d738a-114">Use either the Azure portal or PowerShell to take a snapshot of the Managed Disk.</span></span>

### <a name="use-azure-portal-to-take-a-snapshot"></a><span data-ttu-id="d738a-115">Usar o Portal do Azure para criar um instantâneo</span><span class="sxs-lookup"><span data-stu-id="d738a-115">Use Azure portal to take a snapshot</span></span> 

1. <span data-ttu-id="d738a-116">Entre no [Portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="d738a-116">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="d738a-117">Iniciando no canto superior esquerdo, clique em **Novo** e procure **instantâneo**.</span><span class="sxs-lookup"><span data-stu-id="d738a-117">Starting in the upper left, click **New** and search for **snapshot**.</span></span>
3. <span data-ttu-id="d738a-118">Na folha Instantâneo, clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="d738a-118">In the Snapshot blade, click **Create**.</span></span>
4. <span data-ttu-id="d738a-119">Insira um **Nome** para o instantâneo.</span><span class="sxs-lookup"><span data-stu-id="d738a-119">Enter a **Name** for the snapshot.</span></span>
5. <span data-ttu-id="d738a-120">Selecione um [Grupo de recursos](../../azure-resource-manager/resource-group-overview.md#resource-groups) existente ou digite o nome de um novo.</span><span class="sxs-lookup"><span data-stu-id="d738a-120">Select an existing [Resource group](../../azure-resource-manager/resource-group-overview.md#resource-groups) or type the name for a new one.</span></span> 
6. <span data-ttu-id="d738a-121">Selecione um Local do datacenter do Azure.</span><span class="sxs-lookup"><span data-stu-id="d738a-121">Select an Azure datacenter Location.</span></span>  
7. <span data-ttu-id="d738a-122">Para **Disco de origem**, selecione o Disco Gerenciado para instantâneo.</span><span class="sxs-lookup"><span data-stu-id="d738a-122">For **Source disk**, select the Managed Disk to snapshot.</span></span>
8. <span data-ttu-id="d738a-123">Escolha o **Tipo de conta** a ser usado para armazenar o instantâneo.</span><span class="sxs-lookup"><span data-stu-id="d738a-123">Select the **Account type** to use to store the snapshot.</span></span> <span data-ttu-id="d738a-124">É recomendável **Standard_LRS**, a menos que você precise dele armazenado em um disco de alto desempenho.</span><span class="sxs-lookup"><span data-stu-id="d738a-124">We recommend **Standard_LRS** unless you need it stored on a high performing disk.</span></span>
9. <span data-ttu-id="d738a-125">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="d738a-125">Click **Create**.</span></span>

### <a name="use-powershell-to-take-a-snapshot"></a><span data-ttu-id="d738a-126">Usar o PowerShell para criar um instantâneo</span><span class="sxs-lookup"><span data-stu-id="d738a-126">Use PowerShell to take a snapshot</span></span>
<span data-ttu-id="d738a-127">As etapas a seguir mostram como obter o disco VHD a ser copiado, criar as configurações de instantâneo e criar um instantâneo do disco usando o cmdlet New-AzureRmSnapshot<!--Add link to cmdlet when available-->.</span><span class="sxs-lookup"><span data-stu-id="d738a-127">The following steps show you how to get the VHD disk to be copied, create the snapshot configurations, and take a snapshot of the disk by using the New-AzureRmSnapshot cmdlet<!--Add link to cmdlet when available-->.</span></span> 

1. <span data-ttu-id="d738a-128">Defina alguns parâmetros.</span><span class="sxs-lookup"><span data-stu-id="d738a-128">Set some parameters.</span></span> 

 ```powershell
$resourceGroupName = 'myResourceGroup' 
$location = 'southeastasia' 
$dataDiskName = 'ContosoMD_datadisk1' 
$snapshotName = 'ContosoMD_datadisk1_snapshot1'  
```
  <span data-ttu-id="d738a-129">Substitua os valores de parâmetro:</span><span class="sxs-lookup"><span data-stu-id="d738a-129">Replace the parameter values:</span></span>
  -  <span data-ttu-id="d738a-130">"myResourceGroup" pelo grupo de recursos da VM.</span><span class="sxs-lookup"><span data-stu-id="d738a-130">"myResourceGroup" with the VM's resource group.</span></span>
  -  <span data-ttu-id="d738a-131">"southeastasia" pela localização geográfica onde você quer armazenar o Instantâneo Gerenciado.</span><span class="sxs-lookup"><span data-stu-id="d738a-131">"southeastasia" with the geographic location where you want your Managed Snapshot stored.</span></span> <!---How do you look these up? -->
  -  <span data-ttu-id="d738a-132">"ContosoMD_datadisk1" pelo nome do disco VHD que você quer copiar.</span><span class="sxs-lookup"><span data-stu-id="d738a-132">"ContosoMD_datadisk1" with the name of the VHD disk that you want to copy.</span></span>
  -  <span data-ttu-id="d738a-133">"ContosoMD_datadisk1_snapshot1" pelo nome que você quer usar para o novo instantâneo.</span><span class="sxs-lookup"><span data-stu-id="d738a-133">"ContosoMD_datadisk1_snapshot1" with the name you want to use for the new snapshot.</span></span>

2. <span data-ttu-id="d738a-134">Obtenha o disco VHD a ser copiado.</span><span class="sxs-lookup"><span data-stu-id="d738a-134">Get the VHD disk to be copied.</span></span>

 ```powershell
$disk = Get-AzureRmDisk -ResourceGroupName $resourceGroupName -DiskName $dataDiskName 
```
3. <span data-ttu-id="d738a-135">Crie as configurações do instantâneo.</span><span class="sxs-lookup"><span data-stu-id="d738a-135">Create the snapshot configurations.</span></span> 

 ```powershell
$snapshot =  New-AzureRmSnapshotConfig -SourceUri $disk.Id -CreateOption Copy -Location $location 
```
4. <span data-ttu-id="d738a-136">Crie o instantâneo.</span><span class="sxs-lookup"><span data-stu-id="d738a-136">Take the snapshot.</span></span>

 ```powershell
New-AzureRmSnapshot -Snapshot $snapshot -SnapshotName $snapshotName -ResourceGroupName $resourceGroupName 
```
<span data-ttu-id="d738a-137">Se você planeja usar o instantâneo para criar um Disco Gerenciado e anexá-lo a uma VM que precisa ser de alto desempenho, use o parâmetro `-AccountType Premium_LRS` com o comando New-AzureRmSnapshot.</span><span class="sxs-lookup"><span data-stu-id="d738a-137">If you plan to use the snapshot to create a Managed Disk and attach it a VM that needs to be high performing, use the parameter `-AccountType Premium_LRS` with the New-AzureRmSnapshot command.</span></span> <span data-ttu-id="d738a-138">O parâmetro cria o instantâneo para que ele seja armazenado como um Disco Gerenciado Premium.</span><span class="sxs-lookup"><span data-stu-id="d738a-138">The parameter creates the snapshot so that it's stored as a Premium Managed Disk.</span></span> <span data-ttu-id="d738a-139">Os Discos Gerenciados Premium são mais caros que os Standard.</span><span class="sxs-lookup"><span data-stu-id="d738a-139">Premium Managed Disks are more expensive than Standard.</span></span> <span data-ttu-id="d738a-140">Portanto, assegure-se de que os discos Premium sejam realmente necessários antes de usar esse parâmetro.</span><span class="sxs-lookup"><span data-stu-id="d738a-140">So be sure you really need Premium before using that parameter.</span></span>


