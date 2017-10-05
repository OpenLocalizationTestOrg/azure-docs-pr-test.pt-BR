---
title: "Criar ou modificar laboratórios automaticamente usando modelos do Azure Resource Manager com o PowerShell | Microsoft Docs"
description: "Saiba como usar modelos de Azure Resource Manager com o PowerShell para criar ou modificar laboratórios automaticamente em um laboratório DevTest"
services: devtest-lab,virtual-machines,visual-studio-online
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: dad9944c-0b20-48be-ba80-8f4aa0950903
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/21/2017
ms.author: tarcher
ms.openlocfilehash: cea4531175df2cc39790497dc049d27e23ffa0c6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="create-or-modify-labs-automatically-using-azure-resource-manager-templates-and-powershell"></a><span data-ttu-id="e2fd7-103">Criar ou modificar laboratórios automaticamente usando modelos do Azure Resource Manager e o PowerShell</span><span class="sxs-lookup"><span data-stu-id="e2fd7-103">Create or modify labs automatically using Azure Resource Manager templates and PowerShell</span></span>

<span data-ttu-id="e2fd7-104">Laboratórios DevTest fornece muitos modelos de Azure Resource Manager e scripts do PowerShell que podem ajudá-lo rapidamente e criar automaticamente os novos laboratórios ou modificar laboratórios existentes e implantar esses recursos.</span><span class="sxs-lookup"><span data-stu-id="e2fd7-104">DevTest Labs provides many Azure Resource Manager templates and PowerShell scripts that can help you quickly and automatically create new labs or modify existing labs and then deploy these resources.</span></span>

<span data-ttu-id="e2fd7-105">Este artigo ajuda a orientar você durante o processo de usar esses modelos e scripts para automatizar a criação, modificação e implantação de seus laboratórios.</span><span class="sxs-lookup"><span data-stu-id="e2fd7-105">This article helps guide you through the process of using these templates and scripts to automate the creation, modification, and deployment of your labs.</span></span> <span data-ttu-id="e2fd7-106">Este artigo também mostra onde você pode encontrar mais informações sobre como usar o PowerShell para realizar algumas tarefas comuns nos laboratórios de DevTest.</span><span class="sxs-lookup"><span data-stu-id="e2fd7-106">This article also shows you where you can find more information about how to use PowerShell to perform some common tasks in DevTest Labs.</span></span>

