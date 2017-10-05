---
title: "Criar um laboratório no Azure DevTest Labs | Microsoft Docs"
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
ms.openlocfilehash: 265a968f902f53c7561c8c7e937f8eacfdb37167
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="create-a-lab-in-azure-devtest-labs"></a><span data-ttu-id="f77a9-103">Criar Laboratórios de Desenvolvimento/Teste do Azure</span><span class="sxs-lookup"><span data-stu-id="f77a9-103">Create a lab in Azure DevTest Labs</span></span>
<span data-ttu-id="f77a9-104">Um laboratório no Azure DevTest Labs é a infraestrutura que abrange um grupo de recursos, como Máquinas Virtuais (VMs), que permite gerenciar melhor esses recursos especificando limites e cotas.</span><span class="sxs-lookup"><span data-stu-id="f77a9-104">A lab in Azure DevTest Labs is the infrastructure that encompasses a group of resources, such as Virtual Machines (VMs), that lets you better manage those resources by specifying limits and quotas.</span></span> <span data-ttu-id="f77a9-105">Este artigo explica o processo de criação de um laboratório usando o portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="f77a9-105">This article walks you through the process of creating a lab using the Azure portal.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f77a9-106">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="f77a9-106">Prerequisites</span></span>
<span data-ttu-id="f77a9-107">Para criar um laboratório, você precisa de:</span><span class="sxs-lookup"><span data-stu-id="f77a9-107">To create a lab, you need:</span></span>

