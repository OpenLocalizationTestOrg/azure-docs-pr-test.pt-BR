---
title: "aaaUpdate Azure módulos na automação do Azure | Microsoft Docs"
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
ms.openlocfilehash: afa404a643349f044e55be2280e435b575049dec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooupdate-azure-powershell-modules-in-azure-automation"></a><span data-ttu-id="be8e7-103">Como módulos do PowerShell do Azure tooupdate na automação do Azure</span><span class="sxs-lookup"><span data-stu-id="be8e7-103">How tooupdate Azure PowerShell modules in Azure Automation</span></span>

<span data-ttu-id="be8e7-104">módulos do PowerShell do Azure mais comuns Olá são fornecidos por padrão em cada conta de automação.</span><span class="sxs-lookup"><span data-stu-id="be8e7-104">hello most common Azure PowerShell modules are provided by default in each Automation account.</span></span>  <span data-ttu-id="be8e7-105">atualizações de equipe do Azure Olá Olá regularmente, módulos do Azure para Olá conta de automação fornecemos uma maneira para você tooupdate módulos Olá conta hello quando novas versões estão disponíveis no portal de saudação.</span><span class="sxs-lookup"><span data-stu-id="be8e7-105">hello Azure team updates hello Azure modules regularly, so in hello Automation account we provide a way for you tooupdate hello modules in hello account when new versions are available from hello portal.</span></span>  

<span data-ttu-id="be8e7-106">Porque módulos são atualizados regularmente por grupo de produtos hello, as alterações podem ocorrer com cmdlets de saudação incluído, que pode afetar negativamente seus runbooks dependendo do tipo de saudação de alteração, como renomear um parâmetro ou substituição de um cmdlet inteiramente.</span><span class="sxs-lookup"><span data-stu-id="be8e7-106">Because modules are updated regularly by hello product group, changes can occur with hello  included cmdlets, which may negatively impact your runbooks depending on hello type of change, such as renaming a parameter or deprecating a cmdlet entirely.</span></span> <span data-ttu-id="be8e7-107">tooavoid afetar seus runbooks e hello processos automatizar, é altamente recomendável que você deseja testa e valida antes de continuar.</span><span class="sxs-lookup"><span data-stu-id="be8e7-107">tooavoid impacting your runbooks and hello processes they automate, it is strongly recommended that you test and validate before proceeding.</span></span>  <span data-ttu-id="be8e7-108">Se você não tiver uma conta de automação dedicada destinada para essa finalidade, considere a criação de uma forma que você pode testar vários cenários diferentes e permutações durante o desenvolvimento de saudação de seus runbooks, em alterações de tooiterative de adição, como atualização Olá Módulos do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="be8e7-108">If you do not have a dedicated Automation account intended for this purpose, consider creating one so that you can test many different scenarios and permutations during hello development of your runbooks, in addition tooiterative changes such as updating hello PowerShell modules.</span></span>  <span data-ttu-id="be8e7-109">Depois que os resultados de saudação são validados e você aplicou as alterações necessárias, prosseguir com a coordenação de migração de saudação de todos os runbooks que necessária a modificação e executar atualização Olá conforme descrito abaixo em produção.</span><span class="sxs-lookup"><span data-stu-id="be8e7-109">After hello results are validated and you have applied any changes required, proceed with coordinating hello migration of any runbooks that required modification and perform hello update as described below in production.</span></span>     

## <a name="updating-azure-modules"></a><span data-ttu-id="be8e7-110">Atualizando os módulos do Azure</span><span class="sxs-lookup"><span data-stu-id="be8e7-110">Updating Azure Modules</span></span>

1. <span data-ttu-id="be8e7-111">Olá módulos folha da sua conta de automação é uma opção chamada **atualização Azure módulos**.</span><span class="sxs-lookup"><span data-stu-id="be8e7-111">In hello Modules blade of your Automation account there is an option called **Update Azure Modules**.</span></span>  <span data-ttu-id="be8e7-112">Ela está sempre habilitada.</span><span class="sxs-lookup"><span data-stu-id="be8e7-112">It is always enabled.</span></span><br><br> <span data-ttu-id="be8e7-113">![Opção Atualizar Módulos do Azure na folha Módulos](media/automation-update-azure-modules/automation-update-azure-modules-option.png)</span><span class="sxs-lookup"><span data-stu-id="be8e7-113">![Update Azure Modules option in Modules blade](media/automation-update-azure-modules/automation-update-azure-modules-option.png)</span></span>

2. <span data-ttu-id="be8e7-114">Clique em **atualização Azure módulos** e você verá uma notificação de confirmação que pergunta se você quiser toocontinue.</span><span class="sxs-lookup"><span data-stu-id="be8e7-114">Click **Update Azure Modules** and you will be presented with a confirmation notification that asks you if you want toocontinue.</span></span><br><br> <span data-ttu-id="be8e7-115">![Notificação de Atualizar Módulos do Azure](media/automation-update-azure-modules/automation-update-azure-modules-popup.png)</span><span class="sxs-lookup"><span data-stu-id="be8e7-115">![Update Azure Modules notification](media/automation-update-azure-modules/automation-update-azure-modules-popup.png)</span></span>

