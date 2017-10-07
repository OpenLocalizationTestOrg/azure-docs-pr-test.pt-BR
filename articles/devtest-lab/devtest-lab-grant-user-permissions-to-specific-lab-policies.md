---
title: "políticas de laboratório aaaGrant usuário permissões toospecific | Microsoft Docs"
description: "Saiba como toogrant permissões toospecific laboratório as políticas de usuário no DevTest Labs com base nas necessidades de cada usuário"
services: devtest-lab,virtual-machines,visual-studio-online
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 5ca829f0-eb69-40a1-ae26-03a629db1d7e
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/25/2016
ms.author: tarcher
ms.openlocfilehash: 35647ab837243188f06566cdf365b67fe33a3865
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="grant-user-permissions-toospecific-lab-policies"></a><span data-ttu-id="18377-103">Conceder permissões de usuário toospecific políticas de laboratório</span><span class="sxs-lookup"><span data-stu-id="18377-103">Grant user permissions toospecific lab policies</span></span>
## <a name="overview"></a><span data-ttu-id="18377-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="18377-104">Overview</span></span>
<span data-ttu-id="18377-105">Este artigo ilustra como toouse política do PowerShell toogrant usuários permissões tooa laboratório específico.</span><span class="sxs-lookup"><span data-stu-id="18377-105">This article illustrates how toouse PowerShell toogrant users permissions tooa particular lab policy.</span></span> <span data-ttu-id="18377-106">Dessa forma, as permissões podem ser aplicadas com base nas necessidades de cada usuário.</span><span class="sxs-lookup"><span data-stu-id="18377-106">That way, permissions can be applied based on each user's needs.</span></span> <span data-ttu-id="18377-107">Por exemplo, convém toogrant um configurações de política específica de usuário Olá capacidade toochange Olá VM, mas não Olá custo políticas.</span><span class="sxs-lookup"><span data-stu-id="18377-107">For example, you might want toogrant a particular user hello ability toochange hello VM policy settings, but not hello cost policies.</span></span>

## <a name="policies-as-resources"></a><span data-ttu-id="18377-108">Políticas como recursos</span><span class="sxs-lookup"><span data-stu-id="18377-108">Policies as resources</span></span>
<span data-ttu-id="18377-109">Conforme discutido em Olá [controle de acesso baseado em função do Azure](../active-directory/role-based-access-control-configure.md) artigo, RBAC permite o gerenciamento de acesso refinado de recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="18377-109">As discussed in hello [Azure Role-based Access Control](../active-directory/role-based-access-control-configure.md) article, RBAC enables fine-grained access management of resources for Azure.</span></span> <span data-ttu-id="18377-110">Usando o RBAC, você pode separar as tarefas dentro de sua equipe de DevOps e conceder apenas Olá total acesso toousers que precisam tooperform seus trabalhos.</span><span class="sxs-lookup"><span data-stu-id="18377-110">Using RBAC, you can segregate duties within your DevOps team and grant only hello amount of access toousers that they need tooperform their jobs.</span></span>

