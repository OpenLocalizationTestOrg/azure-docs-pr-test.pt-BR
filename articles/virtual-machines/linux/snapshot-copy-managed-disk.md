---
title: um gerenciado do Azure do disco para fazer backup de aaaCopy | Microsoft Docs
description: "Saiba como toocreate uma cópia de um toouse de disco gerenciado do Azure para fazer backup ou solução de problemas de disco emite."
documentationcenter: 
author: squillace
manager: timlt
editor: 
tags: azure-resource-manager
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 2/6/2017
ms.author: rasquill
ms.openlocfilehash: 41b91c2d68eb5be9c493a66be5f7d085a70450d0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-copy-of-a-vhd-stored-as-an-azure-managed-disk-by-using-managed-snapshots"></a><span data-ttu-id="3b3e8-103">Criar uma cópia de um VHD armazenado como um Disco Gerenciado do Azure usando instantâneos gerenciados</span><span class="sxs-lookup"><span data-stu-id="3b3e8-103">Create a copy of a VHD stored as an Azure Managed Disk by using Managed Snapshots</span></span>
<span data-ttu-id="3b3e8-104">Tirar um instantâneo de um disco de gerenciado para backup ou criar um disco gerenciado de instantâneo hello e anexá-lo tooa tootroubleshoot de máquina virtual de teste.</span><span class="sxs-lookup"><span data-stu-id="3b3e8-104">Take a snapshot of a Managed disk for backup or create a Managed Disk from hello snapshot and attach it tooa test virtual machine tootroubleshoot.</span></span> <span data-ttu-id="3b3e8-105">Um Instantâneo Gerenciado é uma cópia pontual completa de um Disco Gerenciado da VM.</span><span class="sxs-lookup"><span data-stu-id="3b3e8-105">A Managed Snapshot is a full point-in-time copy of a VM Managed Disk.</span></span> <span data-ttu-id="3b3e8-106">Ele cria uma cópia somente leitura do seu VHD e, por padrão, a armazena como um Disco Gerenciado Standard.</span><span class="sxs-lookup"><span data-stu-id="3b3e8-106">It creates a read-only copy of your VHD and, by default, stores it as a Standard Managed Disk.</span></span> 

