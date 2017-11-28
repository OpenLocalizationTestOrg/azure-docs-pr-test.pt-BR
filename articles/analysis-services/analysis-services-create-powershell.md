---
title: Criar um servidor do Azure Analysis Services usando PowerShell | Microsoft Docs
description: Saiba como criar a um servidor do Azure Analysis Services usando PowerShell
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
ms.openlocfilehash: cb42fd3ed51364cf478848cc51ebbb2f175e96d2
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="create-an-azure-analysis-services-server-by-using-powershell"></a><span data-ttu-id="bf08e-103">Criar a um servidor do Azure Analysis Services usando PowerShell</span><span class="sxs-lookup"><span data-stu-id="bf08e-103">Create an Azure Analysis Services server by using PowerShell</span></span>

<span data-ttu-id="bf08e-104">Este guia de início rápido descreve como usar o PowerShell em uma linha de comando para criar um servidor do Azure Analysis Services em um [grupo de recursos do Azure](../azure-resource-manager/resource-group-overview.md), em sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="bf08e-104">This quickstart describes using PowerShell from the command line to create an Azure Analysis Services server in an [Azure resource group](../azure-resource-manager/resource-group-overview.md) in your Azure subscription.</span></span>

<span data-ttu-id="bf08e-105">Esta tarefa exige o módulo do Azure PowerShell, versão 4.0 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="bf08e-105">This task requires Azure PowerShell module version 4.0 or later.</span></span> <span data-ttu-id="bf08e-106">Para saber qual é a versão, execute ` Get-Module -ListAvailable AzureRM`.</span><span class="sxs-lookup"><span data-stu-id="bf08e-106">To find the version, run ` Get-Module -ListAvailable AzureRM`.</span></span> <span data-ttu-id="bf08e-107">Para instalar ou atualizar, confira [Instalar o módulo do Azure PowerShell](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="bf08e-107">To install or upgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span> 

> [!NOTE]
> <span data-ttu-id="bf08e-108">Criar um servidor pode resultar em um novo serviço faturável.</span><span class="sxs-lookup"><span data-stu-id="bf08e-108">Creating a server might result in a new billable service.</span></span> <span data-ttu-id="bf08e-109">Para saber mais, veja [Preços do Analysis Services](https://azure.microsoft.com/pricing/details/analysis-services/).</span><span class="sxs-lookup"><span data-stu-id="bf08e-109">To learn more, see [Analysis Services pricing](https://azure.microsoft.com/pricing/details/analysis-services/).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bf08e-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="bf08e-110">Prerequisites</span></span>
<span data-ttu-id="bf08e-111">Para concluir este início rápido, você precisa de:</span><span class="sxs-lookup"><span data-stu-id="bf08e-111">To complete this quickstart, you need:</span></span>

* <span data-ttu-id="bf08e-112">**Assinatura do Azure**: visite a [Avaliação Gratuita do Azure](https://azure.microsoft.com/offers/ms-azr-0044p/) para criar uma conta.</span><span class="sxs-lookup"><span data-stu-id="bf08e-112">**Azure subscription**: Visit [Azure Free Trial](https://azure.microsoft.com/offers/ms-azr-0044p/) to create an account.</span></span>
* <span data-ttu-id="bf08e-113">**Azure Active Directory**: sua assinatura deve estar associada a um locatário do Azure Active Directory, e você precisa ter uma conta nesse diretório.</span><span class="sxs-lookup"><span data-stu-id="bf08e-113">**Azure Active Directory**: Your subscription must be associated with an Azure Active Directory tenant and you must have an account in that directory.</span></span> <span data-ttu-id="bf08e-114">Para obter mais informações, confira [Autenticação e permissões de usuário](analysis-services-manage-users.md).</span><span class="sxs-lookup"><span data-stu-id="bf08e-114">To learn more, see [Authentication and user permissions](analysis-services-manage-users.md).</span></span>

## <a name="import-azurermanalysisservices-module"></a><span data-ttu-id="bf08e-115">Importar o módulo AzureRm.AnalysisServices</span><span class="sxs-lookup"><span data-stu-id="bf08e-115">Import AzureRm.AnalysisServices module</span></span>
<span data-ttu-id="bf08e-116">Para criar um servidor em sua assinatura, use o módulo de componente [AzureRM.AnalysisServices](https://www.powershellgallery.com/packages/AzureRM.AnalysisServices).</span><span class="sxs-lookup"><span data-stu-id="bf08e-116">To create a server in your subscription, you use the [AzureRM.AnalysisServices](https://www.powershellgallery.com/packages/AzureRM.AnalysisServices)  component module.</span></span> <span data-ttu-id="bf08e-117">Carregar o módulo AzureRm.AnalysisServices em sua sessão do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="bf08e-117">Load the AzureRm.AnalysisServices module into your PowerShell session.</span></span>

```powershell
Import-Module AzureRM.AnalysisServices
```

## <a name="sign-in-to-azure"></a><span data-ttu-id="bf08e-118">Entrar no Azure</span><span class="sxs-lookup"><span data-stu-id="bf08e-118">Sign in to Azure</span></span>

<span data-ttu-id="bf08e-119">Entre em sua assinatura do Azure usando o comando [Add-AzureRmAccount](/powershell/module/azurerm.profile/add-azurermaccount).</span><span class="sxs-lookup"><span data-stu-id="bf08e-119">Sign in to your Azure subscription by using the [Add-AzureRmAccount](/powershell/module/azurerm.profile/add-azurermaccount) command.</span></span> <span data-ttu-id="bf08e-120">Siga as instruções na tela.</span><span class="sxs-lookup"><span data-stu-id="bf08e-120">Follow the on-screen directions.</span></span>

```powershell
Add-AzureRmAccount
```

## <a name="create-a-resource-group"></a><span data-ttu-id="bf08e-121">Criar um grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="bf08e-121">Create a resource group</span></span>
 
<span data-ttu-id="bf08e-122">Um [grupo de recursos do Azure](../azure-resource-manager/resource-group-overview.md) é um contêiner lógico no qual os recursos do Azure são implantados e gerenciados em grupo.</span><span class="sxs-lookup"><span data-stu-id="bf08e-122">An [Azure resource group](../azure-resource-manager/resource-group-overview.md) is a logical container where Azure resources are deployed and managed as a group.</span></span> <span data-ttu-id="bf08e-123">Quando você cria o servidor, precisa especificar um grupo de recursos em sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="bf08e-123">When you create your server, you must specify a resource group in your subscription.</span></span> <span data-ttu-id="bf08e-124">Se você ainda não tiver um grupo de recursos, crie um novo usando o comando [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span><span class="sxs-lookup"><span data-stu-id="bf08e-124">If you do not already have a resource group, you can create a new one by using the [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) command.</span></span> <span data-ttu-id="bf08e-125">O exemplo a seguir cria um grupo de recursos chamado `myResourceGroup` na região Oeste dos EUA.</span><span class="sxs-lookup"><span data-stu-id="bf08e-125">The following example creates a resource group named `myResourceGroup` in the West US region.</span></span>

```powershell
New-AzureRmResourceGroup -Name "myResourceGroup" -Location "West US"
```

## <a name="create-a-server"></a><span data-ttu-id="bf08e-126">Criar um servidor</span><span class="sxs-lookup"><span data-stu-id="bf08e-126">Create a server</span></span>

<span data-ttu-id="bf08e-127">Crie um novo servidor usando o comando [New-AzureRmAnalysisServicesServer](/powershell/module/azurerm.analysisservices/new-azurermanalysisservicesserver).</span><span class="sxs-lookup"><span data-stu-id="bf08e-127">Create a new server by using the [New-AzureRmAnalysisServicesServer](/powershell/module/azurerm.analysisservices/new-azurermanalysisservicesserver) command.</span></span> <span data-ttu-id="bf08e-128">O exemplo a seguir cria um servidor chamado myServer em myResourceGroup, na região Oeste dos EUA, na camada D1, e especifica philipc@adventureworks.com como administrador do servidor.</span><span class="sxs-lookup"><span data-stu-id="bf08e-128">The following example creates a server named myServer in myResourceGroup, in the West US region, at the D1 tier, and specifies philipc@adventureworks.com as a server administrator.</span></span>

```powershell
New-AzureRmAnalysisServicesServer -ResourceGroupName "myResourceGroup" -Name "myServer" -Location West US -Sku D1 -Administrator "philipc@adventure-works.com"
```

## <a name="clean-up-resources"></a><span data-ttu-id="bf08e-129">Limpar recursos</span><span class="sxs-lookup"><span data-stu-id="bf08e-129">Clean up resources</span></span>

<span data-ttu-id="bf08e-130">Você pode remover o servidor de sua assinatura usando o comando [Remove-AzureRmAnalysisServicesServer](/powershell/module/azurerm.analysisservices/new-azurermanalysisservicesserver).</span><span class="sxs-lookup"><span data-stu-id="bf08e-130">You can remove the server from your subscription by using the [Remove-AzureRmAnalysisServicesServer](/powershell/module/azurerm.analysisservices/new-azurermanalysisservicesserver) command.</span></span> <span data-ttu-id="bf08e-131">Se você ainda for seguir outros guias de início rápido e tutoriais desta coleção, não remova o servidor.</span><span class="sxs-lookup"><span data-stu-id="bf08e-131">If you continue with other quickstarts and tutorials in this collection, do not remove your server.</span></span> <span data-ttu-id="bf08e-132">O exemplo a seguir remove o servidor criado na etapa anterior.</span><span class="sxs-lookup"><span data-stu-id="bf08e-132">The following example removes the server created in the previous step.</span></span>


```powershell
Remove-AzureRmAnalysisServicesServer -Name "myServer" -ResourceGroupName "myResourceGroup"
```

## <a name="next-steps"></a><span data-ttu-id="bf08e-133">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="bf08e-133">Next steps</span></span>
<span data-ttu-id="bf08e-134">[Gerenciar o Azure Analysis Services com PowerShell](analysis-services-powershell.md) </span><span class="sxs-lookup"><span data-stu-id="bf08e-134">[Manage Azure Analysis Services with PowerShell](analysis-services-powershell.md) </span></span>  
<span data-ttu-id="bf08e-135">[Implantar um modelo a partir do SSDT](analysis-services-deploy.md) </span><span class="sxs-lookup"><span data-stu-id="bf08e-135">[Deploy a model from SSDT](analysis-services-deploy.md) </span></span>  
[<span data-ttu-id="bf08e-136">Criar um modelo no portal do Azure</span><span class="sxs-lookup"><span data-stu-id="bf08e-136">Create a model in Azure portal</span></span>](analysis-services-create-model-portal.md)