3. <span data-ttu-id="be8e7-116">Clique em **Sim** e começará o processo de atualização de módulo hello.</span><span class="sxs-lookup"><span data-stu-id="be8e7-116">Click **Yes** and hello module update process will begin.</span></span>  <span data-ttu-id="be8e7-117">o processo de atualização Olá leva cerca de saudação do tooupdate 15 a 20 minutos seguintes módulos:</span><span class="sxs-lookup"><span data-stu-id="be8e7-117">hello update process takes about 15-20 minutes tooupdate hello following modules:</span></span>

  * <span data-ttu-id="be8e7-118">As tabelas</span><span class="sxs-lookup"><span data-stu-id="be8e7-118">Azure</span></span>
  * <span data-ttu-id="be8e7-119">Azure.Storage</span><span class="sxs-lookup"><span data-stu-id="be8e7-119">Azure.Storage</span></span>
  * <span data-ttu-id="be8e7-120">AzureRm.Automation</span><span class="sxs-lookup"><span data-stu-id="be8e7-120">AzureRm.Automation</span></span>
  * <span data-ttu-id="be8e7-121">AzureRm.Compute</span><span class="sxs-lookup"><span data-stu-id="be8e7-121">AzureRm.Compute</span></span>
  * <span data-ttu-id="be8e7-122">AzureRm.Profile</span><span class="sxs-lookup"><span data-stu-id="be8e7-122">AzureRm.Profile</span></span>
  * <span data-ttu-id="be8e7-123">AzureRm.Resources</span><span class="sxs-lookup"><span data-stu-id="be8e7-123">AzureRm.Resources</span></span>
  * <span data-ttu-id="be8e7-124">AzureRm.Sql</span><span class="sxs-lookup"><span data-stu-id="be8e7-124">AzureRm.Sql</span></span>
  * <span data-ttu-id="be8e7-125">AzureRm.Storage</span><span class="sxs-lookup"><span data-stu-id="be8e7-125">AzureRm.Storage</span></span>

    <span data-ttu-id="be8e7-126">Se os módulos de saudação já estão ativas toodate, processo Olá será concluída em alguns segundos.</span><span class="sxs-lookup"><span data-stu-id="be8e7-126">If hello modules are already up toodate, then hello process will complete in a few seconds.</span></span>  <span data-ttu-id="be8e7-127">Quando o processo de atualização de saudação for concluído, você será notificado.</span><span class="sxs-lookup"><span data-stu-id="be8e7-127">When hello update process completes you will be notified.</span></span><br><br> ![Status da atualização de Atualizar Módulos do Azure](media/automation-update-azure-modules/automation-update-azure-modules-updatestatus.png)

> [!NOTE]
> <span data-ttu-id="be8e7-129">Automação do Azure usará mais recentes de módulos Olá na sua conta de automação quando um novo trabalho agendado é executado.</span><span class="sxs-lookup"><span data-stu-id="be8e7-129">Azure Automation will use hello latest modules in your Automation account when a new scheduled job is run.</span></span>    

<span data-ttu-id="be8e7-130">Se você usar os cmdlets desses módulos do PowerShell do Azure no seu toomanage runbooks do Azure recursos, em seguida, você desejará tooperform esse processo de atualização de cada mês ou então tooassure tiver Olá módulos mais recentes.</span><span class="sxs-lookup"><span data-stu-id="be8e7-130">If you use cmdlets from these Azure PowerShell modules in your runbooks toomanage Azure resources, then you will want tooperform this update process every month or so tooassure that you have hello latest modules.</span></span>

## <a name="next-steps"></a><span data-ttu-id="be8e7-131">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="be8e7-131">Next steps</span></span>

* <span data-ttu-id="be8e7-132">toolearn mais informações sobre os módulos de integração e como toocreate módulos personalizados toofurther integrar a automação com outros sistemas, serviços ou soluções, consulte [módulos de integração](automation-integration-modules.md).</span><span class="sxs-lookup"><span data-stu-id="be8e7-132">toolearn more about Integration Modules and how toocreate custom modules toofurther integrate Automation with other systems, services, or solutions, see [Integration Modules](automation-integration-modules.md).</span></span>

* <span data-ttu-id="be8e7-133">Considere a integração de controle de origem usando [GitHub corporativo](automation-scenario-source-control-integration-with-github-ent.md) ou [do Visual Studio Team Services](automation-scenario-source-control-integration-with-vsts.md) toocentrally gerenciar e controlar versões do seu portfólio de runbook e a configuração de automação.</span><span class="sxs-lookup"><span data-stu-id="be8e7-133">Consider source control integration using [GitHub Enterprise](automation-scenario-source-control-integration-with-github-ent.md) or [Visual Studio Team Services](automation-scenario-source-control-integration-with-vsts.md) toocentrally manage and control releases of your Automation runbook and configuration portfolio.</span></span>  
