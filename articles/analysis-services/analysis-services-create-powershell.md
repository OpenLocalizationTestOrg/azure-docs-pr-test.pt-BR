---
title: "aaaCreate um servidor de serviços de análise do Azure usando o PowerShell | Microsoft Docs"
description: Saiba como toocreate um Azure Analysis Services server usando o PowerShell
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
ms.assetid: 
ms.service: analysis-services
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 08/01/2017
ms.author: owend
ms.custom: mvc
ms.openlocfilehash: 269b78983410f773d47c4cea34d6d353b19f9e91
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-analysis-services-server-by-using-powershell"></a><span data-ttu-id="0f4f1-103">Criar a um servidor do Azure Analysis Services usando PowerShell</span><span class="sxs-lookup"><span data-stu-id="0f4f1-103">Create an Azure Analysis Services server by using PowerShell</span></span>

<span data-ttu-id="0f4f1-104">Este guia de início rápido descreve como usar o PowerShell do hello toocreate de linha de comando um servidor do Azure Analysis Services em um [grupo de recursos do Azure](../azure-resource-manager/resource-group-overview.md) na sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="0f4f1-104">This quickstart describes using PowerShell from hello command line toocreate an Azure Analysis Services server in an [Azure resource group](../azure-resource-manager/resource-group-overview.md) in your Azure subscription.</span></span>

