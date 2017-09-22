---
title: "Conceder permissões de usuário para políticas específicas do laboratório | Microsoft Docs"
description: "Saiba como conceder permissões de usuário para políticas específicas dos Laboratórios de Desenvolvimento/Teste com base nas necessidades de cada usuário"
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
ms.openlocfilehash: 0bd9f83257834d9681479ba9117c48ffd6d6e166
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="grant-user-permissions-to-specific-lab-policies"></a><span data-ttu-id="2b021-103">Conceder permissões de usuário para políticas específicas do laboratório</span><span class="sxs-lookup"><span data-stu-id="2b021-103">Grant user permissions to specific lab policies</span></span>
## <a name="overview"></a><span data-ttu-id="2b021-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="2b021-104">Overview</span></span>
<span data-ttu-id="2b021-105">Este artigo ilustra como usar o PowerShell para conceder aos usuários permissões para uma determinada política de laboratório.</span><span class="sxs-lookup"><span data-stu-id="2b021-105">This article illustrates how to use PowerShell to grant users permissions to a particular lab policy.</span></span> <span data-ttu-id="2b021-106">Dessa forma, as permissões podem ser aplicadas com base nas necessidades de cada usuário.</span><span class="sxs-lookup"><span data-stu-id="2b021-106">That way, permissions can be applied based on each user's needs.</span></span> <span data-ttu-id="2b021-107">Por exemplo, talvez você queira conceder a um usuário específico a capacidade de alterar as configurações de política de VM, mas não as políticas de custo.</span><span class="sxs-lookup"><span data-stu-id="2b021-107">For example, you might want to grant a particular user the ability to change the VM policy settings, but not the cost policies.</span></span>

## <a name="policies-as-resources"></a><span data-ttu-id="2b021-108">Políticas como recursos</span><span class="sxs-lookup"><span data-stu-id="2b021-108">Policies as resources</span></span>
<span data-ttu-id="2b021-109">Como discutido no artigo [Controle de acesso baseado em função do Azure](../active-directory/role-based-access-control-configure.md) , o RBAC permite o gerenciamento de acesso refinado de recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="2b021-109">As discussed in the [Azure Role-based Access Control](../active-directory/role-based-access-control-configure.md) article, RBAC enables fine-grained access management of resources for Azure.</span></span> <span data-ttu-id="2b021-110">Com o RBAC, você pode separar as tarefas dentro de sua equipe de operação de desenvolvimento e conceder somente a quantidade de acesso que os usuários precisam para realizar seus trabalhos.</span><span class="sxs-lookup"><span data-stu-id="2b021-110">Using RBAC, you can segregate duties within your DevOps team and grant only the amount of access to users that they need to perform their jobs.</span></span>

