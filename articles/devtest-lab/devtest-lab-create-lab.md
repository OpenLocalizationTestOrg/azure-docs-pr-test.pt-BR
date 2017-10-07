---
title: "aaaCreate um laboratório no Azure DevTest Labs | Microsoft Docs"
description: "Crie um laboratório no Azure DevTest Labs para máquinas virtuais"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 8b6d3e70-6528-42a4-a2ef-449575d0f928
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/30/2017
ms.author: tarcher
ms.openlocfilehash: 2ec5498f10e0cc06a196a71e319e340937abb1a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-lab-in-azure-devtest-labs"></a><span data-ttu-id="4ab69-103">Criar Laboratórios de Desenvolvimento/Teste do Azure</span><span class="sxs-lookup"><span data-stu-id="4ab69-103">Create a lab in Azure DevTest Labs</span></span>
<span data-ttu-id="4ab69-104">Um laboratório no Azure DevTest Labs é infraestrutura Olá que abrange um grupo de recursos, como máquinas virtuais (VMs), que lhe permite melhor gerenciar esses recursos, especificando limites e cotas.</span><span class="sxs-lookup"><span data-stu-id="4ab69-104">A lab in Azure DevTest Labs is hello infrastructure that encompasses a group of resources, such as Virtual Machines (VMs), that lets you better manage those resources by specifying limits and quotas.</span></span> <span data-ttu-id="4ab69-105">Este artigo orienta você pelo processo de saudação de criação de um laboratório com hello portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="4ab69-105">This article walks you through hello process of creating a lab using hello Azure portal.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4ab69-106">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="4ab69-106">Prerequisites</span></span>
<span data-ttu-id="4ab69-107">toocreate um laboratório, você precisa:</span><span class="sxs-lookup"><span data-stu-id="4ab69-107">toocreate a lab, you need:</span></span>