<span data-ttu-id="18377-111">Em DevTest Labs, uma política é um tipo de recurso que permite que a ação de RBAC Olá **Microsoft.DevTestLab/labs/policySets/policies/**.</span><span class="sxs-lookup"><span data-stu-id="18377-111">In DevTest Labs, a policy is a resource type that enables hello RBAC action **Microsoft.DevTestLab/labs/policySets/policies/**.</span></span> <span data-ttu-id="18377-112">Cada política de laboratório é um recurso no tipo de recurso de política de saudação e pode ser atribuída como uma função RBAC tooan escopo.</span><span class="sxs-lookup"><span data-stu-id="18377-112">Each lab policy is a resource in hello Policy resource type, and can be assigned as a scope tooan RBAC role.</span></span>

<span data-ttu-id="18377-113">Por exemplo, em ordem toogrant usuários leitura/gravação permissão toohello **permitidos tamanhos de VM** política, você deve criar uma função personalizada que funciona com hello **Microsoft.DevTestLab/labs/policySets/policies/** * a ação e, em seguida, atribuir Olá usuários apropriados toothis função personalizada no escopo de saudação do **Microsoft.DevTestLab/labs/policySets/policies/AllowedVmSizesInLab**.</span><span class="sxs-lookup"><span data-stu-id="18377-113">For example, in order toogrant users read/write permission toohello **Allowed VM Sizes** policy, you would create a custom role that works with hello **Microsoft.DevTestLab/labs/policySets/policies/*** action, and then assign hello appropriate users toothis custom role in hello scope of **Microsoft.DevTestLab/labs/policySets/policies/AllowedVmSizesInLab**.</span></span>

<span data-ttu-id="18377-114">toolearn mais informações sobre funções personalizadas em RBAC, consulte Olá [funções personalizadas de controle de acesso](../active-directory/role-based-access-control-custom-roles.md).</span><span class="sxs-lookup"><span data-stu-id="18377-114">toolearn more about custom roles in RBAC, see hello [Custom roles access control](../active-directory/role-based-access-control-custom-roles.md).</span></span>

## <a name="creating-a-lab-custom-role-using-powershell"></a><span data-ttu-id="18377-115">Criar uma função personalizada do laboratório usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="18377-115">Creating a lab custom role using PowerShell</span></span>
<span data-ttu-id="18377-116">Em tooget ordem iniciado, você precisará Olá tooread artigo que explica a seguir como tooinstall e configurar os cmdlets do PowerShell do Azure Olá: [https://azure.microsoft.com/blog/azps-1-0-pre](https://azure.microsoft.com/blog/azps-1-0-pre).</span><span class="sxs-lookup"><span data-stu-id="18377-116">In order tooget started, you’ll need tooread hello following article, which will explain how tooinstall and configure hello Azure PowerShell cmdlets: [https://azure.microsoft.com/blog/azps-1-0-pre](https://azure.microsoft.com/blog/azps-1-0-pre).</span></span>

<span data-ttu-id="18377-117">Depois que você configurou Olá cmdlets do PowerShell do Azure, você pode executar Olá tarefas a seguir:</span><span class="sxs-lookup"><span data-stu-id="18377-117">Once you’ve set up hello Azure PowerShell cmdlets, you can perform hello following tasks:</span></span>

* <span data-ttu-id="18377-118">Lista todas as operações/ações Olá para um provedor de recursos</span><span class="sxs-lookup"><span data-stu-id="18377-118">List all hello operations/actions for a resource provider</span></span>
* <span data-ttu-id="18377-119">Listar ações em uma função específica:</span><span class="sxs-lookup"><span data-stu-id="18377-119">List actions in a particular role:</span></span>
* <span data-ttu-id="18377-120">Criar uma função personalizada</span><span class="sxs-lookup"><span data-stu-id="18377-120">Create a custom role</span></span>

<span data-ttu-id="18377-121">saudação de script do PowerShell a seguir mostra exemplos de como tooperform essas tarefas:</span><span class="sxs-lookup"><span data-stu-id="18377-121">hello following PowerShell script illustrates examples of how tooperform these tasks:</span></span>

    ‘List all hello operations/actions for a resource provider.
    Get-AzureRmProviderOperation -OperationSearchString "Microsoft.DevTestLab/*"

    ‘List actions in a particular role.
    (Get-AzureRmRoleDefinition "DevTest Labs User").Actions

    ‘Create custom role.
    $policyRoleDef = (Get-AzureRmRoleDefinition "DevTest Labs User")
    $policyRoleDef.Id = $null
    $policyRoleDef.Name = "Policy Contributor"
    $policyRoleDef.IsCustom = $true
    $policyRoleDef.AssignableScopes.Clear()
    $policyRoleDef.AssignableScopes.Add("/subscriptions/<SubscriptionID> ")
    $policyRoleDef.Actions.Add("Microsoft.DevTestLab/labs/policySets/policies/*")
    $policyRoleDef = (New-AzureRmRoleDefinition -Role $policyRoleDef)

## <a name="assigning-permissions-tooa-user-for-a-specific-policy-using-custom-roles"></a><span data-ttu-id="18377-122">Atribuir permissões tooa usuário para uma política específica usando funções personalizadas</span><span class="sxs-lookup"><span data-stu-id="18377-122">Assigning permissions tooa user for a specific policy using custom roles</span></span>
<span data-ttu-id="18377-123">Depois que você tiver definido suas funções personalizadas, você pode atribuí-los toousers.</span><span class="sxs-lookup"><span data-stu-id="18377-123">Once you’ve defined your custom roles, you can assign them toousers.</span></span> <span data-ttu-id="18377-124">Em ordem tooassign um usuário de tooa de função personalizada, você deve primeiro obter Olá **ObjectId** representar esse usuário.</span><span class="sxs-lookup"><span data-stu-id="18377-124">In order tooassign a custom role tooa user, you must first obtain hello **ObjectId** representing that user.</span></span> <span data-ttu-id="18377-125">toodo que use Olá **AzureRmADUser Get** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="18377-125">toodo that, use hello **Get-AzureRmADUser** cmdlet.</span></span>

<span data-ttu-id="18377-126">Em Olá exemplo a seguir, Olá **ObjectId** de saudação *SomeUser* usuário é 05DEFF7B-0AC3-4ABF-B74D-6A72CD5BF3F3.</span><span class="sxs-lookup"><span data-stu-id="18377-126">In hello following example, hello **ObjectId** of hello *SomeUser* user is 05DEFF7B-0AC3-4ABF-B74D-6A72CD5BF3F3.</span></span>

    PS C:\>Get-AzureRmADUser -SearchString "SomeUser"

    DisplayName                    Type                           ObjectId
    -----------                    ----                           --------
    someuser@hotmail.com                                          05DEFF7B-0AC3-4ABF-B74D-6A72CD5BF3F3

<span data-ttu-id="18377-127">Depois que você tiver Olá **ObjectId** para usuário hello e um nome de função personalizada, você pode atribuir usuário função toohello com hello **AzureRmRoleAssignment novo** cmdlet:</span><span class="sxs-lookup"><span data-stu-id="18377-127">Once you have hello **ObjectId** for hello user and a custom role name, you can assign that role toohello user with hello **New-AzureRmRoleAssignment** cmdlet:</span></span>

    PS C:\>New-AzureRmRoleAssignment -ObjectId 05DEFF7B-0AC3-4ABF-B74D-6A72CD5BF3F3 -RoleDefinitionName "Policy Contributor" -Scope /subscriptions/<SubscriptionID>/resourceGroups/<ResourceGroupName>/providers/Microsoft.DevTestLab/labs/<LabName>/policySets/policies/AllowedVmSizesInLab

<span data-ttu-id="18377-128">No exemplo anterior de saudação, Olá **AllowedVmSizesInLab** política é usada.</span><span class="sxs-lookup"><span data-stu-id="18377-128">In hello previous example, hello **AllowedVmSizesInLab** policy is used.</span></span> <span data-ttu-id="18377-129">Você pode usar qualquer um dos Olá políticas a seguir:</span><span class="sxs-lookup"><span data-stu-id="18377-129">You can use any of hello following polices:</span></span>

* <span data-ttu-id="18377-130">MaxVmsAllowedPerUser</span><span class="sxs-lookup"><span data-stu-id="18377-130">MaxVmsAllowedPerUser</span></span>
* <span data-ttu-id="18377-131">MaxVmsAllowedPerLab</span><span class="sxs-lookup"><span data-stu-id="18377-131">MaxVmsAllowedPerLab</span></span>
* <span data-ttu-id="18377-132">AllowedVmSizesInLab</span><span class="sxs-lookup"><span data-stu-id="18377-132">AllowedVmSizesInLab</span></span>
* <span data-ttu-id="18377-133">LabVmsShutdown</span><span class="sxs-lookup"><span data-stu-id="18377-133">LabVmsShutdown</span></span>

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="next-steps"></a><span data-ttu-id="18377-134">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="18377-134">Next steps</span></span>
<span data-ttu-id="18377-135">Uma vez você concedeu políticas de laboratório de toospecific de permissões de usuário, aqui estão alguns próxima tooconsider de etapas:</span><span class="sxs-lookup"><span data-stu-id="18377-135">Once you've granted user permissions toospecific lab policies, here are some next steps tooconsider:</span></span>

* <span data-ttu-id="18377-136">[Laboratório de tooa acesso seguro](devtest-lab-add-devtest-user.md).</span><span class="sxs-lookup"><span data-stu-id="18377-136">[Secure access tooa lab](devtest-lab-add-devtest-user.md).</span></span>
* <span data-ttu-id="18377-137">[Definir políticas de laboratório](devtest-lab-set-lab-policy.md).</span><span class="sxs-lookup"><span data-stu-id="18377-137">[Set lab policies](devtest-lab-set-lab-policy.md).</span></span>
* <span data-ttu-id="18377-138">[Criar um modelo de laboratório](devtest-lab-create-template.md).</span><span class="sxs-lookup"><span data-stu-id="18377-138">[Create a lab template](devtest-lab-create-template.md).</span></span>
* <span data-ttu-id="18377-139">[Criar artefatos personalizados para suas VMs](devtest-lab-artifact-author.md).</span><span class="sxs-lookup"><span data-stu-id="18377-139">[Create custom artifacts for your VMs](devtest-lab-artifact-author.md).</span></span>
* <span data-ttu-id="18377-140">[Adicionar uma VM com o laboratório de tooa artefatos](devtest-lab-add-vm-with-artifacts.md).</span><span class="sxs-lookup"><span data-stu-id="18377-140">[Add a VM with artifacts tooa lab](devtest-lab-add-vm-with-artifacts.md).</span></span>

