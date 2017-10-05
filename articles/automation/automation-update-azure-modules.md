---
title: "Atualizar módulos do Azure na Automação do Azure | Microsoft Docs"
description: "Este artigo descreve como você pode atualizar módulos comuns do Azure PowerShell fornecidos por padrão na Automação do Azure."
services: automation
documentationcenter: 
author: MGoedtel
manager: carmonm
editor: tysonn
ms.assetid: 
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/13/2017
ms.author: magoedte
ms.openlocfilehash: ed8c97b642d406a05817ec6c67f31a1b4bce93b0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-update-azure-powershell-modules-in-azure-automation"></a><span data-ttu-id="bc6bf-103">Como atualizar módulos do Azure PowerShell na Automação do Azure</span><span class="sxs-lookup"><span data-stu-id="bc6bf-103">How to update Azure PowerShell modules in Azure Automation</span></span>

<span data-ttu-id="bc6bf-104">Os módulos mais comuns do Azure PowerShell são fornecidos por padrão em cada conta de Automação.</span><span class="sxs-lookup"><span data-stu-id="bc6bf-104">The most common Azure PowerShell modules are provided by default in each Automation account.</span></span>  <span data-ttu-id="bc6bf-105">A equipe do Azure atualiza os módulos do Azure regularmente, assim, na conta de Automação fornecemos uma maneira de atualizar os módulos na conta quando novas versões são disponibilizadas do portal.</span><span class="sxs-lookup"><span data-stu-id="bc6bf-105">The Azure team updates the Azure modules regularly, so in the Automation account we provide a way for you to update the modules in the account when new versions are available from the portal.</span></span>  

<span data-ttu-id="bc6bf-106">Uma vez que os módulos são atualizados regularmente pelo grupo de produtos, as alterações podem ocorrer com os cmdlets incluídos, o que pode afetar negativamente seus runbooks dependendo do tipo de alteração, como renomear um parâmetro ou descontinuar um cmdlet inteiramente.</span><span class="sxs-lookup"><span data-stu-id="bc6bf-106">Because modules are updated regularly by the product group, changes can occur with the  included cmdlets, which may negatively impact your runbooks depending on the type of change, such as renaming a parameter or deprecating a cmdlet entirely.</span></span> <span data-ttu-id="bc6bf-107">Para evitar impacto a seus runbooks e os processos que eles automatizam, é altamente recomendável testar e validar antes de continuar.</span><span class="sxs-lookup"><span data-stu-id="bc6bf-107">To avoid impacting your runbooks and the processes they automate, it is strongly recommended that you test and validate before proceeding.</span></span>  <span data-ttu-id="bc6bf-108">Se você não tiver uma conta de Automação dedicada destinada para essa finalidade, considere criar uma para que você possa testar vários cenários e permutações diferentes durante o desenvolvimento de seus runbooks, além das alterações iterativas, como atualizar os módulos do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="bc6bf-108">If you do not have a dedicated Automation account intended for this purpose, consider creating one so that you can test many different scenarios and permutations during the development of your runbooks, in addition to iterative changes such as updating the PowerShell modules.</span></span>  <span data-ttu-id="bc6bf-109">Depois que os resultados forem validados e você tiver aplicado as alterações necessárias, continue com a coordenação da migração de todos os runbooks que precisem de modificação e execute a atualização conforme descrito abaixo em produção.</span><span class="sxs-lookup"><span data-stu-id="bc6bf-109">After the results are validated and you have applied any changes required, proceed with coordinating the migration of any runbooks that required modification and perform the update as described below in production.</span></span>     

## <a name="updating-azure-modules"></a><span data-ttu-id="bc6bf-110">Atualizando os módulos do Azure</span><span class="sxs-lookup"><span data-stu-id="bc6bf-110">Updating Azure Modules</span></span>

1. <span data-ttu-id="bc6bf-111">Na folha Módulos da sua conta de Automação, há uma opção chamada **Atualizar Módulos do Azure**.</span><span class="sxs-lookup"><span data-stu-id="bc6bf-111">In the Modules blade of your Automation account there is an option called **Update Azure Modules**.</span></span>  <span data-ttu-id="bc6bf-112">Ela está sempre habilitada.</span><span class="sxs-lookup"><span data-stu-id="bc6bf-112">It is always enabled.</span></span><br><br> <span data-ttu-id="bc6bf-113">![Opção Atualizar Módulos do Azure na folha Módulos](media/automation-update-azure-modules/automation-update-azure-modules-option.png)</span><span class="sxs-lookup"><span data-stu-id="bc6bf-113">![Update Azure Modules option in Modules blade](media/automation-update-azure-modules/automation-update-azure-modules-option.png)</span></span>

2. <span data-ttu-id="bc6bf-114">Clique em **Atualizar Módulos do Azure** e você receberá uma notificação de confirmação que pergunta se deseja continuar.</span><span class="sxs-lookup"><span data-stu-id="bc6bf-114">Click **Update Azure Modules** and you will be presented with a confirmation notification that asks you if you want to continue.</span></span><br><br> <span data-ttu-id="bc6bf-115">![Notificação de Atualizar Módulos do Azure](media/automation-update-azure-modules/automation-update-azure-modules-popup.png)</span><span class="sxs-lookup"><span data-stu-id="bc6bf-115">![Update Azure Modules notification](media/automation-update-azure-modules/automation-update-azure-modules-popup.png)</span></span>