<span data-ttu-id="3b3e8-107">Para saber mais sobre preços, confira [Preços de Armazenamento do Azure](https://azure.microsoft.com/pricing/details/managed-disks/).</span><span class="sxs-lookup"><span data-stu-id="3b3e8-107">For information about pricing, see [Azure Storage Pricing](https://azure.microsoft.com/pricing/details/managed-disks/).</span></span> <!--Add link tootopic or blog post that explains managed disks. -->

<span data-ttu-id="3b3e8-108">Use o hello Azure tootake de 2.0 do CLI do Azure do portal ou hello um instantâneo de saudação disco gerenciado.</span><span class="sxs-lookup"><span data-stu-id="3b3e8-108">Use either hello Azure portal or hello Azure CLI 2.0 tootake a snapshot of hello Managed Disk.</span></span>

## <a name="use-azure-cli-20-tootake-a-snapshot"></a><span data-ttu-id="3b3e8-109">Usar o Azure CLI 2.0 tootake um instantâneo</span><span class="sxs-lookup"><span data-stu-id="3b3e8-109">Use Azure CLI 2.0 tootake a snapshot</span></span>

> [!NOTE] 
> <span data-ttu-id="3b3e8-110">Olá exemplo a seguir requer hello Azure CLI 2.0 instalado e registrado na sua conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="3b3e8-110">hello following example requires hello Azure CLI 2.0 installed and logged into your Azure account.</span></span>

<span data-ttu-id="3b3e8-111">Olá etapas a seguir mostram como tooobtain e tirar um instantâneo de um sistema operacional gerenciado disco usando Olá `az snapshot create` com hello `--source-disk` parâmetro.</span><span class="sxs-lookup"><span data-stu-id="3b3e8-111">hello following steps show how tooobtain and take a snapshot of a managed OS disk using hello `az snapshot create` command with hello `--source-disk` parameter.</span></span> <span data-ttu-id="3b3e8-112">Olá exemplo a seguir supõe que haja uma VM chamada `myVM` criado com um disco de sistema operacional gerenciado no hello `myResourceGroup` grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="3b3e8-112">hello following example assumes that there is a VM called `myVM` created with a managed OS disk in hello `myResourceGroup` resource group.</span></span>

```azure-cli
# take hello disk id with which toocreate a snapshot
osDiskId=$(az vm show -g myResourceGroup -n myVM --query "storageProfile.osDisk.managedDisk.id" -o tsv)
az snapshot create -g myResourceGroup --source "$osDiskId" --name osDisk-backup
```

<span data-ttu-id="3b3e8-113">saída de Hello deve ser algo como:</span><span class="sxs-lookup"><span data-stu-id="3b3e8-113">hello output should look something like:</span></span>

```json
{
  "accountType": "Standard_LRS",
  "creationData": {
    "createOption": "Copy",
    "imageReference": null,
    "sourceResourceId": null,
    "sourceUri": "/subscriptions/<guid>/resourceGroups/myResourceGroup/providers/Microsoft.Compute/disks/osdisk_6NexYgkFQU",
    "storageAccountId": null
  },
  "diskSizeGb": 30,
  "encryptionSettings": null,
  "id": "/subscriptions/<guid>/resourceGroups/myResourceGroup/providers/Microsoft.Compute/snapshots/osDisk-backup",
  "location": "westus",
  "name": "osDisk-backup",
  "osType": "Linux",
  "ownerId": null,
  "provisioningState": "Succeeded",
  "resourceGroup": "myResourceGroup",
  "tags": null,
  "timeCreated": "2017-02-06T21:27:10.172980+00:00",
  "type": "Microsoft.Compute/snapshots"
}
```

## <a name="use-azure-portal-tootake-a-snapshot"></a><span data-ttu-id="3b3e8-114">Use tootake portal do Azure um instantâneo</span><span class="sxs-lookup"><span data-stu-id="3b3e8-114">Use Azure portal tootake a snapshot</span></span> 

1. <span data-ttu-id="3b3e8-115">Entrar toohello [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="3b3e8-115">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="3b3e8-116">Iniciando no hello superior esquerdo, clique em **novo** e procure **instantâneo**.</span><span class="sxs-lookup"><span data-stu-id="3b3e8-116">Starting in hello upper-left, click **New** and search for **snapshot**.</span></span>
3. <span data-ttu-id="3b3e8-117">Na folha de instantâneo hello, clique em **criar**.</span><span class="sxs-lookup"><span data-stu-id="3b3e8-117">In hello Snapshot blade, click **Create**.</span></span>
4. <span data-ttu-id="3b3e8-118">Insira um **nome** para instantâneo de saudação.</span><span class="sxs-lookup"><span data-stu-id="3b3e8-118">Enter a **Name** for hello snapshot.</span></span>
5. <span data-ttu-id="3b3e8-119">Selecione uma existente [grupo de recursos](../../azure-resource-manager/resource-group-overview.md#resource-groups) ou nome de saudação do tipo para um novo.</span><span class="sxs-lookup"><span data-stu-id="3b3e8-119">Select an existing [Resource group](../../azure-resource-manager/resource-group-overview.md#resource-groups) or type hello name for a new one.</span></span> 
6. <span data-ttu-id="3b3e8-120">Selecione um Local do datacenter do Azure.</span><span class="sxs-lookup"><span data-stu-id="3b3e8-120">Select an Azure datacenter Location.</span></span>  
7. <span data-ttu-id="3b3e8-121">Para **disco de origem**, selecione Olá toosnapshot de disco gerenciado.</span><span class="sxs-lookup"><span data-stu-id="3b3e8-121">For **Source disk**, select hello Managed Disk toosnapshot.</span></span>
8. <span data-ttu-id="3b3e8-122">Selecione Olá **tipo de conta** instantâneo de saudação do toouse toostore.</span><span class="sxs-lookup"><span data-stu-id="3b3e8-122">Select hello **Account type** toouse toostore hello snapshot.</span></span> <span data-ttu-id="3b3e8-123">É recomendável **Standard_LRS**, a menos que você precise dele armazenado em um disco de alto desempenho.</span><span class="sxs-lookup"><span data-stu-id="3b3e8-123">We recommend **Standard_LRS** unless you need it stored on a high performing disk.</span></span>
9. <span data-ttu-id="3b3e8-124">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="3b3e8-124">Click **Create**.</span></span>

<span data-ttu-id="3b3e8-125">Se você planejar toouse Olá instantâneo toocreate um disco gerenciado e anexá-lo uma VM que precisa toobe alto desempenho, use o parâmetro hello `--sku Premium_LRS` com hello `az snapshot create` comando.</span><span class="sxs-lookup"><span data-stu-id="3b3e8-125">If you plan toouse hello snapshot toocreate a Managed Disk and attach it a VM that needs toobe high performing, use hello parameter `--sku Premium_LRS` with hello `az snapshot create` command.</span></span> <span data-ttu-id="3b3e8-126">Isso cria o instantâneo Olá para que ela é armazenada como um disco de gerenciado para Premium.</span><span class="sxs-lookup"><span data-stu-id="3b3e8-126">This creates hello snapshot so that it is stored as a Premium Managed Disk.</span></span> <span data-ttu-id="3b3e8-127">Os Discos Gerenciados Premium têm melhor desempenho porque são SSDs (unidades de estado sólido), mas são mais caros que os HDDs (discos rígidos) Standard.</span><span class="sxs-lookup"><span data-stu-id="3b3e8-127">Premium Managed Disks perform better because they are solid-state drives (SSDs), but cost more than Standard disks (HDDs).</span></span>