* <span data-ttu-id="4ab69-108">Uma assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="4ab69-108">An Azure subscription.</span></span> <span data-ttu-id="4ab69-109">toolearn sobre as opções de compra do Azure, consulte [como toobuy Azure](https://azure.microsoft.com/pricing/purchase-options/) ou [um mês avaliação gratuita](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="4ab69-109">toolearn about Azure purchase options, see [How toobuy Azure](https://azure.microsoft.com/pricing/purchase-options/) or [Free one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> <span data-ttu-id="4ab69-110">Você deve ser o proprietário de saudação do laboratório de Olá Olá assinatura toocreate.</span><span class="sxs-lookup"><span data-stu-id="4ab69-110">You must be hello owner of hello subscription toocreate hello lab.</span></span>

## <a name="steps-toocreate-a-lab-in-azure-devtest-labs"></a><span data-ttu-id="4ab69-111">Etapas toocreate um laboratório no Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="4ab69-111">Steps toocreate a lab in Azure DevTest Labs</span></span>
<span data-ttu-id="4ab69-112">Olá, as etapas a seguir ilustra como toouse Olá toocreate portal do Azure um laboratório no Azure DevTest Labs.</span><span class="sxs-lookup"><span data-stu-id="4ab69-112">hello following steps illustrate how toouse hello Azure portal toocreate a lab in Azure DevTest Labs.</span></span> 

1. <span data-ttu-id="4ab69-113">Entrar toohello [portal do Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="4ab69-113">Sign in toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
1. <span data-ttu-id="4ab69-114">No menu principal do hello no lado esquerdo do hello, selecione **mais serviços** (final Olá Olá lista).</span><span class="sxs-lookup"><span data-stu-id="4ab69-114">From hello main menu on hello left side, select **More Services** (at hello bottom of hello list).</span></span>

    ![Opção do menu Mais serviços](./media/devtest-lab-create-lab/more-services-menu-option.png)

1. <span data-ttu-id="4ab69-116">Na lista de saudação de serviços disponíveis, **DevTest Labs**.</span><span class="sxs-lookup"><span data-stu-id="4ab69-116">From hello list of available services, **DevTest Labs**.</span></span>
1. <span data-ttu-id="4ab69-117">Em Olá **DevTest Labs** folha, selecione **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="4ab69-117">On hello **DevTest Labs** blade, select **Add**.</span></span>
   
    ![Adicionar um laboratório](./media/devtest-lab-create-lab/add-lab-button.png)

1. <span data-ttu-id="4ab69-119">Em Olá **criar um laboratório de DevTest** folha:</span><span class="sxs-lookup"><span data-stu-id="4ab69-119">On hello **Create a DevTest Lab** blade:</span></span>
   
    1. <span data-ttu-id="4ab69-120">Insira um **nome do laboratório** laboratório novo hello.</span><span class="sxs-lookup"><span data-stu-id="4ab69-120">Enter a **Lab Name** for hello new lab.</span></span>
    2. <span data-ttu-id="4ab69-121">Selecione Olá **assinatura** tooassociate com laboratório hello.</span><span class="sxs-lookup"><span data-stu-id="4ab69-121">Select hello **Subscription** tooassociate with hello lab.</span></span>
    3. <span data-ttu-id="4ab69-122">Selecione um **local** no laboratório de saudação que toostore.</span><span class="sxs-lookup"><span data-stu-id="4ab69-122">Select a **Location** in which toostore hello lab.</span></span>
    4. <span data-ttu-id="4ab69-123">Selecione **desligamento automático** toospecify tooenable - e definir parâmetros de saudação para - Olá automáticas desligar do laboratório Olá todas as VMs.</span><span class="sxs-lookup"><span data-stu-id="4ab69-123">Select **Auto-shutdown** toospecify if you want tooenable - and define hello parameters for - hello automatic shutting down of all hello lab's VMs.</span></span> <span data-ttu-id="4ab69-124">Hello desligamento automático é principalmente uma economia de custo de recurso no qual você pode especificar quando deseja Olá VM tooautomatically ser desligada.</span><span class="sxs-lookup"><span data-stu-id="4ab69-124">hello auto-shutdown feature is mainly a cost-saving feature whereby you can specify when you want hello VM tooautomatically be shut down.</span></span> <span data-ttu-id="4ab69-125">Você pode alterar as configurações de desligamento automático depois de criar o laboratório Olá seguindo Olá etapas descritas no artigo Olá, [gerenciar todas as políticas para um laboratório no Azure DevTest Labs](./devtest-lab-set-lab-policy.md#set-auto-shutdown).</span><span class="sxs-lookup"><span data-stu-id="4ab69-125">You can change auto-shutdown settings after creating hello lab by following hello steps outlined in hello article, [Manage all policies for a lab in Azure DevTest Labs](./devtest-lab-set-lab-policy.md#set-auto-shutdown).</span></span>
    5. <span data-ttu-id="4ab69-126">Selecione **tooDashboard Pin** se você deseja um atalho de saudação laboratório tooappear no painel do portal hello.</span><span class="sxs-lookup"><span data-stu-id="4ab69-126">Select **Pin tooDashboard** if you want a shortcut of hello lab tooappear on hello portal dashboard.</span></span>
    6. <span data-ttu-id="4ab69-127">Selecione **opções de automação** tooget modelos de Gerenciador de recursos do Azure para a automação de configuração.</span><span class="sxs-lookup"><span data-stu-id="4ab69-127">Select **Automation options** tooget Azure Resource Manager templates for configuration automation.</span></span> 
    7. <span data-ttu-id="4ab69-128">Selecione **Criar**.</span><span class="sxs-lookup"><span data-stu-id="4ab69-128">Select **Create**.</span></span> <span data-ttu-id="4ab69-129">Depois de selecionar **criar**, Olá **DevTest Labs** exibe folha.</span><span class="sxs-lookup"><span data-stu-id="4ab69-129">After selecting **Create**, hello **DevTest Labs** blade displays.</span></span> <span data-ttu-id="4ab69-130">Você pode monitorar o status de saudação do processo de criação de laboratório Olá observando Olá **notificações** área.</span><span class="sxs-lookup"><span data-stu-id="4ab69-130">You can monitor hello status of hello lab creation process by watching hello **Notifications** area.</span></span> <span data-ttu-id="4ab69-131">Depois de concluído, atualize o laboratório do hello página toosee Olá recém-criado na lista de saudação de laboratórios.</span><span class="sxs-lookup"><span data-stu-id="4ab69-131">Once completed, refresh hello page toosee hello newly created lab in hello list of labs.</span></span>  
    
    ![Criar uma folha de laboratório](./media/devtest-lab-create-lab/create-devtestlab-blade.png)

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="next-steps"></a><span data-ttu-id="4ab69-133">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="4ab69-133">Next steps</span></span>
<span data-ttu-id="4ab69-134">Depois que você criou seu laboratório, aqui estão alguns próxima tooconsider de etapas:</span><span class="sxs-lookup"><span data-stu-id="4ab69-134">Once you've created your lab, here are some next steps tooconsider:</span></span>

* <span data-ttu-id="4ab69-135">[Laboratório de tooa acesso seguro](devtest-lab-add-devtest-user.md).</span><span class="sxs-lookup"><span data-stu-id="4ab69-135">[Secure access tooa lab](devtest-lab-add-devtest-user.md).</span></span>
* <span data-ttu-id="4ab69-136">[Definir políticas de laboratório](devtest-lab-set-lab-policy.md).</span><span class="sxs-lookup"><span data-stu-id="4ab69-136">[Set lab policies](devtest-lab-set-lab-policy.md).</span></span>
* <span data-ttu-id="4ab69-137">[Criar um modelo de laboratório](devtest-lab-create-template.md).</span><span class="sxs-lookup"><span data-stu-id="4ab69-137">[Create a lab template](devtest-lab-create-template.md).</span></span>
* <span data-ttu-id="4ab69-138">[Criar artefatos personalizados para suas VMs](devtest-lab-artifact-author.md).</span><span class="sxs-lookup"><span data-stu-id="4ab69-138">[Create custom artifacts for your VMs](devtest-lab-artifact-author.md).</span></span>
* <span data-ttu-id="4ab69-139">[Adicionar uma VM com o laboratório de tooa artefatos](https://azure.microsoft.com/resources/videos/how-to-create-vms-with-artifacts-in-a-devtest-lab/).</span><span class="sxs-lookup"><span data-stu-id="4ab69-139">[Add a VM with artifacts tooa lab](https://azure.microsoft.com/resources/videos/how-to-create-vms-with-artifacts-in-a-devtest-lab/).</span></span>