3. <span data-ttu-id="bc6bf-116">Clique em **Sim** e o processo de atualização do módulo será iniciado.</span><span class="sxs-lookup"><span data-stu-id="bc6bf-116">Click **Yes** and the module update process will begin.</span></span>  <span data-ttu-id="bc6bf-117">O processo de atualização leva aproximadamente de 15 a 20 minutos para atualizar os seguintes módulos:</span><span class="sxs-lookup"><span data-stu-id="bc6bf-117">The update process takes about 15-20 minutes to update the following modules:</span></span>

  * <span data-ttu-id="bc6bf-118">As tabelas</span><span class="sxs-lookup"><span data-stu-id="bc6bf-118">Azure</span></span>
  * <span data-ttu-id="bc6bf-119">Azure.Storage</span><span class="sxs-lookup"><span data-stu-id="bc6bf-119">Azure.Storage</span></span>
  * <span data-ttu-id="bc6bf-120">AzureRm.Automation</span><span class="sxs-lookup"><span data-stu-id="bc6bf-120">AzureRm.Automation</span></span>
  * <span data-ttu-id="bc6bf-121">AzureRm.Compute</span><span class="sxs-lookup"><span data-stu-id="bc6bf-121">AzureRm.Compute</span></span>
  * <span data-ttu-id="bc6bf-122">AzureRm.Profile</span><span class="sxs-lookup"><span data-stu-id="bc6bf-122">AzureRm.Profile</span></span>
  * <span data-ttu-id="bc6bf-123">AzureRm.Resources</span><span class="sxs-lookup"><span data-stu-id="bc6bf-123">AzureRm.Resources</span></span>
  * <span data-ttu-id="bc6bf-124">AzureRm.Sql</span><span class="sxs-lookup"><span data-stu-id="bc6bf-124">AzureRm.Sql</span></span>
  * <span data-ttu-id="bc6bf-125">AzureRm.Storage</span><span class="sxs-lookup"><span data-stu-id="bc6bf-125">AzureRm.Storage</span></span>

    <span data-ttu-id="bc6bf-126">Se os módulos já estiverem atualizados, o processo será concluído em alguns segundos.</span><span class="sxs-lookup"><span data-stu-id="bc6bf-126">If the modules are already up to date, then the process will complete in a few seconds.</span></span>  <span data-ttu-id="bc6bf-127">Quando o processo de atualização for concluído, você será notificado.</span><span class="sxs-lookup"><span data-stu-id="bc6bf-127">When the update process completes you will be notified.</span></span><br><br> ![Status da atualização de Atualizar Módulos do Azure](media/automation-update-azure-modules/automation-update-azure-modules-updatestatus.png)

> [!NOTE]
> <span data-ttu-id="bc6bf-129">A Automação do Azure usará os módulos mais recentes em sua conta de Automação quando um novo trabalho agendado for executado.</span><span class="sxs-lookup"><span data-stu-id="bc6bf-129">Azure Automation will use the latest modules in your Automation account when a new scheduled job is run.</span></span>    

<span data-ttu-id="bc6bf-130">Caso use cmdlets desses módulos do Azure PowerShell em seus runbooks para gerenciar recursos do Azure, convém executar esse processo de atualização todos os meses, ou quase, para garantir que você tenha os módulos mais recentes.</span><span class="sxs-lookup"><span data-stu-id="bc6bf-130">If you use cmdlets from these Azure PowerShell modules in your runbooks to manage Azure resources, then you will want to perform this update process every month or so to assure that you have the latest modules.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bc6bf-131">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="bc6bf-131">Next steps</span></span>

* <span data-ttu-id="bc6bf-132">Para saber mais sobre Módulos de Integração e como criar módulos personalizados para integrar a Automação a outros sistemas, serviços ou soluções, confira [Módulos de integração](automation-integration-modules.md).</span><span class="sxs-lookup"><span data-stu-id="bc6bf-132">To learn more about Integration Modules and how to create custom modules to further integrate Automation with other systems, services, or solutions, see [Integration Modules](automation-integration-modules.md).</span></span>

* <span data-ttu-id="bc6bf-133">Considere a integração de controle do código-fonte usando [GitHub Enterprise](automation-scenario-source-control-integration-with-github-ent.md) ou [Visual Studio Team Services](automation-scenario-source-control-integration-with-vsts.md) para gerenciar e controlar centralmente versões do seu portfólio de runbook e configuração de Automação.</span><span class="sxs-lookup"><span data-stu-id="bc6bf-133">Consider source control integration using [GitHub Enterprise](automation-scenario-source-control-integration-with-github-ent.md) or [Visual Studio Team Services](automation-scenario-source-control-integration-with-vsts.md) to centrally manage and control releases of your Automation runbook and configuration portfolio.</span></span>  