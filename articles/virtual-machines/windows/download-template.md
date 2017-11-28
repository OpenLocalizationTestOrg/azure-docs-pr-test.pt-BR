---
title: Baixar o modelo de uma VM do Azure | Microsoft Docs
description: "Baixe o modelo de uma VM para ajudar a automatizar as implantações no modelo de implantação do Resource Manager"
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 51ef4f51-0942-4249-afea-4a3f87ce1ff8
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 03/22/2017
ms.author: cynthn
ms.openlocfilehash: 9e4c0c3cf0e233447369a24b1d5fe27495abd1cf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="download-the-template-for-a-vm"></a><span data-ttu-id="67215-103">Baixar o modelo para uma VM</span><span class="sxs-lookup"><span data-stu-id="67215-103">Download the template for a VM</span></span>
<span data-ttu-id="67215-104">Quando você cria uma VM no Azure usando o portal ou o PowerShell, um modelo do Resource Manager é criado automaticamente para você.</span><span class="sxs-lookup"><span data-stu-id="67215-104">When you create a VM in Azure using the portal or PowerShell, a Resource Manager template is automatically created for you.</span></span> <span data-ttu-id="67215-105">Você pode usar este modelo para duplicar rapidamente uma implantação.</span><span class="sxs-lookup"><span data-stu-id="67215-105">You can use this template to quickly duplicate a deployment.</span></span> <span data-ttu-id="67215-106">O modelo contém informações sobre todos os recursos em um grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="67215-106">The template contains information about all of the resources in a resource group.</span></span> <span data-ttu-id="67215-107">Para uma máquina virtual, isso significa que o modelo contém tudo o que é criado para dar suporte à VM desse grupo de recursos, incluindo os recursos de rede.</span><span class="sxs-lookup"><span data-stu-id="67215-107">For a virtual machine, this means the template contains everything that is created in support of the VM in that resource group, including the networking resources.</span></span>

## <a name="download-the-template-using-the-portal"></a><span data-ttu-id="67215-108">Baixar o modelo usando o portal</span><span class="sxs-lookup"><span data-stu-id="67215-108">Download the template using the portal</span></span>
1. <span data-ttu-id="67215-109">Faça logon no [Portal do Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="67215-109">Log in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="67215-110">No menu do hub, selecione **Máquinas Virtuais**.</span><span class="sxs-lookup"><span data-stu-id="67215-110">One the hub menu, select **Virtual Machines**.</span></span>
3. <span data-ttu-id="67215-111">Selecione a máquina virtual na lista.</span><span class="sxs-lookup"><span data-stu-id="67215-111">Select the virtual machine from the list.</span></span>
4. <span data-ttu-id="67215-112">Selecione **Script de automação**.</span><span class="sxs-lookup"><span data-stu-id="67215-112">Select **Automation script**.</span></span>
5. <span data-ttu-id="67215-113">Selecione **Baixar** e salve o arquivo zip em seu computador local.</span><span class="sxs-lookup"><span data-stu-id="67215-113">Select **Download** and save the .zip file to your local computer.</span></span>
6. <span data-ttu-id="67215-114">Abra o arquivo zip e extraia os arquivos para uma pasta.</span><span class="sxs-lookup"><span data-stu-id="67215-114">Open the .zip file and extract the files to a folder.</span></span> <span data-ttu-id="67215-115">O arquivo zip conterá:</span><span class="sxs-lookup"><span data-stu-id="67215-115">The .zip file will contain:</span></span>
   
   * <span data-ttu-id="67215-116">deploy.ps1</span><span class="sxs-lookup"><span data-stu-id="67215-116">deploy.ps1</span></span>
   * <span data-ttu-id="67215-117">deploy.sh</span><span class="sxs-lookup"><span data-stu-id="67215-117">deploy.sh</span></span> 
   * <span data-ttu-id="67215-118">deployer.rb</span><span class="sxs-lookup"><span data-stu-id="67215-118">deployer.rb</span></span>
   * <span data-ttu-id="67215-119">DeploymentHelper.cs</span><span class="sxs-lookup"><span data-stu-id="67215-119">DeploymentHelper.cs</span></span>
   * <span data-ttu-id="67215-120">parameters.json</span><span class="sxs-lookup"><span data-stu-id="67215-120">parameters.json</span></span>
   * <span data-ttu-id="67215-121">template.json</span><span class="sxs-lookup"><span data-stu-id="67215-121">template.json</span></span>

<span data-ttu-id="67215-122">O arquivo template.json é o modelo.</span><span class="sxs-lookup"><span data-stu-id="67215-122">The template.json file is the template.</span></span>

## <a name="download-the-template-using-powershell"></a><span data-ttu-id="67215-123">Baixar o modelo usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="67215-123">Download the template using PowerShell</span></span>
<span data-ttu-id="67215-124">Você também pode baixar o arquivo de modelo .json usando o cmdlet [Export-AzureRMResourceGroup](https://msdn.microsoft.com/library/mt715427.aspx).</span><span class="sxs-lookup"><span data-stu-id="67215-124">You can also download the .json template file using the [Export-AzureRMResourceGroup](https://msdn.microsoft.com/library/mt715427.aspx) cmdlet.</span></span> <span data-ttu-id="67215-125">Você pode usar o parâmetro `-path` para fornecer o nome de arquivo e o caminho para o arquivo .json.</span><span class="sxs-lookup"><span data-stu-id="67215-125">You can use the `-path` parameter to provide the filename and path for the .json file.</span></span> <span data-ttu-id="67215-126">Este exemplo mostra como baixar o modelo para o grupo de recursos denominado **myResourceGroup** para a pasta **C:\users\public\downloads** no computador local.</span><span class="sxs-lookup"><span data-stu-id="67215-126">This example shows how to download the template for the resource group named **myResourceGroup** to the **C:\users\public\downloads** folder on your local computer.</span></span>

```powershell
    Export-AzureRmResourceGroup -ResourceGroupName "myResourceGroup" -Path "C:\users\public\downloads"
```

## <a name="next-steps"></a><span data-ttu-id="67215-127">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="67215-127">Next steps</span></span>
<span data-ttu-id="67215-128">Para saber mais sobre como implantar recursos usando modelos, veja o [passo a passo do modelo do Resource Manager](../../azure-resource-manager/resource-manager-template-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="67215-128">To learn more about deploying resources using templates, see [Resource Manager template walkthrough](../../azure-resource-manager/resource-manager-template-walkthrough.md).</span></span>