* <span data-ttu-id="f77a9-108">Uma assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="f77a9-108">An Azure subscription.</span></span> <span data-ttu-id="f77a9-109">Para saber mais sobre as opções de compra do Azure, consulte [Como comprar o Azure](https://azure.microsoft.com/pricing/purchase-options/) ou [Avaliação gratuita de um mês](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f77a9-109">To learn about Azure purchase options, see [How to buy Azure](https://azure.microsoft.com/pricing/purchase-options/) or [Free one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> <span data-ttu-id="f77a9-110">Você deve ser o proprietário da assinatura para criar o laboratório.</span><span class="sxs-lookup"><span data-stu-id="f77a9-110">You must be the owner of the subscription to create the lab.</span></span>

## <a name="steps-to-create-a-lab-in-azure-devtest-labs"></a><span data-ttu-id="f77a9-111">Etapas para criar um laboratório n o Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="f77a9-111">Steps to create a lab in Azure DevTest Labs</span></span>
<span data-ttu-id="f77a9-112">As etapas a seguir ilustram como usar o portal do Azure para criar um laboratório no Azure DevTest Labs.</span><span class="sxs-lookup"><span data-stu-id="f77a9-112">The following steps illustrate how to use the Azure portal to create a lab in Azure DevTest Labs.</span></span> 

1. <span data-ttu-id="f77a9-113">Entre no [Portal do Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="f77a9-113">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
1. <span data-ttu-id="f77a9-114">No menu principal à esquerda, selecione **Mais Serviços** (na parte inferior da lista).</span><span class="sxs-lookup"><span data-stu-id="f77a9-114">From the main menu on the left side, select **More Services** (at the bottom of the list).</span></span>

    ![Opção do menu Mais serviços](./media/devtest-lab-create-lab/more-services-menu-option.png)

1. <span data-ttu-id="f77a9-116">Na lista de serviços disponíveis, **DevTest Labs**.</span><span class="sxs-lookup"><span data-stu-id="f77a9-116">From the list of available services, **DevTest Labs**.</span></span>
1. <span data-ttu-id="f77a9-117">Na folha **Laboratórios de Desenvolvimento/Teste**, selecione **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="f77a9-117">On the **DevTest Labs** blade, select **Add**.</span></span>
   
    ![Adicionar um laboratório](./media/devtest-lab-create-lab/add-lab-button.png)

1. <span data-ttu-id="f77a9-119">Na folha **Criar um Laboratório de Desenvolvimento/Teste** :</span><span class="sxs-lookup"><span data-stu-id="f77a9-119">On the **Create a DevTest Lab** blade:</span></span>
   
    1. <span data-ttu-id="f77a9-120">Insira um **Nome do Laboratório** para o novo laboratório.</span><span class="sxs-lookup"><span data-stu-id="f77a9-120">Enter a **Lab Name** for the new lab.</span></span>
    2. <span data-ttu-id="f77a9-121">Selecione a **Assinatura** para associar ao laboratório.</span><span class="sxs-lookup"><span data-stu-id="f77a9-121">Select the **Subscription** to associate with the lab.</span></span>
    3. <span data-ttu-id="f77a9-122">Selecione um **Local** no qual o laboratório será armazenado.</span><span class="sxs-lookup"><span data-stu-id="f77a9-122">Select a **Location** in which to store the lab.</span></span>
    4. <span data-ttu-id="f77a9-123">Selecione **Desligamento Automático** para especificar se você deseja ativar e definir os parâmetros de desligamento automático de todas as VMs do laboratório.</span><span class="sxs-lookup"><span data-stu-id="f77a9-123">Select **Auto-shutdown** to specify if you want to enable - and define the parameters for - the automatic shutting down of all the lab's VMs.</span></span> <span data-ttu-id="f77a9-124">O recurso de autodesligamento é principalmente um recurso de economia de custos no qual você pode especificar quando deseja que a VM seja desligada automaticamente.</span><span class="sxs-lookup"><span data-stu-id="f77a9-124">The auto-shutdown feature is mainly a cost-saving feature whereby you can specify when you want the VM to automatically be shut down.</span></span> <span data-ttu-id="f77a9-125">Você pode alterar as configurações de autodesligamento após criar o laboratório seguindo as etapas descritas no artigo [Gerenciar todas as políticas de um laboratório no Azure DevTest Labs](./devtest-lab-set-lab-policy.md#set-auto-shutdown).</span><span class="sxs-lookup"><span data-stu-id="f77a9-125">You can change auto-shutdown settings after creating the lab by following the steps outlined in the article, [Manage all policies for a lab in Azure DevTest Labs](./devtest-lab-set-lab-policy.md#set-auto-shutdown).</span></span>
    5. <span data-ttu-id="f77a9-126">Selecione **Fixar no painel** se você deseja exibir um atalho do laboratório no painel do portal.</span><span class="sxs-lookup"><span data-stu-id="f77a9-126">Select **Pin to Dashboard** if you want a shortcut of the lab to appear on the portal dashboard.</span></span>
    6. <span data-ttu-id="f77a9-127">Selecione **Opções de automação** para obter modelos do Azure Resource Manager para automação da configuração.</span><span class="sxs-lookup"><span data-stu-id="f77a9-127">Select **Automation options** to get Azure Resource Manager templates for configuration automation.</span></span> 
    7. <span data-ttu-id="f77a9-128">Selecione **Criar**.</span><span class="sxs-lookup"><span data-stu-id="f77a9-128">Select **Create**.</span></span> <span data-ttu-id="f77a9-129">Depois de selecionar **Criar**, a folha **DevTest Labs** é exibida.</span><span class="sxs-lookup"><span data-stu-id="f77a9-129">After selecting **Create**, the **DevTest Labs** blade displays.</span></span> <span data-ttu-id="f77a9-130">Você pode monitorar o status do processo de criação do laboratório vendo a área **Notificações**.</span><span class="sxs-lookup"><span data-stu-id="f77a9-130">You can monitor the status of the lab creation process by watching the **Notifications** area.</span></span> <span data-ttu-id="f77a9-131">Depois de concluído, atualize a página para ver o laboratório recém-criado na lista de laboratórios.</span><span class="sxs-lookup"><span data-stu-id="f77a9-131">Once completed, refresh the page to see the newly created lab in the list of labs.</span></span>  
    
    ![Criar uma folha de laboratório](./media/devtest-lab-create-lab/create-devtestlab-blade.png)

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="next-steps"></a><span data-ttu-id="f77a9-133">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="f77a9-133">Next steps</span></span>
<span data-ttu-id="f77a9-134">Depois de criar seu laboratório, aqui estão algumas das próximas etapas a serem consideradas:</span><span class="sxs-lookup"><span data-stu-id="f77a9-134">Once you've created your lab, here are some next steps to consider:</span></span>

* <span data-ttu-id="f77a9-135">[Proteger o acesso a um laboratório](devtest-lab-add-devtest-user.md).</span><span class="sxs-lookup"><span data-stu-id="f77a9-135">[Secure access to a lab](devtest-lab-add-devtest-user.md).</span></span>
* <span data-ttu-id="f77a9-136">[Definir políticas de laboratório](devtest-lab-set-lab-policy.md).</span><span class="sxs-lookup"><span data-stu-id="f77a9-136">[Set lab policies](devtest-lab-set-lab-policy.md).</span></span>
* <span data-ttu-id="f77a9-137">[Criar um modelo de laboratório](devtest-lab-create-template.md).</span><span class="sxs-lookup"><span data-stu-id="f77a9-137">[Create a lab template](devtest-lab-create-template.md).</span></span>
* <span data-ttu-id="f77a9-138">[Criar artefatos personalizados para suas VMs](devtest-lab-artifact-author.md).</span><span class="sxs-lookup"><span data-stu-id="f77a9-138">[Create custom artifacts for your VMs](devtest-lab-artifact-author.md).</span></span>
* <span data-ttu-id="f77a9-139">[Adicionar uma VM com artefatos a um laboratório](https://azure.microsoft.com/resources/videos/how-to-create-vms-with-artifacts-in-a-devtest-lab/).</span><span class="sxs-lookup"><span data-stu-id="f77a9-139">[Add a VM with artifacts to a lab](https://azure.microsoft.com/resources/videos/how-to-create-vms-with-artifacts-in-a-devtest-lab/).</span></span>

