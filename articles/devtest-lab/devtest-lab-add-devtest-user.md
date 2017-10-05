---
title: "Adicionar usuários e proprietários aos Azure DevTest Labs | Microsoft Docs"
description: "Adicionar usuários e proprietários aos Azure DevTest Labs usando o portal do Azure ou o PowerShell"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 4f51d9a5-2702-45f0-a2d5-a3635b58c416
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/11/2017
ms.author: tarcher
ms.openlocfilehash: d67fa257574d6cb4ad4b18521900374fb51da290
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="add-owners-and-users-in-azure-devtest-labs"></a><span data-ttu-id="594ac-103">Adicionar usuários e proprietários aos Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="594ac-103">Add owners and users in Azure DevTest Labs</span></span>
> [!VIDEO https://channel9.msdn.com/Blogs/Azure/How-to-set-security-in-your-DevTest-Lab/player]
> 
> 

<span data-ttu-id="594ac-104">O acesso a Azure DevTest Labs é controlado pelo [RBAC (Controle de Acesso Baseado em Função do Azure)](../active-directory/role-based-access-control-what-is.md).</span><span class="sxs-lookup"><span data-stu-id="594ac-104">Access in Azure DevTest Labs is controlled by [Azure Role-Based Access Control (RBAC)](../active-directory/role-based-access-control-what-is.md).</span></span> <span data-ttu-id="594ac-105">Com o RBAC, você pode separar as tarefas de sua equipe em *funções* , onde só concederá o acesso de que os usuários precisam para realizar seus trabalhos.</span><span class="sxs-lookup"><span data-stu-id="594ac-105">Using RBAC, you can segregate duties within your team into *roles* where you grant only the amount of access necessary to users to perform their jobs.</span></span> <span data-ttu-id="594ac-106">Três dessas funções RBAC são *Proprietário*, *Usuário dos DevTest Labs* e *Colaborador*.</span><span class="sxs-lookup"><span data-stu-id="594ac-106">Three of these RBAC roles are *Owner*, *DevTest Labs User*, and *Contributor*.</span></span> <span data-ttu-id="594ac-107">Neste artigo, você aprenderá quais ações podem ser executadas em cada uma das três funções RBAC principais.</span><span class="sxs-lookup"><span data-stu-id="594ac-107">In this article, you learn what actions can be performed in each of the three main RBAC roles.</span></span> <span data-ttu-id="594ac-108">A partir daí, você aprenderá como adicionar usuários a um laboratório - por meio do portal e por meio de um script do PowerShell, além de como adicionar usuários no nível de assinatura.</span><span class="sxs-lookup"><span data-stu-id="594ac-108">From there, you learn how to add users to a lab - both via the portal and via a PowerShell script, and how to add users at the subscription level.</span></span>

## <a name="actions-that-can-be-performed-in-each-role"></a><span data-ttu-id="594ac-109">Ações que podem ser executadas em cada função</span><span class="sxs-lookup"><span data-stu-id="594ac-109">Actions that can be performed in each role</span></span>
<span data-ttu-id="594ac-110">Há três funções principais às quais você pode atribuir um usuário:</span><span class="sxs-lookup"><span data-stu-id="594ac-110">There are three main roles that you can assign a user:</span></span>

* <span data-ttu-id="594ac-111">Proprietário</span><span class="sxs-lookup"><span data-stu-id="594ac-111">Owner</span></span>
* <span data-ttu-id="594ac-112">Usuário do DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="594ac-112">DevTest Labs User</span></span>
* <span data-ttu-id="594ac-113">Colaborador</span><span class="sxs-lookup"><span data-stu-id="594ac-113">Contributor</span></span>

<span data-ttu-id="594ac-114">A tabela a seguir ilustra as ações que podem ser executadas por usuários em cada uma dessas funções:</span><span class="sxs-lookup"><span data-stu-id="594ac-114">The following table illustrates the actions that can be performed by users in each of these roles:</span></span>

| <span data-ttu-id="594ac-115">**Ações que os usuários nesta função podem executar**</span><span class="sxs-lookup"><span data-stu-id="594ac-115">**Actions users in this role can perform**</span></span> | <span data-ttu-id="594ac-116">**Usuário do DevTest Labs**</span><span class="sxs-lookup"><span data-stu-id="594ac-116">**DevTest Labs User**</span></span> | <span data-ttu-id="594ac-117">**Proprietário**</span><span class="sxs-lookup"><span data-stu-id="594ac-117">**Owner**</span></span> | <span data-ttu-id="594ac-118">**Colaborador**</span><span class="sxs-lookup"><span data-stu-id="594ac-118">**Contributor**</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="594ac-119">**Tarefas do laboratório**</span><span class="sxs-lookup"><span data-stu-id="594ac-119">**Lab tasks**</span></span> | | | |
| <span data-ttu-id="594ac-120">Adicionar usuários a um laboratório</span><span class="sxs-lookup"><span data-stu-id="594ac-120">Add users to a lab</span></span> |<span data-ttu-id="594ac-121">Não</span><span class="sxs-lookup"><span data-stu-id="594ac-121">No</span></span> |<span data-ttu-id="594ac-122">Sim</span><span class="sxs-lookup"><span data-stu-id="594ac-122">Yes</span></span> |<span data-ttu-id="594ac-123">Não</span><span class="sxs-lookup"><span data-stu-id="594ac-123">No</span></span> |
| <span data-ttu-id="594ac-124">Atualizar configurações de custo</span><span class="sxs-lookup"><span data-stu-id="594ac-124">Update cost settings</span></span> |<span data-ttu-id="594ac-125">Não</span><span class="sxs-lookup"><span data-stu-id="594ac-125">No</span></span> |<span data-ttu-id="594ac-126">Sim</span><span class="sxs-lookup"><span data-stu-id="594ac-126">Yes</span></span> |<span data-ttu-id="594ac-127">Sim</span><span class="sxs-lookup"><span data-stu-id="594ac-127">Yes</span></span> |
| <span data-ttu-id="594ac-128">**Tarefas de base da VM**</span><span class="sxs-lookup"><span data-stu-id="594ac-128">**VM base tasks**</span></span> | | | |
| <span data-ttu-id="594ac-129">Adicionar e remover imagens personalizadas</span><span class="sxs-lookup"><span data-stu-id="594ac-129">Add and remove custom images</span></span> |<span data-ttu-id="594ac-130">Não</span><span class="sxs-lookup"><span data-stu-id="594ac-130">No</span></span> |<span data-ttu-id="594ac-131">Sim</span><span class="sxs-lookup"><span data-stu-id="594ac-131">Yes</span></span> |<span data-ttu-id="594ac-132">Sim</span><span class="sxs-lookup"><span data-stu-id="594ac-132">Yes</span></span> |
| <span data-ttu-id="594ac-133">Adicionar, atualizar e excluir fórmulas</span><span class="sxs-lookup"><span data-stu-id="594ac-133">Add, update, and delete formulas</span></span> |<span data-ttu-id="594ac-134">Sim</span><span class="sxs-lookup"><span data-stu-id="594ac-134">Yes</span></span> |<span data-ttu-id="594ac-135">Sim</span><span class="sxs-lookup"><span data-stu-id="594ac-135">Yes</span></span> |<span data-ttu-id="594ac-136">Sim</span><span class="sxs-lookup"><span data-stu-id="594ac-136">Yes</span></span> |
| <span data-ttu-id="594ac-137">Incluir imagens do Azure Marketplace na listra branca</span><span class="sxs-lookup"><span data-stu-id="594ac-137">Whitelist Azure Marketplace images</span></span> |<span data-ttu-id="594ac-138">Não</span><span class="sxs-lookup"><span data-stu-id="594ac-138">No</span></span> |<span data-ttu-id="594ac-139">Sim</span><span class="sxs-lookup"><span data-stu-id="594ac-139">Yes</span></span> |<span data-ttu-id="594ac-140">Sim</span><span class="sxs-lookup"><span data-stu-id="594ac-140">Yes</span></span> |
| <span data-ttu-id="594ac-141">**Tarefas da VM**</span><span class="sxs-lookup"><span data-stu-id="594ac-141">**VM tasks**</span></span> | | | |
| <span data-ttu-id="594ac-142">Criar VMs</span><span class="sxs-lookup"><span data-stu-id="594ac-142">Create VMs</span></span> |<span data-ttu-id="594ac-143">Sim</span><span class="sxs-lookup"><span data-stu-id="594ac-143">Yes</span></span> |<span data-ttu-id="594ac-144">Sim</span><span class="sxs-lookup"><span data-stu-id="594ac-144">Yes</span></span> |<span data-ttu-id="594ac-145">Sim</span><span class="sxs-lookup"><span data-stu-id="594ac-145">Yes</span></span> |
| <span data-ttu-id="594ac-146">Iniciar, parar e excluir VMs</span><span class="sxs-lookup"><span data-stu-id="594ac-146">Start, stop, and delete VMs</span></span> |<span data-ttu-id="594ac-147">Somente máquinas virtuais criadas pelo usuário</span><span class="sxs-lookup"><span data-stu-id="594ac-147">Only VMs created by the user</span></span> |<span data-ttu-id="594ac-148">Sim</span><span class="sxs-lookup"><span data-stu-id="594ac-148">Yes</span></span> |<span data-ttu-id="594ac-149">Sim</span><span class="sxs-lookup"><span data-stu-id="594ac-149">Yes</span></span> |
| <span data-ttu-id="594ac-150">Atualizar políticas de VM</span><span class="sxs-lookup"><span data-stu-id="594ac-150">Update VM policies</span></span> |<span data-ttu-id="594ac-151">Não</span><span class="sxs-lookup"><span data-stu-id="594ac-151">No</span></span> |<span data-ttu-id="594ac-152">Sim</span><span class="sxs-lookup"><span data-stu-id="594ac-152">Yes</span></span> |<span data-ttu-id="594ac-153">Sim</span><span class="sxs-lookup"><span data-stu-id="594ac-153">Yes</span></span> |
| <span data-ttu-id="594ac-154">Adicionar/remover discos de dados de/para máquinas virtuais</span><span class="sxs-lookup"><span data-stu-id="594ac-154">Add/remove data disks to/from VMs</span></span> |<span data-ttu-id="594ac-155">Somente máquinas virtuais criadas pelo usuário</span><span class="sxs-lookup"><span data-stu-id="594ac-155">Only VMs created by the user</span></span> |<span data-ttu-id="594ac-156">Sim</span><span class="sxs-lookup"><span data-stu-id="594ac-156">Yes</span></span> |<span data-ttu-id="594ac-157">Sim</span><span class="sxs-lookup"><span data-stu-id="594ac-157">Yes</span></span> |
| <span data-ttu-id="594ac-158">**Tarefas de artefato**</span><span class="sxs-lookup"><span data-stu-id="594ac-158">**Artifact tasks**</span></span> | | | |
| <span data-ttu-id="594ac-159">Adicionar e remover repositórios de artefato</span><span class="sxs-lookup"><span data-stu-id="594ac-159">Add and remove artifact repositories</span></span> |<span data-ttu-id="594ac-160">Não</span><span class="sxs-lookup"><span data-stu-id="594ac-160">No</span></span> |<span data-ttu-id="594ac-161">Sim</span><span class="sxs-lookup"><span data-stu-id="594ac-161">Yes</span></span> |<span data-ttu-id="594ac-162">Sim</span><span class="sxs-lookup"><span data-stu-id="594ac-162">Yes</span></span> |
| <span data-ttu-id="594ac-163">Aplicar artefatos</span><span class="sxs-lookup"><span data-stu-id="594ac-163">Apply artifacts</span></span> |<span data-ttu-id="594ac-164">Sim</span><span class="sxs-lookup"><span data-stu-id="594ac-164">Yes</span></span> |<span data-ttu-id="594ac-165">Sim</span><span class="sxs-lookup"><span data-stu-id="594ac-165">Yes</span></span> |<span data-ttu-id="594ac-166">Sim</span><span class="sxs-lookup"><span data-stu-id="594ac-166">Yes</span></span> |

> [!NOTE]
> <span data-ttu-id="594ac-167">Quando um usuário cria uma VM, esse usuário é atribuído automaticamente à função **Proprietário** da VM criada.</span><span class="sxs-lookup"><span data-stu-id="594ac-167">When a user creates a VM, that user is automatically assigned to the **Owner** role of the created VM.</span></span>
> 
> 

## <a name="add-an-owner-or-user-at-the-lab-level"></a><span data-ttu-id="594ac-168">Adicionar um usuário ou proprietário no nível do laboratório</span><span class="sxs-lookup"><span data-stu-id="594ac-168">Add an owner or user at the lab level</span></span>
<span data-ttu-id="594ac-169">Os proprietários e os usuários podem ser adicionados no nível do laboratório por meio do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="594ac-169">Owners and users can be added at the lab level via the Azure portal.</span></span> <span data-ttu-id="594ac-170">Isso inclui usuários externos com uma [Conta da Microsoft (MSA)](devtest-lab-faq.md#what-is-a-microsoft-account)válida.</span><span class="sxs-lookup"><span data-stu-id="594ac-170">This includes external users with a valid [Microsoft account (MSA)](devtest-lab-faq.md#what-is-a-microsoft-account).</span></span>
<span data-ttu-id="594ac-171">As etapas a seguir vão orientá-lo durante o processo de adição de um proprietário ou de um usuário a um laboratório nos Azure DevTest Labs:</span><span class="sxs-lookup"><span data-stu-id="594ac-171">The following steps guide you through the process of adding an owner or user to a lab in Azure DevTest Labs:</span></span>

1. <span data-ttu-id="594ac-172">Entre no [Portal do Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="594ac-172">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
2. <span data-ttu-id="594ac-173">Selecione **Mais serviços** e selecione **Laboratórios de Desenvolvimento/Teste** na lista.</span><span class="sxs-lookup"><span data-stu-id="594ac-173">Select **More services**, and then select **DevTest Labs** from the list.</span></span>
3. <span data-ttu-id="594ac-174">Na lista de laboratórios, selecione o laboratório desejado.</span><span class="sxs-lookup"><span data-stu-id="594ac-174">From the list of labs, select the desired lab.</span></span>
4. <span data-ttu-id="594ac-175">Na folha do laboratório, selecione **Configuração**.</span><span class="sxs-lookup"><span data-stu-id="594ac-175">On the lab's blade, select **Configuration**.</span></span> 
5. <span data-ttu-id="594ac-176">Na folha **Configuração**, selecione **Usuários**.</span><span class="sxs-lookup"><span data-stu-id="594ac-176">On the **Configuration** blade, select **Users**.</span></span>
6. <span data-ttu-id="594ac-177">Na folha **Usuários**, selecione **+Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="594ac-177">On the **Users** blade, select **+Add**.</span></span>
   
    ![Adicionar usuário](./media/devtest-lab-add-devtest-user/devtest-users-blade.png)
7. <span data-ttu-id="594ac-179">Na folha **Selecionar uma função** , selecione a função desejada.</span><span class="sxs-lookup"><span data-stu-id="594ac-179">On the **Select a role** blade, select the desired role.</span></span> <span data-ttu-id="594ac-180">A seção [Ações que podem ser executadas em cada função](#actions-that-can-be-performed-in-each-role) lista as diversas ações que podem ser executadas por usuários nas funções Proprietário, Usuário de DevTest e Colaborador.</span><span class="sxs-lookup"><span data-stu-id="594ac-180">The section [Actions that can be performed in each role](#actions-that-can-be-performed-in-each-role) lists the various actions that can be performed by users in the Owner, DevTest User, and Contributor roles.</span></span>
8. <span data-ttu-id="594ac-181">Na folha **Adicionar usuários** , insira o endereço de email ou o nome do usuário que você deseja adicionar à função especificada.</span><span class="sxs-lookup"><span data-stu-id="594ac-181">On the **Add users** blade, enter the email address or name of the user you want to add in the role you specified.</span></span> <span data-ttu-id="594ac-182">Se o usuário não for encontrado, uma mensagem de erro explicará o problema.</span><span class="sxs-lookup"><span data-stu-id="594ac-182">If the user can't be found, an error message explains the issue.</span></span> <span data-ttu-id="594ac-183">Se o usuário for encontrado, esse usuário será listado e selecionado.</span><span class="sxs-lookup"><span data-stu-id="594ac-183">If the user is found, that user is listed and selected.</span></span> 
9. <span data-ttu-id="594ac-184">Selecione **Selecionar**.</span><span class="sxs-lookup"><span data-stu-id="594ac-184">Select **Select**.</span></span>
10. <span data-ttu-id="594ac-185">Selecione **OK** para fechar a folha **Adicionar acesso**.</span><span class="sxs-lookup"><span data-stu-id="594ac-185">Select **OK** to close the **Add access** blade.</span></span>
11. <span data-ttu-id="594ac-186">Quando você retornar para a folha **Usuários** , o usuário terá sido adicionado.</span><span class="sxs-lookup"><span data-stu-id="594ac-186">When you return to the **Users** blade, the user has been added.</span></span>  

## <a name="add-an-external-user-to-a-lab-using-powershell"></a><span data-ttu-id="594ac-187">Adicionar um usuário externo a um laboratório usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="594ac-187">Add an external user to a lab using PowerShell</span></span>
<span data-ttu-id="594ac-188">Além de adicionar usuários no portal do Azure, você poderá adicionar um usuário externo ao seu laboratório usando um script do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="594ac-188">In addition to adding users in the Azure portal, you can add an external user to your lab using a PowerShell script.</span></span> <span data-ttu-id="594ac-189">No exemplo a seguir, apenas modifique os valores de parâmetro no comentário **Valores a alterar** .</span><span class="sxs-lookup"><span data-stu-id="594ac-189">In the following example, simply modify the parameter values under the **Values to change** comment.</span></span>
<span data-ttu-id="594ac-190">Você pode recuperar os valores `subscriptionId`, `labResourceGroup` e `labName` da folha do laboratório no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="594ac-190">You can retrieve the `subscriptionId`, `labResourceGroup`, and `labName` values from the lab blade in the Azure portal.</span></span>

> [!NOTE]
> <span data-ttu-id="594ac-191">O script de exemplo pressupõe que o usuário especificado tenha sido adicionado como um convidado ao Active Directory e falhará se não for o caso.</span><span class="sxs-lookup"><span data-stu-id="594ac-191">The sample script assumes that the specified user has been added as a guest to the Active Directory, and will fail if that is not the case.</span></span> <span data-ttu-id="594ac-192">Para adicionar um usuário que não esteja no Active Directory a um laboratório, use o portal do Azure para atribuir o usuário a uma função conforme ilustrado na seção [Adicionar um proprietário ou usuário no nível do laboratório](#add-an-owner-or-user-at-the-lab-level).</span><span class="sxs-lookup"><span data-stu-id="594ac-192">To add a user not in the Active Directory to a lab, use the Azure portal to assign the user to a role as illustrated in the section, [Add an owner or user at the lab level](#add-an-owner-or-user-at-the-lab-level).</span></span>   
> 
> 

    # Add an external user in DevTest Labs user role to a lab
    # Ensure that guest users can be added to the Azure Active directory:
    # https://azure.microsoft.com/en-us/documentation/articles/active-directory-create-users/#set-guest-user-access-policies

    # Values to change
    $subscriptionId = "<Enter Azure subscription ID here>"
    $labResourceGroup = "<Enter lab's resource name here>"
    $labName = "<Enter lab name here>"
    $userDisplayName = "<Enter user's display name here>"

    # Log into your Azure account
    Login-AzureRmAccount

    # Select the Azure subscription that contains the lab. 
    # This step is optional if you have only one subscription.
    Select-AzureRmSubscription -SubscriptionId $subscriptionId

    # Retrieve the user object
    $adObject = Get-AzureRmADUser -SearchString $userDisplayName

    # Create the role assignment. 
    $labId = ('subscriptions/' + $subscriptionId + '/resourceGroups/' + $labResourceGroup + '/providers/Microsoft.DevTestLab/labs/' + $labName)
    New-AzureRmRoleAssignment -ObjectId $adObject.Id -RoleDefinitionName 'DevTest Labs User' -Scope $labId

## <a name="add-an-owner-or-user-at-the-subscription-level"></a><span data-ttu-id="594ac-193">Adicionar um usuário ou proprietário no nível da assinatura</span><span class="sxs-lookup"><span data-stu-id="594ac-193">Add an owner or user at the subscription level</span></span>
<span data-ttu-id="594ac-194">As permissões do Azure são propagadas do escopo pai para o escopo filho no Azure.</span><span class="sxs-lookup"><span data-stu-id="594ac-194">Azure permissions are propagated from parent scope to child scope in Azure.</span></span> <span data-ttu-id="594ac-195">Portanto, os proprietários de uma assinatura do Azure que contenha laboratórios automaticamente serão proprietários desses laboratórios.</span><span class="sxs-lookup"><span data-stu-id="594ac-195">Therefore, owners of an Azure subscription that contains labs are automatically owners of those labs.</span></span> <span data-ttu-id="594ac-196">Eles também possuem as máquinas virtuais e outros recursos criados por usuários do laboratório, além do serviço Azure DevTest Labs.</span><span class="sxs-lookup"><span data-stu-id="594ac-196">They also own the VMs and other resources created by the lab's users, and the Azure DevTest Labs service.</span></span> 

<span data-ttu-id="594ac-197">Você pode adicionar outros proprietários a um laboratório por meio da folha do laboratório no [Portal do Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="594ac-197">You can add additional owners to a lab via the lab's blade in the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span> <span data-ttu-id="594ac-198">No entanto, o escopo de administração do proprietário adicionado é mais restrito do que o do proprietário da assinatura.</span><span class="sxs-lookup"><span data-stu-id="594ac-198">However, the added owner's scope of administration is more narrow than the subscription owner's scope.</span></span> <span data-ttu-id="594ac-199">Por exemplo, os proprietários adicionados não têm acesso total a alguns dos recursos criados na assinatura pelo serviço DevTest Labs.</span><span class="sxs-lookup"><span data-stu-id="594ac-199">For example, the added owners do not have full access to some of the resources that are created in the subscription by the DevTest Labs service.</span></span> 

<span data-ttu-id="594ac-200">Para adicionar um proprietário a uma assinatura do Azure, siga estas etapas:</span><span class="sxs-lookup"><span data-stu-id="594ac-200">To add an owner to an Azure subscription, follow these steps:</span></span>

1. <span data-ttu-id="594ac-201">Entre no [Portal do Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="594ac-201">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
2. <span data-ttu-id="594ac-202">Selecione **Mais Serviços** e selecione **Assinaturas na lista**.</span><span class="sxs-lookup"><span data-stu-id="594ac-202">Select **More Services**, and then select **Subscriptions** from the list.</span></span>
3. <span data-ttu-id="594ac-203">Selecione a assinatura desejada.</span><span class="sxs-lookup"><span data-stu-id="594ac-203">Select the desired subscription.</span></span>
4. <span data-ttu-id="594ac-204">Selecione o ícone **Acesso** .</span><span class="sxs-lookup"><span data-stu-id="594ac-204">Select **Access** icon.</span></span> 
   
    ![Usuários do Access](./media/devtest-lab-add-devtest-user/access-users.png)
5. <span data-ttu-id="594ac-206">Na folha **Usuários**, selecione **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="594ac-206">On the **Users** blade, select **Add**.</span></span>
   
    ![Adicionar usuário](./media/devtest-lab-add-devtest-user/devtest-users-blade.png)
6. <span data-ttu-id="594ac-208">Na folha **Selecionar uma função**, selecione **Proprietário**.</span><span class="sxs-lookup"><span data-stu-id="594ac-208">On the **Select a role** blade, select **Owner**.</span></span>
7. <span data-ttu-id="594ac-209">Na folha **Adicionar usuários** , insira o endereço de email ou o nome do usuário que deseja adicionar como um proprietário.</span><span class="sxs-lookup"><span data-stu-id="594ac-209">On the **Add users** blade, enter the email address or name of the user you want to add as an owner.</span></span> <span data-ttu-id="594ac-210">Se não for possível encontrar o usuário, você obterá uma mensagem de erro explicando o problema.</span><span class="sxs-lookup"><span data-stu-id="594ac-210">If the user can't be found, you get an error message explaining the issue.</span></span> <span data-ttu-id="594ac-211">Se o usuário for encontrado, ele será listado na caixa de texto **Usuário** .</span><span class="sxs-lookup"><span data-stu-id="594ac-211">If the user is found, that user is listed under the **User** text box.</span></span>
8. <span data-ttu-id="594ac-212">Selecione o nome de usuário localizado.</span><span class="sxs-lookup"><span data-stu-id="594ac-212">Select the located user name.</span></span>
9. <span data-ttu-id="594ac-213">Selecione **Selecionar**.</span><span class="sxs-lookup"><span data-stu-id="594ac-213">Select **Select**.</span></span>
10. <span data-ttu-id="594ac-214">Selecione **OK** para fechar a folha **Adicionar acesso**.</span><span class="sxs-lookup"><span data-stu-id="594ac-214">Select **OK** to close the **Add access** blade.</span></span>
11. <span data-ttu-id="594ac-215">Quando você retornar à folha **Usuários** , o usuário terá sido adicionado como proprietário.</span><span class="sxs-lookup"><span data-stu-id="594ac-215">When you return to the **Users** blade, the user has been added as an owner.</span></span> <span data-ttu-id="594ac-216">Agora, esse usuário é o proprietário de todos os laboratórios criados nessa assinatura e, portanto, é capaz de executar tarefas de proprietário.</span><span class="sxs-lookup"><span data-stu-id="594ac-216">This user is now an owner of any labs created under this subscription, and thus be able to perform owner tasks.</span></span> 

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