<span data-ttu-id="2b021-111">Nos Laboratórios de Desenvolvimento/Teste, uma política é um tipo de recurso que habilita a ação de RBAC **Microsoft.DevTestLab/labs/policySets/policies/**.</span><span class="sxs-lookup"><span data-stu-id="2b021-111">In DevTest Labs, a policy is a resource type that enables the RBAC action **Microsoft.DevTestLab/labs/policySets/policies/**.</span></span> <span data-ttu-id="2b021-112">Cada política do laboratório é um recurso do tipo de recurso Política e pode ser atribuída como um escopo a uma função RBAC.</span><span class="sxs-lookup"><span data-stu-id="2b021-112">Each lab policy is a resource in the Policy resource type, and can be assigned as a scope to an RBAC role.</span></span>

<span data-ttu-id="2b021-113">Por exemplo, para conceder permissão de leitura/gravação de usuários para o **permitidos tamanhos de VM** política, você deve criar uma função personalizada que funciona com o **Microsoft.DevTestLab/labs/policySets/policies/*** ação e, em seguida, atribuir usuários adequados para esta função personalizada no escopo do **Microsoft.DevTestLab/labs/policySets/policies/AllowedVmSizesInLab**.</span><span class="sxs-lookup"><span data-stu-id="2b021-113">For example, in order to grant users read/write permission to the **Allowed VM Sizes** policy, you would create a custom role that works with the **Microsoft.DevTestLab/labs/policySets/policies/*** action, and then assign the appropriate users to this custom role in the scope of **Microsoft.DevTestLab/labs/policySets/policies/AllowedVmSizesInLab**.</span></span>

<span data-ttu-id="2b021-114">Para saber mais sobre as funções personalizadas no RBAC, consulte o [Controle de acesso das funções personalizadas](../active-directory/role-based-access-control-custom-roles.md).</span><span class="sxs-lookup"><span data-stu-id="2b021-114">To learn more about custom roles in RBAC, see the [Custom roles access control](../active-directory/role-based-access-control-custom-roles.md).</span></span>

## <a name="creating-a-lab-custom-role-using-powershell"></a><span data-ttu-id="2b021-115">Criar uma função personalizada do laboratório usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="2b021-115">Creating a lab custom role using PowerShell</span></span>
<span data-ttu-id="2b021-116">Para começar, você precisará ler o seguinte artigo, que explica como instalar e configurar os cmdlets do Azure PowerShell: [https://azure.microsoft.com/blog/azps-1-0-pre](https://azure.microsoft.com/blog/azps-1-0-pre).</span><span class="sxs-lookup"><span data-stu-id="2b021-116">In order to get started, you’ll need to read the following article, which will explain how to install and configure the Azure PowerShell cmdlets: [https://azure.microsoft.com/blog/azps-1-0-pre](https://azure.microsoft.com/blog/azps-1-0-pre).</span></span>

<span data-ttu-id="2b021-117">Depois de configurar os cmdlets do Azure PowerShell, você pode executar as seguintes tarefas:</span><span class="sxs-lookup"><span data-stu-id="2b021-117">Once you’ve set up the Azure PowerShell cmdlets, you can perform the following tasks:</span></span>

* <span data-ttu-id="2b021-118">Listar todas as operações/ações para um provedor de recursos</span><span class="sxs-lookup"><span data-stu-id="2b021-118">List all the operations/actions for a resource provider</span></span>
* <span data-ttu-id="2b021-119">Listar ações em uma função específica:</span><span class="sxs-lookup"><span data-stu-id="2b021-119">List actions in a particular role:</span></span>
* <span data-ttu-id="2b021-120">Criar uma função personalizada</span><span class="sxs-lookup"><span data-stu-id="2b021-120">Create a custom role</span></span>

<span data-ttu-id="2b021-121">O seguinte script do PowerShell apresenta exemplos de como executar essas tarefas:</span><span class="sxs-lookup"><span data-stu-id="2b021-121">The following PowerShell script illustrates examples of how to perform these tasks:</span></span>

    ‘List all the operations/actions for a resource provider.
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

## <a name="assigning-permissions-to-a-user-for-a-specific-policy-using-custom-roles"></a><span data-ttu-id="2b021-122">Atribuir permissões a um usuário para uma política específica usando funções personalizadas</span><span class="sxs-lookup"><span data-stu-id="2b021-122">Assigning permissions to a user for a specific policy using custom roles</span></span>
<span data-ttu-id="2b021-123">Depois de definir suas funções personalizadas, você pode atribuí-las aos usuários.</span><span class="sxs-lookup"><span data-stu-id="2b021-123">Once you’ve defined your custom roles, you can assign them to users.</span></span> <span data-ttu-id="2b021-124">Para atribuir uma função personalizada a um usuário, você deve primeiro obter o **ObjectId** que representa esse usuário.</span><span class="sxs-lookup"><span data-stu-id="2b021-124">In order to assign a custom role to a user, you must first obtain the **ObjectId** representing that user.</span></span> <span data-ttu-id="2b021-125">Para fazer isso, use o cmdlet **Get-AzureRmADUser** .</span><span class="sxs-lookup"><span data-stu-id="2b021-125">To do that, use the **Get-AzureRmADUser** cmdlet.</span></span>

<span data-ttu-id="2b021-126">No exemplo a seguir, o **ObjectId** do usuário *SomeUser* é 05DEFF7B-0AC3-4ABF-B74D-6A72CD5BF3F3.</span><span class="sxs-lookup"><span data-stu-id="2b021-126">In the following example, the **ObjectId** of the *SomeUser* user is 05DEFF7B-0AC3-4ABF-B74D-6A72CD5BF3F3.</span></span>

    PS C:\>Get-AzureRmADUser -SearchString "SomeUser"

    DisplayName                    Type                           ObjectId
    -----------                    ----                           --------
    someuser@hotmail.com                                          05DEFF7B-0AC3-4ABF-B74D-6A72CD5BF3F3

<span data-ttu-id="2b021-127">Depois de você ter o **ObjectId** para o usuário e um nome de função personalizado, poderá atribuir essa função ao usuário com o cmdlet **New-AzureRmRoleAssignment**:</span><span class="sxs-lookup"><span data-stu-id="2b021-127">Once you have the **ObjectId** for the user and a custom role name, you can assign that role to the user with the **New-AzureRmRoleAssignment** cmdlet:</span></span>

    PS C:\>New-AzureRmRoleAssignment -ObjectId 05DEFF7B-0AC3-4ABF-B74D-6A72CD5BF3F3 -RoleDefinitionName "Policy Contributor" -Scope /subscriptions/<SubscriptionID>/resourceGroups/<ResourceGroupName>/providers/Microsoft.DevTestLab/labs/<LabName>/policySets/policies/AllowedVmSizesInLab

<span data-ttu-id="2b021-128">No exemplo anterior, a política **AllowedVmSizesInLab** é usada.</span><span class="sxs-lookup"><span data-stu-id="2b021-128">In the previous example, the **AllowedVmSizesInLab** policy is used.</span></span> <span data-ttu-id="2b021-129">Você pode usar qualquer uma das políticas a seguir:</span><span class="sxs-lookup"><span data-stu-id="2b021-129">You can use any of the following polices:</span></span>

* <span data-ttu-id="2b021-130">MaxVmsAllowedPerUser</span><span class="sxs-lookup"><span data-stu-id="2b021-130">MaxVmsAllowedPerUser</span></span>
* <span data-ttu-id="2b021-131">MaxVmsAllowedPerLab</span><span class="sxs-lookup"><span data-stu-id="2b021-131">MaxVmsAllowedPerLab</span></span>
* <span data-ttu-id="2b021-132">AllowedVmSizesInLab</span><span class="sxs-lookup"><span data-stu-id="2b021-132">AllowedVmSizesInLab</span></span>
* <span data-ttu-id="2b021-133">LabVmsShutdown</span><span class="sxs-lookup"><span data-stu-id="2b021-133">LabVmsShutdown</span></span>

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="next-steps"></a><span data-ttu-id="2b021-134">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="2b021-134">Next steps</span></span>
<span data-ttu-id="2b021-135">Após você tiver concedido permissões de usuário para políticas específicas do laboratório, estas são algumas das próximas etapas a serem consideradas:</span><span class="sxs-lookup"><span data-stu-id="2b021-135">Once you've granted user permissions to specific lab policies, here are some next steps to consider:</span></span>

* <span data-ttu-id="2b021-136">[Proteger o acesso a um laboratório](devtest-lab-add-devtest-user.md).</span><span class="sxs-lookup"><span data-stu-id="2b021-136">[Secure access to a lab](devtest-lab-add-devtest-user.md).</span></span>
* <span data-ttu-id="2b021-137">[Definir políticas de laboratório](devtest-lab-set-lab-policy.md).</span><span class="sxs-lookup"><span data-stu-id="2b021-137">[Set lab policies](devtest-lab-set-lab-policy.md).</span></span>
* <span data-ttu-id="2b021-138">[Criar um modelo de laboratório](devtest-lab-create-template.md).</span><span class="sxs-lookup"><span data-stu-id="2b021-138">[Create a lab template](devtest-lab-create-template.md).</span></span>
* <span data-ttu-id="2b021-139">[Criar artefatos personalizados para suas VMs](devtest-lab-artifact-author.md).</span><span class="sxs-lookup"><span data-stu-id="2b021-139">[Create custom artifacts for your VMs](devtest-lab-artifact-author.md).</span></span>
* <span data-ttu-id="2b021-140">[Adicionar uma VM com artefatos a um laboratório](devtest-lab-add-vm-with-artifacts.md).</span><span class="sxs-lookup"><span data-stu-id="2b021-140">[Add a VM with artifacts to a lab](devtest-lab-add-vm-with-artifacts.md).</span></span>