<span data-ttu-id="0f4f1-105">Esta tarefa exige o módulo do Azure PowerShell, versão 4.0 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="0f4f1-105">This task requires Azure PowerShell module version 4.0 or later.</span></span> <span data-ttu-id="0f4f1-106">versão de hello toofind, execute ` Get-Module -ListAvailable AzureRM`.</span><span class="sxs-lookup"><span data-stu-id="0f4f1-106">toofind hello version, run ` Get-Module -ListAvailable AzureRM`.</span></span> <span data-ttu-id="0f4f1-107">tooinstall ou atualização, consulte [instalar o módulo PowerShell Azure](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="0f4f1-107">tooinstall or upgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span> 

> [!NOTE]
> <span data-ttu-id="0f4f1-108">Criar um servidor pode resultar em um novo serviço faturável.</span><span class="sxs-lookup"><span data-stu-id="0f4f1-108">Creating a server might result in a new billable service.</span></span> <span data-ttu-id="0f4f1-109">mais, consulte toolearn [preços do Analysis Services](https://azure.microsoft.com/pricing/details/analysis-services/).</span><span class="sxs-lookup"><span data-stu-id="0f4f1-109">toolearn more, see [Analysis Services pricing](https://azure.microsoft.com/pricing/details/analysis-services/).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0f4f1-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="0f4f1-110">Prerequisites</span></span>
<span data-ttu-id="0f4f1-111">toocomplete este guia de início rápido, você precisa:</span><span class="sxs-lookup"><span data-stu-id="0f4f1-111">toocomplete this quickstart, you need:</span></span>

* <span data-ttu-id="0f4f1-112">**Assinatura do Azure**: visite [avaliação gratuita do Azure](https://azure.microsoft.com/offers/ms-azr-0044p/) toocreate uma conta.</span><span class="sxs-lookup"><span data-stu-id="0f4f1-112">**Azure subscription**: Visit [Azure Free Trial](https://azure.microsoft.com/offers/ms-azr-0044p/) toocreate an account.</span></span>
* <span data-ttu-id="0f4f1-113">**Azure Active Directory**: sua assinatura deve estar associada a um locatário do Azure Active Directory, e você precisa ter uma conta nesse diretório.</span><span class="sxs-lookup"><span data-stu-id="0f4f1-113">**Azure Active Directory**: Your subscription must be associated with an Azure Active Directory tenant and you must have an account in that directory.</span></span> <span data-ttu-id="0f4f1-114">mais, consulte toolearn [permissões de usuário e autenticação](analysis-services-manage-users.md).</span><span class="sxs-lookup"><span data-stu-id="0f4f1-114">toolearn more, see [Authentication and user permissions](analysis-services-manage-users.md).</span></span>

## <a name="import-azurermanalysisservices-module"></a><span data-ttu-id="0f4f1-115">Importar o módulo AzureRm.AnalysisServices</span><span class="sxs-lookup"><span data-stu-id="0f4f1-115">Import AzureRm.AnalysisServices module</span></span>
<span data-ttu-id="0f4f1-116">toocreate um servidor em sua assinatura, você usar Olá [AzureRM.AnalysisServices](https://www.powershellgallery.com/packages/AzureRM.AnalysisServices) módulo de componente.</span><span class="sxs-lookup"><span data-stu-id="0f4f1-116">toocreate a server in your subscription, you use hello [AzureRM.AnalysisServices](https://www.powershellgallery.com/packages/AzureRM.AnalysisServices)  component module.</span></span> <span data-ttu-id="0f4f1-117">Carregar o módulo de AzureRm.AnalysisServices de saudação em sua sessão do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="0f4f1-117">Load hello AzureRm.AnalysisServices module into your PowerShell session.</span></span>

```powershell
Import-Module AzureRM.AnalysisServices
```

## <a name="sign-in-tooazure"></a><span data-ttu-id="0f4f1-118">Entrar tooAzure</span><span class="sxs-lookup"><span data-stu-id="0f4f1-118">Sign in tooAzure</span></span>

<span data-ttu-id="0f4f1-119">Entrar tooyour assinatura do Azure usando Olá [AzureRmAccount adicionar](/powershell/module/azurerm.profile/add-azurermaccount) comando.</span><span class="sxs-lookup"><span data-stu-id="0f4f1-119">Sign in tooyour Azure subscription by using hello [Add-AzureRmAccount](/powershell/module/azurerm.profile/add-azurermaccount) command.</span></span> <span data-ttu-id="0f4f1-120">Siga Olá na tela instruções.</span><span class="sxs-lookup"><span data-stu-id="0f4f1-120">Follow hello on-screen directions.</span></span>

```powershell
Add-AzureRmAccount
```

## <a name="create-a-resource-group"></a><span data-ttu-id="0f4f1-121">Criar um grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="0f4f1-121">Create a resource group</span></span>
 
<span data-ttu-id="0f4f1-122">Um [grupo de recursos do Azure](../azure-resource-manager/resource-group-overview.md) é um contêiner lógico no qual os recursos do Azure são implantados e gerenciados em grupo.</span><span class="sxs-lookup"><span data-stu-id="0f4f1-122">An [Azure resource group](../azure-resource-manager/resource-group-overview.md) is a logical container where Azure resources are deployed and managed as a group.</span></span> <span data-ttu-id="0f4f1-123">Quando você cria o servidor, precisa especificar um grupo de recursos em sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="0f4f1-123">When you create your server, you must specify a resource group in your subscription.</span></span> <span data-ttu-id="0f4f1-124">Se você não tiver um grupo de recursos, você pode criar um novo usando Olá [AzureRmResourceGroup novo](/powershell/module/azurerm.resources/new-azurermresourcegroup) comando.</span><span class="sxs-lookup"><span data-stu-id="0f4f1-124">If you do not already have a resource group, you can create a new one by using hello [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) command.</span></span> <span data-ttu-id="0f4f1-125">Olá, exemplo a seguir cria um grupo de recursos denominado `myResourceGroup` na região Oeste dos EUA de saudação.</span><span class="sxs-lookup"><span data-stu-id="0f4f1-125">hello following example creates a resource group named `myResourceGroup` in hello West US region.</span></span>

```powershell
New-AzureRmResourceGroup -Name "myResourceGroup" -Location "West US"
```

## <a name="create-a-server"></a><span data-ttu-id="0f4f1-126">Criar um servidor</span><span class="sxs-lookup"><span data-stu-id="0f4f1-126">Create a server</span></span>

<span data-ttu-id="0f4f1-127">Criar um novo servidor usando Olá [AzureRmAnalysisServicesServer novo](/powershell/module/azurerm.analysisservices/new-azurermanalysisservicesserver) comando.</span><span class="sxs-lookup"><span data-stu-id="0f4f1-127">Create a new server by using hello [New-AzureRmAnalysisServicesServer](/powershell/module/azurerm.analysisservices/new-azurermanalysisservicesserver) command.</span></span> <span data-ttu-id="0f4f1-128">Olá exemplo a seguir cria um servidor chamado myServer na myResourceGroup, na região do Oeste dos EUA hello, na camada de saudação D1 e especifica philipc@adventureworks.com como um administrador de servidor.</span><span class="sxs-lookup"><span data-stu-id="0f4f1-128">hello following example creates a server named myServer in myResourceGroup, in hello West US region, at hello D1 tier, and specifies philipc@adventureworks.com as a server administrator.</span></span>

```powershell
New-AzureRmAnalysisServicesServer -ResourceGroupName "myResourceGroup" -Name "myServer" -Location West US -Sku D1 -Administrator "philipc@adventure-works.com"
```

## <a name="clean-up-resources"></a><span data-ttu-id="0f4f1-129">Limpar recursos</span><span class="sxs-lookup"><span data-stu-id="0f4f1-129">Clean up resources</span></span>

<span data-ttu-id="0f4f1-130">Você pode remover o servidor de saudação da sua assinatura usando Olá [AzureRmAnalysisServicesServer remover](/powershell/module/azurerm.analysisservices/new-azurermanalysisservicesserver) comando.</span><span class="sxs-lookup"><span data-stu-id="0f4f1-130">You can remove hello server from your subscription by using hello [Remove-AzureRmAnalysisServicesServer](/powershell/module/azurerm.analysisservices/new-azurermanalysisservicesserver) command.</span></span> <span data-ttu-id="0f4f1-131">Se você ainda for seguir outros guias de início rápido e tutoriais desta coleção, não remova o servidor.</span><span class="sxs-lookup"><span data-stu-id="0f4f1-131">If you continue with other quickstarts and tutorials in this collection, do not remove your server.</span></span> <span data-ttu-id="0f4f1-132">Olá, exemplo a seguir remove o servidor de saudação criado na etapa anterior Olá.</span><span class="sxs-lookup"><span data-stu-id="0f4f1-132">hello following example removes hello server created in hello previous step.</span></span>


```powershell
Remove-AzureRmAnalysisServicesServer -Name "myServer" -ResourceGroupName "myResourceGroup"
```

## <a name="next-steps"></a><span data-ttu-id="0f4f1-133">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="0f4f1-133">Next steps</span></span>
<span data-ttu-id="0f4f1-134">[Gerenciar o Azure Analysis Services com PowerShell](analysis-services-powershell.md) </span><span class="sxs-lookup"><span data-stu-id="0f4f1-134">[Manage Azure Analysis Services with PowerShell](analysis-services-powershell.md) </span></span>  
<span data-ttu-id="0f4f1-135">[Implantar um modelo a partir do SSDT](analysis-services-deploy.md) </span><span class="sxs-lookup"><span data-stu-id="0f4f1-135">[Deploy a model from SSDT](analysis-services-deploy.md) </span></span>  
[<span data-ttu-id="0f4f1-136">Criar um modelo no portal do Azure</span><span class="sxs-lookup"><span data-stu-id="0f4f1-136">Create a model in Azure portal</span></span>](analysis-services-create-model-portal.md)