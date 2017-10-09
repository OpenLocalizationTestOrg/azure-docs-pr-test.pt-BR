---
title: "aaaAdd proprietários e usuários no Azure DevTest Labs | Microsoft Docs"
description: "Adicionar usuários e proprietários no Azure DevTest Labs usando Olá portal do Azure ou o PowerShell"
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
ms.openlocfilehash: 2a98f5fe1efbd7c23e0d97f58f47c37462aed3b6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="add-owners-and-users-in-azure-devtest-labs"></a><span data-ttu-id="3d669-103">Adicionar usuários e proprietários aos Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="3d669-103">Add owners and users in Azure DevTest Labs</span></span>
> [!VIDEO https://channel9.msdn.com/Blogs/Azure/How-to-set-security-in-your-DevTest-Lab/player]
> 
> 

<span data-ttu-id="3d669-104">O acesso a Azure DevTest Labs é controlado pelo [RBAC (Controle de Acesso Baseado em Função do Azure)](../active-directory/role-based-access-control-what-is.md).</span><span class="sxs-lookup"><span data-stu-id="3d669-104">Access in Azure DevTest Labs is controlled by [Azure Role-Based Access Control (RBAC)](../active-directory/role-based-access-control-what-is.md).</span></span> <span data-ttu-id="3d669-105">Usando o RBAC, você pode separar tarefas dentro de sua equipe em *funções* onde você conceder somente a quantidade Olá de acesso necessário toousers tooperform seus trabalhos.</span><span class="sxs-lookup"><span data-stu-id="3d669-105">Using RBAC, you can segregate duties within your team into *roles* where you grant only hello amount of access necessary toousers tooperform their jobs.</span></span> <span data-ttu-id="3d669-106">Três dessas funções RBAC são *Proprietário*, *Usuário dos DevTest Labs* e *Colaborador*.</span><span class="sxs-lookup"><span data-stu-id="3d669-106">Three of these RBAC roles are *Owner*, *DevTest Labs User*, and *Contributor*.</span></span> <span data-ttu-id="3d669-107">Neste artigo, você aprenderá quais ações podem ser executadas em cada um dos três principais funções RBAC hello.</span><span class="sxs-lookup"><span data-stu-id="3d669-107">In this article, you learn what actions can be performed in each of hello three main RBAC roles.</span></span> <span data-ttu-id="3d669-108">A partir daí, você aprenderá como laboratório de tooa de usuários tooadd - ambos via Olá portal e por meio de um script do PowerShell, e como os usuários tooadd Olá nível de assinatura.</span><span class="sxs-lookup"><span data-stu-id="3d669-108">From there, you learn how tooadd users tooa lab - both via hello portal and via a PowerShell script, and how tooadd users at hello subscription level.</span></span>

## <a name="actions-that-can-be-performed-in-each-role"></a><span data-ttu-id="3d669-109">Ações que podem ser executadas em cada função</span><span class="sxs-lookup"><span data-stu-id="3d669-109">Actions that can be performed in each role</span></span>
<span data-ttu-id="3d669-110">Há três funções principais às quais você pode atribuir um usuário:</span><span class="sxs-lookup"><span data-stu-id="3d669-110">There are three main roles that you can assign a user:</span></span>

* <span data-ttu-id="3d669-111">Proprietário</span><span class="sxs-lookup"><span data-stu-id="3d669-111">Owner</span></span>
* <span data-ttu-id="3d669-112">Usuário do DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="3d669-112">DevTest Labs User</span></span>
* <span data-ttu-id="3d669-113">Colaborador</span><span class="sxs-lookup"><span data-stu-id="3d669-113">Contributor</span></span>

<span data-ttu-id="3d669-114">Olá tabela a seguir ilustra as ações de saudação que podem ser executadas por usuários em cada uma dessas funções:</span><span class="sxs-lookup"><span data-stu-id="3d669-114">hello following table illustrates hello actions that can be performed by users in each of these roles:</span></span>

| <span data-ttu-id="3d669-115">**Ações que os usuários nesta função podem executar**</span><span class="sxs-lookup"><span data-stu-id="3d669-115">**Actions users in this role can perform**</span></span> | <span data-ttu-id="3d669-116">**Usuário do DevTest Labs**</span><span class="sxs-lookup"><span data-stu-id="3d669-116">**DevTest Labs User**</span></span> | <span data-ttu-id="3d669-117">**Proprietário**</span><span class="sxs-lookup"><span data-stu-id="3d669-117">**Owner**</span></span> | <span data-ttu-id="3d669-118">**Colaborador**</span><span class="sxs-lookup"><span data-stu-id="3d669-118">**Contributor**</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="3d669-119">**Tarefas do laboratório**</span><span class="sxs-lookup"><span data-stu-id="3d669-119">**Lab tasks**</span></span> | | | |
| <span data-ttu-id="3d669-120">Adicionar o laboratório de tooa de usuários</span><span class="sxs-lookup"><span data-stu-id="3d669-120">Add users tooa lab</span></span> |<span data-ttu-id="3d669-121">Não</span><span class="sxs-lookup"><span data-stu-id="3d669-121">No</span></span> |<span data-ttu-id="3d669-122">Sim</span><span class="sxs-lookup"><span data-stu-id="3d669-122">Yes</span></span> |<span data-ttu-id="3d669-123">Não</span><span class="sxs-lookup"><span data-stu-id="3d669-123">No</span></span> |
| <span data-ttu-id="3d669-124">Atualizar configurações de custo</span><span class="sxs-lookup"><span data-stu-id="3d669-124">Update cost settings</span></span> |<span data-ttu-id="3d669-125">Não</span><span class="sxs-lookup"><span data-stu-id="3d669-125">No</span></span> |<span data-ttu-id="3d669-126">Sim</span><span class="sxs-lookup"><span data-stu-id="3d669-126">Yes</span></span> |<span data-ttu-id="3d669-127">Sim</span><span class="sxs-lookup"><span data-stu-id="3d669-127">Yes</span></span> |
| <span data-ttu-id="3d669-128">**Tarefas de base da VM**</span><span class="sxs-lookup"><span data-stu-id="3d669-128">**VM base tasks**</span></span> | | | |
| <span data-ttu-id="3d669-129">Adicionar e remover imagens personalizadas</span><span class="sxs-lookup"><span data-stu-id="3d669-129">Add and remove custom images</span></span> |<span data-ttu-id="3d669-130">Não</span><span class="sxs-lookup"><span data-stu-id="3d669-130">No</span></span> |<span data-ttu-id="3d669-131">Sim</span><span class="sxs-lookup"><span data-stu-id="3d669-131">Yes</span></span> |<span data-ttu-id="3d669-132">Sim</span><span class="sxs-lookup"><span data-stu-id="3d669-132">Yes</span></span> |
| <span data-ttu-id="3d669-133">Adicionar, atualizar e excluir fórmulas</span><span class="sxs-lookup"><span data-stu-id="3d669-133">Add, update, and delete formulas</span></span> |<span data-ttu-id="3d669-134">Sim</span><span class="sxs-lookup"><span data-stu-id="3d669-134">Yes</span></span> |<span data-ttu-id="3d669-135">Sim</span><span class="sxs-lookup"><span data-stu-id="3d669-135">Yes</span></span> |<span data-ttu-id="3d669-136">Sim</span><span class="sxs-lookup"><span data-stu-id="3d669-136">Yes</span></span> |
| <span data-ttu-id="3d669-137">Incluir imagens do Azure Marketplace na listra branca</span><span class="sxs-lookup"><span data-stu-id="3d669-137">Whitelist Azure Marketplace images</span></span> |<span data-ttu-id="3d669-138">Não</span><span class="sxs-lookup"><span data-stu-id="3d669-138">No</span></span> |<span data-ttu-id="3d669-139">Sim</span><span class="sxs-lookup"><span data-stu-id="3d669-139">Yes</span></span> |<span data-ttu-id="3d669-140">Sim</span><span class="sxs-lookup"><span data-stu-id="3d669-140">Yes</span></span> |
| <span data-ttu-id="3d669-141">**Tarefas da VM**</span><span class="sxs-lookup"><span data-stu-id="3d669-141">**VM tasks**</span></span> | | | |
| <span data-ttu-id="3d669-142">Criar VMs</span><span class="sxs-lookup"><span data-stu-id="3d669-142">Create VMs</span></span> |<span data-ttu-id="3d669-143">Sim</span><span class="sxs-lookup"><span data-stu-id="3d669-143">Yes</span></span> |<span data-ttu-id="3d669-144">Sim</span><span class="sxs-lookup"><span data-stu-id="3d669-144">Yes</span></span> |<span data-ttu-id="3d669-145">Sim</span><span class="sxs-lookup"><span data-stu-id="3d669-145">Yes</span></span> |
| <span data-ttu-id="3d669-146">Iniciar, parar e excluir VMs</span><span class="sxs-lookup"><span data-stu-id="3d669-146">Start, stop, and delete VMs</span></span> |<span data-ttu-id="3d669-147">Somente máquinas virtuais criadas pelo usuário Olá</span><span class="sxs-lookup"><span data-stu-id="3d669-147">Only VMs created by hello user</span></span> |<span data-ttu-id="3d669-148">Sim</span><span class="sxs-lookup"><span data-stu-id="3d669-148">Yes</span></span> |<span data-ttu-id="3d669-149">Sim</span><span class="sxs-lookup"><span data-stu-id="3d669-149">Yes</span></span> |
| <span data-ttu-id="3d669-150">Atualizar políticas de VM</span><span class="sxs-lookup"><span data-stu-id="3d669-150">Update VM policies</span></span> |<span data-ttu-id="3d669-151">Não</span><span class="sxs-lookup"><span data-stu-id="3d669-151">No</span></span> |<span data-ttu-id="3d669-152">Sim</span><span class="sxs-lookup"><span data-stu-id="3d669-152">Yes</span></span> |<span data-ttu-id="3d669-153">Sim</span><span class="sxs-lookup"><span data-stu-id="3d669-153">Yes</span></span> |
| <span data-ttu-id="3d669-154">Adicionar/remover discos de dados de/para máquinas virtuais</span><span class="sxs-lookup"><span data-stu-id="3d669-154">Add/remove data disks to/from VMs</span></span> |<span data-ttu-id="3d669-155">Somente máquinas virtuais criadas pelo usuário Olá</span><span class="sxs-lookup"><span data-stu-id="3d669-155">Only VMs created by hello user</span></span> |<span data-ttu-id="3d669-156">Sim</span><span class="sxs-lookup"><span data-stu-id="3d669-156">Yes</span></span> |<span data-ttu-id="3d669-157">Sim</span><span class="sxs-lookup"><span data-stu-id="3d669-157">Yes</span></span> |
| <span data-ttu-id="3d669-158">**Tarefas de artefato**</span><span class="sxs-lookup"><span data-stu-id="3d669-158">**Artifact tasks**</span></span> | | | |
| <span data-ttu-id="3d669-159">Adicionar e remover repositórios de artefato</span><span class="sxs-lookup"><span data-stu-id="3d669-159">Add and remove artifact repositories</span></span> |<span data-ttu-id="3d669-160">Não</span><span class="sxs-lookup"><span data-stu-id="3d669-160">No</span></span> |<span data-ttu-id="3d669-161">Sim</span><span class="sxs-lookup"><span data-stu-id="3d669-161">Yes</span></span> |<span data-ttu-id="3d669-162">Sim</span><span class="sxs-lookup"><span data-stu-id="3d669-162">Yes</span></span> |
| <span data-ttu-id="3d669-163">Aplicar artefatos</span><span class="sxs-lookup"><span data-stu-id="3d669-163">Apply artifacts</span></span> |<span data-ttu-id="3d669-164">Sim</span><span class="sxs-lookup"><span data-stu-id="3d669-164">Yes</span></span> |<span data-ttu-id="3d669-165">Sim</span><span class="sxs-lookup"><span data-stu-id="3d669-165">Yes</span></span> |<span data-ttu-id="3d669-166">Sim</span><span class="sxs-lookup"><span data-stu-id="3d669-166">Yes</span></span> |

> [!NOTE]
> <span data-ttu-id="3d669-167">Quando um usuário cria uma máquina virtual, esse usuário é atribuído automaticamente toohello **proprietário** função da saudação criada VM.</span><span class="sxs-lookup"><span data-stu-id="3d669-167">When a user creates a VM, that user is automatically assigned toohello **Owner** role of hello created VM.</span></span>
> 
> 

## <a name="add-an-owner-or-user-at-hello-lab-level"></a><span data-ttu-id="3d669-168">Adicionar um proprietário ou usuário no nível de laboratório Olá</span><span class="sxs-lookup"><span data-stu-id="3d669-168">Add an owner or user at hello lab level</span></span>
<span data-ttu-id="3d669-169">Os proprietários e os usuários podem ser adicionados no nível de laboratório Olá via Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="3d669-169">Owners and users can be added at hello lab level via hello Azure portal.</span></span> <span data-ttu-id="3d669-170">Isso inclui usuários externos com uma [Conta da Microsoft (MSA)](devtest-lab-faq.md#what-is-a-microsoft-account)válida.</span><span class="sxs-lookup"><span data-stu-id="3d669-170">This includes external users with a valid [Microsoft account (MSA)](devtest-lab-faq.md#what-is-a-microsoft-account).</span></span>
<span data-ttu-id="3d669-171">Olá etapas a seguir orientam você por meio do processo de saudação de adição de um laboratório de tooa proprietário ou usuário no Azure DevTest Labs:</span><span class="sxs-lookup"><span data-stu-id="3d669-171">hello following steps guide you through hello process of adding an owner or user tooa lab in Azure DevTest Labs:</span></span>

1. <span data-ttu-id="3d669-172">Entrar toohello [portal do Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="3d669-172">Sign in toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
2. <span data-ttu-id="3d669-173">Selecione **mais serviços**e, em seguida, selecione **DevTest Labs** da lista de saudação.</span><span class="sxs-lookup"><span data-stu-id="3d669-173">Select **More services**, and then select **DevTest Labs** from hello list.</span></span>
3. <span data-ttu-id="3d669-174">Saudação de laboratórios, selecione lista laboratório desejado hello.</span><span class="sxs-lookup"><span data-stu-id="3d669-174">From hello list of labs, select hello desired lab.</span></span>
4. <span data-ttu-id="3d669-175">Na folha do laboratório hello, selecione **configuração**.</span><span class="sxs-lookup"><span data-stu-id="3d669-175">On hello lab's blade, select **Configuration**.</span></span> 
5. <span data-ttu-id="3d669-176">Em Olá **configuração** folha, selecione **usuários**.</span><span class="sxs-lookup"><span data-stu-id="3d669-176">On hello **Configuration** blade, select **Users**.</span></span>
6. <span data-ttu-id="3d669-177">Em Olá **usuários** folha, selecione **+ adicionar**.</span><span class="sxs-lookup"><span data-stu-id="3d669-177">On hello **Users** blade, select **+Add**.</span></span>
   
    ![Adicionar usuário](./media/devtest-lab-add-devtest-user/devtest-users-blade.png)
7. <span data-ttu-id="3d669-179">Em Olá **selecionar uma função** folha, função desejada Olá select.</span><span class="sxs-lookup"><span data-stu-id="3d669-179">On hello **Select a role** blade, select hello desired role.</span></span> <span data-ttu-id="3d669-180">Olá seção [ações que podem ser executadas em cada função](#actions-that-can-be-performed-in-each-role) listas Olá várias ações que podem ser executadas por usuários em funções de proprietário, usuário do DevTest e colaborador hello.</span><span class="sxs-lookup"><span data-stu-id="3d669-180">hello section [Actions that can be performed in each role](#actions-that-can-be-performed-in-each-role) lists hello various actions that can be performed by users in hello Owner, DevTest User, and Contributor roles.</span></span>
8. <span data-ttu-id="3d669-181">Em Olá **adicionar usuários** folha, insira o endereço de email de saudação ou nome de usuário de saudação desejado tooadd na função hello especificado.</span><span class="sxs-lookup"><span data-stu-id="3d669-181">On hello **Add users** blade, enter hello email address or name of hello user you want tooadd in hello role you specified.</span></span> <span data-ttu-id="3d669-182">Se o usuário Olá não for encontrado, uma mensagem de erro explica problema hello.</span><span class="sxs-lookup"><span data-stu-id="3d669-182">If hello user can't be found, an error message explains hello issue.</span></span> <span data-ttu-id="3d669-183">Se o usuário Olá for encontrado, esse usuário é listado e selecionado.</span><span class="sxs-lookup"><span data-stu-id="3d669-183">If hello user is found, that user is listed and selected.</span></span> 
9. <span data-ttu-id="3d669-184">Selecione **Selecionar**.</span><span class="sxs-lookup"><span data-stu-id="3d669-184">Select **Select**.</span></span>
10. <span data-ttu-id="3d669-185">Selecione **Okey** tooclose Olá **adicionar acesso** folha.</span><span class="sxs-lookup"><span data-stu-id="3d669-185">Select **OK** tooclose hello **Add access** blade.</span></span>
11. <span data-ttu-id="3d669-186">Ao retornar toohello **usuários** folha, Olá usuário foi adicionado.</span><span class="sxs-lookup"><span data-stu-id="3d669-186">When you return toohello **Users** blade, hello user has been added.</span></span>  

## <a name="add-an-external-user-tooa-lab-using-powershell"></a><span data-ttu-id="3d669-187">Adicionar um laboratório de tooa de usuário externo usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="3d669-187">Add an external user tooa lab using PowerShell</span></span>
<span data-ttu-id="3d669-188">Além disso tooadding usuários Olá portal do Azure, você pode adicionar um laboratório de tooyour de usuário externo usando um script do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3d669-188">In addition tooadding users in hello Azure portal, you can add an external user tooyour lab using a PowerShell script.</span></span> <span data-ttu-id="3d669-189">Olá seguinte exemplo, basta modificar Olá parâmetro valores em Olá **toochange valores** comentário.</span><span class="sxs-lookup"><span data-stu-id="3d669-189">In hello following example, simply modify hello parameter values under hello **Values toochange** comment.</span></span>
<span data-ttu-id="3d669-190">Você pode recuperar Olá `subscriptionId`, `labResourceGroup`, e `labName` valores na folha de laboratório Olá no hello portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="3d669-190">You can retrieve hello `subscriptionId`, `labResourceGroup`, and `labName` values from hello lab blade in hello Azure portal.</span></span>

> [!NOTE]
> <span data-ttu-id="3d669-191">script de exemplo Hello pressupõe que Olá especificado usuário foi adicionado como um toohello de convidado do Active Directory e irá falhar se não for o caso de saudação.</span><span class="sxs-lookup"><span data-stu-id="3d669-191">hello sample script assumes that hello specified user has been added as a guest toohello Active Directory, and will fail if that is not hello case.</span></span> <span data-ttu-id="3d669-192">tooadd um usuário não Olá laboratório de tooa do Active Directory, usar Olá tooassign portal do Azure Olá tooa função, conforme ilustrado na seção hello, [adicionar um proprietário ou usuário no nível de laboratório Olá](#add-an-owner-or-user-at-the-lab-level).</span><span class="sxs-lookup"><span data-stu-id="3d669-192">tooadd a user not in hello Active Directory tooa lab, use hello Azure portal tooassign hello user tooa role as illustrated in hello section, [Add an owner or user at hello lab level](#add-an-owner-or-user-at-the-lab-level).</span></span>   
> 
> 

    # Add an external user in DevTest Labs user role tooa lab
    # Ensure that guest users can be added toohello Azure Active directory:
    # https://azure.microsoft.com/en-us/documentation/articles/active-directory-create-users/#set-guest-user-access-policies

    # Values toochange
    $subscriptionId = "<Enter Azure subscription ID here>"
    $labResourceGroup = "<Enter lab's resource name here>"
    $labName = "<Enter lab name here>"
    $userDisplayName = "<Enter user's display name here>"

    # Log into your Azure account
    Login-AzureRmAccount

    # Select hello Azure subscription that contains hello lab. 
    # This step is optional if you have only one subscription.
    Select-AzureRmSubscription -SubscriptionId $subscriptionId

    # Retrieve hello user object
    $adObject = Get-AzureRmADUser -SearchString $userDisplayName

    # Create hello role assignment. 
    $labId = ('subscriptions/' + $subscriptionId + '/resourceGroups/' + $labResourceGroup + '/providers/Microsoft.DevTestLab/labs/' + $labName)
    New-AzureRmRoleAssignment -ObjectId $adObject.Id -RoleDefinitionName 'DevTest Labs User' -Scope $labId

## <a name="add-an-owner-or-user-at-hello-subscription-level"></a><span data-ttu-id="3d669-193">Adicionar um proprietário ou usuário no nível de assinatura de saudação</span><span class="sxs-lookup"><span data-stu-id="3d669-193">Add an owner or user at hello subscription level</span></span>
<span data-ttu-id="3d669-194">Permissões do Azure são propagadas do toochild escopo pai no Azure.</span><span class="sxs-lookup"><span data-stu-id="3d669-194">Azure permissions are propagated from parent scope toochild scope in Azure.</span></span> <span data-ttu-id="3d669-195">Portanto, os proprietários de uma assinatura do Azure que contenha laboratórios automaticamente serão proprietários desses laboratórios.</span><span class="sxs-lookup"><span data-stu-id="3d669-195">Therefore, owners of an Azure subscription that contains labs are automatically owners of those labs.</span></span> <span data-ttu-id="3d669-196">Eles também possuem Olá VMs e outros recursos criados por usuários do laboratório hello e Olá serviço Azure DevTest Labs.</span><span class="sxs-lookup"><span data-stu-id="3d669-196">They also own hello VMs and other resources created by hello lab's users, and hello Azure DevTest Labs service.</span></span> 

<span data-ttu-id="3d669-197">Você pode adicionar laboratório de tooa proprietários adicionais por meio de folha do laboratório Olá Olá [portal do Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="3d669-197">You can add additional owners tooa lab via hello lab's blade in hello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span> <span data-ttu-id="3d669-198">No entanto, Olá adicionada escopo do proprietário de administração é mais estreito que o escopo do proprietário da assinatura hello.</span><span class="sxs-lookup"><span data-stu-id="3d669-198">However, hello added owner's scope of administration is more narrow than hello subscription owner's scope.</span></span> <span data-ttu-id="3d669-199">Por exemplo, a saudação adicionado proprietários não têm acesso completo toosome de recursos de saudação que são criados na assinatura Olá por Olá serviço DevTest Labs.</span><span class="sxs-lookup"><span data-stu-id="3d669-199">For example, hello added owners do not have full access toosome of hello resources that are created in hello subscription by hello DevTest Labs service.</span></span> 

<span data-ttu-id="3d669-200">tooadd tooan um proprietário assinatura do Azure, siga estas etapas:</span><span class="sxs-lookup"><span data-stu-id="3d669-200">tooadd an owner tooan Azure subscription, follow these steps:</span></span>

1. <span data-ttu-id="3d669-201">Entrar toohello [portal do Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="3d669-201">Sign in toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
2. <span data-ttu-id="3d669-202">Selecione **mais serviços**e, em seguida, selecione **assinaturas** da lista de saudação.</span><span class="sxs-lookup"><span data-stu-id="3d669-202">Select **More Services**, and then select **Subscriptions** from hello list.</span></span>
3. <span data-ttu-id="3d669-203">Selecione a assinatura de saudação desejada.</span><span class="sxs-lookup"><span data-stu-id="3d669-203">Select hello desired subscription.</span></span>
4. <span data-ttu-id="3d669-204">Selecione o ícone **Acesso** .</span><span class="sxs-lookup"><span data-stu-id="3d669-204">Select **Access** icon.</span></span> 
   
    ![Usuários do Access](./media/devtest-lab-add-devtest-user/access-users.png)
5. <span data-ttu-id="3d669-206">Em Olá **usuários** folha, selecione **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="3d669-206">On hello **Users** blade, select **Add**.</span></span>
   
    ![Adicionar usuário](./media/devtest-lab-add-devtest-user/devtest-users-blade.png)
6. <span data-ttu-id="3d669-208">Em Olá **selecionar uma função** folha, selecione **proprietário**.</span><span class="sxs-lookup"><span data-stu-id="3d669-208">On hello **Select a role** blade, select **Owner**.</span></span>
7. <span data-ttu-id="3d669-209">Em Olá **adicionar usuários** folha, insira o nome ou endereço de email de saudação do usuário Olá deseja tooadd como proprietário.</span><span class="sxs-lookup"><span data-stu-id="3d669-209">On hello **Add users** blade, enter hello email address or name of hello user you want tooadd as an owner.</span></span> <span data-ttu-id="3d669-210">Se o usuário Olá não for encontrado, você receberá uma mensagem de erro explicando o problema de saudação.</span><span class="sxs-lookup"><span data-stu-id="3d669-210">If hello user can't be found, you get an error message explaining hello issue.</span></span> <span data-ttu-id="3d669-211">Se o usuário Olá for encontrado, esse usuário será listado em Olá **usuário** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="3d669-211">If hello user is found, that user is listed under hello **User** text box.</span></span>
8. <span data-ttu-id="3d669-212">Selecione o nome do usuário localizada de saudação.</span><span class="sxs-lookup"><span data-stu-id="3d669-212">Select hello located user name.</span></span>
9. <span data-ttu-id="3d669-213">Selecione **Selecionar**.</span><span class="sxs-lookup"><span data-stu-id="3d669-213">Select **Select**.</span></span>
10. <span data-ttu-id="3d669-214">Selecione **Okey** tooclose Olá **adicionar acesso** folha.</span><span class="sxs-lookup"><span data-stu-id="3d669-214">Select **OK** tooclose hello **Add access** blade.</span></span>
11. <span data-ttu-id="3d669-215">Ao retornar toohello **usuários** folha, Olá usuário foi adicionado como um proprietário.</span><span class="sxs-lookup"><span data-stu-id="3d669-215">When you return toohello **Users** blade, hello user has been added as an owner.</span></span> <span data-ttu-id="3d669-216">Esse usuário é agora um proprietário de todos os laboratórios criados sob essa assinatura e, portanto, ser capaz de tooperform tarefas de proprietário.</span><span class="sxs-lookup"><span data-stu-id="3d669-216">This user is now an owner of any labs created under this subscription, and thus be able tooperform owner tasks.</span></span> 

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