## <a name="step-1-gather-your-templates-and-scripts"></a><span data-ttu-id="e2fd7-107">Etapa 1: Coletar seus modelos e scripts</span><span class="sxs-lookup"><span data-stu-id="e2fd7-107">Step 1: Gather your templates and scripts</span></span>
<span data-ttu-id="e2fd7-108">Você pode encontrar [modelos do Azure Resource Manager](https://github.com/Azure/azure-devtestlab/tree/master/ARMTemplates) e [scripts do PowerShell](https://github.com/Azure/azure-devtestlab/tree/master/Scripts) pré-realizados em nosso [repositório Github](https://github.com/Azure/azure-devtestlab) público.</span><span class="sxs-lookup"><span data-stu-id="e2fd7-108">You can find pre-made [Azure Resource Manager templates](https://github.com/Azure/azure-devtestlab/tree/master/ARMTemplates) and [PowerShell scripts](https://github.com/Azure/azure-devtestlab/tree/master/Scripts) at our public [Github repository](https://github.com/Azure/azure-devtestlab).</span></span> <span data-ttu-id="e2fd7-109">Use-os como estão, ou personalize-os para suas necessidades e armazene-os em seu próprio [repositório particular do Git](devtest-lab-add-artifact-repo.md).</span><span class="sxs-lookup"><span data-stu-id="e2fd7-109">Use them as-is, or customize them for your needs and store them in your own [private Git repo](devtest-lab-add-artifact-repo.md).</span></span> 

## <a name="step-2-modify-your-azure-resource-manager-template"></a><span data-ttu-id="e2fd7-110">Etapa 2: Modificar o modelo do Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="e2fd7-110">Step 2: Modify your Azure Resource Manager template</span></span>
<span data-ttu-id="e2fd7-111">Você pode seguir as etapas em [Criar seu primeiro modelo do Azure Resource Manager](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-manager-create-first-template) se você nunca tiver criado um modelo antes.</span><span class="sxs-lookup"><span data-stu-id="e2fd7-111">You can follow the steps at [Create your first Azure Resource Manager template](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-manager-create-first-template) if you have never created a template before.</span></span>

<span data-ttu-id="e2fd7-112">Além disso, [Práticas recomendadas para criação de modelos do Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/resource-manager-template-best-practices) oferece muitas diretrizes e sugestões para lhe ajudar a criar modelos do Azure Resource Manager que são confiáveis e fáceis de usar.</span><span class="sxs-lookup"><span data-stu-id="e2fd7-112">In addition, [Best practices for creating Azure Resource Manager templates](https://docs.microsoft.com/azure/azure-resource-manager/resource-manager-template-best-practices) offers many guidelines and suggestions to help you create Azure Resource Manager templates that are reliable and easy to use.</span></span> <span data-ttu-id="e2fd7-113">Normalmente, você usará uma variação de um dos exemplos ou abordagens fornecidos e modificará o modelo para suas necessidades.</span><span class="sxs-lookup"><span data-stu-id="e2fd7-113">Typically, you will use a variation of one of the approaches or examples provided and modify your template for your needs.</span></span>

## <a name="step-3-deploy-resources-with-powershell"></a><span data-ttu-id="e2fd7-114">Etapa 3: Implantar recursos com o PowerShell</span><span class="sxs-lookup"><span data-stu-id="e2fd7-114">Step 3: Deploy resources with PowerShell</span></span>
<span data-ttu-id="e2fd7-115">Depois que você personalizou os modelos e scripts, siga as etapas necessárias para [implantar recursos com modelos do Resource Manager e o Azure PowerShell](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-template-deploy).</span><span class="sxs-lookup"><span data-stu-id="e2fd7-115">After you have customized your templates and scripts, follow the steps necessary to [deploy resources with Resource Manager templates and Azure PowerShell](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-template-deploy).</span></span> <span data-ttu-id="e2fd7-116">O artigo fornece informações gerais sobre como usar o Azure PowerShell com modelos do Azure Resource Manager para implantar os recursos no Azure.</span><span class="sxs-lookup"><span data-stu-id="e2fd7-116">The article provides general information about using Azure PowerShell with Azure Resource Manager templates to deploy your resources to Azure.</span></span>


## <a name="common-tasks-you-can-perform-in-devtest-labs-using-powershell"></a><span data-ttu-id="e2fd7-117">Tarefas comuns que você pode executar nos laboratórios de DevTest usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="e2fd7-117">Common tasks you can perform in DevTest labs using PowerShell</span></span>
<span data-ttu-id="e2fd7-118">Há várias outras tarefas comuns que você pode automatizar usando o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e2fd7-118">There are many other common tasks that you can automate by using PowerShell.</span></span> <span data-ttu-id="e2fd7-119">As seções da documentação a seguir descrevem as etapas necessárias para executar essas tarefas.</span><span class="sxs-lookup"><span data-stu-id="e2fd7-119">The following sections of the documentation outline the steps required to perform these tasks.</span></span>

* [<span data-ttu-id="e2fd7-120">Criar uma imagem personalizada de um arquivo VHD usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="e2fd7-120">Create a custom image from a VHD file using PowerShell</span></span>](devtest-lab-create-custom-image-from-vhd-using-powershell.md)
* [<span data-ttu-id="e2fd7-121">Carregar arquivo VHD na conta de armazenamento do laboratório usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="e2fd7-121">Upload VHD file to lab's storage account using PowerShell</span></span>](devtest-lab-upload-vhd-using-powershell.md)
* [<span data-ttu-id="e2fd7-122">Adicionar um usuário externo a um laboratório usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="e2fd7-122">Add an external user to a lab using PowerShell</span></span>](devtest-lab-add-devtest-user.md#add-an-external-user-to-a-lab-using-powershell)
* [<span data-ttu-id="e2fd7-123">Criar uma função personalizada do laboratório usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="e2fd7-123">Create a lab custom role using PowerShell</span></span>](devtest-lab-grant-user-permissions-to-specific-lab-policies.md#creating-a-lab-custom-role-using-powershell)

### <a name="next-steps"></a><span data-ttu-id="e2fd7-124">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="e2fd7-124">Next steps</span></span>
* <span data-ttu-id="e2fd7-125">Saiba como criar um [repositório gito](devtest-lab-add-artifact-repo.md) em que você armazenará seus modelos personalizados ou scripts.</span><span class="sxs-lookup"><span data-stu-id="e2fd7-125">Learn how to create a [private Git repository](devtest-lab-add-artifact-repo.md) where you will store your customized templates or scripts.</span></span>
* <span data-ttu-id="e2fd7-126">Explore os [modelos do Azure Resource Manager na galeria de modelos de Início Rápido do Azure](https://github.com/Azure/azure-quickstart-templates).</span><span class="sxs-lookup"><span data-stu-id="e2fd7-126">Explore the [Azure Resource Manager templates from Azure Quickstart template gallery](https://github.com/Azure/azure-quickstart-templates).</span></span>
