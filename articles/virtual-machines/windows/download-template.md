---
title: "modelo de saudação aaaDownload para uma VM do Azure | Microsoft Docs"
description: "Baixar Olá templatefor toohelp uma VM com a automação implantações no modelo de implantação do Gerenciador de recursos de saudação"
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
ms.openlocfilehash: 86fd05f67409019b5e5c9023881745047860eee1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="download-hello-template-for-a-vm"></a><span data-ttu-id="d3b73-103">Baixar modelo de saudação para uma máquina virtual</span><span class="sxs-lookup"><span data-stu-id="d3b73-103">Download hello template for a VM</span></span>
<span data-ttu-id="d3b73-104">Quando você cria uma máquina virtual no Azure usando o portal de saudação ou o PowerShell, um Gerenciador de recursos de modelo é criado automaticamente para você.</span><span class="sxs-lookup"><span data-stu-id="d3b73-104">When you create a VM in Azure using hello portal or PowerShell, a Resource Manager template is automatically created for you.</span></span> <span data-ttu-id="d3b73-105">Você pode usar essa cópia do modelo tooquickly uma implantação.</span><span class="sxs-lookup"><span data-stu-id="d3b73-105">You can use this template tooquickly duplicate a deployment.</span></span> <span data-ttu-id="d3b73-106">modelo de saudação contém informações sobre todos os recursos de saudação em um grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="d3b73-106">hello template contains information about all of hello resources in a resource group.</span></span> <span data-ttu-id="d3b73-107">Para uma máquina virtual, isso significa modelo Olá contém tudo o que é criado para oferecer suporte a saudação VM desse grupo de recursos, incluindo recursos de rede hello.</span><span class="sxs-lookup"><span data-stu-id="d3b73-107">For a virtual machine, this means hello template contains everything that is created in support of hello VM in that resource group, including hello networking resources.</span></span>

## <a name="download-hello-template-using-hello-portal"></a><span data-ttu-id="d3b73-108">Baixar modelo hello usando o portal de saudação</span><span class="sxs-lookup"><span data-stu-id="d3b73-108">Download hello template using hello portal</span></span>
1. <span data-ttu-id="d3b73-109">Faça logon no toohello [portal do Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="d3b73-109">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="d3b73-110">Menu de hub uma saudação, selecione **máquinas virtuais**.</span><span class="sxs-lookup"><span data-stu-id="d3b73-110">One hello hub menu, select **Virtual Machines**.</span></span>
3. <span data-ttu-id="d3b73-111">Selecione máquina virtual de Olá Olá lista.</span><span class="sxs-lookup"><span data-stu-id="d3b73-111">Select hello virtual machine from hello list.</span></span>
4. <span data-ttu-id="d3b73-112">Selecione **Script de automação**.</span><span class="sxs-lookup"><span data-stu-id="d3b73-112">Select **Automation script**.</span></span>
5. <span data-ttu-id="d3b73-113">Selecione **baixar** e salve o computador local do tooyour do arquivo hello. zip.</span><span class="sxs-lookup"><span data-stu-id="d3b73-113">Select **Download** and save hello .zip file tooyour local computer.</span></span>
6. <span data-ttu-id="d3b73-114">Abra o arquivo. zip de saudação e extração Olá arquivos tooa pasta.</span><span class="sxs-lookup"><span data-stu-id="d3b73-114">Open hello .zip file and extract hello files tooa folder.</span></span> <span data-ttu-id="d3b73-115">arquivo. zip de saudação conterá:</span><span class="sxs-lookup"><span data-stu-id="d3b73-115">hello .zip file will contain:</span></span>
   
   * <span data-ttu-id="d3b73-116">deploy.ps1</span><span class="sxs-lookup"><span data-stu-id="d3b73-116">deploy.ps1</span></span>
   * <span data-ttu-id="d3b73-117">deploy.sh</span><span class="sxs-lookup"><span data-stu-id="d3b73-117">deploy.sh</span></span> 
   * <span data-ttu-id="d3b73-118">deployer.rb</span><span class="sxs-lookup"><span data-stu-id="d3b73-118">deployer.rb</span></span>
   * <span data-ttu-id="d3b73-119">DeploymentHelper.cs</span><span class="sxs-lookup"><span data-stu-id="d3b73-119">DeploymentHelper.cs</span></span>
   * <span data-ttu-id="d3b73-120">parameters.json</span><span class="sxs-lookup"><span data-stu-id="d3b73-120">parameters.json</span></span>
   * <span data-ttu-id="d3b73-121">template.json</span><span class="sxs-lookup"><span data-stu-id="d3b73-121">template.json</span></span>

<span data-ttu-id="d3b73-122">arquivo de template.json Olá é o modelo de saudação.</span><span class="sxs-lookup"><span data-stu-id="d3b73-122">hello template.json file is hello template.</span></span>

## <a name="download-hello-template-using-powershell"></a><span data-ttu-id="d3b73-123">Baixar modelo hello usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="d3b73-123">Download hello template using PowerShell</span></span>
<span data-ttu-id="d3b73-124">Você também pode baixar o arquivo de modelo do hello. JSON usando Olá [AzureRMResourceGroup de exportação](https://msdn.microsoft.com/library/mt715427.aspx) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="d3b73-124">You can also download hello .json template file using hello [Export-AzureRMResourceGroup](https://msdn.microsoft.com/library/mt715427.aspx) cmdlet.</span></span> <span data-ttu-id="d3b73-125">Você pode usar o hello `-path` parâmetro tooprovide Olá filename e o caminho de arquivo do hello. JSON.</span><span class="sxs-lookup"><span data-stu-id="d3b73-125">You can use hello `-path` parameter tooprovide hello filename and path for hello .json file.</span></span> <span data-ttu-id="d3b73-126">Este exemplo mostra como o modelo de saudação do toodownload Olá para grupo de recursos denominado **myResourceGroup** toohello **C:\users\public\downloads** pasta no computador local.</span><span class="sxs-lookup"><span data-stu-id="d3b73-126">This example shows how toodownload hello template for hello resource group named **myResourceGroup** toohello **C:\users\public\downloads** folder on your local computer.</span></span>

```powershell
    Export-AzureRmResourceGroup -ResourceGroupName "myResourceGroup" -Path "C:\users\public\downloads"
```

## <a name="next-steps"></a><span data-ttu-id="d3b73-127">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="d3b73-127">Next steps</span></span>
<span data-ttu-id="d3b73-128">toolearn mais sobre a implantação de recursos usando modelos, consulte [passo a passo do Gerenciador de recursos modelo](../../azure-resource-manager/resource-manager-template-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="d3b73-128">toolearn more about deploying resources using templates, see [Resource Manager template walkthrough](../../azure-resource-manager/resource-manager-template-walkthrough.md).</span></span>

